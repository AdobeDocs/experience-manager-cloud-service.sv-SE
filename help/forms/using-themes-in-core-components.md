---
title: Hur skapar och använder man teman i Adaptive Forms?
description: Du kan använda teman för att utforma och ge en visuell identitet till ett adaptivt formulär med hjälp av kärnkomponenter. Du kan dela ett tema med ett valfritt antal adaptiva Forms.
keywords: teman för formulärbyggare, adaptiva formulärformatmallar, verktyg för att skapa formulärteman, formatera anpassningsbara formulär, anpassa teman, skapa formulärteman
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: c5bea0d9386617b8ff51309f5cba45e7068f71e8
workflow-type: tm+mt
source-wordcount: '2843'
ht-degree: 0%

---

# Använd teman för att utforma Core Components-baserade Adaptive Forms{#themes-for-af-using-core-components}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | Den här artikeln |

Du kan skapa och använda teman för att utforma ett anpassat formulär. Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter. Ett tema hanteras separat utan referens till ett adaptivt formulär och kan återanvändas i flera adaptiva Forms.

I den här artikeln får du veta hur du utformar anpassade looks för Core Component-baserade Adaptive Forms med hjälp av teman.

## Tillgängliga teman för att formatera kärnkomponenter

Forms som Cloud Service tillhandahåller listas nedan teman för Core Components based Adaptive Forms:

