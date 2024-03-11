---
title: Skapa ett formulär med dokumentbaserad redigering för AEM Forms Edge Delivery Service
description: Skapa perfekta formulär, snabbt! ⚡ AEM Forms Edge Delivery + doc-based authoring = blazingerande hastighet & SEO-vänliga formulär för nöjdare användare och sökmotorer.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# Skapa ett formulär med dokumentbaserad redigering för AEM Forms Edge Delivery Service

I dagens digitala samhälle är det viktigt för alla företag att skapa användarvänliga formulär. Med dokumentbaserad redigering i AEM Forms Edge Delivery kan du skapa formulär med välbekanta verktyg som Word eller Google Docs. Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft Sharepoint för att enkelt bearbeta inlämnade data eller för att starta ett befintligt arbetsflöde.

Den här guiden leder dig igenom:

* Förbereda kalkylbladet: Lär dig hur du konfigurerar en Excel- eller Google-bladfil för datainsamling och lägger till formulärfält i den.
* Skicka data till bladet: Lär dig att skicka data till bladet med hjälp av POSTER.
* Publicera formuläret: Integrera formuläret på din AEM Sites-sida eller publicera det som en fristående sida.

Oavsett om du är nybörjare eller proffs ger den här guiden dig möjlighet att skapa snygga, funktionella formulär som användarna gillar. Låt oss låsa upp effektivt skapande av formulär - dyk in nu!

## Innan du börjar

`WIP`

## Förbered kalkylbladet för att ta emot data

1. Skapa en Microsoft Excel-arbetsbok eller ett Google-blad var som helst under AEM Edge Delivery-projektkatalog på Microsoft OneDrive eller Google Drive. Det här dokumentet använder ett Google-blad med namnet `contact-us.xlsx`, som finns i roten av ett Adobe Experience Manager-projekt (AEM).

1. Kontrollera att AEM användare (till exempel helix@adobe.com) som är konfigurerad för ditt projekt har redigeringsbehörighet för bladet.

1. Öppna arbetsboken som du har skapat och ändra namnet på standardbladet till &quot;inkommande&quot;.

   >[!NOTE]
   >
   > Om det inkommande bladet inte finns kommer AEM inte att skicka några data till den här arbetsboken.

1. Förhandsgranska bladet i sidosparken.

   >[!NOTE]
   >
   >Även om du har förhandsgranskat bladet tidigare måste du förhandsgranska det igen när du har skapat det inkommande bladet för första gången.

1. Förbered bladet genom att lägga till rubriker som matchar de data du skickar in. I följande exempel visas fält för ett kontaktformulär:

   ![Fält för ett kontaktformulär](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   Du kan göra detta manuellt eller genom att använda en begäran om POST i formulärflödet i AEM Admin-tjänsten. Administrationstjänsten undersöker informationen i POSTEN och genererar de rubriker, tabeller och blad som behövs för att effektivt kunna importera data och få ut det mesta av blanketttjänsten.

   Om du vill veta hur du formaterar POSTEN för att konfigurera bladet kan du läsa [Dokumentation för Admin API](https://www.hlx.live/docs/admin.html#tag/form). Ta också en titt på exemplet nedan:

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
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

Om du föredrar att skapa rubrikerna manuellt bör du läsa dokumentet Admin Service [Manuell inställning av Forms-blad](https://www.hlx.live/docs/manual-forms-sheet-setup).

När du skickar en begäran om POST till administratörstjänsten kommer du att se följande ändringar i arbetsboken:

* Ett nytt blad med namnet&quot;shared-default&quot; läggs till i Excel-arbetsboken eller Google-bladet. Data som finns i bladet&quot;shared-default&quot; hämtas när en GET begärs till bladet. Denna docka fungerar som en optimal plats där du kan använda kalkylbladsformler för att sammanfatta inkommande data, vilket gör den lättare att använda i andra sammanhang.

  Under inga omständigheter får det&quot;delade standardformuläret&quot; innehålla någon personligt identifierbar information eller känsliga data som du inte känner dig bekväm med att vara tillgänglig för allmänheten.

* Ett blad med namnet&quot;slack&quot; läggs till i Excel-arbetsboken eller Google-bladet. I det här bladet kan du konfigurera automatiska meddelanden för en angiven Slack-kanal när nya data hämtas till kalkylbladet. För närvarande stöder AEM endast meddelanden till AEM Engineering Slack och Adobe Enterprise Support.

   1. Om du vill konfigurera Slack-meddelanden anger du teamId för arbetsytan i Slack och kanalnamnet eller ID:t. Du kan också fråga en robot (med felsökningskommandot) för teamId och channel ID. Det är bättre att använda kanal-ID i stället för kanalnamn eftersom kanalens namn bevaras.

      >[!NOTE]
      >
      > Äldre formulär hade inte kolumnen teamId. &quot;teamId&quot; inkluderades i kanalkolumnen, avgränsad med &quot;#&quot; eller &quot;/&quot;.

   1. Ange en titel som du vill ha och under fält anger du namnen på de fält som du vill se i Slack-meddelandet. Varje rubrik ska avgränsas med kommatecken (till exempel namn, e-post).

Blanketten är nu konfigurerad för att ta emot data och du kan skicka POST-förfrågningar direkt till den med hlx.page, hlx.live eller din produktionsdomän.


## Skicka data till bladet {#send-data-to-your-sheet}

När kalkylbladet är inställt på att ta emot data kan du skicka POST-förfrågningar direkt till det med hlx.page, hlx.live eller din produktionsdomän för att skicka data.

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL:en ska inte ha filnamnstillägget .json. Du måste publicera bladet för att POST-åtgärder ska fungera på .live eller i produktionsdomänen.

### Formatera data för EDS Forms

Det finns olika sätt att formatera formulärdata i POSTENS brödtext.

* Array med namn:värdepar:

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
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* Objekt med nyckel:värdepar

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

* `x-www-form-urlencoded` brödtext (`content-type` header must set to `application/x-www-form-urlencoded`) &#39;firstName=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



