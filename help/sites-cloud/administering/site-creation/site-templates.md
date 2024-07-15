---
title: Webbplatsmallar
description: Lär dig hur AEM webbplatsmallar kan användas för att fördefiniera webbplatsstrukturen och det ursprungliga innehållet så att du snabbt kan skapa webbplatser.
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Webbplatsmallar {#site-templates}

Lär dig hur AEM webbplatsmallar kan användas för att fördefiniera webbplatsstrukturen och det ursprungliga innehållet så att du snabbt kan skapa webbplatser.

## Ökning {#overview}

Det är bekvämt att ha fördefinierade strukturer tillgängliga för att snabbt kunna driftsätta en ny webbplats baserat på en uppsättning befintliga standarder. Webbplatsmallar är ett sätt att kombinera grundläggande webbplatsinnehåll i ett bekvämt och återanvändbart paket.

Webbplatsmallar innehåller i allmänhet information om baswebbplatsinnehåll och struktur- och webbplatsformat, så kallat [webbplatstemat](site-themes.md), för att snabbt komma igång med en ny webbplats. Administratörer väljer en webbplatsmall som webbplatsen [ ska baseras på när webbplatsen skapas.](create-site.md)

Mallarna är kraftfulla eftersom de kan återanvändas och anpassas. Och eftersom du kan ha flera mallar tillgängliga i AEM kan du skapa olika webbplatser som passar olika affärsbehov.

>[!NOTE]
>
>AEM webbplatsmallar ska inte blandas ihop med [sidmallar](/help/sites-cloud/authoring/sites-console/templates.md). Platsmallar definierar den övergripande strukturen för en plats. En sidmall definierar strukturen och det ursprungliga innehållet för en enskild sida.
>
>AEM webbplatsmallar ska inte blandas ihop med [AEM webbplatsteman](site-themes.md). AEM webbplatsteman innehåller bara formatinformation för en AEM. AEM webbplatsmallar definierar webbplatsens struktur och ursprungliga innehåll och innehåller ett AEM webbplatstema som tillåter [snabb webbplatsgenerering](create-site.md).

## Lägga till en platsmall i AEM {#adding}

Du kan lägga till flera mallar i AEM, som sedan kan användas för att [skapa webbplatser](create-site.md).

1. Logga in i AEM redigeringsmiljö och navigera till webbplatskonsolen

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Välj **Skapa** längst upp till höger på skärmen och välj **Plats från mall** på den nedrullningsbara menyn.

   ![Skapa en plats från en mall](../assets/create-site-from-template.png)

1. I guiden Skapa plats väljer du **Importera** längst upp i den vänstra kolumnen.

   ![Guiden Skapa webbplats](../assets/site-creation-wizard.png)

1. Leta reda på mallen som du vill använda i filläsaren och välj **Överför**.

1. När den har överförts visas den i listan med tillgängliga mallar.

Mallen har överförts och kan användas för att [skapa nya webbplatser](create-site.md).

När du väljer en befintlig mall visas information om mallen i den högra kolumnen.

![Välj en mall](../assets/select-site-template.png)

## Platsmallstruktur {#structure}

Webbplatsmallar är helt enkelt paket med en logisk struktur som tydligt återspeglar syftet med paketinnehållet. En platsmall har följande struktur.

* `files`: Mapp med UI-kit, XD och eventuellt andra filer
* `previews`: Mapp med skärmbilder av platsmallen
* `site`: Innehållspaket för innehållet som kopieras för varje plats som skapas från den här mallen, till exempel sidmallar, sidor och så vidare.
* `theme`: Källor till [webbplatstemat](site-themes.md) som ändrar hur webbplatsen ser ut, t.ex. CSS, JavaScript.

## Standardmall för webbplats {#standard-site-template}

Adobe tillhandahåller en referensmall som du kan använda som utgångspunkt för att skapa egna mallar. [Standardwebbplatsmallen är tillgänglig på GitHub.](https://github.com/adobe/aem-site-template-standard)

[Den senaste versionen av standardwebbplatsmallen](https://github.com/adobe/aem-site-template-standard/releases) kan hämtas och användas direkt för [att skapa nya webbplatser](create-site.md).

## Utveckla webbplatsmallar {#developing-templates}

Adobe tillhandahåller och AEM Site Template Builder som en uppsättning skript för att skapa nya webbplatsmallar.

[AEM Site Template Builder är tillgänglig tillsammans med användningsdokumentation för GitHub](https://github.com/adobe/aem-site-template-builder). Det krävs en upplevelse av gränssnittsutvecklare för att anpassa [webbplatstemat](site-themes.md) och AEM utvecklarkunskap krävs för att anpassa webbplatsens struktur och innehåll.
