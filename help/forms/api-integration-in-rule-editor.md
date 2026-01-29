---
title: Integrera API i regelredigeraren för Forms
description: Läs om de senaste förbättringarna av Invoke Service i regelredigeraren, inklusive hur du integrerar API:er för adaptiv Forms baserat på kärnkomponenter utan att använda en formulärdatamodell.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: integrera API i regelredigeraren, anropa tjänstförbättringar
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: 478b9c21e5b96dc31f5926a49864ea867e1ae86c
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Integrera API i regelredigeraren

<span>Integrering av API i regelredigeraren sker under Tidigt Adobe-program. Du kan skriva till `aem-forms-ea@adobe.com` från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen.</span>

>[!NOTE]
>
> Visual Rule Editor stöder API-integrering i Adaptive Forms baserat på Core Components och [Edge Delivery Services Forms som skapats i Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

Visual Rule Editor i Adaptive Forms stöder direkt API-integrering utan att skapa en formulärdatamodell. Du kan ansluta till en API-slutpunkt genom att antingen ange API-URL:en (i JSON-format) eller importera konfigurationen med ett cURL-kommando. När åtgärden **Anropa tjänst** har integrerats kan den användas för att anropa API:t.

Formulärfält kan mappas direkt till de indataparametrar som definieras i API-konfigurationen. På samma sätt kan utdataparametrar mappas till formulärfält med alternativet **händelsenyttolast** för motsvarande API-svar.

Med Visual Rule Editor kan du dessutom definiera **success** - och **error-hanterare** när du anropar en tjänst. Hanterare för lyckade åtgärder anger vilka åtgärder som ska utföras efter ett lyckat API-anrop, medan felhanterare definierar hur formuläret ska svara när ett fel inträffar.

## Jämförelse: API-integreringsmetoder

| Proportioner | API-integrering med FDM (Form Data Model) | Direkt API-integrering (via *Skapa API-integrering*) |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **Syfte** | Centraliserad, återanvändbar API-integrering för flera formulär | Snabb, formulärspecifik API-integrering |
| **Installationsplats** | Skapad och redigerad i formulärdatamodellredigeraren (AEM-konsol) | Skapat och redigerat direkt i redigeraren för anpassade formulärregler |
| **Komplexitet** | Högre installationsinsats (kräver mappning och konfiguration) | Enkel och lätt |
| **Passar bäst för** | Användningsexempel i storskala eller företag med flera blanketter | Små formulär, prototyper eller enstaka API-anrop |

## Konfiguration av API-integrering

Skärmbilden nedan visar konfigurationsfönstret för API-integrering:

![API-integreringskonfiguration](/help/forms/assets/api-integration-configuration.png)

### Alternativ för nyckelkonfiguration

**API-integreringskonfiguration**

* **Importera från cURL**: Konfigurera API-integreringen genom att klistra in ett färdigt cURL-kommando i stället för att manuellt ange information som API-URL, HTTP-metod, rubriker och parametrar.
* **Visningsnamn**: Anpassat namn för API-tjänsten.
* **API-URL**: API-tjänstens slutpunkt.
* **Välj HTTP-metod**: Den HTTP-förfrågningsmetod som används för att anropa API:t.
* **Innehållstyp**: Definierar begärande- och svarsformatet.
* **Kryptering krävs**: (Valfritt) Ser till att känsliga data krypteras under överföring.
* **Kör på klienten**: När detta är aktiverat görs API-anropet från klienten (webbläsaren) i stället för från servern.

**Autentiseringstyp**

* **Alternativ**: Ingen, Grundläggande, API-nyckel, OAuth 2.0.

**Indataparametrar**

* **Överför JSON för indata**: Överför en JSON-exempelfil för att automatiskt fylla i indatamappningar.
   * **Namn**: Indataparameternamnet som krävs av API:t.
   * **Typ**: Datatypen för indata (String, Number, Boolean osv.).
   * **In**: Parameterns plats (fråga, huvud eller brödtext).
   * **Standardvärde**: Förfyllt värde om det inte anges av användaren.
   * **Lägg till**: Alternativ för att lägga till ytterligare indataparametrar.

**Utdataparametrar**

* **Överför JSON för utdata**: Överför ett exempel-API-svar för automatisk generering av mappningar.
   * **Namn**: Utdataparameternamn från API-svaret.
   * **Typ**: Datatypen för utdataparametern förväntades (String, Number osv.).
   * **In**: Definierar var det mappade värdet förväntas.
   * **Lägg till/ta bort**: Lägg till nya mappningar eller ta bort befintliga.

## Användningsfall: Fylla i fält för land i en ansökningsblankett för visum

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**Scenario**: En myndighet tillhandahåller ett onlineansökningsformulär för Visa med följande fält:

1. Fullständigt namn (text)
2. Födelsedatum (datum)
3. Medborgarskap (nedrullningsbar lista)
4. Passport-nummer (text)
5. Land för utfärdande av pass (nedrullningsbar lista)
6. Destinationsland (listruta)
7. Planerat ankomstdatum (datum)

Istället för att underhålla en statisk lista över länder hämtar formuläret dynamiskt landsinformation (kontinent, huvudstad, ISO Alpha-koder osv.) med **getCountryName API**:

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

Detta gör att de sökande alltid ser en uppdaterad och korrekt lista över länder samtidigt som de fyller i formuläret.

### Implementering med API-integrering i regelredigeraren

Du kan integrera ett API utan att skapa en formulärdatamodell genom att klicka på knappen **Skapa API-integrering** i regelredigeraren.

![Skapa API-integrering](/help/forms/assets/create-api-integration.png)

En API-tjänst med namnet **getCountryName** har konfigurerats under **API-integreringskonfiguration** i regelredigeraren:

![Konfiguration av API-vila för slutpunkt](/help/forms/assets/api-restendpoint.png)

* **URL för API-slutpunkt** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* **HTTP-metod** → GET
* **Innehållstyp** → JSON
* **Indata** → `username` skickas som en frågeparameter (`aemforms`).
* **Utdata** → Svarsfält som `continent`, `capital`, `countrynames`, `isoAlpha3` och `languages` mappas till formulärfält.

I **formuläret för viseringsansökan** är de tre listrutefälten, **Land för medborgarskap**, **Land för Passport-utfärdande** och **Destinationsland**, bundna till åtgärden **Anropa tjänst** .

När formuläret läses in hämtar **Invoke Service** listan över länder från API:t. Svaret mappas sedan för att automatiskt fylla i alternativen i listrutan.

När användaren till exempel öppnar **Land där han/hon är medborgare** visas listan över länder dynamiskt från API-svaret.

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![API-integreringsutdata](/help/forms/assets/api-integration-output.png)

På samma sätt använder **Land för Passport-utfärdande** och **destinationsland** samma API-anrop för att säkerställa konsekventa och aktuella data i alla tre fälten.

>
>
> Du kan [hämta egenskapsvärden från en JSON-array genom att anropa ett API och använda en anpassad funktion &#x200B;](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array). På så sätt kan du extrahera värden och binda dem direkt till formulärfält.

## Implementera återförsöksmekanism för API-fel

När en API-begäran misslyckas är det ofta användbart att försöka utföra begäran igen innan ett fel rapporteras till användaren. Du kan implementera en avsöknings- och återförsöksmekanism genom att skriva egen kod i filen **function.js** .

I följande exempel visas hur du hanterar API-fel med upp till två återförsök och exponentiell säkerhetskopiering mellan återförsök:

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

I ovanstående kod hanterar funktionen **retryHandler** API-begäranden med automatiska försök om fel uppstår. Den tar en begärandefunktion (requestFn) och försöker utföra begäran upp till två gånger, och lägger till metadata för varje nytt försök.

## Vanliga frågor

* **Behöver jag skapa en formulärdatamodell för att integrera ett API i adaptiv Forms?**\
  Nej. Med Visual Rule Editor kan du integrera API:er direkt med alternativet **Skapa API-integrering** utan att skapa en formulärdatamodell. Den här metoden lämpar sig bäst för enkla eller formulärspecifika användningsområden.

* **Kan jag skydda API-anrop från regelredigeraren?**\
  Ja. API-integreringskonfigurationen innehåller autentiseringsalternativ som **Basic, API Key och OAuth 2.0**. Du kan även aktivera **Kryptering krävs** för att säkerställa att känsliga data överförs på ett säkert sätt.
