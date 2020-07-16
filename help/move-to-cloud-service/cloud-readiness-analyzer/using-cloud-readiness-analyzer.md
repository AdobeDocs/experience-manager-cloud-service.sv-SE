---
title: Använda Cloud Readiness Analyzer
description: Använda Cloud Readiness Analyzer
translation-type: ht
source-git-commit: a0e58c626f94b778017f700426e960428b657806
workflow-type: ht
source-wordcount: '1871'
ht-degree: 100%

---


# Använda Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Viktigt att tänka på när du använder Cloud Readiness Analyzer {#imp-considerations}

Läs avsnittet nedan när du vill veta mer om viktiga aspekter när du använder Cloud Readiness Analyzer (CRA):

* CRA-rapporten byggs med utdata från Adobe Experience Manager (AEM) [Pattern Detector](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html). Den version av Pattern Detector som används av CRA ingår i CRA-installationspaketet.

* CRA kan bara köras av **administratörsanvändaren** eller en användare i gruppen **Administratörer**.

* CRA stöds på AEM-instanser med version 6.1 och senare.

   >[!NOTE]
   > Se [Installera på AEM 6.1](#installing-on-aem61) för särskilda krav gällande installation av CRA på AEM 6.1.

* CRA kan köras i vilken miljö som helst, men det är bättre att köra det i en *mellanlagringsmiljö*.

   >[!NOTE]
   >För att undvika att affärskritiska instanser påverkas rekommenderar vi att du kör CRA i en *författarmiljö* som är så nära *produktionsmiljön* som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Alternativt kan det köras på en klon av *författarmiljön* i produktion.

* Det kan ta lång tid att generera innehållet i en CRA-rapport, från flera minuter till några timmar. Hur lång tid som krävs beror i hög grad på storlek och typ av AEM-databasinnehåll, AEM-version och andra faktorer.

* På grund av den tid som kan krävas för att generera rapportinnehållet, genereras det av en bakgrundsprocess och lagras i ett cacheminne. Det bör gå relativt snabbt att visa och hämta rapporten eftersom den använder innehållscachen tills den upphör att gälla eller tills rapporten uttryckligen uppdateras. Under genereringen av rapportinnehållet kan du stänga webbläsarfliken och sedan gå tillbaka och visa rapporten när innehållet är tillgängligt i cachen.

## Tillgänglighet {#availability}

Cloud Readiness Analyzer kan hämtas som en zip-fil från Software Distribution portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM).

>[!NOTE]
>Hämta Cloud Readiness Analyzer från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) Portal.

## Visa Cloud Readiness Analyzer-rapporten {#viewing-report}

### Adobe Experience Manager 6.3.0 och senare {#aem-later-versions}

Läs det här avsnittet för att få veta hur du visar Cloud Readiness Analyzer-rapporten:

