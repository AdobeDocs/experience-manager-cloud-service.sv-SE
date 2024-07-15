---
title: Headless and Headless in AEM
description: AEM kan implementeras i en headful och headless-modell, men valet är inte binärt. AEM erbjuder flexibiliteten att utnyttja fördelarna med båda modellerna i ett och samma projekt.
exl-id: 709850ca-7757-47ab-9625-f411121cde2c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Headless and Headless in AEM {#headful-headless}

Adobe Experience Manager-projekt kan implementeras i både headful och headless-modeller, men valet är inte binärt. AEM erbjuder flexibiliteten att utnyttja fördelarna med båda modellerna i ett och samma projekt. Det här dokumentet innehåller en översikt över de olika modellerna och beskriver SPA integrationsnivåer.

## Ökning {#overview}

AEM har kraftfulla verktyg för att hantera både framtagning av innehåll och distribution av det på en och samma plattform. Detta är en traditionell&quot;headful&quot; modell för innehållshantering, där innehållsförfattare och utvecklare arbetar på samma plattform för att leverera upplevelserna till innehållskunderna.

AEM kan också användas för att enkelt hantera innehåll, vilket gör att presentationen och leveransen av innehållet kan hanteras av en annan plattform. Det här är den&quot;headless&quot; modellen för innehållshantering, där innehållsförfattare och utvecklare arbetar på olika plattformar för att leverera upplevelser till innehållskunderna.

Men detta behöver inte vara ett binärt val. AEM erbjuder oöverträffad flexibilitet och du kan utnyttja fördelarna med båda modellerna i ditt projekt.

![AEM implementeringsmodeller](/help/headless/assets/aem-implementation-models.png)

I en modell med headful eller full stack hanteras innehållet i AEM och AEM komponenter som baseras på Java, HTL och så vidare används för att återge innehållet för användarupplevelsen. I den här modellen skapas innehållet, formateras, presenteras och distribueras allt i AEM.

I en headless-modell hanteras innehållet i AEM, men levereras via API:er som REST och GraphQL till ett annat system för att återge innehållet för användarupplevelsen. I den här modellen skapas innehåll i AEM, men formateras, presenteras och distribueras allt på en annan plattform.

Single Page Applications (SPA) är ofta målet för innehåll som levereras headless av AEM. Dessa SPA behöver dock inte vara helt externa för AEM. AEM låter dig avgöra i vilken grad dina SPA är integrerade i AEM. Låt oss ta ett exempel.

## Exempel på Web Shop {#web-shop-example}

Säg att du har en befintlig webbutik för ditt företag som SPA. Där finns all produktinformation och alla bilder. Sedan introducerar ni AEM för att stärka era marknadsföringssatsningar, som reklamwebbplatser, bloggar och kampanjinnehåll. Hur integrerar man de två? AEM har flera alternativ:

* **Tillåt att systemen fungerar oberoende.**
* **Tillhandahåll webbbutiken med begränsat innehåll från AEM via GraphQL.**-innehåll kan skapas av författare i AEM, men bara visas via SPA.
* **Bädda in SPA i AEM.**-innehåll kan skapas av författare i AEM och visas i AEM i webbutiken, men inte ändras.
* **Bädda in SPA i AEM och aktivera redigerbara punkter.**-innehåll kan skapas av författare i AEM och visas i AEM i webbutikens sammanhang, och författarna har begränsad möjlighet att ändra innehållet i webbutikens SPA i AEM.
* **Bädda in webbutikens SPA i AEM och aktivera hela zoner för redigering.**-innehåll kan skapas av författare i AEM och visas i AEM i webbutikens sammanhang, och författarna har begränsad möjlighet att ändra innehållet i webbutikens SPA i AEM.

I nästa avsnitt beskrivs dessa integreringsnivåer mer ingående.

>[!NOTE]
>
>Du kan förstås även implementera om SPA som en fullt fungerande AEM SPA [med AEM SPA Editor-ramverket](/help/implementing/developing/hybrid/introduction.md). Om du redan har AEM och vill skapa en webshop eller någon annan SPA, rekommenderas den här metoden, men den ligger utanför dokumentets omfång.

## SPA integreringsnivåer {#integration-levels}

SPA integrering faller på ett spektrum av fyra nivåer i AEM.

* **Nivå 0: Ingen integrering**
   * SPA och AEM finns separat och utbyter ingen information.
   * Innehållet skapas, hanteras och levereras oberoende av varandra i två olika system.
* **Nivå 1: Integrering av innehållsfragment**
   * [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) används i AEM för att skapa och hantera begränsat innehåll för SPA.
   * SPA hämtar det här innehållet via AEM [GraphQL API](/help/headless/graphql-api/content-fragments.md).
   * Visst innehåll hanteras i AEM och andra i ett externt system.
   * Innehåll kan bara visas i SPA.
* **Nivå 2: Bädda in SPA i AEM**
   * [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) används i AEM för att skapa och hantera innehåll för SPA.
   * SPA hämtar det här innehållet via AEM [GraphQL API](/help/headless/graphql-api/content-fragments.md).
   * Visst innehåll hanteras i AEM och andra i ett externt system.
   * Innehåll kan visas i sitt sammanhang i AEM.
   * Begränsat innehåll kan redigeras i AEM.
* **Nivå 3: Bädda in och aktivera SPA fullständigt i AEM**
   * [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) används i AEM för att skapa och hantera innehåll för SPA.
   * SPA hämtar det här innehållet via AEM [GraphQL API](/help/headless/graphql-api/content-fragments.md).
   * Innehåll kan visas i sitt sammanhang i AEM.
   * Det mesta innehållet kan redigeras i AEM.

Nivå 1 är ett exempel på en typisk headless-implementering. Innehållsförfattare kan dock bara visa sitt innehåll i sitt sammanhang i SPA. AEM är bara ett redigeringsverktyg.

Fördelen med och flexibiliteten i AEM blir tydlig med nivåerna 2 och 3 samtidigt som fördelarna med SPA bibehålls. Innehållsförfattare kan skapa sitt innehåll i AEM, men kan också se det i sitt sammanhang i AEM. SPA får möjlighet att skriva i AEM, men kan ändå levereras som en SPA.

## Implementera integreringsnivåer {#implementing}

Det finns olika verktyg i AEM beroende på vilken integrationsnivå du väljer. Varje nivå bygger på de verktyg som använts tidigare. Följande lista länkar till relevanta resurser.

* **Nivå 1:** Innehållsfragment och det [AEM headless-ramverket](/help/headless/introduction.md) kan användas för att leverera AEM innehåll till SPA.
* **Nivå 2:** Förutom nivå ett:
   * [RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md) kan användas för att bädda in det externa SPA i AEM där AEM innehåll kan visas i sitt sammanhang.
   * Vissa punkter på SPA kan också aktiveras för att [tillåta begränsad redigering i AEM](/help/implementing/developing/hybrid/editing-external-spa.md).
* **Nivå 3:** Förutom nivå två:
   * Hela zoner i SPA kan aktiveras för omfattande redigering i AEM.
