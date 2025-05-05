---
title: Hur delar jag länkar till resurser?
description: Generera en länk och dela resurser med andra som inte har tillgång till programmet  [!DNL Assets view] .
exl-id: 7d7d488b-410b-4e90-bd10-4ffbb5fcec49
feature: Adobe Asset Link, Link Sharing
role: Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Dela länkar till resurser {#share-links-assets}

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

Med [!DNL Assets view] kan du skapa en länk och dela resurser med externa intressenter som inte har tillgång till programmet [!DNL Assets view]. Du kan definiera ett förfallodatum för länken och sedan dela det med andra via den kommunikationsmetod du föredrar, som e-post eller meddelandetjänster. Mottagarna av länken kan förhandsgranska resurser och hämta dem.

## Generera en länk för resurser {#generate-link-for-assets}

Så här skapar du en länk för en resurs eller en mapp som innehåller resurser:

1. Markera de resurser, eller mappar, eller båda, som innehåller resurser och klicka på **[!UICONTROL Share Link]**.

1. Om du vill justera den klickar du på kalenderikonen för att definiera ett förfallodatum för länken med hjälp av fältet **[!UICONTROL Expiration Date]**. Du kan också ange ett datum direkt i formatet `yyyy-mm-dd`. Som standard är förfallodatumet för en länk inställt på två veckor från delningsdatumet.

1. Kopiera länken från fältet **[!UICONTROL Share Link]**.

   ![Alternativ för att beskära och räta upp](assets/share-asset-link.png)

1. Klicka på **[!UICONTROL Close]** och dela länken med hjälp av e-post eller andra samarbetsverktyg.

## Åtkomst till delade resurser {#access-shared-assets}

När mottagarna har delat den offentliga länken för resurserna kan de klicka på länken för att förhandsgranska eller hämta de delade resurserna i en webbläsare utan att behöva logga in på [!DNL Assets view].

Klicka på länken, klicka på mappen för att navigera till resursen och klicka sedan på resursen för att förhandsgranska den. Du kan välja att visa de delade resurserna i en listvy eller en kortvy.

Du kan hålla muspekaren över den delade resursen eller den delade resursmappen för att antingen välja resursen eller hämta den.

Du kan också markera flera resurser och klicka på **[!UICONTROL Download]**. [!DNL Assets view] hämtar de valda resurserna som en zip-fil. [!DNL Assets view] skapar en undermapp i den överordnade ZIP-filen, med samma namn som resursen, för varje resurs som du väljer att hämta.

Om du vill hämta alla resurser samtidigt växlar du till **[!UICONTROL List view]**, klickar på **[!UICONTROL Select all]** och sedan på **[!UICONTROL Download]**.

![Förhandsgranska delade resurser](assets/preview-shared-assets.png)

## Nästa steg {#next-steps}

* [Titta på en video om du vill dela länkar för resurser i Assets-vyn](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/link-sharing.html?lang=sv-SE)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/sv?support-solution=General#support)
