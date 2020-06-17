---
title: Använda Cloud Readiness Analyzer
description: Använda Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: a53ab47fe954bd48dc34840968a9a47cdcc34556
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 0%

---


# Använda Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Viktigt att tänka på när du använder molnberedskapsanalysen {#imp-considerations}

Följ avsnittet nedan om du vill veta mer om de viktiga sakerna att tänka på när du kör Cloud Readiness Analyzer (CRA):

* CRA-rapporten byggs med hjälp av utdata från Adobe Experience Manager (AEM) [mönsteravkännaren](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html). Den version av Mönsteravkännare som används av CRA ingår i CRA-installationspaketet.

* CRA kan bara köras av **administratörsanvändaren** eller en användare i **administratörerna**.

* CRA stöds på AEM-instanser med version 6.1 och senare.

* CRA kan köras i vilken miljö som helst, men det är bättre att ha det på en *scenmiljö* .

   >[!NOTE]
   >För att undvika att affärskritiska instanser påverkas rekommenderar vi att du kör CRA i en *författarmiljö* som är så nära *produktionsmiljön* som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Alternativt kan det köras på en klon av *författarmiljön* i produktionen.

* Det kan ta lång tid att generera innehållet i en CRA-rapport, från flera minuter till några timmar. Hur lång tid som krävs beror i hög grad på storlek och typ av AEM-databasinnehåll, AEM-version och andra faktorer.

* På grund av den stora tid som kan behövas för att generera rapportinnehållet, genereras de av en bakgrundsprocess och lagras i ett cacheminne. Det bör gå relativt snabbt att visa och hämta rapporten eftersom den använder innehållscachen tills den upphör att gälla eller tills rapporten uppdateras explicit. Under genereringen av rapportinnehåll kan du stänga webbläsarfliken och sedan gå tillbaka och visa rapporten när dess innehåll är tillgängligt i cachen.

## Tillgänglighet {#availability}

Cloud Readiness Analyzer kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via Package Manager på Adobe Experience Manager-källinstansen (AEM).

>[!NOTE]
>Hämta Cloud Readiness Analyzer från Software Distribution Portal.

## Visa Cloud Readiness Analyzer-rapporten {#viewing-report}

### Adobe Experience Manager 6.3.0 och senare {#aem-later-versions}

Följ det här avsnittet för att lära dig hur du visar Cloud Readiness Analyzer-rapporten:

1. Välj Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Cloud Readiness Analyzer**.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. När du klickar på **Cloud Readiness Analyzer** börjar verktyget generera rapporten och visar den när den är tillgänglig.

   >[!NOTE]
   >Du måste rulla nedåt på sidan för att se hela rapporten.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. När CRA-rapporten genereras och visas kan du välja att hämta rapporten med kommaseparerade värden (CSV). Klicka på **CSV** för att ladda ned den fullständiga CRA-rapporten i CSV-format (kommaseparerade värden), vilket visas i bilden nedan.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >Du kan tvinga CRA att rensa sin cache och återskapa rapporten genom att klicka på **Uppdatera rapport**.

### Adobe Experience Manager 6.2 och 6.1 {#aem-specific-versions}

Verktyget Cloud Readiness Analyzer är i Adobe Experience Manager 6.2 begränsat till en länk som genererar och hämtar CSV-rapporten.

För Adobe Experience Manager 6.1 fungerar inte verktyget och bara HTTP-gränssnittet kan användas.

>[!NOTE]
>I alla versioner kan den inkluderade mönsteravkännaren köras oberoende av varandra.

## Tolka Cloud Readiness Analyzer-rapporten {#cra-report}

När verktyget Cloud Readiness Analyzer körs i AEM-instansen visas rapporten som resultat i verktygsfönstret.

Rapportens format är:

