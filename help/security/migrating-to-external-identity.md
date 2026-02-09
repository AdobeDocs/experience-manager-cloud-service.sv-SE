---
title: Migrering till extern identitet och dynamiskt gruppmedlemskap
description: Teknisk guide för migrering av lokala användare och grupper till en extern identitetsmodell med dynamiskt gruppmedlemskap i AEM as a Cloud Service
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: bb4b60523f60b1285c5f2fd2e49f6cc8cff24324
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# Migrering till extern identitet och dynamiskt gruppmedlemskap {#migrating-to-external-identity}

## Ökning {#overview}

När [Datasynkronisering](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization) har aktiverats i AEM as a Cloud Service kan SAML-autentiseringshanteraren konfigureras så att den automatiskt migrerar till externa identiteter med dynamiskt gruppmedlemskap när den hanterar skapad av användare och grupper. Om ditt projekt använder anpassad kod för att skapa användare eller grupper måste du uppdatera den för att skapa externa användare och grupper, till skillnad från lokala användare och grupper.

### Därför krävs externa användare och grupper {#why-external-required}

Att migrera från lokala användare och grupper till externa identiteter med dynamiskt gruppmedlemskap är nödvändigt av flera viktiga skäl:

**Prestandaoptimering:**

* **Minskade databasskrivningar**: Traditionellt lokalt gruppmedlemskap kräver att du skriver medlemsrelationer till databasen i en flervärdesegenskap för gruppnoden. Med dynamiskt gruppmedlemskap har användarna en enda `rep:externalPrincipalNames`-egenskap som innehåller alla grupprinciper, vilket eliminerar behovet av att synkronisera gruppnoden
* **Snabbare synkronisering**: När användare synkroniseras över publiceringsskiktsnoder kräver externa användare med dynamiskt gruppmedlemskap betydligt mindre dataöverföring och färre skrivåtgärder jämfört med lokala användare med traditionella gruppmedlemskap
* **Skalbarhet**: System med ett stort antal användare och grupper drar dramatiskt nytta av minskade databaskostnader. Dynamiskt gruppmedlemskap kan skalas effektivt även med mycket stora grupper.

Detta dokument innehåller teknisk vägledning för

* Förstå den externa identitetsmodellen
* Ändra anpassad kod för att skapa externa användare och grupper
* Migrera befintliga lokala användare och grupper till den externa identitetsmodellen

## Extern identitet {#understanding-external-identity}

### Externa användare {#external-users}

Externa användare identifieras av egenskapen `rep:externalId` som länkar användaren till en extern identitetsleverantör. Formatet är

```
userId;idpName
```

Till exempel: `john.doe;saml-idp`.

>[!NOTE]
>
> `idpName` refererar till namnet på Oak Identity Provider (IDP) enligt definitionen i konfigurationen för Autentiseringshanteraren. För SAML-integreringar är detta det värde som angetts för attributet `idpIdentifier` i SAML Authentication Handler.

**Nyckelegenskaper:**

* `rep:externalId`: Obligatorisk egenskap som anger en användare som extern (t.ex. `john.doe;saml-idp`)
* `rep:externalPrincipalNames`: Flervärdesegenskap som innehåller externa gruppobjekt för dynamiskt medlemskap
* `rep:lastSynced`: Tidsstämpel för den senaste synkroniseringen
* `rep:lastDynamicSync`: Tidsstämpel för den senaste synkroniseringen av dynamiskt gruppmedlemskap

### Externa grupper {#external-groups}

Externa grupper identifieras också av egenskapen `rep:externalId` och använder ett huvudnamnsformat:

```
groupId;idpName
```

Till exempel: `content-authors;saml-idp`

### Dynamiskt gruppmedlemskap {#dynamic-group-membership}

I stället för att direktsända relationer mellan användare och grupper lagras i databasen, används egenskapen `rep:externalPrincipalNames` på användarnoden för dynamiskt gruppmedlemskap. När en användare har ett externt huvudnamn som matchar en extern grupps ID blir de automatiskt medlem i den gruppen. Mer information finns i [dokumentationen för Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html).

**Fördelar:**

* Minskade databasskrivningar (inga noder för gruppmedlemskap ändras när användare läggs till/tas bort från grupper)
* Snabbare synkronisering över publiceringsskiktsnoder
* Skalbar hantering av gruppmedlemskap
* Kompatibel med datasynkroniseringskrav

## Tjänstanvändarkonfiguration {#service-user-configuration}

