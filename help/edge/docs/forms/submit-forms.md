---
title: Förbered kalkylbladet för att ta emot data
description: Skapa kraftfulla formulär snabbare med kalkylblad och formulärblocksfält!
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Förbered kalkylbladet för att ta emot data

En gång har du [skapade och förhandsvisade formuläret](/help/edge/docs/forms/create-forms.md)är det dags att aktivera motsvarande kalkylblad så att det kan börja ta emot data.

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

Aktivera kalkylbladet:

1. Öppna kalkylbladet som innehåller formuläret och lägg till ett nytt blad och ge det ett nytt namn `incoming`.

   >[!WARNING]
   >
   > Om `incoming` bladet finns inte, AEM skickar inga data till kalkylbladet.

1. Spegla formulärfältsnamnen, värden för `Name` kolumn i`shared-default` kalkylblad, till rubrikerna i `incoming` blad.

   Varje värde i `Name` kolumn i `shared-default` kalkylbladet, med undantag för skicka-knappen, fungerar som en rubrik i `incoming` blad. Titta på följande bild som illustrerar rubriker för ett&quot;kontaktformulär&quot;:

   ![Fält för ett kontaktformulär](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Förhandsgranska bladet med hjälp av en sidospark.

   >[!NOTE]
   >
   >Även om du har förhandsgranskat bladet tidigare måste du förhandsgranska det igen när du har skapat `incoming` första gången.


När fältnamnen har lagts till i `incoming` kan du godkänna att ditt formulär skickas vidare. Du kan förhandsgranska formuläret och skicka data till bladet med hjälp av det.

Du kan även se följande ändringar i kalkylbladet:

Ett blad med namnet &quot;Slack&quot; läggs till i Excel-arbetsboken eller Google-bladet. I det här bladet kan du konfigurera automatiska meddelanden för en angiven Slack-kanal när nya data hämtas till kalkylbladet. För närvarande stöder AEM endast meddelanden till AEM Engineering Slack och Adobe Enterprise Support.

1. Om du vill konfigurera Slack-meddelanden anger du teamId för arbetsytan i Slack och kanalnamnet eller ID:t. Du kan också fråga en robot (med felsökningskommandot) för teamId och channel ID. Det är bättre att använda kanal-ID i stället för kanalnamn eftersom kanalens namn bevaras.

   >[!NOTE]
   >
   > Äldre formulär hade inte kolumnen teamId. &quot;teamId&quot; inkluderades i kanalkolumnen, avgränsad med &quot;#&quot; eller &quot;/&quot;.

1. Ange en titel som du vill ha och skriv under fält namnen på de fält som du vill se i Slack-meddelandet. Varje rubrik ska avgränsas med kommatecken (till exempel namn, e-post).

   >[!WARNING]
   >
   >  De ska aldrig innehålla någon personligt identifierbar information eller känsliga data som du inte känner till om de är tillgängliga för allmänheten.


## (Valfritt) Använd admin-API:er för att aktivera ett kalkylblad som accepterar data

Du kan också skicka en begäran om POST till formuläret så att det kan ta emot data och konfigurera rubriker för `incoming` blad. När tjänsten tar emot en begäran om POST analyserar tjänsten innehållet i begäran och skapar automatiskt de huvuden och ark som behövs för datainhämtning.

Så här använder du Admin API:er för att aktivera ett kalkylblad för att ta emot data:


1. Öppna arbetsboken som du har skapat och ändra namnet på standardbladet till `incoming`.

   >[!WARNING]
   >
   > Om `incoming` bladet finns inte, AEM skickar inga data till arbetsboken.

1. Förhandsgranska bladet i sidosparken.

   >[!NOTE]
   >
   >Även om du har förhandsgranskat bladet tidigare måste du förhandsgranska det igen när du har skapat `incoming` första gången.

1. Skicka begäran om POST för att generera lämpliga rubriker i `incoming` och lägg till `shared-default` till uppslagsbladet, om det inte redan finns.

   Om du vill veta hur du formaterar POSTEN för att konfigurera bladet kan du läsa [Dokumentation för Admin API](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Du kan titta på exemplet nedan:

   **Begäran**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
   --header 'Content-Type: application/json' \
   --data '{
       "data": {
           "Email": "john@wknd.com",
           "Name": "John",
           "Subject": "Regarding Product Inquiry",
           "Message": "I have some questions about your products.",
           "Phone": "123-456-7890",
           "Company": "Adobe Inc.",
           "Country": "United States",
           "PreferredContactMethod": "Email",
           "SubscribeToNewsletter": true
       }
   }'
   ```


   **Svar**

   ```JSON
   HTTP/2 200 
   content-type: application/json
   x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
   cache-control: no-store, private, must-revalidate
   accept-ranges: bytes
   date: Sat, 10 Feb 2024 09:26:48 GMT
   via: 1.1 varnish
   x-served-by: cache-del21736-DEL
   x-cache: MISS
   x-cache-hits: 0
   x-timer: S1707557205.094883,VS0,VE3799
   strict-transport-security: max-age=31557600
   content-length: 138
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   Du kan använda verktyg som curl eller Postman för att utföra denna begäran om POST, vilket visas nedan:

   ```JSON
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
       --header 'Content-Type: application/json' \
       --data '{
           "data": {
               "Email": "john@wknd.com",
               "Name": "John",
               "Subject": "Regarding Product Inquiry",
               "Message": "I have some questions about your products.",
               "Phone": "123-456-7890",
               "Company": "Wknd Inc.",
               "Country": "United States",
               "PreferredContactMethod": "Email",
               "SubscribeToNewsletter": true
       }
   }'
   ```

   Ovannämnda POST innehåller exempeldata, inklusive både formulärfält och deras respektive exempelvärden. Dessa data används av administrationstjänsten för att konfigurera formuläret.

   Formuläret är nu aktiverat för att ta emot data. Du kan även se följande ändringar i kalkylbladet:

Ett blad med namnet &quot;Slack&quot; läggs till i Excel-arbetsboken eller Google-bladet. I det här bladet kan du konfigurera automatiska meddelanden för en angiven Slack-kanal när nya data hämtas till kalkylbladet. För närvarande stöder AEM endast meddelanden till AEM Engineering Slack och Adobe Enterprise Support.

1. Om du vill konfigurera Slack-meddelanden anger du teamId för arbetsytan i Slack och kanalnamnet eller ID:t. Du kan också fråga en robot (med felsökningskommandot) för teamId och channel ID. Det är bättre att använda kanal-ID i stället för kanalnamn eftersom kanalens namn bevaras.

   >[!NOTE]
   >
   > Äldre formulär hade inte kolumnen teamId. &quot;teamId&quot; inkluderades i kanalkolumnen, avgränsad med &quot;#&quot; eller &quot;/&quot;.

1. Ange en titel som du vill ha och skriv under fält namnen på de fält som du vill se i Slack-meddelandet. Varje rubrik ska avgränsas med kommatecken (till exempel namn, e-post).


Blanketten är nu konfigurerad för att ta emot data, du kan [förhandsgranska formuläret med hjälp av adaptivt formulärblock](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) eller [använd POST-förfrågningar](#use-admin-apis-to-send-data-to-your-sheet) för att börja skicka data till bladet.

>[!WARNING]
>
>  De ska aldrig innehålla någon personligt identifierbar information eller känsliga data som du inte känner till om de är tillgängliga för allmänheten.

## Skicka data till bladet {#send-data-to-your-sheet}

När bladet är inställt på att ta emot data kan du [förhandsgranska formuläret med hjälp av adaptivt formulärblock](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) eller [använd admin-API:er](#use-admin-apis-to-send-data-to-your-sheet) för att börja skicka data till bladet.

### Använd admin-API:er för att skicka data till bladet

Du kan skicka POST-förfrågningar direkt till ditt formulär med hlx.page, hlx.live eller din produktionsdomän för att skicka data.


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL:en ska inte ha filnamnstillägget .json. Du måste publicera bladet för att POSTEN ska fungera på `.live` eller på produktionsdomänen.

#### Formatera formulärdata

Det finns olika sätt att formatera formulärdata i POSTENS brödtext. Du kan använda

* array med `name:value` par:

  ```JSON
  {
    "data": [
      { "name": "name", "value": "Clark Kent" },
      { "name": "email", "value": "superman@example.com" },
      { "name": "subject", "value": "Regarding Product Inquiry" },
      { "name": "message", "value": "I have some questions about your products." },
      { "name": "phone", "value": "123-456-7890" },
      { "name": "company", "value": "Example Inc." },
      { "name": "country", "value": "United States" },
      { "name": "preferred_contact_method", "value": "Email" },
      { "name": "newsletter_subscribe", "value": true }
    ]
  }
  ```

  Till exempel

  ```JSON
  curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
      --header 'Content-Type: application/json' \
      --data '{
      "data": [
          { "name": "name", "value": "Clark Kent" },
          { "name": "email", "value": "superman@example.com" },
          { "name": "subject", "value": "Regarding Product Inquiry" },
          { "name": "message", "value": "I have some questions about your        products." },
          { "name": "phone", "value": "123-456-7890" },
          { "name": "company", "value": "Example Inc." },
          { "name": "country", "value": "United States" },
          { "name": "preferred_contact_method", "value": "Email" },
          { "name": "newsletter_subscribe", "value": true }
      ]
  }'
  ```



* ett objekt med `key:value` par:

  ```JSON
      {
        "data": {
          "name": "Jessica Jones",
          "email": "jj@example.com",
          "subject": "Regarding Product Inquiry",
          "message": "I have some questions about your products.",
          "phone": "123-456-7890",
          "company": "Example Inc.",
          "country": "United States",
          "preferred_contact_method": "Email",
          "newsletter_subscribe": true
        }
      }
  ```

  Exempel:

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
  --header 'Content-Type: application/json' \
  --data '{
      "data": {
          "Email": "khushwant@wknd.com",
          "Name": "khushwant",
          "Subject": "Regarding Product Inquiry",
          "Message": "I have some questions about your products.",
          "Phone": "123-456-7890",
          "Company": "Adobe Inc.",
          "Country": "United States",
          "PreferredContactMethod": "Email",
          "SubscribeToNewsletter": true
      }
  }'
  ```

* URL-kodad (`x-www-form-urlencoded`) body (with `content-type` sidhuvud inställt på `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  Exempel:

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

Sedan kan du anpassa tackmeddelandet, [konfigurera en tacksida](/help/edge/docs/forms/thank-you-page-form.md), eller [ange omdirigeringar](/help/edge/docs/forms/thank-you-page-form.md).

## Se mer

* [Skapa och förhandsgranska ett formulär](/help/edge/docs/forms/create-forms.md)
* [Aktivera formulär för att skicka data](/help/edge/docs/forms/submit-forms.md)
* [Publicera ett formulär på webbplatssidan](/help/edge/docs/forms/publish-eds-forms.md)
* [Lägga till valideringar i formulärfält](/help/edge/docs/forms/validate-forms.md)
* [Ändra teman och format för formulär](/help/edge/docs/forms/style-theme-forms.md)