* **Rapportöversikt**: Information om själva rapporten och innehåller följande information:
   * **Rapporttid**: När rapportinnehållet genererades och gjordes tillgängligt för första gången.
   * **Förfallotid**: När cachen för rapportinnehåll upphör att gälla.
   * **Tidsperiod** för generering: Den tid som används för att generera rapportinnehåll.
   * **Sökningsantal**: Det totala antalet resultat som ingår i rapporten.
* **Systemöversikt**: Information om det AEM-system som CRA kördes på.
* **Söker efter kategorier**: Flera avsnitt som åtgärdar en eller flera brister i samma kategori. Varje avsnitt innehåller följande: Kategorinamn, undertyper, antal sökningar och deras betydelse, sammanfattning, länk till kategoridokumentation och information om enskild sökning.

Varje upptäckt tilldelas en prioritetsnivå som anger en grov prioritet för åtgärder.

Följ tabellen nedan för att förstå prioritetsnivåerna:

| Prioritet | Beskrivning |
|--- |--- |
| INFORMATION | Denna slutsats lämnas i informationssyfte. |
| RÅDGIVNING | Detta kan vara ett uppgraderingsproblem. Ytterligare undersökningar rekommenderas. |
| STÖRRE | Denna slutsats är sannolikt ett uppgraderingsproblem som bör åtgärdas. |
| KRITISK | Detta är sannolikt ett uppgraderingsproblem som måste åtgärdas för att förhindra funktionsförlust eller prestanda. |


## Tolka CSV-rapporten för Cloud Readiness Analyzer {#cra-csv-report}

När du klickar på alternativet **CSV** från din AEM-instans skapas CSV-formatet för Cloud Readiness Analyzer-rapporten från innehållscachen och returneras till webbläsaren. Beroende på inställningarna i webbläsaren hämtas den här rapporten automatiskt som en fil med standardnamnet `results.csv`.

Om cacheminnet har gått ut genereras rapporten om innan CSV-filen skapas och hämtas.

CSV-formatet för rapporten innehåller information som genereras från utdata för Mönsteravkännare, sorterat och organiserat efter kategorityp, undertyp och prioritetsnivå. Formatet är lämpligt för visning och redigering i program som Microsoft Excel. Avsikten är att ge all sökinformation i ett upprepningsbart format som kan vara användbar vid jämförelse av rapporter över tiden för att mäta förloppet.

Kolumnerna i CSV-formatrapporten är:

* **kod**: kategorikoden
* **typ**: kategorinamnet
* **undertyp**: undertypen av kategori
* **prioritet**: prioritetsnivån
* **identifierare**: den primära identifieraren för sökningen
* **annat**: ytterligare information om sökningen
* **meddelande**: det meddelande som lämnats för sökningen
* **moreInfo**: en länk som du kan använda för att komma åt onlinehjälp om kategorin
* **kontext**: en JSON-sträng med sökdata

Värdet &quot;\N&quot; i en kolumn för en enskild sökning anger att inga data har angetts.

## HTTP-gränssnitt {#http-interface}

CRA tillhandahåller ett HTTP-gränssnitt som kan användas som ett alternativ till användargränssnittet i AEM. Gränssnittet har stöd för både HEAD- och GET-kommandon. Den kan användas för att generera CRA-rapporten och returnera den i ett av tre format: JSON, CSV och tabbseparerade värden (TSV).

