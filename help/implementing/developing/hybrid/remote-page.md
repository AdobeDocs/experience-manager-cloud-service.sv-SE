---
title: RemotePage-komponenten
description: RemotePage-komponenten är en anpassad sidkomponent för redigering av SPA för fjärreaktion i AEM.
translation-type: tm+mt
source-git-commit: 9a1048f6d185d2d3229bab05b8e827845444d11c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# RemotePage-komponenten {#remote-page-component}

När du bestämmer [vilken nivå av integration](/help/implementing/developing/headful-headless.md) du vill ha mellan din externa SPA och AEM är det ofta tydligt att du behöver kunna visa och redigera SPA inom AEM. RemotePage-komponenten är en anpassad sidkomponent för just detta ändamål.

## Översikt {#overview}

RemotePage-komponenten hämtar alla nödvändiga resurser från programmets genererade `asset-manifest.json` och använder den för att återge SPA i AEM.

* Med RemotePage kan du mata in skript och formatmallar för en SPA i brödtexten för en AEM Page-komponent.
* Med Virtual Front Components kan du markera avsnitt som redigerbara AEM redigeraren.
* Tillsammans kan en SPA på en annan domän göras redigerbar i AEM.

Läs artikeln [Redigera en extern SPA i AEM](editing-external-spa.md) om du vill ha mer information om redigerbara, externa SPA i AEM.

## Krav {#requirements}

* Aktivera CORS under utveckling
* Konfigurera fjärr-URL i Sidegenskaper
* Återge SPA i AEM

## Begränsningar {#limitations}

* Den aktuella implementeringen av RemotePage-komponenten stöder endast fjärreaktionsprogram.
* Intern CSS som är definierad i programmets HTML-rotfil samt infogad CSS på DOM-rotnoden är inte tillgänglig vid fjärråtergivning i AEM.

## Teknisk information {#technical-details}

Precis som resten av det AEM SPA projektet är RemotePage-komponenten en öppen källkod. Fullständig teknisk information om RemotePage-komponenten [finns i GitHub-databasen.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
