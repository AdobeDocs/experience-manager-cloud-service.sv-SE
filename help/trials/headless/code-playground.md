---
title: Återge ditt innehåll i en enkel app
description: Upptäck hur du hämtar JSON-innehåll från testmiljön med exempelappen CodePen och den AEM Headless Client för JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '971'
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
>abstract="Den här guiden går igenom frågor om JSON-data från testmiljön till en grundläggande JavaScript-webbapp. Du använder de innehållsfragment som du modellerade och skapade i de tidigare utbildningsmodulerna. Om det behövs kan du gå igenom de här stödlinjerna innan du hoppar in i den här."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="I den här modulen lärde du dig att använda den AEM Headless Client för JavaScript för att hämta JSON-data från testmiljön med hjälp av GraphQL beständiga frågor.<br><br>Nu förstår ni hur ni kan använda den här klienten för att förbruka data från ert eget webbprogram."
>abstract=""

## CodePen {#codepen}

CodePen är en kodredigerare och en lekplats för webbutveckling. Du kan skriva HTML, CSS och JavaScript-kod i webbläsaren och se resultatet nästan direkt. Du kan också spara ditt arbete och dela det med andra. Adobe har skapat en app i CodePen som du kan använda för att hämta JSON-data från testmiljön med [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js). Du kan använda den här appen som den är eller fördela den till ditt eget CodePen-konto för att anpassa den ytterligare.

Klicka på **Starta exempelappen CodePen** från testversionen tar dig till programmet i CodePen. Appen fungerar som ett minimalt exempel på hämtning av JSON-data med JavaScript. Exempelappen är utformad för att återge allt JSON-innehåll som returneras, oavsett strukturen för den underliggande modellen för innehållsfragment. Programmet hämtar data direkt från en `aem-demo-assets` beständig fråga som ingår i testmiljön. Du bör se ett JSON-svar som liknar följande:

```json
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

Om du får ett felmeddelande i stället bör du kontrollera webbläsarkonsolen för mer information eller kontakta [via e-post](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request).

Nu när du känner till lite om CodePen konfigurerar du appen så att den hämtar data från den beständiga fråga du skapade i en tidigare modul.

## JavaScript-kod, genomgång {#code-walkthrough}

The **JS** till höger i CodePen innehåller JavaScript för exempelappen. Från och med rad 2 importerar du den AEM Headless-klienten för JavaScript från Skypack CDN. Skypack används för att underlätta utvecklingen utan ett steg, men du kan även använda AEM Headless Client med NPM eller Garn i dina egna projekt. Läs användningsinstruktionerna i [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) för mer information.

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

På rad 6 lästes informationen om din publiceringsvärd in från `publishHost` frågeparameter. Den här parametern är värddatorn som AEM Headless Client hämtar data från. Den här funktionen kodas vanligtvis i appen, men du använder en frågeparameter för att göra det enklare för CodePen-appen att arbeta i olika miljöer.

Du konfigurerar AEM Headless Client på rad 12:

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs ({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>The **serviceURL** är inställt på att använda en proxy-Adobe I/O Runtime-funktion för att undvika CORS-problem. Denna proxy krävs inte för dina egna projekt, men krävs för att CodePen-appen ska fungera med din testmiljö. Proxyfunktionen är konfigurerad att använda **publishHost** värdet som angavs i frågeparametern.

Slutligen, funktionen `fetchJsonFromGraphQL()` används för att utföra hämtningsbegäran med AEM Headless Client. Den anropas varje gång koden ändras eller kan aktiveras genom att du klickar på **Uppdatera** länk. Den faktiska `aemHeadlessClient.runPersistedQuery(..)` samtal inträffar på rad 34. lite senare ändrar du hur dessa JSON-data återges, men skriver nu ut dem på `#output` div med `resultToPreTag(queryResult)` funktion.

## Hämta data från din beständiga fråga {#use-persisted-query}

På rad 25 anger du från vilken GraphQL beständig fråga appen ska hämta data. Namnet på den beständiga frågan är en kombination av namnet på slutpunkten (det vill säga, `your-project` eller `aem-demo-assets`), följt av ett snedstreck och därefter frågans namn. Om du följde instruktionerna från den tidigare modulen exakt finns den beständiga frågan som du skapade i `your-project` slutpunkt.

1. Uppdatera `persistedQueryName` så att den beständiga frågan som du skapade i föregående modul används. Om du följde namnförslaget skulle du ha skapat en beständig fråga med namnet `adventure-list` i `your-project` slutpunkt, och du anger `persistedQueryName` variabel till `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. När den här ändringen har gjorts bör programmet uppdatera automatiskt och skriva ut det råa JSON-svaret från din beständiga fråga till `#output` div. Om du ser ett felmeddelande bör du kontrollera konsolen för mer information. Nå ut [via e-post](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request) om du fortfarande har problem med det här steget.

1. Innehåller denna JSON exakt de egenskaper som din app behöver? Om inte, gå tillbaka till [Extrahera innehåll med GraphQL API](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) utbildningsguide för att göra ändringar. Glöm inte att spara och publicera frågan när du är klar.

## Ändra JSON-återgivning {#change-rendering}

JSON återges som i en `pre` -tagg, som inte är för kreativ. Du kan växla CodePen för att använda `resultToDom()` i stället för att visa hur JSON-svaret kan itereras över för att skapa ett mer intressant resultat.

1. Gör den här ändringen genom att kommentera rad 37 och ta bort kommentaren från rad 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Den här funktionen återger alla bilder som ingår i JSON-svaret som `img` -tagg. Om **Adventure** innehållsfragment som du har skapat innehåller inga bilder, du kan försöka växla till `aem-demo-assets/adventures-all` beständig fråga genom att ändra rad 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Den här frågan ger ett JSON-svar som innehåller bilder och `resultToDom()` funktionen återger dem textbundet.

![Resultat av frågan adventures-all och renderingsfunktionen resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Nu när du har gjort jobbet med att skapa modeller och frågor kan ditt innehållsteam enkelt ta över. I nästa modul visar du innehållsförfattarflödet.
