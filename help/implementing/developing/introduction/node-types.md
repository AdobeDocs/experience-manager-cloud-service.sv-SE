---
title: AEM
description: AEM baseras på Sling och använder en JCR-databas med nodtyper som erbjuds av båda, men AEM tillhandahåller också ett urval av sina egna nodtyper.
translation-type: tm+mt
source-git-commit: 020cebfa714c098f032df963b7105503c741e748
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# AEM nodtyper {#aem-node-types}

Eftersom AEM baseras på Sling och använder en JCR-databas är de nodtyper som erbjuds av båda dessa standarder tillgängliga för användning i AEM:

* [JCR-nodtyper](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling Node Types](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Förutom dessa. AEM innehåller ett antal anpassade nodtyper. Om du vill visa den senaste listan med alla associerade egenskaper använder du [CRXDE](/help/implementing/developing/tools/crxde.md) och bläddrar till följande sökväg i AEM:

`/jcr:system/jcr:nodeTypes`
