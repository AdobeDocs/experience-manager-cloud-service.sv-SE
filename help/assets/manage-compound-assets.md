---
title: Hantera sammansatta resurser
description: Lär dig hur du skapar referenser till AEM-resurser från Adobe InDesign-, Adobe Illustrator- och Adobe Photoshop-filer. Lär dig även hur du använder funktionen för sidvisning för att visa enskilda sidor med flersidiga filer, inklusive PDF-, INDD-, PPT-, PPTX- och AI-filer.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Hantera sammansatta resurser {#managing-compound-assets}

Adobe Experience Manager Assets (AEM) Assets kan identifiera om en överförd fil innehåller referenser till resurser som redan finns i databasen. Den här funktionen är endast tillgänglig för filformat som stöds. Om den överförda resursen innehåller referenser till AEM-resurser skapas en dubbelriktad länk mellan de överförda och refererade resurserna.

Förutom att eliminera redundans förbättrar referensen till AEM-resurser i Adobe Creative Cloud-program samarbetet och ökar användarnas effektivitet och produktivitet.

AEM Resurser stöder **dubbelriktade referenser**. Du kan hitta refererade resurser på sidan med tillgångsinformation i den överförda filen. Dessutom kan du visa de refererande filerna för AEM-resurser på sidan med resursinformation för den refererade resursen.

Referenser tolkas utifrån sökväg, dokument-ID och instans-ID för de refererade resurserna.

## Lägga till AEM-resurser som referenser i Adobe Illustrator {#refai}

Du kan referera till befintliga AEM-resurser inifrån en Adobe Illustrator-fil.

Om du vill lägga till digitala resurser använder du antingen [AEM-datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) eller [överför med AEM](/help/assets/manage-digital-assets.md#uploading-assets) -användargränssnittet.

När arbetsflödet är klart går du till sidan med resursinformation för resursen. Referenser till befintliga AEM-resurser visas under **Beroenden** i kolumnen **Referenser** . De refererade resurserna som visas under **Beroenden** kan också refereras av andra filer än den aktuella.

Om du vill visa en lista med referensfiler för en resurs klickar du på resursen under **Beroenden**. Klicka på ikonen **Visa egenskaper** i verktygsfältet. På egenskapssidan visas listan med filer som refererar till den aktuella resursen under kolumnen **Referenser** på fliken **Grundläggande** .

## Lägga till AEM-resurser som referenser i Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

Om du vill referera till AEM-resurser från en InDesign-fil drar du AEM-resurserna till InDesign-filen eller exporterar InDesign-filen som en ZIP-fil.

Refererade resurser finns redan i AEM Resurser. Du kan extrahera delresurser genom att konfigurera Adobe InDesign-servern. Inbäddade resurser i en InDesign-fil extraheras som delresurser.

>[!NOTE]
>
>Om InDesign-servern är proxibel bäddas förhandsvisningen in i InDesign-filernas XMP-metadata. I det här fallet krävs inte extrahering av miniatyrer uttryckligen. Om InDesign-servern inte är proxyserver måste dock miniatyrer extraheras explicit för InDesign-filer.

### Skapa referenser genom att dra AEM-resurser {#create-references-by-dragging-aem-assets}

Proceduren liknar den som används för att [lägga till AEM-resurser som referenser i Adobe Illustrator](#refai).

### Skapa referenser till resurser genom att exportera en ZIP-fil {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Skapa ett nytt arbetsflöde.
1. Använd packningsfunktionen i Adobe InDesign för att exportera dokumentet.
I Adobe InDesign kan du exportera ett dokument och de länkade resurserna som ett paket. I det här fallet innehåller den exporterade mappen en länkmapp som innehåller underresurser i InDesign-filen.
1. Skapa en ZIP-fil och överför den till AEM-databasen.
1. Starta arbetsflödet för Unarchiver.
1. När arbetsflödet är klart refereras referenserna i mappen Länkar automatiskt till underresurser. Om du vill visa en lista med refererade resurser går du till sidan med resursinformation.

## Lägga till AEM-resurser som referenser i Adobe Photoshop {#refps}

Om du vill lägga till digitala resurser använder du antingen [AEM-datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) eller [överför med AEM](/help/assets/manage-digital-assets.md#uploading-assets) -användargränssnittet.

När arbetsflödet är klart visas referenserna till befintliga AEM-resurser på sidan med tillgångsinformation. De refererade resurserna innehåller även en lista med resurser som de refereras till från. Om du vill visa en lista med refererade resurser går du till sidan med resursinformation.

>[!NOTE]
>
>Resurserna i sammansatta resurser kan också refereras baserat på deras dokument-ID och instans-ID. Den här funktionen är endast tillgänglig i Adobe Illustrator- och Adobe Photoshop-versioner. För andra görs en referens på grundval av den relativa sökvägen för länkade tillgångar i den huvudsakliga sammansatta tillgången, som i tidigare versioner av AEM.

## Visa sidor i en flersidig fil {#view-pages-of-a-multi-page-file}

Med funktionen för sidvisningsprogram i AEM Resurser kan du visa enskilda sidor med flersidiga filer, inklusive PDF-, INDD-, PPT-, PPTX- och Ai-filer. För InDesign kan du extrahera sidor med InDesign-servern. Om förhandsgranskningarna av sidorna sparas när InDesign-filer skapas behövs inte InDesign Server för sidextrahering.

Du kan bläddra igenom enskilda sidor i en fil från resurssidan. Du kan använda alternativ från verktygsfältet för att kommentera enskilda sidor i filen. Du kan också använda alternativet **Sidöversikt** om du vill visa alla sidor samtidigt.

1. Navigera till mappen i AEM Resurser som innehåller den flersidiga filen.
1. Klicka på resursen för att visa resurssidan.
1. Klicka på ikonen Global navigering och välj sedan **Sidor** på menyn.
1. Klicka på vänster- eller högerpilarna under bilden för att navigera till enskilda sidor i filen.
1. Om du vill kommentera en sida klickar du på ikonen **Anteckna** i verktygsfältet och lägger till en kommentar.
1. Om du vill hämta filen klickar du på **hämtningsikonen** .
1. Om du vill visa alla sidor i filen samtidigt klickar du på ikonen **Sidöversikt** .
1. Om du vill visa filens aktivitetsström, inklusive anteckningar och hämtningar, klickar du på AEM-ikonen och väljer sedan **Tidslinje** på menyn.
1. Om du vill visa och redigera metadataegenskaperna för sidan klickar du på ikonen **Visa egenskaper** i verktygsfältet.
