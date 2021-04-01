---
title: Hantera metadata för digitala resurser
description: Lär dig mer om metadatatyperna och hur [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] gör det möjligt att automatiskt ordna och bearbeta resurser baserat på deras metadata.
contentOwner: AG
mini-toc-levels: 1
feature: Resurshantering,Metadata
role: Affärsman, arkitekt, administratör
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 3%

---


# Hantera metadata för dina digitala resurser {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] sparar metadata för varje resurs. Det gör det enklare att kategorisera och ordna resurser och det hjälper personer som letar efter en viss resurs. Tack vare möjligheten att extrahera metadata från filer som överförts till [!DNL Experience Manager Assets] kan metadatahanteringen integreras med det kreativa arbetsflödet. Med möjligheten att behålla och hantera metadata med dina resurser kan du automatiskt ordna och bearbeta resurser baserat på deras metadata.

>[!MORELIKETHIS]
>
>* [XMP-metadata](xmp-metadata.md)
>* [Redigera eller lägga till metadata](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Därför behöver vi metadata {#why-metadata}

Metadata är data om data. I det här avseendet avser data era digitala resurser, till exempel en bild. Metadata är avgörande för effektiv resurshantering.

Metadata är en samling med alla data som är tillgängliga för en resurs, men som inte nödvändigtvis finns i bilden. Några exempel på metadata är:

* Namnet på resursen.
* Tid och datum för senaste ändring.
* Storlek på resursen när den sparades i databasen.
* Namnet på mappen som den finns i.
* Relaterade resurser eller tillämpade taggar.

Ovanstående är de grundläggande metadataegenskaper som [!DNL Experience Manager] kan hantera för resurser, vilket gör att användare kan se alla resurser. Det kan till exempel vara bra att beställa resurser efter det senaste ändringsdatumet när du försöker identifiera nyligen tillagda resurser.

Du kan lägga till mer högnivådata till digitala resurser, till exempel:

* Typ av resurs (är det en bild, en video, ett ljudklipp eller ett dokument?).
* Tillgångens ägare.
* Tillgångens namn.
* Beskrivning av tillgången.
* Taggar som tilldelats en resurs.

Fler metadata hjälper dig att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer. Det går att hantera några hundra filer baserat på bara filnamnen. Den här metoden är dock inte skalbar. Den blir kort när antalet inblandade och antalet förvaltade tillgångar ökar.

Med hjälp av metadata ökar värdet på en digital resurs eftersom resursen blir

* Mer åtkomligt - system och användare hittar det enkelt.
* Enklare att hantera - du kan hitta resurser med samma uppsättning egenskaper enklare och använda ändringarna på dem.
* Fullständigt - materialet innehåller mer information och sammanhang med fler metadata.

Av dessa anledningar ger [!DNL Assets] dig rätt sätt att skapa, hantera och utbyta metadata för dina digitala resurser.

## Typer av metadata {#types-of-metadata}

De två grundläggande metadatatyperna är tekniska metadata och beskrivande metadata.

Tekniska metadata är användbara för program som hanterar digitala resurser och bör inte underhållas manuellt. [!DNL Experience Manager Assets] och andra program bestämmer automatiskt tekniska metadata och metadata kan ändras när resursen ändras. Vilka tekniska metadata som är tillgängliga för en mediefil beror till stor del på filtypen för resursen. Några exempel på tekniska metadata är:

* Storlek på en fil.
* Dimensioner (höjd och bredd) för en bild.
* Bithastighet för en ljud- eller videofil.
* Upplösning (detaljnivå) för en bild.

Beskrivande metadata är metadata som rör programdomänen, till exempel det företag som en resurs kommer från. Beskrivande metadata kan inte bestämmas automatiskt. Den skapas manuellt eller halvautomatiskt. En GPS-aktiverad kamera kan till exempel automatiskt spåra latitud och longitud och lägga till geotagga bilden.

Kostnaden för att manuellt skapa beskrivande metadatainformation är hög. Därför har standarder upprättats för att underlätta utbyte av metadata mellan olika programsystem och organisationer. [!DNL Experience Manager Assets] stöder alla relevanta standarder för metadatahantering.

## Kodningsstandarder {#encoding-standards}

Det finns olika sätt att bädda in metadata i filer. Ett urval kodningsstandarder stöds:

* XMP: används av [!DNL Assets] för att lagra extraherade metadata i databasen.
* ID3: för ljud- och videofiler.
* Exif: för bildfiler.
* Annat/äldre: från [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] och så vidare.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) är en öppen standard som används av  [!DNL Experience Manager Assets] för all metadatahantering. Standarden erbjuder universell metadatakodning som kan bäddas in i alla filformat. Adobe och andra företag stöder XMP standard eftersom de erbjuder en innehållsmodell med mycket innehåll. Användare av XMP och [!DNL Experience Manager Assets] har en kraftfull plattform att bygga vidare på. Mer information finns i [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Data som lagras i dessa ID3-taggar visas när du spelar upp en digital ljudfil på datorn eller en bärbar MP3-spelare.

ID3-taggar är utformade för filformatet MP3. Mer information om format:

* ID3-taggar fungerar i MP3- och mp3PRO-filer.
* WAV saknar taggar.
* WMA har egna taggar som inte tillåter implementering med öppen källkod.
* Ogg Vorbis använder Xiph-kommentarer som är inbäddade i Ogg-behållaren.
* AAC använder ett märkordsformat.

### Exif {#exif}

Exchangeable image file format (Exif) är det vanligaste metadataformatet som används för digitalfoto. Det är ett sätt att bädda in en fast ordlista med metadataegenskaper i många filformat, till exempel JPEG, TIFF, RIFF och WAV. Exif lagrar metadata som par av ett metadatanamn och ett metadatavärde. Dessa metadata name-value-pars kallas också taggar, som inte ska blandas ihop med taggarna i [!DNL Experience Manager]. Moderna digitalkameror skapar Exif-metadata och moderna grafikprogram stöder det. Exif-formatet är den minsta gemensamma nämnaren för metadatahantering, särskilt för bilder.

En stor begränsning för Exif är att ett fåtal populära bildfilsformat som BMP, GIF och PNG inte har stöd för det.

Metadatafält som definieras av Exif är vanligtvis av teknisk natur och har begränsad användning för beskrivande metadatahantering. Av den anledningen erbjuder [!DNL Experience Manager Assets] mappning av Exif-egenskaper till [vanliga metadatamatchningar](metadata-schemas.md) och till XMP.

#### Andra metadata {#other-metadata}

Andra metadata som kan bäddas in från filer är bland annat [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] och så vidare.

## Hantera metadata för dina digitala resurser {#manage-assets-metadata}

Med Enterprise Manager Assets kan du redigera metadata för flera resurser samtidigt så att du snabbt kan sprida vanliga metadataändringar till resurser samtidigt. Använd sidan [!UICONTROL Properties] om du vill ändra metadataegenskaper till ett gemensamt värde eller lägga till eller ändra taggar. Om du vill anpassa sidan för metadataegenskaper, inklusive lägga till, ändra eller ta bort metadataegenskaper, använder du schemaredigeraren.

>[!NOTE]
>
>Massredigeringsmetoderna fungerar för resurser som är tillgängliga i en mapp eller en samling. För resurser som är tillgängliga mellan mappar eller matchar ett gemensamt villkor är det möjligt att [uppdatera metadata satsvis efter sökning](/help/assets/search-assets.md#metadata-updates).

1. Navigera till platsen för de resurser som du vill redigera.
1. Markera de resurser som du vill redigera gemensamma egenskaper för.
1. Tryck/klicka på **[!UICONTROL Properties]** i verktygsfältet för att öppna sidan [!UICONTROL Properties] för de valda resurserna.

   >[!NOTE]
   >
   >När du väljer flera resurser markeras det lägsta gemensamma överordnade formuläret för resurserna. Med andra ord visar sidan [!UICONTROL Properties] bara metadatafält som är gemensamma på [!UICONTROL Properties]-sidorna för alla enskilda resurser.

1. Ändra metadataegenskaperna för markerade resurser på de olika flikarna.
1. Om du vill visa metadataredigeraren för en viss resurs avbryter du valet av återstående resurser i listan. Metadataredigeringsfälten fylls i med metadata för den aktuella resursen.

   >[!NOTE]
   >
   >* På sidan [!UICONTROL Properties] kan du ta bort resurser från resurslistan genom att avbryta markeringen. Resurslistan har alla resurser markerade som standard. Metadata för resurser som du tar bort från listan uppdateras inte.
   >* Överst i resurslistan markerar du kryssrutan nära **[!UICONTROL Title]** för att växla mellan att markera resurserna och rensa listan.


1. Om du vill välja ett annat metadataram för resurserna trycker/klickar du på **[!UICONTROL Settings]** i verktygsfältet och väljer önskat schema. Spara ändringarna.
1. Om du vill lägga till nya metadata till befintliga metadata i fält som innehåller flera värden väljer du **[!UICONTROL Append mode]**. Om du inte markerar det här alternativet ersätter de nya metadata de data som finns i fälten. Tryck/klicka på **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >För fält med ett enda värde läggs de nya metadata inte till det befintliga värdet i fältet, även om du väljer **[!UICONTROL Append mode]**.

## Anpassade metadata med bearbetningsprofil {#metadata-compute-service}

Resurser som [!DNL Cloud Service] kan generera anpassade metadata för en resurs med molnbaserade tjänster. Konfigurera en bearbetningsprofil för att generera anpassade metadata. Se [hur du använder bearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

![Metadataåtergivning i bearbetningsprofil](assets/processing-profile-metadata.png)

>[!TIP]
>
>Endast en bearbetningsprofil kan användas för en mapp. Om du vill använda flera bearbetningar på resurser i en mapp lägger du till fler alternativ i en enda bearbetningsprofil. En enskild profil kan till exempel generera återgivningar, omkoda resurser, generera anpassade metadata och så vidare. Du kan använda MIME-typfilter för varje åtgärd så att rätt åtgärd aktiveras för det filformat som krävs.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## Metadata schemata {#metadata-schemata}

Metadata-scheman är fördefinierade uppsättningar metadataegenskapsdefinitioner som kan användas i olika program. Egenskaper är alltid kopplade till en resurs, vilket innebär att egenskaperna är&quot;about&quot; för resursen.

Du kan också utforma egna metadatamatchningar om det inte finns några som passar dina behov. Duplicera inte befintlig information. Inom en organisation gör separerade scheman det enklare att dela metadata. [!DNL Experience Manager] innehåller en standardlista med de vanligaste metadataschemana. Listan hjälper dig att snabbt komma igång med metadatastrategin och snabbt välja de metadataegenskaper du behöver.

De metadatamappningar som stöds listas nedan.

### Standardmetadata {#standard-metadata}

* DC - [!DNL Dublin Core] är en viktig och allmänt använd uppsättning metadata.
* DICOM - Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` och  `iptc4xmpExt` - International Press Communications Standard innehåller många ämnesspecifika metadata.
* RDF - Resource Description Framework - för generiska semantiska webbmetadata.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Grundläggande jobbiljetter.

### Programspecifika metadata {#application-specific-metadata}

Programspecifika metadata innehåller tekniska och beskrivande metadata. Om du använder sådana metadata kanske andra program inte kan använda dessa metadata. Ett annat bildåtergivningsprogram kanske inte kan komma åt [!DNL Adobe Photoshop]-metadata. Du kan skapa ett arbetsflödessteg som ändrar en programspecifik egenskap till en standardegenskap.

* ACDSe - Metadata som hanteras av [!DNL ACDSee]-programmet. Se [www.acdsee.com/](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Används av [!DNL Experience Manager Assets].
* DAM - Används av [!DNL Experience Manager Assets].
* DEX - [Optima SC Description Explorer](http://www.optimasc.com/products/dex/index.html) är en samling verktyg för metadata och filhantering för Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* Microsoft Photo och MP - Microsoft Photo.
* PDF och PDF/X.
* Photoshop och psAux - [!DNL Adobe Photoshop].

### Digital Rights Management-metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Universellt system för bildlicensiering](https://www.useplus.com).
* PRISM - [Publiceringskrav för branschstandardmetadata](https://www.idealliance.org/prism-metadata).
* PRL - PRISM Rights Language.
* PUR - PRISM-användningsrättigheter.
* `xmpPlus` - Integration av PLUS med XMP.

### Fotografispecifika metadata {#photography-specific-metadata}

* Exif - Teknisk information från kameran, inklusive GPS-position.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` and `iptc4xmpExt`.
* TIFF - bildmetadata (inte bara för TIFF-bilder).

### Utskriftsspecifika metadata {#print-specific-metadata}

* PDF och PDF/X - Adobe PDF och tredjepartsprogram.
* PRISM - [Publiceringskrav för branschstandardmetadata](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadata för sidindelad text.

### Multimediespecifika metadata {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Mediehantering.

## Metadatadrivna arbetsflöden {#metadata-driven-workflows}

Genom att skapa metadatadrivna arbetsflöden kan du automatisera vissa processer, vilket ökar effektiviteten. I ett metadatadrivet arbetsflöde läser arbetsflödet och utför därför en fördefinierad åtgärd. Du kan till exempel använda metadatadrivna arbetsflöden på olika sätt:

* Arbetsflödet kan kontrollera om en bild har en titel eller inte. Om så inte är fallet meddelas systemet om att en titel ska läggas till.
* Arbetsflödet kan kontrollera om ett copyrightmeddelande för en mediefil tillåter distribution eller inte. Systemet skickar alltså resursen till den ena servern eller den andra.
* Ett arbetsflöde kan söka efter resurser utan fördefinierade, obligatoriska metadata eller resurser med *ogiltiga*-metadata.
