---
title: Hur konfigurerar jag en lokal utvecklingsmiljö för AEM Forms?
description: Konfigurera en lokal utvecklingsmiljö för Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 0%

---

# Konfigurera lokal utvecklingsmiljö för AEM Forms {#overview}

När du konfigurerar och konfigurerar en [!DNL &#x200B; Adobe Experience Manager Forms] som en [!DNL &#x200B; Cloud Service]-miljö konfigurerar du utvecklings-, staging- och produktionsmiljöer i molnet. Dessutom kan du konfigurera och konfigurera en lokal utvecklingsmiljö.

Du kan använda den lokala utvecklingsmiljön för att utföra följande åtgärder utan att logga in i molnutvecklingsmiljön:

* [Skapa formulär](creating-adaptive-form.md) och relaterade resurser (teman, mallar, anpassade överföringsåtgärder med mera)
* [Konvertera PDF forms till adaptiv Forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)
* Bygg program för att generera [kundkommunikation](aem-forms-cloud-service-communications-introduction.md) vid behov eller i gruppläge.

När ett adaptivt formulär eller relaterade resurser är klara på den lokala utvecklingsinstansen eller ett program för att generera [kundkommunikation] är klart, kan du exportera det adaptiva formuläret eller kundkommunikationsprogrammet från den lokala utvecklingsmiljön till en Cloud Service-miljö för ytterligare testning eller för att gå över till produktionsmiljöer.

Du kan också utveckla och testa anpassad kod som anpassade komponenter och förifyllningstjänst i den lokala utvecklingsmiljön. När den anpassade koden har testats och är klar kan du använda Git-databasen i din Cloud Service-utvecklingsmiljö för att distribuera den anpassade koden.

Om du vill konfigurera en ny lokal utvecklingsmiljö och använda den för att utveckla aktiviteter utför du följande åtgärder i listordning:

* [Konfigurera utvecklingsverktyg](#setup-development-tools-for-AEM-projects)

* [Konfigurera lokala författarinstanser och publiceringsinstanser](#set-up-local-experience-manager-environment-for-development)

* [Lägg till Forms-arkiv i lokala utvecklingsinstanser och konfigurera användare](#add-forms-archive-configure-users)

* [Konfigurera lokal utvecklingsmiljö för mikrotjänster](#docker-microservices)

* [Konfigurera ett utvecklingsprojekt](#forms-cloud-service-local-development-environment)

* [Konfigurera lokala Dispatcher-verktyg](#setup-local-dispatcher-tools)

<!--
You can use the local development environment to create and test Adaptive Forms without connecting to the Cloud Service. [!DNL AEM Forms] provides an SDK to help test all the cloud-ready functionalities on the local development environment. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can also develop and test custom code like custom components and prefill service on the local development environment. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code. 

>[!NOTE]
>
> Pre-pilot release does not support using an [!DNL AEM Forms] as a Cloud Service development instance to create forms. You can create forms, related assets, and custom code only on a local development environment.-->

<!--
You configure two types of development environments:

* **[!DNL AEM Forms] as a Cloud Service development environment:** Use the [[!DNL AEM Forms] as a Cloud Service](setup-forms-cloud-service.md) environment to store, manage, and publish Adaptive Forms and related assets. Do not use an [!DNL AEM Forms] as a Cloud Service environment to create Adaptive Forms and related assets <!--, form-centric workflows, a form data model, or to generate a Document of Record. -->

<!--
* **Local development environment:** You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. 
Use a local development environment:
    
    * To create forms and related assets (themes, templates, custom Submit Actions, and more) and convert PDF forms to Adaptive Forms. After an Adaptive Form or related assets are ready on the local development instance, you can export the Adaptive Form and related assets from the local development environment to an [!DNL AEM Forms] as a Cloud Service development environment for publishing.  
    
    * To update configuration settings and develop and test custom code like custom components and prefill service. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code.  

You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can use the [development tools](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/dev-tools.html) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## Förutsättningar

Du behöver följande program för att konfigurera en lokal utvecklingsmiljö. Ladda ned dessa innan du börjar konfigurera den lokala utvecklingsmiljön:

| Programvara | Beskrivning | Hämta länkar |
|---|---|---|
| Adobe Experience Manager as a Cloud Service SDK | SDK innehåller verktygen [!DNL Adobe Experience Manager] QuickStart och Dispatcher | Hämta den senaste SDK-versionen från [Programvarudistribution](#software-distribution) |  |
| Adobe Experience Manager Forms feature archive (AEM Forms add-on) | Verktyg för att skapa, formatera och optimera adaptiva Forms och andra Adobe Experience Manager Forms-funktioner | Hämta från [Programvarudistribution](#software-distribution) |
| (Valfritt) Adobe Experience Manager Forms referensinnehåll | Verktyg för att skapa, formatera och optimera adaptiva Forms och andra Adobe Experience Manager Forms-funktioner | Hämta från [Programvarudistribution](#software-distribution) |
| (Valfritt) Adobe Experience Manager Forms Designer | Verktyg för att skapa, formatera och optimera adaptiva Forms och andra Adobe Experience Manager Forms-funktioner | Hämta från [Programvarudistribution](#software-distribution) |

### Ladda ned den senaste versionen av programvara från Software Distribution {#software-distribution}

Om du vill hämta den senaste versionen av Adobe Experience Manager as a Cloud Service SDK, Experience Manager Forms feature archive (AEM Forms-tillägg), formulärreferensresurser eller Forms Designer från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html):

1. Logga in på <https://experience.adobe.com/#/downloads> med din Adobe ID

   >[!NOTE]
   >
   > Din Adobe-organisation måste vara etablerad för att AEM as a Cloud Service ska kunna hämta AEM as a Cloud Service SDK.

1. Navigera till fliken **[!UICONTROL AEM as a Cloud Service]**.
1. Sortera efter publicerat datum i fallande ordning.
1. Klicka på den senaste versionen av Adobe Experience Manager as a Cloud Service SDK, Experience Manager Forms feature archive (AEM Forms-tillägg), formulärreferensmaterial eller Forms Designer.

   >[!NOTE]
   >
   > Vi rekommenderar att du hämtar den senaste versionen av Experience Manager Forms-funktionsarkiv (AEM Forms-tillägg), formulärreferensmaterial eller Forms Designer för smidig kompatibilitet med Adobe Experience Manager as a Cloud Service SDK.

1. Granska och godkänn slutanvändaravtalet. Välj knappen **[!UICONTROL Download]**.

## Konfigurera utvecklingsverktyg för AEM-projekt {#setup-development-tools-for-AEM-projects}

Adobe Experience Manager Forms-projektet är en anpassad kodbas. Den innehåller kod, konfigurationer och innehåll som distribueras via Cloud Manager till [!DNL Adobe Experience Manager] as a Cloud Service. [AEM Project Maven Archetype](https://github.com/adobe/aem-project-archetype) innehåller projektets baslinjestruktur.

Konfigurera följande utvecklingsverktyg som ska användas för ditt [!DNL Adobe Experience Manager]-projekt för utveckling:

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

Detaljerade instruktioner om hur du ställer in tidigare nämnda utvecklingsverktyg finns i [Konfigurera utvecklingsverktyg](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## Konfigurera lokal Experience Manager-miljö för utveckling

I Cloud Service SDK finns en QuickStart-fil. Den kör en lokal version av Experience Manager. Du kan köra antingen författaren eller publiceringsinstanserna lokalt.

QuickStart har en lokal utvecklingsupplevelse, men inte alla funktioner i [!DNL Adobe Experience Manager] as a Cloud Service. Testa dina funktioner och din kod med [!DNL Adobe Experience Manager] as a Cloud Service-utvecklingsmiljö innan du flyttar funktionerna till scenen eller produktionen.

Så här installerar och konfigurerar du en lokal Experience Manager-miljö:

* [Hämta och extrahera](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) [!DNL Adobe Experience Manager] as a Cloud Service SDK
* [Konfigurera en författarinstans](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [Konfigurera en publiceringsinstans](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## Lägg till Forms-arkiv i lokala Author- och Publish-instanser och konfigurera Forms-specifika användare {#add-forms-archive-configure-users}

Utför följande steg i den angivna ordningen för att lägga till Forms-arkiv i Experience Manager-instanser och konfigurera formulärspecifika användare:

### Installera det senaste funktionsarkivet för Forms-tillägg {#add-forms-archive}

Adobe Experience Manager Forms as a Cloud Service funktionsarkiv innehåller verktyg för att skapa, formatera och optimera adaptiva Forms i den lokala utvecklingsmiljön. Installera paketet för att skapa ett adaptivt formulär och använd olika andra funktioner i [!DNL AEM Forms]. Så här installerar du paketet:

1. Hämta och extrahera det senaste [!DNL AEM Forms]-arkivet för ditt operativsystem från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

1. Navigera till katalogen crx-quickstart/install. Om mappen inte finns skapar du den.

1. Stoppa din AEM-instans och placera arkivet för tilläggsfunktionen [!DNL AEM Forms], `aem-forms-addon-<version>.far`, i installationsmappen.
1. Gå till det aktiva kommandofönstret och tryck på `Ctrl + C` för att starta om SDK.

   >[!NOTE]
   >
   > Du bör använda kommandot Ctrl + C för att starta om SDK. Om du startar om AEM SDK med alternativa metoder, till exempel att stoppa Java-processer, kan det leda till inkonsekvenser i AEM utvecklingsmiljö.

<!--**Q**: I've set up a Aem as a Cloud Service environment and added the Forms Add-On for a project. After the .far file addition, the bundles are not in the active state and are in installed state only due to the missing dependencies. How to make the bundles in the active state?
**A**: To resolve the issue:
1. Start the AEM and wait for it to start completely (all bundles up)
1. Stop aem (ctrl + c). Place the forms far in the install folder.
1. Restart AEM.-->


### Konfigurera användare och behörigheter {#configure-users-and-permissions}

Skapa användare som formulärutvecklare och formulärdeltagare och [lägg till dessa användare i fördefinierade formulärgrupper](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) för att ge dem de behörigheter som krävs. Tabellen nedan visar alla typer av användare och fördefinierade grupper för varje typ av formuläranvändare:

| Användartyp | AEM Group |
|---|---|
| Formuläradministratör / | [!DNL forms-users] (AEM Forms-användare), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors] och [!DNL fdm-authors] |
| Formulärutvecklare | [!DNL forms-users] (AEM Forms-användare), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors] och [!DNL fdm-authors] |
| Customer Experience Lead eller UX Designer | [!DNL forms-users], [!DNL template-authors] |
| AEM-administratör | [!DNL aem-administrators], [!DNL fd-administrators] |
| Slutanvändare | När en användare måste logga in för att visa och skicka ett adaptivt formulär lägger du till sådana användare i gruppen [!DNL forms-users]. </br> Om ingen användarautentisering krävs för att få åtkomst till Adaptiv Forms ska du inte tilldela någon grupp till sådana användare. |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html).  

1. **Install the latest [!DNL AEM Forms] add-on feature archive:** [!DNL AEM Forms] add-on feature archive provides tools to create, style, and optimize Adaptive Forms on the local development environment. Install the package to create an Adaptive Form and use various other features of [!DNL AEM Forms]. To install the package:

    1. Download and extract the latest [!DNL AEM Forms] archive for your operating system from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

    1. Navigate to the crx-quickstart/install directory. If the folder does not exist, create it.

    1. Stop your Cloud ready AEM instance, place the [!DNL AEM Forms] add-on feature archive, `aem-forms-addon-<version>.far`,  in the install folder, and restart the instance.

1. **Configure users and permissions:** Create users like Form Developer and Form Practitioner a nd add these users to pre-defined forms group to provide them required permissions. The table below lists all types of users and pre-defined groups for each type of forms users:
  
    | User Type | AEM Group |
    |---|---|
    | Form Practitioner  | forms-users (AEM Forms Users), template-authors  |
    | Form Developer | forms-users (AEM Forms Users), template-authors |
    | End-User| everyone* |

    `*` When a user should log in to access or submit Adaptive Forms, add such users to the everyone group.  -->

<!--    
### Set up an AEM project for the development tasks related to local AEM 6.5.5 Forms instance

Use this project to update configurations, create overlays, develop custom Adaptive Form components, and custom code using the local development environment. To set up the project:

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/ht-projects-maven.html).

1. Configure the project to use [uber-jar](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=en#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## Ställ in lokal utvecklingsmiljö för DoR (Document of Record){#docker-microservices}

AEM Forms som molntjänster erbjuder en dockningsbaserad SDK-miljö för enklare utveckling av Document of Record och för användning av andra mikrotjänster. Du slipper konfigurera plattformsspecifika binärfiler och anpassningar manuellt. Så här konfigurerar du miljön:

1. Installera och konfigurera Docker:

   * (För Microsoft® Windows) Installera [Docker Desktop](https://www.docker.com/products/docker-desktop). `Docker Engine` och `docker-compose` konfigureras på datorn.

   * (Apple macOS) Installera [Docker Desktop för Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). Det innehåller Docker Engine, Docker CLI-klient, Docker Compose, Docker Content Trust, Kubernetes och Credential Helper.

   * (För Linux®) Installera [Docker Engine](https://docs.docker.com/engine/install/#server) och [Docker Compose](https://docs.docker.com/compose/install/) på datorn.

   >[!NOTE]
   >
   > * För Apple macOS tillåtslista du mappar som innehåller lokala AEM Author-instanser.
   >
   > * Docker Desktop för Windows har stöd för två backends, Hyper-V
   > (äldre) och WSL2 (modern). Fildelning sker automatiskt
   > hanteras av Docker när WSL2 används (modern). Du måste
   > konfigurera fildelning explicit när Hyper-V används (äldre).

1. Skapa en mapp, till exempel aem-sdk, parallellt med författaren och publiceringsinstanser. Exempel: C:\aem-sdk.

1. Extrahera filen `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip`.

   ![extraherade aem-formulär har lagts till i ursprungliga ](assets/microservice-docker.png)

1. Skapa en miljövariabel AEM_HOME och peka på en lokal installation av AEM Author. Exempel: C:\aem\author\.

1. Öppna sdk.bat eller sdk.sh för redigering. Ställ in AEM_HOME så att det pekar på en lokal installation av AEM Author. Exempel: C:\aem\author\.

1. Öppna kommandotolken och navigera till mappen `aem-forms-addon-native-<version>`.

1. Kontrollera att den lokala AEM Author-instansen är igång och körs. Kör följande kommandon för att starta SDK:

   * På Microsoft® Windows

     ```shell
     sdk.bat start
     ```


   * Linux® eller Apple macOS

     ```Shell
     % export AEM_HOME=[local AEM Author installation]
     % ./sdk.sh start
     ```


   >[!NOTE]
   >
   > Om du har definierat miljövariabeln i sdk.sh-filen är det valfritt att ange den på kommandoraden. Alternativet att definiera systemvariabeln på kommandoraden ges för att köra kommandot utan att uppdatera gränssnittsskriptet.

   ![start-sdk-command](assets/start-sdk.png)

Du kan nu använda den lokala utvecklingsmiljön för att återge arkivhandlingar. Testa genom att överföra en XDP-fil till miljön och återge den. <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> konverterar till exempel XDP-filen till PDF-dokumentet.

## Konfigurera ett utvecklingsprojekt för Forms baserat på Experience Manager arkityp {#forms-cloud-service-local-development-environment}

Använd det här projektet för att skapa Adaptiv Forms, distribuera konfigurationsuppdateringar, övertäckningar, skapa anpassade adaptiva formulärkomponenter, testa och anpassad kod på den lokala [!DNL Experience Manager Forms] SDK. När du har testat lokalt kan du distribuera projektet till [!DNL Experience Manager Forms] as a Cloud Service produktions- och icke-produktionsmiljöer. När du distribuerar projektet distribueras även följande AEM Forms-resurser:

| Teman | Mallar | FDM (Form Data Model) |
---------|----------|---------
| Arbetsyta 3.0 | Grundläggande | Microsoft® Dynamics 365 |
| Tranquil | Tom | Salesforce |
| Urbane |   |  |
| Ultramarin |  |  |
| Beryl |  |  |

>[!NOTE]
>
> Konfigurera AEM Archetype version 30 eller senare-baserade projekt för att hämta och använda Microsoft® Dynamics 365 och Salesforce Form Data Model (FDM) med AEM Forms as a Cloud Service.
> &#x200B;> Konfigurera AEM Archetype version 32 eller senare-baserade projekt för att hämta och använda temana Tranquil, Urbane och Ultramarine med AEM Forms as a Cloud Service.

Så här ställer du in projektet:

1. **Klona Cloud Manager Git-databasen på din lokala utvecklingsinstans:** Din Cloud Manager Git-databas innehåller ett AEM-standardprojekt. Den baseras på [AEM-arkitekturen](https://github.com/adobe/aem-project-archetype/). Klona din Cloud Manager Git-databas med Git-kontohantering för självbetjäning från Cloud Manager användargränssnitt och lägg projektet i din lokala utvecklingsmiljö. Mer information om hur du får åtkomst till databasen finns i [Åtkomst till databaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **Skapa ett [!DNL Experience Manager Forms] som ett [Cloud Service]-projekt:** Skapa ett [!DNL Experience Manager Forms] som ett [Cloud Service]-projekt baserat på den senaste [AEM-arkitekturen](https://github.com/adobe/aem-project-archetype) eller senare. Med hjälp av arkitypen kan utvecklare enkelt börja utveckla för [!DNL AEM Forms] as a Cloud Service. Den innehåller även några exempelteman och mallar som hjälper dig att snabbt komma igång.

   Öppna kommandotolken och kör nedanstående kommando för att skapa ett [!DNL Experience Manager Forms] as a Cloud Service-projekt.

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="41" -D appTitle=mysite -D appId=mysite -D groupId=com.mysite -D includeFormsenrollment="y" -D aemVersion="cloud"
   ```

   Ändra `appTitle`, `appId` och `groupId` i ovanstående kommando så att den återspeglar din miljö. Ange också ett värde för includeFormsenrollment, includeFormsCommunications och includeFormsheadless till `y` eller `n` beroende på din licens och dina krav. IncludeFormsheadless är obligatoriskt för att skapa Adaptiv Forms baserat på kärnkomponenter.

   * Använd alternativet `includeFormsenrollment=y` om du vill inkludera Forms-specifika konfigurationer, teman, mallar, kärnkomponenter och beroenden som krävs för att skapa Adaptiv Forms. Om du använder Forms Portal anger du alternativet `includeExamples=y`. Dessutom läggs kärnkomponenterna i Forms Portal till i projektet.

   * Använd alternativet `includeFormscommunications=y` för att inkludera Forms Core-komponenter och beroenden som krävs för att inkludera funktionen för kundkommunikation.

     >[!WARNING]
     >
     >* När du skapar ett Arketype-projekt med version 45 anger [AEM Archetype Project Folder]/pom.xml till att börja med 2.0.64 som formulärkärnkomponent. Innan du bygger eller driftsätter Archetype-projektet ska du uppdatera formulärkärnkomponentens version till 2.0.62.

1. Distribuera projektet till din lokala utvecklingsmiljö. Du kan använda följande kommando för att distribuera till den lokala utvecklingsmiljön

   `mvn -PautoInstallPackage clean install`

   En fullständig lista med kommandon finns i [Bygga och installera](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Distribuera koden till din [!DNL AEM Forms] as a Cloud Service-miljö](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Konfigurera lokala Dispatcher-verktyg {#setup-local-dispatcher-tools}

Dispatcher är en Apache HTTP Web Server-modul som tillhandahåller ett säkerhets- och prestandalager mellan CDN- och AEM-publiceringsskiktet. Dispatcher är en integrerad del av Experience Manager övergripande arkitektur och bör ingå i den lokala utvecklingsmiljön.

Utför följande steg för att konfigurera lokala Dispatcher och lägg sedan till Forms-specifika regler:

### Konfigurera lokal Dispatcher {#setup-local-dispatcher}

[!DNL Experience Manager] as a Cloud Service SDK innehåller den rekommenderade Dispatcher-versionen som gör det lättare att konfigurera, validera och simulera Dispatcher lokalt. Dispatcher Tools är Docker-baserade och har kommandoradsverktyg för att överföra konfigurationsfilerna för Apache HTTP Web Server och Dispatcher till ett kompatibelt format och driftsätta dem i Dispatcher som körs i Docker-behållaren.

Cachelagring på Dispatcher gör att [!DNL AEM Forms] kan förifylla Adaptiv Forms på en klient. Det förbättrar återgivningshastigheten för förfyllda formulär.

Detaljerade anvisningar om hur du konfigurerar Dispatcher finns i [Konfigurera lokala Dispatcher-verktyg](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### Lägg till Forms-specifika regler i Dispatcher {#forms-specific-rules-to-dispatcher}

Så här konfigurerar du Dispatcher-cachen för Experience Manager Forms as a Cloud Service:

1. Öppna ditt AEM-projekt och gå till `\src\conf.dispatcher.d\available_farms`
1. Skapa en kopia av filen `default.farm`. Exempel: `forms.farm`.
1. Öppna den skapade `forms.farm`-filen för redigering och ersätt följande kod:

   ```json
   #/ignoreUrlParams {
   #/0001 { /glob "*" /type "deny" }
   #/0002 { /glob "q" /type "allow" }
   #}
   ```

   med

   ```json
   /ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   /0002 { /glob "dataRef" /type "allow" }
   }
   ```

1. Spara och stäng filen.
1. Gå till `conf.d/enabled_farms` och skapa en symbolisk länk till filen `forms.farm`.
1. Kompilera och distribuera projektet till din [!DNL AEM Forms] as a Cloud Service-miljö.

### Att tänka på vid cachelagring {#considerations-about-caching}

* Med Dispatcher-cachning kan [!DNL AEM Forms] förifylla Adaptiv Forms på en klient. Det förbättrar återgivningshastigheten för förfyllda formulär.
* Cachelagring av funktioner för skyddat innehåll är inaktiverat som standard. Om du vill aktivera funktionen kan du utföra instruktionerna i artikeln [Cachelagra skyddat innehåll](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en)
* Dispatcher kan inte ogiltigförklara vissa adaptiva Forms och relaterade adaptiva Forms. Information om hur du löser sådana problem finns i [[!DNL AEM Forms] Caching](troubleshooting-caching-performance.md) i felsökningsavsnittet.
* Cachelagrar lokaliserade adaptiva Forms:
   * Använd URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` för att begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Alternativet Webbläsarspråk är inaktiverat som standard. Om du vill ändra språkinställningen för webbläsaren
* När du använder URL-formatet `http://host:port/content/forms/af/<adaptivefName>.html` och Använd webbläsarspråk i konfigurationshanteraren är inaktiverat, visas den icke-lokaliserade versionen av det adaptiva formuläret. Det icke-lokaliserade språket är det språk som används vid utvecklingen av det adaptiva formuläret. Det språk som är konfigurerat för webbläsaren (webbläsarens språkområde) beaktas inte och en icke-lokaliserad version av det anpassade formuläret används.
* När du använder URL-formatet `http://host:port/content/forms/af/<adaptivefName>.html`, och Använd webbläsarspråk i konfigurationshanteraren är aktiverat, visas en lokaliserad version av det adaptiva formuläret, om en sådan finns. Språket i det lokaliserade adaptiva formuläret baseras på det språk som är konfigurerat för webbläsaren (webbläsarens språkområde). Det kan leda till [cachelagring av endast den första instansen av ett adaptivt formulär]. Om du vill förhindra att problemet inträffar på din instans läser du [endast den första instansen av ett adaptivt formulär cachas](troubleshooting-caching-performance.md) i felsökningsavsnittet.

Din lokala utvecklingsmiljö är klar.

## Aktivera adaptiva Forms Core-komponenter i AEM Forms as a Cloud Service och lokal utvecklingsmiljö

Genom att aktivera adaptiva Forms Core-komponenter i AEM Forms as a Cloud Service kan du börja skapa, publicera och leverera Core Components-baserade adaptiva Forms och Headless Forms med hjälp av AEM Forms Cloud Service-instanser i flera kanaler. Du behöver en adaptiv Forms Core Components-aktiverad miljö för att kunna använda Headless Adaptive Forms.

>[!NOTE]
>
> Installera den senaste versionen för att aktivera adaptiva Forms Core-komponenter för din AEM Cloud-tjänstmiljö.

## Uppgradera din lokala utvecklingsmiljö {#upgrade-your-local-development-environment}

Om du uppgraderar SDK till en ny version måste du ersätta hela den lokala utvecklingsmiljön, vilket resulterar i att all kod, konfiguration och innehåll i de lokala databaserna går förlorad. Kontrollera att kod, konfiguration eller innehåll som inte ska tas bort är säkert implementerat i Git eller exporteras från de lokala Experience Manager-instanserna som CRX-Packages.

### Så undviker du innehållsförluster när du uppgraderar SDK {#avoid-content-loss-when-upgrading--SDK}

Genom att uppgradera SDK skapas en helt ny instans av typen Författare och Publicera, inklusive en ny databas ([Konfigurera AEM-projekt](#forms-cloud-service-local-development-environment)), vilket innebär att ändringar som gjorts i en tidigare SDK-databas går förlorade. Viktiga strategier för hur du kan hjälpa till med beständigt innehåll mellan SDK-uppgraderingar finns i [Så här undviker du innehållsförluster när du uppgraderar AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

<!--When you update any  Forms-specifc configuration, create overlays, develop custom Adaptive Form components, or develop and test any custom code in AEM project for the development tasks related to local development instance, use the AEM project cloned from the Cloud Manager Git repository to [deploy the custom code and other changes to your [!DNL AEM Forms] as a Cloud Service's production or non-production environment](https://video.tv.adobe.com/v/30191?quality=9).

## Upgrade your local development environment {#update-local-setup}

Update the local AEM setup (AEM SDK) to latest version at least monthly on, or shortly after, the last Thursday of each month, which is the release cadence for AEM as a Cloud Service "feature releases". You can download local AEM SDK from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

Updating the AEM SDK to a new version requires replacing the entire local development environment, resulting in a loss of all code, configuration and content in the local AEM repositories. Ensure that any code, config or content that should not be destroyed is safely committed to Git, or exported from the local AEM instance as AEM Packages.

### How to avoid content loss when upgrading the AEM SDK {#avoid-content-loss-when-upgrading--AEM-SDK}

Upgrading the AEM SDK is effectively creating a brand new AEM runtime ([Set up a local AEM instance](setup-forms-cloud-service.md)), including a new repository ([Set up AEM project](#forms-cloud-service-local-development-environment)), meaning any changes made to a prior AEM SDK's repository are lost. The following are viable strategies for aiding in persisting content between AEM SDK upgrades, and can be used discretely or in concert:

1. Create a content package dedicated to containing the sample content to aid in development and maintain it in Git. Any content that should be persisted through AEM SDK upgrades would be persisted into this package and re-deployed after upgrading the AEM SDK.
1. Use [oak-upgrade](https://jackrabbit.apache.org/oak/docs/migration.html) with the `includepaths` directive, to copy content from the prior AEM SDK repository to the new AEM SDK repository.
1. Back up any content using AEM Package Manager and content packages on the prior AEM SDK and re-install them on the new AEM SDK.

Remember, using the above approaches to maintain code between AEM SDK upgrades, indicates a development anti-pattern. Non-disposable code should originate in your Development IDE and flow into AEM SDK via deployments.

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#local-development-environment-set-up).-->

### Säkerhetskopiera och importera Forms-specifikt material till en ny SDK-miljö {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

Så här säkerhetskopierar och flyttar du resurser från SDK till en ny SDK-miljö:

* Skapa en säkerhetskopia av befintligt innehåll.

* Konfigurera en ny SDK-miljö.

* Importera säkerhetskopian till din nya SDK-miljö.

### Skapa en säkerhetskopia av befintligt innehåll {#create-backup-of-your-existing-content}

Säkerhetskopiera adaptiva Forms, mallar, formulärdatamodell (FDM), tema, konfigurationer och anpassad kod. Du kan utföra följande åtgärd för att skapa en säkerhetskopia:

1. [Hämta](import-export-forms-templates.md#manage-forms-and-related-assets) anpassningsbara Forms, teman och PDF forms.
1. Exportera adaptiva formulärmallar.

1. Hämta formulärdatamodeller

1. Exportera redigerbara mallar, molnkonfigurationer och arbetsflödesmodell. Om du vill exportera alla tidigare nämnda objekt från din befintliga SDK skapar du ett [CRX-paket](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html) med följande filter:

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. Exportera e-postkonfigurationer, skicka och förifyll åtgärdskod från den lokala utvecklingsmiljön. Om du vill exportera dessa inställningar och konfigurationer skapar du en kopia av följande mappar och filer i den lokala utvecklingsmiljön:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### Importera säkerhetskopian till din nya SDK-miljö {#import-the-backup-to-your-new-SDK-environment}

Importera adaptiva Forms, mallar, formulärdatamodell, tema, konfigurationer och anpassad kod till din nya miljö. Du kan utföra följande åtgärd för att importera säkerhetskopior:

1. [Importera](import-export-forms-templates.md#manage-forms-and-related-assets) anpassningsbara Forms, teman och PDF forms till nya SDK-miljöer.
1. Importera adaptiva blankettmallar i en ny SDK-miljö.

1. Överför formulärdatamodeller till en ny SDK-miljö.

1. Importera redigerbara mallar, molnkonfigurationer och arbetsflödesmodell. Om du vill importera alla tidigare nämnda objekt i din nya SDK-miljö importerar du det CRX-paket som innehåller dessa objekt till din nya SDK-miljö.

1. Importera e-postkonfigurationer, skicka och förifyll åtgärdskod från den lokala utvecklingsmiljön. Om du vill importera dessa inställningar och konfigurationer placerar du följande filer från ditt gamla Arketype-projekt i ditt nya Arketype-projekt:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

Din nya miljö innehåller nu formulär och relaterade resurser från den gamla miljön.
