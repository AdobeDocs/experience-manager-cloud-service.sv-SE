---
title: IMS-stöd för Adobe Experience Manager as a Cloud Service
description: IMS-stöd för Adobe Experience Manager as a Cloud Service
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: 1e3130578b7e36e5ffd5ad7b04cc7981a95bb291
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 87%

---

# IMS-stöd för Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introduktion {#introduction}

* AEM as a Cloud Service har stöd för Admin Console för AEM-instanser och Adobe Identity Management System (förkortas till IMS) för autentisering.
* Med Admin Console kan administratörer hantera alla Experience Cloud-användare centralt.
* Användare och grupper kan tilldelas produktprofiler som är kopplade till instanser i AEM as a Cloud Service, vilket gör att de kan logga in på instansen.

>[!TIP]
>
>Se vår Experience League-kurs [Konfigurera åtkomst till AEM för administratörer](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem) för en introduktion till hur användare autentiserar med Adobe IMS för att AEM as a Cloud Service och hur Adobe IMS-användare, användargrupper och produktprofiler används för att styra åtkomsten till AEM och dess funktioner. Adobe ID krävs.

>[!NOTE]
>
>AEM stöder för närvarande inte tilldelning av grupper till profiler. Användare bör läggas till individuellt i stället.

## Viktiga funktioner {#key-highlights}

AEM as a Cloud Service har bara stöd för IMS-autentisering för författare, administratörer och utvecklare. Det har inte stöd för externa slutanvändare på kundwebbplatser som webbplatsbesökare.

* I Admin Console representeras kunder som IMS-organisationer och författar- och publiceringsinstanser representeras som produktkontextinstanser. Det gör att system- och produktadministratörer kan hantera åtkomst till instanserna.
* Produktprofiler i Admin Console avgör vilka instanser en användare har åtkomst till.
* Kunderna kan använda sina egna SAML 2-kompatibla identitetsleverantörer (förkortas till IDP) för enkel inloggning.
* Endast Enterprise ID:n eller Federated ID:n för kunder med enkel inloggning stöds, inga personliga Adobe ID.

## Arkitektur {#architecture}

IMS-autentisering fungerar med OAuth-protokoll mellan AEM och Adobe IMS-slutpunkten. När en användare som har en Adobe-identitet har lagts till i IMS kan hen logga in på AEM-redigeringstjänsten med IMS-inloggningsuppgifter.

Inloggningsflödet för användaren visas nedan. Användaren omdirigeras till IMS och eventuellt till kundens IDP för enkel inloggning och omdirigeras sedan tillbaka till AEM.

![IMS-arkitektur](/help/security/assets/ims1.png)

## Konfigurera {#how-to-set-up}

### Integrera organisationer i Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

Kunden måste registreras för Adobe Admin Console för att kunna använda Adobe IMS för AEM-autentisering.

Det första steget är att etablera en organisation i Adobe IMS för kunden. Adobe Enterprise-kunder representeras som IMS-organisationer i [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html). Det är den portal som används av Adobe-kunder för att hantera produktberättiganden för användare och grupper.

AEM-kunder bör redan ha en etablerad organisation och som en del av IMS-etableringen kommer kundinstanser att bli tillgängliga i Admin Console för hantering av användarberättiganden och åtkomst.

När en kund finns som IMS-organisation måste hen konfigurera sitt system enligt sammanfattningen nedan:

![IMS-integrering](/help/security/assets/ims2.png)

1. Den utsedda systemadministratören får en inbjudan att logga in på Cloud Manager. Efter inloggning på Cloud Manager kan systemadministratörerna välja att etablera AEM-program och -miljöer eller navigera till Admin Console för administrativa uppgifter.
1. Systemadministratören gör anspråk på en domän för att bekräfta ägarskap av domänen (till exempel acme.com).
1. Systemadministratören ställer in användarkataloger.
1. Systemadministratören konfigurerar IDP i Admin Console för att ställa in enkel inloggning.
1. AEM-administratören hanterar lokala grupper samt behörigheter och privilegier som vanligt.

