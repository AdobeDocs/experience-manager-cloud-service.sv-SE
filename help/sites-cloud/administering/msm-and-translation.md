---
title: Hanterare och översättning av flera webbplatser
description: Lär dig hur du återanvänder ditt innehåll i ditt projekt och hanterar flerspråkiga webbplatser i AEM.
feature: Administering
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
solution: Experience Manager Sites
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Hanterare och översättning av flera webbplatser {#msm-and-translation}

Adobe Experience Manager inbyggda verktyg för Multi Site Manager och översättning gör det enklare att lokalisera innehållet.

* Med Multi Site Manager (MSM) och dess Live Copy-funktioner kan du använda samma webbplatsinnehåll på flera platser samtidigt som du kan använda olika varianter:
   * [Återanvända innehåll: Multi Site Manager och Live Copy](msm/overview.md)
* Med översättningen kan du automatisera översättningen av sidinnehåll för att skapa och underhålla flerspråkiga webbplatser:
   * [Översätta innehåll för flerspråkiga webbplatser](translation/overview.md)

Dessa två funktioner kan kombineras för att passa för webbplatser som är både [multinationella och flerspråkiga](#multinational-and-multilingual-sites).

>[!TIP]
>
>Om du inte har börjat översätta innehåll tidigare läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md). Det är en guidad väg genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg. Perfekt om du inte har någon erfarenhet av AEM eller översättning.

## Flerspråkiga och flerspråkiga webbplatser {#multinational-and-multilingual-sites}

Ni kan effektivt skapa innehåll för multinationella och flerspråkiga webbplatser genom att kombinera Multi Site Manager och arbetsflödet för översättning.

Vanligtvis skapar du en primär webbplats på ett språk och för ett visst land, och använder sedan innehållet som bas för de andra webbplatserna, med översättning där det behövs.

1. [Översätt](translation/overview.md) den primära webbplatsen till olika språk.
1. Använd [Multi Site Manager](msm/overview.md) för att:
   1. Återanvänd innehåll från den primära webbplatsen och dess översättningar för att skapa webbplatser för andra länder och kulturer.
   1. Om det behövs frigör du element i Live-kopior för att lägga till lokaliseringsinformation.

>[!TIP]
>
>Begränsa användningen av Multi Site Manager till innehåll på ett språk.
>
>Använd till exempel den primära engelska för att skapa den engelska versionen av sidorna för USA, Kanada och Storbritannien. Använd sedan den primära franska versionen för att skapa den franska versionen av sidor för Frankrike, Schweiz, Kanada och så vidare.

I följande diagram visas hur huvudbegreppen överlappar (men inte alla nivåer/element som berörs):

![Lokalisering - översikt](assets/localization-overview.png)

I det här scenariot, och i jämförbara fall, hanterar inte MSM de olika språkversionerna som sådana.

* [MSM](msm/overview.md) hanterar distributionen av översatt innehåll från en plan (d.v.s. en primär global) till Live-kopior (d.v.s. lokala platser) inom ett språks gränser.
* Integreringsfunktionerna i [translation](translation/overview.md) i AEM, med översättningshanteringstjänster från tredje part, hanterar språken och översätter innehåll till dessa olika språk.

För mer avancerade användningsområden kan MSM även användas på andra primära språk.

>[!TIP]
>
>För alla användningsfall rekommenderas följande metodtips:
>
>* [Bästa praxis för MSM](msm/best-practices.md)
>* [Bästa metoder för översättning](translation/best-practices.md)
