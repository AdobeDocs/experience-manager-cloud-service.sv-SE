---
title: Sidopanelen i platskonsolen
description: Lär dig hur du använder sidopanelen i konsolen AEM webbplatser för att bättre förstå och navigera i ditt innehåll.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---


# Sidopanelen i platskonsolen {#side-panel}

Lär dig hur du använder sidopanelen i AEM **Webbplatser** för att bättre förstå och navigera i innehållet.

## Orientering {#orientation}

Sidpanelen är som standard stängd när du anger **Webbplatser** konsol. På så sätt är skärmen helt och hållet dedikerad till ditt innehåll.

Tryck eller klicka på **Side Panel** ikonen i **Webbplatser** konsolens verktygsfält för att aktivera sidopanelen och välja hur innehållet ska visas.

* [Endast innehåll](#content-only)
* [Innehållsträd](#content-tree)
* [Tidslinje](#timeline)
* [Referenser](#references)
* [Plats](#site)
* [Filter](#filter)
* [Konfigurationsanalys](#setup-analytics)

![Vyer av sidpanelen i webbplatskonsolen](assets/sites-console-side-panel-views.png)

Den aktuella vyn markeras med en blå bockmarkering i listrutan och sidpanelsikonen i verktygsfältet uppdateras med namnet på den valda vyn.

## Endast innehåll {#content-only}

Den här vyn av sidopanelen stänger av den, d.v.s. den visar bara innehållet på din webbplats.

>[!TIP]
>
>Använd grav accent/backtick `´` kortkommando för att växla till vyn med endast innehåll på sidopanelen.

## Innehållsträd {#content-tree}

I den här vyn på sidopanelen visas ditt innehåll i en trädhierarki. Innehållsträdet kan användas för att snabbt navigera i platshierarkin på sidopanelen och visa mycket information om sidorna i den aktuella mappen.

![Vyn Innehållsträd på sidpanelen](assets/console-side-panel-content-tree.png)

En högerriktad kniv bredvid ett objekt i trädet anger en nod som kan expanderas för att visa dess underordnade noder. Tryck eller klicka på avrivningen för att visa de underordnade.

Konsolen visar innehållet i det för närvarande valda objektet i innehållsträdet.

Med innehållsträdets sidopanel i kombination med en listvy eller kortvy kan du enkelt se projektets hierarkiska struktur och enkelt navigera i innehållsstrukturen med innehållsträdets sidopanel, samt visa detaljerad sidinformation i listvyn.

>[!TIP]
>
>* Använd `Alt+1` kortkommando för att växla till vyn för innehållsträdet på sidopanelen.
>* När du har markerat en post i hierarkin kan du använda piltangenterna för att snabbt navigera i hierarkin.
>* Se [kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) för mer information.

## Tidslinje {#timeline}

Tidslinjen kan användas för att visa händelser som har påverkat den valda resursen. Du kan också använda den för att starta vissa händelser, till exempel arbetsflöden eller versioner.

![Information om tidslinjen](/help/sites-cloud/authoring/assets/timeline-detail.png)

The **Tidslinje** I sidopanelen kan du visa olika händelser för ett markerat objekt som kan markeras som typer i en nedrullningsbar lista:

* Kommentar
* [Anteckningar](/help/sites-cloud/authoring/page-editor/annotations.md)
* [Verksamhet](/help/sites-cloud/authoring/personalization/activities.md)
* [Launches](/help/sites-cloud/authoring/launches/overview.md)
* [Versioner](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md)
   * Observera att ingen information visas för tillfälliga arbetsflöden eftersom ingen historikinformation sparas för dessa.<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* Visa alla

Du kan dessutom lägga till/visa kommentarer om det markerade objektet med **Kommentar** som visas längst ned i listan med händelser. Skriva en kommentar följt av `Return` registrerar kommentaren. Den visas när **Kommentarer** eller **Visa alla** markeras.

I **Webbplatser** konsolen kan du också komma åt ytterligare funktioner via ellipsknappen bredvid **Kommentar** fält.

* [Spara en version](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Starta ett arbetsflöde](/help/sites-cloud/authoring/workflows/applying.md)

![Kommentarfält för platskonsolen](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* Använd `Alt+2` kortkommando för att växla till tidslinjevyn på sidopanelen.
>* Se [kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) för mer information.

## Referenser {#references}

The **Referenser** I visas en lista med referenstyper till eller från till den resurs som valts i konsolen.

![Referensinformation](assets/console-side-panel-references-detail.png)

Välj lämplig referenstyp för mer information. I vissa situationer är ytterligare åtgärder tillgängliga när du väljer en specifik referens, bland annat:

* **Inkommande länkar**, innehåller en lista med sidor som refererar till sidan, tillsammans med direktåtkomst till **Redigera** en av dessa sidor när du markerar en specifik länk.
   * Detta kan bara visa statiska länkar, inte dynamiskt genererade länkar som till exempel från List-komponenten.
* [Startar](/help/sites-cloud/authoring/launches/overview.md), ger åtkomst till relaterade starter
* [Live-kopior](/help/sites-cloud/administering/msm/overview.md) visar sökvägarna för alla live-kopior som baseras på den valda resursen.
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md), innehåller information och olika åtgärder
* [Språk Kopior](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel), innehåller information och olika åtgärder

## Plats {#site}

The **Plats** vy över sidpanelen med information om platser [som har skapats med en webbplatsmall.](/help/sites-cloud/administering/site-creation/create-site.md)

![Panelen Plats](assets/console-side-panel-site-paenl.png)

Se dokumentet [Hantera platstemat med hjälp av platspanelen](/help/sites-cloud/administering/site-creation/site-rail.md) om du vill ha mer information om hur du kan använda panelen för att hantera [temat för din webbplats.](/help/sites-cloud/administering/site-creation/site-themes.md).

Om du ännu inte har konfigurerat frontendinje för att kunna skapa temabaserade webbplatser kommer sidopanelen att erbjuda det alternativet.

![Möjlighet att aktivera frontendpipeline på sidopanelen](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>En fullständig beskrivning av processen att skapa en webbplats från en mall och anpassa dess tema finns i [En resa där man snabbt skapar webbplatser.](/help/journey-sites/quick-site/overview.md)

## Filter {#filter}

The **Filter** -panelen liknar [sökfunktion](/help/sites-cloud/authoring/search.md) med rätt platsfilter redan inställda så att du kan filtrera innehållet ytterligare.

![Exempel på filter](assets/console-side-panel-filter.png)

Om du vill växla till en annan vy trycker du på eller klickar på `X` i sökfältet.

## Konfigurationsanalys {#setup-analytics}

I den här vyn kan du snabbt konfigurera Adobe Analytics för en vald webbplats.

![Konfigurationsanalys](assets/sites-console-side-panel-setup-analytics.png)
