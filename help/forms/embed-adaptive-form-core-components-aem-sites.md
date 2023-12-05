---
title: Hur lägger man till eller skapar en adaptiv Form Core Components på AEM Sites-sidan?
description: Använd komponenter för adaptiv Form Core på en AEM Sites-sida för att fylla i och skicka ett formulär utan att lämna AEM Sites sidor.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 0%

---

# Skapa eller lägga till ett adaptivt formulär med AEM Sites Editor {#add-an-adaptive-form-to-aem-sites-page}

Du kan smidigt skriva eller bädda in Adaptiv Forms på en AEM Sites-sida så att användarna kan fylla i och skicka ett formulär utan att behöva lämna sajtsidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

Du kan välja någon av följande metoder för att skapa eller lägga till ett adaptivt formulär på en AEM Sites-sida:

* **Skapa ett adaptivt formulär med komponenten Adaptiv Forms Container**: [Adaptiv formulärbehållare](#af-container-component) kan ni skapa digitala registreringsupplevelser genom att använda adaptiva Forms-komponenter direkt i AEM Sites redigerare. Integreringen ger en smidig upplevelse för de som skapar AEM Sites och vill skapa och hantera formulär på sina AEM Sites-sidor.

* **Lägg till ett befintligt anpassat formulär**: [Adaptiv Forms - Embed(v2)](#embed-existing-af) kan du enkelt lägga till ett anpassat formulär på en sida i AEM Sites. Den här funktionen gör det enklare att anpassa och återanvända Adaptive Forms. Den här integreringen är ett bekvämt sätt för kunder att återanvända adaptiva Forms som de redan har skapat.

* **Använd Adaptiv Forms-guide för att skapa ett formulär**: Använd [Adaptiv Forms - Embed(v2)](#embed-new-af) för att skapa ett adaptivt formulär i AEM Sites-redigeraren med hjälp av guiden Skapa formulär. Formuläret sparas som en extern entitet. Du kan även återanvända det här formuläret på andra webbplatssidor och i fristående formulär.

* **Lägga till flera adaptiva Forms på en AEM Sites-sida**: Om du vill lägga till flera adaptiva Forms-filer på en AEM Sites-sida använder du AEM Forms behållarkomponenter - [Adaptiv Forms - Embed(v2)](#embed-new-af) och [Adaptiv formulärbehållare](#af-container-component). Om du behöver lägga till mer än ett adaptivt formulär som en div på en AEM Sites-sida kan du använda komponenten Adaptiv formulärbehållare.

Du kan använda regelredigeraren för att lägga till eller styra det dynamiska beteendet för adaptiva formulärkomponenter. Du kan till exempel dölja eller visa en komponent. Regelredigeraren är inte tillgänglig för icke-adaptiva formulärkomponenter. Så var försiktig när du använder icke-adaptiva formulärkomponenter i AEM Forms Container-komponenten.

## Skapa ett adaptivt formulär med komponenten Adaptiv Forms Container {#af-container-component}

The [!UICONTROL Adaptive Form Container] kan man skapa digitala registreringsupplevelser med hjälp av adaptiva Forms-komponenter i AEM Sites Editor. Du kan skapa ett anpassat formulär genom att dra och släppa formulärkomponenterna.

### Förutsättningar {#prerequisites-af-container}

+++ Aktivera **[!UICONTROL Adaptive Forms Container]** -komponenten.

Aktivera [!UICONTROL Adaptive Forms Container] utför följande steg i mallens policy:

1. Gå till [!UICONTROL Page Information] > [!UICONTROL Edit Template]
1. Klicka på [!UICONTROL Policy] och väljer **[!UICONTROL Adaptive Forms Container]**  kryssrutan under **[AEM Archetype Project Name] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Inkludera adaptiva Forms Client Libraries på AEM Sites

Om du vill använda adaptiva Forms-komponenter på en AEM Sites-sida inkluderar du kundbiblioteken CustomHeaderlibs och CustomFoterlibs på AEM Sites-sidan med hjälp av AEM Archetype/Git Repository och driftsättningsflödet.

1. Öppna [AEM Forms Archetype eller Klonad Git-databas](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) i en textredigerare. Exempel: Visual Studio Code.
1. Navigera till `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Kopiera värdet för `sling:resourceSuperType`. Värdet är till exempel `core/wcm/components/page/v3/page`.

   ![försäljningsresurs](/help/forms/assets/slingresource.png)

1. Skapa en liknande struktur på platsen `ui.apps/src/main/content/jcr_root/apps` samma som `core/wcm/components/page/v3/page`.

   ![övertäckningsstruktur](/help/forms/assets/overlaystructure.png)

1. Lägg till `customheaderlibs.html` och `customfooterlibs.html` filer.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   CustomFooterlibs.html används för JavaScript och customheaderlibs.html för css.

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera ändringarna.

+++

### Skapa ett adaptivt formulär med komponenten Adaptiv Forms Container {#create-af-using-af-container}


Skapa ett adaptivt formulär med [!UICONTROL Adaptive Forms Container] komponent:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponentens **[!UICONTROL Adaptive Forms Container]** på sidan.
1. Skapa ett adaptivt formulär med de adaptiva Forms-komponenterna.
1. Spara inställningarna.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Formuläret är klart. När du publicerar AEM Sites-sidan publiceras automatiskt det adaptiva formuläret och tillhörande refererade resurser.

#### Konfigurera egenskaper för adaptiv formulärbehållare {#configure-additional-settings-container}

Du kan anpassa de avancerade inställningarna för [!UICONTROL Adaptive Form Container] -komponenten. Exempel:

* Du kan konfigurera förifyllningstjänsten så att den läser in ett adaptivt formulär med förfyllda värden på en webbplats sida.
* Du kan konfigurera datamodellsinställningarna för att associera det adaptiva formuläret med en datakälla.
* Du kan konfigurera skicka-åtgärderna så att de skickar data på Microsoft® OneDrive, Microsoft® OneDrive eller andra datakällor när du skickar ett formulär. Du kan också skapa och välja en anpassad Skicka-åtgärd för din adaptiva Forms.

Ange egenskaperna för **[!UICONTROL Adaptive Forms Container]** klickar du på ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) i åtgärdsfältet. The **[!UICONTROL Edit Adaptive Forms Container]** öppnas.

![Dialogrutan Redigera](/help/forms/assets/adaptiveformcontainer-editdialog.png)

I [!UICONTROL Edit Adaptive Forms Container] kan du ange följande:
* **Fliken Grundläggande**
   * **Förifyllningstjänst**: Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Mer information om förifyllningstjänsten finns i [Förifyll adaptiva formulärfält](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Kategori för klientbibliotek**: Ange [JavaScript-funktioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) som används i uttryck och stöds av Adaptive Forms.
* **Datamodell**: Med en datamodell kan du integrera enheter och tjänster från olika datakällor i ett adaptivt formulär. Välj **[!UICONTROL Form Data Model]** om det adaptiva formulär som du skapar inbegriper att hämta och skriva data från och till flera datakällor.
   * **Formulärdatamodell**: Med en formulärdatamodell kan ett adaptivt formulär kommunicera med olika datakällor. Mer information om hur du konfigurerar en datakälla finns i [Konfigurera datakällor](/help/forms/configure-data-sources.md).
   * **Schema**: Schema representerar den struktur i vilken data produceras eller används av det bakomliggande systemet i din organisation. Du kan [associera schemat med ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) och använder elementen för att lägga till dynamiskt innehåll i ett adaptivt formulär.

     >[!NOTE]
     >
     > När formulärdatamodellen har konfigurerats kan du inte ändra den associerade formulärmodellen. Det går dock att ändra schemat som är kopplat till datamodellen Formulär.

* **Fliken Skicka**

   * **Omdirigera till URL**
      * **Omdirigerings-URL/sökväg**: Anger den URL eller sökväg som ett anpassat formulär ska omdirigeras till efter överföringen.

      * **Skicka åtgärd**: En skicka-åtgärd utlöses när en användare klickar på Skicka-knappen i ett anpassat formulär. Du kan [konfigurera skicka-åtgärden för anpassat formulär](/help/forms/configuring-submit-actions.md). Adaptiva formulär innehåller följande inskickningsåtgärder:
         * Skicka till REST-slutpunkt
         * Skicka e-post
         * Skicka med formulärdatamodell
         * Anropa ett AEM
         * Skicka till SharePoint
         * Skicka till OneDrive
         * Skicka till Azure Blob Storage

  Du kan också [utöka standardåtgärderna för att skicka](custom-submit-action-form.md) för att skapa en egen anpassad skickaåtgärd.

* **Visa meddelande**
   * **Meddelandeinnehåll**: Skriv ett meddelande med textredigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.

## Bädda in ett anpassat formulär  {#aem-container-component}

Använda **[!UICONTROL Adaptive Forms - Embed (V2)]** kan du antingen bädda in ett nytt adaptivt formulär eller bädda in ett befintligt adaptivt formulär på webbplatsens sida. The [!UICONTROL Adaptive Forms - Embed(v2)] kan du göra följande:

* [Lägg till ett befintligt anpassat formulär](#embed-new-af)

* [Skapa och lägga till ett nytt adaptivt formulär](#embed-existing-af)

### Förutsättningar {#prerequisites}

+++ Aktivera **Adaptiv Forms - Bädda in** -komponenten.

Aktivera [!UICONTROL Adaptive Forms - Embed(v2)] utför följande steg i mallens policy:

1. Gå till [!UICONTROL Page Information] > [!UICONTROL Edit Template]

1. Klicka på [!UICONTROL Policy] och väljer **[!UICONTROL Adaptive Form - Embed (v2)]** kryssrutan under **[!UICONTROL [AEM Archetype Project Name] - Forms]** grupp .
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Inkludera adaptiva Forms Client Libraries på AEM Sites

När **[!UICONTROL When form covers entire width of a page]** alternativet är markerat i **[!UICONTROL Form Containers]** konfigurera dialogruta och **Adaptiv Forms med kärnkomponenter** om du använder dem måste du inkludera klientlibs på sidan för din motsvarande webbplats.

![Överlägg Gif](/help/forms/assets/overlaycorecomponent.gif)

Om du vill använda adaptiva Forms-komponenter på en AEM Sites-sida inkluderar du `Customheaderlibs` och `Customfooterlibs` klientbibliotek till AEM Sites-sidan med AEM Archetype/Git Repository och distribution.

1. Öppna [AEM Forms Archetype eller Klonad Git-databas](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) i en textredigerare. Exempel: Visual Studio Code.
1. Navigera till `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Kopiera värdet för `sling:resourceSuperType`. Värdet är till exempel `core/wcm/components/page/v3/page`.

   ![försäljningsresurs](/help/forms/assets/slingresource.png)

1. Skapa en liknande struktur på platsen `ui.apps/src/main/content/jcr_root/apps` samma som `core/wcm/components/page/v3/page`.

   ![övertäckningsstruktur](/help/forms/assets/overlaystructure.png)

1. Lägg till `customheaderlibs.html` och `customfooterlibs.html` filer.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   The `customfooterlibs.html` används för JavaScript och `customheaderlibs.html` för CSS.

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera ändringarna.

+++

### Lägg till ett befintligt anpassat formulär på AEM Sites-sidan {#embed-existing-af}

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponentens [!UICONTROL Adaptive Forms - Embed] på sidan.
1. Välj [!UICONTROL Adaptive Forms - Embed] på webbplatssidan och markera ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) i åtgärdsfältet. The **[!UICONTROL Edit Adaptive Forms - Embed]** öppnas.
1. Bläddra och välj det adaptiva formulär som ska bäddas in i [!UICONTROL Asset Path].
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### Skapa och lägg till nya adaptiva formulär på AEM Sites-sidan {#embed-new-af}

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponentens [!UICONTROL Adaptive Forms - Embed(v2)] på sidan.
1. Klicka på **Plus** och du omdirigeras till guiden för att skapa formulär.

   ![Adaptiv Forms - Bädda in komponent](/help/forms/assets/aemformcontainer.png)

1. Skapa ett nytt adaptivt formulär från [!UICONTROL Form Creation] guide.
1. The [!UICONTROL Asset Path] innehåller redan sökvägen till ett skapat adaptivt formulär
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### Konfigurera anpassad form - egenskaper för inbäddning (v2) {#configure-adaptive-form-embed}

Du kan anpassa de avancerade inställningarna för [!UICONTROL Adaptive Form - Embed(v2)] -komponenten. I [!UICONTROL Edit Adaptive Forms - Embed(v2)] kan du ange följande:

* **Resurssökväg**: Bläddra och välj det adaptiva formulär som ska bäddas in. Den fylls i automatiskt om du släppte den från Assets-webbläsaren.
* **Efterbeställning** : Välj den åtgärd som ska utlösas när formulär skickas. Du kan visa ett tackmeddelande eller en tacksida.
   * **Visa tackmeddelande**: Skriv ett meddelande med textredigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
   * **Visa tacksida**: Bläddra och välj den sida som ska visas när formuläret skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Omdirigering till dig som tackar dig**: Aktivera alternativet att ersätta sidan som innehåller det inbäddade adaptiva formuläret med tacksidan. I annat fall ersätter tack-sidan det adaptiva formuläret i dialogrutan [!UICONTROL Adaptive Forms - Embed] utan att uppdatera underliggande webbplatser på sidan. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
* **Använd sidspråk**: Använd lokala sidor på AEM Sites-sidan i stället för anpassade formulär.
* **Sätt fokus på formulär**: Välj det här alternativet om du vill fokusera på det första fältet i det adaptiva formuläret.
* **Formuläret täcker ramens hela bredd**: Om det här alternativet är markerat används inte iframe för att återge formuläret.
* **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
* **CSS-klientbibliotek**: Ange sökväg till ett CSS-klientbibliotek.

### Publicera tillagd adaptiv Forms med hjälp av adaptiv form - komponenten Embed(v2)  {#publish-embedded-adaptive-form}

Tänk på följande scenarier för publicering av tillagd Adaptive Forms med **[!UICONTROL Adaptive Form - Embed(v2)]** komponent:

* När du publicerar en AEM Sites-sida för första gången publiceras de formulär som läggs till på sidan Webbplatser automatiskt.
* När du ändrar ett adaptivt formulär som lagts till på en redan publicerad webbplats publicerar du motsvarande adaptiva Forms manuellt.
* När du ändrar en sajtsida och motsvarande adaptiva Forms publicerar du om sidan Webbplatser och alla adaptiva Forms som lagts till på sidan Webbplatser.

### Modifiera tillagd adaptiv-Forms med hjälp av adaptiv form - komponenten Embed(v2)  {#modifying-embedded-adaptive-form}

Gör något av följande om du vill ändra någon konfiguration eller egenskap för ett adaptivt formulär:

* Öppna originalformuläret i ett adaptivt formulär i respektive redigerare och ändra dem.
* Markera det adaptiva formuläret på webbplatssidan i redigeringsläge och välj sedan **[!UICONTROL Edit in a new window]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

## Ändra layout för ett adaptivt formulär som lagts till på en AEM Sites-sida {#change-layout-af-aem-sites-page}

På AEM Sites-sidan [Layoutläge](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) Med kan du ändra storlek på ett anpassat formulär som skapas eller läggs till på en AEM Sites-sida.

![Stöd för AF-layout](/help/forms/assets/afsite-layoutsupport.gif)

Sidan AEM webbplatser innehåller en referens till det adaptiva formuläret. När du översätter en AEM Sites-sida översätts automatiskt ett adaptivt formulär och tillhörande refererade resurser med hjälp av [översättningsprojekt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) till andra språk.

## God praxis {#best-practices}

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickat Forms på Forms Portal.

>[!MORELIKETHIS]
>
>* [Bädda in anpassningsbara formulär baserade på kärnkomponenter på en extern webbsida](/help/forms/embed-adaptive-form-core-components-external-web-page.md)
>* [Bädda in anpassningsbara formulär på en extern webbsida](/help/forms/embed-adaptive-form-external-web-page.md)