1. Välj Adobe Experience Manager och navigera till Tools -> **Operations** -> **Cloud Readiness Analyzer**.

   ![bild](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. När du klickar på **Cloud Readiness Analyzer** börjar verktyget generera rapporten och den visas när den är tillgänglig.

   >[!NOTE]
   >Du måste rulla nedåt på sidan för att se hela rapporten.

   ![bild](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. När CRA-rapporten har genererats och visas kan du välja att hämta rapporten i kommaavgränsat format (CSV) genom att klicka på **CSV** så som visas på bilden nedan.

   ![bild](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >Du kan tvinga CRA att rensa cachen och återskapa rapporten genom att klicka på **Refresh Report**.

### Adobe Experience Manager 6.2 och 6.1 {#aem-specific-versions}

Verktyget Cloud Readiness Analyzer begränsas i Adobe Experience Manager 6.2 till en länk som genererar och hämtar CSV-rapporten.

Verktyget fungerar inte i Adobe Experience Manager 6.1, endast HTTP-gränssnittet kan användas.

>[!NOTE]
>I alla versioner kan medföljande Pattern Detector köras fristående.

## Tolka Cloud Readiness Analyzer-rapporten {#cra-report}

När verktyget Cloud Readiness Analyzer körs i AEM-instansen visas rapporten i verktygsfönstret.

Rapportens format är:

* **Report Overview**: Information om själva rapporten med följande information:
   * **Report Time**: När rapportinnehållet genererades och gjordes tillgängligt för första gången.
   * **Expiration Time**: När cachen för rapportinnehållet upphör att gälla.
   * **Generation Time Period**: Den tid det tog att generera rapportinnehållet.
   * **Finding Count**: Det totala antalet resultat som ingår i rapporten.
* **System Overview**: Information om det AEM-system som CRA kördes på.
* **Finding Categories**: Flera avsnitt som vart och ett handlar om ett eller flera resultat i samma kategori. Varje avsnitt innehåller följande: kategorinamn, undertyper, antal resultat och viktighetsgrad, sammanfattning, länk till kategoridokumentation och information om enskilda resultat.

Viktighetsgrad tilldelas varje resultat och anger ungefärlig prioritet för åtgärder.

Läs tabellen nedan för mer information om viktighetsgrad:

| Viktighetsgrad | Beskrivning |
|--- |--- |
| INFO | Resultatet tillhandahålls i informationssyfte. |
| ADVISORY | Resultatet kan innebära ett uppgraderingsproblem. Ytterligare undersökningar rekommenderas. |
| MAJOR | Detta resultat innebär sannolikt ett uppgraderingsproblem som bör åtgärdas. |
| CRITICAL | Detta resultat innebär sannolikt ett uppgraderingsproblem som måste åtgärdas för att förhindra funktions- eller prestandaproblem. |


## Tolka CSV-rapporten från Cloud Readiness Analyzer {#cra-csv-report}

När du klickar på alternativet **CSV** från din AEM-instans skapas Cloud Readiness Analyzer-rapporten i CSV-format från innehållscachen och returneras till webbläsaren. Beroende på inställningarna i webbläsaren hämtas rapporten automatiskt som en fil med standardnamnet `results.csv`.

Om cacheminnet har gått ut genereras rapporten på nytt innan CSV-filen skapas och hämtas.

Rapporten i CSV-format innehåller information som genereras med utdata från Pattern Detector och som sorteras och organiseras efter kategorityp, undertyp och viktighetsgrad. Formatet är lämpligt för visning och redigering i program som Microsoft Excel. Avsikten är att ge information om alla resultat i ett upprepningsbart format som kan användas för att jämföra rapporter från olika tidpunkter för att mäta framsteg.

Kolumnerna i rapporten i CSV-format är:

* **code**: kategorikoden
* **type**: kategorinamnet
* **subtype**: undertypen av kategori
* **importance**: viktighetsgrad
* **identifier**: den primära identifieraren för resultatet
* **other**: ytterligare information om resultatet
* **message**: det meddelande som tillhandahålls för resultatet
* **moreInfo**: en länk som kan användas för att öppna onlinehjälpen för kategorin
* **context**: en JSON-sträng med resultatdata

Värdet &quot;\N&quot; i en kolumn för enskilda resultat anger att inga data finns.

## HTTP-gränssnitt {#http-interface}

CRA har ett HTTP-gränssnitt som kan användas som ett alternativ till användargränssnittet i AEM. Gränssnittet har stöd för både HEAD- och GET-kommandon. Det kan användas för att generera CRA-rapporten och returnera den i ett av tre format: JSON, CSV och tabbavgränsade värden (TSV).

Följande URL:er är tillgängliga för HTTP-åtkomst där `<host>` är värdnamnet och porten på servern där CRA är installerat om det behövs:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` för JSON-format
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` för CSV-format
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` för TSV-format

### Köra en HTTP-begäran {#executing-http-request}

HTTP-gränssnittet kan användas på flera olika sätt.

Ett enkelt sätt är att öppna en webbläsarflik i den webbläsare där du har loggat in i AEM som administratör. Du kan ange URL-adressen på webbläsarfliken och låta webbläsaren visa eller hämta resultat.

Du kan också använda ett kommandoradsverktyg som `curl` eller `wget` samt HTTP-klientprogram. Om du inte använder en webbläsarflik med en autentiserad session måste du ange ett administratörsanvändarnamn och lösenord som en del av kommentaren.

Nedan visas ett exempel på hur du gör det:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### Sidhuvuden och parametrar {#http-headers-and-parameters}

Följande HTTP-sidhuvuden används i gränssnittet:

* `Cache-Control: max-age=<seconds>`: Ange livslängd för cacheminnet i sekunder. (Se [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Anger att servern ska svara asynkront. (Se [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)

Följande HTTP-frågeparametrar är praktiska när det är svårt att använda HTTP-sidhuvuden:

* `max-age` (tal, valfritt): Ange livslängd för cacheminnet i sekunder. Siffran måste vara 0 eller större. Utan den här parametern eller motsvarande sidhuvud är standardlivslängden 86 400 sekunder, vilket innebär att ett nytt cacheminne används för förfrågningar i 24 timmar innan rapporten måste genereras igen. Om du använder `max-age=0` kommer cachen att rensas och rapporten genereras igen. Direkt efter begäran återställs livslängden till det senaste värdet som inte är noll.
* `respond-async` (booleskt, valfritt): Anger att svaret ska tillhandahållas asynkront. Om du använder `respond-async=true` när cachen är gammal kommer servern att returnera svaret `202 Accepted, processing cache` utan att vänta på att rapporten genereras och att cachen uppdateras. Om cacheminnet är uppdaterat har den här parametern ingen effekt. Standardvärdet är `false`, vilket innebär att utan den här parametern eller motsvarande sidhuvud kommer servern att svara synkront, vilket kan ta lång tid och kräva en justering av den maximala svarstiden för HTTP-klienten.

När det finns både ett HTTP-sidhuvud och motsvarande frågeparameter har frågeparametern företräde.

Ett enkelt sätt att initiera rapportgenereringen via HTTP-gränssnittet är med följande kommando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

När en begäran har skickats behöver klienten inte vara aktiv för att rapporten ska genereras. Rapportgenereringen kan initieras via en klient med en HTTP GET-begäran. När rapporten har genererats visas den från cachen i en annan klient eller i CSV-verktyget i användargränssnittet i AEM.

### Svar {#http-responses}

Följande svarsvärden är möjliga:

* `200 OK`: Svaret innehåller resultat från Pattern Detector som genererades under cacheminnets livstid.
* `202 Accepted, processing cache`: Tillhandahålls för asynkrona svar för att indikera att cachen var inaktuell och att en uppdatering pågår.
* `400 Bad Request`: Anger att det uppstod ett fel med begäran. Ett meddelande i formatet Problem Details (se [RFC 7807](https://tools.ietf.org/html/rfc7807)) för mer information.
* `401 Unauthorized`: Begäran var inte auktoriserad.
* `500 Internal Server Error`: Anger att ett internt serverfel uppstod. Ett meddelande i formatet Problem Details innehåller mer information.
* `503 Service Unavailable`: Anger att servern är upptagen med ett annat svar och inte kan hantera begäran i tid. Detta inträffar troligtvis bara när synkrona förfrågningar görs. Ett meddelande i formatet Problem Details innehåller mer information.

## Administratörsinformation

### Justera cacheminnets livslängd {#cache-adjustment}

Standardlivslängden för CRA-cacheminnet är 24 timmar. Med alternativet att uppdatera en rapport och återskapa cachen, både i AEM-instansen och i HTTP-gränssnittet, är det här standardvärdet troligtvis lämpligt för de flesta användningsområden för CRA. Om rapportgenereringstiden är särskilt lång för AEM-instansen kanske du bör justera cachelivslängden för att minimera genereringen av rapporter.

Livslängdsvärdet för cacheminnet lagras som egenskapen `maxCacheAge` på följande databasnod:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

Värdet för den här egenskapen är cachelivslängden i sekunder. Administratören kan justera cachelivslängden med CRX/DE Lite.

### Installera på AEM 6.1 {#installing-on-aem61}

CRA använder ett användarkonto för systemtjänster vid namn `repository-reader-service` för att köra Mönsteravkännaren. Det här kontot är tillgängligt på AEM 6.2 och senare. På AEM 6.1 måste det här kontot skapas *innan* CRA installeras via följande steg:

1. Följ instruktionerna på [Skapa en ny tjänstanvändare](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) för att skapa en användare. Ange användar-ID till `repository-reader-service` och lämna den mellanliggande sökvägen tom. Klicka sedan på den gröna bockmarkeringen.

2. Följ instruktionerna i [Hantera användare och grupper](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security.html#managing-users-and-groups). Särskilt instruktionerna för hur man lägger till användare i en grupp för att lägga till `repository-reader-service`-användaren i `administrators`-gruppen.

3. Installera CRA-paketet via Package Manager på AEM-källinstansen. (Detta lägger till den nödvändiga konfigurationsändringen i konfigurationen ServiceUserMapper för `repository-reader-service`-systemtjänstanvändaren.)
