---
title: IMS-stöd för Adobe Experience Manager som en molntjänst
description: 'IMS-stöd för Adobe Experience Manager som en molntjänst '
translation-type: tm+mt
source-git-commit: 7ece752a5f59966e0c6be638c37bcaaf238b629a

---


# IMS-stöd för Adobe Experience Manager som en molntjänst {#ims-support-for-aem-as-a-cloud-service}

## Introduktion {#introduction}

* AEM som en molntjänst inkluderar stöd för Admin Console för AEM-instanser och Adobe Identity Management System (IMS för kort autentisering).
* Med Admin Console kan administratörer hantera alla Experience Cloud-användare centralt.
* Användare och grupper kan tilldelas produktprofiler som är kopplade till AEM som molntjänstinstanser, vilket gör att de kan logga in på den instansen.

## Viktiga markeringar {#key-highlights}

AEM som en molntjänst erbjuder endast stöd för IMS-autentisering för författare, administratörer och utvecklare. Det erbjuder inte stöd för externa slutanvändare på kundsajter som besökare på sajten.

* Admin Console representerar kunder som IMS-organisationer, författare och publiceringsinstanser i en miljö som produktkontextinstanser. På så sätt kan system- och produktadministratörer hantera åtkomst till instanser.
* Produktprofiler på Admin Console avgör vilka instanser en användare har åtkomst till.
* Kunderna kan använda sina egna SAML 2-kompatibla identitetsleverantörer (IDP for short) för enkel inloggning.
* Endast Enterprise ID:n eller Federated ID:n för kunder med enkel inloggning stöds, inga personliga Adobe ID:n.

## Arkitektur {#architecture}

IMS-autentisering fungerar med OAuth-protokoll mellan AEM och Adobe IMS-slutpunkten. När en användare har lagts till i IMS och har en Adobe-identitet kan han/hon logga in på AEM Managed Services-instanser med IMS-inloggningsuppgifter.

Inloggningsflödet för användaren visas nedan. Användaren omdirigeras till IMS och eventuellt till kund-ID för enkel inloggning och omdirigeras sedan tillbaka till AEM.

![IMS-arkitektur](/help/security/assets/ims1.png)

## Konfigurera {#how-to-set-up}

### Integrera organisationer i Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

Kunden måste registrera sig för Adobe Admin Console för att kunna använda Adobe IMS för AEM-autentisering.

Som ett första steg måste kunderna ha en organisation som är etablerad i Adobe IMS. Adobe Enterprise-kunder representeras som IMS-organisationer i [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) . Det här är den portal som används av Adobe-kunder för att hantera produktberättiganden för användare och grupper.

AEM-kunder bör redan ha en organisation etablerad, och som en del av IMS-etableringen kommer kundinstanser att vara tillgängliga i Admin Console för hantering av användarrättigheter och åtkomst.

När en kund finns som IMS-organisation måste han/hon konfigurera sitt system enligt sammanfattningen nedan:

![IMS-introduktion](/help/security/assets/ims2.png)

1. Den utsedda systemadministratören får en inbjudan att logga in i Cloud Manager. När du har loggat in på Cloud Manager kan systemadministratörerna välja att tillhandahålla AEM-program och -miljöer eller navigera till Admin Console för administrativa uppgifter.
1. Systemadministratören gör anspråk på en domän för att bekräfta ägarskapet för respektive domän (till exempel acme.com)
1. Systemadministratören ställer in användarkataloger
1. Systemadministratören gör IDP-konfigurationen i Admin Console för att konfigurera enkel inloggning.
1. AEM Administrator hanterar lokala grupper och behörigheter som vanligt.

