---
title: Universal Editor Overview for AEM Developers
description: Om du är AEM-utvecklare och är intresserad av hur den universella redigeraren fungerar och hur du använder den i ditt projekt ger det här dokumentet dig en heltäckande introduktion genom att leda dig genom att instrumentera WKND-projektet så att det fungerar tillsammans med den universella redigeraren.
exl-id: d6f9ed78-f63f-445a-b354-f10ea37b0e9b
feature: Developing
role: Admin, Developer
source-git-commit: 392fdb0a0c1982f9be59cb530e86f13aeea3316b
workflow-type: tm+mt
source-wordcount: '3179'
ht-degree: 0%

---


# Universal Editor Overview for AEM Developers {#developer-overview}

Om du är AEM-utvecklare och är intresserad av hur den universella redigeraren fungerar och hur du använder den i ditt projekt ger det här dokumentet dig en heltäckande introduktion genom att leda dig genom att instrumentera WKND-projektet så att det fungerar tillsammans med den universella redigeraren.

## Syfte {#purpose}

Det här dokumentet är en introduktion för utvecklare av både hur den universella redigeraren fungerar och hur du kan mäta hur programmet fungerar med det.

Den gör detta genom att ta ett standardexempel som de flesta av AEM utvecklare känner till, Core Components och WKND, och instrumentera några exempelkomponenter som kan redigeras med Universal Editor.

>[!TIP]
>
>Det här dokumentet innehåller extra steg som illustrerar hur den universella redigeraren fungerar och är avsett att fördjupa utvecklarens förståelse för redigeraren. Det är därför inte den mest direkta vägen till att instrumentera ett program, utan det mest illustrativa i den universella redigeraren och hur det fungerar.
>
>Om du vill komma igång så snabbt som möjligt kan du läsa dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md) .

## Förutsättningar {#prerequisites}

Du behöver följande för att kunna följa med i den här översikten.

