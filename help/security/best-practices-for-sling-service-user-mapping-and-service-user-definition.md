---
title: Bästa praxis för användarmappning av delningstjänst och användardefinition av tjänst
description: Läs mer om de bästa sätten att sälja användarmappning för tjänster och användardefinition för tjänster
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Bästa praxis för användarmappning av delningstjänst och användardefinition av tjänst {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## Mappning av tjänstanvändare {#service-user-mapping}

Om du vill lägga till en mappning från tjänsten till motsvarande systemanvändare måste du skapa en fabrikskonfiguration för tjänsten `ServiceUserMapper`. För att behålla denna modulära form kan sådana konfigurationer tillhandahållas med Sling-funktionen för&quot;ändring&quot; (mer information finns i [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578)). Det rekommenderade sättet att installera sådana konfigurationer med ditt paket är att lägga till det i provisioneringsmodellen för QuickStart enligt följande exempel:

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### Mappningsformat {#mapping-format}

Sedan AEM 6.4 definieras mappningsformatet enligt följande:

>[!NOTE]
>
>`userName` är föråldrad och bör inte längre användas.

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` och `subserviceName` identifierar tjänsten, `userName/principalNames` identifierar tjänstanvändaren och `principalNames` är en kommaavgränsad lista.

Observera också att `principalNames` är en lista över tjänstanvändarens huvudnamn som inte är samma som ID:t.


**Bästa praxis**

* Undertjänstnamn för olika aktiviteter - om tjänsterna i ditt paket utför olika uppgifter rekommenderar vi att du identifierar `subserviceNames` för att gruppera dem efter aktiviteter
* Om en viss tjänst utför olika åtgärder (till exempel läser resursinnehåll och uppdaterar information under ett underträd till `/var`), bör du spegla detta genom att samla olika tjänstobjekt som speglar den enskilda åtgärden, till exempel genom att sammanfoga den vanliga `dam-reader-service` med din funktionsspecifik `assetreport-writer-service`
* Varje tjänst är idealisk bunden till en mycket specifik och begränsad uppsättning operationer
* Det nya formatet med `[one,or,multiple,principalNames]` rekommenderas för att definiera tjänstanvändarmappningar från och med AEM 6.4.

Nedan finns en lista med skäl för att ändra formatet och varför Adobe rekommenderar att du använder det istället för versionsmappning bara för ett enda användar-ID:

* Möjlighet att återanvända serviceanvändare genom att kombinera kundernas särskilda behov med vanliga uppgifter
* Undvik dubblering av behörighetsinställningar
* Bättre förståelse för vilka behörigheter (och uppgifter) en viss tjänst faktiskt utför
* Inget behov av explicit gruppmedlemskap för tjänstanvändare. Detta kan få besvärliga biverkningar när gruppbehörigheter ändras
* Prestandaförbättringar och skalbarhet

## Mappningsupplösning och tjänstinloggning {#mapping-resolution-and-service-login}

### Lösning för tjänstmappning {#service-mapping-resolution}

Sekvensen med anrop för att lösa tjänstmappningen som beskrivs nedan:

1. Sök efter aktiv `principalNames`-mappning för angiven `bundleId` och `subserviceName`
1. `principalNames`-mappning för `bundleId` och null `subserviceName`
1. `userName`-mappning för `bundleId` och `subserviceName`
1. `userName`-mappning för `bundleId` och null `subserviceName`
1. Standardmappning
1. Standardanvändare

### SlingRepository - tjänstinloggning {#slingrepository-servicelogin}

Sekvensen för att hämta en tjänst `Session/ResourceResolver` fungerar så här:

1. Hämta huvudnamn från `ServiceUserMapper` =>-databasinloggning före autentisering enligt beskrivningen nedan
1. Hämta användar-ID från `ServiceUserMapper`
1. Kontrollera om 1ServiceUserConfiguration&grave; är inaktuellt användar-ID
1. Standardinloggning för Sling-tjänsten med användar-ID (t.ex. en sekvens av `createAdministrativeSession` och personifiering för användar-ID)

Den nya mappningen med huvudnamn resulterar i följande förenklade databasinloggning:

* Uppsättningen med huvudnamn behandlas som de faktiska huvudnamn som ska användas för att fylla i `Subject`
* Databasinloggning kan följaktligen vara förautentiserad
* Ingen upplösning av gruppmedlemskap

  >[!NOTE]
  >
  >Alla nödvändiga behörigheter måste deklareras för tjänstanvändarna. Alla och andra gruppbehörigheter ärvs inte längre.

* Inga ytterligare administratörsinloggningar för tjänsten `Session/ResourceResolver` har skapats.

### ServiceUserConfiguration har tagits bort {#deprecated-serviceUserConfiguration}

Observera att det är samma sak att ange ett användarnamn i mappningen som det befintliga `ServiceUserConfiguration.simpleSubjectPopulation`. Med det nya formatet kan den tillfälliga lösning som tillhandahålls av `ServiceUserConfiguration` återspeglas direkt med tjänstanvändarmappningen. `ServiceUserConfiguration` har därför ersatts för AEM och alla befintliga användningar har ersatts.

## Tjänstanvändare {#service-users}

### Återanvända befintliga tjänstanvändare {#reusing-existing-service-users}

Vi rekommenderar att du återanvänder befintliga användare om följande villkor uppfylls:

* Dina behov matchar den befintliga tjänstanvändarens avsikt
* Tjänsten kräver att du utför en vanlig uppgift som täcks av en befintlig vanlig tjänstanvändare. I det här fallet bör du återanvända tjänstanvändaren i stället för att införa dubbletter
* Tjänsten kräver en specifik uppgift som täcks av en befintlig tjänstanvändare. Om du är osäker på detta frågar du det funktionsteam som äger det.

Återanvänd inte befintliga tjänstanvändare om:

* Du måste ändra behörigheten på ett icke-relaterat sätt för att det ska fungera
* Om du bara behöver en liten del av behörigheten som den ger och du bara vill återanvända den eftersom den får din funktion att fungera istället för att den matchar
* Om namnet anger en helt annan avsikt än vad du vill ha. Om du väljer den eftersom den fungerar kan det orsaka problem eftersom det funktionsteam som äger en viss tjänst kan ändra behörigheterna och bryta funktionen.

### Skapa en tjänstanvändare {#creating-a-service-user}

När du har verifierat att ingen befintlig tjänstanvändare i AEM kan användas för ditt användningsfall och att motsvarande RTC-problem har godkänts kan du lägga till den nya användaren i standardinnehållet. Helst är det en medlem i det utökade säkerhetsteamet som deltar i RTC-omröstningen, så se till att du även engagerar lämpliga intressenter.

**Namnkonvention**

AEM säkerhetsteam har definierat följande namngivningskonvention för tjänstanvändare för att göra nya tjänstanvändare mer konsekventa och för att förbättra läsbarheten och underhållet.

Ett tjänstanvändarnamn består av 3 element avgränsade med bindestreck **-**:

1. Den logiska entiteten/funktionen som är målet för tjänståtgärderna (undvik sökvägselement som kan ändras)
1. Den uppgift som tjänsterna ska utföra
1. Slutför **-tjänsten** så att det är enkelt att hitta ID:t och huvudnamnet att användaren är en tjänstanvändare

**God praxis**

* Blanda inte olika enheter/funktioner. Dela till enskilda tjänstanvändare och slå ihop dem i mappningen om tjänsten har olika behov
* Begränsa dig till en väldefinierad uppgift per tjänstanvändare. Dela om du slutar bevilja för många eller orelaterade behörigheter
* Tillbringa tid med att identifiera det verkliga behovet av tjänsten
* Tillbringa tid med att hitta ett bra, meningsfullt och självförklarande användarnamn för tjänsten
* Be om feedback och granskning: utvecklare som inte känner till din funktion bör kunna läsa och förstå din avsikt. De kan i framtiden behöva åtgärda eller underhålla det.

I slutet bör tjänstens användarnamn visa:

* Hur det ska användas och om det kan återanvändas:

   * Mycket allmänt: `content-writer-service`. Säkert att återanvända i aggregering om era tjänster också behöver kunna läsa allt innehåll
   * Mycket specifik: `asset-linkshare-service`. Det är inte så säkert att återanvända om inte din tjänst också gör länkdelning av resurser.

* Hur funktionsuppsättningen och behörighetsinställningarna ser ut:

   * Den logiska entiteten måste matcha behörighetsinställningarna:

      * En `content-foo-service` ska bara associeras med åtgärder för innehåll. Bevilja den behörighet att arbeta på andra enheter, som konfiguration eller användare, skulle vara fel
      * En specifik tjänst som `personalization-foo-service` bör också ha särskilda behörigheter. Om ni ger behörigheter för allt innehåll är det inte längre specifikt. Återanvänd en vanlig användare i en aggregering
      * En funktionsspecifik tjänst som `msm-xyz-service` ska endast ha msm-relaterade behörigheter. Utöka inte behörigheter till icke-relaterade funktioner som att hantera communitykonfiguration eller skärmanvändare.

   * Aktiviteten måste matcha behörigheterna:

      * En `foo-reader-service` ska bara kunna läsa vanliga objekt. Ge aldrig skrivbehörigheter
      * En `foo-writer-service` kan förväntas utföra skrivåtgärder. Det bör dock inte ges behörighet att läsa/ändra innehåll för åtkomstkontroll
      * `foo-replicator-service` kan förväntas ha `crx:replicate` tilldelat.

**Exempel**

Exempel för `configuration-reader-service`:

* Namnet anger att det refererar till konfigurationer i allmänhet och inte konfigurering av en viss funktion, som konfiguration av DM-integrering. En tjänstanvändare som är specifikt inriktad på att läsa konfigurationen för en sådan integrering får i stället namnet `dmconfig-reader-service` eller `s7config-reader-service`

  >[!NOTE]
  >
  >Ingen sökvägsinformation inkluderas i namngivningen. Konfigurationer har flyttats från `/etc` till `/conf`.

* Aktivitetselementet anger att tjänster som är bundna till den användaren endast utför läsåtgärder.

Exempel för `userproperties-copy-service`:

* Tjänster som är bundna till den här tjänstanvändaren kommer att fungera på användar-/gruppegenskaper som profiler eller inställningar
* Det är specifikt avsett att bara kopiera den informationen i motsats till ett namn som `userproperties-writer-service` som skulle innehålla alla typer av skrivåtgärder. Det är därför möjligt att behörighetsinställningarna för de här kopieringsåtgärderna endast tillåter att objekt på en plats läggs till och tas bort från en annan plats.

**Bästa praxis för behörighetsinställningar**

* Använd alltid huvudbaserad åtkomstkontroll för tjänstanvändare. Mer information finns i exemplen nedan:

   * Tillåt att markera tjänstanvändare och deras behörigheter som oföränderligt programinnehåll i himlen
   * Du behöver inte skapa sökvägar och trädstrukturer

* Bevilja endast behörigheter, neka aldrig
* Begränsa behörigheter

   * Ge bara den minsta uppsättning behörigheter som behövs
   * Mer information finns i dokumentationen för [Mappningsbehörigheter till objekt](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) och [Mappnings-API-anrop till behörigheter](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html)
   * Ge inte behörighet till `jcr:all`. Det är sannolikt inte minimalt.

* Minska omfånget

   * Placera åtkomstkontrollprinciper i funktionsspecifika underträd
   * Vid distribuerade objekt: använd begränsningar för att begränsa omfånget (se [dokumentationen](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) för en lista över inbyggda begränsningar).

* Säkerställ enhetlighet

   * Gör behörigheterna konsekventa med entiteten och aktiviteten som du använde i tjänstens användarnamn
   * Undvik att lägga till orelaterade behörigheter. Det skulle till exempel vara konstigt att ha en `workflow-administration-service` och ge den behörighet att utföra användarhanteringsåtgärder på `/home/users/screens` eller låta den läsa s7-config.

* Fullständighet

   * Se till att din tjänst har alla behörigheter den behöver för att utföra de uppgifter den är avsedd att utföra. Tjänsten måste komma igång direkt även i kundmiljöer.
   * Förvänta dig aldrig/be kunder utöka behörighetsinställningarna (till exempel under `/apps`)

* Undvik dubblering av behörighetsinställningar

   * Återanvänd vanliga tjänstanvändare
   * Sammanställ dem med funktionsspecifika tjänstanvändare som ger dig den specifika behörighet du behöver.

* Dela inte upp behörighetsinställningar mellan olika funktioner. Behovet av att göra detta visar att din tjänstanvändare inte är väldefinierad eller gör för många olika saker
* Placera inte tjänstanvändare i grupper eftersom:

   * Den blandar implementeringsinformation från tjänstanvändare med publika grupper
   * Du saknar kontroll för behörighetsändringar (ofta för regressioner och eskaleringar av behörigheter)
   * Inloggning och utvärdering
   * Fungerar inte med huvudbaserad AC-installation

* Åtkomst till noden user-home (eller något underträd i den), som inte har en förutsägbar sökväg, uppnås i repo init med home(`userId`). Mer information finns i försäljningsrepo init [documentation](https://sling.apache.org/documentation/bundles/repository-initialization.html).
* RTC: skapa ett dedikerat RTC-problem om du ändrar behörigheter för en befintlig tjänstanvändare och ser till att du får det granskat av säkerhetsteamet.

**Skapad med databasinitiering**

Använd alltid `repo-init` för att definiera tjänstanvändare och deras behörighetsinställningar och placera båda i rätt avsnitt i QuickStart-funktionsmodellen:

**God praxis**

* Använd alltid `repo-init` för att skapa tjänstanvändaren
* Ange alltid en mellanliggande sökväg för att skapa en tjänstanvändare
* Alla inbyggda tjänstanvändare för AEM måste finnas under `system/cq:services/internal`
* Lägg dessutom till den mellanliggande relativa sökvägen till grupperade tjänstanvändare efter funktion: `system/cq:services/internal/<your-feature>`
* Kunddefinierade tjänstanvändare måste finnas under `system/cq:services/<customer-intermediate-rel-path>` och aldrig under det interna trädet
* Använd **med den tvingade sökvägen** i stället för **med sökvägen** om det redan finns en användare som måste flyttas till den nya platsen som stöder huvudbaserad auktorisering.

**Exempel**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### Rensning av tjänstanvändare och behörigheter {#cleanup-service-users-and-permissions}

Följande init-kommando för repo kan användas för att rensa bort oanvända tjänstanvändare och deras behörigheter:

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### Testtjänstanvändare {#testing-service-users}

Det är viktigt att skriva tester på serversidan för tjänstanvändare och deras behörighetsinställningar. Detta verifierar inte bara att konfigurationen fungerar, utan hjälper dig även att upptäcka regressioner och oavsiktliga misstag när du ändrar innehåll för åtkomstkontroll eller tjänstanvändare.

Biblioteket `com.adobe.granite.testing.clients` innehåller många verktyg som gör det enkelt att skriva SST-filer för tjänstanvändare.
