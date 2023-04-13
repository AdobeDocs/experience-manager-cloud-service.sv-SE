---
title: Hämta JSON-innehåll med JavaScript
description: Upptäck hur du hämtar JSON-innehåll från testmiljön med en CodePen-app och den AEM Headless Client för JavaScript.
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Hämta JSON-innehåll med JavaScript {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Hämta JSON-innehåll med JavaScript"
>abstract="Upptäck hur du hämtar JSON-innehåll från testmiljön med en CodePen-app och den AEM Headless Client för JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Starta exempelappen CodePen"
>abstract="Vi har skapat en minimal CodePen-app för att införa hämtning av JSON-data från testmiljön med hjälp av GraphQL beständiga frågor.<br><br>Starta CodePen-exemplet genom att klicka nedan och följ sedan den här guiden för mer information."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="I den här modulen lärde du dig att använda den AEM Headless Client för JavaScript för att hämta JSON-data från testmiljön med GraphQL beständiga frågor.<br><br>Nu förstår ni hur ni kan använda den här klienten för att förbruka data från ert eget webbprogram."
>abstract=""

## Introduktion {#intro}

Du börjar i CodePen-appen, som fungerar som ett minimalt exempel på hur du hämtar JSON-data med [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js). Exempelappen är utformad för att återge allt JSON-innehåll som returneras, oavsett strukturen för den underliggande innehållsfragmentmodellen. CodePen-appen försöker vara detaljerad med eventuella fel som påträffas, så du kan se följande felmeddelande som skrivs ut i appens nedre del:

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

Detta fel förväntas eftersom programmet ännu inte har konfigurerats för att använda den beständiga fråga som du sparade och publicerade i en tidigare modul. Du konfigurerar appen att hämta data från din specifika fråga i följande steg.

## Genomgång av CodePen {#code-walkthrough}

JS-rutan (Javascript) på CodePen innehåller hjärnan i exempelappen. Från och med rad 2 importerar vi den AEM Headless Client för JavaScript från Skypack CDN. Skypack används för att underlätta utvecklingen utan ett steg, men du kan även använda AEM Headless Client med NPM eller Garn i dina egna projekt. Läs användningsinstruktionerna i [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) för mer information.

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

På rad 6 läser vi informationen om din publiceringsvärd från `publishHost` frågeparameter. Det här är värddatorn som AEM Headless Client hämtar data från. Detta kodas vanligtvis i din app, men vi använder en frågeparameter för att göra det enklare för CodePen-appen att arbeta i olika miljöer.

Vi konfigurerar den AEM Headless Client på rad 12 att använda en proxy-Adobe IO-körningsfunktion för att undvika CORS-problem. Detta krävs inte för dina egna projekt, men det krävs för att CodePen-appen ska fungera med din testmiljö. Proxyfunktionen är konfigurerad att använda `publishHost` värdet som angavs i frågeparametern.

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

Funktionen `fetchJsonFromGraphQL()` används för att utföra hämtningsbegäran med AEM Headless Client. Den anropas varje gång koden ändras eller kan aktiveras genom att du trycker på länken &quot;Uppdatera&quot;. Den faktiska `aemHeadlessClient.runPersistedQuery(..)` samtal inträffar på rad 34. Vi ändrar lite senare hur dessa JSON-data återges, men för tillfället skriver vi bara ut dem på `#output` div med `resultToPreTag(queryResult)` funktion.

## Hämta data från din beständiga fråga {#use-persisted-query}

På rad 25 anger vi vilken GraphQL-fråga som appen ska hämta data från. Namnet på den beständiga frågan är en kombination av namnet på projektet (dvs. `your-project`), följt av ett snedstreck och därefter frågans namn.

Uppdatera `persistedQueryName` variabeln för att använda den beständiga frågan som du skapade i föregående modul. Om du följde namnförslaget exakt skulle du ha skapat en beständig fråga med namnet `adventures` i `your-project` -projektet och du ställer in `persistedQueryName` variabel till `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

När den här ändringen har gjorts bör programmet uppdatera automatiskt och skriva ut det råa JSON-svaret från din beständiga fråga till `#output` div. Om du ser ett felmeddelande bör du kontrollera konsolen för mer information.

Innehåller denna JSON exakt de egenskaper som din app behöver? Om inte, gå tillbaka till AEM Author Environment, Tools, GraphQL Query Editor (eller gå till `/aem/graphiql.html` sökvägar) och gör ändringar i den beständiga frågan. Glöm inte att spara och publicera frågan när du är klar.

## Ändra JSON-återgivning {#change-rendering}

För närvarande återges JSON som i en `pre` -tagg, som inte är särskilt kreativ. Vi kan byta CodePen för att använda `resultToDom()` i stället för att visa hur JSON-svaret kan itereras över för att skapa ett mer intressant resultat.

Gör den här ändringen genom att kommentera rad 37 och ta bort kommentaren från rad 40:

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

Den här funktionen återger även alla bilder som ingår i JSON-svaret som `img` -tagg. Om de&quot;Adventure&quot;-innehållsfragment som du har skapat inte innehåller några bilder kan du försöka med att växla till `aem-demo-assets/adventures-all` beständig fråga genom att ändra rad 25:

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

Den här frågan ger ett JSON-svar som innehåller bilder och `resultToDom()` funktionen återger dem textbundet.

![Resultat av frågan adventures-all och renderingsfunktionen resultToDom](assets/do-not-localize/adventures-all-query-result.png)
