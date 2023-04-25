---
title: Återge ditt innehåll i en enkel app
description: Upptäck hur du hämtar JSON-innehåll från testmiljön med exempelappen CodePen och den AEM Headless Client för JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 3bfecf4d577c8cb81b1c1cf02b1f9299277fbc8b
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---


# Återge ditt innehåll i en enkel app {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Återge ditt innehåll i en enkel app"
>abstract="Upptäck hur du hämtar JSON-innehåll från testmiljön med exempelappen CodePen och den AEM Headless Client för JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Starta exempelappen CodePen"
>abstract="Den här guiden går igenom frågor om JSON-data från testmiljön till en grundläggande JavaScript-webbapp. Vi kommer att använda de innehållsavsnitt du modellerade och skapade i de tidigare utbildningsmodulerna, så gå igenom dessa handledningar innan du går in i den här.<br><br>För att visa hur innehåll kan hämtas från ett JavaScript-webbprogram har vi skapat en CodePen som du kan använda som den är, eller förgrena till ditt eget konto för att anpassa ytterligare."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="I den här modulen lärde du dig att använda den AEM Headless Client för JavaScript för att hämta JSON-data från testmiljön med GraphQL beständiga frågor.<br><br>Nu förstår ni hur ni kan använda den här klienten för att förbruka data från ert eget webbprogram."
>abstract=""

## CodePen-app {#codepen-app}

CodePen är en kodredigerare och en lekplats för webbutveckling. Du kan skriva HTML, CSS och JavaScript-kod i webbläsaren och se resultatet nästan direkt. Du kan också spara ditt arbete och dela det med andra. Vi har skapat en CodePen-app som du kan använda för att hämta JSON-data från testmiljön med [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js). Du kan använda den här appen som den är eller fördela den till ditt eget CodePen-konto för att anpassa den ytterligare.

När du klickar på knappen &quot;Starta&quot; ovan kommer du till CodePen-appen, som fungerar som ett minimalt exempel på hämtning av JSON-data med JavaScript. Exempelappen är utformad för att återge allt JSON-innehåll som returneras, oavsett strukturen för den underliggande modellen för innehållsfragment. Programmet hämtar data från en `aem-demo-assets` Beständig fråga som ingår i testmiljön. Du bör se ett JSON-svar som liknar följande:

```
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

Om du får ett felmeddelande i stället kan du kontrollera om webbläsarkonsolen innehåller mer information eller kontakta oss [på Slack](https://adobe-dx-support.slack.com).

Därefter konfigurerar du appen så att den hämtar data från den beständiga fråga som du skapade i en tidigare modul.

## Genomgång av JavaScript-kod {#code-walkthrough}

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

På rad 25 anger vi vilken GraphQL-fråga som appen ska hämta data från. Det beständiga frågenamnet är en kombination av slutpunktens namn (dvs. `your-project` eller `aem-demo-assets`), följt av ett snedstreck och därefter frågans namn. Om du följde instruktionerna från den tidigare modulen exakt, kommer den beständiga fråga du skapade att finnas i `your-project` slutpunkt.

1. Uppdatera `persistedQueryName` variabeln för att använda den beständiga frågan som du skapade i föregående modul. Om du följde namnförslaget skulle du ha skapat en beständig fråga med namnet `adventure-list` i `your-project` slutpunkt, och du anger `persistedQueryName` variabel till `your-project/adventure-list`:

```javascript
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventure-list';
```

1. När den här ändringen har gjorts bör programmet uppdatera automatiskt och skriva ut det råa JSON-svaret från din beständiga fråga till `#output` div. Om du ser ett felmeddelande bör du kontrollera konsolen för mer information. Nå ut till oss [på Slack](https://adobe-dx-support.slack.com) om du fortfarande har problem med det här steget.

1. Innehåller denna JSON exakt de egenskaper som din app behöver? Om inte, gå tillbaka till [Extrahera innehåll med GraphQL API](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) utbildningsguide för att göra ändringar. Glöm inte att spara och publicera frågan när du är klar.

## Ändra JSON-återgivning {#change-rendering}

För närvarande återges JSON som i en `pre` -tagg, som inte är särskilt kreativ. Vi kan byta CodePen för att använda `resultToDom()` i stället för att visa hur JSON-svaret kan itereras över för att skapa ett mer intressant resultat.

1. Gör den här ändringen genom att kommentera rad 37 och ta bort kommentaren från rad 40:

```javascript
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

1. Den här funktionen återger även alla bilder som ingår i JSON-svaret som `img` -tagg. Om de&quot;Adventure&quot;-innehållsfragment som du har skapat inte innehåller några bilder kan du försöka med att växla till `aem-demo-assets/adventures-all` beständig fråga genom att ändra rad 25:

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

Den här frågan ger ett JSON-svar som innehåller bilder och `resultToDom()` funktionen återger dem textbundet.

![Resultat av frågan adventures-all och renderingsfunktionen resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Nu när du har gjort jobbet med att skapa modeller och frågor kan ditt innehållsteam enkelt ta över. Vi visar innehållsförfattarflödet i nästa modul.
