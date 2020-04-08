---
title: Kända fel
description: Versionsinformation som är specifik för Kända problem med Adobe Experience Manager som en molntjänst
translation-type: tm+mt
source-git-commit: ce82d7c9ca1fd8fe3d6f61213cfee360fc6496fd

---


# Known issues {#known-issues}

I den här artikeln listas kända problem i Adobe Experience Manager som ett molnerbjudande. Listan revideras och uppdateras med varje kontinuerlig version av Experience Manager.

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

Några av funktionerna i Adobe Experience Manager Assets som är beroende av grundfunktionerna, som ännu inte är tillgängliga i Experience Manager som en distributionsarkitektur för molntjänster, förväntas aktiveras i ett senare skede:

* Förbättrade smarta taggningsfunktioner som utnyttjar AI-tjänster i Adobe I/O är inte tillgängliga just nu.
* Funktioner som inte är aktiverade i det här skedet på grund av beroendet av API:er i Commerce Integration Framework:
   * Arbetsflödesmodeller för Photoshop.
   * Fliken Produktinformation i användargränssnittet för resursegenskaper har inte fyllts i.
* Funktioner som inte är aktiverade i det här skedet på grund av beroendet av InDesign Server-integrering:
   * Resursmallar och tillgångskataloger.
   * Flersidig förhandsgranskning av InDesign-filer.

>[!MORELIKETHIS]
>
>* [Större förändringar i AEM](aem-cloud-changes.md)
>* [Föråldrade och borttagna funktioner](deprecated-removed-features.md)
>* [Versionsinformation](home.md)

