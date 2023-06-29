---
title: Webbplatsteman
description: Lär dig hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design.
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Webbplatsteman {#site-themes}

Lär dig hur AEM webbplatsteman kan användas för att anpassa webbplatsens stil och design.

## Översikt {#overview}

Ett AEM webbplatstema är ett paket som innehåller CSS-, JavaScript- och statiska resurser som definierar formateringen för din AEM och som följer strukturen för ett AEM webbplatstema.

Webbplatser som skapats med AEM webbplatsmallar gör det enkelt att hämta, anpassa och omdistribuera teman.

>[!NOTE]
>
>AEM teman ska inte blandas ihop med [AEM webbplatsmallar](site-templates.md). AEM webbplatsteman innehåller bara formatinformation för en AEM. AEM webbplatsmallar definierar webbplatsens struktur och innehåll samt innehåller ett AEM webbplatstema för [skapa webbplatser snabbt](create-site.md).

## Använda webbplatsteman {#using-themes}

Webbplatsteman används på två olika sätt:

* De används som en del av en webbplatsmall för att definiera format när [skapa en plats.](create-site.md)
* De laddas ned när du har skapat en webbplats baserad på en webbplatsmall så att en gränssnittsutvecklare kan anpassa formatet ytterligare.

>[!TIP]
>
>En fullständig beskrivning av processen att skapa en webbplats från en mall och anpassa dess tema finns i [Skapa snabbt webbplatser](/help/journey-sites/quick-site/overview.md).

## Platstemastruktur {#structure}

Webbplatsteman är helt enkelt paket med en logisk struktur som tydligt återspeglar syftet med paketinnehållet. Ett webbplatstema har följande struktur som är typisk för ett frontendprojekt.

* `src/main.ts`: Huvudingångspunkten för JS- och CSS-temat
* `src/site`: JS- och CSS-filer som gäller för hela platsen
* `src/components`: JS- och CSS-filer som är specifika för AEM
* `src/resources`: Statiska filer som ikoner, logotyper och teckensnitt

## Standardtema för webbplats {#standard-site-theme}

Adobe tillhandahåller ett referenstema som du kan använda som utgångspunkt för att skapa ett eget tema. [Standardwebbplatstemat är tillgängligt på GitHub](https://github.com/adobe/aem-site-template-standard/tree/main/theme).

## Utveckla webbplatsteman {#developing-themes}

Adobe tillhandahåller en AEM Site Theme Builder som en uppsättning skript för att skapa nya webbplatsteman.

[AEM Site Theme Builder är tillgänglig tillsammans med användningsdokumentation för GitHub](https://github.com/adobe/aem-site-theme-builder). Utvecklingsupplevelsen i gränssnittet krävs för att anpassa temat.
