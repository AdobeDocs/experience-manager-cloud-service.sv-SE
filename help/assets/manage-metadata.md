---
title: Hantera metadata för digitala resurser
description: Lär dig mer om metadatatyperna och hur AEM Assets hjälper dig att hantera metadata för resurser så att det blir enklare att kategorisera och ordna resurser. Tack vare möjligheten att behålla och hantera godtyckliga metadata med dina resurser kan AEM Assets automatiskt ordna och bearbeta resurser baserat på deras metadata.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Hantera metadata för digitala resurser {#managing-metadata-for-digital-assets}

Adobe Experience Manager (AEM) Assets bevarar metadata för alla resurser. Detta gör det enklare att kategorisera och organisera mediefiler och det hjälper personer som letar efter en viss mediefil. Tack vare möjligheten att extrahera metadata från filer som överförts till AEM Assets kan metadatahanteringen integreras med det kreativa arbetsflödet. Tack vare möjligheten att behålla och hantera godtyckliga metadata med dina resurser kan AEM Assets automatiskt ordna och bearbeta resurser baserat på deras metadata.

>[!MORELIKETHIS]
>
>* [XMP-metadata](xmp-metadata.md)
>* [Redigera eller lägga till metadata](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Varför metadata {#why-metadata}

Metadata är data om data. I detta avseende avser data den tillgång du hanterar, till exempel en bild. Metadata är viktiga eftersom de gör det möjligt för användarna att hantera resurser mer effektivt.

Metadata är samlingen av alla data som är tillgängliga för den här bilden, men det behöver inte finnas i bilden, till exempel:

* namnet på tillgången
* tid och datum då den senast ändrades
* storleken på bilden som den sparades i databasen
* namnet på mappen som den finns i

Detta är de grundläggande metadataegenskaper som AEM kan hantera för resurser, vilket gör att användare kan se alla resurser, till exempel ordnade efter det senaste ändringsdatumet - användbart när de försöker identifiera vilka resurser som nyligen har lagts till i databasen.

Du kan lägga till mer högnivådata till digitala resurser, till exempel:

* resurstypen (är det en bild, en video, ett ljudklipp eller ett dokument?)
* tillgångens ägare
* tillgångens namn
* beskrivningen av tillgången
* taggarna som har tilldelats en resurs

Fler metadata hjälper dig att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer. Även om det är möjligt för en enskild person att hantera en lista med några hundra filer helt enkelt baserat på deras filnamn, är det här tillvägagångssättet inte tillräckligt när antalet inblandade personer och antalet mediefiler som hanteras ökar.

När metadata läggs till i resurser växer resursens värde, eftersom resursen blir

* mer åtkomligt - det blir mycket enklare för andra
* enklare att hantera - du kan hitta resurser med samma uppsättning egenskaper enklare och använda ändringar på dem
* mer komplex - ju mer metadata du har lagt till i en resurs, desto viktigare blir det att hantera metadata

Av dessa anledningar ger AEM Assets dig rätt sätt att skapa, hantera och utbyta metadata för dina digitala resurser.

## Grundläggande om metadata {#metadata-basics}

Metadata extraheras från resurser när de importeras (hämtas). Genom att lägga till metadata kan du kategorisera materialet ytterligare.

I det här avsnittet beskrivs olika typer av metadata och kodningsstandarder.

### Tekniska metadata {#technical-metadata}

Tekniska metadata är användbara för program som hanterar digitala resurser och bör inte underhållas manuellt. Tekniska metadata kan fastställas automatiskt av AEM Assets och annan programvara och kan ändras när resursen ändras. Vilka tekniska metadata som är tillgängliga för en mediefil beror till stor del på filtypen för resursen. Exempel på tekniska metadata är följande:

* en fils storlek
* bildens mått (höjd och bredd)
* bithastigheten för en ljud- eller videofil
* bildens upplösning (detaljnivå)

### Beskrivande metadata {#descriptive-metadata}

Beskrivande metadata är metadata som rör programdomänen, till exempel det företag som en resurs kommer från. Beskrivande metadata kan inte bestämmas automatiskt. Den måste skapas manuellt eller halvautomatiskt. En GPS-aktiverad kamera kan till exempel automatiskt spåra latituden och longituden som en bild togs på och lägga till den här informationen i bildens metadata.

På grund av den höga kostnaden för manuell insats som krävs för att skapa beskrivande metadatainformation har standarder upprättats för att underlätta utbyte av metadata mellan olika programsystem och organisationer.

AEM Assets stöder alla relevanta standarder för metadatahantering.

Eftersom metadata är så viktiga och det krävs mycket manuellt arbete för att skapa metadata har standarder fastställts som gör det enklare att utbyta.

### Kodningsstandarder {#encoding-standards}

Det finns flera olika sätt att bädda in metadata i filer. Ett urval kodningsstandarder stöds:

* XMP: som används av AEM Resurser för att lagra extraherade metadata i databasen.
* ID3: för ljud- och videofiler.
* EXIF: för bildfiler.
* Annat/äldre: från Microsoft Word, PowerPoint, Excel och så vidare.

#### XMP {#xmp}

XMP betyder Extensible Metadata Platform och är den metadatastandard som används av AEM Assets för all metadatahantering. XMP erbjuder universell metadatakodning som kan bäddas in i alla filformat, och erbjuder en innehållsmodell som stöds av Adobe och andra företag, så att användare av XMP i kombination med AEM Assets har en kraftfull plattform att bygga vidare på.

#### ID3 {#id}

Data som lagras i dessa ID3-taggar visas när du spelar upp en digital ljudfil på datorn eller en bärbar MP3-spelare.

ID3-taggar är utformade för filformatet MP3. Mer information om format:

* ID3-taggar fungerar i MP3- och MP3pro-filer.
* WAV saknar taggar.
* WMA har egna taggar som inte tillåter implementering med öppen källkod.
* Ogg Vorbis använder Xiph-kommentarer som är inbäddade i OGG-behållaren.
* AAC använder ett märkordsformat.

#### EXIF {#exif}

EXIF betyder Utbytbart bildfilformat och är det vanligaste metadataformatet som används för digitalfoto. Det är ett sätt att bädda in ett fast språk med metadataegenskaper i ett antal filformat, till exempel

* JPEG
* TIFF
* RIFF
* WAV

En stor begränsning för EXIF är att det inte stöds av andra populära bildfilformat som BMP, GIF eller PNG.

EXIF lagrar metadata som par av ett metadatanamn och ett metadatavärde. Dessa metadata name-value-pars kallas också taggar, som inte ska blandas ihop med taggningen i AEM.

Eftersom EXIF automatiskt skapas av moderna digitalkameror och stöds av moderna grafikprogram, kan det ses som den lägsta gemensamma nämnaren för metadatahantering.

De flesta metadatafält som definieras av EXIF är av mycket teknisk karaktär och har begränsad användning för beskrivande metadatahantering. Av den anledningen erbjuder AEM Assets mappning av EXIF-egenskaper till [vanliga metadatamatchningar](metadata-schemas.md) och till [XMP](xmp-metadata.md), det kraftfulla metadataformatet som AEM Assets använder för metadatahantering.

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
1. Om du vill lägga till nya metadata med befintliga metadata i fält som innehåller flera värden väljer du **[!UICONTROL Lägg till läge]**. Om du inte markerar det här alternativet ersätter de nya metadata som finns i fälten. Tryck/klicka på **[!UICONTROL Skicka]**.

   >[!CAUTION]
   >
   >För fält med ett värde läggs de nya metadata inte till det befintliga värdet i fältet, även om du väljer **[!UICONTROL Lägg till läge]**.

## Konfigurera gräns för uppdatering av massmetadata {#configlimit}

För att förhindra DOS-liknande situationer begränsar AEM antalet parametrar som stöds i en Sling-begäran. När du uppdaterar metadata för många resurser på en gång kan du nå gränsen och metadata uppdateras inte för fler resurser. AEM genererar följande varning i loggarna:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Om du vill ändra gränsen öppnar du Webbkonsol ( **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**) och ändrar värdet för **[!UICONTROL maximalt antal POST-parametrar]** i konfigurationen för **[!UICONTROL APache Sling Request Parameter Handling]** OSGi.

## Metadata-schema {#metadata-schemata}

Metadata-scheman är fördefinierade uppsättningar metadata-egenskapsdefinitioner som kan användas i en mängd olika program. Egenskaper är alltid kopplade till en resurs, vilket innebär att egenskaperna är&quot;about&quot; the resource.

Du kan också utforma egna metadatamappningar om det inte finns några som passar dina behov (var försiktig, men inte med att duplicera något som redan finns). Inom en organisation blir det enklare att dela metadata mellan olika organisationer.

Med AEM får du en färdig lista över de vanligaste metadatamappningarna så att du snabbt kan komma igång med din metadatastrategi och välja de metadataegenskaper du behöver från ett redan definierat schema.

De metadatamodeller som stöds visas i följande avsnitt.

### Standardmetadata {#standard-metadata}

* dc - Dublin Core - den viktigaste och mest använda uppsättningen metadata
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard - massor av ämnesspecifika metadata
* rdf - Resource Description Framework - för generiska semantiska webbmetadata
* xmp - Extensible Metadata Platform
* xmpBJ - grundläggande jobbiljetter

### Programspecifika metadata {#application-specific-metadata}

>[!NOTE]
>
>Programspecifika metadata innehåller tekniska och beskrivande metadata. Om du använder dessa kanske andra program inte kan använda metadata. Om du till exempel har en resurs med Adobe Photoshop-metadata och ett annat bildåtergivningsprogram försöker få åtkomst till metadata kanske det inte går att få åtkomst till den.
>
>Om du har många programspecifika metadata i dina resurser kan du skapa ett arbetsflödessteg som ändrar den programspecifika egenskapen till ett standardsteg.

* cd-see - metadata hanteras av ACDSee-programmet [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - används av AEM Assets
* dam - används av AEM Assets
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* Microsoft Photo &amp; MP - Microsoft Photo
* pdf och pdfx
* photoshop &amp; psAux - Adobe Photoshop

### Metadata för hantering av digitala rättigheter {#digital-rights-management-metadata}

* cc - creative comms
* xmpRights
* plus - Picture Licensing Universal System - https://www.useplus.com/
* prisma - https://www.idealliance.org/prism-metadata Publiceringskrav för branschstandardmetadata
* prl - Prism Rights Language
* pur - Användarrättigheter för prismaanvändning
* xmpPlus - integrering av PLUS med XMP

### Fotografispecifika metadata {#photography-specific-metadata}

* exif - massor av teknisk information från kameran, inklusive GPS-position
* crs - photoshop camera raw
* Iptc4xmpCore och iptc4xmpExt
* TIFF - bildmetadata (inte bara för TIFF-bilder)

### Utskriftsspecifika metadata {#print-specific-metadata}

* pdf och pdfx - Adobe PDF och tredjepartsprogram
* prisma - [www.prismstandard.org](https://www.prismstandard.org) publiceringskrav för branschstandardmetadata
* xmp
* xmpPG - xmp för växlad text

### Multimediaspecifika metadata {#multimedia-specific-metadata}

* xmpDM - Dynamiska media
* xmpMM - Mediehantering

## Metadatastyrda arbetsflöden {#metadata-driven-workflows}

Genom att skapa metadatadrivna arbetsflöden kan du automatisera vissa processer, vilket ökar effektiviteten. I ett metadatadrivet arbetsflöde läser arbetsflödet och utför därför en fördefinierad åtgärd.

Du kan till exempel använda metadatadrivna arbetsflöden på olika sätt:

* Arbetsflödet kan kontrollera om en bild har en titel. Om så inte är fallet meddelas användaren om att lägga till en titel.
* Arbetsflödet kan kontrollera om ett copyrightmeddelande för en mediefil tillåter distribution. Om så är fallet skickas resursen till en server. Om så inte är fallet skickas resursen till en annan server.
