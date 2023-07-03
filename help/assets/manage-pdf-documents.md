---
title: Hantera dina PDF-dokument i [!DNL Adobe Experience Manager].
description: Hantera PDF-dokument i [!DNL Adobe Experience Manager] som [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 589ed1e1befa84c0caec0eed986c3e1a717ae602
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 1%

---

# Hantera PDF-dokument i Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets integreras smidigt med visningsprogrammet för Document Cloud PDF, som gör att du kan förhandsgranska flera sidor i ett PDF-dokument. Dessutom kan du använda avancerade visningsfunktioner för Document Cloud PDF, som anteckningar, söktext, navigera i PDF-dokumentet med bokmärken och miniatyrbilder med mera under samma tak. Med Experience Manager Assets kan du även överföra dokument i andra format som stöds och förhandsgranska dem i PDF-format.

Document Cloud PDF viewer ger AEM Assets fördelar på följande sätt:
* [Stöd för visningsprogramkomponenter för PDF Document Cloud](#pdf-doc-cloud)
* [Stöd för förhandsvisning av flera sidor och anteckningar för PDF-resurser](#multi-page)
* [Stöd för förhandsgranskning av flera sidor för dokument i andra format](#multi-format)

> Tips
> Om du inte kan hämta förhandsgranskning av flera sidor för ett tidigare överfört PDF-dokument markerar du PDF och klickar på **![Återbearbeta](/help/assets/assets/Reprocess.svg) Bearbeta resurser igen**.
>

## Stöd för visningsprogramkomponenter för PDF Document Cloud {#pdf-doc-cloud}

Det inbyggda visningsprogrammet för PDF Doc Cloud har följande komponenter i AEM Assets:

* **PDF-visningsprogram med sidminiatyrer** Miniatyrbildsvyn är en liten förhandsvisning av sidorna i ett PDF-dokument. Med hjälp av miniatyrbilder kan du gå direkt till önskad sida. Du kommer åt miniatyrbilder av det markerade PDF-dokumentet via ![miniatyrbild](/help/assets/assets/thumbnail.svg) till vänster.

* **PDF viewer med bokmärken** Bokmärke är en direktlänk som leder dig till innehållet i dokumentet. Du kan öppna bokmärken i det markerade PDF-dokumentet via ![bokmärke](/help/assets/assets/bookmark.svg) till vänster.

* **Sök i PDF** Du kan använda sökning ![sök](/help/assets/assets/Search.svg) om du vill söka efter texten i PDF-dokumentet.

* **Page Up/Page Down** Använd Page Up ![Page Up](/help/assets/assets/ArrowUp.svg) eller Page Down ![Page Down](/help/assets/assets/ArrowDown.svg) för att bläddra igenom dokumentet.

* **Zooma ut/zooma in** Använd utzoomning ![Zooma ut](/help/assets/assets/ZoomOut.svg) eller Zooma in ![Zooma in](/help/assets/assets/ZoomIn.svg) för att flöda dokumentet.

* **Sidanpassning** Använd bredd- eller höjddimensionerna för att anpassa dokumentet efter skärmstorleken.

* **Docka/avdocka PDF** Du kan docka eller avdocka komponenterna i det inbyggda PDF-visningsprogrammet med det här alternativet.

## Stöd för förhandsvisning av flera sidor och anteckningar för PDF-resurser {#multi-page}

Med Adobe Experience Manager Assets kan du förhandsgranska PDF-dokument som består av flera sidor. Om du vill förhandsgranska flera sidor i ett PDF-dokument följer du de här stegen:

1. Följ stegen för att [överföra resurser i AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Bläddra i det PDF-dokument som du vill överföra och förhandsgranska.
1. Öppna dokumentet.
1. Dokumentvisningsprogrammet i PDF läses in som standard. Du kan också välja PDF återgivning på återgivningspanelen.
1. Under listrutan Återgivningar väljer du **Alla återgivningar**.

Du kan också använda [anteckningar](#pdf-annotations) till PDF-dokumentet i en förhandsvisning av flera sidor.

> ANMÄRKNING
> Den maximala storleken för en resurs som du kan förhandsgranska är upp till 100 MB.
>

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF Anteckningar{#pdf-annotations}**

Med Experience Manager Assets kan du lägga till kommentarer i ett PDF-dokument. Ett PDF-dokument kan ha flera anteckningar.

Gör så här om du vill lägga till kommentarer i ett PDF-dokument:
1. Gå till Assets-gränssnittet och navigera till det PDF-dokument som du vill kommentera. Det inbyggda visningsprogrammet för PDF öppnas till höger och förhandsvisar det markerade PDF-dokumentet.
1. Klicka **Anteckna** på den översta menyn.
Följande anteckningar kan användas på ett PDF-dokument:

<table>
        <tr>
             <th> Anteckning </th>
            <th> Beskrivning </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> Kommentar </td>
            <td> Markera Kommentar för att uttrycka en observation. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> Textruta </td>
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
            <td> <img src="/help/assets/assets/TextUnderline.svg"> Understrykning av text </td>
            <td> Markera texten som du vill stryka under. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> Genomstruken </td>
            <td> Markera texten som du vill stryka över. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> Rita </td>
            <td> Infoga en visuell konst på PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Radera ritning </td>
             <td> Ta bort eller ångra ritning. </td>
        </tr>
    </table>

>[!NOTE]
>
>Anteckningarna som du lägger till i PDF-dokumentet är tillgängliga i förhandsgranskningsläget. Anteckningarna visas dock inte när du hämtar eller skriver ut dokumentet PDF.

## Stöd för förhandsgranskning av flera sidor för dokument i andra format {#multi-format}

Förutom PDF-dokument kan du även förhandsgranska flera sidor för dokument i andra formattyper. De dokumentformat som stöds är TXT, RTF, DOC, DOCX, PPT, PPTX, XLS och XLSX. Experience Manager Assets konverterar automatiskt dessa dokumentformat till ett PDF-format och gör dem tillgängliga för förhandsgranskning.

![Flersidig förhandsgranskning av dokument i andra format](/help/assets/assets/multi-page-other-formats.png)

Utför följande steg för att förhandsgranska flera sidor i andra dokumentformat som stöds:
1. Följ stegen för att [överföra resurser i AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Bläddra i dokumentet som du vill överföra och förhandsgranska.
1. Öppna dokumentet.
1. Markera PDF under det statiska avsnittet på den vänstra panelen. Den högra panelen visar förhandsgranskningen av en resurs på flera sidor. Välj en miniatyrbild i den vänstra panelen för att välja den sida som du vill förhandsgranska.

> ANMÄRKNING
> * Den maximala storleken för en resurs som du kan förhandsgranska är upp till 100 MB.
> * Den maximala storleken på XLS- eller XLSX-filer som kan förhandsgranskas är 20 MB.
>

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
