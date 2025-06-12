---
title: Webbplatsteman
description: Lär dig hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design.
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Webbplatsteman {#site-themes}

{{traditional-aem}}

Lär dig hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design.

## Ökning {#overview}

Ett AEM-tema är ett paket som innehåller CSS-, JavaScript- och statiska resurser som definierar formateringen för din AEM-webbplats och som följer strukturen för ett AEM-webbplatstema.

Webbplatser som skapats med AEM webbplatsmallar gör det enkelt att ladda ned, anpassa och omdistribuera teman.

>[!NOTE]
>
>AEM webbplatsteman ska inte blandas ihop med [AEM webbplatsmallar](site-templates.md). AEM webbplatsteman innehåller endast formatinformation för en AEM-webbplats. AEM webbplatsmallar definierar webbplatsens struktur och innehåll samt innehåller ett AEM-tema som gör det möjligt att skapa [webbplatser snabbt](create-site.md).

## Använda webbplatsteman {#using-themes}

Webbplatsteman används på två olika sätt:

* De används som en del av en webbplatsmall för att definiera format när [en plats ](create-site.md) skapas.
* De laddas ned när du har skapat en webbplats baserad på en webbplatsmall så att en gränssnittsutvecklare kan anpassa formatet ytterligare.

>[!TIP]
>
>En fullständig beskrivning av processen att skapa en webbplats från en mall och anpassa dess tema finns på [snabbwebbplatsresan](/help/journey-sites/quick-site/overview.md).

## Platstemastruktur {#structure}

Webbplatsteman är helt enkelt paket med en logisk struktur som tydligt återspeglar syftet med paketinnehållet. Adobe rekommenderar följande struktur för ett tema:

* `src/theme.ts`: Huvudstartpunkten för JS- och CSS-temat
* `src/site`: JS- och CSS-filer som gäller för hela platsen
* `src/components`: JS- och CSS-filer specifika för AEM-komponenter
* `src/resources`: Statiska filer som ikoner, logotyper och teckensnitt

Beroende på specifika projektbehov kan temastrukturen variera så länge huvudstartpunkten, `src/theme.ts`, bevaras.

## Standardtema för webbplats {#standard-site-theme}

Adobe har ett referenstema som du kan använda som utgångspunkt för att skapa ett eget tema. [Standardwebbplatstemat är tillgängligt på GitHub](https://github.com/adobe/aem-site-template-standard/tree/main/theme).

## Utveckla webbplatsteman {#developing-themes}

Adobe tillhandahåller en AEM Site Theme Builder som en uppsättning skript för att skapa nya webbplatsteman.

[AEM Site Theme Builder är tillgänglig tillsammans med användningsdokumentation för GitHub](https://github.com/adobe/aem-site-theme-builder). Utvecklingsupplevelsen i gränssnittet krävs för att anpassa temat.
