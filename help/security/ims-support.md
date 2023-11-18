---
title: IMS-stöd för Adobe Experience Manager as a Cloud Service
description: Stöd för Image Management System i Adobe Experience Manager as a Cloud Service
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 37%

---

# IMS-stöd för Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introduktion {#introduction}

* AEM as a Cloud Service har stöd för Admin Console för AEM-instanser och Adobe Identity Management System (förkortas till IMS) för autentisering.
* Med Admin Console kan administratörer hantera alla Experience Cloud-användare centralt.
* Användare och grupper kan tilldelas till produktprofiler som är kopplade till en AEM as a Cloud Service instans, så att de kan logga in på den instansen.

>[!TIP]
>
>Se [Konfigurera åtkomst till AEM för administratörer](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem) för en introduktion till hur användare autentiserar med Adobe IMS för att AEM as a Cloud Service. Läs också om hur Adobe IMS-användare, användargrupper och produktprofiler används för att styra åtkomsten till AEM samt funktioner och funktioner. Adobe ID krävs.

{{ims-group-profiles}}

## Viktiga funktioner {#key-highlights}

AEM as a Cloud Service har endast stöd för IMS-autentisering för författare, administratörer och utvecklare. Det har inte stöd för externa slutanvändare på kundwebbplatser som webbplatsbesökare.

* Admin Console representerar kunder som IMS-organisationer, författare och publiceringsinstanser i en miljö som produktkontextinstanser. Den här representationen gör att system- och produktadministratörer kan hantera åtkomst till instanser.
* Produktprofiler i Admin Console avgör vilka instanser en användare har åtkomst till.
* Kunder kan använda sina egna SAML 2-kompatibla identitetsleverantörer (IDP for short) för enkel inloggning.
* Endast Enterprise ID:n eller Federated ID:n för kunder med enkel inloggning stöds, inga personliga Adobe ID:n.

## Arkitektur {#architecture}

IMS-autentisering fungerar med OAuth-protokoll mellan AEM och Adobe IMS-slutpunkten. När en användare som har en Adobe-identitet har lagts till i IMS kan hen logga in på AEM-redigeringstjänsten med IMS-inloggningsuppgifter.

Användarens inloggningsflöde visas nedan, användaren omdirigeras till IMS och eventuellt till kund-ID för enkel inloggning och sedan omdirigeras tillbaka till AEM.

![IMS-arkitektur](/help/security/assets/ims1.png)

## Konfigurera {#how-to-set-up}

### Integrera organisationer i Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

Kunden måste registreras för Adobe Admin Console för att kunna använda Adobe IMS för AEM-autentisering.

Som ett första steg måste kunderna ha en organisation som är etablerad i Adobe IMS. Adobe Enterprise-kunder representeras som IMS-organisationer i [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html). Det här området är den portal som Adobe-kunder använder för att hantera sina produkträttigheter för användare och grupper.

AEM kunder bör redan ha en organisation etablerad, och som en del av IMS-etableringen är kundinstanserna tillgängliga i Admin Console för hantering av användarrättigheter och åtkomst.

När en kund finns som IMS-organisation måste han/hon konfigurera sitt system enligt följande:

![IMS-integrering](/help/security/assets/ims2.png)

1. Den utsedda systemadministratören får en inbjudan att logga in på Cloud Manager. Efter inloggning på Cloud Manager kan systemadministratörerna välja att etablera AEM-program och -miljöer eller navigera till Admin Console för administrativa uppgifter.
1. Systemadministratören gör anspråk på en domän för att bekräfta ägarskap av domänen (till exempel acme.com).
1. Systemadministratören ställer in användarkataloger.
1. Systemadministratören gör IDP-konfiguration i Admin Console för att konfigurera enkel inloggning.
1. AEM-administratören hanterar lokala grupper samt behörigheter och privilegier som vanligt.

