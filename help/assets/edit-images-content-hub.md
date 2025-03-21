---
title: Redigera bilder i Content Hub med Adobe Express
description: Redigera bilder i Content Hub med Adobe Express
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Redigera bilder i Content Hub {#edit-images-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

![Redigera bilder i Content Hub med Adobe Express](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Med Content Hub kan du skapa nytt innehåll med Adobe Express. Du kan redigera befintligt innehåll med lättanvända verktyg, producera varumärkesanpassade varianter med mallar och märkeselement och skapa nytt innehåll med de senaste GenAI-funktionerna från Adobe Firefly.

## Förutsättningar {#prereqs-edit-image-content-hub}

Tillstånd att få åtkomst till Adobe Express- och [Content Hub-användare med rätt att mixa om resurser till nya varianter](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets) kan redigera bilder med Content Hub.

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

   Adobe rekommenderar att du anger värden i resten av fälten och skapar en förbättrad sökupplevelse för dina överförda resurser.

1. [Valfritt] Definiera värden för fälten **[!UICONTROL Keywords]**, **[!UICONTROL Channels]**, **[!UICONTROL Timeframe]** och **[!UICONTROL Region]**. Genom att tagga och gruppera resurser efter nyckelord, kanaler och plats kan alla som använder ditt godkända företagsinnehåll hitta och ordna mediefilerna.

1. Klicka på **[!UICONTROL Save as new asset]** för att spara resursen.

Administratörer kan också konfigurera obligatoriska och valfria fält som visas när resurser läggs till i Content Hub, till exempel kampanjnamn, nyckelord, kanaler osv. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-upload-options-content-hub).
