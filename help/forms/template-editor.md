---
title: Hur skapar vi en anpassad formulärmall?
description: Skapa adaptiva formulärmallar för att definiera den grundläggande strukturen och det ursprungliga innehållet med mallredigeraren.
feature: Adaptive Forms, Foundation Components
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
role: User, Developer, Admin
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1994'
ht-degree: 0%

---

# Skapa en adaptiv formulärmall {#adaptive-form-templates}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/template-editor.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

När du skapar ett formulär lägger du till fält och komponenter för att definiera formulärstruktur, innehåll och åtgärder i redigeraren. Du lägger till fält och komponenter i `guideRootPanel` för formulärbehållaren. Med mallredigeraren kan du skapa en mall som innehåller grundläggande struktur och ursprungligt innehåll som författare kan använda för att skapa formulär.

Du vill till exempel att alla formulärförfattare ska ha vissa textrutor, navigeringsknappar och en skicka-knapp i ett registreringsformulär. Du kan skapa en mall med de komponenter som författare kan använda för att skapa ett formulär som är konsekvent med andra registreringsformulär. När författare använder mallen för att skapa ett adaptivt formulär ärver det nya formuläret strukturen och komponenterna som du har angett i mallen. Med mallredigeraren kan du:

* Lägg till sidhuvud- och sidfotskomponenter i ett formulär i strukturlagret.
* Ange formulärets ursprungliga innehåll.
* Ange ett tema, Skicka åtgärder.

Du kan hämta och installera [!DNL AEM Forms]-referenspaketet för innehåll från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) om du vill importera referensteman och mallar till din miljö.

## Arbeta med mallar {#working-with-templates}

Du kommer åt mallredigeraren på Verktyg-menyn genom att gå till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]**. Här är mallarna ordnade i mappar som är aktiverade för redigerbara mallar.

