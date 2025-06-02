---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 67416999d068af6350748d610e7c1c7b1d991bc4
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# Forms Submission Service med Edge Delivery Services Forms

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande med ditt GitHub-organisationsnamn och databasnamn från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>

Med tjänsten Forms Submission kan du lagra data från de inskickade formulären i alla kalkylblad, t.ex. OneDrive, SharePoint eller Google Sheets, så att du enkelt kan komma åt och hantera formulärdata på den kalkylbladsplattform du föredrar.

![Forms överföringstjänst](/help/forms/assets/form-submission-service.png)

## Fördelar med att använda tjänsten Forms Submission

Några fördelar med att använda Forms Submission Service med kalkylblad är:

* **Direktintegrering**: Du kan konfigurera formulär så att de skickar data direkt till ett visst kalkylblad, vilket eliminerar behovet av manuell dataöverföring.
* **Datastruktur**: När du konfigurerar överföringen kan du mappa formulärfält till motsvarande kalkylbladskolumner för organiserad datalagring.
* **Åtkomstkontroll**: Du kan använda befintliga behörigheter för att styra vem som kan få åtkomst till och ändra skickade formulärdata, beroende på vilken kalkylbladstjänst som valts.

## Krav

Nedan visas förutsättningarna för att använda Forms Submission-tjänsten:

* Kontrollera att ditt AEM-projekt har det senaste adaptiva formulärblocket.
* Se till att din Git-databas har lagts till på tillåtelselista för att använda Forms inskickningstjänst. [mailto:aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) med ditt GitHub-organisationsnamn och databasnamn om du vill att de ska läggas till i tillåtelselista för att använda Forms överföringstjänst.

## Konfigurera tjänsten Forms Submit

Skapa ett nytt AEM-projekt som har konfigurerats med Adaptive Forms Block. Läs artikeln [Komma igång - självstudiekurs för utvecklare](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) om du vill veta mer om hur du skapar ett nytt AEM-projekt. Uppdatera filen `fstab.yaml` i ditt projekt. Ersätt den befintliga referensen med sökvägen till mappen som du har delat med `forms@adobe.com`.

