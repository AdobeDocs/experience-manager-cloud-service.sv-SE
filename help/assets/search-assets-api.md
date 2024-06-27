---
title: Sök i Assets API
description: Lär dig använda API:t för sökning i Assets.
role: User
source-git-commit: 3e2fe458460fe8ec4c1dd12152c1134bfb9ca62b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Sök i Assets API {#search-assets-api}

Alla [godkända tillgångar](approve-assets.md) som finns i Experience Manager-resurskatalogen kan sökas igenom och sedan levereras till integrerade program längre fram i kedjan med en leverans-URL.

Att söka efter rätt godkända resurser från Experience Manager-databasen är det första steget mot att leverera resurser med hjälp av URL:en för leverans. Svaret på sökbegäran består av en array med JSON-dokument som motsvarar de resurser som uppfyller sökvillkoren. Varje JSON-dokument identifieras med en `id` -fält, som används för att disponera över resursleveransen.

![Översikt över protokollet för direkt binär överföring](assets/search-assets-api-overview.png)

Du kan definiera egenskaper i Search Assets API-begäran för att aktivera följande funktioner:

* **Fulltextsökning**: Använd `match` fråga för att definiera texten som ska sökas igenom.  Du kan också använda operatorer i `match` -fråga för att filtrera resultaten.

* **Använda filter**: Använd `term` fråga för att filtrera resultaten ytterligare genom att definiera en `key` och ett eller flera värden. `key` identifierar fältet vars värde måste matchas och `value` representerar det som ska matchas. På samma sätt kan du använda `range` -fråga för att definiera ett intervall för ett fält med hjälp av egenskaperna Större än (gt), Större än eller lika med (gte), Mindre än (lt) och Mindre än eller lika med (lte).

* **Sortera resultat**: Använd `OrderBy` för att sortera sökresultat baserat på ett eller flera fält. Du kan sortera resultatet i stigande eller fallande ordning.

* **Sidnumrering**: Använd `limit` och `cursor` egenskaper för att definiera pagineringsegenskaper i en sökning-API-begäran. `limit` -egenskapen definierar det maximala antalet objekt som ska hämtas i ett API-svar. `cursor` -egenskapen gör det lättare att hämta startpunkten för nästa uppsättning resurser som definieras i `limit` -egenskap. Om du till exempel definierar `50` som gräns i API-begäran kan du använda `cursor` för att starta och hämta nästa 50 objekt med nästa API-begäran.

## API-slutpunkt för sökresurser {#search-assets-api-endpoint}

Slutpunkten i en API-begäran för sökresurser måste ha följande format:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

Leveransdomänen har liknande struktur som Experience Manager författarmiljöns domän. Den enda skillnaden är att ersätta termen `author` med `delivery`.

`pXXXX` refererar till program-ID

`eYYYY` refererar till miljö-ID

## API-begärandemetoden för sökresurser {#search-assets-api-request-method}

POST

## Sök i Assets API-huvud {#search-assets-api-header}

Du måste ange följande information när du definierar en rubrik i API:t för sökresurser:

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

Om du vill anropa API:t för sökning krävs en IMS-token för att definiera i `Authorization` information. IMS-token hämtas från ett tekniskt konto. Se [Hämta AEM as a Cloud Service-autentiseringsuppgifter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) för att skapa ett nytt tekniskt konto. Se [Genererar åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) för att generera IMS-token och använda den på rätt sätt i API-begärandehuvudet för sökresurser.

Information om hur du visar exempel på förfrågningar, svarsexempel och svarskoder finns i [Sök i Assets API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).
