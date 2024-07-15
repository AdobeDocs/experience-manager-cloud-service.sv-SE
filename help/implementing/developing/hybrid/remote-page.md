---
title: RemotePage-komponenten
description: RemotePage-komponenten är en anpassad sidkomponent för redigering av SPA för fjärreaktion i AEM.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# RemotePage-komponenten {#remote-page-component}

När du bestämmer [vilken nivå av integration](/help/implementing/developing/headful-headless.md) du vill ha mellan din externa SPA och AEM är det ofta tydligt att du måste kunna visa och redigera SPA inom AEM. RemotePage-komponenten är en anpassad sidkomponent för just detta ändamål.

## Ökning {#overview}

RemotePage-komponenten hämtar alla nödvändiga resurser från programmets genererade `asset-manifest.json` och använder den för att återge SPA i AEM.

* Med RemotePage kan du mata in skript och formatmallar för en SPA i brödtexten för en AEM Page-komponent.
* Med Virtual Front Components kan du markera avsnitt som redigerbara AEM redigeraren.
* Tillsammans kan en SPA på en annan domän göras redigerbar i AEM.

Mer information om redigerbar, extern SPA i AEM finns i artikeln [Redigera en extern SPA i AEM](editing-external-spa.md).

## Krav {#requirements}

* Aktivera CORS under utveckling
* Konfigurera fjärr-URL i Sidegenskaper
* Återge SPA i AEM
* Webbprogrammet måste använda ett resurmanifest som något av följande och visa en `asset-manifest.json`-fil i domänroten som listar alla CSS- och JS-filer som ska läsas in i en `entrypoints property` :
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![exempel på egenskapen entrypoints](assets/asset-manifest-entrypoints.png)
* Programmet måste kunna initieras i ett `<div id="root"></div>` under elementet `body`. Om en annan kod förväntas för att programmet ska kunna instansieras måste detta justeras i HTML-skripten för proxykomponenten som har en `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Begränsningar {#limitations}

* RemotePage-komponenten förväntar sig att implementeringen tillhandahåller ett tillgångsmanifest som den [ som finns här.](https://github.com/shellscape/webpack-manifest-plugin) RemotePage-komponenten har bara testats för att fungera med React Framework (och Next.js via komponenten remote-page-next) och stöder därför inte fjärrinläsning av program från andra ramverk, till exempel Angular.
* Intern CSS som är definierad i programmets rotfil och infogad CSS på DOM-rotnoden är inte tillgänglig vid fjärråtergivning i AEM.

## Teknisk information {#technical-details}

Precis som resten av AEM SPA är RemotePage-komponenten öppen källkod. Fullständig teknisk information om RemotePage-komponenten finns i [GitHub-databasen.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
