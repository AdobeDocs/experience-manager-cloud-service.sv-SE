---
title: Redigera eller lägga till metadata
description: Läs mer om metadata för resurser i [!DNL Experience Manager Assets] olika sätt att redigera metadata för resurser.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 2%

---

# Redigera eller lägga till metadata {#how-to-edit-or-add-metadata}

Metadata är ytterligare information om resursen som kan sökas igenom. Den extraheras automatiskt när du överför en bild. Du kan redigera befintliga metadata eller lägga till nya metadataegenskaper i befintliga fält (till exempel när ett metadatafält är tomt).

Eftersom företag behöver kontrollerade och tillförlitliga metadata-språk, [!DNL Experience Manager Assets] tillåter inte ad hoc-tillägg av nya metadataegenskaper. Även om författare inte kan lägga till nya metadatafält för resurser kan utvecklare göra det. Se [Skapar ny metadataegenskap för resurser](meta-edit.md#editing-metadata-schema).

## Redigera metadata för en resurs {#editing-metadata-for-an-asset}

Så här redigerar du metadata:

1. Gör något av följande:

   * Välj resursen i resursgränssnittet och välj **[!UICONTROL View Properties]** -ikonen i verktygsfältet.
   * Välj miniatyrbilden för resursen **[!UICONTROL View Properties]** snabbåtgärd.
   * Välj på resurssidan **[!UICONTROL View Properties]** i verktygsfältet.

   Resurssidan visar resursens metadata. Dessa metadata extraherades automatiskt när de överfördes (överfördes) till Experience Manager Assets.

1. Redigera metadata under de olika flikarna efter behov och markera **[!UICONTROL Save]** i verktygsfältet för att spara ändringarna. Välj **[!UICONTROL Close]** för att återgå till webbgränssnittet Resurser.

   >[!NOTE]
   >
   >Om ett textfält är tomt finns det ingen befintlig metadatauppsättning. Du kan ange ett värde i fältet och spara det för att lägga till metadataegenskapen.

Alla ändringar av metadata för en resurs skrivs tillbaka till den ursprungliga binärfilen som en del av dess XMP data. Detta görs via Experience Manager metadata-återskrivningsarbetsflöde. Ändringar som gjorts i befintliga egenskaper (till exempel `dc:title`) är överskrivna och nyligen skapade egenskaper (inklusive anpassade egenskaper som `cq:tags`) läggs till tillsammans med schemat.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Redigerar metadataschema {#editing-metadata-schema}

Mer information om hur du redigerar metadataschemat finns i [Redigera metadata-schemaformulär](metadata-schemas.md#edit-metadata-schema-forms).

## Registrera ett anpassat namnutrymme i Experience Manager {#registering-a-custom-namespace-within-aem}

Du kan lägga till egna namnutrymmen i Experience Manager. Precis som det finns fördefinierade namnutrymmen som cq, jcr och sling kan du ha ett namnutrymme för databasens metadata och XML-bearbetning.

1. Gå till administrationssidan för nodtypen *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Välj **[!UICONTROL Namespaces]** överst på sidan. Namnutrymmesadministrationssidan visas i ett fönster.

1. Om du vill lägga till ett namnutrymme väljer du **[!UICONTROL New]** längst ned.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen (ange id:t i form av en URI och ett associerat prefix för id:t) och välj **[!UICONTROL Save]**.

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
