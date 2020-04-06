---
title: AEM - systemöversikt
description: AEM - systemöversikt
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# AEM - systemöversikt {#aem-system}

På den här sidan beskrivs AEM som en molntjänst som ger nya funktioner med en arkitektur som är en betydande förbättring jämfört med tidigare AEM-versioner. Att uppgradera till den nya arkitekturen kräver stora ansträngningar.

## Beskrivning {#background}

ACRA-metamönstret används för att identifiera flera problem som rör uppgraderingar till AEM som en molntjänst. Det stöder flera typer av rådgivande information genom en kombination av mönstrets *referenspunkter* och&quot;referencedBy&quot;-värden och dess *context* -objekt. Typvärdet ** i *kontextobjektet* avgör vilket fel som har upptäckts.

De beredskapsfrågor som ingår i ACRA-mönstret förväntas ha relativt få instanser som ger råd. Det finns andra beredskapsproblem relaterade till AEM som en molntjänst som kan ha många instanser som behöver åtgärdas och dessa får sin egen mönsterkod. (Se Gränssnitt och URL.)

## Mönsterdata {#pattern-data}

Följande objekt ingår i JSON-representationen av mönstret:

* **item.message**: Typ av beredskapsproblem. (Se nedan.)
* **data**: Ett JSON-objekt som innehåller de data som motsvarar typen.

### Möjliga konsekvenser och risker {#possible-implications}

TBD

### Möjliga lösningar {#possible-solutions}

TBD