Du kan [konfigurera Forms Submission Service manuellt](#configuring-the-forms-submission-service-manually) eller [konfigurera Forms Submission Service med API](#configuring-the-forms-submission-service-using-api).

### Konfigurera Forms Submission Service manuellt

![Arbetsflöde för tjänsten för att skicka formulär](/help/forms/assets/forms-submission-service-workflow.png)

#### &#x200B;1. Skapa ett formulär med en formulärdefinition

Skapa ett formulär med Google Sheets eller Microsoft Excel. [Klicka här](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms) om du vill lära dig hur du skapar ett formulär med en formulärdefinition i Microsoft Excel eller Google Sheets.

Skärmbilden nedan visar formulärdefinitionen som används för att skapa formuläret:

![Formulärdefinition](/help/forms/assets/form-submission-definition.png)

>[!IMPORTANT]
>
>**Det blad där formuläret har skapats har begränsningar för vad det kan namnges. Endast `helix-default` och `shared-aem` kan användas som bladnamn.**

#### &#x200B;2. Aktivera kalkylbladet så att data accepteras.

När du har skapat och förhandsgranskat formuläret kan du aktivera motsvarande kalkylblad för att börja ta emot data. lägg till ett nytt blad som `incoming`. Du kan [manuellt aktivera kalkylbladet för att ta emot data](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data).

![Inkommande blad](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> Om bladet `incoming` inte finns skickar AEM inga data till arbetsboken.

#### &#x200B;3. Dela kalkylbladet och skapa en länk.

Så här delar du kalkylbladet till kontot `forms@adobe.com` och skapar en länk:

1. Klicka på knappen **Dela** i det övre högra hörnet i Excel- eller Google-blad.
1. Lägg till kontot `forms@adobe.com` och
klicka på ögonikonen, välj **Redigera** åtkomst och klicka på **Skicka** .

   ![Dela inkommande blad](/help/forms/assets/form-submission-share-incoming.png)

1. Om du vill kopiera kalkylbladslänken klickar du på knappen **Dela** i det övre högra hörnet och väljer **Kopiera länk**.

   ![Kopiera länk för inkommande blad](/help/forms/assets/form-submission-copy-link.png)

#### &#x200B;4. Länka kalkylbladet i formulärdefinitionen

Så här konfigurerar du Forms Submission-tjänsten med Google Sheets eller Microsoft Excel:

1. Öppna det kalkylblad som innehåller formulärdefinitionen.
1. Klistra in den kopierade kalkylbladslänken i kolumnen **Åtgärd** i raden som motsvarar fältet **Skicka**.

   ![Länka ett kalkylblad](/help/forms/assets/form-submission-sheet-linking.png)

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/docs/sidekick) med den uppdaterade tjänsten för formuläröverföring.

>[!NOTE]
>
> Du kan referera till [kalkylbladet](/help/forms/assets/spreadsheet.xlsx) för att använda tjänsten Forms Submission.

### Konfigurera Forms Submission Service med API

Du kan också skicka en **POST**-begäran till formuläret för att uppdatera `incoming`-bladet med data.

>[!NOTE]
>
> * Om bladet `incoming` inte finns skickar AEM inga data till arbetsboken.
> * Dela bladet `incoming` med Adobe Experience Manager `forms@adobe.com` och ge redigeringsåtkomst.
> * Förhandsgranska och publicera `incoming`-bladet i sidosparken.

Mer information om hur du formaterar POST-begäran för att konfigurera bladet finns i [API-dokumentationen](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/). Du kan titta på exemplet nedan:

Du kan använda verktyg som curl eller Postman för att utföra denna POST-begäran, vilket visas nedan.

* **Använda Postman**:

Skicka till exempel begäran nedan i Postman efter att ha ersatt:
* `{id}` med ditt formulär-ID
* `site or repository` med ditt GitHub-databas eller webbplatsnamn
* `organization` med ditt GitHub-användarnamn

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

Om du klickar på knappen **Skicka** i Postman returneras ett `201 Created`-svar, och bladet `incoming` uppdateras med skickade data.

![postmansskärm](/help/forms/assets/postman-api.png)

* **Använder kommandot Rulla**:

Kör till exempel följande kommando i terminal eller kommandotolk när du har ersatt:
* `{id}` med ditt formulär-ID
* `site or repository` med ditt GitHub-databas eller webbplatsnamn
* `organization` med ditt GitHub-användarnamn


>[!BEGINTABS]

>[!TAB För macOS]

    &quot;json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
    —header &quot;Content-Type: application/json&quot; \
    —header &quot;x-adobe-routing: tier=live,bucket=main—[plats/databas]—[organisation]&quot; \
    —data &#39;&lbrace;
    &quot;data&quot;: 
    &quot;startDate&quot;: &quot;2 025-01-10&quot;,
    &quot;endDate&quot;: &quot;2025-01-25&quot;,
    &quot;destination&quot;: &quot;Australia&quot;,
    &quot;class&quot;: &quot;First Class&quot;,
    &quot;budget&quot;: &quot;2000&quot;,
    &quot;amount&quot;: &quot;100 00000&quot;,
    &quot;name&quot;: &quot;Joe&quot;,
    &quot;age&quot;: &quot;35&quot;,
    &quot;subscribe&quot;: null,
    &quot;email&quot;: &quot;mary@gmail.com&quot;
    &rbrace;
    &#39;
    
    &quot;

>[!TAB För Windows OS]

    &quot;json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
    —header &quot;Content-Type: application/json&quot; ^
    —header &quot;x-adobe-routing: tier=live,bucket=main—[plats/databas]—[organisation]&quot; ^
    —data &quot;{\&quot;data\&quot;: {\&quot;startDate\&quot;: \&quot;20 25-01-10\&quot;, \&quot;slutdatum\&quot;: \&quot;2025-01-25\&quot;, \&quot;mål\&quot;: \&quot;Australien\&quot;, \&quot;klass\&quot;: \&quot;första klass\&quot;, \&quot;budget\&quot;: \&quot;2000\&quot;, \&quot;belopp\&quot;: \&quot;100 0000, \&quot;namn\&quot;: \&quot;Joe\&quot;, \&quot;ålder\&quot;: \&quot;35\&quot;, \&quot;prenumerera\&quot;: null, \&quot;e-post\&quot;: \&quot;mary@gmail.com\&quot;}}&quot;
    
    &quot;

>[!ENDTABS]

Ovannämnda POST-begäran uppdaterar `incoming`-bladet med följande svar:

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

Skärmen nedan visar skärmbilden för bladet `incoming` som uppdaterats av data som skickats med API:

![uppdaterat blad](/help/forms/assets/updated-sheet.png)

## Se även

{{see-more-forms-eds}}