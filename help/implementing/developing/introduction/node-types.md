---
title: AEM-nodtyper
description: AEM är baserat på Sling och använder en JCR-databas med nodtyper som erbjuds av båda, men AEM har också ett urval av sina egna nodtyper.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# AEM-nodtyper {#aem-node-types}

Eftersom AEM baseras på Sling och använder en JCR-databas är de nodtyper som erbjuds av båda dessa standarder tillgängliga för användning i AEM:

* [JCR-nodtyper](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Dela nodtyper](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Förutom dessa. AEM har ett antal anpassade nodtyper. [Använd CRXDE](/help/implementing/developing/tools/crxde.md) för att bläddra i följande sökväg i AEM-databasen för den senaste listan med alla associerade egenskaper:

`/jcr:system/jcr:nodeTypes`
