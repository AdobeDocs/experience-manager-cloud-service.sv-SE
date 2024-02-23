---
title: Hantera platstemat med hjälp av platspanelen
description: Lär dig de kraftfulla funktionerna i panelen Webbplats så att du enkelt kan anpassa och hantera ditt webbplatstema.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Hantera ditt webbplatstema med hjälp av platspanelen {#site-panel}

Lär dig de kraftfulla funktionerna i panelen Webbplats så att du enkelt kan anpassa och hantera ditt webbplatstema.

## Ökning {#overview}

På platspanelen kan du hantera teman och mallresurser för din webbplats. [Precis som andra paneler](/help/sites-cloud/authoring/sites-console/console-side-panel.md) som panelen Innehållsträd, Referenser eller Tidslinje visas platspanelen som den vänstra panelen i platskonsolen och visar information om det markerade objektet. Till skillnad från andra paneler gäller platspanelen endast platsrötter.

Panelen Plats används för att hantera tema- och mallrelaterad information för din webbplats, inklusive:

* [Hämtar temakällor](#downloading-theme-sources)
* [Hämtar mallresurser som trådramar](#downloading-template-resources)
* [Visa och ändra temaversioner](#theme-vrsions)
* [Aktivera frontendpipeline](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Granska [Skapa snabbt webbplatser](/help/journey-sites/quick-site/overview.md) för att bekanta dig med verktyget för att skapa snabbwebbplatser och den rörliga produktionsprocessen för att enkelt anpassa webbplatstemat.

## Hämtar temakällor {#downloading-theme-sources}

När du skapar en plats i AEM baserad på en [webbplatsmall,](site-templates.md) du kan ladda ned [webbplatstema](site-themes.md) med panelen Plats.

När platspanelen visas i platskonsolen markerar du platsens rot för att visa temainformation om platsen.

![Hämta temakällor](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Välj **Hämta temakällor** för att ladda ned en lokal kopia av webbplatstemat som `.zip` -fil för anpassning.

## Hämtar mallresurser {#downloading-template-resources}

[Webbplatsmallar](site-templates.md) kan innehålla information utöver webbplatsens innehållsstruktur och [webbplatstema.](site-themes.md) Platsmallar kan till exempel innehålla trådramsdesign eller andra platsrelaterade filer.

Om webbplatsen är baserad på en platsmall, där platspanelen visas i platskonsolen, markerar du platsens rot för att visa temainformation om platsen, inklusive ytterligare webbplatsresurser.

![Hämta temakällor](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Markera knappen eller knapparna under rubriken **Hämta ytterligare mallresurser** om du vill hämta en lokal kopia av de tillgängliga filerna.

## Visa och ändra temaversioner {#them-versions}

Om din webbplats är baserad på en webbplatsmall är det möjligt att temat redan har anpassats av din frontendutvecklare. Med hjälp av panelen Plats kan du visa vilken version av webbplatstemat som är distribuerad och växla till tidigare versioner.

När platspanelen visas i platskonsolen markerar du platsens rot för att visa temainformation om platsen.

![Webbplatsversioner i panelen](/help/sites-cloud/administering/assets/theme-versions.png)

Den aktuella versionen av temat visas med sin implementeringshash tillsammans med tidsstämpeln för den senaste uppdateringen.

Välj **Välj version** om du vill visa tidigare versioner av temat.

![Välj temaversion](/help/sites-cloud/administering/assets/select-theme-versions.png)

Markera den version som du vill ändra till och välj sedan **Använd** för att göra ändringen.

Om AEM upptäcker att en nyare version av temat har distribuerats via front end-pipeline men inte tillämpats på din webbplats, visas en meddelandeikon.

![Senare version av temaindikatorn](/help/sites-cloud/administering/assets/new-theme-version.png)

Du kan använda **Välj version** för att uppdatera till den nya temaversionen.

## Aktivera frontendspipelinen {#enabling-front-end-pipeline}

Om webbplatsen inte har skapats med en webbplatsmall går det inte att använda frontendpipeline för att anpassa och distribuera temat.

Du kan emellertid aktivera frontendpipeline för webbplatsen med hjälp av platspanelen.

När platspanelen visas i platskonsolen markerar du platsens rot för att visa temainformation om platsen och väljer sedan **Aktivera frontdelspipeline**.

![Aktivera frontendpipeline](/help/sites-cloud/administering/assets/enable-fep.png)

Mer information finns i dokumentet [Aktiverar frontendspipelinen.](enable-front-end-pipeline.md)
