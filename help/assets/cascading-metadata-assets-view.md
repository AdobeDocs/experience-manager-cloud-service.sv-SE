---
title: Överlappande metadata
description: I den här artikeln beskrivs hur du definierar överlappande metadata för resurser i resursvyn.
feature: Metadata
role: Admin, User
source-git-commit: 2bb309afc372fe18ce274a2813ed25cba22eb4de
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---


# Cascading Metadata Assets View{#cascading-metadata-assets-view}

När användare hämtar metadatainformation för en resurs anger de information som finns i de olika tillgängliga fälten. Du kan visa specifika metadatafält eller fältvärden som är beroende av vilka alternativ som är markerade i de andra fälten. En sådan villkorlig visning av metadata kallas överlappande metadata. Du kan med andra ord skapa ett beroende mellan ett visst metadatafält/värde och ett eller flera fält och/eller deras värden.

Använd Forms-metadata för att definiera regler för visning av överlappande metadata. Om ditt metadataformulär t.ex. innehåller ett tillgångstypfält kan du definiera en relevant uppsättning fält som ska visas baserat på vilken typ av resurs som användaren väljer.

Här följer några exempel där du kan definiera överlappande metadata:

* Där användarplats krävs, visa relevanta stadsnamn baserat på användarens val av land och delstat.
* Läs in relevanta varumärkesnamn i en lista baserat på användarens val av produktkategori.
* Växla synlighet för ett visst fält baserat på värdet som anges i ett annat fält. Visa t.ex. separata leveransadressfält om användaren vill att leveransen ska ske till en annan adress.
* Ange ett fält som obligatoriskt baserat på det värde som anges i ett annat fält.
* Ändra alternativen som visas för ett visst fält baserat på värdet som anges i ett annat fält.
* Ange standardvärdet för metadata i ett visst fält baserat på det värde som anges i ett annat fält.

>[!IMPORTANT]
>
>Funktionen Cascading Metadata finns som begränsad tillgänglighet. Du kan [skapa och skicka ett Adobe kundsupportärende](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) för att aktivera det för din distribution.

## Konfigurera metadata i [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Tänk dig ett scenario där du vill visa överlappande metadata baserat på den typ av resurs som är markerad. Till exempel-

* För en video visar du tillämpliga fält som format, kodek, längd och så vidare.
* För Word- eller PDF-dokument visas fält, t.ex. sidantal, författare osv.

Vi använder ett listrutefält med namnet `Image` som exempel för att kategorisera filer baserat på deras bildtyp. Listrutan innehåller alternativ som representerar bildtillägg som stöds (t.ex. JPG/JPEG, GIF). För att säkerställa att data är konsekventa och förhindra att format som inte stöds väljs eller bearbetas, tillämpas en valideringsregel på det här fältet. Regeln utvärderar det valda rullgardinsvärdet och tillämpar begränsningar som är anpassade till de godkända bildformaten.

>[!IMPORTANT]
>
>Du kan bara skapa regler baserat på listrutefält.

