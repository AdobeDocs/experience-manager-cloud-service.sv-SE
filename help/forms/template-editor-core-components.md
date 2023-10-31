---
title: Hur skapar man en adaptiv blankettmall som bygger på kärnkomponenten?
description: Skapa adaptiva formulärmallar baserade på kärnkomponenten för att definiera den grundläggande strukturen och det ursprungliga innehållet med mallredigeraren.
Keywords: create adaptive form template, create adaptive form template based on core components, Use template to create adpative form.
exl-id: c1c050d3-953e-4e56-a96b-d84f2ec05e5e
source-git-commit: f562d082520037fa1b15272c763d35e93dab137f
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 0%

---

# Skapa en adaptiv formulärmall baserad på kärnkomponenter {#adaptive-form-templates}

När du skapar ett formulär lägger du till fält och komponenter för att definiera formulärstruktur, innehåll och åtgärder i redigeraren. Du lägger till fält och komponenter i `guideRootPanel` för formulärbehållaren. Med mallredigeraren kan du skapa en mall som innehåller grundläggande struktur och ursprungligt innehåll som författare kan använda för att skapa formulär.

Du vill till exempel att alla formulärförfattare ska ha vissa textrutor, navigeringsknappar och en skicka-knapp i ett registreringsformulär. Du kan skapa en mall med de komponenter som författare kan använda för att skapa ett formulär som är konsekvent med andra registreringsformulär. När författare använder mallen för att skapa ett adaptivt formulär ärver det nya formuläret strukturen och de komponenter du har angett i mallen. Med mallredigeraren kan du:

* Lägg till sidhuvud- och sidfotskomponenter i ett formulär i strukturlagret.
* Ange formulärets ursprungliga innehåll.
* Ange ett tema, Skicka åtgärder.

<!--
You can download and install [!DNL AEM Forms] reference content package from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal to import reference themes and templates to your environment.
-->

## Förutsättning

**Aktivera adaptiva Forms Core-komponenter för din miljö**: När du skapar ett program är de adaptiva Forms Core-komponenterna redan aktiverade för din miljö. Om du har en as a Cloud Service formulärmiljö baserad på [AEM Archetype 39 eller tidigare](https://github.com/adobe/aem-project-archetype), [Aktivera adaptiva Forms Core-komponenter för din miljö](enable-adaptive-forms-core-components.md).

>[!NOTE]
>
> Vid driftsättning av Forms as a Cloud Service miljö baserad på Archetype 45, **Adaptiv Forms (kärnkomponent)** -mallar och kärnkomponentbaserade teman läggs till i din miljö.

## Arbeta med mall {#working-with-templates}

Du kommer åt mallredigeraren på Verktyg-menyn genom att gå till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]**. Här är mallarna ordnade i mappar som är aktiverade för redigerbara mallar.

>[!NOTE]
>
> Du hittar de redigerbara mallarna som bygger på kärnkomponenten i kärnkomponentspecifika mappar.

