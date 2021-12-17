---
title: Webbplatsmallar
description: Lär dig hur AEM webbplatsmallar kan användas för att fördefiniera webbplatsstrukturen och det ursprungliga innehållet så att du snabbt kan skapa webbplatser.
feature: Administering
role: Admin
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Webbplatsmallar {#site-templates}

Lär dig hur AEM webbplatsmallar kan användas för att fördefiniera webbplatsstrukturen och det ursprungliga innehållet så att du snabbt kan skapa webbplatser.

## Översikt {#overview}

Det är bekvämt att ha fördefinierade strukturer tillgängliga för att snabbt kunna driftsätta en ny webbplats baserat på en uppsättning befintliga standarder. Webbplatsmallar är ett sätt att kombinera grundläggande webbplatsinnehåll i ett bekvämt och återanvändbart paket.

Webbplatsmallar innehåller i allmänhet baswebbplatsinnehåll och -struktur samt information om webbplatsformat, som kallas [webbplatstema,](site-themes.md) för att snabbt komma igång med en ny webbplats. Administratörer väljer en webbplatsmall som webbplatsen ska baseras på [när webbplatsen skapades.](create-site.md)

Mallarna är kraftfulla eftersom de både kan återanvändas och anpassas. Och eftersom du kan ha flera mallar tillgängliga i AEM kan du skapa olika webbplatser som passar olika affärsbehov.

>[!NOTE]
>
>AEM webbplatsmallar ska inte blandas ihop med [sidmallar.](/help/sites-cloud/authoring/features/templates.md) Platsmallar definierar den övergripande strukturen för en plats. En sidmall definierar strukturen och det ursprungliga innehållet för en enskild sida.
>
>AEM webbplatsmallar ska inte blandas ihop med [AEM webbplatsteman.](site-themes.md) AEM webbplatsteman innehåller bara formatinformation för en AEM. AEM webbplatsmallar definierar webbplatsens struktur och innehåll samt innehåller ett AEM platstema för att möjliggöra [skapa webbplatser snabbt.](create-site.md)

## Lägga till en platsmall i AEM {#adding}

Du kan lägga till flera mallar i AEM, som sedan kan användas för att [skapa webbplatser.](create-site.md)

1. Logga in i AEM redigeringsmiljö och navigera till webbplatskonsolen

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Tryck eller klicka **Skapa** längst upp till höger på skärmen och i listrutan väljer **Plats från mall**.

   ![Skapa en plats från en mall](../assets/create-site-from-template.png)

1. Tryck eller klicka på i guiden Skapa plats **Importera** överst i den vänstra kolumnen.

   ![Guiden Skapa webbplats](../assets/site-creation-wizard.png)

1. Leta reda på mallen som du vill använda i filläsaren och tryck eller klicka på **Överför**.

1. När den har överförts visas den i listan med tillgängliga mallar.

Mallen har överförts och kan användas för [skapa nya webbplatser.](create-site.md)

När du väljer en befintlig mall visas information om mallen i den högra kolumnen.

![Välj en mall](../assets/select-site-template.png)

## Platsmallstruktur {#structure}

Webbplatsmallar är helt enkelt paket med en logisk struktur som tydligt återspeglar syftet med paketinnehållet. En platsmall har följande struktur.

* `files`: Mapp med UI-kit, XD och eventuellt andra filer
* `previews`: Mapp med skärmbilder av platsmallen
* `site`: Innehållspaket för det innehåll som kopieras för varje plats som skapas från den här mallen, t.ex. sidmallar, sidor osv.
* `theme`: Källor till [webbplatstema](site-themes.md) för att ändra hur webbplatsen ser ut, t.ex. CSS, JavaScript osv.

## Standardmall för webbplats {#standard-site-template}

Adobe tillhandahåller en referensmall som du kan använda som utgångspunkt för att skapa egna mallar. [Standardwebbplatsmallen är tillgänglig på GitHub.](https://github.com/adobe/aem-site-template-standard)

[Den senaste versionen av standardwebbplatsmallen](https://github.com/adobe/aem-site-template-standard/releases) kan laddas ned och användas direkt för [skapa nya webbplatser.](create-site.md)

## Utveckla webbplatsmallar {#developing-templates}

Adobe tillhandahåller och AEM Site Template Builder som en uppsättning skript för att skapa nya webbplatsmallar.

[AEM Site Template Builder är tillgänglig tillsammans med användningsdokumentation för GitHub.](https://github.com/adobe/aem-site-template-builder) Det krävs en upplevelse av gränssnittsutvecklare för att anpassa [webbplatstema](site-themes.md) och AEM utvecklarkunskap krävs för att anpassa webbplatsens struktur och innehåll.
