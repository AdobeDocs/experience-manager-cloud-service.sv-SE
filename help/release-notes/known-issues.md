---
title: Kända fel
description: Versionsinformation om kända problem med Adobe Experience Manager som Cloud Service
translation-type: tm+mt
source-git-commit: 165dc4af656ce1bc431d2f921775ebda4cf4de9f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---


# Known issues {#known-issues}

I den här artikeln listas de kända problemen med Adobe Experience Manager som en Cloud Service. Förteckningen revideras och uppdateras för varje kontinuerlig version av Experience Manager.

[Kontakta supporten](https://helpx.adobe.com/support/experience-manager.html) om du vill ha mer information om kända fel.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Några kända fel är:

* **Metadataschema**: Widget för tillgångsklassificering som används för att orsaka JSP-kompileringsfel. Den togs bort från metadataschemat. <!-- CQ-4282865, CQ-4284633 -->

### Kommande Assets-funktioner {#upcoming-assets-capabilities}

Några funktioner i Adobe Experience Manager Assets som bygger på grundfunktioner, som ännu inte är tillgängliga i Experience Manager som arkitektur för driftsättning av Cloud Service, förväntas aktiveras i ett senare skede:

* Funktioner som inte är aktiverade i det här skedet på grund av beroendet av API:er i Commerce Integration Framework:
   * Arbetsflödesmodeller för Photoshop.
   * Fliken Produktinformation i användargränssnittet för resursegenskaper har inte fyllts i.
* Funktioner som inte är aktiverade i det här skedet på grund av beroendet av integrering med InDesign Server:
   * Resursmallar och tillgångskataloger.
   * Flersidig förhandsgranskning av Adobe InDesign-filer.

>[!MORELIKETHIS]
>
>* [Större förändringar i AEM](aem-cloud-changes.md)
>* [Föråldrade och borttagna funktioner](deprecated-removed-features.md)
>* [Versionsinformation](home.md)

