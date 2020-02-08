---
title: Kända fel
description: Versionsinformation som är specifik för Kända problem med Adobe Experience Manager som en molntjänst
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Kända fel {#known-issues}

I den här artikeln listas kända problem i Adobe Experience Manager som ett molnerbjudande. Listan revideras och uppdateras med varje kontinuerlig version av Experience Manager.

[Kontakta supporten](https://helpx.adobe.com/support/experience-manager.html) om du vill ha mer information om kända fel.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Resurser {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Några kända fel är:

* **Metadataschema**: Widget för tillgångsklassificering kan orsaka JSP-kompileringsfel. Du kan lösa problemet genom att ta bort resursklassificeringskomponenten från metadataschemat. <!-- CQ-4282865 -->

Vissa begränsningar för Assets-funktionen är:

* Med AEM Assets som molntjänst fungerar funktionen för anslutna resurser när AEM 6.5 Sites distribueras i AMS.

### Kommande Assets-funktioner {#upcoming-assets-capabilities}

Några av funktionerna i Adobe Experience Manager Assets som är beroende av grundfunktionerna, som ännu inte är tillgängliga i Experience Manager som en distributionsarkitektur för molntjänster, förväntas aktiveras i ett senare skede:

* Publicering till varumärkesportalen är inte aktiverat för närvarande. Du kan utöka och distribuera implementeringen av [Resursdelningskommentarer](https://adobe-marketing-cloud.github.io/asset-share-commons/) för användningsfall för resursdistribution.
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

