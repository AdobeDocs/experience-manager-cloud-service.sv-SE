---
title: Kända fel
description: Kända problem med Adobe Experience Manager as a Cloud Service
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Kända fel {#known-issues}

I den här artikeln listas kända problem med [!DNL Adobe Experience Manager] som [!DNL Cloud Service] erbjuder. Listan revideras och uppdateras varje gång [!DNL Experience Manager].

[Kontakta support](https://experienceleague.adobe.com/?lang=en&amp;support-solution=Experience+Manager#support) för mer information om kända fel.

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

Vissa kända fel i [!DNL Sites] är:

* I GraphQL IDE kan du [hantera cacheminnet för dina beständiga frågor](/help/headless/graphql-api/graphiql-ide.md##managing-cache).
   * När du sparar första gången anges värdena för rubrikerna till `0` (i stället för standardvärdena) - om användaren inte har ändrat dessa värden i dialogrutan.
   * Värdena sparas korrekt när de sparas därefter.
   * Därför måste användaren spara rubrikerna två gånger.

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Vissa kända fel i [!DNL Assets] är:

* **Hämta**: Om du hämtar en tom mapp [!DNL Experience Manager] förmedlar ett meddelande om att ett ZIP-arkiv har skapats, men arkivet har inte skapats.

* **Metadataschema**: Widget för tillgångsklassificering som används för att orsaka JSP-kompileringsfel. Den togs bort från metadataschemat. <!-- CQ-4282865, CQ-4284633 -->

Se även [noterbara ändringar i [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md).

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [Större förändringar i [!DNL Experience Manager]](aem-cloud-changes.md)
>* [Föråldrade och borttagna funktioner](deprecated-removed-features.md)
>* [Versionsinformation](home.md)