Grunderna om Adobe Identity Management, inklusive IDP-konfiguration, beskrivs [här](https://helpx.adobe.com/enterprise/using/set-up-identity.html).

Användning av Enterprise Administration och Admin Console beskrivs [här](https://helpx.adobe.com/enterprise/admin-guide.html).

### Integrera användare i Admin Console {#onboarding-users-in-admin-console}

Det finns tre sätt att introducera användare. Varje metod beror på kundens storlek och önskemål. Du kan skapa användare i Admin Console manuellt, överföra en CSV-fil eller synkronisera användare från kundens Enterprise Active Directory.

**Lägga till manuellt via användargränssnittet i Admin Console**

Användare och grupper kan skapas manuellt i Admin Console-gränssnittet. Den här metoden kan användas om du inte har många användare att hantera. Färre än 50 AEM användare, eller om du redan använder den här metoden för att administrera andra Adobe-produkter som Analytics-, Target- eller Creative Cloud-program.

![Användarintegrering](/help/security/assets/ims3.png)

**Filöverföring i Admin Console-gränssnittet**

Ett enkelt sätt att skapa användare är att ladda upp en `.csv`-fil så att flera användare läggs till samtidigt.

![Filöverföring](/help/security/assets/ims4.png)

**Verktyg för användarsynkronisering**

Med verktyget för användarsynkronisering (UST i korthet) kan Adobe företagskunder skapa och hantera Adobe-användare med Active Directory. DETTA FUNGERAR även för andra testade OpenLDAP-katalogtjänster. Målanvändarna är IT-identitetsadministratörer (Enterprise Directory eller System Admins) som kan installera och konfigurera verktyget. Verktyget med öppen källkod är anpassbart så att kunderna kan anpassa det efter sina egna behov.

När användarsynkronisering körs hämtar den en lista över användare från organisationens Active Directory och jämför den med listan över användare i Admin Console. Därefter anropas API:t för användarhantering i Adobe så att Admin Console synkroniseras med organisationens katalog. Flödet är enkelriktat. Ändringar som görs i Admin Console överförs inte till katalogen.

Med verktyget kan systemadministratören mappa användargrupper i kundens katalog med produktkonfiguration och användargrupper i Admin Console.

För att konfigurera användarsynkronisering måste organisationen skapa en uppsättning autentiseringsuppgifter på samma sätt som de använder [API för användarhantering](https://developer.adobe.com/umapi/).

![Verktyg för användarsynkronisering](/help/security/assets/ims5.png)

Verktyget för användarsynkronisering distribueras via Adobe GitHub-databasen [på den här platsen](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2).

>[!NOTE]
>
>En förhandsversion, **2.4RC1**, med stöd för att skapa dynamiska grupper finns [här](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

De viktigaste funktionerna i den här versionen är möjligheten att dynamiskt mappa nya LDAP-grupper för användarmedlemskap i Admin Console och att skapa dynamiska användargrupper.

Mer information om de nya gruppfunktionerna finns på [den här webbplatsen](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options).

**Dokumentation om användarsynkronisering**

Se [UST-dokumentation](https://adobe-apiplatform.github.io/user-sync.py/en/) för mer information.

Verktyget för användarsynkronisering måste registreras som Adobe Developer klient-UMAPI enligt proceduren [här](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

Adobe Developer Console Documentation finns [här](https://developer.adobe.com/developer-console/).

API:t för User Management som används av verktyget för användarsynkronisering beskrivs [här](https://adobe-apiplatform.github.io/user-sync.py/en/).

## Adobe Experience as a Cloud Service-konfiguration {#aem-configuration}

>[!NOTE]
>
>Den AEM IMS-konfiguration som krävs konfigureras automatiskt när AEM miljöer och instanser etableras. Administratören kan dock ändra den efter behov med metoden som beskrivs [här](/help/implementing/deploying/overview.md).

Den AEM IMS-konfiguration som krävs konfigureras automatiskt när AEM miljöer och instanser etableras. Kundadministratörer kan ändra en del av konfigurationen efter behov.

Det övergripande tillvägagångssättet är att konfigurera Adobe IMS som OAuth-leverantör. **Synkroniseringshanteraren för Apache Jackrabbit Oak som används som standard** kan ändras precis som för LDAP-synkronisering.

Nedan visas de viktigaste OSGI-konfigurationerna som måste ändras för att ändra egenskaper som Automatiskt användarmedlemskap eller gruppmappningar.

<!-- Arun to provide list of osgi configs -->

## Användning {#how-to-use}

### Hantera produkter och användaråtkomst i Admin Console {#managing-products-and-user-access-in-admin-console}

När produktadministratören loggar in på Admin Console visas flera instanser av den AEM as a Cloud Service produktkontexten, vilket visas nedan. Välj till exempel någon av produkterna i **Ökning** sida:

![Inloggning på instanser](/help/security/assets/ims6.png)

En lista över befintliga instanser visas:

![Inloggning på instanser2](/help/security/assets/ims7.png)

Under varje instans av produktkontext finns instanser som sträcker sig över redigerings- eller publiceringstjänsterna i produktions-, scen- eller utvecklingsmiljöer. Varje instans är associerad med produktprofiler eller Cloud Manager-roller. De här produktprofilerna används för att tilldela användare och grupper behörighet.

The **AEM administratörer_xxx** profilen används för att ge administratörsbehörighet i den associerade AEM-instansen när **AEM Users_xxx** används för att lägga till vanliga användare.

Alla användare och grupper som läggs till under den här produktprofilen kan logga in på den instansen enligt exemplet nedan:

![Produktprofil](/help/security/assets/ims8.png)

>[!WARNING]
>
>Ändra inte **AEM administratörer** produktprofilnamn. Ändra namnet på **AEM administratörer** produktprofilen tar bort administratörsrättigheter för alla användare som har tilldelats den profilen.

### Logga in på Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Lokal administratörsinloggning**

AEM kan även i fortsättningen ha stöd för lokal inloggning för administratörsanvändare. På inloggningsskärmen kan du logga in lokalt:

![Lokal inloggning](/help/security/assets/ims9.png)

<!-- the above image must be updated for skyline -->

**IMS-baserad inloggning**

För andra användare används den IMS-baserade inloggningen efter att IMS har konfigurerats på instansen. Användaren klickar på knappen Logga in med Adobe enligt nedan:

![IMS-inloggning](/help/security/assets/ims10.png)


>[!NOTE]
>
>Alla användare som skapas i IMS kan skapas med Adobe ID eller Federated ID. Om en användare konfigureras med Federated ID autentiseras de med hjälp av företagets identitetsleverantör för inloggning.

De dirigeras om till inloggningsskärmen för IMS och måste ange sina autentiseringsuppgifter:

![IMS-inloggning 2](/help/security/assets/ims11.png)

![IMS-inloggning 3](/help/security/assets/ims12.png)

Om en federerad IDP konfigureras under den första konfigurationen av Admin Console dirigeras användaren till kund-ID:t för enkel inloggning:

![IMS-inloggning 4](/help/security/assets/ims13.png)

När autentiseringen är klar omdirigeras användaren tillbaka till AEM och loggas in:

![IMS-inloggning 5](/help/security/assets/ims14.png)

### Hantera behörigheter och åtkomstkontrollistor i Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

Åtkomstkontrollistorna och behörigheterna fortsätter att hanteras i AEM. Användargrupper som synkroniseras från IMS kan tilldelas lokala grupper där åtkomstkontrollistor och behörigheter definieras.

I exemplet nedan läggs synkroniserade grupper till i den lokala **Dam_Users** gruppera som exempel.

Användaren ingår i följande grupper i IMS:

![ACL1](/help/security/assets/ims15.png)

När användaren loggar in synkroniseras hans/hennes gruppmedlemskap enligt nedan:

![ACL2](/help/security/assets/ims16.png)

I AEM kan användargrupper som synkroniseras från IMS läggas till som medlemmar i befintliga lokala grupper, som **DAM Users**.

![ACL3](/help/security/assets/ims17.png)

Som visas nedan är gruppen **AEM-GRP_008** ärver behörigheter och behörigheter för **DAM-användare**. Detta arv är ett effektivt sätt att hantera behörigheter för synkroniserade grupper och används ofta i den LDAP-baserade autentiseringsmetoden.

![ACL3](/help/security/assets/ims18.png)


### Åtkomst till Cloud Manager {#accessing-cloud-manager}

För att kunna komma åt Cloud Manager eller miljöer på AEM as a Cloud Service måste du tilldelas Profiler för Cloud Manager-produkten.

Mer information om roller för användare som styr tillgängligheten av specifika funktioner i Cloud Manager finns i Rolldefinitioner.

>[!NOTE]
>Cloud Manager har förkonfigurerade roller med lämpliga behörigheter. Om du vill veta mer om de roller som har specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll kan du läsa [Rollbaserade behörigheter](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions.html?lang=en).

**Steg för att lägga till en användare**

1. Lägg till en användare till en viss profil från en befintlig användarskärm eller en ny användarskärm.

1. Du kan också lägga till en användare från skärmen **Overview** som visas i bilden nedan.

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >Du kan tilldela mer än en profil till en användare som du kan se i bilden nedan.

   ![ACL3](/help/security/assets/ims22.png)


1. När du har lagts till i rätt profil bör du kunna komma åt respektive innehavare i Cloud Manager via [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) med hjälp av det övre högra hörnet i användargränssnittet.


### Få tillgång till Experience Manager as a Cloud Service {#accessing-instance-cloud-service}

>[!IMPORTANT]
>Stegen som nämns i föregående avsnitt måste vara slutförda innan du beviljas åtkomst till en instans i AEM as a Cloud Service.

Så här får du åtkomst till en AEM i **Admin Console**, ska du se Cloud Manager-programmet och miljöerna i programmet i produktlistan på **Admin Console**.

På skärmbilden nedan visas två tillgängliga miljöer, nämligen *dev-författare* och *publicera*.

![ACL3](/help/security/assets/ims19.png)

För att få åtkomst till AEM instanser måste användaren läggas till i en grupp av rätt Cloud Service Product.

Varje författarinstans har en AEM administratörs- och AEM användarprofil och varje publiceringsinstans har en AEM användarprofil. Du kan lägga till andra profiler efter behov.

Om du vill ge åtkomst på administratörsnivå till AEM-instansen lägger du till användaren i AEM-administratörsprofilen för den aktuella produkten.
