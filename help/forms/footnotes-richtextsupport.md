---
title: Hur lägger man till fotnot i ett anpassat formulär?
description: Använd RTF-redigerare (Rich Text Editor) för fotnoter i en adaptiv form.
feature: Adaptive Forms, Foundation Components
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
role: User, Developer
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Fotnotskomponent {#footnotecomponent}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

**[!UICONTROL Footnote]** är den extra biten med information eller anteckningar som visas i slutet av sidan. [!UICONTROL Footnote] innehåller anteckningarna som anges i texten med siffror som upphöjda.

Fotnoterna numreras sekventiellt i den ordning som de visas på sidan. Varje fotnot har ett unikt nummer som upphöjd text, vilket motsvarar numret som placeras längst ned på sidan. Bredvid numret visas den kompletterande informationen som en fotnotsbeskrivning.

![Fotnotsbeskrivning](/help/forms/assets/footnote_description.png)


## Användning av fotnoten {#usesoffootnotes}

* Hjälper till att tillhandahålla citat.
* Ger extra information som kan avbryta det normala flödet av huvudinformationen.
* Tillhandahåller parentetisk information eller copyrightbehörigheter.

I Adaptiv Forms används [!UICONTROL footnote] för att visa information om hur du fyller i eller använder formuläret. Mer information om hur du skapar ett adaptivt Forms finns i [Skapa ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Fotnot i Adaptiv Forms {#using-footnote-adaptiveforms}

Så här lägger du till en fotnot i Adaptiv Forms:
1. Öppna ett anpassat formulär i läget **Redigera**.
1. Dra komponenten **[!UICONTROL Text]** från komponentwebbläsaren till det adaptiva formuläret.
1. Markera **[!UICONTROL Text]**-komponenten som du har lagt till och välj ![cmpr](assets/configure-icon.svg) för att redigera dess egenskaper.

   ![Fotnot i anpassad Forms](/help/forms/assets/footnote_rte.png)

1. Markera den text som du vill lägga till en fotnotsbeskrivning för och klicka på knappen ![stjärna](/help/forms/assets/asterisk.svg) för att formatera komponenten **[!UICONTROL Footnote]**.

1. Klicka på ![check](/help/forms/assets/save_icon.svg) för att spara ändringarna och formaten.

   >[!NOTE]
   >
   >* Fotnoter numreras automatiskt och visas på ett sätt som de skapas i det anpassade formuläret.
   >* Om det finns duplicerade fotnoter är numreringen densamma för alla duplicerade fotnoter.

1. Dra komponenten **[!UICONTROL Footnote Placeholder]** från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   >
   >* I publiceringsinstansen visas fotnoter på den plats där komponenten **[!UICONTROL Footnote Placeholder]** placeras i det adaptiva formuläret.
   >* När du navigerar mellan olika paneler visas endast synliga fotnoter i **[!UICONTROL Footnote Placeholder]** som finns på den navigerade panelen.

1. Spara egenskaperna.

Vid körning visas siffran i texten som upphöjd och motsvarande beskrivning visas i komponenten **[!UICONTROL Footnote]** på den plats där [!UICONTROL Footnote Placeholder] placeras i det adaptiva formuläret. Du kan navigera direkt till fotnotsbeskrivningen genom att klicka på motsvarande nummer på [!UICONTROL Footnote].


## Se även {#see-also}

{{see-also}}