Grunderna för Adobe Identity Management, inklusive IDP-konfiguration, beskrivs [här](https://helpx.adobe.com/enterprise/using/set-up-identity.html).

Användning av Enterprise Administration och Admin Console beskrivs [här](https://helpx.adobe.com/enterprise/managing/user-guide.html).

### Onboarding-användare på Admin Console {#onboarding-users-in-admin-console}

Det finns tre sätt att introducera användare beroende på kundens storlek och deras önskemål: manuellt skapa användare i Admin Console, överföra en CSV-fil eller synkronisera användare från kundens Enterprise Active Directory.

**Manuellt tillägg via användargränssnittet i Admin Console**

Användare och grupper kan skapas manuellt i Admin Console-gränssnittet. Den här metoden kan användas om du inte har ett stort antal användare att hantera. Till exempel färre än 50 AEM-användare eller om du redan använder den här metoden för att administrera andra Adobe-produkter som Analytics, Target eller Creative Cloud.

![Användarintroduktion](/help/security/assets/ims3.png)

**Filöverföring i Admin Console-gränssnittet**

För att förenkla hanteringen av användargenereringen kan en `.csv` fil laddas upp för att flera användare ska kunna läggas in samtidigt.

![Filöverföring](/help/security/assets/ims4.png)

**Verktyget för användarsynkronisering**

Med verktyget för användarsynkronisering (UST i korthet) kan våra företagskunder skapa och hantera Adobe-användare med Active Directory. Detta fungerar även för andra testade OpenLDAP-katalogtjänster. Målanvändarna är IT-identitetsadministratörer (Enterprise Directory eller System Admins) som kan installera och konfigurera verktyget. Verktyget med öppen källkod är anpassbart så att kunderna kan anpassa det efter sina egna behov.

När användarsynkronisering körs hämtar den en lista över användare från organisationens Active Directory och jämför den med listan över användare i Admin Console.  Därefter anropas API:t för Adobes användarhantering så att Admin Console synkroniseras med organisationens katalog. Ändringsflödet är helt enkelt ett sätt. Ändringar som görs i Admin Console skickas inte ut till katalogen.

Verktyget gör att systemadministratören kan mappa användargrupper i kundens katalog med produktkonfigurationer och användargrupper i Admin Console.

För att konfigurera användarsynkronisering måste organisationen skapa en uppsättning autentiseringsuppgifter på samma sätt som de använder API:t för [användarhantering](https://www.adobe.io/apis/experienceplatform/umapi-new.html).

![Verktyget för användarsynkronisering](/help/security/assets/ims5.png)

Verktyget för användarsynkronisering distribueras via Adobe Github-databasen [på den här platsen](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> En prerelease version **2.4RC1** finns tillgänglig med stöd för att skapa dynamiska grupper och finns [här](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

De viktigaste funktionerna i den här versionen är möjligheten att dynamiskt mappa nya LDAP-grupper för användarmedlemskap i Admin Console samt att skapa dynamiska användargrupper.

Mer information om de nya gruppfunktionerna finns [på den här platsen](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Dokumentation för användarsynkronisering**

Mer information finns i [UST-dokumentationen](https://adobe-apiplatform.github.io/user-sync.py/en/) .

Verktyget för användarsynkronisering måste registrera som ett UMAPI för en Adobe I/O-klient [här](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

Adobe I/O Console Documentation finns [här](https://www.adobe.io/apis/cloudplatform/console.html).

API:t för användarhantering som används av verktyget för användarsynkronisering beskrivs [här](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## Adobe Experience som en molntjänstkonfiguration {#aem-configuration}

> [!NOTE]
>
>Den AEM IMS-konfiguration som krävs konfigureras automatiskt när AEM-miljöer och instanser etableras. Administratören kan dock ändra den enligt sina krav med den metod som beskrivs [här](/help/implementing/deploying/overview.md).

Den AEM IMS-konfiguration som krävs konfigureras automatiskt när AEM-miljöer och instanser etableras.  Kundadministratörer kan ändra en del av konfigurationen enligt sina krav

Det övergripande tillvägagångssättet är att konfigurera Adobe IMS som OAuth-leverantör. Synkroniseringshanteraren **för** Apache Jackrabbit Oak kan ändras precis som för LDAP-synkronisering.

Nedan anges de viktigaste OSGI-konfigurationer som behöver ändras för att kunna ändra egenskaper som Automatiskt användarmedlemskap eller gruppmappningar.

<!-- Arun to provide list of osgi configs -->

## Så här använder du {#how-to-use}

### Hantera produkter och användaråtkomst i Admin Console {#managing-products-and-user-access-in-admin-console}

När produktadministratören loggar in på Admin Console visas flera instanser av produktkontexten för AEM Managed Services enligt nedan:

![Inloggning av instanser](/help/security/assets/ims6.png)

I det här exemplet har organisationen **AEM-MS-Onboard** 32 instanser som spänner över olika topologier och miljöer som Stage eller Prod.

![Inloggning för instanser2](/help/security/assets/ims7.png)

Under varje produktkontextinstans kommer det att finnas associerade produktprofiler. De här produktprofilerna används för att tilldela användare och grupper behörighet.

Profilen **Administrator_xxx** används för att ge administratörsbehörighet i den associerade AEM-instansen medan profilen **User_xxx** används för att lägga till vanliga användare.

Alla användare och grupper som läggs till under den här produktprofilen kan logga in på den aktuella instansen enligt exemplet nedan:

![Produktprofil](/help/security/assets/ims8.png)

### Logga in på Adobe Experience Manager som en molntjänst (#log-in-to-aem)

**Lokal administratörsinloggning**

AEM kan fortsätta att ha stöd för lokala inloggningar för administratörsanvändare. Inloggningsskärmen har ett alternativ för att logga in lokalt:

![Lokal inloggning](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**IMS-baserad inloggning**

För andra användare kan den IMS-baserade inloggningen användas när IMS har konfigurerats på instansen. Användaren klickar först på knappen Logga in med Adobe enligt nedan:

![IMS-inloggning](/help/security/assets/ims10.png)

De dirigeras sedan om till inloggningsskärmen för IMS och måste ange sina inloggningsuppgifter:

![IMS-inloggning2](/help/security/assets/ims11.png)

![IMS-inloggning3](/help/security/assets/ims12.png)

Om en federerad IDP konfigureras under den första konfigurationen av Admin Console kommer användaren att omdirigeras till kund-ID:t för enkel inloggning:

![IMS-inloggning4](/help/security/assets/ims13.png)

När autentiseringen är klar omdirigeras användaren tillbaka till AEM och loggas in:

![IMS-inloggning5](/help/security/assets/ims14.png)

### Hantera behörigheter och åtkomstkontrollistor i Adobe Experience Manager som en molntjänst {#managing-permissions-in-aem}

Åtkomstkontrollistorna och behörigheterna fortsätter att hanteras i AEM. Användargrupper som synkroniseras från IMS kan tilldelas lokala grupper där åtkomstkontrollistor och behörigheter definieras.

I exemplet nedan lägger vi till synkroniserade grupper i den lokala gruppen **Dam_Users** som exempel.

Användaren ingår i följande grupper i IMS:

![ACL1](/help/security/assets/ims15.png)

När användaren loggar in synkroniseras deras gruppmedlemskap enligt nedan:

![ACL2](/help/security/assets/ims16.png)

I AEM kan användargrupper som synkroniseras från IMS läggas till som medlemmar i befintliga lokala grupper, som **DAM-användare**.

![ACL3](/help/security/assets/ims17.png)

Som framgår nedan ärver gruppen **AEM-GRP_008** behörigheterna och behörigheterna för **DAM-användare**, vilket är ett effektivt sätt att hantera behörigheter för synkroniserade grupper och det används ofta även i den LDAP-baserade autentiseringsmetoden.

![ACL3](/help/security/assets/ims18.png)