I Experience Manager finns en global mapp där du kan ordna mallar. Den är dock inte aktiverad som standard. Du kan begära att administratören aktiverar den globala mappen eller skapar en mapp för mallar. Mer information om hur du skapar mappar finns i [Mallmappar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html?lang=sv-SE#editing-templates-template-authors).

### Skapa en mall {#create-template}

När du har skapat en mapp öppnar du mappen och utför följande steg för att skapa en mall:

1. Välj **[!UICONTROL Create]** i mappen som du har skapat.
1. I avsnittet Välj en malltyp väljer du **[!UICONTROL Adaptive Form template]** och sedan **[!UICONTROL Next]**.

1. Ange en malltitel i avsnittet Mallinformation och välj **[!UICONTROL Create]**.
Du kan också ange en beskrivning.

1. Välj **[!UICONTROL Done]** om du vill återgå till konsolen eller välj **[!UICONTROL Open]** om du vill öppna mallen i redigeraren.

### Mallredigeringsgränssnitt {#template-editor-ui}

När du öppnar en mall för redigering kan du se följande AEM Editor-komponenter:

* **Verktygsfältet Sida**
Innehåller följande alternativ:

   * **Växla sidopanel**: Här kan du visa eller dölja sidofältet.
   * **Sidinformation**: Gör att du kan ange information som publicerings-/avpubliceringstid, miniatyrer, klientbibliotek, sidprincip och klientbibliotek för siddesign.
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Lägesväljare:** Du kan ändra läge.Du kan välja **[!UICONTROL Structure]** läge, **[!UICONTROL Initial Content]**, **[!UICONTROL Layout Control]** läge. I strukturläget kan du lägga till och anpassa sidhuvud och sidfot. Med det inledande innehållsläget kan du anpassa formulärinnehållet.
   * **Förhandsgranska:** Du kan förhandsgranska hur mallen ser ut när du publicerar den. Du kan använda Lagerväljaren och Förhandsgranska för att växla redigerings- och förhandsgranskningslägen.
* **Sidofältet:** Tillhandahåller webbläsarna Innehåll, Egenskaper, Assets och Komponenter.
* **Komponentverktygsfältet:** När du markerar en komponent visas ett verktygsfält där du kan anpassa komponenten.
* **Sida**: Det område där du lägger till innehåll för att skapa mallen.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### Redigera en mall {#editing-a-template}

En mall för anpassat formulär skapas med två lager:

* Struktur
* Ursprungligt innehåll

Lagerväljaren är tillgänglig bredvid alternativet Förhandsgranska i skärmens övre högra hörn.

### Struktur {#structure}

När du markerar strukturlagret i mallredigeraren kan du se layoutbehållarna ovanför och under den adaptiva formulärbehållaren. Författare kan använda dessa layoutbehållare för sidhuvud och sidfot. Du kan lägga till, redigera eller anpassa sidhuvudet och sidfoten. Dra och släpp komponenten Adaptiv formulärrubrik i layoutbehållaren ovanför den adaptiva formulärbehållaren för att anpassa mallrubriken. Dra och släpp komponenten Adaptiv formulärsidfot i layoutbehållaren nedanför den adaptiva formulärbehållaren för att anpassa mallsidfoten.

![Layoutbehållare i strukturlagret](assets/header-layer-selector.png)

Layoutbehållare i strukturlagret

**A.** Layoutbehållare för huvudkomponent **B.** Layoutbehållare för sidfotskomponent

Dra och släpp komponenten Adaptiv formulärrubrik i layoutbehållaren ovanför behållaren för adaptiv form. När du har lagt till komponenten kan du ange dess egenskaper så att du kan lägga till en logotyp och ange dess titel.

På samma sätt kan du ange copyrightinformation och företagsinformation när du drar sidfotskomponenten i layoutbehållaren nedanför den adaptiva formulärbehållaren.

![Sidhuvud och sidfot har lagts till i strukturlagret](assets/header-and-footer.png)

Sidhuvud och sidfot som lagts till i strukturlagret

#### Låsa/låsa upp komponenter i strukturlagret {#locking-unlocking-components-in-the-structure-layer}

När du redigerar mallen med strukturlagret markerat kan du låsa upp mallens sidhuvud och sidfot. Om en komponent är olåst i mallen kan formulärförfattare redigera komponenten i det adaptiva formulär som använder mallen. Genom att låsa en komponent förhindrar du att formulärförfattare redigerar den i det adaptiva formuläret. Alternativet Lås är tillgängligt i komponentens verktygsfält.

Du kan till exempel lägga till rubrikkomponenten i mallen. När du markerar komponenten kan du se ett låsalternativ i komponentens verktygsfält. Vanligtvis innehåller rubriken företagsnamn och logotyp, och du vill inte att formulärförfattare ska ändra logotypen och rubriken i en mall. I ett adaptivt formulär som skapats med mallen med huvudkomponenten låst kan formulärförfattare inte ändra logotypen och företagsnamnet.

>[!NOTE]
>
>Du bör inte låsa eller låsa upp en bild eller logotyp separat i rubrikkomponenten. Du kan låsa upp rubrikkomponenten.

### Ursprungligt innehåll {#initial-content}

När alternativet Ursprungligt innehåll är markerat öppnas mallens adaptiva formulärbehållare som ett adaptivt formulär för redigering. Precis som när du skapar ett adaptivt formulär kan du ange inledande inställningar, som att välja ett tema och skicka åtgärder.

Formulärförfattare använder det som bas för att skapa ett formulär. Innehållsflödesstrukturen anges i lagret Ursprungligt innehåll i mallen. Om du vill växla till att redigera det ursprungliga innehållet i formulärmallen väljer du ![listrutan för arbetsyta](assets/canvas-drop-down.png) **>** **[!UICONTROL Initial Content]** innan du förhandsgranskar i sidverktygsfältet.


I lagret Ursprungligt innehåll skapar du mallen Adaptivt formulär som dina författare använder som bas. Om du redigerar en mall på samma sätt som när du redigerar ett formulär, använder du de alternativ som finns i sidofältet. Sidofältet innehåller webbläsare för innehåll, egenskaper, resurser och komponenter.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>När du väljer Lagra innehåll eller Lagra PDF som överföringsåtgärd får du ett alternativ för att ange lagringssökvägen. Om du anger en sökväg i en mall får alla formulär som skapas från den samma sökväg. Du kan ange rätt lagringssökväg eller se till att formulärförfattare uppdaterar den för att förhindra att data från alla formulär lagras på samma plats.

#### Skapa en anpassad formulärmall med flikar och paneler {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Du kan till exempel skapa en mall med följande flikar:

* Allmän information
* Professional Information

Du har lagt till en logotyp, angett en rubrik och lagt till en sidfot i strukturlagret. Lås sidhuvudet och sidfoten för att hindra formulärförfattare från att redigera dem när de använder mallen för att skapa formulär.

Ändra lagret från Struktur till Inledande innehåll och börja lägga till innehåll i formuläret. Om du vill skapa en flikstruktur lägger du till en underordnad panel i guideRootPanel i behållaren för adaptivt format. Så här lägger du till en panel:

* Du kan lägga till en panel genom att trycka på knappen **[!UICONTROL +]** när du väljer alternativet **[!UICONTROL Drag components here]**.

* Du kan dra och släppa panelkomponenten från komponentwebbläsaren i sidofältet.
* Du kan lägga till en underordnad panel för `guideRootPanel` från komponentens verktygsfält.

Om du vill skapa flikarna Allmän information och Professional Information lägger du till två paneler i den underordnade panelen för `guideRootPanel`. Markera panelerna och välj ![cmpr](assets/configure-icon.svg) för att öppna egenskaperna i sidofältet. Ändra elementnamnen som `general-info` och `professional-info`, och titlarna som Allmän information respektive Professional Information. I sidlisten väljer du innehåll för att öppna innehållsläsaren. Välj `guideRootPanel` på fliken Formulärobjekt. I redigeraren markeras guideRootPanel. Välj ![cmpr](assets/configure-icon.svg) i komponentens verktygsfält för att öppna dess egenskaper. Markera **[!UICONTROL Tabs on Top]** och välj **[!UICONTROL Done]** i fältet Panellayout. Flikmallstrukturen används.

#### Lägga till innehåll på flikar {#adding-content-in-tabs}

När du har lagt till paneler och strukturerat dem som flikar kan du lägga till fält inuti flikarna. När du väljer en flik i redigeraren kan du se alternativet **[!UICONTROL Drag components here]**. Du kan dra och släppa komponenter som textrutor, listobjekt och knappar. Du kan dra och släppa komponenter från komponentwebbläsaren i sidofältet.

Varje komponent har egenskaper som förbättrar datainhämtning och -hantering. Du kan till exempel aktivera egenskapen **[!UICONTROL Required field]** för en komponent. Författarna kan ange ett meddelande som kunderna ser när de inte fyller i ett obligatoriskt fält. Ange meddelandet i egenskapen **[!UICONTROL Required Field Message]**.

I exempelmallen läggs fälten Namn, Telefonnummer och Födelsedatum till på fliken Allmän information. På fliken Professional Information, Anställda, typ av anställning, läggs fält för utbildningsbehörighet till.

När du har lagt till fält kan du lägga till knappar som Skicka och Återställ.

### Aktivera mallen {#enabling-the-template}

När du skapar en mall läggs den till som ett utkast. Aktivera mallen för att använda den för att skapa Adaptiv Forms. Så här aktiverar du en mall:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Templates]** och öppna mappen där du har skapat mallen.