Grunderna om Adobe Identity Management, inklusive IDP-konfiguration, beskrivs [här](https://helpx.adobe.com/enterprise/using/set-up-identity.html).

Användning av Enterprise Administration och Admin Console beskrivs [här](https://helpx.adobe.com/enterprise/managing/user-guide.html).

### Integrera användare i Admin Console {#onboarding-users-in-admin-console}

Användare kan integreras på tre sätt beroende på kundens storlek och önskemål: användare skapas manuellt i Admin Console, en CSV-fil överförs eller användare synkroniseras från kundens Enterprise Active Directory.

**Lägga till manuellt via användargränssnittet i Admin Console**

Användare och grupper kan skapas manuellt i Admin Console-gränssnittet. Den här metoden kan användas om du bara har ett fåtal användare att hantera, till exempel färre än 50 AEM-användare eller om du redan använder den här metoden för att administrera andra Adobe-produkter som Analytics, Target eller Creative Cloud.

![Användarintegrering](/help/security/assets/ims3.png)

**Filöverföring i Admin Console-gränssnittet**

Ett enkelt sätt att skapa användare är att ladda upp en `.csv`-fil så att flera användare läggs till samtidigt.

![Filöverföring](/help/security/assets/ims4.png)

**Verktyg för användarsynkronisering**

Med verktyget för användarsynkronisering (förkortas till UST) kan Enterprise-kunder skapa och hantera Adobe-användare med Active Directory. Det fungerar även för andra testade OpenLDAP-katalogtjänster. Målanvändarna är IT-identitetsadministratörer (Enterprise Directory- eller systemadministratörer) som kan installera och konfigurera verktyget. Verktyget med öppen källkod är anpassningsbart så att du kan anpassa det efter dina egna behov.

När användarsynkronisering körs hämtas en lista över användare från organisationens Active Directory och jämförs med listan över användare i Admin Console.  Därefter anropas API:t för Adobe User Management så att Admin Console synkroniseras med organisationens katalog. Flödet är enkelriktat. Ändringar som görs i Admin Console överförs inte till katalogen.

Verktyget gör att systemadministratören kan mappa användargrupper i kundens katalog med produktkonfigurationer och användargrupper i Admin Console.

För att användarsynkronisering ska kunna konfigureras måste organisationen skapa en uppsättning inloggningsuppgifter på samma sätt som [API:t för User Management](https://www.adobe.io/apis/experienceplatform/umapi-new.html) används.

![Verktyg för användarsynkronisering](/help/security/assets/ims5.png)

Verktyget för användarsynkronisering distribueras via Adobe Github-databasen på [den här webbplatsen](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
>En förhandsversion, **2.4RC1**, med stöd för att skapa dynamiska grupper finns [här](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

De viktigaste funktionerna i den här versionen är möjligheten att dynamiskt mappa nya LDAP-grupper för användarmedlemskap i Admin Console samt att skapa dynamiska användargrupper.

Mer information om de nya gruppfunktionerna finns på [den här webbplatsen](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Dokumentation om användarsynkronisering**

Mer information finns i [UST-dokumentationen](https://adobe-apiplatform.github.io/user-sync.py/en/).

Verktyget för användarsynkronisering måste registreras som UMAPI för en Adobe I/O-klient med proceduren som beskrivs [här](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

Dokumentation om Adobe I/O Console finns [här](https://www.adobe.io/apis/cloudplatform/console.html).

API:t för User Management som används av verktyget för användarsynkronisering beskrivs [här](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## Adobe Experience as a Cloud Service-konfiguration {#aem-configuration}

>[!NOTE]
>
>Den AEM IMS-konfiguration som krävs konfigureras automatiskt när AEM-miljöer och instanser etableras. Administratören kan dock ändra den efter behov med metoden som beskrivs [här](/help/implementing/deploying/overview.md).

Den AEM IMS-konfiguration som krävs konfigureras automatiskt när AEM-miljöer och instanser etableras.  Kundadministratörer kan ändra en del av konfigurationen efter behov.

Det övergripande tillvägagångssättet är att konfigurera Adobe IMS som OAuth-leverantör. **Synkroniseringshanteraren för Apache Jackrabbit Oak som används som standard** kan ändras precis som för LDAP-synkronisering.

Nedan anges de viktigaste OSGI-konfigurationerna som måste ändras för att egenskaper som automatiskt användarmedlemskap och gruppmappningar ska kunna ändras.

<!-- Arun to provide list of osgi configs -->

## Användning {#how-to-use}

### Hantera produkter och användaråtkomst i Admin Console {#managing-products-and-user-access-in-admin-console}

När produktadministratören loggar in på Admin Console visas flera instanser av den AEM as a Cloud Service produktkontexten, vilket visas nedan. Välj till exempel någon av produkterna i **Översikt** sida:

![Inloggning på instanser](/help/security/assets/ims6.png)

En lista med befintliga instanser visas:

![Inloggning på instanser2](/help/security/assets/ims7.png)

Under varje instans av produktkontext kommer det att finnas instanser som sträcker sig över redigerings- eller publiceringstjänsterna i produktions-, scen- eller utvecklingsmiljöer. Varje instans kommer att kopplas till produktprofiler eller Cloud Manager-roller. De här produktprofilerna används för att tilldela användare och grupper behörighet.

The **AEM administratörer_xxx** profilen kommer att användas för att ge administratörsbehörighet i den associerade AEM instansen medan **AEM Users_xxx** används för att lägga till vanliga användare.

Alla användare och grupper som läggs till under den här produktprofilen kan logga in på den aktuella instansen enligt exemplet nedan:

![Produktprofil](/help/security/assets/ims8.png)

>[!WARNING]
>
>The **AEM administratörer** produktprofilens namn får inte ändras. Ändra namnet på **AEM administratörer** produktprofilen tar bort administratörsrättigheter för alla användare som har tilldelats den profilen.

### Logga in på Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Lokal administratörsinloggning**

AEM kan även i fortsättningen ha stöd för lokal inloggning för administratörsanvändare. På inloggningsskärmen finns ett alternativ för att logga in lokalt:

![Lokal inloggning](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**IMS-baserad inloggning**

Andra användare kan använda IMS-baserad inloggning när IMS har konfigurerats för instansen. Användarna klickar först på knappen Logga in med Adobe enligt nedan:

![IMS-inloggning](/help/security/assets/ims10.png)


>[!NOTE]
>
>Alla användare som skapas i IMS kan skapas med Adobe ID eller Federated ID. Om en användare konfigureras med Federated ID autentiseras de med hjälp av företagets identitetsleverantör för inloggning.

De dirigeras sedan om till inloggningsskärmen för IMS där de måste ange sina inloggningsuppgifter:

![IMS-inloggning 2](/help/security/assets/ims11.png)

![IMS-inloggning 3](/help/security/assets/ims12.png)

Om en federerad IDP konfigureras under den inledande konfigurationen av Admin Console kommer användaren att omdirigeras till kundens IDP för enkel inloggning:

![IMS-inloggning 4](/help/security/assets/ims13.png)

När autentiseringen är klar omdirigeras användaren tillbaka till AEM och loggas in:

![IMS-inloggning 5](/help/security/assets/ims14.png)

### Hantera behörigheter och åtkomstkontrollistor i Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

Åtkomstkontrollistorna och behörigheterna fortsätter att hanteras i AEM. Användargrupper som synkroniseras från IMS kan tilldelas lokala grupper där åtkomstkontrollistor och behörigheter definieras.

I exemplet nedan lägger vi till synkroniserade grupper i den lokala gruppen **Dam_Users** som exempel.

Användaren ingår i följande grupper i IMS:

![ACL1](/help/security/assets/ims15.png)

När användaren loggar in synkroniseras hans/hennes gruppmedlemskap enligt nedan:

![ACL2](/help/security/assets/ims16.png)

I AEM kan användargrupper som synkroniseras från IMS läggas till som medlemmar i befintliga lokala grupper, som **DAM Users**.

![ACL3](/help/security/assets/ims17.png)

Som framgår nedan ärver gruppen **AEM-GRP_008** behörigheterna och privilegierna för **DAM Users**. Det är ett effektivt sätt att hantera behörigheter för synkroniserade grupper och det används ofta även i den LDAP-baserade autentiseringsmetoden.

![ACL3](/help/security/assets/ims18.png)


### Åtkomst till Cloud Manager {#accessing-cloud-manager}

För att kunna komma åt Cloud Manager eller AEM as a Cloud Service-miljöerna måste du tilldelas en profil i Cloud Manager-produkten.

Läs Rolldefinitioner om du vill veta mer om roller för användare som styr tillgången till specifika funktioner i Cloud Manager.

>[!NOTE]
>Cloud Manager har förkonfigurerade roller med lämpliga behörigheter. Om du vill veta mer om de olika rollerna med specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll kan du läsa [Rollbaserade behörigheter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html).

**Steg för att lägga till en användare**

1. Lägg till en användare till en viss profil från en befintlig användarskärm eller en ny användarskärm.

1. Du kan också lägga till en användare från skärmen **Overview** som visas i bilden nedan.

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >Du kan tilldela mer än en profil till en användare som du kan se i bilden nedan.

   ![ACL3](/help/security/assets/ims22.png)


1. När du har lagts till i rätt profil bör du ha tillgång till respektive klientorganisation i Cloud Manager via [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) i det övre högra hörnet i användargränssnittet.


### Få tillgång till Experience Manager as a Cloud Service {#accessing-instance-cloud-service}

>[!IMPORTANT]
>Stegen som nämns i föregående avsnitt måste vara slutförda innan du beviljas åtkomst till en instans i AEM as a Cloud Service.

För att få tillgång till en AEM-instans i **Admin Console** bör du läsa Cloud Manager-programmet och miljöerna i programmet i produktlistan på **Admin Console**.

I skärmbilden nedan visas två tillgängliga miljöer, *dev author* och *publish*.

![ACL3](/help/security/assets/ims19.png)

För att få tillgång till AEM-instanser måste användaren läggas till i en grupp för den Cloud Service-produkten.

Alla författarinstanser har en AEM-administratörsprofil och AEM-användarprofil, och alla publiceringsinstanser har en AEM-användarprofil. Du kan lägga till andra profiler efter behov.

Om du vill ge åtkomst på administratörsnivå till AEM-instansen lägger du till användaren i AEM-administratörsprofilen för den aktuella produkten.