Alla åtgärder som skapar eller ändrar externa användare och grupper ska utföras med en **tjänstanvändare** som är korrekt konfigurerad att kringgå standardskyddet för egenskaperna `rep:externalId` och `rep:externalPrincipalNames`.

### Varför krävs en tjänstanvändare {#why-is-a-service-user-required}

Som standard förhindrar Oak-säkerhet att vanliga sessioner ändrar skyddade egenskaper som:

* `rep:externalId` - Markerar användare/grupper som externa
* `rep:externalPrincipalNames` - Lagrar principer för dynamiskt gruppmedlemskap

Endast en korrekt konfigurerad tjänstanvändare kan ändra dessa egenskaper.

### Konfiguration och mappning av tjänstanvändare {#service-user-configuration-mapping}

Det krävs tre koordinerade konfigurationer för att konfigurera en tjänstanvändare för att hantera externa identiteter:

1. Skapa tjänstanvändaren via `repoinit`
2. Konfigurera `ExternalPrincipal`-skydd
3. Koppla tjänstanvändaren till ditt programpaket.

Nedan finns en omfattande beskrivning av dessa steg.

#### Steg 1: Skapa tjänstanvändaren via Påpeka {#create-the-serviice-user-via-repoinit}

I det här steget beskrivs hur du skapar tjänstanvändaren med nödvändig behörighet med hjälp av ett `repoinit`-skript.

**Konfigurationsfil:** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**Exemplarplats:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**Behörighetsöversikt**

* `jcr:read`: Läs användare och grupper
* `jcr:readAccessControl`: Läs ACL:er
* `jcr:modifyAccessControl`: Ändra åtkomstkontrollistor (krävs för att ange egenskaper)
* `rep:userManagement`: Skapa och hantera användare/grupper
* `rep:write`: Skriv egenskaper som `rep:externalId` och `rep:externalPrincipalNames`

>[!NOTE]
>
>Tjänstanvändaren skapas under `/home/users/system/yourproject` för att hålla den organiserad med andra systemanvändare.

#### Steg 2: Konfigurera ExternalPrincipal Protection {#configure-externalprincipal-protection}

Nedan visas ett exempel på konfiguration för vitlistning av tjänstanvändaren så att den kan kringgå skyddet som tillämpas på externa identitetsegenskaper.

**Konfigurationsfilens namn:** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**Exempelplats:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**Konfigurationsegenskaper:**

* `protectExternalIdentities`: Kontrollerar skyddsnivån för externa identitetsegenskaper:
   * `"Strict"`: Endast systemobjekt i vitlistan kan ändra externa egenskaper. Detta är den rekommenderade nivån för produktion.
   * `"Warn"`: Loggar varningar men tillåter ändringar. Användbar för utveckling/testning.
   * `"None"`: Inget skydd. Rekommenderas inte.
* `systemPrincipalNames`: Lista med tjänstanvändarnamn som får ändra `rep:externalId` och `rep:externalPrincipalNames`. Inkludera alla tjänstanvändare som behöver hantera externa identiteter (t.ex. `group-provisioner`, `saml-migration-service`).

>[!IMPORTANT]
>
>Tjänstanvändarnamnen i `systemPrincipalNames` måste exakt matcha tjänstanvändar-ID:n som skapats i pekskriptet.

#### Steg 3: Mappning av tjänstanvändare {#service-user-mapping}

Koppla tjänstanvändaren till ditt programpaket så att koden kan använda det.

**Konfigurationsfil:** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**Plats:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**Mappningsformat:**

* `yourproject.core`: Det symboliska paketnamnet (finns i `pom.xml` `<Bundle-SymbolicName>`)
* `group-provisioner` (före `=`): Undertjänstnamnet som du använder i koden
* `[group-provisioner]` (efter `=`): Det faktiska användar-ID för tjänsten som skapades i referenspunkten

### Använda tjänstanvändaren i koden {#using-the-service-user-in-code}

När du öppnar en session för att utföra migrerings- eller användar-/gruppskapande åtgärder måste du använda tjänstanvändaren:

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>Om tjänstens användarkonfiguration inte är korrekt misslyckas försök att ange `rep:externalId` eller `rep:externalPrincipalNames` med behörighetsfel. Kontrollera att tjänstanvändaren är korrekt konfigurerad i `ExternalPrincipal`-konfigurationen innan du försöker migrera.

## Exempel på fullständig konfiguration {#complete-configuration-example}

Här nedan hittar du ett komplett fungerande exempel som visar alla tre konfigurationerna tillsammans:

### Filstruktur {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### Ändra anpassad kod {#modifying-custom-code}

#### Skapa externa användare {#creating-external-users}