Följande URL:er är tillgängliga för HTTP-åtkomst, där `<host>` är värdnamnet och porten, om det behövs, för servern där CRA är installerat:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` för JSON-format
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` för CSV-format
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` för TSV-format

### Köra en HTTP-begäran {#executing-http-request}

HTTP-gränssnittet kan användas på flera olika sätt.

Ett enkelt sätt är att öppna en webbläsarflik i samma webbläsare där du redan har loggat in på AEM som administratör. Du kan ange URL-adressen på fliken Webbläsare och låta resultatet visas eller hämtas av webbläsaren.

Du kan också använda ett kommandoradsverktyg som `curl` eller `wget` alla HTTP-klientprogram. Om du inte använder en webbläsarflik med en autentiserad session måste du ange ett administratörsanvändarnamn och lösenord som en del av kommentaren.

Följande är ett exempel på hur detta kan göras:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### Sidhuvuden och parametrar {#http-headers-and-parameters}

Följande HTTP-huvuden används av det här gränssnittet:

* `Cache-Control: max-age=<seconds>`: Ange livstid för cacheuppdateringarna i sekunder. (Se [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Anger att servern ska svara asynkront. (Se [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)

Följande HTTP-frågeparametrar är bekväma när det är svårt att använda HTTP-rubriker:

* `max-age` (tal, valfritt): Ange livstid för cacheuppdateringarna i sekunder. Talet måste vara 0 eller större. Standardlivstiden för aktualitet är 86400 sekunder, vilket innebär att utan den här parametern eller motsvarande rubrik används ett nytt cacheminne för att hantera begäranden i 24 timmar innan rapporten måste genereras om. Om du använder `max-age=0` kommer cachen att rensas och en omgenerering av rapporten kommer att påbörjas. Omedelbart efter denna begäran återställs aktualitetens livstid till det tidigare värdet som inte är noll.
* `respond-async` (boolesk, valfritt): Ange att svaret ska anges asynkront. Om du använder `respond-async=true` när cachen är inaktiv kommer servern att returnera ett svar `202 Accepted, processing cache` utan att vänta på att rapporten ska skapas och cachen uppdateras. Om cacheminnet är uppdaterat har den här parametern ingen effekt. Standardvärdet är `false`, vilket innebär att utan den här parametern eller motsvarande rubrik kommer servern att svara synkront, vilket kan ta lång tid och kräva en justering av den maximala svarstiden för HTTP-klienten.

När det finns både en HTTP-rubrik och motsvarande frågeparameter får frågeparametern företräde.

Ett enkelt sätt att initiera genereringen av rapporten via HTTP-gränssnittet är med följande kommando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

När en begäran har gjorts behöver klienten inte vara aktiv för att rapporten ska kunna genereras. Rapportgenereringen kan initieras med en klient med en HTTP GET-begäran och när rapporten har genererats visas den från cachen i en annan klient eller CSV-verktyget i användargränssnittet i AEM.

### Svar (#http-responses)

Följande svarsvärden är möjliga:

* `200 OK`: Svaret innehåller upptäckter från mönsteravkännaren som genererades under cachelagringens aktualitetstid.
* `202 Accepted, processing cache`: Tillhandahålls för asynkrona svar för att indikera att cachen var inaktuell och att en uppdatering pågår.
* `400 Bad Request`: Anger att det uppstod ett fel med begäran. Ett meddelande i formatet Probleminformation (se [RFC 7807](https://tools.ietf.org/html/rfc7807)) innehåller mer information.
* `401 Unauthorized`: Begäran var inte auktoriserad.
* `500 Internal Server Error`: Anger att ett internt serverfel uppstod. Ett meddelande i formatet Probleminformation innehåller mer information.
* `503 Service Unavailable`: Anger att servern är upptagen med ett annat svar och kan inte hantera denna begäran i tid. Detta fungerar bara som när synkrona begäranden görs. Ett meddelande i formatet Probleminformation innehåller mer information.

## Cache-livstidsjustering {#cache-adjustment}

Standardlivstiden för CRA-cache är 24 timmar. Med alternativet att uppdatera en rapport och återskapa cachen, både i AEM-instansen och i HTTP-gränssnittet, är det här standardvärdet troligtvis lämpligt för de flesta användningsområden för CRA. Om rapportgenereringstiden är särskilt lång för AEM-instansen kanske du vill justera cachelivstiden för att minimera omgenereringen av rapporten.

Livslängdsvärdet för cacheminnet lagras som egenskapen `maxCacheAge` på följande databasnod:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

Värdet för den här egenskapen är cachelivstiden i sekunder. Administratören kan justera cachelivstiden med CRXDE Lite.





