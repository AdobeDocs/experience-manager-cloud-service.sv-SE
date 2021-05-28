---
title: Riktlinjer för Java API
description: AEM bygger på en programhög med öppen källkod som visar många Java API:er för användning.
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Riktlinjer för Java API {#java-api-guidelines}

Adobe Experience Manager (AEM) bygger på en omfattande programstack med öppen källkod som visar många Java API:er för användning under utveckling.

AEM bygger på följande fyra primära Java API-uppsättningar i fallande prioritetsordning.

1. **[Adobe Experience Manager (AEM)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/index.html)**  - produktabstraktioner som sidor, resurser, arbetsflöden osv.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST och resursbaserade abstraktioner som resurser, värdekartor och HTTP-begäranden.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** - Data- och innehållsavvikelser som nod, egenskaper och sessioner.
1. **[OSGi (Apache Felix)](https://felix.apache.org)** - OSGi-programbehållarabstreringar som tjänster och OSGi-komponenter.

Om ett API tillhandahålls av AEM bör du föredra det framför Sling, JCR och OSGi. Om AEM inte har något API bör du välja Sling framför JCR och OSGi.

Mer information om de här riktlinjerna finns i dokumentet [Förstå bästa praxis för Java API.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