**Före (lokal användare):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**Efter (extern användare):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### Skapa externa grupper {#creating-external-groups}

**Före (lokal grupp):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**Efter (extern grupp):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### Tilldela dynamiskt gruppmedlemskap {#assigning-dynamic-membership}

**Före (direktmedlemskap):**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**Efter (dynamiskt medlemskap):**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## Migreringsprocess {#migration-process}

Befintliga lokala användare och grupper behöver inte migreras till den externa identiteten när den anpassade koden har uppdaterats innan datasynkroniseringstjänsterna aktiveras.

Om lokala användare och grupper redan har befunnits befinna sig i databasen och miljön används aktivt, rekommenderar vi att du utför en migrering i flera steg som följande för att undvika avbrott eller inkonsekvenser.

>[!IMPORTANT]
>
>Alla migreringssteg måste utföras med en korrekt konfigurerad tjänstanvändare (till exempel `group-provisioner`) som har beviljats behörighet att kringgå skyddet för `rep:externalId`- och `rep:externalPrincipalNames`-egenskaper. Mer information finns i [Tjänstanvändarkonfiguration](#service-user-configuration).

### Steg 1: Skapa extern gruppstruktur {#step-1-create-external-group-structure}

För varje lokal grupp som behöver migreras:

1. Skapa en motsvarande extern grupp med huvudnamn: `<localGroupId>;<idpName>`. Använd en namnkonvention som hjälper till att länka externa grupper till lokala grupper
1. Ange egenskapen `rep:externalId` för den externa gruppen med värden: `<localGroupId>;<idpName>`
1. Lägg till den externa gruppen som medlem i den ursprungliga lokala gruppen.

**Validering**

* Du kan validera resultaten genom att kontrollera om alla lokala grupper har en motsvarande extern grupp. Dessutom är varje extern grupp medlem i motsvarande lokal grupp.

**Exempel på serverslutpunkt:**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**Användning:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### Steg 2: Konvertera användare och tilldela dynamiskt medlemskap {#step-2-convert-users-and-assign-dynamic-membership}

För varje användare som är medlem i en lokal grupp:

1. Kontrollera att `rep:externalId` har angetts (konvertera till extern användare om det behövs).
1. Lägg till motsvarande externt gruppobjekt i `rep:externalPrincipalNames` för varje gruppmedlemskap
1. Uppdatera synkroniseringstidsstämplar.

>[!IMPORTANT]
>
>Hoppa över systemgrupper som &quot;alla&quot; under den här processen.

**Exempel på serverslutpunkt:**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**Användning:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**Validering**

Du kan validera detta genom att kontrollera att alla användare har attributen `rep:externalId` och `rep:externalPrincipalName` med `principalName` för varje extern grupp. Användarna är medlemmar i de lokala grupperna *och* i de externa grupperna.

### Steg 3: Ta bort medlemskap för direktanvändare {#step-3-remove-direct-user-memberships}

När användare har konfigurerat dynamiskt gruppmedlemskap:

1. Ta bort direkta användarmedlemskap från lokala grupper
1. Behåll grupp-till-grupp-medlemskap (inklusive externt gruppmedlemskap)

**Exempel på serverslutpunkt:**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**Användning:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**Validering**

* Du kan validera detta genom att kontrollera att varje lokal grupp endast har motsvarande externa grupp, eller andra grupper, som medlem.


## Arbetsflöde för migrering {#migration-workflow}

### Checklista före migrering {#pre-migration-checklist}

* [ ] **Konfigurera tjänstanvändare**: Skapa och konfigurera tjänstanvändaren (till exempel `group-provisioner`) med rätt behörigheter
* [ ] **Verifiera ExternalPrincipal Configuration**: Kontrollera att tjänstanvändaren har konfigurerats att kringgå skyddet på `rep:externalId` och `rep:externalPrincipalNames`
* [ ] **Testa tjänstens användarbehörigheter**: Verifiera att tjänstanvändaren kan ange externa identitetsegenskaper under utvecklingen
* [ ] Identifiera all anpassad kod som skapar användare eller grupper
* [ ] Granska och uppdatera anpassad kod för att använda en extern identitetsmodell
* [ ] Testa uppdaterad kod i utvecklingsmiljön
* [ ] Inventera alla befintliga lokala användare och grupper att migrera
* [ ] Testa migreringsprocessen i lägre miljöer

### Körningssteg {#execution-steps}

1. **Distribuera uppdaterad kod**: Distribuera anpassade kodändringar för att skapa externa användare/grupper

1. **Skapa externa grupper** (för varje lokal grupp):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **Migrera användare** (för varje användare):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **Rensa** (för varje migrerad grupp):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **Verifiera**: Kontrollera användargruppsmedlemskap och testa åtkomstbehörigheter

1. **Aktivera datasynkronisering**: Kontakta kundsupport om du vill aktivera funktionen

### Validering efter migrering {#post-migration-validation}

Verifiera migreringen:

1. **Kontrollera användaregenskaper**:

   På användarnoder verifieras närvaro av:

   * `rep:externalId`: Formatet ska vara `userId;idpName`
   * `rep:externalPrincipalNames`: Array med grupprincipobjekt i formatet `groupId;idpName`
   * `rep:lastSynced`: Tidsstämpeln är inställd på långt framöver (ungefär 10 år från migreringsdatumet)
   * `rep:lastDynamicSync`: Tidsstämpeln är inställd på långt framöver (ungefär 10 år från migreringsdatumet)

   **Obs!**: Tidsstämplarna anges avsiktligt till ett långt framtida datum som en tillfällig lösning för OAK-12079. Detta är förväntat beteende.

1. **Kontrollera gruppegenskaper**:

   På lokala gruppnoder verifieras närvaro av:

   * Extern gruppmedlem med formatet `groupId;idpName`
   * Inga direkta användarmedlemmar (endast efter steg 3)

1. **Testa användarinloggning**: Verifiera att användare kan logga in och ha rätt behörigheter

1. **Testa åtkomstkontroll**: Verifiera att användare kan komma åt innehåll som skyddas av CUG/ACL

## Felsökning {#troubleshooting}

### Vanliga problem {#common-issues}

**Problem: Behörighetsfel vid inställning av `rep:externalId` eller`rep:externalPrincipalNames`**

**Felmeddelanden:**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**Lösning**: Sessionen måste öppnas med en korrekt konfigurerad tjänstanvändare som har beviljats behörighet att kringgå skyddet för externa identitetsegenskaper.

**Steg som ska lösas:**

1. **Kontrollera att tjänstanvändaren finns**: Kontrollera att tjänstanvändaren (t.ex. `group-provisioner`) har skapats via repoinit
1. **Kontrollera tjänstanvändarmappning**: Verifiera att servern eller tjänsten använder `repository.loginService("group-provisioner", null)`
1. **Verifiera ExternalPrincipal-konfiguration**: Kontrollera att `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration` är korrekt konfigurerat
1. **Kontrollera användarbehörigheter för tjänsten**: Tjänstanvändaren behöver `rep:write` och `rep:userManagement` behörigheter för `/home/users` och `/home/groups`

Se [Tjänstanvändarkonfiguration](#service-user-configuration) för fullständiga installationsanvisningar.

**Utgåva:`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**Lösning**: Användarna måste ha `rep:externalId` inställt innan `rep:externalPrincipalNames` anges. Kontrollera att steg 2 först konverterar användare till externa användare.

**Problem: Användare förlorar gruppmedlemskap efter migrering**

**Lösning**: Verifiera att:

* Den externa gruppen skapades med korrekt huvudnamnsformat (`groupId;idpName`)
* Den externa gruppen lades till som medlem i den lokala gruppen (steg 1)
* Användaren har rätt externa huvudnamn i `rep:externalPrincipalNames` (steg 2)
* Steg 3-rensning utfördes först när steg 1 och 2 slutfördes

**Problem: Externa gruppmedlemskap tas oväntat bort efter användarinloggning (OAK-12079)**

**Problem**: På grund av Oak-fel [OAK-12079](https://issues.apache.org/jira/browse/OAK-12079) kan Oak-synkroniseringsfunktionen på ett tidigt sätt rensa upp externa gruppmedlemskap baserat på tidsstämplarna `rep:lastSynced` och `rep:lastDynamicSync`.

**Lösning**: Ange `rep:lastSynced` och `rep:lastDynamicSync` tidsstämplar till ett långt framtida datum (10 år från och med nu) i stället för den aktuella tiden. Detta förhindrar att rensningsprocessen för synkronisering tar bort externa gruppmedlemskap.

**Implementering:**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**Varför detta fungerar**: Genom att ställa in tidsstämplarna till ett långt framtida datum hanterar Oak synkroniseringslogik de här användarna som&quot;nyligen synkroniserade&quot; och utlöser inte rensningsprocessen som skulle ta bort de externa huvudnamnen och gruppmedlemskapen.

**Obs!** Det här är en tillfällig lösning tills OAK-12079 har lösts i en framtida version av Oak. Alla kodexempel i det här dokumentet innehåller redan den här lösningen.

**Problem: Systemgruppen &quot;alla&quot; orsakar fel**

**Lösning**: Hoppa alltid över systemgruppen Alla under användarmigrering (steg 2). Den här gruppen hanteras automatiskt av AEM.

### Återställningsprocedur {#rollback-procedure}

Om migreringen stöter på problem:

1. Stoppa migreringsprocessen
1. Återställ från säkerhetskopia om viktiga data påverkades
1. Återställ ändringarna av koden för att skapa externa användare och grupper med dynamiskt gruppmedlemskap
1. Granska och åtgärda problem innan du försöker migrera igen.

## Bästa praxis {#best-practices}

* **Testa noggrant**: Testa alltid migrering i utvecklings- och mellanlagringsmiljöer före produktion
* **Gruppbearbetning**: För stora användarbaser bör du bearbeta migreringar i grupper för att undvika timeoutproblem
* **Övervaka prestanda**: Övervaka databasprestanda under migrering
* **Underhåll granskningsspår**: Logga alla migreringsåtgärder för felsökning
* **Tjänstens användarbehörigheter**: Se till att flyttservrarna använder lämpliga tjänstanvändare med nödvändig behörighet. Tjänstanvändaren måste konfigureras i konfigurationen ExternalPrincipal för att kringgå skyddet för egenskaperna `rep:externalId` och `rep:externalPrincipalNames`
* **Idempotenta åtgärder**: Designmigreringskoden ska kunna köras igen
* **Validera vid varje steg**: Kontrollera resultatet efter varje migreringssteg innan du fortsätter

## Skydda migreringsservrar {#securing-migration-servlets}

Migreringsservletarna har utökad behörighet för att skapa och ändra användare och grupper. Det är viktigt att begränsa åtkomsten till dessa slutpunkter för att förhindra obehörig åtkomst.

### Rekommenderad metod: IMS-autentisering av tekniskt konto {#recommended-approach-ims-technical-account}

Vi rekommenderar att du skyddar dessa serverlets med hjälp av Adobe IMS-integration, så att endast ett behörigt tekniskt konto kan komma åt dem.

#### Steg 1: Skapa ett tekniskt konto i AEM Developer Console {#create-a-technical-account-in-aem-developer-console}

1. Navigera till [Experience Manager](https://experience.adobe.com/) och sedan till **Cloud Manager**
1. Välj program och klicka sedan på den miljö där du vill skapa det tekniska kontot
1. Klicka på **Developer Console** i miljöns ellipsmeny
1. Gå till fliken **Integrationer** i AEM Developer Console
1. Klicka på **Skapa nytt tekniskt konto**
1. Ange ett namn för integreringen (t.ex. &quot;Migreringstjänstkonto&quot;)
1. Klicka på **Skapa**
1. Observera följande värden från den skapade integreringen:
   * **Klient-ID**
   * **Klienthemlighet**
   * **ID för tekniskt konto** (detta blir det användar-ID som får åtkomst till dina servlets - format: `XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`)

Mer information finns i [Skapa åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

Exempelkod för att kontrollera om anroparen är auktoriserad:

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### Djupförsvar: IP-baserade restriktioner {#defense-in-depth-ip-based-restrictions}

Som ett extra säkerhetslager kan du konfigurera CDN-regler för att begränsa åtkomst till migreringsslutpunkter via IP-adress. Detta är användbart när migreringar körs från en känd infrastruktur.

>[!NOTE]
>
>Endast IP-begränsningar räcker inte. Kombinera alltid med autentiseringskontroller enligt beskrivningen ovan.

### Säkerhetschecklista {#security-checklist}

Innan du distribuerar migreringsservrar till produktion:

* [ ] Skapa IMS-integrering i AEM Developer Console
* [ ] Konfigurera servlets för att verifiera det tekniska konto-ID:t
* [ ] Testa autentiseringsflödet i utvecklings-/mellanlagringsmiljöer
* [ ] Överväg ytterligare IP-baserade begränsningar på CDN-nivå
* [ ] planerar att inaktivera eller ta bort migreringsservrar när migreringen är klar
* [ ] Granska och logga all åtkomst till migreringsslutpunkter

>[!IMPORTANT]
>
>När migreringen är klar bör du inaktivera eller ta bort migreringsservrarna från distributionen för att undvika eventuella säkerhetsrisker.

## Ytterligare resurser {#additional-resources}

* [Användar- och gruppsynkronisering för publiceringsnivå](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [SAML 2.0-autentiseringshanterare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=sv-SE)
* [Extern identitetsleverantör](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)
* [Dynamiskt gruppmedlemskap](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
