---
title: AEM - systemöversikt
description: AEM - systemöversikt
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# AEM - systemöversikt {#aem-system}

Den här sidan beskriver Adobe Experience Manager (AEM) - systemöversikt.

## Bakgrund {#background}

Det här mönstret används för att identifiera allmän information som ger en översikt över AEM-systemet. Informationen kan innehålla bl.a. följande:

AEM-versionAEM-produkter som används (Sites, Assets, Forms, osv.)Antal noder (sidor, resurser osv.)

## Mönsterdata {#pattern-data}

Följande objekt ingår i JSON-representationen av mönstret:

* **item.message**: refererar till mönstrets meddelande.
* **item.context**: hänvisar till ytterligare information om översiktsinformationen:
   * *typ*: Typ av kontextdata, antingen &quot;aem.version&quot;, &quot;aem.product&quot; eller &quot;node.count&quot;.
   * *data*: Ett JSON-objekt som innehåller de data som motsvarar typen: &quot;version&quot; (sträng), &quot;product&quot; (sträng) eller &quot;count&quot; (heltal).

### Möjliga konsekvenser och risker {#possible-implications}

Ej relevant.

### Möjliga lösningar {#possible-solutions}

Ej relevant.
