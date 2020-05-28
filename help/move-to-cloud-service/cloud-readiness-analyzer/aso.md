---
title: AEM - systemöversikt
description: AEM - systemöversikt
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%

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

### Möjliga lösningar  {#possible-solutions}

Ej relevant.
