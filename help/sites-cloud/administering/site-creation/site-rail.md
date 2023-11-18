---
title: Använda webbplatsservern för att hantera ditt webbplatstema
description: Lär dig de kraftfulla funktionerna i webbplatsspåret för att enkelt anpassa och hantera webbplatstemat.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Använda webbplatsservern för att hantera ditt webbplatstema {#site-rail}

Lär dig de kraftfulla funktionerna i webbplatsspåret för att enkelt anpassa och hantera webbplatstemat.

## Översikt {#overview}

Med hjälp av webbplatsspåret kan du hantera temat och mallresurserna för din webbplats. [Som andra skenor](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) som t.ex. innehållsträd, referenser eller tidslinje, visas platsspåret som panelen längst till vänster i platskonsolen och visar information om det markerade objektet. Till skillnad från andra spår gäller Site-spåret endast platsrötter.

Webbplatsfältet används för att hantera tema- och mallrelaterad information för din webbplats, inklusive:

* [Hämtar temakällor](#downloading-theme-sources)
* [Hämtar mallresurser som trådramar](#downloading-template-resources)
* [Visa och ändra temaversioner](#theme-vrsions)
* [Aktivera frontendpipeline](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Granska [Skapa snabbt webbplatser](/help/journey-sites/quick-site/overview.md) för att bekanta dig med verktyget för att skapa snabbwebbplatser och den rörliga produktionsprocessen för att enkelt anpassa webbplatstemat.

## Hämtar temakällor {#downloading-theme-sources}

När du skapar en plats i AEM baserad på en [webbplatsmall,](site-templates.md) du kan ladda ned [webbplatstema](site-themes.md) med hjälp av platsspåret.

Markera platsens rot för att visa temainformation om platsen när webbplatsspåret visas i platskonsolen.

![Hämta temakällor](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Välj **Hämta temakällor** för att ladda ned en lokal kopia av webbplatstemat som `.zip` -fil för anpassning.

## Hämtar mallresurser {#downloading-template-resources}

[Webbplatsmallar](site-templates.md) kan innehålla information utöver webbplatsens innehållsstruktur och [webbplatstema.](site-themes.md) Platsmallar kan till exempel innehålla trådramsdesign eller andra platsrelaterade filer.

Om webbplatsen är baserad på en webbplatsmall, där webbplatsspåret visas i platskonsolen, markerar du platsens rot för att visa temainformation om webbplatsen, inklusive ytterligare webbplatsresurser.

![Hämta temakällor](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Markera knappen eller knapparna under rubriken **Hämta ytterligare mallresurser** om du vill hämta en lokal kopia av de tillgängliga filerna.

## Visa och ändra temaversioner {#them-versions}

Om din webbplats är baserad på en webbplatsmall är det möjligt att temat redan har anpassats av din frontendutvecklare. Med hjälp av webbplatsspåret kan du visa vilken version av webbplatstemat som är distribuerad och växla till tidigare versioner.

Markera platsens rot för att visa temainformation om platsen när webbplatsspåret visas i platskonsolen.

![Webbplatsversioner i rälsen](/help/sites-cloud/administering/assets/theme-versions.png)

Den aktuella versionen av temat visas med sin implementeringshash tillsammans med tidsstämpeln för den senaste uppdateringen.

Välj **Välj version** om du vill visa tidigare versioner av temat.

![Välj temaversion](/help/sites-cloud/administering/assets/select-theme-versions.png)

Markera den version som du vill ändra till och välj sedan **Använd** för att göra ändringen.

Om AEM upptäcker att en nyare version av temat har distribuerats via front end-pipeline men inte tillämpats på din webbplats, visas en meddelandeikon.

![Senare version av temaindikatorn](/help/sites-cloud/administering/assets/new-theme-version.png)

Du kan använda **Välj version** för att uppdatera till den nya temaversionen.

## Aktivera frontendspipelinen {#enabling-front-end-pipeline}

Om webbplatsen inte har skapats med en webbplatsmall går det inte att använda frontendpipeline för att anpassa och distribuera temat.

Du kan emellertid aktivera frontendspipelinen för din webbplats med hjälp av platsspåret.

Markera platsens rot för att visa temainformation om webbplatsen och välj sedan **Aktivera frontdelspipeline**.

![Aktivera frontendpipeline](/help/sites-cloud/administering/assets/enable-fep.png)

Mer information finns i dokumentet [Aktiverar frontendspipelinen.](enable-front-end-pipeline.md)