* [Arbetsytans tema](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND-tema](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL-tema](https://github.com/adobe/aem-forms-theme-easel)

## Förstå temastrukturen

Ett tema är ett paket som innehåller formatkomponenter som CSS-filer, JavaScript-filer och resurser (som ikoner) som definierar formatet för din adaptiva Forms. Temat Adaptiv form följer en särskild organisation som består av följande komponenter:

* `src/theme.scss`: Den här mappen innehåller CSS-filen som har stor effekt på hela temat. Det fungerar som en central plats för att definiera och hantera temats format och beteende. Genom att redigera den här filen kan du göra ändringar som tillämpas överallt i temat, vilket påverkar både utseendet och funktionaliteten på dina adaptiva Forms- och AEM Sites-sidor.

* `src/site`: Den här mappen innehåller CSS-filer som används på en hel AEM-webbplats. De här filerna består av kod och format som påverkar den övergripande funktionaliteten och layouten på din AEM-webbplats. Alla ändringar som görs här återspeglas på alla sidor på webbplatsen. [När ska den användas?]

* `src/components`: CSS-filerna i den här mappen är utformade för enskilda AEM kärnkomponenter. Varje dedikerad mapp för en komponent innehåller en `.scss`-fil som formaterar den specifika komponenten i ett adaptivt formulär. Filen /src/components/accordion/_accordion.scss innehåller till exempel formatinformation för den adaptiva Forms-dragspelskomponenten.

  ![adaptiv formulärbaserad temastruktur](/help/forms/assets/theme_structure.png)

* `src/resources`: Den här mappen innehåller statiska filer som ikoner, logotyper och teckensnitt. Resurserna används för att förbättra temats visuella element och övergripande design.

## Skapa ett tema

Forms, som Cloud Service tillhandahåller, listas nedan med adaptiva formulärstilteman för Core Components-baserade Adaptive Forms.

* [Arbetsytans tema](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND-tema](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL-tema](https://github.com/adobe/aem-forms-theme-easel)

Du kan [anpassa något av dessa teman och skapa ett nytt tema](#customize-a-theme-core-components).

![Arbetsflöde för temaanpassning](/help/forms/assets/workflow-of-customization-of-theme.png)

## Anpassa ett tema {#customize-a-theme-core-components}

Att anpassa ett tema avser processen att ändra, formatera och anpassa ett temas utseende. När du anpassar ett tema ändrar du dess designelement, layout, färger, typografi och ibland den underliggande koden. Du kan skapa ett unikt och skräddarsytt utseende för webbplatsen eller tillämpningen, samtidigt som du bibehåller den grundläggande strukturen och funktionaliteten som temat ger.

### Förutsättningar {#prerequisites-to-customize}

* Bekanta dig med att [konfigurera en pipeline i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline) och att ha grundläggande kunskaper om hur du konfigurerar en pipeline hjälper dig att hantera och distribuera dina temaanpassningar på ett effektivt sätt.
* Lär dig hur du [konfigurerar en användare med rollen som medarbetare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html). Genom att förstå hur du konfigurerar en användare med rollen Medarbetare kan du ge de behörigheter som krävs för att anpassa temat.
* Installera den senaste versionen av [Apache Maven](https://maven.apache.org/download.cgi). Apache Maven är ett automatiserat byggverktyg som ofta används för Java™-projekt. Genom att installera den senaste versionen får du de beroenden du behöver för att anpassa temat.
* Installera en vanlig textredigerare. Exempel: Microsoft® Visual Studio Code. Med en vanlig textredigerare som Microsoft® Visual Studio Code får du en användarvänlig miljö där du kan redigera och ändra temafiler.

### Konfigurera din miljö

* Konfigurera en [frontenddistributionspipeline](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html) för din Cloud Service-miljö. Du kan också konfigurera pipeline senare, så att du kan prioritera testning och finjustering av temat innan du ställer in distributionsflödet.

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

När du har lärt dig förinställningarna och konfigurerat utvecklingsmiljön är du väl beredd att börja anpassa eller formatera temat efter dina specifika behov.

### Anpassa ett tema {#steps-to-customize-a-theme-core-components}

Att anpassa ett tema är en process i flera steg. Om du vill anpassa temat utför du stegen i listordning:

1. [Klona ett tema](#download-a-theme-core-components)
1. [Ange namn på ett tema](#set-name-of-theme)
1. [Anpassa ett tema](#customize-the-theme)
1. [Testa ett tema](#test-the-theme)
1. [Distribuera ett tema](#deploy-the-theme)

Exemplen i dokumentet är baserade på temat **Canvas**, men det är viktigt att notera att du kan klona ett tema och anpassa det med samma instruktioner. Dessa instruktioner kan användas för alla teman och du kan ändra teman efter dina specifika behov.

Låt oss börja med en process för att skapa en varumärkesanpassad upplevelse för dina Core Component-baserade Adaptive Forms med teman?

#### &#x200B;1. Klona ett tema {#download-a-theme-core-components}

Om du vill klona ett tema för Core Components based Adaptive Forms väljer du ett av följande teman:

* [Arbetsytans tema](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND-tema](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL-tema](https://github.com/adobe/aem-forms-theme-easel)

Så här klonar du ett tema:

1. Öppna kommandotolken eller terminalfönstret i den lokala utvecklingsmiljön.

1. Kör kommandot `git clone` om du vill klona ett tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Ersätt [Sökvägen till Git-databasen för temat] med den faktiska URL:en för motsvarande Git-databas för temat

   Om du till exempel vill klona arbetsytans tema kör du följande kommando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   När kommandot har körts har du en lokal kopia av temat på datorn i mappen `aem-forms-theme-canvas`.


#### &#x200B;2. Ange ett temats namn {#set-name-of-theme}

1. Öppna temamappen i din utvecklingsmiljö. Om du till exempel vill öppna mappen `aem-forms-theme-canvas` i Visual Studio Code editor.

1. Navigera till mappen `aem-forms-theme-canvas`.

1. Kör följande kommando:

   ```
      code .
   ```

   ![Öppna temamappen i en vanlig textredigerare](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   Mappen öppnas i Visual Studio-koden.

1. Öppna filen `package.json` för redigering.

1. Ange värden för attributen `name` och `version`.

   ![Byt bild på temanamnet på arbetsytan](/help/forms/assets/changename_canvastheme.png)

   >[!NOTE]
   >
   > * Namnattributet används för att unikt identifiera temat och det angivna namnet visas på fliken **Format** i **guiden Skapa formulär**.
   > * Du kan välja att välja ett namn för temat enligt ditt val, till exempel `mytheme` eller `customtheme`. I det här fallet har vi angett namnet som `aem-forms-wknd-theme`.

1. Öppna filen `package-lock.json` för redigering.
1. Ange värden för attributen `name` och `version`. Kontrollera att värdena för attributen `name` och `version` i filen `Package-lock`.json matchar värdena i filen `Package.json`.

   ![Byt bild på temanamnet på arbetsytan](/help/forms/assets/changename_canvastheme-package-lock.png)

1. (Valfritt) Öppna filen `ReadMe` för att redigera och uppdatera namnet på temat.

   ![Byt bild på temanamnet på arbetsytan](/help/forms/assets/changename_canvastheme-readme-file.png)

1. Spara och stäng filerna.

**Att tänka på när namnet på temat anges**

* Det är obligatoriskt att ta bort `@aemforms` från temanamnet i filen `Package.json` och filen `Package-lock.json`. Om du inte kan ta bort `@aemforms` från ditt anpassade temanamn resulterar det i att frontend-pipeline inte kan tas bort under temats distribution.
* Vi rekommenderar att du uppdaterar temat `version` i filen `Package.json` och filen `Package-lock.json` så att ändringar och förbättringar av temat återspeglas korrekt över tid.
* Om du vill ha viktig information om användning, installationsinstruktioner och annan relevant information bör du uppdatera namnet på temat i filen `ReadMe`.

#### &#x200B;3. Anpassa ett tema {#customize-the-theme}

Du kan anpassa enskilda komponenter eller göra ändringar på temanivå med hjälp av globala variabler i ett tema. Ändringar som görs i globala variabler påverkar alla enskilda komponenter. Du kan till exempel använda globala variabler för att ändra kantfärgen för alla komponenter i ett adaptivt formulär och en ljus fyllningsfärg för att ställa in CTA (Call to action) med hjälp av knappkomponenten:

* [Ange format för temanivåer](#theme-customization-global-level)

* [Ange format för komponentnivå](#component-based-customization)

##### Ange format för temanivåer{#theme-customization-global-level}

Filen `variable.scss` innehåller temats globala variabler. Genom att uppdatera dessa variabler kan du göra formatrelaterade ändringar på temanivå. Så här använder du format på temanivå:

1. Öppna filen `<your-theme-sources>/src/site/_variables.scss` för redigering.
1. Ändra värdet för alla egenskaper. Standardfelfärgen är till exempel `red`. Om du vill ändra felfärgen från `red` till `blue` ändrar du färghexkoden för `$errorvariable`. Exempel: `$error: #196ee5`.
1. Spara och stäng filen.

   ![Redigera tema](/help/forms/assets/edit_theme.png)

På samma sätt kan du använda filen `variable.scss` för att ange teckensnittsfamilj och -typ, tema- och teckensnittsfärger, teckensnittsstorlek, temaavstånd, felikon, temagränsformat och mer variabel som påverkar flera adaptiva formulärkomponenter.

##### Ange format för komponentnivå {#component-based-customization}

Du kan också ändra teckensnitt, färg, storlek och andra CSS-egenskaper för en viss kärnkomponent i Adaptiv form. Till exempel knapp, kryssruta, behållare, sidfot med mera. Du kan formatera en knapp eller kryssruta genom att redigera CSS-filen för den specifika komponenten så att den anpassas till din organisations stil. Så här anpassar du en stil för en komponent:

1. Öppna filen `<your-theme-sources>/src/components/<component>/<component.scss>` för redigering. Om du till exempel vill ändra teckenfärgen för knappkomponenten öppnar du filen `<your-theme-sources>/src/components/button/button.scss`.
1. Ändra värdet enligt dina önskemål. Om du till exempel vill ändra färgen på knappkomponenten vid mushovring till `green` ändrar du värdet på egenskapen `color: $white` i klassen `cmp-adaptiveform-button__widget:hover` till hexadecimal kod `#12B453` eller någon annan nyans av `green`. Den färdiga koden ser ut så här:

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. Spara och stäng filen.

   ![Redigera CSS för textruta](/help/forms/assets/edit_color_textbox.png)

   >[!NOTE]
   >
   > När ett format definieras både på tema- och komponentnivå prioriteras det format som definieras på komponentnivå.

#### &#x200B;4. Testa ett anpassat tema {#test-the-theme}

Så här förhandsgranskar och testar du ändringarna i den lokala miljön och anpassar temat enligt kraven för olika AEM-komponenter:

* 4.1 [Konfigurera en lokal miljö för testning](#rename-env-file-theme-folder)
* 4.2 [Testa temat i den lokala miljön](#start-a-local-proxy-server)

##### 4.1. Konfigurera en lokal miljö för testning {#rename-env-file-theme-folder}

1. Öppna temamappen i din utvecklingsmiljö. Öppna till exempel mappen `aem-forms-theme-canvas` i Visual Studio Code editor.
1. Byt namn på filen `env_template` till filen `.env` i temamappen och lägg till följande parametrar:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Formulärets URL är till exempel `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. Värdena för:

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. Spara filen.

   ![Arbetsytans temastruktur](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 Testa temat i en lokal miljö {#start-a-local-proxy-server}

1. Navigera till temamappens rot. I det här fallet är temamappens namn `aem-forms-theme-canvas`.
1. Öppna kommandotolken eller terminalen.
1. Kör `npm install` för att installera beroendena.
1. Kör `npm run live` om du vill förhandsgranska formuläret med det uppdaterade temat i den lokala webbläsaren.

   >[!NOTE]
   >
   > Om ett fel inträffar när kommandot `npm run live` körs kör du följande kommandon före kommandot `npm run live`:
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

Det här är en het driftsättning. Så när du gör några ändringar och sparar filerna `_variables.scss` och `button.scss` väljs ändringarna automatiskt och de senaste utdata förhandsgranskas. Raden `[Browsersync] File event [change]` anger att servern har identifierat de senaste ändringarna och distribuerar ändringarna i den lokala miljön.

![Webbläsarsynkronisering för proxy](/help/forms/assets/browser_sync.png)

Efter att ha följt exemplen för att formatera ett adaptivt formulär (kärnkomponenter) på både temanivå och komponentnivå för temaanpassningar, ändras felmeddelandena i ett adaptivt formulär till färgen `blue`, medan etikettfärgen för knappkomponenten ändras till `green` när den hovrar.

**Förhandsgranska stil på temanivå**

![Exempel: Felfärgen är blå](/help/forms/assets/theme-level-changes.png)

**Förhandsgranska komponentnivåstil**

![Exempel: Hovringsfärgen är grön](/help/forms/assets/button-customization.png)

Att anpassa ett tema hjälper till att utforma anpassade utseenden för Core Component-baserade Adaptive Forms enligt organisationens krav.

###### Testa temat för formulär som lagras i en Cloud Service-miljö

Du kan också testa temat för den adaptiva formen som finns på din AEM Forms as a Cloud Service-instans. Så här konfigurerar och anger du den lokala miljön för testning av teman med Adaptive Forms på molninstansen:

1. Öppna temamappen i din utvecklingsmiljö. Öppna till exempel mappen `aem-forms-theme-canvas` i Visual Studio Code editor.
1. Byt namn på filen `env_template` till filen `.env` och lägg till följande parametrar:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   URL:en för formuläret i molnmiljön är till exempel `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. Värdena för:

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. Spara filen.
1. Skapa en lokal användare.

   >[!NOTE]
   >
   > Så här skapar du en lokal användare:
   >
   > * Gå till **[!UICONTROL AEM Home]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]** .
   > * Kontrollera att användaren är medlem i gruppen `forms-users`.

1. Navigera till temamappens rot. I det här fallet är temamappens namn `aem-forms-theme-canvas`.
1. Kör `npm run live` och du omdirigeras till en lokal webbläsare.
1. Klicka på `SIGN IN LOCALLY (ADMIN TASKS ONLY)` och logga in med den lokala användarens autentiseringsuppgifter.

Du kan förhandsgranska det adaptiva formuläret med de senaste ändringarna. När du är nöjd med ändringarna som gjorts i en temamapp distribuerar du temat till din AEM Cloud-tjänstmiljö med hjälp av frontendriet.

#### &#x200B;5. Använd ett tema {#deploy-the-theme}

Så här distribuerar du temat till din Cloud Service-miljö med hjälp av pipeline i gränssnittet:

* 5.1 [Skapa en databas för temat](#create-a-new-theme-repo)
* 5.2 [Överför ändringarna till databasen](#committing-the-changes)
* 5.3 [Ställ in versionen Node.js till 20](#53-set-the-nodejs-version-to-20)
* 5.4 [Kör frontpipeline](#run-a-frontend-pipeline)

##### 5.1 Skapa en databas för temat{#create-a-new-theme-repo}

Du behöver en databas för att distribuera temat. Logga in på din [AEM Cloud Manager-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) och lägg till en ny databas för ditt tema.

1. Skapa en ny databas för ett tema genom att klicka på **[!UICONTROL Repositories]** > **[!UICONTROL Add Repository]**.

   ![skapa nytt tema &#x200B;](/help/forms/assets/createrepo_canvastheme.png)


1. Ange **databasnamnet** i dialogrutan **Lägg till databas**. Angivet namn är till exempel `custom-canvas-theme-repo`.
1. Klicka på **[!UICONTROL Save]**.

   ![Lägg till upprepning av arbetsytans tema](/help/forms/assets/addcanvasthemerepo.png)

1. Klicka på **[!UICONTROL Copy Repository URL]** för att kopiera databasens URL.

   ![URL för arbetsytans tema](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   >* Du kan använda en databas för flera teman.
   >* Om du vill distribuera olika teman måste du skapa separata rörledningar.
   >* Du kan till exempel använda samma databas, som `custom-canvas-theme-repo`, för Canvas-temat, WKND-temat och EASEL-temat. För att kunna använda teman måste du dock skapa separata frontledningar. Framtida anpassningar av ett specifikt tema distribueras med motsvarande frontendpipeline.

##### 5.2. Skicka ändringarna till databasen {#committing-the-changes}

Nu kan du föra över ändringarna till temadatabasen för din AEM Forms Cloud Service.

1. Navigera till temamappens rot.  I det här fallet är temamappens namn `aem-forms-theme-canvas`.
1. Öppna kommandotolken eller terminalen.
1. Kör följande kommando i den ordning som visas:

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   Till exempel:

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![Ändringar har implementerats](/help/forms/assets/cmd_git_push.png)

##### 5.3 Ange version 20 av Node.js

Så här anger du versionen Node.js till 20 med pipelinekonfigurationen:

1. Gå till avsnittet **Pipelines** och leta upp din frontendpipeline.
2. Klicka på trepunktsmenyn **⋯** till höger om pipelinen och välj **Visa/redigera variabler** i listrutan.
3. I dialogrutan **Variabelkonfiguration** fyller du i fälten enligt följande:
   * **NAME** - NODE_VERSION
   * **VÄRDE** - 20
   * **STEP APPLIED** - Bygge
   * **TYP** - Variabel
4. Klicka på **Spara** för att använda konfigurationen.

![pipeline-konfiguration](/help/forms/assets/pipeline-config.png)


##### 5.4 Köra frontlinjen {#run-a-frontend-pipeline}

Temat distribueras med [front-end-pipeline](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html). Så här distribuerar du temat:

1. Logga in på din AEM Cloud Manager-databas.
1. Klicka på knappen **[!UICONTROL Add]** i avsnittet **[!UICONTROL Pipelines]**.
1. Välj **[!UICONTROL Add Non-Production Pipeline]** eller **[!UICONTROL Add Production Pipeline]** baserat på Cloud Service-miljön. Här är till exempel alternativet **[!UICONTROL Add Production Pipeline]** markerat.
1. I dialogrutan **[!UICONTROL Add Production Pipeline]** som en del av **[!UICONTROL Configuration]** -stegen anger du namnet på din pipeline. Pipeline-elementets namn är till exempel `customcanvastheme`.
1. Klicka på **[!UICONTROL Continue]**.
1. Välj **[!UICONTROL Targeted Deployment]** > alternativen för **[!UICONTROL Front-end code]** i
**[!UICONTROL Source Code]** -stegen.
1. Markera värdena **[!UICONTROL Repository]** och **[!UICONTROL Git Branch]** som du har ändrat senast. Här är till exempel det valda databasnamnet `custom-canvas-theme-repo` och Git-grenen `main`.
1. Välj **[!UICONTROL Code Location]** som `/` om dina ändringar finns i rotmappen.
1. Klicka på **[!UICONTROL Save]**.
   ![skapa frontpipeline](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   När pipeline-konfigurationen är klar uppdateras call-to-action-kortet.

   >[!NOTE]
   >
   > [Ställ in Node.js-versionen till 20](#set-the-nodejs-vesrion-to-20) för att se till att frontendpipeline inte fungerar i Cloud Manager.

1. Högerklicka på den pipeline som skapats.
1. Klicka på **[!UICONTROL Run]** .

   ![run-a-pipleine](/help/forms/assets/canvas-theme-run-pipeline.png)

När bygget är klart blir temat tillgängligt vid författarinstansen för användning. Det visas under fliken **[!UICONTROL Style]** i guiden Skapa anpassat formulär när du skapar ett anpassat formulär.

![anpassat tema tillgängligt under formatfliken](/help/forms/assets/custom-theme-style-tab.png)

Det anpassade temat hjälper till att skapa en varumärkesanpassad upplevelse för Core Component-baserade Adaptive Forms.

## Använda ett tema i ett anpassat formulär {#using-theme-in-adaptive-form}

Steg för att tillämpa ett tema på ett adaptivt formulär är:

1. Logga in på din AEM Forms-författarinstans.

1. Välj **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.

1. Klicka på **Skapa** > **Adaptiv Forms**. Guiden för att skapa adaptiva formulär öppnas.

1. Markera kärnkomponentmallen på fliken **Source**.
1. Välj temat på fliken **Format**.
1. Klicka på **Skapa**.

Adaptiva formulärteman används som en del av en adaptiv formulärmall för att definiera format när du skapar ett adaptivt formulär.

## God praxis {#best-practices}

* **Undviker resurser från ett annat tema**

  När du redigerar ett tema kan du bläddra bland och lägga till resurser (till exempel bilder) från andra teman. Du redigerar till exempel bakgrunden på en sida. Om du till exempel väljer **[!UICONTROL Page]** ![edit-button](assets/edit-button.png)> **[!UICONTROL Background]** > **[!UICONTROL Add]** > **[!UICONTROL Image]** visas en dialogruta där du kan bläddra bland och lägga till bilder i andra teman.

  Du kan stöta på problem med det aktuella temat om en resurs läggs till från ett annat tema och det andra temat flyttas eller tas bort. Du bör undvika att bläddra bland och lägga till resurser från andra teman.

* **Ändrar behållarpanelens layoutbredd**

  Du bör inte ändra bredden på behållarpanelens layout. När du anger bredden på en behållarpanel blir den statisk och anpassas inte till olika skärmar.

## Frågor och svar {#faq}

**F:** Vilken anpassning prioriterar när du gör anpassningar i en temamapp på både global nivå och komponentnivå?

**Ans:** När anpassningar görs på både global nivå och komponentnivå prioriteras anpassningen på komponentnivå.



## Se även {#see-also}

{{see-also}}

* [Ange formulärlayout för olika skärmstorlekar och enhetstyper](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generera urkunder för adaptiva Forms (kärnkomponenter)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Skapa en adaptiv Forms med upprepningsbara avsnitt](/help/forms/create-forms-repeatable-sections.md)
* [Exempelmallar för teman och formulärdatamodeller](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
