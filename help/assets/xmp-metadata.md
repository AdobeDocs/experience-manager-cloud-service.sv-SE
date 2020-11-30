---
title: XMP-metadata
description: Läs mer om metadatastandarden XMP (Extensible Metadata Platform) för metadatahantering. Det används av AEM som ett standardiserat format för att skapa, bearbeta och utbyta metadata.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0c915b32d676ff225cbe276be075d3ae1a865f11
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 20%

---


# XMP-metadata {#xmp-metadata}

XMP (Extensible Metadata Platform) är den metadatastandard som används av AEM Assets för all metadatahantering. XMP har ett standardformat för att skapa, bearbeta och utbyta metadata för en mängd olika program.

Förutom universell metadatakodning som kan bäddas in i alla filformat, har XMP en innehållsmodell [som](#xmp-core-concepts) stöds av Adobe [](#advantages-of-xmp) och andra företag, så att användare av XMP i kombination med AEM Assets har en kraftfull plattform att bygga vidare på.

## XMP översikt och ekosystem {#xmp-ecosystem}

AEM Assets stöder XMP metadatastandard. XMP är en standard för bearbetning och lagring av standardiserade och egna metadata i digitala resurser. XMP är en standard som gör att flera program kan arbeta effektivt med metadata.

Produktionsproffs kan t.ex. använda det inbyggda XMP-stödet i Adobe-program för att skicka information till flera filformat. AEM Assets-databasen extraherar XMP metadata och använder den för att hantera innehållets livscykel och ger möjlighet att skapa automatiserade arbetsflöden.

XMP standardiserar hur metadata definieras, skapas och bearbetas genom att tillhandahålla en datamodell, en lagringsmodell och scheman. Alla dessa begrepp beskrivs i detta avsnitt.

Alla äldre metadata från EXIF, ID3 eller Microsoft Office översätts automatiskt till XMP, som kan utökas för att stödja kundspecifika metadatamatchningar, som produktkataloger.

Metadata i XMP består av en uppsättning egenskaper. Dessa egenskaper är alltid kopplade till en specifik enhet som kallas resurs. Egenskaperna är alltså&quot;om&quot; resursen. När det gäller XMP är resursen alltid resursen.

XMP definierar en [metadatamodell](https://sv.wikipedia.org/wiki/Metadata) som kan användas med alla definierade metadataobjekt. XMP definierar också särskilda [scheman](https://en.wikipedia.org/wiki/XML_schema) för grundläggande egenskaper som är användbara för att logga en resurs historik genom olika bearbetningssteg – från fotografering, [skanning](https://sv.wikipedia.org/wiki/Bildl%C3%A4sare) och textredigering via fotoredigeringssteg (som [beskärning](https://sv.wikipedia.org/wiki/Bildbesk%C3%A4rning) eller färgjustering) till den slutliga bilden. Med XMP kan alla program och enheter längs vägen lägga till egen information i en digital resurs, som sedan sparas i den slutliga digitala filen.

XMP serialiseras och lagras oftast med en underuppsättning av [W3C](https://sv.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://sv.wikipedia.org/wiki/Resource_Description_Framework) (RDF), som i sin tur uttrycks i [XML](https://sv.wikipedia.org/wiki/XML).

### Fördelar med XMP {#advantages-of-xmp}

XMP har följande fördelar jämfört med andra kodningsstandarder och -scheman:

* XMP metadata är mycket kraftfulla och detaljerade.
* XMP kan du ha flera värden för en egenskap.
* XMP har standardiserad kodning, vilket gör det enkelt att utbyta metadata.
* XMP kan utökas. Du kan lägga till ytterligare information i dina resurser.

XMP är utformad för att vara utökningsbar, så att du kan lägga till anpassade typer av metadata i XMP. EXIF har däremot inte det, utan en fast lista över egenskaper som inte kan utökas.

>[!NOTE]
>
>XMP tillåter vanligtvis inte att binära datatyper bäddas in. Om du vill ha binära data i XMP, t.ex. miniatyrbilder, måste de kodas i ett XML-anpassat format, t.ex. `Base64`.

### XMP grundläggande begrepp {#xmp-core-concepts}

**Namnutrymmen och scheman**

Ett XMP är en uppsättning egenskapsnamn i ett vanligt XML-namnutrymme som innehåller datatypen och beskrivande information. Ett XMP-schema identifieras av dess XML-namnområdes-URI. Om du använder namnutrymmen förhindras konflikter mellan egenskaper i olika scheman som har samma namn men en annan betydelse.

Egenskapen **Creator** i två självständigt utformade scheman kan till exempel avse den person som skapade resursen eller det program som skapade resursen (till exempel Adobe Photoshop).

**XMP egenskaper och värden**

XMP kan innehålla egenskaper från ett eller flera av scheman. En vanlig delmängd som används av många Adobe-program kan till exempel vara följande:

* Dublin Core-schema: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP grundläggande schema: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* XMP Rättighetshanteringsschema: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP för mediahantering: `xmpMM:DocumentID`

**Språkalternativ**

XMP ger dig möjlighet att lägga till en `xml:lang` egenskap i textegenskaper för att ange textens språk.

## XMP till återgivning {#xmp-writeback-to-renditions}

Den här XMP återskrivningsfunktionen i Adobe Experience Manager (AEM) Resurser replikerar ändringar i resursens återgivningar av metadata.

När du ändrar metadata för en resurs i AEM Assets eller när du överför resursen, lagras ändringarna först i resursnoden i CRXDE.

XMP återskrivningsfunktion sprider metadataändringarna till alla eller specifika återgivningar av resursen.

Tänk dig ett scenario där du ändrar egenskapen [!UICONTROL Title] för resursen som har namnet `Classic Leather` på `Nylon`.

![metadata](assets/metadata.png)

I det här fallet sparar AEM Assets ändringarna i **[!UICONTROL Title]** egenskapen i `dc:title` -parametern för resursens metadata som lagras i resurshierarkin.

![metadata_stored](assets/metadata_stored.png)

AEM Assets sprider dock inte automatiskt några metadataändringar till återgivningar av en resurs.

Med funktionen XMP kan du sprida metadataändringarna till alla eller vissa återgivningar av resursen. Ändringarna lagras dock inte under metadatanoden i resurshierarkin. I stället bäddar den här funktionen in ändringarna i de binära filerna för återgivningarna.

### Aktivera XMP {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Om du vill att metadataändringarna ska kunna spridas till återgivningarna av resursen när du överför den ändrar du **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfigurationen i Configuration Manager.

1. Öppna Configuration Manager genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfigurationen.
1. Markera **[!UICONTROL Propagate XMP]** alternativet och spara sedan ändringarna.

### Aktivera XMP återskrivning för specifika återgivningar {#enable-xmp-writeback-for-specific-renditions}

Om du vill att XMP återskrivningsfunktion ska kunna sprida metadataändringar för att välja återgivningar, anger du dessa återgivningar i arbetsflödessteget för DAM-metadataåterställningsarbetsflödet. [!UICONTROL XMP Writeback Process] Som standard konfigureras det här steget med den ursprungliga återgivningen.

Utför de här stegen för att XMP återskrivningsfunktionen för att sprida metadata till återgivningsminiatyrerna 140.100.png och 319.319.png.

1. Tryck/klicka på AEM-logotypen och navigera sedan till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Öppna arbetsflödesmodellen på sidan **[!UICONTROL DAM Metadata Writeback]** Modeller.
1. På egenskapssidan för **[!UICONTROL DAM Metadata Writeback]** öppnar du steget **[!UICONTROL XMP Writeback Process]**.
1. I dialogrutan **[!UICONTROL Step Properties]** trycker/klickar du på fliken **[!UICONTROL Process]**.
1. Lägg till i **[!UICONTROL Arguments]** rutan `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`och tryck/klicka sedan **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Spara ändringarna.
1. Om du vill återskapa Pyramid TIFF-återgivningar (PTIFF) för Dynamic Media-bilder med de nya attributen lägger du till steget **[!UICONTROL Dynamic Media Process Image Assets]** i arbetsflödet för DAM-metadataåterskrivning. PTIFF-återgivningar skapas och lagras bara lokalt i en Dynamic Media-hybridimplementering.

1. Spara arbetsflödet.

Metadataändringarna sprids till miniatyrbilden för återgivningarna.140.100.png och miniatyrbilden.319.319.png för resursen, inte till de andra.

>[!MORELIKETHIS]
>
>* [XMP specifikationer från Adobe](https://www.adobe.com/devnet/xmp.html)

