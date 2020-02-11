---
title: Vad är annorlunda och vad är nytt - Adobe Experience Manager som en molntjänst
description: 'Vad är annorlunda och vad är nytt - Adobe Experience Manager (AEM) som en molntjänst. '
translation-type: tm+mt
source-git-commit: b9a32b3ac4c296f4bb02e9a590c1b3e22d53f562

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

<!-- * [Miscellaneous](#miscellaneous) -->

## Arkitektur {#architecture}

>[!NOTE]
>
>Mer information finns i [Arkitektur](/help/core-concepts/architecture.md).

### Tidigare versioner {#previous-versions-architecture}

Både AEM lokalt och AEM under Managed Services använde en statisk arkitektur som består av ett fast antal datorer och instanser.

![Statisk](assets/introduction-01.png "arkitekturStatisk arkitektur")

Dessa:

* De har anpassats för *topptrafik* (internet) och *toppaktivitet* (marknadsföring), vilket resulterade i att de var inaktiva under betydande tidsperioder:
   ![Statisk struktur måste ta hänsyn till varierande](assets/introduction-02.png "användningsmönsterStatisk struktur måste ta hänsyn till varierande användningsmönster")

* var monolitiska applikationer (snabbstart).

* hade en enda författarinstans, som var föremål för driftstopp under underhållsperioden.

### AEM som molntjänst {#aem-as-a-cloud-service-architecture}

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

<!--
>[!NOTE]
>
>For further details see the [Deploying Introduction](/help/sites/deploying/introduction.md).
-->

### Tidigare versioner {#previous-versions-upgrades}

Både AEM på plats och AEM under Managed Services var föremål för ett fast mönster i en årlig större version som utökades med Service Pack, funktionspaket och snabbkorrigeringar. Ibland körs en större version i två eller flera år.

Beroende på typ av uppgradering kan processen kräva betydande förberedelser, bestående av analys, utveckling och testning, följt av ett tidsfönster för den faktiska uppgraderingen.

### AEM som molntjänst {#aem-as-a-cloud-service-upgrades}

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

* från kundlicensavtalet, [Shankari- vi kan inte nämna krediter]

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

<!--
>[!NOTE]
>
>For further details see [Onboarding - An Overview](/help/onboarding/overview.md).
-->

### Tidigare versioner {#previous-versions-onboarding}

Implementeringen av ett AEM-projekt följer i princip traditionella metoder för projekthantering.

### AEM som molntjänst {#aem-as-a-cloud-service-onboarding}

Att starta och hantera ett AEM-projekt är mycket enklare när du använder AEM som en molntjänst eftersom Adobe ansvarar för många aspekter:

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
>Mer information finns i dokumentationen till [riktlinjerna](/help/implementing/developing/introduction/development-guidelines.md) för utveckling.

<!--
>[!NOTE]
>
>For further details start with [The Developing Experience](/help/sites/developing/introduction/developer-experience.md, [Developing - The Basics](/help/sites/developing/introduction/the-basics.md) and [Developing Best Practices](/help/sites/best-practices/developing.md).
-->

### Tidigare versioner {#previous-versions-developing}

<!-- needs more detail -->
Utvecklingen var en intensiv uppgift som utfördes lokalt, följt av distribution till produktionsinstansen.

### AEM som molntjänst {#aem-as-a-cloud-service-developing}

<!-- Will need information for new customers -->
Den nya arkitekturen som stöder AEM som en molntjänst inbegriper några viktiga förändringar av den övergripande utvecklingsupplevelsen. Ett av de främsta målen för AEM som molntjänst är att göra det möjligt för erfarna kunder (som har använt AEM antingen lokalt eller i Adobe Managed Services) att migrera till AEM som molntjänst så snabbt som möjligt, utan att behöva skriva om huvuddelen av den anpassade koden. Vissa justeringar kan dock fortfarande behövas.

#### Molnutveckling {#aem-as-a-cloud-service-developing-cloud-development}

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

#### Lokal utveckling {#aem-as-a-cloud-service-developing-local-development}

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

### Tidigare versioner {#previous-versions-operations-and-performance}

Tidigare, särskilt på författarsidan, fanns det ett behov av att regelbundet stoppa en instans. för rutinmässig underhållsverksamhet samt uppgraderingar och uppdateringar. För vissa kunder resulterade detta i timmar av schemalagda driftstopp varje vecka.

### AEM som molntjänst {#aem-as-a-cloud-service-operatioms-and-performance}

Med AEM som molntjänst automatiseras sådana åtgärder så att inga avbrott i tjänsten behövs längre.

Inom dessa områden:

* Många uppgifter har automatiserats.

* Topologier är optimerade för maximal motståndskraft och effektivitet. Bindesign-less-replikering är till exempel standard.

* Kraftfulla uppgifter, som köer, jobb och gruppbearbetning, har flyttats från den centrala AEM-instansen för att hanteras av delade och dedikerade mikrotjänster.

Åtgärder för AEM som molntjänst stöds också av en ny infrastruktur för övervakning, rapportering och varningar. Detta gör att Adobe SRE:er (Site Reliable Engineers) proaktivt kan hålla tjänsten frisk. Arkitekturens olika delar är utrustade med en rad olika hälsokontroller. Om en viss nod i arkitekturen av någon anledning inte anses vara felfri tas den bort från tjänsten och ersätts i tysthet med en ny, felfri nod.

## Identitetshantering {#identity-management}

<!--
>[!NOTE]
>
>For further details see [Security - Single Sign-On](/help/sites/security/single-sign-on.md).
-->

### Tidigare versioner {#previous-versions-identity-management}

Som standard var identitetshanteringen intern för AEM.

>[!NOTE]
>
>AEM 6.4.3.0 introducerade:
>
>* Stöd för Admin Console för AEM-instanser.
>* Adobe IMS-baserad autentisering (Identity Management System) för kunder med AEM Managed Services.


### AEM som molntjänst {#aem-as-a-cloud-service-identity-management}

En stor förändring av AEM som en molntjänst är den helintegrerade användningen av Adobe ID:n för att komma åt författarnivån.

Detta kräver att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) används för att hantera användare och användargrupper. Med användarkontona kan användarna få tillgång till Adobes produkter och tjänster, eftersom användarprofilinformation centraliseras i Adobe Identity Management System (IMS) och delas över alla molntjänster. När AEM tilldelats åtkomst kan användarkontona refereras i AEM som en molntjänst (som tidigare); till exempel för att definiera roller och behörigheter från användargränssnitten i AEM Security.

Detta kombinerar fördelarna med:

* Använda Adobe Identity Management System (IMS) för enkel inloggning i alla Adobe-molnprogram.

* Användarinställningarna är fortfarande lokala för varje instans av AEM som en molntjänst.

## Användargränssnitt för redigering {#authoring-user-interface}

<!--
>[!NOTE]
>
>For further details, the [Basic Handling](/help/sites/authoring/getting-started/basic-handling.md) and [Best Practices](/help/sites/best-practices/authoring.md) are good starting points.
-->

### Tidigare versioner {#previous-versions-authoring}

Användargränssnittet för författarinstansen (UI), för både Sites och Assets, utvecklades och optimerades för att passa alla användningsfall, med både det beröringskänsliga och klassiska användargränssnittet.

### AEM som molntjänst {#aem-as-a-cloud-service-authoring}

De grundläggande principerna för användargränssnittet, för både Sites och Assets, kommer att vara mycket välkända för alla som har använt AEM tidigare.

Den största skillnaden är att användargränssnittet är helt beröringskänsligt. det klassiska användargränssnittet är inte längre tillgängligt. I annat fall förblir grunderna oförändrade, med endast små ändringar synliga.

## AEM Sites {#aem-sites}

Med Adobe Experience Manager Sites som en molntjänst kan ni ge kunderna personaliserade, innehållsledda upplevelser genom att kombinera kraften i AEM Content Management System med AEM Digital Asset Management.

Mer information finns i översikten över [Ändringar av platser](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets som en molntjänst erbjuder en inbyggd SaaS-lösning i molnet som gör att företag inte bara kan utföra sina Digital Asset Management- och Dynamic Media-åtgärder snabbt och effektivt, utan även använda nästa generations smarta funktioner, som AI/ML, inifrån ett system som alltid är aktuellt, alltid tillgängligt och alltid är inlärningsbart.

Resurserbjudandet omfattar nästa generation av mediehantering i molnet samt högpresterande tillgångsinmatning och sökning.

Mer information finns i [översikt och introduktion till Assets som en molntjänst](/help/assets/overview.md).


