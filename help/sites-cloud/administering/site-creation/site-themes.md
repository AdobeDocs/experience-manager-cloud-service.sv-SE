---
title: Webbplatsteman
description: Läs om hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design för AEM traditionella projekt med publiceringsleverans.
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 9efba01add46c09e9839da6bb96b138d48018e54
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Webbplatsteman {#site-themes}

{{traditional-aem}}

Läs om hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design för AEM traditionella projekt med publiceringsleverans.

## Ökning {#overview}

Ett AEM-tema är ett paket som innehåller CSS-, JavaScript- och statiska resurser som definierar formateringen för din AEM-webbplats och som följer strukturen för ett AEM-webbplatstema.

Webbplatser som skapats med AEM webbplatsmallar gör det enkelt att hämta, anpassa och omdistribuera teman för AEM traditionella redigeringsprojekt med [publiceringsleverans.](/help/sites-cloud/authoring/author-publish.md)

>[!NOTE]
>
>AEM webbplatsteman ska inte blandas ihop med [AEM webbplatsmallar](site-templates.md). AEM webbplatsteman innehåller endast formatinformation för en AEM-webbplats. AEM webbplatsmallar definierar webbplatsens struktur och innehåll samt innehåller ett AEM-tema som gör att du kan skapa [webbplatser snabbt.](create-site.md)

## Använda webbplatsteman {#using-themes}

Webbplatsteman används på två olika sätt:

* De används som en del av en webbplatsmall för att definiera format när [en webbplats skapas.](create-site.md)
* De laddas ned när du har skapat en webbplats baserad på en webbplatsmall så att en gränssnittsutvecklare kan anpassa formatet ytterligare.

>[!TIP]
>
>En fullständig beskrivning av processen att skapa en webbplats från en mall och anpassa dess tema finns i [snabbwebbplatsgenereringsresan.](/help/journey-sites/quick-site/overview.md)

## Platstemastruktur {#structure}

Webbplatsteman är helt enkelt paket med en logisk struktur som tydligt återspeglar syftet med paketinnehållet. Adobe rekommenderar följande struktur för ett tema:

* `src/theme.ts`: Huvudstartpunkten för JS- och CSS-temat
* `src/site`: JS- och CSS-filer som gäller för hela platsen
* `src/components`: JS- och CSS-filer specifika för AEM-komponenter
* `src/resources`: Statiska filer som ikoner, logotyper och teckensnitt

Beroende på specifika projektbehov kan temastrukturen variera så länge huvudstartpunkten, `src/theme.ts`, bevaras.

## Standardtema för webbplats {#standard-site-theme}

Adobe har ett referenstema som du kan använda som utgångspunkt för att skapa ett eget tema. [Standardwebbplatstemat är tillgängligt på GitHub.](https://github.com/adobe/aem-site-template-standard/tree/main/theme)

## Utveckla webbplatsteman {#developing-themes}

Adobe tillhandahåller en AEM Site Theme Builder som en uppsättning skript för att skapa nya webbplatsteman.

[AEM Site Theme Builder är tillgänglig tillsammans med användningsdokumentation för GitHub.](https://github.com/adobe/aem-site-theme-builder) Utvecklingsupplevelsen i gränssnittet krävs för att anpassa temat.
