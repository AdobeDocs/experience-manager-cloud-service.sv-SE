---
title: XMP-metadata
description: Läs om metadatastandarden XMP (Extensible Metadata Platform) för metadatahantering. Det används av AEM som ett standardiserat format för att skapa, bearbeta och utbyta metadata.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 496ad0831d20eb7653a3c5727999a2abc5728ec7
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 15%

---


# XMP-metadata {#xmp-metadata}

XMP (Extensible Metadata Platform) är den metadatastandard som används av AEM Assets för all metadatahantering. XMP har ett standardformat för att skapa, bearbeta och utbyta metadata för ett stort antal program.

Förutom universell metadatakodning som kan bäddas in i alla filformat, erbjuder XMP en innehållsmodell [som](#xmp-core-concepts) stöds av Adobe [](#advantages-of-xmp) och andra företag, så att användare av XMP i kombination med AEM Assets har en kraftfull plattform att bygga vidare på.

## XMP - översikt och ekosystem {#xmp-ecosystem}

AEM Assets stöder metadatastandarden XMP. XMP är en standard för bearbetning och lagring av standardiserade och egna metadata i digitala resurser. XMP är en standard som gör att flera program kan arbeta effektivt med metadata.

Produktionspersonal kan till exempel använda det inbyggda XMP-stödet i Adobes program för att skicka information till flera filformat. AEM Assets-databasen extraherar XMP-metadata och använder dem för att hantera innehållets livscykel och ger möjlighet att skapa automatiserade arbetsflöden.

XMP standardiserar hur metadata definieras, skapas och bearbetas genom att tillhandahålla en datamodell, en lagringsmodell och scheman. Alla dessa begrepp beskrivs i detta avsnitt.

Alla äldre metadata från EXIF, ID3 eller Microsoft Office översätts automatiskt till XMP, som kan utökas för att stödja kundspecifika metadatamatchningar, som produktkataloger.

Metadata i XMP består av en uppsättning egenskaper. Dessa egenskaper är alltid kopplade till en specifik enhet som kallas resurs. Egenskaperna är alltså&quot;om&quot; resursen. För XMP är resursen alltid resursen.

XMP definierar en [metadatamodell](https://sv.wikipedia.org/wiki/Metadata) som kan användas med alla definierade metadataobjekt. XMP definierar också särskilda [scheman](https://en.wikipedia.org/wiki/XML_schema) för grundläggande egenskaper som är användbara för att logga en resurs historik genom olika bearbetningssteg – från fotografering, [skanning](https://sv.wikipedia.org/wiki/Bildl%C3%A4sare) och textredigering via fotoredigeringssteg (som [beskärning](https://sv.wikipedia.org/wiki/Bildbesk%C3%A4rning) eller färgjustering) till den slutliga bilden. Med XMP kan alla program och enheter längs vägen lägga till egen information i en digital resurs, som sedan sparas i den slutliga digitala filen.

XMP serialiseras och lagras oftast med en underuppsättning av [W3C](https://sv.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://sv.wikipedia.org/wiki/Resource_Description_Framework) (RDF), som i sin tur uttrycks i [XML](https://sv.wikipedia.org/wiki/XML).

### Fördelar med XMP {#advantages-of-xmp}

XMP har följande fördelar jämfört med andra kodningsstandarder och -scheman:

* XMP-baserade metadata är mycket kraftfulla och detaljerade.
* Med XMP kan du ha flera värden för en egenskap.
* XMP har standardiserad kodning, vilket gör att du enkelt kan utbyta metadata.
* XMP är utökningsbart. Du kan lägga till ytterligare information i dina resurser.

XMP-standarden är utformad för att vara utökningsbar så att du kan lägga till anpassade typer av metadata i XMP-data. EXIF har däremot inte det, utan en fast lista över egenskaper som inte kan utökas.

>[!NOTE]
>
>XMP tillåter vanligtvis inte att binära datatyper bäddas in. Om du vill ha binära data i XMP-filer, till exempel miniatyrbilder, måste de kodas i ett XML-anpassat format, till exempel `Base64`.

### XMP-kärnkoncept {#xmp-core-concepts}

**Namnutrymmen och scheman**

Ett XMP-schema är en uppsättning egenskapsnamn i ett vanligt XML-namnutrymme som innehåller datatypen och beskrivande information. Ett XMP-schema identifieras av dess XML-namnområdes-URI. Om du använder namnutrymmen förhindras konflikter mellan egenskaper i olika scheman som har samma namn men en annan betydelse.

Egenskapen **Creator** i två självständigt utformade scheman kan till exempel avse den person som skapade resursen eller det program som skapade resursen (till exempel Adobe Photoshop).

**XMP-egenskaper och -värden**

XMP kan innehålla egenskaper från ett eller flera av scheman. En vanlig delmängd som används av många Adobe-program kan till exempel vara följande:

* Dublin Core-schema: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP grundläggande schema: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* XMP-schema för rättighetshantering: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP-schema för mediehantering: `xmpMM:DocumentID`

**Språkalternativ**

Med XMP kan du lägga till en egenskap i textegenskaper för att ange textens språk. `xml:lang`

## XMP-tillbakaskrivning till återgivningar {#xmp-writeback-to-renditions}

Den här XMP-återskrivningsfunktionen i Adobe Experience Manager (AEM) Assets replikerar ändringar i resursens återgivningar av metadata.

När du ändrar metadata för en resurs i AEM Resurser eller när du överför resursen, lagras ändringarna först i resursnoden i CRXDE.

XMP-återskrivningsfunktionen sprider metadataändringarna till alla eller specifika återgivningar av resursen.

Tänk dig ett scenario där du ändrar egenskapen [!UICONTROL Title] för resursen som har namnet `Classic Leather` på `Nylon`.

![metadata](assets/metadata.png)

I det här fallet sparar AEM Resurser ändringarna av **[!UICONTROL Title]** egenskapen i `dc:title` parametern för resursens metadata som lagras i resurshierarkin.

![metadata_stored](assets/metadata_stored.png)

AEM Resurser sprider dock inte automatiskt några metadataändringar i återgivningarna av en resurs.

Med XMP-återskrivningsfunktionen kan du sprida metadataändringarna till alla eller specifika återgivningar av resursen. Ändringarna lagras dock inte under metadatanoden i resurshierarkin. I stället bäddar den här funktionen in ändringarna i de binära filerna för återgivningarna.

### Aktivera XMP-återskrivning {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Om du vill att metadataändringarna ska kunna spridas till återgivningarna av resursen när du överför den ändrar du **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfigurationen i Configuration Manager.

1. Öppna Configuration Manager genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfigurationen.
1. Markera **[!UICONTROL Propagate XMP]** alternativet och spara sedan ändringarna.

### Aktivera XMP-återskrivning för specifika återgivningar {#enable-xmp-writeback-for-specific-renditions}

Om du vill att XMP-återskrivningsfunktionen ska kunna sprida metadataändringar för att välja återgivningar, anger du dessa återgivningar i arbetsflödessteget för DAM-metadata WriteBack-arbetsflödet. [!UICONTROL XMP Writeback Process] Som standard konfigureras det här steget med den ursprungliga återgivningen.

Utför dessa steg för att XMP-återskrivningsfunktionen ska kunna sprida metadata till återgivningsminiatyrerna 140.100.png och 319.319.png.

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

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

### Filtrera XMP-metadata {#filtering-xmp-metadata}

AEM Resurser har stöd för filtrering av egenskaper/noder för XMP-metadata som läses från objektbinärfiler och lagras i JCR när resurser hämtas. Filtrering är möjlig via en blockerad lista och en tillåten lista.

Genom att filtrera med hjälp av en blockerad lista kan du importera alla XMP-metadataegenskaper utom de egenskaper som har angetts för undantag. För resurstyper som INDD-filer som har stora mängder XMP-metadata (till exempel 1 000 noder med 10 000 egenskaper) är namnen på de noder som ska filtreras inte alltid kända i förväg. Om filtrering med hjälp av en blockerad lista tillåter att ett stort antal resurser med flera XMP-metadata importeras, kan AEM-instansen/klustret stöta på stabilitetsproblem, till exempel övervakningskö med stoppning.

Filtrering av XMP-metadata via tillåten lista löser problemet genom att du kan definiera XMP-egenskaperna som ska importeras. På så sätt ignoreras andra/okända XMP-egenskaper. För bakåtkompatibilitet kan du lägga till några av dessa egenskaper i filtret som använder en blockerad lista.

>[!NOTE]
>
>Filtrering fungerar bara för egenskaper som härletts från XMP-källor i objektbinärfiler. För egenskaper som härleds från andra källor än XMP, t.ex. EXIF- och IPTC-format, fungerar inte filtreringen. Datumet då resursen skapades sparas till exempel i egenskapen EXIF TIFF `CreateDate` . AEM berättar det här värdet i metadatafältet med namnet `exif:DateTimeOriginal`. Eftersom källan inte är en XMP-källa fungerar inte filtrering på den här egenskapen.

1. Öppna Configuration Manager genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM XmpFilter]** konfigurationen.
1. Om du vill använda filtrering via en tillåten lista markerar du **[!UICONTROL Apply Whitelist to XMP Properties]** och anger de egenskaper som ska importeras i **[!UICONTROL Whitelisted XML Names for XMP filtering]** rutan.

1. Om du vill filtrera bort blockerade XMP-egenskaper efter att ha använt filtrering via tillåten lista anger du dem i **[!UICONTROL Blacklisted XML Names for XMP filtering]** rutan.

   >[!NOTE]
   >
   >The **[!UICONTROL Apply Blacklist to XMP Properties]** option is selected by default. Som standard är filtrering med hjälp av en blockerad lista aktiverat. Om du vill inaktivera sådan filtrering avmarkerar du **[!UICONTROL Apply Blacklist to XMP Properties]** alternativet.

1. Spara ändringarna.

>[!MORELIKETHIS]
>
>* [XMP-specifikation av Adobe](https://www.adobe.com/devnet/xmp.html)

