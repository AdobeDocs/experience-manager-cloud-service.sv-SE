---
title: Hantera dina PDF-dokument i [!DNL Adobe Experience Manager].
description: Hantera PDF-dokument i [!DNL Adobe Experience Manager] som en [!DNL Cloud Service].
feature: Asset Management
role: User, Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---

# Hantera PDF-dokument i Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets integreras smidigt med Document Cloud PDF Viewer så att du kan förhandsgranska flera sidor i ett PDF-dokument. Dessutom kan du använda avancerade visningsfunktioner i Document Cloud PDF som anteckningar, söktext, navigera i PDF-dokumentet med bokmärken och miniatyrbilder med mera under samma tak. Med Experience Manager Assets kan du även överföra dokument i andra format som stöds och förhandsgranska dem i ett PDF-format.

Document Cloud PDF Viewer har följande fördelar:

* [Stöd för PDF Document Cloud Viewer Components](#pdf-doc-cloud)
* [Stöd för förhandsgranskning av och anteckningar på flera sidor för PDF-resurser](#multi-page)
* [Stöd för förhandsgranskning av flera sidor för dokument i andra format](#multi-format)

>[!TIP]
>
> Om du inte kan hämta förhandsgranskning av flera sidor för ett tidigare överfört PDF-dokument markerar du PDF och klickar på ![Bearbeta igen](/help/assets/assets/Reprocess.svg) **Bearbeta Assets igen**.

## Stöd för PDF Document Cloud Viewer Components {#pdf-doc-cloud}

Det inbyggda visningsprogrammet för PDF Doc Cloud har följande komponenter i AEM Assets:

* **PDF-visningsprogrammet som använder sidminiatyrer** Miniatyrbildsvyn är en liten förhandsvisning av sidorna i ett PDF-dokument. Med hjälp av miniatyrbilder kan du gå direkt till önskad sida. Du kommer åt miniatyrbilder av det markerade PDF-dokumentet via ![miniatyrbild](/help/assets/assets/thumbnail.svg) i den vänstra rutan.

* **PDF-visningsprogrammet som använder bokmärken** är en direktlänk som leder dig till innehållet i dokumentet. Du kan komma åt bokmärken för det markerade PDF-dokumentet via ![bokmärke](/help/assets/assets/bookmark.svg) i den vänstra rutan.

* **Sök i PDF** Du kan använda sökningen ![search](/help/assets/assets/Search.svg) för att söka efter texten i PDF-dokumentet.

* **Page Up/Page Down** Använd Page Up ![Page Up](/help/assets/assets/ArrowUp.svg) eller Page Down ![Page Down](/help/assets/assets/ArrowDown.svg) för att bläddra igenom dokumentet.

* **Zooma ut/zooma in** Använd Zooma ut ![Zooma ut](/help/assets/assets/Zoom-out.svg) eller Zooma in ![Zooma in](/help/assets/assets/zoom-in.svg) för att strömma dokumentet.

* **Sidanpassning** Använd bredd- och höjddimensioner för att passa dokumentet efter skärmstorleken.

* **Docka/avdocka PDF** Du kan docka eller avdocka komponenterna i det inbyggda visningsprogrammet för PDF med det här alternativet.

## Stöd för förhandsgranskning av och anteckningar på flera sidor för PDF-resurser {#multi-page}

Med Adobe Experience Manager Assets kan du förhandsgranska PDF-dokument som består av flera sidor. Så här förhandsgranskar du flera sidor i ett PDF-dokument:

1. Följ stegen för att [överföra resurser i AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=sv-SE).
1. Bläddra i det PDF-dokument som du vill ladda upp och förhandsgranska.
1. Öppna dokumentet.
1. PDF dokumentvisningsprogram läses in som standard. Du kan också välja PDF-återgivning på panelen Återgivning.
1. Välj **Alla återgivningar** i listrutan Återgivningar.

Du kan också använda [anteckningar](#pdf-annotations) i PDF-dokumentet i en förhandsvisning av flera sidor.

>[!NOTE]
>
> Den maximala storleken för en resurs som du kan förhandsgranska är upp till 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF-anteckningar{#pdf-annotations}**

Med Experience Manager Assets kan du lägga till kommentarer i ett PDF-dokument. Ett PDF-dokument kan innehålla flera anteckningar.

Gör så här om du vill kommentera i ett PDF-dokument:

1. Gå till Assets-gränssnittet och navigera till det PDF-dokument som du vill kommentera. Det inbyggda PDF-visningsprogrammet öppnas till höger och förhandsvisar det markerade PDF-dokumentet.
1. Klicka på **Anteckna** på den översta menyn.
Följande anteckningar kan användas på ett PDF-dokument:

<table>
        <tr>
             <th> Anteckning </th>
            <th> Beskrivning </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg">-kommentar </td>
            <td> Markera Kommentar för att uttrycka en observation. </td>
        </tr>
        <tr>
            <td> Textruta för <img src="/help/assets/assets/Text.svg"> </td>
            <td> Ange texten genom att markera Textruta. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Anteckningar </td>
            <td> Lägg till en liten text eller påminnelse som du kan lägga till i ett visst område på PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Markering av text </td>
            <td> Markera texten som ska markeras i olika färger. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> understrykning av text </td>
            <td> Markera texten som du vill stryka under. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> genomstruken </td>
            <td> Markera texten som du vill stryka över. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg">-teckning </td>
            <td> Lägg in visuell grafik i PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Radera ritning </td>
             <td> Ta bort eller ångra ritning. </td>
        </tr>
    </table>

>[!NOTE]
>
>Anteckningarna som du lägger till i PDF-dokumentet är tillgängliga i förhandsgranskningsläget. Anteckningarna visas dock inte när du hämtar eller skriver ut PDF-dokumentet.

## Stöd för förhandsgranskning av flera sidor för dokument i andra format {#multi-format}

Förutom PDF-dokumenten kan du även förhandsgranska flera sidor för dokument i andra format. De dokumentformat som stöds är TXT, RTF, DOC, DOCX, PPT, PPTX, XLS och XLSX. Experience Manager Assets konverterar automatiskt dessa dokumentformat till ett PDF-format och gör dem tillgängliga för förhandsgranskning.

![Flersidig förhandsgranskning av dokument i andra format](/help/assets/assets/multi-page-other-formats.png)

Utför följande steg för att förhandsgranska flera sidor i andra dokumentformat som stöds:

1. Följ stegen för att [överföra resurser i AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=sv-SE).
1. Bläddra i dokumentet som du vill överföra och förhandsgranska.
1. Öppna dokumentet.
1. Välj PDF under det statiska avsnittet på den vänstra panelen. Den högra panelen visar förhandsgranskningen av en resurs på flera sidor. Välj en miniatyrbild i den vänstra panelen för att välja den sida som du vill förhandsgranska.

>[!NOTE]
>
> * Den maximala storleken för en resurs som du kan förhandsgranska är upp till 100 MB.
> * Den maximala storleken på XLS- eller XLSX-filer som kan förhandsgranskas är 20 MB.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
