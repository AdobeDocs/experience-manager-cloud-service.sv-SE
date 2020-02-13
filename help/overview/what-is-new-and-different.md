---
title: Vad är annorlunda och vad är nytt - Adobe Experience Manager som en molntjänst
description: 'Vad är annorlunda och vad är nytt - Adobe Experience Manager (AEM) som en molntjänst. '
translation-type: tm+mt
source-git-commit: b8eed5bd68d961a95d0ed15a4e88cee327a82594

---


# Vad är nytt och vad är annorlunda? {#what-is-new-and-what-is-different}

I många år har AEM varit tillgängligt för båda:

* Lokal

* som en hanterad tjänst

Det finns inneboende skillnader mellan dessa tidigare metoder och AEM som molntjänst:

* [Arkitektur](#architecture)
* [Uppgraderingar](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Onboarding](#onboarding)
* [Utvecklar](#developing)
* [Drift och prestanda](#operations-and-performance)
* [Identitetshantering](#identity-management)
* [Användargränssnitt för redigering](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Dessa översikter är inte uttömmande, men är avsedda att utgöra en introduktion.

<!-- change link when 6.5 hub page migrated -->

>[!NOTE]
>
>Mer information om On-Premise och Managed Service finns i dokumentationen för [AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html).

## Arkitektur {#architecture}

>[!NOTE]
>
>Mer information finns i [Arkitektur](/help/core-concepts/architecture.md).

<!--
### Previous Versions {#previous-versions-architecture}

Both AEM on-premise, and AEM under Managed Services used a static architecture comprised of a fixed number of machines and instances. 

![Static architecture](assets/introduction-01.png "Static architecture")

These:

* Were sized for *peak* traffic (internet) and *peak* activity (marketing), which resulted in them being idle for significant periods of time:
![Static structure must cater for varying usage patterns](assets/introduction-02.png "Static structure must cater for varying usage patterns")

* Were monolithic applications (the quickstart).

* Had a single author instance; which was subject to downtime during maintenance windows.

### AEM as a Cloud Service {#aem-as-a-cloud-service-architecture}
-->

AEM som molntjänst har nu:

* En dynamisk arkitektur med ett varierande antal AEM-bilder.

![Dynamisk](assets/introduction-03.png "arkitekturDynamisk arkitektur")

Arkitekturen:

* Skalas baserat på den *faktiska* trafiken och den *faktiska* aktiviteten.

* Har enskilda instanser som bara körs vid behov.

* Använder modulära program.

* Har ett författarkluster som standard; På så sätt undviker du driftavbrott för underhållsåtgärder.

Detta möjliggör autoskalning för olika användningsmönster:

![Automatisk skalning för olika](assets/introduction-04.png "användningsmönsterAutomatisk skalning för olika användningsmönster")


## Uppgraderingar {#upgrades}

>[!NOTE]
>
>Mer information finns i Introduktion till [distribution](/help/implementing/deploying/overview.md).

<!--
### Previous Versions {#previous-versions-upgrades}

Both AEM on-premise, and AEM under Managed Services were subject to a fixed pattern of a yearly major release augmented by service packs, feature packs and hot-fixes. Often instances would run a major version for two or more years. 

Depending on the upgrade type, the process could require significant preparation consisting of analysis, development and testing, followed with a window of downtime for the actual upgrade.

### AEM as a Cloud Service {#aem-as-a-cloud-service-upgrades}
-->

AEM som molntjänst använder nu kontinuerlig integrering och kontinuerlig leverans (CI/CD) för att säkerställa att dina projekt är helt uppdaterade. Detta innebär att alla uppgraderingsåtgärder är helt automatiserade, så du behöver inte avbryta tjänsten för användarna.

Adobe ansvarar aktivt för att uppdatera alla driftsinstanser av tjänsten till den senaste versionen av AEM-kodbasen:

* Felkorrigeringar:

   * Kan frisläppas dagligen.

   * Instanser uppdateras ofta med de senaste felkorrigeringarna. I takt med att ändringarna utförs regelbundet blir effekten inkrementell, vilket minskar påverkan på tjänsten.

   * De flesta uppdateringar är av underhålls- och säkerhetsskäl.

* Nya funktioner:

   * Kommer att släppas enligt ett förutsägbart månadsschema.

>[!NOTE]
>
>Mer information finns i [Distributionsarkitektur](/help/core-concepts/architecture.md#deployment-architecture).

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager är en väsentlig del av AEM:s kontinuerliga uppgraderingsstrategi som en molntjänst, eftersom det styr alla uppdateringar av dina instanser - detta är obligatoriskt.

Uppdateringar kan utlösas av Adobe när en ny version av molntjänsten är tillgänglig. Du kan även utlösa programuppdateringar med hjälp av de rörledningar som finns i Cloud Manager.

Cloud Manager är:

* används för att hantera AEM-program och -miljöer,

* en viktig komponent i AEM som en molntjänst, varje ny klientorganisation först etableras för Cloud Manager-åtkomst,

* en enda startpunkt för er drift- och utvecklingspersonal.

Antalet och typen av AEM-program som kan skapas från Cloud Manager kommer antingen från:

* från kundlicensavtalet,

* från interna aktörer när AEM som molntjänst används för aktivering, eller utbildning,

* från externa processer som testversioner från Adobe.com.

Cloud Manager har utvecklats till en självbetjäningsportal där huvudkomponenterna i AEM som molntjänst kan skapas och konfigureras:

* Skapa och hantera nya program.

* Skapa och hantera AEM-miljöer i dessa program.

* Skapa och hantera pipelines för distribution av kundkoden och den relaterade konfigurationen till en viss miljö.

* Meddelas om viktiga livscykelhändelser för dessa komponenter (t.ex. produktuppdateringar).

För närvarande kan Cloud Manager skapa miljöer i tre geografiska regioner (med fler regioner efter):

* USA (öst)

* EMEA (Nederländerna)

* APAC (Australien)

## Onboarding {#onboarding}

>[!NOTE]
>
>Mer information finns i [Onboarding](/help/onboarding/home.md).

<!--
### Previous Versions {#previous-versions-onboarding}

Implementing an AEM project basically followed traditional project management methods.  

### AEM as a Cloud Service {#aem-as-a-cloud-service-onboarding}

Starting and managing an AEM project is significantly easier when using AEM as a Cloud service as Adobe is responsible for many aspects:
-->

Att starta och hantera ett AEM-projekt är enkelt när man använder AEM som en molntjänst eftersom Adobe ansvarar för många aspekter:

* Baslinje-AEM-bilder är optimerade för specifika användningsområden.

* Många av de manuella konfigurationsåtgärderna har blivit redundanta.

Det är också mycket annorlunda nu:

* En bedömningsfas för att säkerställa att alla krav är uppfyllda. bl.a. följande:

   * Juridiska krav

   * Kontraktsavtal

   * Tekniska krav för befintligt innehåll och/eller kod som kunden anpassat

* Distributionskrav:

   * Koduppdateringar. Alla kundapplikationer som utvecklats för en tidigare version av AEM måste granskas och uppdateras.

   * Migrering av innehåll

## Utvecklar {#developing}

>[!NOTE]
>
>Mer information finns i [Utvecklingsriktlinjer](/help/implementing/developing/introduction/development-guidelines.md) och [Utvecklingsprogram - WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

<!--
### Previous Versions {#previous-versions-developing}
-->

<!-- needs more detail -->

<!-- 
Development was an intensive task performed locally, followed by deployment to the production instance. 

### AEM as a Cloud Service {#aem-as-a-cloud-service-developing}
-->

<!-- Will need information for new customers -->
Den nya arkitekturen som stöder AEM som en molntjänst inbegriper några viktiga förändringar av den övergripande utvecklingsupplevelsen. Ett av de främsta målen för AEM som molntjänst är att göra det möjligt för erfarna kunder (som har använt AEM antingen lokalt eller i Adobe Managed Services) att migrera till AEM som molntjänst så snabbt som möjligt, utan att behöva skriva om huvuddelen av den anpassade koden. Vissa justeringar kan dock fortfarande behövas.

<!-- adjusting title level -->

### Molnutveckling {#aem-as-a-cloud-service-developing-cloud-development}

För att befintliga AEM-program ska kunna köras på AEM som en molntjänst förväntas följande steg:

* Programkoden och konfigurationen måste lagras i Git-koddatabasen för det associerade Cloud Manager-programmet.
* Programkoden och konfigurationen måste vara kompatibla med den senaste versionen av AEM-originalbilden (som kan ändras dagligen).
   * Kundprogrammet måste byggas och distribueras med den molnhanterarpipeline som är kopplad till Cloud Manager-miljön.
* Kundprogrammet måste klara alla kodkvalitets-, säkerhets- och prestandagränser som används i pipeline.
* De bilder som har skapats för kundprogrammet måste distribueras via molnhanterarens pipeline.

<!-- duration of what? -->
Den här processen kallas vanligtvis för utveckling i molnet först. Eftersom längden från början till slut förväntas ta några minuter (från 20 till 50 beroende på programmets komplexitet), är det nödvändigt att använda snabba utvecklingsmetoder innan det görs ett försök att utföra väntande kodändringar och konfigurationsändringar i molnet.

<!-- is this really relevant at this point? -->
Webbkonsolen, där OSGI-paket och tillhörande konfigurationer hanteras, och tidigare ingår i AEM QuickStart, är inte längre direkt tillgänglig för användare av en AEM som en molntjänstmiljö. Gränssnittet kan fortfarande nås i skrivskyddat läge med en ny utvecklarkonsol. Med den här konsolen kan utvecklare välja och logga in direkt på en viss nod i en författare eller publiceringstjänst och sedan komma åt de områden som blockerats som standard.

Ett annat vanligt krav för utvecklare är snabb åtkomst till loggfilerna i olika miljöer. Med AEM som molntjänst blir loggfilerna för de olika noderna i författaren och publiceringsnoderna tillgängliga via molnhanteraren, antingen i form av filer som kan hämtas eller via API:er.

På grund av den tydliga åtskillnaden mellan kod och innehåll kan utvecklare använda en viss process för att uppdatera innehåll som en del av en distribution. De typiska användningsområdena för muterbart innehåll är:

* Standardinnehåll *som* ingår i kundprojektet (t.ex. mappar, mallar, arbetsflöden)

* Sök i indexdefinitioner

* Behörighetslistor

* Tjänstanvändare och användargrupper

<!-- adjusting title level -->

### Lokal utveckling {#aem-as-a-cloud-service-developing-local-development}

För att stödja snabba iterationer och utveckling är det också möjligt att utveckla AEM-program utanför AEM som en molntjänst. För detta ändamål görs följande artefakter tillgängliga för utvecklarna:

* Snabbstart för AEM som molntjänst: ett `.jar` baserat, fristående installationsprogram för den senaste AEM-kodbasen med samma funktionalitet och API-yta.

* AEM som en Cloud Service Dispatcher SDK: en bildbaserad process för att testa och validera Dispatcher-konfigurationer lokalt

>[!NOTE]
>
>Observera att molnet för QuickStart inte tillåter alla AEM Sites- och AEM Assets-funktioner. Det består av en enkel författarmiljö där de flesta tilläggen kan utvecklas och testas.

## Drift och prestanda {#operations-and-performance}

>[!NOTE]
>
>Mer information får du från [Säkerhetskopiering](/help/operations/backup.md), [indexering](/help/operations/indexing.md)och [andra underhållsåtgärder](/help/operations/maintenance.md).

<!--
### Previous Versions {#previous-versions-operations-and-performance}

In the past, especially on the author side, there was a need to periodically stop an instance; for routine maintenance operations, as well as upgrades and updates. For some customers, this resulted in hours of scheduled downtime on a weekly basis. 

### AEM as a Cloud Service {#aem-as-a-cloud-service-operatioms-and-performance}
-->

Med AEM som molntjänst automatiseras sådana åtgärder så att inga avbrott i tjänsten behövs längre.

Inom dessa områden:

* Många uppgifter har automatiserats.

* Topologier är optimerade för maximal motståndskraft och effektivitet. Bindesign-less-replikering är till exempel standard.

* Kraftfulla uppgifter, som köer, jobb och gruppbearbetning, har flyttats från den centrala AEM-instansen för att hanteras av delade och dedikerade mikrotjänster.

Åtgärder för AEM som molntjänst stöds också av en ny infrastruktur för övervakning, rapportering och varningar. Detta gör att Adobe SRE:er (Site Reliable Engineers) proaktivt kan hålla tjänsten frisk. Arkitekturens olika delar är utrustade med en rad olika hälsokontroller. Om en viss nod i arkitekturen av någon anledning inte anses vara felfri tas den bort från tjänsten och ersätts i tysthet med en ny, felfri nod.

## Identitetshantering {#identity-management}

>[!NOTE]
>
>Mer information finns i [Säkerhet - IMS-stöd](/help/security/ims-support.md).

<!--
### Previous Versions {#previous-versions-identity-management}

By default, identity management was internal to AEM.

>[!NOTE]
>
>AEM 6.4.3.0 introduced:
>
>* Admin Console support for AEM instances. 
>* Adobe IMS (Identity Management System) based authentication for AEM Managed Services customers.

### AEM as a Cloud Service {#aem-as-a-cloud-service-identity-management}
-->

En stor förändring av AEM som en molntjänst är den helintegrerade användningen av Adobe ID:n för att komma åt författarnivån.

Detta kräver att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) används för att hantera användare och användargrupper. Med användarkontona kan användarna få tillgång till Adobes produkter och tjänster, eftersom användarprofilinformation centraliseras i Adobe Identity Management System (IMS) och delas över alla molntjänster. När AEM tilldelats åtkomst kan användarkontona refereras i AEM som en molntjänst (som tidigare); till exempel för att definiera roller och behörigheter från användargränssnitten i AEM Security.

Detta kombinerar fördelarna med:

* Använda Adobe Identity Management System (IMS) för enkel inloggning i alla Adobe-molnprogram.

* Användarinställningarna är fortfarande lokala för varje instans av AEM som en molntjänst.

## Användargränssnitt för redigering {#authoring-user-interface}

>[!NOTE]
>
>Mer information finns i [Grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md) .

<!--
### Previous Versions {#previous-versions-authoring}

The user interface of the author instance (UI), for both Sites and Assets, was progressively developed and optimized to cater for all use-cases, using both the touch-enabled and classic UIs.

### AEM as a Cloud Service {#aem-as-a-cloud-service-authoring}
-->

De grundläggande principerna för användargränssnittet, för både Sites och Assets, kommer att vara mycket välkända för alla som har använt AEM tidigare.

Den största skillnaden är att användargränssnittet är helt beröringskänsligt. det klassiska användargränssnittet är inte längre tillgängligt. I annat fall förblir grunderna oförändrade, med endast små ändringar synliga.

## AEM Sites {#aem-sites}

Med Adobe Experience Manager Sites som en molntjänst kan ni ge kunderna personaliserade, innehållsledda upplevelser genom att kombinera kraften i AEM Content Management System med AEM Digital Asset Management.

Mer information finns i översikten över [Ändringar av platser](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets som en molntjänst erbjuder en inbyggd SaaS-lösning i molnet som gör att företag inte bara kan utföra sina Digital Asset Management- och Dynamic Media-åtgärder snabbt och effektivt, utan även använda nästa generations smarta funktioner, som AI/ML, inifrån ett system som alltid är aktuellt, alltid tillgängligt och alltid är inlärningsbart.

Resurserbjudandet omfattar nästa generation av mediehantering i molnet samt högpresterande tillgångsinmatning och sökning.

Mer information finns i [översikt och introduktion till Assets som en molntjänst](/help/assets/overview.md).
