---
title: Redigera bilder i Content Hub med Adobe Express
description: Redigera bilder i Content Hub med Adobe Express
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Redigera bilder i Content Hub {#edit-images-content-hub}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Redigera bilder i Content Hub med Adobe Express](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Med Content Hub kan du skapa nytt innehåll med Adobe Express. Du kan redigera befintligt innehåll med lättanvända verktyg, producera varumärkesanpassade varianter med mallar och märkeselement och skapa nytt innehåll med de senaste GenAI-funktionerna från Adobe Firefly.

## Förutsättningar {#prereqs-edit-image-content-hub}

Tillstånd att få tillgång till Adobe Express och [Content Hub-användare med rätt att mixa om resurser till nya varianter](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets) kan redigera bilder med Content Hub.

>[!NOTE]
>
Du kan redigera bilder av filtyperna PNG och JPG/JPEG med [!DNL Adobe Express].

## Redigera bilder med [!DNL Adobe Express] {#edit-images-using-content-hub}

Så här redigerar du bilder med Content Hub:

1. Klicka på **[!DNL Open in Adobe Express]** på resurskortet för bilden som du vill redigera. Du kan också klicka på bilden för att öppna informationen och sedan klicka på logotypen [!DNL Adobe Express]. Den inbäddade redigeraren för Adobe Express läses sedan in utan att någonsin behöva lämna Content Hub.

   Du kan använda funktionen [!DNL Adobe Express] för att utföra alla bildredigeringsrelaterade åtgärder, till exempel [ändra storlek på bild](https://helpx.adobe.com/express/using/resize-image.html), [ta bort eller ändra bakgrundsfärg](https://helpx.adobe.com/express/using/remove-background.html), [beskära bild](https://helpx.adobe.com/express/using/crop-image.html), kombinera bilden med AI-genererad bild eller text och mycket annat.

1. Utför ändringarna och klicka på **[!UICONTROL Save]** för att spara den redigerade resursen i någon av formattyperna:

   * **[!UICONTROL PNG]** (används som bildformat med bra kvalitet)
   * **[!UICONTROL JPG]** (som passar för små filer)
   * **[!UICONTROL PDF]** (som passar för dokument)

   ![Spara bild med Adobe Express](assets/adobe-express-save-as.png)

1. Ange ett namn för resursen i fältet **[!UICONTROL Save as]**.

1. Ange kampanjnamnet för resursen med fältet **[!UICONTROL Campaign name]**. Du kan använda ett befintligt namn eller skapa ett nytt. I Content Hub finns fler alternativ när du skriver namnet. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Som en god praxis rekommenderar Adobe att du anger värden i resten av fälten, liksom att du får en förbättrad sökupplevelse för dina överförda resurser.

1. [Valfritt] Definiera värden för fälten **[!UICONTROL Keywords]**, **[!UICONTROL Channels]**, **[!UICONTROL Timeframe]** och **[!UICONTROL Region]**. Genom att tagga och gruppera resurser efter nyckelord, kanaler och plats kan alla som använder ditt godkända företagsinnehåll hitta och ordna mediefilerna.

1. Klicka på **[!UICONTROL Save as new asset]** för att spara resursen.

Administratörer kan också konfigurera obligatoriska och valfria fält som visas när resurser läggs till i Content Hub, till exempel kampanjnamn, nyckelord, kanaler osv. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-upload-options-content-hub).
