---
title: 'Introduktion till sandlådeprogram '
description: 'Introduktion till sandlådeprogram '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introduktion till sandlådeprogram {#sandbox-programs}

## Introduktion {#introduction}

Ett sandlådeprogram är en av de två typer av program som finns i AEM Cloud Service, och den andra är ett produktionsprogram.

En sandlåda skapas vanligtvis för utbildning, löpande demonstrationer, aktivering eller korrektur av begrepp (POC). De är inte avsedda att bära livstrafik. De omfattas inte av [AEM som en Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Miljöerna som skapas i en sandlåda är inte konfigurerade för automatisk skalning. Därför är dessa miljöer inte lämpliga för prestanda- eller belastningstestning.

Sandlådeprogram innehåller Sites and Assets och är automatiskt ifyllda med en Git-databas, en utvecklingsmiljö och en icke-produktionsprocess.  Git-databasen innehåller ett exempelprojekt baserat på AEM projekttyp.

Mer information om programtyperna finns i [Förstå program och programtyper](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md).

### Attribut för sandlådeprogram {#attributes-sandbox}

Sandlådeprogram har följande attribut:

1. **Skapa program:** I sandlådeprogrammet skapas automatiskt:
   * konfiguration av projekt med exempelkod och innehåll
   * utvecklingsmiljö
   * Skapande av icke-produktionsförlopp för distribution till utvecklingsmiljö (överordnad filial distribuering till utvecklingsmiljö)

1. **Lösningar:** Sandlådeprogram innehåller AEM Sites och Assets.

1. **AEM:** AEM uppdateringar kan användas manuellt i miljöer i sandlådeprogram och skickas inte automatiskt.
Mer information finns i [AEM uppdateringar av sandlådemiljöer](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox).

1. **Viloläge:** miljöer i ett sandlådeprogram försätts automatiskt i viloläge om ingen aktivitet identifieras under en viss tid. Vilolägen miljöer kan avaktiveras manuellt.
Mer information finns i [Viloläge och Viloläge i sandlådemiljöer](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md).