I Experience Manager finns en global mapp där du kan ordna mallar. Den är dock inte aktiverad som standard. Du kan begära att administratören aktiverar den globala mappen eller skapar en mapp för mallar. Mer information om hur du skapar mappar finns i [Mallmappar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

## Skapa en mall {#create-template}

När du har skapat en mapp öppnar du mappen och utför följande steg för att skapa en mall:

1. Tryck **[!UICONTROL Create]** i den mapp du har skapat.
1. I **[!UICONTROL Pick a Template Type]** avsnitt, markera **[!UICONTROL Adaptive Form (Core Component) template]** och knacka **[!UICONTROL Next]**.

1. I **[!UICONTROL Template Details]** -avsnitt, ange **Malltitel** och knacka **[!UICONTROL Create]**.
Du kan också ange en beskrivning.

1. Tryck **[!UICONTROL Done]** för att gå tillbaka till konsolen, eller tryck **[!UICONTROL Open]** om du vill öppna mallen i redigeraren.

## Mallredigeringsgränssnitt {#template-editor-ui}

När du öppnar en mall för redigering kan du se följande AEM Editor-komponenter:

* **Verktygsfältet Sida**
Innehåller följande alternativ:

   * **Växla sidopanel**: Visa eller dölj sidofältet.
   * **Sidinformation**: Gör att du kan ange information som publicerings-/avpubliceringstid, miniatyrbilder, klientbibliotek, sidprincip och klientbibliotek för siddesign.
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Lägesväljare:** Gör att du kan ändra läge. Du kan **[!UICONTROL Structure]** läge, **[!UICONTROL Initial Content]**, **[!UICONTROL Layout Control]** läge. I strukturläget kan du lägga till och anpassa sidhuvud och sidfot. Med det inledande innehållsläget kan du anpassa formulärinnehållet.
   * **Förhandsgranska:** Gör att du kan förhandsgranska hur mallen ser ut när du publicerar den. Du kan använda Lagerväljaren och Förhandsgranska för att växla redigerings- och förhandsgranskningslägen.
* **Sidofält:** Tillhandahåller webbläsarna Innehåll, Egenskaper, Resurser och Komponenter.
* **Komponentverktygsfältet:** När du markerar en komponent visas ett verktygsfält där du kan anpassa komponenten.
* **Sida**: Det område där du lägger till innehåll för att skapa mallen.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

## Redigera en mall {#editing-a-template}

Olika lägen för att markera och redigera rätt aspekt av mallen är:

* [Struktur](#structure)
* [Ursprungligt innehåll](#initial-content)
* [Layout](#layout)

Lagerväljaren är tillgänglig bredvid alternativet Förhandsgranska i skärmens övre högra hörn.

### Struktur {#structure}

När du markerar strukturlagret i mallredigeraren kan det vara bra att fördefiniera det innehåll som inte kan ändras när du skapar adaptiv Forms som är associerat med mallen.

<!-- you can see the layout containers above and below the Adaptive Form Container. Authors can use these layout containers for header and footer. -->


![Layoutbehållare i strukturlagret](/help/forms/assets/header-layer-selector-core-component.png)

<!--

**A. Layout container for Header component**
Drag-drop the Adaptive Form Header component in the layout container above the Adaptive Form Container. After you add the component, you can specify its properties that let you add a logo and provide its title.
**B. Adaptive Form Container component**
Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. After you add the components, you can specify its properties.
**C. Layout container for Footer component**
Similarly, when you drag-drop the footer component in the layout container below the Adaptive Form Container, you can provide the copyright information and company details. 
You can add, edit, or customize the header and footer. Drag-drop the Adaptive Form Header and Footer component to customize the template. Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. 


Header and footer are added in the Initial Content layer.
-->

#### Låsa/låsa upp komponenter i strukturlagret {#locking-unlocking-components-in-the-structure-layer}

När du redigerar mallen med strukturlagret markerat kan du låsa upp mallens sidhuvud och sidfot. Om en komponent är olåst i mallen kan formulärförfattare redigera komponenten i det adaptiva formulär som använder mallen. Genom att låsa en komponent förhindrar du att formulärförfattare redigerar den i det adaptiva formuläret. Alternativet Lås är tillgängligt i komponentens verktygsfält.

Du kan till exempel lägga till rubrikkomponenten i mallen. När du markerar komponenten kan du se ett låsalternativ i komponentens verktygsfält. Vanligtvis innehåller rubriken företagsnamn och logotyp, och du vill inte att formulärförfattare ska ändra logotypen och rubriken i en mall. I ett adaptivt formulär som skapats med mallen med huvudkomponenten låst kan formulärförfattare inte ändra logotypen och företagsnamnet.

>[!NOTE]
>
>Du bör inte låsa eller låsa upp en bild eller logotyp separat i rubrikkomponenten. Du kan låsa upp rubrikkomponenten.

### Ursprungligt innehåll {#initial-content}

När alternativet Ursprungligt innehåll är markerat öppnas mallens adaptiva formulärbehållare som ett adaptivt formulär för redigering. Med den kan du skapa ett fördefinierat innehåll som kan ändras när du skapar adaptiv Forms som är kopplat till mallen. Precis som när du skapar ett adaptivt formulär kan du ange inledande inställningar, som att välja ett tema och skicka åtgärder.

Formulärförfattare använder det som bas för att skapa ett formulär. Innehållsflödesstrukturen anges i lagret Ursprungligt innehåll i mallen. Om du vill växla till att redigera det ursprungliga innehållet i formulärmallen innan du förhandsgranskar i sidverktygsfältet trycker du på ![canvas-drop-down](assets/canvas-drop-down.png) **>** **[!UICONTROL Initial Content]**.

![Sidhuvud och sidfot som lagts till i lagret Ursprungligt innehåll](assets/header-and-footer.png)

I lagret Ursprungligt innehåll skapar du mallen Adaptivt formulär som dina författare använder som bas. Om du redigerar en mall på samma sätt som när du redigerar ett formulär, använder du de alternativ som finns i sidofältet. Sidofältet innehåller webbläsare för innehåll, egenskaper, resurser och komponenter.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>När du väljer Lagra innehåll eller Lagra PDF som överföringsåtgärd får du ett alternativ för att ange lagringssökvägen. Om du anger en sökväg i en mall får alla formulär som skapas från den samma sökväg. Du kan ange rätt lagringssökväg eller se till att formulärförfattare uppdaterar den för att förhindra att data från alla formulär lagras på samma plats.

### Layout {#layout}

När du redigerar en mall kan du definiera layouten, vilket innebär att en responsiv standardlayout används. Layouten hjälper till att hantera bredden på en komponent baserat på enhetens bredd för att underlätta en responsiv adaptiv formulärdesign.

![Layoutbehållare i strukturlagret](/help/forms/assets/layout-template-core-component.png)

Läs artikeln [förstå responsiv layout](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/responsive-layout-feature-video-understand.html?lang=en) om du vill ha mer information.

## Aktivera mallen {#enabling-the-template}

När du skapar en mall läggs den till som ett utkast. Aktivera mallen för att använda den för att skapa Adaptiv Forms. Så här aktiverar du en mall:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Templates]**och öppna mappen där du har skapat mallen.
Mallen som du har skapat markeras som Utkast.
1. Markera mallen och tryck på **[!UICONTROL Enable]** i verktygsfältet.
När du skapar ett adaptivt formulär kan du se mallen som visas när du ombeds att välja en mall.

## Importera eller exportera en mall {#importing-or-exporting-a-template}

Ett formulär fungerar med sin mall. När du hämtar ett adaptivt formulär som skapats med en anpassad mall hämtas inte mallen. När du importerar formuläret till ett annat [!DNL AEM Forms] -instansen importeras den utan sin mall. Om ett formulär importeras men mallen inte är tillgänglig, återges inte formuläret. Du kan paketera den anpassade mallen från `/conf` nod i `https://<server>:<port>/crx/packmgr`och lägga in den i [!DNL AEM Forms] instans där du vill överföra formuläret. Du kan också [Skapa en mall med AEM Archetype och distribuera den till din Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * Du kan även konfigurera [!UICONTROL Document of Record] direkt från redigeraren för adaptiva formulär eller redigeraren för adaptiva formulärmallar. Mer information finns i [Generera arkivdokument för adaptiv Forms](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

## Koppla ett formulärdatamodellschema till en mall {#associating-form-data-model-schema-in-template}

Författare kan associera en [!UICONTROL Form Data Model Schema] till en adaptiv formulärmall i mallredigeraren. Det gör att författare kan välja ett schema i mallredigeraren. När du kopplar ett schema till en mall och en formulärförfattare skapar ett formulär baserat på mallen, markeras schemat automatiskt för formuläret. Det hjälper formulärförfattare att reglera användningen av scheman och sparar tid även för formulärförfattare. Så här väljer du ett formulärdatamodellschema i mallredigeraren:

1. Tryck **[!UICONTROL Content Browser]** till vänster.
1. Gå till formulärbehållaren **[!UICONTROL Setting]**.
1. Välj **[!UICONTROL Data Model]**.
1. Välj formulärdatamodell genom att **[!UICONTROL Select Form Data Model]** och spara konfigurationen.

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img-core-component.png)

<!--

## Creating an Adaptive Form template with tabs and panels {#creating-an-adaptive-form-template-with-tabs-and-panels-nbs}

For example, you want to create a template with the following tabs:

* General Information
* Professional Information

You have added a logo, provided a title, and added a footer in the structure layer. Lock the header and footer to stop form authors from editing them when they use the template to create forms.

Change the layer from **Structure** to **Initial Content**, and start adding content to the form. To create a tabbed structure, add a child Panel in the guideRootPanel of the Adaptive Form container. To add a panel:

* You can add a panel by tapping the **[!UICONTROL +]** button when you select the **[!UICONTROL Drag components here]** option.

* You can drag-drop the panel component from the components browser in the sidebar.
* You can add child panel of the `guideRootPanel` from the component toolbar.

To create the General Information and Professional Information tabs, add two panels in the child panel of the `guideRootPanel`. Select the panels and tap ![cmppr](assets/configure-icon.svg) to open the properties in the sidebar. Change the element names as `general-info` and `professional-info`, and titles as General Information and Professional Information respectively. In the sidebar, tap content to open the content browser. In the Form Objects tab, select `guideRootPanel`. In the editor, the guideRootPanel is selected. Tap ![cmppr](assets/configure-icon.svg) in the component toolbar to open its properties. In the Panel Layout field, select **[!UICONTROL Tabs on Top]** and tap **[!UICONTROL Done]**. The tabbed template structure is applied.

### Adding content in tabs {#adding-content-in-tabs}

After you add panels and structure them as tabs, you can add fields inside the tabs. When you select a tab in the editor, you can see the **[!UICONTROL Drag components here]** option. You can drag-drop components such as text-boxes, list items, and buttons. You can drag-drop components from the components browser in the sidebar.

Each component has properties that enhance data capturing and manipulation. For example, you can enable the **[!UICONTROL Required field]** property of a component. Your authors can specify a message that your customers see when they skip filling a required field. Specify the message in **[!UICONTROL Required Field Message]** property.

In the example template, Name, Phone number, and Date of birth fields are added in the General Information tab. In the Professional Information tab, Currently employed, employment type, Educational qualification fields are added.

After you have added fields, you can add buttons such as Submit and Reset.
-->

### Lägga till anpassade egenskaper i adaptiva formulärkomponenter med hjälp av en mallpolicy

Med anpassade egenskaper kan du koppla anpassade attribut (nyckelvärdepar) till en anpassad formulärets kärnkomponent med hjälp av formulärmallen. De anpassade egenskaperna visas i **[!UICONTROL properties]** i den headless-renderingen av komponenten. Det gör att du kan skapa dynamiskt formulärbeteende som anpassas baserat på anpassade attributvärden. Utvecklare kan till exempel utforma olika renderingar av en Headless Forms-komponent för mobiler, datorer eller webbplattformar, vilket avsevärt förbättrar användarupplevelsen på en mängd olika enheter.

Steg för att lägga till anpassade egenskaper i komponentfält för adaptiva formulär är:

1. [Lägga till ett anpassat gruppnamn i principen för en mallredigerare](#add-a-custom-group-name)
1. [Välj ett eget gruppnamn i redigeringsdialogrutan för komponenten för ett adaptivt formulär](#select-a-custom-group-name)

#### Lägga till ett anpassat gruppnamn i principen för mallredigeraren {#add-a-custom-group-name}

1. Gå till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]**.
1. Markera mallen baserat på kärnkomponenter och öppna den i redigeringsläge.
1. Klicka på **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) ikonen för ett fält av typen Adaptiv Form Core Component där de anpassade egenskaperna måste definieras. The **[!UICONTROL Adaptive Form Field]** visas.
1. Välj **[!UICONTROL Custom Properties]** -fliken.
1. Ange **[!UICONTROL Policy Title]** under **[!UICONTROL Policy]** -avsnitt.
1. Ange **[!UICONTROL Group name]** och lägg till nyckelvärdepar som är kopplade till en viss grupp. Gruppnamnet är synligt för formulärförfattare i redigeringsdialogrutan för en komponent. Om du väljer gruppnamnet kan alla associerade nyckelvärdepar användas för en komponent.
1. Klicka **[Klar]**.

![Lägga till gruppnamn för anpassade egenskaper i mallredigeraren](/help/forms/assets/custom-properties-core-component.png)

När du lägger till minst en anpassad egenskapsgrupp med hjälp av mallprincipen visas **[!UICONTROL Advanced]** visas i dialogrutan Redigera för en motsvarande kärnkomponent.

#### Välj ett eget gruppnamn i redigeringsdialogrutan för en kärnkomponent {#select-a-custom-group-name}

1. Öppna ett adaptivt formulär i redigeringsläge.
1. Tryck på komponenten som de anpassade egenskaperna har definierats för i mallredigeraren och tryck sedan på ![settings_icon](assets/configure-icon.svg) för att öppna komponentens redigeringsdialogruta.
1. Välj **[!UICONTROL Advanced]** -fliken.
1. Välj det anpassade egenskapsgruppnamnet från **[!UICONTROL Custom Property Select]** nedrullningsbar meny. Alla definierade egna gruppnamn fylls i automatiskt i listrutan.
1. Tryck **[!UICONTROL Done]** för att spara egenskaperna.

![välj namn på anpassad egenskapsgrupp](/help/forms/assets/select-custom-properties-group-name.png)

>[!NOTE]
>
> * The **[!UICONTROL Additional Custom Properties]** Med kryssrutan kan du lägga till komponentspecifika anpassade egenskaper dynamiskt utöver de som anges i mallprincipen. Den anpassade egenskapen för den specifika komponenten har företräde framför den anpassade egenskapen som angetts i mallprincipen när nyckelnamnsvärdena matchar.

## Skapa ett anpassat formulär med hjälp av mallen {#creating-an-adaptive-form-using-the-template}

När du har skapat och aktiverat en mall är den tillgänglig i formulärhanteraren när du skapar ett anpassat formulär. Information om hur du använder en mall och skapar ett adaptivt formulär finns i [Skapa ett adaptivt formulär baserat på kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md).
<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, and you want it to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. 

## Save an Adaptive Form as a template {#saving-adaptive-form-as-template}

You can also save an Adaptive Form as a template for future use. To save a Adaptive Form as a template:

1. Select an Adaptive Form to save it as a template.
1. Click **[!UICONTROL Save as Template]**. A dialog box appears.
1. Specify **[!UICONTROL Title]** (mandatory field), **[!UICONTROL Location]** (mandatory field) and **[!UICONTROL Description]** (optional field) for the template. 
1. Click **[!UICONTROL Create]**.

   ![Save as Form as Template](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>To use the same container policy as of the source Adaptive Form, it is recommended to save the template in the same folder as of the source Adaptive Form. In case, the template is saved in any other folder, than the created template uses a default container policy.
-->

## Bästa praxis {#best-practices}

* Skapa mallar med komponenterna som bygger på kärnkomponenter, till exempel adaptiv formulärtext, adaptiv formulärbehållare med mera. Om du vill ha information om adaptiva Forms Core-komponenter [klicka här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html).
* Begränsa antalet mallar så att de matchar de i grunden olika formulärtyperna som finns på webbplatserna
* Ge de anpassade komponenter som används i en mall den flexibilitet och konfigurationsmöjligheter som behövs.

<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)

-->

## Se även {#see-also}

{{see-also}}
* [Skapa stilar eller teman för formulären](using-themes-in-core-components.md)
* [Skapa en adaptiv form (kärnkomponenter)](/help/forms/creating-adaptive-form-core-components.md)

