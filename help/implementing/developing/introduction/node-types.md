---
title: AEM nodtyper
description: AEM baseras på Sling och använder en JCR-databas med nodtyper som erbjuds av båda, men AEM tillhandahåller också ett urval av sina egna nodtyper.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# AEM nodtyper {#aem-node-types}

Eftersom AEM baseras på Sling och använder en JCR-databas är de nodtyper som erbjuds av båda dessa standarder tillgängliga för användning i AEM:

* [JCR-nodtyper](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling Node Types](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Förutom dessa. AEM innehåller ett antal anpassade nodtyper. För den senaste listan med alla associerade egenskaper [använd CRXDE](/help/implementing/developing/tools/crxde.md) om du vill bläddra i följande sökväg i AEM:

`/jcr:system/jcr:nodeTypes`
