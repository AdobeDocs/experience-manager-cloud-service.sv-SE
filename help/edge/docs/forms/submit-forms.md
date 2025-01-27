---
title: Förbered kalkylbladet för att ta emot data
description: Skapa kraftfulla formulär snabbare med kalkylblad och anpassade Forms-blockfält!
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Architect, Developer
source-git-commit: 552779d9d1cee2ae9f233cabc2405eb6416c41bc
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Konfigurera dina Google-blad eller Microsoft Excel-filer så att du kan börja ta emot data


När du har [skapat och förhandsgranskat formuläret](/help/edge/docs/forms/create-forms.md) är det dags att aktivera motsvarande kalkylblad för att börja ta emot data. Du kan

* [Aktivera kalkylbladet manuellt för att acceptera data](#manually-enable-the-spreadsheet-to-accept-data)
* [Använd admin-API:er för att aktivera ett kalkylblad som accepterar data](#use-admin-apis-to-enable-a-spreadsheet-to-accept-data)

![Dokumentbaserat redigeringssystem](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)


<!--

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

## Aktivera kalkylbladet manuellt för att ta emot data

Aktivera att kalkylbladet accepterar data

1. Öppna kalkylbladet som innehåller ditt formulär och lägg till ett nytt blad och ge det ett nytt namn till `incoming`. [Förfrågan](/help/edge/assets/enquiry.xlsx) är till exempel en Microsoft Excel-arbetsbok.

   >[!WARNING]
   >
   > Om bladet `incoming` inte finns skickar AEM inga data till kalkylbladet.

1. I det här bladet infogar du en tabell med namnet &quot;intag_form&quot;. Välj det antal kolumner som krävs för att matcha formulärfältsnamnen. Gå sedan till Infoga > Tabell i verktygsfältet och klicka på OK.

1. Ändra namnet på tabellen till &quot;intag_form&quot;. Om du vill ändra namnet på tabellen i Microsoft Excel markerar du tabellen och klickar på Tabelldesign.

1. Lägg sedan till formulärfältsnamnen som tabellrubriker. Om du vill vara säker på att fälten är exakt desamma kan du kopiera och klistra in dem från bladet&quot;shared-aem&quot;.  I ditt&quot;shared-aem&quot;-blad markerar och kopierar du de formulär-ID som anges i kolumnen&quot;Name&quot;, förutom i fältet submit.

1. I det inkommande bladet väljer du Klistra in special > Transponera rader till kolumner för att kopiera fält-ID:n som kolumnrubriker i det nya bladet. Behåll endast de fält vars data behöver hämtas från andra fält som kan ignoreras.

   Varje värde i `Name`-kolumnen i `shared-aem` -bladet, förutom skicka-knappen, kan fungera som en rubrik i `incoming` -bladet. Titta på följande bild som illustrerar rubriker i ett frågeformulär:

   ![Fält för ett kontaktformulär](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Använd tillägget [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska formuläruppdateringarna. Ditt blad är nu klart att ta emot inkommande formulärinskickat material.

   >[!NOTE]
   >
   >Även om du har förhandsgranskat bladet tidigare måste du förhandsgranska det igen när du har skapat bladet `incoming` för första gången.


När fältnamnen har lagts till i bladet `incoming` kan ditt formulär ta emot inskickade data. Du kan förhandsgranska formuläret och skicka data till bladet med hjälp av det.

När kalkylbladet har konfigurerats för att ta emot data kan du [förhandsgranska formuläret](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) <!--or [use POST requests](#use-admin-apis-to-send-data-to-your-sheet)--> för att börja skicka data till bladet.

>[!WARNING]
>
>  De får aldrig innehålla någon personligt identifierbar information eller känsliga data som du inte känner till om de är tillgängliga för allmänheten.


## Använd admin-API:er för att aktivera ett kalkylblad som accepterar data

Du kan också skicka en begäran om POST till formuläret så att det kan ta emot data och konfigurera rubriker för bladet `incoming`. När tjänsten tar emot en begäran om POST analyserar tjänsten innehållet i begäran och skapar automatiskt de huvuden och ark som behövs för datainhämtning.

Så här använder du Admin API:er för att aktivera ett kalkylblad för att ta emot data:


1. Öppna arbetsboken som du har skapat och ändra namnet på standardbladet till `incoming`.

   >[!WARNING]
   >
   > Om bladet `incoming` inte finns skickar AEM inga data till arbetsboken.

1. Förhandsgranska bladet i sidosparken.

   >[!NOTE]
   >
   >Även om du har förhandsgranskat bladet tidigare måste du förhandsgranska det igen när du har skapat bladet `incoming` för första gången.

1. Skicka begäran om POST för att generera lämpliga rubriker i `incoming`-bladet och lägg till `shared-default`-bladen i ditt uppslagsblad, om det inte redan finns.

   Mer information om hur du formaterar begäran om POST för att konfigurera bladet finns i [dokumentationen för Admin API](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Du kan titta på exemplet nedan:

   **Begäran**

   ```JSON
   POST 'https://admin.aem.page/form/{owner}/{repo}/{branch}/contact-us.json' \
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
   curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
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

## Automatiska ändringar i bladet när det har aktiverats för att ta emot data.

När kalkylbladet är inställt på att ta emot data kan du se följande ändringar i kalkylbladet:

Ett blad med namnet &quot;Slack&quot; läggs till i Excel-arbetsboken eller Google-bladet. I det här bladet kan du konfigurera automatiska meddelanden för en angiven Slack-kanal när nya data hämtas till kalkylbladet. För närvarande stöder AEM endast meddelanden till AEM Engineering Slack och Adobe Enterprise Support.

1. Om du vill konfigurera Slack-meddelanden anger du teamId för arbetsytan i Slack och kanalnamnet eller ID:t. Du kan också fråga en robot (med felsökningskommandot) för teamId och channel ID. Det är bättre att använda kanal-ID i stället för kanalnamn eftersom kanalens namn bevaras.

   >[!NOTE]
   >
   > Äldre formulär hade inte kolumnen teamId. &quot;teamId&quot; inkluderades i kanalkolumnen, avgränsad med &quot;#&quot; eller &quot;/&quot;.

1. Ange en titel som du vill ha och skriv under fält namnen på de fält som du vill se i Slack-meddelandet. Varje rubrik ska avgränsas med kommatecken (till exempel namn, e-post).

   >[!WARNING]
   >
   >  De ska aldrig innehålla någon personligt identifierbar information eller känsliga data som du inte känner till om de är tillgängliga för allmänheten.



<!--
## Send data to your sheet {#send-data-to-your-sheet}

After the sheet is set to receive data, you can [preview the form using Adaptive Forms Block](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) or [use Admin APIs](#use-admin-apis-to-send-data-to-your-sheet) to start sending data to the sheet.

### Use Admin APIs to send data to your sheet

You can send POST requests directly to your form using aem.page, aem.live, or your production domain, to send data. 


```JSON

POST https://branch–repo–owner.aem.(page|live)/email-form
POST https://my-domain.com/email-form

```

>[!NOTE] 
>
> The URL should not have the .json extension. You must publish the sheet for POST operations to function on `.live` or on the production domain.

#### Formatting the form data

There are a few different ways that you can format the form data in the POST body. You can use: 

* array of `name:value` pairs: 
    
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

    For example

    ```JSON

    curl -s -i -X POST 'https://main--wefinance--wkndform.aem.page/contact-us' \
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



* an object with `key:value` pairs:

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

    For example,

    ```JSON

    curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
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

* URL encoded (`x-www-form-urlencoded`) body (with `content-type` header set to `application/x-www-form-urlencoded`)

    ```Shell

    'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'

    ```

    For example, if your project's repository is named "wefinance", it's located under the account owner "wkndform", and you're using the "main" branch.,

    ```Shell

    curl -s -i -X POST \
      -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
      https://main--wefinance--wkndform.aem.live/contact-us

    ```
-->

Sedan kan du [anpassa tackmeddelandet](/help/edge/docs/forms/thank-you-page-form.md).

## Se även

{{see-more-forms-eds}}