* [En lokal utvecklingsinstans av AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)
   * Din lokala utvecklingsinstans måste vara [konfigurerad med HTTPS för utvecklingssyfte på `localhost`](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html).
   * [WKND-demowebbplatsen måste vara installerad](https://github.com/adobe/aem-guides-wknd).
* [Åtkomst till Universal Editor](/help/implementing/universal-editor/getting-started.md#onboarding).
* [En lokal Universal Editor-tjänst](/help/implementing/universal-editor/local-dev.md) som körs i utvecklingssyfte.
   * Ange att webbläsaren ska [acceptera det självsignerade certifikatet för lokala tjänster](/help/implementing/universal-editor/local-dev.md#editing).

Förutom att man är van vid webbutveckling utgår man i det här dokumentet från att man är van vid AEM utveckling. Om du inte är van vid AEM-utveckling bör du överväga att granska [WKND-självstudiekursen innan du fortsätter](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

## Starta AEM och logga in i den universella redigeraren {#sign-in}

Om du inte redan har det måste du ha din lokala AEM-utvecklingsinstans installerad med WKND och HTTPS aktiverat som [enligt villkoren](#prerequisites). Den här översikten förutsätter att din instans körs på `https://localhost:8443`.

1. Öppna mallsidan för WKND English i AEM Editor.

   ```text
   https://localhost:8443/editor.html/content/wknd/language-masters/en.html
   ```

1. Välj **Visa som publicerad** på menyn **Sidinformation** i redigeraren. Då öppnas samma sida på en ny flik där AEM Editor är inaktiverat.

   ```text
   https://localhost:8443/content/wknd/language-masters/en.html?wcmmode=disabled
   ```

1. Kopiera länken.

1. Logga nu in på Universal Editor.

   ```text
   https://experience.adobe.com/#/aem/editor
   ```

1. Klistra in länken som du kopierade tidigare av WKND-innehållet i fältet **Webbplats-URL** i den universella redigeraren och klicka på **Öppna**.

   ![Öppna WKND-sidan i den universella redigeraren](assets/dev-ue-open.png)

## Universal Editor försöker läsa in innehållet {#sameorigin}

Universal Editor läser in innehåll som ska redigeras i en ram. AEM standardinställningar för X-Frame-alternativ förhindrar detta, som tydligt kan ses som ett fel i webbläsaren och som visas i konsolutdata när du försöker läsa in din lokala kopia av WKND.

![Webbläsarfel på grund av SAMEORIGIN-alternativet](assets/dev-sameorigin.png)

Alternativet X-Frame `sameorigin` förhindrar återgivning av AEM-sidor i en bildruta. Du måste ta bort det här sidhuvudet för att sidorna ska kunna läsas in i Universal Editor.

1. Öppna Configuration Manager.

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. Redigera OSGi-konfigurationen `org.apache.sling.engine.impl.SlingMainServlet`

   ![OSGi-egenskap för SAMEORIGIN](assets/dev-sameorigin-osgi.png)

1. Ta bort egenskapen `X-Frame-Options=SAMEORIGIN` för egenskapen **Ytterligare svarshuvuden**.

1. Spara ändringarna.

Om du läser in den universella redigeraren ser du att AEM-sidan läses in.

>[!TIP]
>
>* Mer information om OSGi-konfigurationen finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#sameorigin).
>* Mer information om OSGi i AEM finns i dokumentet [Konfigurera OSGi för Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Hantera samma webbplatskookies {#samesite-cookies}

När Universal Editor läser in din sida, läses den in till inloggningssidan för AEM för att säkerställa att du är autentiserad att göra ändringar.

Du kan dock inte logga in. När du visar webbläsarkonsolen ser du att webbläsaren har blockerat indata i bildrutan

![Indata blockerad](assets/dev-cross-origin.png)

Inloggningstokens cookie skickas till AEM som en tredjepartsdomän. Därför måste cookies från samma webbplats vara tillåtna i AEM.

1. Öppna Configuration Manager.

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. Redigera OSGi-konfigurationen `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`

   ![OSGi-egenskap för cookies för samma webbplats](assets/dev-cross-origin-osgi.png)

1. Ändra egenskapen **SameSite-attributet för cookien** för inloggningstoken till `Partitioned`.

1. Spara ändringarna.

Om du nu läser in den universella redigeraren igen kan du logga in på AEM och målsidan läses in.

>[!TIP]
>
>* Mer information om OSGi-konfigurationen finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#samesite-cookies).
>* Mer information om OSGi i AEM finns i dokumentet [Konfigurera OSGi för Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Universell redigerare Ansluter till fjärrramen {#ue-connect-remote-frame}

När sidan har lästs in i Universal Editor och du har loggat in på AEM försöker den universella redigeraren ansluta till fjärrbildrutan. Detta görs via ett JavaScript-bibliotek som måste läsas in i fjärrbildrutan. Om JavaScript-biblioteket inte finns skapas ett timeout-fel i konsolen.

![Timeout-fel](assets/dev-timeout.png)

Du måste lägga till det nödvändiga JavaScript-biblioteket till sidkomponenten i WKND-appen.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Redigera filen `/apps/wknd/components/page` under `customheaderlibs.html`.

   ![Redigera filen customheaderlibs.html](assets/dev-customheaderlibs.png)

1. Lägg till JavaScript-biblioteket i slutet av filen.

   ```html
   <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
   ```

1. Klicka på **Spara alla** och läs sedan in den universella redigeraren igen.

Sidan läses nu in med rätt JavaScript-bibliotek så att den universella redigeraren kan ansluta till sidan och timeoutfelet visas inte längre i konsolen.

>[!TIP]
>
>* Biblioteket kan läsas in antingen i sidhuvudet eller i sidfoten.

>[!NOTE]
>
>Den tidigare rekommenderade metoden att inkludera JavaScript-biblioteket, `<script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST"></script>` eller via npmjs.com rekommenderas inte längre eftersom paketet har tagits bort.
>
>Om ett program fortfarande använder det föråldrade paketet visas en varning i gränssnittet om att ett föråldrat paket identifieras.

## Definiera en anslutning för att behålla ändringar {#connection}

WKND-sidan läses nu in korrekt i Universal Editor och JavaScript-biblioteket läses in för att ansluta redigeraren till din app.

Du har dock troligen lagt märke till att du inte kan interagera med sidan i Universalläsaren. Universal Editor kan inte redigera sidan. För att den universella redigeraren ska kunna redigera innehållet måste du definiera en anslutning så att den vet var innehållet ska skrivas. För lokal utveckling måste du skriva tillbaka till din lokala AEM-utvecklingsinstans på `https://localhost:8443`.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Redigera filen `/apps/wknd/components/page` under `customheaderlibs.html`.

   ![Redigera filen customheaderlibs.html](assets/dev-instrument-app.png)

1. Lägg till de metadata som behövs för anslutningen till den lokala AEM-instansen i slutet av filen.

   ```html
   <meta name="urn:adobe:aue:system:aem" content="aem:https://localhost:8443">
   ```

   * Den senaste versionen av biblioteket rekommenderas alltid. Om du behöver en tidigare version läser du dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#alternative).

1. Lägg till de metadata som behövs för anslutningen till den lokala Universal Editor-tjänsten i slutet av filen.

   ```html
   <meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
   ```

1. Klicka på **Spara alla** och läs sedan in den universella redigeraren igen.

Nu kan den universella redigeraren inte bara läsa in ditt innehåll från den lokala AEM-utvecklingsinstansen, utan du vet också var ändringarna ska sparas i den lokala universella redigeringstjänsten. Det här är det första steget när du ska göra ditt program redigerbart med den universella redigeraren.

>[!TIP]
>
>* Mer information om anslutningsmetadata finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#connection).
>* Mer information om strukturen för den universella redigeraren finns i dokumentet [Universal Editor Architecture](/help/implementing/universal-editor/architecture.md#service).
>* Se dokumentet [Local AEM Development with the Universal Editor](/help/implementing/universal-editor/local-dev.md) för mer information om hur du ansluter till en självvärdbaserad version av Universal Editor.

## Instrumenting Components {#instrumenting-components}

Men du märker antagligen att du fortfarande inte kan göra så mycket med den universella redigeraren. Om du försöker klicka på lagret högst upp på WKND-sidan i Universalläsaren kan du inte markera det (eller något annat på sidan).

Komponenterna måste också vara instrumenterade för att kunna redigeras med den universella redigeraren. Om du vill göra det måste du redigera teaserkomponenten. Därför måste du täcka över kärnkomponenterna eftersom kärnkomponenterna är under `/libs`, som inte kan ändras.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Markera noden `/libs/core/wcm/components` och klicka på **Överläggsnod** i verktygsfältet.

1. Med `/apps/` markerat som **plats för övertäckning** klickar du på **OK**.

   ![Täck över lagret](assets/dev-overlay-teaser.png)

1. Markera noden `teaser` under `/libs/core/wcm/components` och klicka på **Kopiera** i verktygsfältet.

1. Markera den överlappande noden på `/apps/core/wcm/components` och klicka på **Klistra in** i verktygsfältet.

1. Dubbelklicka på filen `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` för att redigera den.

   ![Redigera filen teaser.html](assets/dev-edit-teaser.png)

1. Lägg till instrumenteringsinformation för komponenten i slutet av den första `div` på ungefär rad 26.

   ```text
   data-aue-resource="urn:aem:${resource.path}"
   data-aue-type="component"
   data-aue-label="Teaser"
   ```

1. Klicka på **Spara alla** i verktygsfältet och läs in den universella redigeraren igen.

1. Klicka på teaserkomponenten överst på sidan i Universalläsaren och se att du nu kan markera den.

1. Om du klickar på ikonen **Innehållsträd** på egenskapspanelen i den universella redigeraren ser du att redigeraren känner igen alla scener på sidan nu när du har instrumenterat den. Det lager du valde är det som är markerat.

   ![Markera den instrumenterade teaserkomponenten](assets/dev-select-teaser.png)

>[!TIP]
>
>Mer information om att täcka över noder finns i dokumentet [Använda sammanslagningen av delningsresurser i Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/sling-resource-merger.md).

## Teaser-underkomponenterna för instrument {#subcomponents}

Nu kan du markera suddgummit, men fortfarande inte redigera det. Detta beror på att teaser är en sammansättning av olika komponenter som bild- och titelkomponenten. Du måste mäta dessa underkomponenter för att kunna redigera dem.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Markera noden `/apps/core/wcm/components/teaser/v2/teaser/` och dubbelklicka på filen `title.html`.

   ![Redigera filen title.html](assets/dev-edit-title.png)

1. Infoga följande egenskaper i slutet av taggen `h2` (nära rad 17).

   ```text
   data-aue-prop="jcr:title"
   data-aue-type="text"
   data-aue-label="Title"
   ```

1. Klicka på **Spara alla** i verktygsfältet och läs in den universella redigeraren igen.

1. Klicka på titeln för samma teaser-komponent överst på sidan och se att du nu kan markera den. Innehållsträdet visar också titeln som en del av den valda teaserkomponenten.

   ![Välj en titel i lagret](assets/dev-select-title.png)

Nu kan du redigera teaserkomponentens titel!

## Vad betyder allt det? {#what-does-it-mean}

Nu när du kan redigera teaser titel ska vi titta på vad du har gjort och hur.

Du har identifierat teaser-komponenten för Universal Editor genom att instrumentera den.

* `data-aue-resource` identifierar resursen i AEM som redigeras.
* `data-aue-type` definierar att objekten ska behandlas som en sidkomponent (till skillnad från en behållare).
* `data-aue-label` visar en användarvänlig etikett i användargränssnittet för det valda lagret.

Du har även instrumenterat titelkomponenten i teaserkomponenten.

* `data-aue-prop` är JCR-attributet som är skrivet.
* `data-aue-type` är så attributet ska redigeras. I det här fallet med textredigeraren eftersom det är en titel (till skillnad från RTF-redigeraren).

## Definiera autentiseringsrubriker {#auth-header}

Nu kan du redigera titeln på teaser in-line och ändringarna sparas i webbläsaren.

![Redigerad titel på teaser](assets/dev-edited-title.png)

Om du läser in webbläsaren igen läses den tidigare titeln in igen. Detta beror på att även om den universella redigeraren kan ansluta till din AEM-instans kan redigeraren ännu inte autentisera till din AEM-instans för att skriva tillbaka ändringar i JCR.

Om du visar nätverksfliken för webbläsarutvecklarverktygen och söker efter `update`, kan du se att det uppstår ett 401-fel när du försöker redigera titeln.

![Fel vid försök att redigera titeln](assets/dev-edit-error.png)

När du använder Universal Editor för att redigera ditt AEM-material använder den universella redigeraren samma IMS-token som du använde för att logga in på redigeraren för att autentisera till AEM för att underlätta återskrivningen till JCR.

När du utvecklar lokalt kan du inte använda AEM identitetsleverantör eftersom IMS-tokens bara skickas till Adobe-ägda domäner. Du måste manuellt ange ett sätt att autentisera genom att explicit ange en autentiseringshuvud.

1. Klicka på ikonen **Autentiseringshuvuden** i verktygsfältet i det universella redigeringsgränssnittet.

1. Kopiera den autentiseringsrubrik som krävs för att autentisera den lokala AEM-instansen och klicka på **Spara**.

   ![Konfigurerar autentiseringsrubriker](assets/dev-authentication-headers.png)

1. Läs in den universella redigeraren igen och redigera nu teaser titel.

Det finns inte längre några fel rapporterade i webbläsarkonsolen och ändringarna sparas sedan i den lokala AEM-utvecklingsinstansen.

Om du undersöker trafiken i webbläsarens utvecklingsverktyg och letar efter händelserna `update` kan du se uppdateringens detaljer.

![Teaser title har redigerats](assets/dev-edit-title-successfully.png)

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

* `connections` är anslutningen till din lokala AEM-instans
* `target` är den exakta noden och de egenskaper som uppdateras i JCR
* `value` är den uppdatering du har gjort.

Du kan se ändringen som finns kvar i JCR.

![Uppdatera i JCR](assets/dev-write-back-jcr.png)

>[!TIP]
>
>Det finns många verktyg tillgängliga online för att generera nödvändiga autentiseringshuvuden för dina test- och utvecklingssyften.
>
>Det grundläggande exemplet `Basic YWRtaW46YWRtaW4=` för autentiseringshuvudet gäller kombinationen `admin:admin` för användare/lösenord, vilket är vanligt vid lokal AEM-utveckling.

## Instrumentera appen för egenskapspanelen {#properties-rail}

Du har nu ett program som är instrumenterat för att kunna redigeras med Universal Editor!

Redigeringen är för närvarande begränsad till redigering av teaserns titel. Det finns dock tillfällen när redigering på plats inte räcker. Text som t.ex. teaserns titel kan redigeras där den finns med tangentbordsinmatning. Men mer komplicerade objekt måste kunna visas och tillåta redigering av strukturerade data som skiljer sig från hur de återges i webbläsaren. Det här är vad egenskapspanelen är till för.

Om du vill uppdatera appen så att den använder egenskapspanelen för redigering går du tillbaka till sidhuvudfilen för sidkomponenten i appen. Här har du redan upprättat anslutningarna till den lokala AEM-utvecklingsinstansen och den lokala universella redigeringstjänsten. Här måste du definiera de komponenter som är redigerbara i programmet och deras datamodeller.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Redigera filen `/apps/wknd/components/page` under `customheaderlibs.html`.

   ![Redigera filen customheaderlibs.html](assets/dev-instrument-properties-rail.png)

1. Till slutet av filen lägger du till det skript som behövs för att definiera komponenterna.

   ```html
   <script type="application/vnd.adobe.aue.component+json">
   {
     "groups": [
       {
         "title": "General Components",
         "id": "general",
         "components": [
           {
             "title": "Teaser",
             "id": "teaser",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/teaser"
                 }
               }
             }
           },
           {
             "title": "Title",
             "id": "title",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/title"
                 }
               }
             }
           }
         ]
       }
     ]
   }
   </script>
   ```

1. Under det lägger du till det skript som behövs för att definiera modellen i slutet av filen.

   ```html
   <script type="application/vnd.adobe.aue.model+json">
   [
     {
       "id": "teaser",
       "fields": [
         {
           "component": "text-input",
           "name": "jcr:title",
           "label": "Title",
           "valueType": "string"
         },
         {
           "component": "text-area",
           "name": "jcr:description",
           "label": "Description",
           "valueType": "string"
         }
       ]
     },
     {
       "id": "title",
       "fields": [
         {
           "component": "select",
           "name": "type",
           "value": "h1",
           "label": "Type",
           "valueType": "string",
           "options": [
             { "name": "h1", "value": "h1" },
             { "name": "h2", "value": "h2" },
             { "name": "h3", "value": "h3" },
             { "name": "h4", "value": "h4" },
             { "name": "h5", "value": "h5" },
             { "name": "h6", "value": "h6" }
           ]
         }
       ]
     }
   ]
   </script>
   ```

1. Klicka på **Spara alla** i verktygsfältet.

## Vad betyder allt det? {#what-does-it-mean-2}

Om du vill kunna redigera med egenskapspanelen måste komponenterna tilldelas `groups`, så varje definition börjar som en lista med grupper som innehåller komponenterna.

* `title` är namnet på gruppen.
* `id` är gruppens unika identifierare, i det här fallet allmänna komponenter som utgör sidinnehållet i motsats till avancerade komponenter för sidlayout, till exempel.

Varje grupp har sedan en matris på `components`.

* `title` är namnet på komponenten.
* `id` är den unika identifieraren för komponenten, i det här fallet en teaser.

Varje komponent har sedan en plugin-definition som definierar hur komponenten mappas till AEM.

* `aem` är det plugin-program som hanterar redigeringen. Detta kan ses som den tjänst som bearbetar komponenten.
* `page` definierar vilken typ av komponent det är, i det här fallet en standardsidkomponent.
* `resourceType` är mappningen till den faktiska AEM-komponenten.

Varje komponent måste sedan mappas till en `model` för att definiera de enskilda redigerbara fälten.

* `id` är modellens unika identifierare, som måste matcha komponentens ID.
* `fields` är en array med de enskilda fälten.
* `component` är den typ av indata som t.ex. text eller textområde.
* `name` är fältnamnet i den JCR som fältet mappas till.
* `label` är beskrivningen av fältet som visas i redigerarens användargränssnitt.
* `valueType` är datatypen.

## Instrumentera komponenten för egenskapspanelen {#properties-rail-component}

Du måste också definiera på komponentnivå vilken modell komponenten ska använda.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Dubbelklicka på filen `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` för att redigera den.

   ![Redigera filen teaser.html](assets/dev-edit-teaser.png)

1. I slutet av den första `div` på ungefär rad 32, efter de egenskaper du lade till tidigare, lägger du till instrumenteringsinformation för modellen som den teaserkomponenten ska använda.

   ```text
   data-aue-model="teaser"
   ```

1. Klicka på **Spara alla** i verktygsfältet och läs in den universella redigeraren igen.

Nu kan du testa egenskapspanelen som är instrumenterad för komponenten.

1. Klicka en gång till på teaser i Universal Editor för att redigera den.

1. Klicka på egenskapspanelen för att visa egenskapsfliken och visa fälten som du just instrumenterat.

   ![Panelen med instrumenterade egenskaper](assets/dev-properties-rail-instrumented.png)

Nu kan du redigera teaser-objektets titel antingen direkt som du gjorde tidigare eller i egenskapspanelen. I båda fallen sparas ändringarna i den lokala AEM-utvecklingsinstansen.

## Lägg till ytterligare fält i egenskapspanelen {#add-fields}

Med hjälp av den grundläggande strukturen i datamodellen för komponenten som du redan har implementerat kan du lägga till ytterligare fält enligt samma modell.

Du kan till exempel lägga till ett fält för att justera komponentens format.

1. Öppna CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Redigera filen `/apps/wknd/components/page` under `customheaderlibs.html`.

   ![Redigera filen customheaderlibs.html](assets/dev-instrument-styles.png)

1. Lägg till ytterligare ett objekt i `fields`-arrayen för formatfältet i modelldefinitionsskriptet. Kom ihåg att lägga till ett kommatecken efter det sista fältet innan du infogar det nya.

   ```json
   {
      "component": "select",
      "name": "cq:styleIds",
      "label": "Style",
      "valueType": "string",
        "multi": true,
      "options": [
        {"name": "hero", "value":"1555543212672"},
        {"name": "card", "value":"1605057868937"}
      ]
   }
   ```

1. Klicka på **Spara alla** i verktygsfältet och läs in den universella redigeraren igen.

1. Klicka en gång till på teaserns titel för att redigera den.

1. Klicka på egenskapspanelen och se att det finns ett nytt fält för att justera komponentens stil.

   ![Den instrumenterade egenskapspanelen med formatfältet](assets/dev-style-instrumented.png)

Alla fält i JCR för komponenten kan visas på det här sättet i Universal Editor.

## Sammanfattning {#summary}

Grattis! Nu kan du instrumentera dina egna AEM-program så att de fungerar tillsammans med den universella redigeraren.

När du börjar instrumentera ditt eget program bör du tänka på de grundläggande steg du utförde i det här exemplet.

1. [Du konfigurerar utvecklingsmiljön](#prerequisites).
   * AEM körs lokalt på HTTPS med WKND installerat
   * Universell redigeringstjänst som körs lokalt på HTTPS
1. Du har uppdaterat inställningarna för AEM OSGi så att dess innehåll kan läsas in på fjärrbasis.
   * [`org.apache.sling.engine.impl.SlingMainServlet`](#sameorigin)
   * [`com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`](#samesite-cookies)
1. [Du har lagt till biblioteket `universal-editor-embedded.js` i filen `customheaderlibs.html` för sidkomponenten i appen &#x200B;](#ue-connect-remote-frame).
1. [Du har definierat en anslutning som ska innehålla ändringar i `customheaderlibs.html`-filen för sidkomponenten i appen &#x200B;](#connection).
   * Du definierade en anslutning till den lokala AEM-utvecklingsinstansen.
   * Du har även definierat en anslutning till den lokala tjänsten Universal Editor.
1. [Du har instrumenterat teaserkomponenten](#instrumenting-components).
1. [Du har instrumenterat underkomponenterna för teaser](#subcomponents).
1. [Du har definierat ett anpassat autentiseringshuvud så att du kan spara ändringar med den lokala universella redigeringstjänsten](#auth-header).
1. [Du instrumenterade programmet för att använda egenskapspanelen](#properties-rail).
1. [Du instrumenterade teaserkomponenten för att använda egenskapspanelen](#properties-rail-component).

Du kan följa dessa steg för att mäta hur din egen app kan användas med den universella redigeraren. Alla egenskaper i JCR kan visas för den universella redigeraren.

## Ytterligare resurser {#additional-resources}

Titta på följande dokument för mer information om funktionerna i den universella redigeraren.

* Om du vill komma igång så snabbt som möjligt kan du läsa dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md) .
* Mer information om nödvändiga OSGi-konfigurationer finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#sameorigin).
* Mer information om anslutningsmetadata finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#connection).
* Mer information om strukturen för den universella redigeraren finns i dokumentet [Universal Editor Architecture](/help/implementing/universal-editor/architecture.md#service).
* Se dokumentet [Local AEM Development with the Universal Editor](/help/implementing/universal-editor/local-dev.md) för mer information om hur du ansluter till en självvärdbaserad version av Universal Editor.
* Mer information om att täcka över noder finns i dokumentet [Använda sammanslagningen av delningsresurser i Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/sling-resource-merger.md).

