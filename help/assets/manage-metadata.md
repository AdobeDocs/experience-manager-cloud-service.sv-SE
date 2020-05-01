---
title: Hantera metadata för digitala resurser i [!DNL Adobe Experience Manager].
description: Lär dig mer om metadatatyperna och hur [!DNL Adobe Experience Manager Assets] hjälper dig att hantera metadata för resurser så att det blir enklare att kategorisera och ordna resurser. Med [!DNL Experience Manager] går det att automatiskt ordna och bearbeta resurser baserat på deras metadata.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Hantera metadata för dina digitala resurser {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] sparar metadata för varje resurs. Detta gör det enklare att kategorisera och ordna resurser och det hjälper personer som letar efter en viss resurs. Tack vare möjligheten att extrahera metadata från filer som överförts till [!DNL Experience Manager Assets]kan metadatahanteringen integreras med det kreativa arbetsflödet. Tack vare möjligheten att behålla och hantera metadata med dina resurser kan du automatiskt ordna och bearbeta resurser baserat på deras metadata. [!DNL Experience Manager Assets]

>[!MORELIKETHIS]
>
>* [XMP-metadata](xmp-metadata.md)
>* [Redigera eller lägga till metadata](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Varför metadata {#why-metadata}

Metadata är data om data. I det här avseendet avser data era digitala resurser, till exempel en bild. Metadata är avgörande för effektiv resurshantering.

Metadata är en samling med alla data som är tillgängliga för en resurs, men som inte nödvändigtvis finns i bilden. Några exempel på metadata är:

* Namnet på resursen.
* Tid och datum för senaste ändring.
* Storlek på resursen när den sparades i databasen.
* Namnet på mappen som den finns i.
* Relaterade resurser eller tillämpade taggar.

Detta är de grundläggande metadataegenskaperna som [!DNL Experience Manager] kan hantera resurser, vilket gör att användare kan se alla resurser, till exempel ordnade efter det senaste ändringsdatumet - användbart när de försöker identifiera vilka resurser som nyligen har lagts till i databasen.

Du kan lägga till mer högnivådata till digitala resurser, till exempel:

* Typ av resurs (är det en bild, en video, ett ljudklipp eller ett dokument?).
* Tillgångens ägare.
* Tillgångens namn.
* Beskrivning av tillgången.
* Taggar som tilldelats en resurs.

Fler metadata hjälper dig att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer. Det går att hantera några hundra filer baserat på bara filnamnen. Den här metoden är dock inte skalbar och blir snabbt kort när antalet inblandade personer och antalet förvaltade resurser ökar.

Med hjälp av metadata ökar värdet på en digital resurs eftersom resursen blir

* Mer åtkomligt - system och användare hittar det enkelt.
* Enklare att hantera - du kan hitta resurser med samma uppsättning egenskaper enklare och använda ändringarna på dem.
* Mer komplett - ju fler metadata du har lagt till i en resurs, desto mer information och sammanhang får den.

Därför har du tillgång [!DNL Assets] till rätt sätt att skapa, hantera och utbyta metadata för dina digitala resurser.

## Typer av metadata {#types-of-metadata}

De två grundläggande metadatatyperna är tekniska metadata och beskrivande metadata.

Tekniska metadata är användbara för program som hanterar digitala resurser och bör inte underhållas manuellt. [!DNL Experience Manager Assets] och andra program bestämmer automatiskt tekniska metadata och metadata kan ändras när resursen ändras. Vilka tekniska metadata som är tillgängliga för en mediefil beror till stor del på filtypen för resursen. Några exempel på tekniska metadata är:

* Storlek på en fil.
* Bildens mått (höjd och bredd).
* Bithastighet för en ljud- eller videofil.
* Upplösning (detaljnivå) för en bild.

Beskrivande metadata är metadata som rör programdomänen, till exempel det företag som en resurs kommer från. Beskrivande metadata kan inte bestämmas automatiskt. Den skapas manuellt eller halvautomatiskt. En GPS-aktiverad kamera kan till exempel automatiskt spåra latitud och longitud och lägga till geotagga bilden.

På grund av den höga kostnaden för manuell insats som krävs för att skapa beskrivande metadatainformation har standarder upprättats för att underlätta utbyte av metadata mellan olika programsystem och organisationer.

[!DNL Experience Manager Assets] stöder alla relevanta standarder för metadatahantering.

Eftersom metadata är så viktiga och det krävs mycket manuellt arbete för att skapa metadata har standarder fastställts som gör det enklare att utbyta.

## Kodningsstandarder {#encoding-standards}

Det finns olika sätt att bädda in metadata i filer. Ett urval kodningsstandarder stöds:

* XMP: används av [!DNL Assets] för att lagra extraherade metadata i databasen.
* ID3: för ljud- och videofiler.
* Exif: för bildfiler.
* Annat/äldre: från [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]och så vidare.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) är en öppen standard som används av [!DNL Experience Manager Assets] för all metadatahantering. Standarden erbjuder universell metadatakodning som kan bäddas in i alla filformat. Adobe och andra företag stöder XMP-standarden eftersom den erbjuder en innehållsmodell med mycket innehåll. Användare av XMP-standard och av [!DNL Experience Manager Assets] har en kraftfull plattform att bygga vidare på. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Data som lagras i dessa ID3-taggar visas när du spelar upp en digital ljudfil på datorn eller en bärbar MP3-spelare.

ID3-taggar är utformade för filformatet MP3. Mer information om format:

* ID3-taggar fungerar i MP3- och mp3PRO-filer.
* WAV saknar taggar.
* WMA har egna taggar som inte tillåter implementering med öppen källkod.
* Ogg Vorbis använder Xiph-kommentarer som är inbäddade i Ogg-behållaren.
* AAC använder ett märkordsformat.

### Exif {#exif}

Exchangeable image file format (Exif) är det vanligaste metadataformatet som används för digitalfoto. Det är ett sätt att bädda in en fast ordlista med metadataegenskaper i många filformat, till exempel JPEG, TIFF, RIFF och WAV. Exif lagrar metadata som par av ett metadatanamn och ett metadatavärde. Dessa metadata name-value-pars kallas också taggar, som inte ska blandas ihop med taggarna i [!DNL Experience Manager]. Eftersom Exif automatiskt skapas av moderna digitalkameror och stöds av moderna grafikprogram, kan det ses som den lägsta gemensamma nämnaren för metadatahantering.

En stor begränsning för Exif är att ett fåtal populära bildfilsformat som BMP, GIF och PNG inte har stöd för det.

Metadatafält som vanligtvis definieras av Exif är av teknisk natur och har begränsad användning för beskrivande metadatahantering. Därför erbjuder [!DNL Experience Manager Assets] mappning av Exif-egenskaper till [vanliga metadatamatchningar](metadata-schemas.md) och till XMP.

#### Andra metadata {#other-metadata}

Andra metadata som kan bäddas in från filer är bland annat Microsoft Word, PowerPoint och Excel.

## Hantera metadata för dina digitala resurser {#manage-assets-metadata}

Med Enterprise Manager Assets kan du redigera metadata för flera resurser samtidigt så att du snabbt kan sprida vanliga metadataändringar till resurser samtidigt. Använd sidan [!UICONTROL Egenskaper] om du vill ändra metadataegenskaper till ett gemensamt värde eller lägga till eller ändra taggar. Om du vill anpassa sidan för metadataegenskaper, inklusive lägga till, ändra eller ta bort metadataegenskaper, använder du schemaredigeraren.

>[!NOTE]
>
>Massredigeringsmetoderna fungerar för resurser som är tillgängliga i en mapp eller en samling. För resurser som är tillgängliga i olika mappar eller som matchar ett gemensamt villkor är det möjligt att [uppdatera metadata satsvis efter sökning](/help/assets/search-assets.md#metadataupdates).

1. Navigera till platsen för de resurser som du vill redigera.
1. Markera de resurser som du vill redigera gemensamma egenskaper för.
1. Tryck/klicka på **[!UICONTROL Egenskaper]** i verktygsfältet för att öppna sidan [!UICONTROL Egenskaper] för de valda resurserna.

   >[!NOTE]
   >
   >När du väljer flera resurser markeras det lägsta gemensamma överordnade formuläret för resurserna. På sidan [!UICONTROL Egenskaper] visas alltså endast metadatafält som är gemensamma för alla [!UICONTROL egenskapssidor] för de enskilda resurserna.

1. Ändra metadataegenskaperna för markerade resurser på de olika flikarna.
1. Om du vill visa metadataredigeraren för en viss resurs avmarkerar du återstående resurser i listan. Metadataredigeringsfälten fylls i med metadata för den aktuella resursen.

   >[!NOTE]
   >
   >* På sidan [!UICONTROL Egenskaper] kan du ta bort resurser från resurslistan genom att avmarkera dem. Resurslistan har alla resurser markerade som standard. Metadata för resurser som du tar bort från listan uppdateras inte.
   >* Överst i resurslistan markerar du kryssrutan nära **[!UICONTROL Titel]** för att växla mellan att markera resurserna och rensa listan.


1. Om du vill välja ett annat metadataram för resurserna trycker/klickar du på **[!UICONTROL Inställningar]** i verktygsfältet och väljer önskat schema. Spara ändringarna.
1. Om du vill lägga till nya metadata till befintliga metadata i fält som innehåller flera värden väljer du **[!UICONTROL tilläggsläget]**. Om du inte markerar det här alternativet ersätter de nya metadata de data som finns i fälten. Tryck/klicka på **[!UICONTROL Skicka]**.

   >[!CAUTION]
   >
   >För fält med ett enda värde läggs de nya metadata inte till det befintliga värdet i fältet, även om du väljer **[!UICONTROL tilläggsläget]**.

## Konfigurera gräns för uppdatering av massmetadata {#configlimit}

För att förhindra DOS-liknande situationer begränsar AEM antalet parametrar som stöds i en Sling-begäran. När du uppdaterar metadata för många resurser på en gång kan du nå gränsen och metadata uppdateras inte för fler resurser. AEM genererar följande varning i loggarna:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Om du vill ändra gränsen öppnar du Webbkonsol ( **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**) och ändrar värdet för **[!UICONTROL maximalt antal POST-parametrar]** i konfigurationen för **[!UICONTROL APache Sling Request Parameter Handling]** OSGi.

## Metadata-scheman {#metadata-schemata}

Metadata-scheman är fördefinierade uppsättningar metadataegenskapsdefinitioner som kan användas i olika program. Egenskaper är alltid kopplade till en resurs, vilket innebär att egenskaperna är&quot;about&quot; för resursen.

Du kan också utforma egna metadatamatchningar om det inte finns några som passar dina behov. Duplicera inte befintlig information. Inom en organisation gör separerade scheman det enklare att dela metadata. [!DNL Experience Manager] innehåller en standardlista med de vanligaste metadataschemana. Listan hjälper dig att snabbt komma igång med metadatastrategin och snabbt välja de metadataegenskaper du behöver.

De metadatamappningar som stöds listas nedan.

### Standardmetadata {#standard-metadata}

* dc - [!DNL Dublin Core] är den viktigaste och mest använda uppsättningen metadata.
* DICOM - Digital Imaging and Communications in Medicine.
* Iptc4xmpCore och iptc4xmpExt - International Press Communications Standard innehåller många ämnesspecifika metadata.
* rdf - Resource Description Framework - för generiska semantiska webbmetadata.
* xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - Grundläggande jobbiljetter.

### Programspecifika metadata {#application-specific-metadata}

Programspecifika metadata innehåller tekniska och beskrivande metadata. Om du använder dessa kanske andra program inte kan använda metadata. Om du t.ex. har en resurs med [!DNL Adobe Photoshop] metadata och ett annat bildåtergivningsprogram försöker få åtkomst till metadata kanske den inte kan få åtkomst till metadata. Om du har mycket programspecifika metadata i dina resurser kan du skapa ett arbetsflödessteg som ändrar en programspecifik egenskap till en standardegenskap.

* ACDSee - metadata som hanteras av [!DNL ACDSee] programmet. Se [www.acdsee.com/](https://www.acdsee.com/).
* album - [!DNL Adobe Photoshop Album].
* cq - Används av [!DNL Experience Manager Assets].
* dam - Används av [!DNL Experience Manager Assets].
* dex - Optima SC Description Explorer.
* crs - Adobe Photoshop Camera Raw.
* lr - [!DNL Adobe Lightroom].
* mediapro - IView MediaPro.
* Microsoft Photo &amp; MP - Microsoft Photo.
* pdf och pdfx.
* photoshop &amp; psAux - [!DNL Adobe Photoshop].

### Metadata för hantering av digitala rättigheter {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* plus - [Picture Licensing Universal System](https://www.useplus.com).
* prism - https://www.idealliance.org/prism-metadata för publicering av standardmetadata.
* PRL - PRISM Rights Language.
* PUR - PRISM-användningsrättigheter.
* xmpPlus - integrering av PLUS med XMP.

### Fotografispecifika metadata {#photography-specific-metadata}

* Exif - Teknisk information från kameran, inklusive GPS-position.
* CRS - [!DNL Camera Raw] schema.
* Iptc4xmpCore och iptc4xmpExt.
* TIFF - bildmetadata (inte bara för TIFF-bilder).

### Utskriftsspecifika metadata {#print-specific-metadata}

* pdf och pdfx - Adobe PDF och tredjepartsprogram.
* prism - [www.prismstandard.org](https://www.prismstandard.org) publiceringskrav för branschstandardmetadata.
* XMP.
* xmpPG - XMP-metadata för växlad text.

### Multimediaspecifika metadata {#multimedia-specific-metadata}

* xmpDM - [!DNL Dynamic Media].
* xmpMM - Mediehantering.

## Metadatastyrda arbetsflöden {#metadata-driven-workflows}

Genom att skapa metadatadrivna arbetsflöden kan du automatisera vissa processer, vilket ökar effektiviteten. I ett metadatadrivet arbetsflöde läser arbetsflödet och utför därför en fördefinierad åtgärd. Du kan till exempel använda metadatadrivna arbetsflöden på olika sätt:

* Arbetsflödet kan kontrollera om en bild har en titel eller inte. Om så inte är fallet meddelas systemet om att en titel ska läggas till.
* Arbetsflödet kan kontrollera om ett copyrightmeddelande för en mediefil tillåter distribution eller inte. Systemet skickar därför resursen till den ena servern eller den andra.
* Ett arbetsflöde kan söka efter resurser utan fördefinierade, obligatoriska metadata eller resurser med *ogiltiga* metadata.
