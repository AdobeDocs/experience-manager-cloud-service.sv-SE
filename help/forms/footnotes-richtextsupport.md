---
title: Stöd för fotnoter
description: RTE-stöd för fotnoter.
source-git-commit: 3d713304512065819ed16bbc9604f2cf9d1cf43f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Fotnotskomponent {#footnotecomponent}

**[!UICONTROL Footnote]** är den extra information eller anteckningar som visas i slutet av sidan. [!UICONTROL Footnote] innehåller de anteckningar som anges i texten med siffror som upphöjda.

Fotnoterna numreras sekventiellt i den ordning som de visas på sidan. Varje fotnot har ett unikt nummer som upphöjd text, vilket motsvarar numret som placeras längst ned på sidan. Bredvid numret visas den kompletterande informationen som en fotnotsbeskrivning.

![Fotnotsbeskrivning](/help/forms/assets/footnote_description.png)


## Användning av fotnot {#usesoffootnotes}

* Hjälper till att tillhandahålla citat.
* Ger extra information som kan avbryta det normala flödet av huvudinformationen.
* Tillhandahåller parentetisk information eller copyrightbehörigheter.

I Adaptive Forms [!UICONTROL footnote] används för att visa information om hur du fyller i eller använder formuläret. Mer information om hur du skapar en adaptiv Forms finns i [Skapa ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Fotnot i Adaptiv Forms {#using-footnote-adaptiveforms}

Så här lägger du till en fotnot i Adaptiv Forms:
1. Öppna ett anpassat formulär i **Redigera** läge.
1. Dra från komponentwebbläsaren och släpp **[!UICONTROL Text]** på adaptiva formulär.
1. Välj **[!UICONTROL Text]** som du lade till och trycker på ![cmppr](assets/configure-icon.svg) om du vill redigera dess egenskaper.

   ![Fotnot i Adaptiv Forms](/help/forms/assets/footnote_rte.png)

1. Markera den text som du vill lägga till en fotnotsbeskrivning för och klicka på  ![stjärna](/help/forms/assets/asterisk.svg) för att formatera **[!UICONTROL Footnote]** -komponenten.

1. Klicka ![check](/help/forms/assets/save_icon.svg) om du vill spara ändringarna och formaten.

   >[!NOTE]
   >
   >* Fotnoter numreras automatiskt och visas på ett sätt som de skapas i det anpassade formuläret.
   >* Om det finns duplicerade fotnoter är numreringen densamma för alla duplicerade fotnoter.


1. Dra från komponentwebbläsaren och släpp **[!UICONTROL Footnote Placeholder]** på adaptiva formulär.
   >[!NOTE]
   >
   >* I publiceringsinstansen visas fotnoterna på den plats där **[!UICONTROL Footnote Placeholder]** placeras på den adaptiva formen.
   >* När du navigerar mellan olika paneler visas endast synliga fotnoter i **[!UICONTROL Footnote Placeholder]** som finns på den navigerade panelen.


1. Spara egenskaperna.

Vid körning visas siffran i texten som upphöjd och motsvarande beskrivning visas i **[!UICONTROL Footnote]** komponenten vid den position där [!UICONTROL Footnote Placeholder] placeras på det adaptiva formuläret. Du kan navigera direkt till fotnotsbeskrivningen genom att klicka på motsvarande nummer på [!UICONTROL Footnote].