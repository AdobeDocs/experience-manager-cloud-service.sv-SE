---
title: Sidopanelen i platskonsolen
description: Lär dig hur du använder sidopanelen i konsolen AEM webbplatser för att bättre förstå och navigera i ditt innehåll.
exl-id: 7f2571d6-b847-4cce-8e94-94ba0d2e04a5
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# Sidopanelen i platskonsolen {#side-panel}

Lär dig hur du använder sidopanelen i konsolen AEM **Platser** för att bättre förstå och navigera i ditt innehåll.

## Orientering {#orientation}

Sidpanelen stängs som standard när du öppnar konsolen **Platser**. På så sätt är skärmen helt och hållet dedikerad till ditt innehåll.

Tryck eller klicka på ikonen **Side Panel** i konsolens verktygsfält **Sites** för att aktivera sidopanelen och välja hur du vill visa innehållet.

* [Endast innehåll](#content-only)
* [Innehållsträd](#content-tree)
* [Tidslinje](#timeline)
* [Referenser](#references)
* [Plats](#site)
* [Filter](#filter)
* [Konfigurationsanalys](#setup-analytics)

![Vyer av panelen Sida i webbplatskonsolen](assets/sites-console-side-panel-views.png)

Den aktuella vyn markeras med en blå bockmarkering i listrutan och sidpanelsikonen i verktygsfältet uppdateras med namnet på den valda vyn.

## Endast innehåll {#content-only}

Den här vyn av sidopanelen stänger av den, d.v.s. den visar bara innehållet på din webbplats.

>[!TIP]
>
>Använd kortkommandot för grav accent/backtick `´` om du vill växla till vyn för endast innehåll på sidopanelen.

## Innehållsträd {#content-tree}

I den här vyn på sidopanelen visas ditt innehåll i en trädhierarki. Innehållsträdet kan användas för att snabbt navigera i platshierarkin på sidopanelen och visa mycket information om sidorna i den aktuella mappen.

![Vyn Innehållsträd på sidpanelen](assets/console-side-panel-content-tree.png)

En högerriktad kniv bredvid ett objekt i trädet anger en nod som kan expanderas för att visa dess underordnade noder. Tryck eller klicka på avrivningen för att visa de underordnade.

Konsolen visar innehållet i det för närvarande valda objektet i innehållsträdet.

Med innehållsträdets sidopanel i kombination med en listvy eller kortvy kan du enkelt se projektets hierarkiska struktur och enkelt navigera i innehållsstrukturen med innehållsträdets sidopanel, samt visa detaljerad sidinformation i listvyn.

>[!TIP]
>
>* Använd kortkommandot `Alt+1` för att växla till vyn för innehållsträdet på sidopanelen.
>* När du har markerat en post i hierarkin kan du använda piltangenterna för att snabbt navigera i hierarkin.
>* Mer information finns i [kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

## Tidslinje {#timeline}

Tidslinjen kan användas för att visa händelser som har påverkat den valda resursen. Du kan också använda den för att starta vissa händelser, till exempel arbetsflöden eller versioner.

![Information om tidslinjen](/help/sites-cloud/authoring/assets/timeline-detail.png)

På sidopanelen **Tidslinje** kan du visa olika händelser som hör till ett markerat objekt som kan väljas som typer i en nedrullningsbar lista:

* Kommentar
* [Anteckningar](/help/sites-cloud/authoring/page-editor/annotations.md)
* [Verksamhet](/help/sites-cloud/authoring/personalization/activities.md)
* [Launches](/help/sites-cloud/authoring/launches/overview.md)
* [Versioner](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md)
   * Observera att ingen information visas för tillfälliga arbetsflöden eftersom ingen historikinformation sparas för dessa.<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* Visa alla

Du kan dessutom lägga till/visa kommentarer om det markerade objektet med rutan **Kommentar** längst ned i händelselistan. Om du skriver en kommentar följt av `Return` registreras kommentaren. Den visas när **Kommentarer** eller **Visa alla** markeras.

I konsolen **Platser** kan du även komma åt ytterligare funktioner via ellipsknappen bredvid fältet **Kommentar**.

* [Spara en version](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Starta ett arbetsflöde](/help/sites-cloud/authoring/workflows/applying.md)

![Kommentarfält för platskonsolen](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* Använd kortkommandot `Alt+2` för att växla till tidslinjevyn på sidopanelen.
>* Mer information finns i [kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

## Referenser {#references}

I vyn **Referenser** visas en lista med referenstyper till eller från till den valda resursen i konsolen.

![Referensinformation](assets/console-side-panel-references-detail.png)

Välj lämplig referenstyp för mer information. I vissa situationer är ytterligare åtgärder tillgängliga när du väljer en specifik referens, bland annat:

* **Inkommande länkar** innehåller en lista med sidor som refererar till sidan, tillsammans med direktåtkomst till **Redigera** en av dessa sidor när du väljer en specifik länk.
   * Detta kan bara visa statiska länkar, inte dynamiskt genererade länkar som till exempel från List-komponenten.
* [Startar](/help/sites-cloud/authoring/launches/overview.md), ger åtkomst till relaterade starter
* [Live-kopior](/help/sites-cloud/administering/msm/overview.md) visar sökvägarna för alla live-kopior som baseras på den valda resursen.
* [Utskrift](/help/sites-cloud/administering/msm/best-practices.md), innehåller information och olika åtgärder
* [Språkkopior](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel), innehåller information och olika åtgärder

## Plats {#site}

I vyn **Plats** på sidpanelen visas information om platser [som skapats med en webbplatsmall](/help/sites-cloud/administering/site-creation/create-site.md).

![Platspanelen](assets/console-side-panel-site-paenl.png)

Mer information om hur du kan använda panelen för att hantera [temat för din plats](/help/sites-cloud/administering/site-creation/site-themes.md) finns i dokumentet [Hantera ditt platstema på panelen Plats](/help/sites-cloud/administering/site-creation/site-rail.md).

Om du ännu inte har konfigurerat frontendinje för att kunna skapa temabaserade webbplatser kommer sidopanelen att erbjuda det alternativet.

![Alternativ för att aktivera frontendpipeline på sidopanelen](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>En fullständig beskrivning av processen att skapa en webbplats från en mall och anpassa dess tema finns på [snabbwebbplatsresan](/help/journey-sites/quick-site/overview.md).

## Filter {#filter}

Panelen **Filter** liknar [sökfunktionen](/help/sites-cloud/authoring/search.md) med rätt platsfilter inställda, vilket gör att du kan filtrera innehållet ytterligare.

![Exempel på filter](assets/console-side-panel-filter.png)

Till skillnad från andra vyer på sidopanelen kan du växla till en annan vy genom att trycka eller klicka på `X` i sökfältet.

## Konfigurationsanalys {#setup-analytics}

I den här vyn kan du snabbt konfigurera Adobe Analytics för en vald webbplats.

![Konfigurera analys](assets/sites-console-side-panel-setup-analytics.png)
