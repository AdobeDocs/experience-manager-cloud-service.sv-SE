---
title: Nyheter och skillnader – Adobe Experience Manager as a Cloud Service
description: 'Nyheter och skillnader – Adobe Experience Manager (AEM) as a Cloud Service. '
translation-type: tm+mt
source-git-commit: 52e8cf1e3fb503c1d222a9543cfc1ddfe87132b6
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 90%

---


# Nyheter och skillnader {#what-is-new-and-what-is-different}

I många år har AEM varit tillgängligt:

* lokalt

* som hanterad tjänst

Det finns grundläggande skillnader mellan dessa tidigare metoder och AEM as a Cloud Service:

* [Arkitektur](#architecture)
* [Uppgraderingar](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Onboarding](#onboarding)
* [Utveckling](#developing)
* [Drift och prestanda](#operations-and-performance)
* [Identity Management](#identity-management)
* [Användargränssnitt för redigering](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Dessa översikter är inte uttömmande utan är avsedda som en introduktion.

>[!NOTE]
>
>Mer information om On-Premise- och Managed Service-versionerna finns i dokumentationen för [AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html).

## Arkitektur {#architecture}

>[!NOTE]
>
>Mer information finns i [Arkitektur](/help/core-concepts/architecture.md).

AEM as a Cloud Service har nu:

* En dynamisk arkitektur med ett varierande antal AEM-bilder.

![Dynamisk arkitektur](assets/introduction-03.png "Dynamisk arkitektur")

Arkitekturen:

* Skalas baserat på den *faktiska* trafiken och den *faktiska* aktiviteten.

* Har enskilda instanser som bara körs vid behov.

* Använder modulära program.

* Har ett redigeringskluster som standard och på så sätt undviks driftavbrott vid underhåll.

Det möjliggör automatisk skalning för olika användningsmönster:

![Automatisk skalning för olika användningsmönster](assets/introduction-04.png "Automatisk skalning för olika användningsmönster")


## AEM {#aem-updates}

>[!NOTE]
>Mer information finns i [AEM versionsuppdateringar](/help/implementing/deploying/aem-version-updates.md).

AEM som Cloud Service använder nu Continuous Integration och Continuous Delivery (CI/CD) för att säkerställa att dina projekt finns i den senaste AEM versionen. Det innebär att instanser av Production och Stage uppdateras till den senaste AEM utan att tjänsten avbryts för användarna.

>[!NOTE]
> Om uppdateringen till produktionsmiljön misslyckas kommer Cloud Manager automatiskt att återställa scenmiljön. Detta görs automatiskt för att säkerställa att både fas- och produktionsmiljöer har samma AEM när uppdateringen är klar.

AEM versionsuppdateringar är av två typer:

* **AEM Push-uppdateringar**

   * Kan släppas dagligen.
   * Mest underhållet, inklusive de senaste felkorrigeringarna och säkerhetsuppdateringarna.

      Eftersom ändringarna utförs regelbundet blir effekten inkrementell vilket minskar påverkan på tjänsten.

* **Nya funktionsuppdateringar**

   * Frisläppt via ett förutsägbart månadsschema.

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager är en viktig del av den kontinuerliga uppgraderingsstrategin för AEM as a Cloud Service eftersom det styr alla uppdateringar av dina instanser och detta är obligatoriskt.

Uppdateringar kan utlösas av Adobe när en ny version av Cloud Service är tillgänglig. Du kan även utlösa programuppdateringar med de pipelines som finns i Cloud Manager.

Cloud Manager:

* används för att hantera AEM-program och -miljöer,

* är en viktig komponent i AEM as a Cloud Service och varje ny klientorganisation etableras först för Cloud Manager-åtkomst,

* är en central startpunkt för drift- och utvecklingspersonal.

Antal och typer av AEM-program som kan skapas via Cloud Manager beror på:

* kundens licensavtal,

* interna aktörer när AEM as a Cloud Service används för aktivering eller utbildning,

* externa processer som provversioner som startas från Adobe.com.

Cloud Manager har utvecklats till en självbetjäningsportal där huvudkomponenterna i AEM as a Cloud Service kan skapas och konfigureras:

* Skapa och hantera nya program. Mer information finns i [Förstå program och programtyper](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) .

* Skapa och hantera AEM-miljöer i dessa program. Mer information finns i [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) .

* Skapa och hantera pipelines för distribution av kundkoden och den relaterade konfigurationen för en viss miljö. Mer information finns i [Konfigurera CI-CD-pipeline](/help/implementing/cloud-manager/configure-pipeline.md) .

* Meddelas om viktiga livscykelhändelser för dessa komponenter (t.ex. produktuppdateringar).

För närvarande kan Cloud Manager skapa miljöer i tre geografiska regioner (fler regioner kommer):

* USA (öst)

* EMEA (Nederländerna)

* APAC (Australien)

>[!NOTE]
>Använd [Experience Manager som Cloud Service](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md) för att komma igång med Cloud Manager i AEM som Cloud Service.

## Onboarding {#onboarding}

>[!NOTE]
>
>Mer information finns i [Onboarding](/help/onboarding/home.md).

Att starta och hantera ett AEM-projekt är enkelt när du använder AEM as a Cloud Service eftersom Adobe ansvarar för många aspekter:

* AEM-baslinjebilder optimeras för specifika användningsområden.

* Många av de manuella konfigurationsåtgärderna är överflödiga.

En annan viktig skillnad är att det nu finns:

* En utvärderingsfas som säkerställer att alla krav är uppfyllda, bland annat:

   * Juridiska krav

   * Avtalsvillkor

   * Tekniska krav för befintligt innehåll och/eller kod som kunden anpassat

* Distributionskrav:

   * Koduppdateringar, alla kundprogram som utvecklats för en tidigare version av AEM måste granskas och eventuellt uppdateras.

   * Migrering av innehåll

## Utveckling {#developing}

>[!NOTE]
>
>Mer information finns i [Utvecklingsriktlinjer](/help/implementing/developing/introduction/development-guidelines.md) och [Utveckling – WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

Den nya arkitekturen som stöder AEM as a Cloud Service inbegriper några viktiga förändringar av den övergripande utvecklingsupplevelsen. Ett av de främsta målen för AEM as a Cloud Service är att göra det möjligt för erfarna kunder (som har använt AEM antingen lokalt eller i Adobe Managed Services) att migrera till AEM as a Cloud Service så snabbt som möjligt, utan att behöva skriva om en stor mängd av den anpassade koden. Vissa justeringar kan dock fortfarande behövas.

### Molnutveckling {#aem-as-a-cloud-service-developing-cloud-development}

För att befintliga AEM-program ska kunna köras på AEM as a Cloud Service måste följande steg utföras:

* Programkoden och konfigurationen måste lagras i Git-koddatabasen för det associerade Cloud Manager-programmet.
* Programkoden och konfigurationen måste vara kompatibel med den senaste versionen av AEM-baslinjebilden (som kan ändras dagligen).
   * Kundprogrammet måste byggas och distribueras med den Cloud Manager-pipeline som är kopplad till Cloud Manager-miljön.
* Kundprogrammet måste klara alla krav på kodkvalitet, säkerhet och prestanda som används i pipelinen.
* De bilder som skapas för kundprogrammet måste distribueras via Cloud Manager-pipelinen.

Den här processen kallas vanligtvis för Cloud-first-utveckling. Eftersom längden från början till slut förväntas ta några minuter (från 20 till 50 beroende på programmets komplexitet), måste snabba utvecklingsmetoder användas innan den väntande koden och konfigurationen ändras i molnet.

Web Console, där OSGI-paket och tillhörande konfigurationer hanteras och som tidigare ingick i AEM QuickStart, är inte längre åtkomlig för användare med AEM as a Cloud Service. Gränssnittet kan fortfarande nås i skrivskyddat läge via den nya utvecklarkonsolen. Med den här konsolen kan utvecklare välja och logga in direkt på en viss nod i en redigerings- eller publiceringstjänst och sedan komma åt de områden som blockerats som standard.

>[!NOTE]
>
>Se även [OSGi-konfiguration](/help/implementing/deploying/overview.md#osgi-configuration)

Ett annat vanligt behov hos utvecklare är snabb åtkomst till loggfilerna i olika miljöer. Med AEM as a Cloud Service blir loggfilerna för de olika noderna i redigerings- och publiceringsnoderna tillgängliga via Cloud Manager i form av filer som kan hämtas eller via API:er.

På grund av den tydliga åtskillnaden mellan kod och innehåll kan utvecklare använda en viss process för att uppdatera innehåll som en del av en distribution. De typiska användningsområdena för innehåll som kan ändras är:

* *Standardinnehåll* som ingår i kundprojektet (t.ex. mappar, mallar, arbetsflöden)

* Definitioner för sökindex

* Listor för åtkomstkontroll och behörighet

* Tjänstanvändare och användargrupper

### Lokal utveckling {#aem-as-a-cloud-service-developing-local-development}

För att stödja snabba iterationer och utveckling är det också möjligt att utveckla AEM-program utanför AEM as a Cloud Service. För detta ändamål finns följande artefakter tillgängliga för utvecklare:

* Snabbstart för AEM as a Cloud Service: ett `.jar`-baserat, fristående installationsprogram för den senaste AEM-kodbasen med samma funktionalitet och API-område.

* Dispatcher SDK för AEM as a Cloud Service: en bildbaserad process för att testa och validera Dispatcher-konfigurationer lokalt

>[!NOTE]
>
>Observera att en del AEM Sites- och AEM Assets-funktioner inte har stöd i Cloud QuickStart. Det består av en enkel redigeringsmiljö där de flesta tillägg kan utvecklas och testas.

## Drift och prestanda {#operations-and-performance}

>[!NOTE]
>
>Du får mer information om du börjar med [säkerhetskopiering](/help/operations/backup.md), [indexering](/help/operations/indexing.md) och [andra underhållsåtgärder](/help/operations/maintenance.md).

Med AEM as a Cloud Service automatiseras sådana åtgärder så att tjänsten inte längre behöver avbrytas.

Det innebär att:

* Många uppgifter har automatiserats.

* Topologier är optimerade för maximal återhämtningsförmåga och effektivitet, till exempel är binärfri replikering standard.

* Tunga uppgifter, som köer, jobb och gruppbearbetning, har flyttats från den centrala AEM-instansen för att hanteras av delade och dedikerade mikrotjänster.

AEM as a Cloud Service stöds också av en ny infrastruktur för övervakning, rapportering och varningar. Detta gör att Adobe SRE:er (Site Reliability Engineers) proaktivt kan underhålla tjänsten. Arkitekturens olika delar är utrustade med en rad olika hälsokontroller. Om en viss nod i arkitekturen av någon anledning inte anses vara felfri tas den bort från tjänsten och ersätts i tysthet med en ny, felfri nod.

## Identity Management {#identity-management}

>[!NOTE]
>
>Mer information finns i [Säkerhet – IMS-stöd](/help/security/ims-support.md).

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön.

Det innebär att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) måste användas för att hantera användare och användargrupper. Med användarkonton kan användarna få tillgång till Adobes produkter och tjänster eftersom användarprofilinformationen centraliseras i Adobe Identity Management System (IMS) och delas över alla Cloud Services. När användarkonton fått åtkomst till AEM, refereras de i AEM as a Cloud Service (som tidigare); till exempel för att definiera roller och behörigheter via användargränssnitten i AEM Security.

Det kombinerar fördelarna med:

* Adobe Identity Management System (IMS) som används för enkel inloggning i alla Adobes molnprogram.

* Användarinställningarna är fortfarande lokala för varje instans av AEM as a Cloud Service.

## Användargränssnitt för redigering {#authoring-user-interface}

>[!NOTE]
>
>Mer information finns till att börja med i [Grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md).

De grundläggande principerna i redigeringsgränssnittet för Sites och Assets är välbekanta för alla som har använt AEM tidigare.

Den största skillnaden är att användargränssnittet är helt pekskärmskompatibelt och det klassiska användargränssnittet inte längre är tillgängligt. I övrigt är grunderna oförändrade med endast små synliga ändringar.

## AEM Sites {#aem-sites}

Med Adobe Experience Manager Sites as a Cloud Service kan ni ge kunderna anpassade, innehållsledda upplevelser genom att kombinera kraften i AEM:s innehållshanteringssystem med AEM:s digitala resurshantering.

Mer information finns i översikten över [Ändringar i Sites](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service är en molnbaserad SaaS-lösning som företag kan använda för att snabbt och effektivt hantera digitala resurser och dynamiska medier. De får även tillgång till nästa generations smarta funktioner, som artificiell intelligens/maskininlärning, i ett system som alltid är aktuellt, alltid tillgängligt och alltid lär sig.

Assets inkluderar nästa generations materialbearbetning i molnet samt högpresterande materialimport och sökning.

Mer information finns i [Översikt och introduktion till Assets as a Cloud Service](/help/assets/overview.md).

## Lär känna Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Mer information finns i:

* [En introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* [Arkitekturen](/help/core-concepts/architecture.md) i Adobe Experience Manager as a Cloud Service
* [Viktiga ändringar i AEM as a Cloud Service (versionsinformation)](/help/release-notes/aem-cloud-changes.md)
* [Viktiga ändringar i AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Viktiga ändringar i AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Nu kommer AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Självstudiekurser om Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
