---
title: Lägga till ett adaptivt formulär (kärnkomponenter) på AEM Sites-sidan
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: Du kan använda Adaptiv form (Core Components) på en AEM Sites-sida för att fylla i och skicka ett formulär utan att lämna AEM Sites sidor.
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 0d21b4ba2e7ce7592e3f2c57e4d320adc0af1008
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 0%

---

# Lägg till adaptiv Forms på en AEM Sites-sida {#add-an-adaptive-form-to-aem-sites-page}

## Översikt {#overview}

Du kan smidigt skriva eller bädda in Adaptiv Forms på en AEM Sites-sida så att användarna kan fylla i och skicka ett formulär utan att behöva lämna sajtsidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

Du kan välja någon av följande metoder för att skapa eller bädda in ett adaptivt formulär på en AEM Sites-sida:

* **Skapa ett anpassat formulär genom att dra och släppa formulärkomponenter i den adaptiva Forms Container-komponenten**: Använd [Adaptiv Forms-behållare](#af-container-component) om du vill skapa ett utrymme på webbsidan som innehåller det adaptiva formuläret. Du kan skapa ett formulär genom att dra och släppa adaptiva formulärkomponenter i det här området. Se till exempel videon nedan för att lära dig hur du skapar ett adaptivt formulär med [!UICONTROL Adaptive Forms Container] komponent:

The [Adaptiv formulärbehållare](#af-container-component) kan ni skapa digitala registreringsupplevelser genom att använda adaptiva Forms-komponenter direkt i AEM Sites redigerare. Integreringen ger en smidig upplevelse för de som skapar AEM Sites och vill skapa och hantera formulär på sina AEM Sites-sidor.

* **Bädda in ett befintligt anpassat formulär**: The [Adaptiv Forms - Embed(V2)](#embed-existing-af) kan du enkelt lägga in ett befintligt adaptivt formulär på en sida i AEM Sites. Bädda in ett anpassat formulär med [!UICONTROL Adaptive Forms - Embed] -komponenten på webbplatsens sida, som i följande video:

Den här funktionen gör det enklare att anpassa och återanvända Adaptive Forms. Integreringen är ett bekvämt sätt för kunder att återanvända adaptiva Forms som de redan har skapat.

* **Använd Adaptiv Forms-guide för att skapa ett formulär**:

   Använd [Adaptiv Forms - Embed(v2)](#embed-new-af) för att skapa ett adaptivt formulär i AEM Sites-redigeraren med hjälp av guiden Skapa formulär. Formuläret sparas som en extern entitet. Du kan även återanvända det här formuläret på andra webbplatssidor och i fristående formulär.
Se till exempel videon nedan om du vill lära dig hur du skapar och bäddar in ett nyskapat adaptivt formulär med [!UICONTROL Adaptive Forms - Embed] -komponenten på webbplatsens sida.

### Övervägande {#considerations}

Du kan använda regelredigeraren för att lägga till eller styra det dynamiska beteendet i adaptiva formulärkomponenter. Du kan till exempel dölja eller visa en komponent. Regelredigeraren är inte tillgänglig för icke-adaptiva formulärkomponenter. Så var försiktig när du använder icke-adaptiva formulärkomponenter i AEM Forms Container-komponenten.

## Skapa ett adaptivt formulär med hjälp av adaptiv Forms Container-komponent {#af-container-component}

The [!UICONTROL Adaptive Form Container] kan man skapa digitala registreringsupplevelser med hjälp av adaptiva Forms-komponenter i AEM Sites Editor. Du kan skapa ett anpassat formulär genom att dra och släppa formulärkomponenterna.

### Förutsättningar {#prerequisites-af-container}

+++ Aktivera **[!UICONTROL Adaptive Forms Container]** -komponenten i den associerade mallens policy.

Aktivera [!UICONTROL Adaptive Forms Container] utför följande steg i mallens policy:

1. Gå till [!UICONTROL Page Information] > [!UICONTROL Edit Template]
1. Klicka på [!UICONTROL Policy] och väljer **[!UICONTROL Adaptive Forms Container]**  kryssrutan under **[AEM Archetype Project Name] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Inkludera klientlibs på webbplatsens sida

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

Formuläret är klart. När du publicerar AEM Sites-sidan publiceras automatiskt ett adaptivt formulär och tillhörande refererade resurser.

#### Konfigurera egenskaper för adaptiv formulärbehållare {#configure-additional-settings-container}

Du kan anpassa de avancerade inställningarna för [!UICONTROL Adaptive Form Container] -komponenten. Du kan till exempel konfigurera förifyllningstjänsten så att den läser in ett adaptivt formulär med förfyllda värden på en webbplats sida. Du konfigurerar datamodellsinställningarna för att associera det adaptiva formuläret med en datamodell. Om du vill spara data på OneDrive eller SharePoint när du skickar ett anpassat formulär, konfigurerar du inställningarna för åtgärden Skicka. Du kan också lägga till en anpassad Skicka-åtgärd för din adaptiva Forms.

Ange egenskaperna för **[!UICONTROL Adaptive Forms Container]** klickar du på ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) i åtgärdsfältet. The **[!UICONTROL Edit Adaptive Forms Container]** öppnas.

![Dialogrutan Redigera](/help/forms/assets/adaptiveformcontainer-editdialog.png)

I [!UICONTROL Edit Adaptive Forms Container] kan du ange följande:
* **Fliken Grundläggande**
   * **Förifyllningstjänst**: Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Mer information om förifyllningstjänsten finns i [Förifyll adaptiva formulärfält](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Kategori för klientbibliotek**: Ange [JavaScript-funktioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) som används i uttryck och stöds av Adaptive Forms.
* **Datamodell**: Med en datamodell kan du integrera enheter och tjänster från olika datakällor i ett adaptivt formulär. Välj **[!UICONTROL Form Data Model]** om det adaptiva formulär som du skapar inbegriper att hämta och skriva data från och till flera datakällor.
   * **Formulärdatamodell**: Med en formulärdatamodell kan ett adaptivt formulär kommunicera med olika datakällor. Mer information om hur du konfigurerar en datakälla finns i [Konfigurera datakällor.](/help/forms/configure-data-sources.md)
   * **Schema**: Schema representerar den struktur i vilken data produceras eller används av det bakomliggande systemet i din organisation. Du kan [associera schemat med ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) och använder elementen för att lägga till dynamiskt innehåll i ett adaptivt formulär.

      >[!NOTE]
      >
      > När du har konfigurerat formulärdatamodellen kan du inte ändra den associerade formulärmodellen. Det går dock att ändra schemat som är kopplat till datamodellen Formulär.

* **Fliken Skicka**

   * **Omdirigera till URL**

      **Omdirigerings-URL/sökväg**: Anger den URL eller sökväg som ett anpassat formulär omdirigeras till efter att ha skickat.

      **Skicka åtgärd**: En sändningsåtgärd aktiveras när en användare klickar på knappen Skicka i ett anpassat formulär. Du kan [konfigurera skicka-åtgärden för anpassat formulär](/help/forms/configuring-submit-actions.md). Med adaptiva formulär kan du skicka in några få åtgärder:
      * Skicka till REST-slutpunkt
      * Skicka e-post
      * Skicka med formulärdatamodell
      * Anropa ett AEM arbetsflöde
      * Skicka till SharePoint
      * Skicka till OneDrive
      * Skicka till Azure Blob Storage

   Du kan också [utöka standardskickaåtgärder](custom-submit-action-form.md) för att skapa en egen anpassad skickaåtgärd.

* **Visa meddelande**
   * **Meddelandeinnehåll**: Skriv ett meddelande med RTF-redigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.

## Bädda in ett anpassat formulär  {#aem-container-component}

Använda **[!UICONTROL Adaptive Forms - Embed (V2)]** kan du antingen bädda in ett nytt adaptivt formulär eller bädda in ett befintligt adaptivt formulär på webbplatsens sida. The [!UICONTROL Adaptive Forms - Embed] kan du göra följande:

* [Bädda in ett befintligt anpassat formulär](#embed-new-af)

* [Skapa och bädda in ett nytt adaptivt formulär](#embed-existing-af)

### Förutsättningar {#prerequisites}

+++ Aktivera **Adaptiv Forms - Bädda in** -komponenten i den associerade mallens policy.

Aktivera [!UICONTROL Adaptive Forms - Embed(v2)] utför följande steg i mallens policy:

1. Gå till [!UICONTROL Page Information] > [!UICONTROL Edit Template]

1. Klicka på [!UICONTROL Policy] och väljer **[!UICONTROL Adaptive Form - Embed (v2)]** kryssrutan under **[!UICONTROL [AEM Archetype Project Name] - Forms]** grupp .
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Inkludera klientlibs på webbplatsens sida

När **[!UICONTROL When form covers entire width of a page]** alternativet är markerat i **[!UICONTROL Form Containers]** konfigurera dialogruta och **Adaptiv Forms med kärnkomponenter** om du använder dem måste du inkludera klientlibs på sidan för din motsvarande webbplats.

![Överlägg Gif](/help/forms/assets/overlaycorecomponent.gif)

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

   CustomFooterlibs.html används för JavaScript och customheaderlibs.html för CSS.

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera ändringarna.

+++

### Bädda in nytt anpassat formulär {#embed-new-af}

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponentens [!UICONTROL Adaptive Forms - Embed(v2)] på sidan.
1. Klicka på **Plus** och du omdirigeras till guiden för att skapa formulär.

   ![Adaptiv Forms - Bädda in komponent](/help/forms/assets/aemformcontainer.png)

1. Skapa ett nytt adaptivt formulär från [!UICONTROL Form Creation] guide.
1. The [!UICONTROL Asset Path] innehåller redan sökvägen till ett skapat adaptivt formulär
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

### Bädda in befintligt anpassat formulär {#embed-existing-af}

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponentens [!UICONTROL Adaptive Forms - Embed] på sidan.
1. Tryck på [!UICONTROL Adaptive Forms - Embed] på webbplatssidan och tryck på ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) i åtgärdsfältet. The **[!UICONTROL Edit Adaptive Forms - Embed]** öppnas.
1. Bläddra och välj det adaptiva formulär som ska bäddas in i [!UICONTROL Asset Path].
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

#### Konfigurera anpassad form _ Bädda in egenskaper

Du kan anpassa de avancerade inställningarna för [!UICONTROL Adaptive Form - Embed(v2)] -komponenten. I [!UICONTROL Edit Adaptive Forms - Embed(v2)] kan du ange följande:

* **Resurssökväg**: Bläddra och välj det adaptiva formulär som ska bäddas in. Den fylls i automatiskt om du släppte den från Assets-webbläsaren.
* **Efterbeställning** : Välj den åtgärd som ska utlösas när formulär skickas. Du kan välja att visa ett tackmeddelande eller en tacksida.
   * **Visa tackmeddelande**: Skriv ett meddelande med RTF-redigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
   * **Visa tacksida**: Bläddra och välj den sida som ska visas när formuläret skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Omdirigering till dig som tackar dig**: Aktivera alternativet att ersätta sidan som innehåller det inbäddade adaptiva formuläret med tacksidan. I annat fall ersätter tack-sidan det adaptiva formuläret i dialogrutan [!UICONTROL Adaptive Forms - Embed] utan att de underliggande webbplatserna uppdateras på sidan. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
* **Använd sidspråk**: Använd den lokala delen av AEM Sites-sidan i stället för den anpassade formulärens språkinställning.
* **Sätt fokus på formulär**: Välj det här alternativet om du vill ange fokus på det första fältet i det adaptiva formuläret.
* **Formuläret täcker ramens hela bredd**: Om du markerar det här alternativet används inte iframe för att återge formuläret.
* **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
* **CSS-klientbibliotek**: Ange sökväg till ett CSS-klientbibliotek.

### Publicera inbäddat adaptivt formulär {#publishing-embedded-adaptive-form}

Vi ska titta på följande scenarier för publicering av ett inbäddat adaptivt formulär på AEM webbplatssida:

* Om du publicerar sidan AEM webbplatser för första gången och den innehåller ett inbäddat adaptivt formulär publicerar du webbplatssidan och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret på en publicerad webbplatssida publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du har ändrat webbplatssidan och det inbäddade adaptiva formuläret publicerar du om webbplatssidan och den inbäddade resursen.

### Ändra inbäddat anpassat formulär  {#modifying-embedded-adaptive-form}

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret gör du något av följande.

* Öppna originalformuläret i ett adaptivt formulär i respektive redigerare och ändra dem.
* Tryck på det adaptiva formuläret på webbplatssidan i redigeringsläge och tryck sedan på **[!UICONTROL Edit in a new window]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

>[!NOTE]
>
>De ändringar som gjorts i det ursprungliga adaptiva formuläret återspeglas automatiskt i det inbäddade formuläret. Publicera dock om det adaptiva formuläret eller webbplatsens sida så att ändringarna på den publicerade sidan återspeglas.

### God praxis {#best-practices}

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickat Forms på Forms Portal.

[På AEM Sites-sidan visas layoutläget](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) Med kan du ändra storlek på ett anpassat formulär som har skapats eller bäddats in på en sida i en AEM.

![Stöd för AF-layout](/help/forms/assets/afsite-layoutsupport.gif)

Sidan AEM webbplatser innehåller en referens till det adaptiva formuläret. När du översätter en AEM Sites-sida översätts automatiskt ett adaptivt formulär och tillhörande refererade resurser med hjälp av [översättningsprojekt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) till andra språk.
