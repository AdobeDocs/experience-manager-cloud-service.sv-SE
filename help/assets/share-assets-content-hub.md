---
title: Dela Assets i [!DNL the Content Hub]
description: Dela Assets i [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Dela resurser i Content Hub {#search-assets-as-a-link}

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

![Dela banderollbild för resurser](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Att dela resurser via en länk är ett bekvämt sätt att göra resurserna tillgängliga för [!DNL the Content Hub]-användare. Funktionen gör att behöriga användare kan komma åt och hämta de resurser som delas med dem. När du hämtar resurser från en delad länk använder [!DNL the Content Hub] en asynkron tjänst som ger snabbare och oavbruten hämtning.

## Förutsättningar {#prerequisites}

[Content Hub-användare](deploy-content-hub.md#onboard-content-hub-users) kan utföra åtgärder som nämns i den här artikeln.

## Dela en enda resurs {#share-a-single-asset}

Du kan dela en enskild resurs genom att utföra följande steg:

1. Markera en resurs och klicka på ikonen ![dela](assets/share.svg) för att dela en resurs.

   ![Dela en resurs](assets/sharing-single-asset.png)

1. Använd fältet **[!UICONTROL Expiration]** för att ange ett förfallodatum för länken. Välj ett av de tillgängliga alternativen, till exempel 24 timmar, 1 vecka, 30 dagar, 90 dagar, 1 år eller ange ett anpassat datum.

1. Klicka på **[!UICONTROL Copy share link]**. Sedan kan du dela den kopierade länken med mottagaren.

## Dela flera resurser {#share-multiple-assets}

Med [!DNL The Content Hub] kan du dela flera resurser via en delad länk. Utför följande steg:

1. Välj resurser som du vill dela med den auktoriserade mottagaren. Du kan välja flera resurser en i taget eller klicka på **[!UICONTROL Select All]** för att markera alla tillgängliga resurser samtidigt. Alternativet **[!UICONTROL Select All]** visas bara när du väljer minst en resurs.

1. Klicka på ikonen ![Dela](assets/share.svg) .

   ![Dela flera resurser](assets/sharing-multiple-assets.png)

1. I förhandsvisningsavsnittet kan du även ta bort resurser efter dina behov. Använd fältet **[!UICONTROL Expiration]** för att ange ett förfallodatum för länken. Välj ett av de tillgängliga alternativen, till exempel 24 timmar, 1 vecka, 30 dagar, 90 dagar, 1 år eller ange ett anpassat datum.

1. Klicka på **[!UICONTROL Copy share link]**. Sedan kan du dela den kopierade länken med mottagaren.

## Förhandsgranska och dela resurser {#preview-assets}

Du kan förhandsgranska om du vill se hur en digital resurs ser ut innan du delar den med en länkmottagare. Klicka på resursen som du vill förhandsgranska. [!DNL Content Hub] visar den [detaljerade vyn för resursen](asset-properties-content-hub.md).

Klicka på ikonen ![dela](assets/share.svg) om du vill dela en resurs. Använd fältet **[!UICONTROL Expiration]** för att ange ett förfallodatum för länken. Välj ett av de tillgängliga alternativen, till exempel 24 timmar, 1 vecka, 30 dagar, 90 dagar, 1 år eller ange ett anpassat datum. Klicka på **[!UICONTROL Copy share link]**. Sedan kan du dela den kopierade länken med mottagaren.

![Förhandsgranska resurser i Content Hub](assets/preview-assets-content-hub.png)

## Åtkomst till delade resurser {#access-shared-assets}

När länken för resurserna har delats kan de behöriga mottagarna klicka på länken för att förhandsgranska eller hämta de delade resurserna i en webbläsare.

Klicka på den delade länken och klicka på nedladdningsikonen som finns på resurskortet för att hämta en resurs.  Du kan också markera flera resurser och klicka på **[!UICONTROL Download]**. <!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub] hämtar varje resurs en i taget till det lokala filsystemet.

![Använd delade länkar](assets/content-hub-access-shared-links.png)
