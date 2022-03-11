---
title: Hanterare och översättning av flera webbplatser
description: Lär dig hur du återanvänder innehåll i hela projektet och hanterar flerspråkiga webbplatser i AEM.
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Hanterare och översättning av flera webbplatser {#msm-and-translation}

Adobe Experience Manager inbyggda verktyg för Multi Site Manager och översättning gör det enklare att lokalisera innehållet.

* Med Multi Site Manager (MSM) och dess Live Copy-funktioner kan du använda samma webbplatsinnehåll på flera platser samtidigt som du kan använda olika varianter:
   * [Återanvända innehåll: Multi Site Manager och Live Copy](msm/overview.md)
* Översättning gör att du kan automatisera översättningen av sidinnehåll för att skapa och underhålla flerspråkiga webbplatser:
   * [Översätta innehåll för flerspråkiga webbplatser](translation/overview.md)

Dessa två funktioner kan kombineras för att passa för webbplatser som båda [multinationella och flerspråkiga](#multinational-and-multilingual-sites).

>[!TIP]
>
>Om du är nybörjare på att översätta innehåll kan du läsa [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

## Flerspråkiga och flerspråkiga webbplatser {#multinational-and-multilingual-sites}

Ni kan effektivt skapa innehåll för multinationella och flerspråkiga webbplatser genom att kombinera Multi Site Manager och arbetsflödet för översättning.

Vanligtvis skapar du en överordnad webbplats på ett språk och för ett visst land, och använder sedan innehållet som bas för de andra webbplatserna, med översättning där det behövs.

1. [Översätt](translation/overview.md) den överordnad webbplatsen till olika språk.
1. Använd [Multi Site Manager](msm/overview.md) till:
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

* [MSM](msm/overview.md) hanterar distributionen av översatt innehåll från en ritning (dvs. en global överordnad) till Live-kopior (dvs. lokala platser), inom ett språks gränser.
* The [översättning](translation/overview.md) integreringsfunktionerna i AEM, tillsammans med översättningshanteringstjänster från tredje part, hanterar språken och översätter innehåll till dessa olika språk.

För mer avancerade användningsområden kan MSM användas även av flerspråkiga mallsidor.

>[!TIP]
>
>För alla användningsfall rekommenderas följande metodtips:
>
>* [Bästa praxis för MSM](msm/best-practices.md)
>* [Best Practices for Translation](translation/best-practices.md)

