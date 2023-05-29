---
title: XMP-metadata
description: Läs mer om metadatastandarden XMP (Extensible Metadata Platform) för metadatahantering. Det används av Experience Manager som ett standardiserat format för att skapa, bearbeta och utbyta metadata.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 5da4be3ec9af6a00cce8d80b8eea7f7520754a1d
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 17%

---

# XMP-metadata {#xmp-metadata}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html) |
| AEM as a Cloud Service | Den här artikeln |

XMP (Extensible Metadata Platform) är den metadatastandard som används av Experience Manager Assets för all metadatahantering. XMP har ett standardformat för att skapa, bearbeta och utbyta metadata för en mängd olika program.

Förutom universell metadatakodning som kan bäddas in i alla filformat har XMP [innehållsmodell](#xmp-core-concepts) och är [stöds av Adobe](#advantages-of-xmp) och andra företag, så att användare av XMP i kombination med [!DNL Assets] har en kraftfull plattform att bygga vidare på.

## XMP översikt och ekosystem {#xmp-ecosystem}

[!DNL Assets] stöder XMP metadatastandard. XMP är en standard för bearbetning och lagring av standardiserade och egna metadata i digitala resurser. XMP är en standard som gör att flera program kan arbeta effektivt med metadata.

Produktionsproffs kan t.ex. använda det inbyggda XMP-stödet i Adobe-program för att skicka information till flera filformat. The [!DNL Assets] databasen extraherar XMP metadata och använder den för att hantera innehållets livscykel och ger möjlighet att skapa automatiserade arbetsflöden.

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

Till exempel **Skapare** i två oberoende utformade scheman kan betyda den person som skapade resursen eller det kan betyda programmet som skapade resursen (till exempel Adobe Photoshop).

**XMP egenskaper och värden**

XMP kan innehålla egenskaper från ett eller flera av scheman. En vanlig delmängd som används av många Adobe-program kan till exempel vara följande:

* Dublin Core-schema: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP grundläggande schema: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* XMP Rättighetshanteringsschema: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP för mediahantering: `xmpMM:DocumentID`

**Språkalternativ**

XMP ger dig möjlighet att lägga till en `xml:lang` egenskapen till textegenskaper för att ange textens språk.

## XMP till återgivning {#xmp-writeback-to-renditions}

Den här XMP återskrivningsfunktionen i [!DNL Adobe Experience Manager Assets] återger metadataändringarna i återgivningarna av den ursprungliga resursen.
När du ändrar metadata för en resurs från [!DNL Assets] När du överför resursen lagras ändringarna först i metadatanoden i resurshierarkin. Med återskrivningsfunktionen kan du sprida metadataändringarna till alla eller vissa återgivningar av resursen. Funktionen skriver bara tillbaka de metadataegenskaper som använder `jcr` namespace, d.v.s. en egenskap med namnet `dc:title` skrivs tillbaka men egenskapen heter `mytitle` inte.

Tänk dig ett scenario där du ändrar [!UICONTROL Title] egenskap för tillgången i namnet `Classic Leather` till `Nylon`.

![metadata](assets/metadata.png)

I detta fall [!DNL Assets] sparar ändringarna i **[!UICONTROL Title]** -egenskapen i `dc:title` parameter för resursens metadata som lagras i resurshierarkin.

![metadata som lagras i resursnoden i databasen](assets/metadata_stored.png)

>[!IMPORTANT]
>
>Återskrivningsfunktionen är inte aktiverad som standard i [!DNL Assets]. Se hur man [aktivera metadatatillbakaskrivning](#enable-xmp-writeback). MSM för digitala resurser fungerar inte när återkoppling av metadata är aktiverat. Vid tillbakaskrivning avbryts arvet.

### Aktivera XMP {#enable-xmp-writeback}

[!UICONTROL DAM Metadata Writeback] arbetsflödet används för att skriva tillbaka metadata för en resurs. Om du vill aktivera tillbakaskrivning följer du någon av följande tre metoder:

* Använd startprogram.
* Starta manuellt `DAM MetaData Writeback` arbetsflöde.
* Konfigurera arbetsflödet som en del av efterbearbetningen.

Så här använder du Launcher:

1. Som administratör får du åtkomst **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.
1. Välj [!UICONTROL Launcher] som **[!UICONTROL Workflow]** kolumn visas **[!UICONTROL DAM MetaData Writeback]**. Klicka på **[!UICONTROL Properties]** i verktygsfältet.

   ![Välj DAM-metadataåterskrivningsstartaren för att ändra dess egenskaper och aktivera den](assets/launcher-properties-metadata-writeback1.png)

1. Välj **[!UICONTROL Activate]** på **[!UICONTROL Launcher Properties]** sida. Klicka på **[!UICONTROL Save & Close]**.

Om du bara vill tillämpa arbetsflödet på en resurs manuellt en gång använder du [!UICONTROL DAM Metadata Writeback] arbetsflöde från den vänstra listen.

Om du vill använda arbetsflödet på alla överförda resurser lägger du till arbetsflödet i en efterbearbetningsprofil.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

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