Oavsett vilken resurstyp du väljer visas copyrightinformationen som ett obligatoriskt fält. Du kan använda de [fördefinierade metadatakomponenterna](metadata-assets-view.md#property-components) och [tilldela metadata till en mapp](metadata-assets-view.md#assign-metadata-form-folder).

### Skapa metadata-Forms {#build-metadata-schema-forms}

Följ stegen nedan för att skapa ett nytt metadataformulär:

1. Välj logotypen [!DNL Experience Manager] och gå till **[!UICONTROL Settings]** > **[!UICONTROL Metadata Forms]** > **[!UICONTROL Create]**.

1. Välj lämplig formulärtyp i listrutan **[!UICONTROL Type]**: **[!UICONTROL File]**, **[!UICONTROL Folder]** eller **[!UICONTROL Collection]**.

1. Ange metadataformulärets rubrik i fältet **[!UICONTROL Name]**.

1. Du kan också välja en befintlig metadatamall i listrutan **[!UICONTROL Choose from existing form template]**.

1. Ett tomt metadataformulär visas. Lägg till en ny flik.

   ![Användargränssnitt för metadataformulär](assets/metadata-form-ui.png)

   * **A:** Växla mellan [!UICONTROL Edit] eller [!UICONTROL Preview]
   * **B:** [Komponenter i metadataformulär](metadata-assets-view.md#property-components)
   * **C:** Växla till annat metadataformulär
   * **D:** Lägg till en ny flik
   * **E:** Arbetsyta
   * **F:** Allmänna inställningar för den valda komponenten
   * **G:** Fliken Regler
   * **H:** Komponentegenskaper

I den här videon visas stegsekvensen [Konfigurera metadata Forms](https://video.tv.adobe.com/v/341275).

### Ändra ett befintligt metadataformulär {#modify-existing-metadata-form}

Om du vill ändra ett befintligt metadataformulär följer du stegen nedan:

1. Öppna ett befintligt metadataformulär och gå till de [fördefinierade komponenterna](metadata-assets-view.md#property-components) som du vill lägga till i formuläret och släpp elementen på arbetsytan.

   Lägg till ett listrutefält för att definiera bildresurstyper i enlighet med **bilden**. Ange namn och egenskapssökväg i **Inställningar** och konfigurera fältet som **[!UICONTROL Read-Only]** eller **[!UICONTROL Multiple Selections]** om du vill.

1. Ange nyckelvärdesalternativen för listrutan antingen genom att ange dem manuellt, ange en JSON-sökväg eller genom att importera en CSV-fil.

   * Om du vill ange värdena manuellt väljer du **[!UICONTROL Add Manually]** under **[!UICONTROL Choices]**, klickar på `Add` och anger alternativetiketten och värdet. Ange till exempel resurstyperna Video, PDF och Bild.

     ![Bildresurstyp](assets/image-asset-type.png)

   * Om du vill hämta värden från en JSON-sökväg väljer du **[!UICONTROL Add through JSON Path]** och anger sökvägen till JSON-filen.

     >[!NOTE]
     >
     >Se till att JSON-filen lagras på en delad plats som är tillgänglig för alla DAM-redigerare och författare.

     ![Lägg till alternativ via JSON-sökväg](assets/add-json-choices.png)

   * Om du vill hämta värden dynamiskt från en CSV-fil klickar du på **[!UICONTROL Import CSV]** och anger sökvägen till CSV-filen. [!DNL Experience Manager] hämtar nyckelvärdepar i realtid när formuläret presenteras för användaren.

     ![Lägg till alternativ via CSV](assets/import-csv-choices.png)

   >[!NOTE]
   > 
   >Du kan inte importera alternativen från en CSV-fil och redigera dem manuellt eftersom båda alternativen utesluter varandra.

1. Om du vill skapa ett beroende mellan bildfältet och andra fält markerar du det beroende fältet och öppnar fliken **[!UICONTROL Rules]**. Varje komponent har stöd för en viss uppsättning regler. I det här fallet används alternativen för Image Asset Type för att definiera regellogiken.

   <!--![Image Asset Type Rule](assets/image-asset-type-rule.png)-->

   <!--![rule tab](assets/rule-tab.png)-->

1. Välj alternativet **[!UICONTROL Required]** under **[!UICONTROL Required based on new rule]**. Klicka på ![plustecknet](assets/do-not-localize/aem_assets_add_icon.png) för att lägga till en ny regel.

   ![regel](assets/image-required-rule1.png)

   I det aktuella fallet är fältet Resurstyp obligatoriskt när bildresursen har formatet JPG/JPEG, PNG, GIF, TIFF eller WEBP. Klicka på ![redigeringsikonen](assets/do-not-localize/edit.svg) om du vill definiera om regeln eller klicka på ![borttagningsikonen](assets/do-not-localize/delete.svg) om du vill ta bort den definierade regeln.

   ![regel](assets/image-required-rule2.png)

1. Välj alternativet **[!UICONTROL Visibility]** under **[!UICONTROL Visible, based on new rule]**. Klicka på ![plustecknet](assets/do-not-localize/aem_assets_add_icon.png) för att lägga till en ny regel.

   >[!NOTE]
   >
   >Du kan använda villkoret **[!UICONTROL Requirement]** och villkoret **[!UICONTROL Visibility]** oberoende av varandra.

   ![regel](assets/image-visible-rule1.png)

   I det aktuella användningsfallet är fältet Resurstyp synligt när bildresursformatet är JPG/JPEG, PNG eller GIF. Klicka på ![redigeringsikonen](assets/do-not-localize/edit.svg) om du vill definiera om regeln eller klicka på ![borttagningsikonen](assets/do-not-localize/delete.svg) om du vill ta bort den definierade regeln.

   ![regel](assets/image-visible-rule2.png)

1. Välj **[!UICONTROL Choices based on rule]** om du vill skapa ett beroende och definiera regel. Klicka på ![plustecknet](assets/do-not-localize/aem_assets_add_icon.png) för att lägga till en ny regel.

   ![regel](assets/image-choices-rule1.png)

   Om du vill konfigurera regelbaserade alternativ för listrutan Resurstyp skapar du en regel och anger Bild som det beroende fältet. Definiera sedan visningsvärdena för varje bildformat genom att välja Bild för JPG/JPEG, PNG, GIF och TIFF, och välja Video för WEBP. På så sätt säkerställs att endast de avsedda värdena kontrolleras för varje format dynamiskt för att visa relevanta alternativ. Klicka på ![redigeringsikonen](assets/do-not-localize/edit.svg) om du vill definiera om regeln eller klicka på ![borttagningsikonen](assets/do-not-localize/delete.svg) om du vill ta bort den definierade regeln.

   ![regel](assets/image-choices-rule2.png)

1. Upprepa på samma sätt stegen för att skapa beroende mellan andra resurser som PDF och Word i fältet [!UICONTROL Asset Type] och fält som [!UICONTROL Page Count] och [!UICONTROL Author].

1. Klicka på **[!UICONTROL Save]**. Använd metadataformuläret på en mapp.

1. Navigera till mappen som du tillämpade metadataformuläret på och öppna egenskapssidan för en resurs. Beroende på vad du väljer i fältet Resurstyp visas relevanta överlappande metadatafält.

   ![Överlappande metadataformulärutdata](assets/cascading-metadata-form-output.png)

>[!NOTE]
> 
>[Skapa och skicka ett Adobe kundsupportärende](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) om du vill få tidig åtkomst till Cascading Metadata på ditt Assets View-konto.

## Nästa steg {#next-steps}

* [Titta på en video om hur du hanterar metadataformulär i Assets-vyn](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=sv-SE)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/sv?support-solution=General#support)