1. Mallen som du har skapat markeras som Utkast.
1. Markera mallen och välj **[!UICONTROL Enable]** i verktygsfältet.
När du skapar ett adaptivt formulär kan du se mallen som visas när du ombeds att välja en mall.

## Importera eller exportera en mall {#importing-or-exporting-a-template}

Ett formulär fungerar med sin mall. När du hämtar ett adaptivt formulär som skapats med en anpassad mall hämtas inte mallen. När du importerar formuläret till en annan [!DNL AEM Forms]-instans importeras det utan någon mall. Om ett formulär importeras men mallen inte är tillgänglig, återges inte formuläret. Du kan paketera den anpassade mallen från noden `/conf` i `https://<server>:<port>/crx/packmgr` och portera den i instansen [!DNL AEM Forms] där du vill överföra formuläret. Du kan också [skapa en mall med AEM Archeype och distribuera den till din molntjänstinstans](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html?lang=sv-SE#prerequisites).

>[!NOTE]
>
> * Du kan också konfigurera mallen [!UICONTROL Document of Record] direkt från modulen Adaptiv formulärbyggaren eller mallbyggaren för adaptiv form. Mer information finns i [Skapa postdokument för adaptiv Forms](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).


## Koppla ett formulärdatamodellschema till en mall {#associating-form-data-model-schema-in-template}

Författare kan associera en [!UICONTROL Form Data Model Schema] till en anpassad formulärmall i mallredigeraren. Det gör att författare kan välja ett schema i mallredigeraren. När du kopplar ett schema till en mall och en formulärförfattare skapar ett formulär baserat på mallen, markeras schemat automatiskt för formuläret. Det hjälper formulärförfattare att reglera användningen av scheman och sparar tid även för formulärförfattare. Så här väljer du ett formulärdatamodellschema i mallredigeraren:

1. Välj **[!UICONTROL Content Browser]** som finns till vänster.
1. Gå till formulärbehållaren **[!UICONTROL Setting]**.
1. Välj **[!UICONTROL Data Model]**.
1. Välj formulärdatamodellen via **[!UICONTROL Select Form Data Model]** och spara konfigurationen.

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img.png)



## Skapa ett anpassat formulär med hjälp av mallen {#creating-an-adaptive-form-using-the-template}

När du har skapat och aktiverat en mall är den tillgänglig i formulärhanteraren när du skapar ett anpassat formulär. Mer information om hur du använder en mall och skapar ett adaptivt formulär finns i [Skapa ett adaptivt formulär](creating-adaptive-form.md).


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

1. Click **Save**. The display options for the out of the box templates are changed. -->

## Spara ett anpassat formulär som en mall {#saving-adaptive-form-as-template}

Du kan också spara ett anpassat formulär som en mall för framtida bruk. Så här sparar du ett anpassat formulär som en mall:

1. Välj ett anpassat formulär för att spara det som en mall.
1. Klicka på **[!UICONTROL Save as Template]**. En dialogruta visas.
1. Ange **[!UICONTROL Title]** (obligatoriskt fält), **[!UICONTROL Location]** (obligatoriskt fält) och **[!UICONTROL Description]** (valfritt fält) för mallen.
1. Klicka på **[!UICONTROL Create]**.

   ![Spara som formulär som mall](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>Om du vill använda samma behållarprofil som för det adaptiva källformuläret bör du spara mallen i samma mapp som det adaptiva källformuläret. Om mallen sparas i en annan mapp används en standardbehållarprofil för den skapade mallen.

## Rekommendationer {#recommendations}

* När du ändrar egenskaper för formuläret i mallredigeraren ska du inte använda egenskapen BindReference.
* Om du vill lägga till en brytpunkt skapar du den när du skapar en anpassad formulärmall.
Mer information om brytpunkter finns i [Responsiv layout](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html?lang=sv-SE#authoring).


## Se även {#see-also}

{{see-also}}
