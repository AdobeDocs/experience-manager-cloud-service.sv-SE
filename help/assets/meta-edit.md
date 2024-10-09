---
title: Redigera eller lägga till metadata
description: Lär dig mer om metadata för resurser i  [!DNL Experience Manager Assets] ett sätt att redigera metadata för resurser.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Redigera eller lägga till metadata {#how-to-edit-or-add-metadata}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Metadata är ytterligare information om resursen som kan sökas igenom. Den extraheras automatiskt när du överför en bild. Du kan redigera befintliga metadata eller lägga till nya metadataegenskaper i befintliga fält (till exempel när ett metadatafält är tomt).

Eftersom företag behöver kontrollerade och tillförlitliga metadata-ordlistor tillåter inte [!DNL Experience Manager Assets] att nya metadataegenskaper läggs till på begäran. Även om författare inte kan lägga till nya metadatafält för resurser kan utvecklare göra det. Se [Skapa ny metadataegenskap för Assets](meta-edit.md#editing-metadata-schema).

## Redigera metadata för en resurs {#editing-metadata-for-an-asset}

Så här redigerar du metadata:

1. Gör något av följande:

   * I Assets-gränssnittet markerar du resursen och väljer ikonen **[!UICONTROL View Properties]** i verktygsfältet.
   * Välj snabbåtgärden **[!UICONTROL View Properties]** från miniatyrbilden av resursen.
   * Välj **[!UICONTROL View Properties]** i verktygsfältet på resurssidan.

   Resurssidan visar resursens metadata. Dessa metadata extraherades automatiskt när de överfördes (överfördes) till Experience Manager Assets.

1. Redigera metadata under de olika flikarna efter behov och när du är klar väljer du **[!UICONTROL Save]** i verktygsfältet för att spara ändringarna. Välj **[!UICONTROL Close]** om du vill återgå till Assets webbgränssnitt.

   >[!NOTE]
   >
   >Om ett textfält är tomt finns det ingen befintlig metadatauppsättning. Du kan ange ett värde i fältet och spara det för att lägga till metadataegenskapen.

Alla ändringar av metadata för en resurs skrivs tillbaka till den ursprungliga binärfilen som en del av dess XMP data. Detta görs via Experience Manager metadata-återskrivningsarbetsflöde. Ändringar som görs i befintliga egenskaper (till exempel `dc:title`) skrivs över och skapade egenskaper (inklusive anpassade egenskaper som `cq:tags`) läggs ihop med schemat.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Redigerar metadataschema {#editing-metadata-schema}

Mer information om hur du redigerar metadataschemat finns i [Redigera metadataschemaformulär](metadata-schemas.md#edit-metadata-schema-forms).

## Registrera ett anpassat namnutrymme i Experience Manager {#registering-a-custom-namespace-within-aem}

Du kan lägga till egna namnutrymmen i Experience Manager. Precis som det finns fördefinierade namnutrymmen som cq, jcr och sling kan du ha ett namnutrymme för databasens metadata och XML-bearbetning.

1. Gå till administrationssidan för nodtypen *https://&lt;värd>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Välj **[!UICONTROL Namespaces]** överst på sidan. Namnutrymmesadministrationssidan visas i ett fönster.

1. Om du vill lägga till ett namnutrymme väljer du **[!UICONTROL New]** längst ned.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen (ange id:t i form av en URI och ett associerat prefix för id:t) och välj **[!UICONTROL Save]**.

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
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
