---
title: Hanterare och översättning av flera webbplatser
description: Lär dig hur du återanvänder innehåll i hela projektet och hanterar flerspråkiga webbplatser i AEM.
translation-type: tm+mt
source-git-commit: 4fc4dbe2386d571fa39fd6d10e432bb2fc060da1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Multi Site Manager och Translation {#msm-and-translation}

Adobe Experience Manager inbyggda verktyg för Multi Site Manager och översättning gör det enklare att lokalisera innehållet.

* Med Multi Site Manager (MSM) och dess Live Copy-funktioner kan du använda samma webbplatsinnehåll på flera platser samtidigt som du kan använda olika varianter:
   * [Återanvända innehåll: Multi Site Manager och Live Copy](msm/overview.md)
* Översättning gör att du kan automatisera översättningen av sidinnehåll för att skapa och underhålla flerspråkiga webbplatser:
   * [Översätta innehåll för flerspråkiga webbplatser](translation/overview.md)

Dessa två funktioner kan kombineras för att passa för webbplatser som är både [multinationella och flerspråkiga](#multinational-and-multilingual-sites).

## Flerspråkiga och flerspråkiga platser {#multinational-and-multilingual-sites}

Ni kan effektivt skapa innehåll för multinationella och flerspråkiga webbplatser genom att kombinera Multi Site Manager och arbetsflödet för översättning.

Vanligtvis skapar du en överordnad webbplats på ett språk och för ett visst land, och använder sedan innehållet som bas för de andra webbplatserna, med översättning där det behövs.

1. [Översätt ](translation/overview.md) den överordnad webbplatsen till olika språk.
1. Använd [Multi Site Manager](msm/overview.md) för att:
   1. Återanvänd innehåll från den överordnad webbplatsen och dess översättningar för att skapa webbplatser för andra länder och kulturer.
   1. Om det behövs frigör du element i Live-kopior för att lägga till lokaliseringsinformation.

>[!TIP]
>
>Begränsa användningen av Multi Site Manager till innehåll på ett språk.
>
>Använd t.ex. den engelska överordnad för att skapa den engelska versionen av sidor för USA, Kanada, Storbritannien osv. och använder den franska överordnad för att skapa den franska versionen av sidor för Frankrike, Schweiz, Kanada osv.

I följande diagram visas hur huvudbegreppen överlappar (men inte alla nivåer/element som berörs):

![Översikt över lokalisering](assets/localization-overview.png)

I detta fall, och på liknande sätt, hanterar inte MSM de olika språkversionerna som sådana.

* [MSM ](msm/overview.md) hanterar distributionen av översatt innehåll från en plan (dvs. en global överordnad) till Live-kopior (dvs. de lokala platserna), inom ett språks gränser.
* Integreringsfunktionerna i [translation](translation/overview.md) i AEM, tillsammans med översättningshanteringstjänster från tredje part, hanterar språken och översätter innehåll till dessa olika språk.

För mer avancerade användningsområden kan MSM användas även av flerspråkiga mallsidor.

>[!TIP]
>
>För alla användningsfall rekommenderas följande metodtips:
>
>* [Bästa praxis för MSM](msm/best-practices.md)
>* [Best Practices for Translation](translation/best-practices.md)

