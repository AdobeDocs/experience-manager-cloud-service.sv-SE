---
title: Använda Best Practices Analyzer
description: Lär dig hur du använder Best Practices Analyzer för att förstå uppgraderingsberedskapen.
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 30%

---

# Använda Best Practices Analyzer {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Använda Best Practices Analyzer"
>abstract="Läs dokumentationen om hur du använder Best Practices Analyzer (tidigare Cloud Readiness Analyzer) och den genererade rapporten. Best Practices Analyzer-rapporten används för att få en god förståelse för den allmänna uppgraderingsberedskapen."
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Webinar] Vi presenterar verktyg för att snabba upp resan till Adobe Experience Manager as a Cloud Service"

## Viktigt att tänka på när du använder Best Practices Analyzer {#imp-considerations}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter av att köra Best Practices Analyzer (BPA):

* BPA-rapporten byggs med utdata från Adobe Experience Manager (AEM) [Mönsteravkännare](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). Den version av Mönsteravkännare som används av BPA ingår i BPA-installationspaketet.

* BPA kan bara köras av användaren **admin** eller en användare i gruppen **administratörer**.

* BPA stöds på AEM-instanser med version 6.1 och senare.

  >[!NOTE]
  >Se [Installera på AEM 6.1](#installing-on-aem61) för särskilda krav för installation av BPA på AEM 6.1.

* BPA kan köras i alla miljöer, men bör köras i en *Stage* -miljö.

  >[!NOTE]
  >För att undvika att affärskritiska instanser påverkas rekommenderar vi att du kör BPA i en *Stage* -miljö som är så nära *Production* -miljön som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Alternativt kan det köras på en klon av *författarmiljön* i produktion.

* Det kan ta lång tid att generera BPA-rapportinnehåll, från flera minuter till några timmar. Hur lång tid som krävs beror i hög grad på storlek och typ av AEM-databasinnehåll, AEM-version och andra faktorer.

* På grund av den tid som kan krävas för att generera rapportinnehållet, genereras det av en bakgrundsprocess och lagras i ett cacheminne. Det bör gå relativt snabbt att visa och hämta rapporten eftersom den använder innehållscachen tills den upphör att gälla eller tills rapporten uttryckligen uppdateras. Under genereringen av rapportinnehållet kan du stänga webbläsarfliken och sedan gå tillbaka och visa rapporten när innehållet är tillgängligt i cachen.

## Tillgänglighet {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="Hämta Best Practices Analyzer"
>abstract="Best Practices Analyzer kan laddas ned som en zip-fil från portalen för programvarudistribution. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM)."

Best Practices Analyzer kan laddas ned som en zip-fil från portalen för programvarudistribution. Du kan installera paketet via [Package Manager](/help/implementing/developing/tools/package-manager.md) på din Adobe Experience Manager-källinstans (AEM).

>[!NOTE]
>Hämta Best Practices Analyzer från portalen [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Source Environment Connectivity {#source-environment-connectivity}

Källinstansen av AEM kanske körs bakom en brandvägg där den bara kan nå vissa värdar som har lagts till i Tillåtelselista. För att automatiskt överföra den BPA-genererade rapporten till Cloud Acceleration Manager måste följande slutpunkter vara tillgängliga från instansen som kör AEM:

* Azure-blobblagringstjänsten: `casstorageprod.blob.core.windows.net`


## Visa rapporten Best Practices Analyzer {#viewing-report}

### Adobe Experience Manager 6.3.0 och senare {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="Överför automatiskt analysrapport om bästa praxis till CAM"
>abstract="Ange BPA-överföringsnyckeln för att automatiskt överföra den genererade BPA-rapporten till Cloud Acceleration Manager (CAM)."

Följ det här avsnittet för att lära dig hur du visar rapporten Best Practices Analyzer:

1. Välj Adobe Experience Manager och navigera till verktyg > **Åtgärder** > **Best Practices Analyzer**.

   ![Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. Klicka på **Generera rapport** för att köra Best Practices Analyzer.

   ![Generera rapport](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

>[!NOTE]
> Från och med BPA-version 2.1.54 har en ny funktion introducerats för att hämta Lightroom-bakgrundsmusiken.
1. När du har klickat på **Generera rapport** visas ett popup-fönster med en begäran om AEM Public Site URL för Lightroom-bakgrundsmusiken. Användaren måste ange en giltig URL i det angivna fältet.

   ![bild](/help/journey-migration/best-practices-analyzer/assets/bpa_popup_url.png)

   1. Om URL:en är giltig visas ett meddelande om att åtgärden lyckades.

      ![bild](/help/journey-migration/best-practices-analyzer/assets/valid_url.png)

   1. Om URL:en är ogiltig visas ett felmeddelande.

      ![bild](/help/journey-migration/best-practices-analyzer/assets/invalid_url.png)

1. Ange BPA-överföringsnyckeln för att automatiskt överföra den genererade BPA-rapporten till [Cloud Acceleration Manager (CAM)](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md). Navigera till [Best Practices Analysis i CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis) om du vill hämta överföringsnyckeln.

   ![Ange BPA-överföringsnyckel](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>Du kan välja att hoppa över den automatiska överföringen till CAM genom att välja **Hoppa över automatisk rapportöverföring till CAM**. Om du väljer att hoppa över måste du hämta BPA-rapporten manuellt som en kommaseparerad värdefil och sedan överföra filen i CAM. Du bör använda alternativet för överföringsnyckel eftersom det effektiviserar åtgärden.

>[!IMPORTANT]
>Vid manuell överföring till CAM begränsas rapportstorlekarna till cirka 200 MB. För större rapporter måste du utnyttja den automatiska överföringen.

1. Knappen **Generera** aktiveras när en giltig nyckel anges. Klicka på **Generera** för att initiera rapportgenerering.

   ![Generera rapport](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. Medan BPA genererar rapporten kan du se hur verktyget utvecklas på skärmen. Den visar förloppet i procent slutfört. Här visas också antalet analyserade objekt och även antalet upptäckter.

   ![Skapar rapport](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>Tidsstämpeln för förfallotid för BPA-överföringsnyckeln visas i det övre högra hörnet. Du bör förnya BPA-överföringsnyckeln när den snart upphör att gälla. Om du vill förnya nyckeln kan du klicka på **Förnya** och navigera till CAM för att förnya nyckeln.

1. När BPA-rapporten har genererats visas en sammanfattning och antalet resultat i ett tabellformat, ordnade efter typ av fynd och prioritetsnivå. Om du vill ha mer information om en viss sökning kan du klicka på talet som motsvarar sökningstypen i tabellen.

   ![Rapportöversikt](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Du kan hämta rapporten i ett kommaavgränsat värdeformat (CSV) genom att klicka på **Exportera till CSV**. Du kan också visa rapporten i CAM genom att klicka på **Gå till CAM**. Du kommer nu till sidan [Best Practices Analysis](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis) i CAM.

Du kan tvinga BPA att rensa sin cache och återskapa rapporten genom att klicka på **Uppdatera rapport**.

![Uppdatera rapport](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Om cachen förfaller kan du välja att visa den senast genererade rapporten i CAM genom att klicka på **Visa den senast genererade rapporten i CAM** eller starta en ny rapportgenerering genom att klicka på **Skapa ny rapport**.

![Ingen rapport](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### Använda filter i rapporten Best Practices Analyzer {#bpa-filters}

Följ stegen nedan för att filtrera bort resultat relaterade till [ACS-kommandon](https://adobe-consulting-services.github.io/acs-aem-commons/):

1. Klicka på ikonen för den vänstra listen till vänster på sidan. Då visas **ACS-kommandofiltret**. Klicka på **ACS-kommandofiltret** för att visa den interaktiva kryssrutan som visas i bilden nedan.

   ![ACS-kommandofilter](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >Ikonen för vänster spår visas bara om BPA upptäcker att ACS Commons används.

1. Avmarkera rutan om du vill filtrera bort alla upptäckter som rör ACS-kommandon. Rapporten **Antal filtrerade sökningar** visas i bilden nedan. Filtret används också i rapporten när den exporteras i ett CSV-format (kommaavgränsat värde).

   ![Antal filtrerade sökningar](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >ACS Commons-resultaten ska inte ignoreras. Mer information om kompatibilitet med AEM as a Cloud Service finns i [dokumentation](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility).

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## Tolka rapporten Best Practices Analyzer {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="Tolka rapporten Best Practices Analyzer"
>abstract="Det finns två alternativ för att visa BPA-rapportutdata: UI och CSV. När verktyget Best Practices Analyzer körs i AEM-instansen visas UI-rapporten som resultat i verktygsfönstret. CSV-formatet för rapporten innehåller information som genereras från utdata för Mönsteravkännare, sorterat och organiserat efter kategorityp, undertyp och prioritetsnivå."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#analysis-report" text="Analysrapport om metodtips för granskning"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html" text="Om rapportkategorier i Best Practices Analyzer"

När verktyget Best Practices Analyzer körs i AEM-instansen visas rapporten som resultat i verktygsfönstret.

Rapportens format är:

* **Report Overview**: Information om själva rapporten med följande information:
   * **Report Time**: När rapportinnehållet genererades och gjordes tillgängligt för första gången.
   * **Expiration Time**: När cachen för rapportinnehållet upphör att gälla.
   * **Generation Time Period**: Den tid det tog att generera rapportinnehållet.
   * **Finding Count**: Det totala antalet resultat som ingår i rapporten.
* **Systemöversikt**: Information om det AEM-system som BPA kördes på.
* **Finding Categories**: Flera avsnitt som vart och ett handlar om ett eller flera resultat i samma kategori. Varje avsnitt innehåller följande: kategorinamn, undertyper, antal resultat och viktighetsgrad, sammanfattning, länk till kategoridokumentation och information om enskilda resultat.

Viktighetsgrad tilldelas varje resultat och anger ungefärlig prioritet för åtgärder.

>[!NOTE]
>Mer information om de olika sökkategorierna finns i [Mönsterdetektorkategorierna](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

Läs tabellen nedan för mer information om viktighetsgrad:

| Viktighetsgrad | Beskrivning |
|--- |--- |
| INFO | Resultatet tillhandahålls i informationssyfte. |
| ADVISORY | Resultatet kan innebära ett uppgraderingsproblem. Ytterligare undersökningar rekommenderas. |
| MAJOR | Detta resultat innebär sannolikt ett uppgraderingsproblem som bör åtgärdas. |
| CRITICAL | Detta resultat innebär sannolikt ett uppgraderingsproblem som måste åtgärdas för att förhindra funktions- eller prestandaproblem. |

## Tolka CSV-rapporten för Best Practices Analyzer {#cra-csv-report}

När du klickar på alternativet **CSV** från din AEM-instans skapas CSV-formatet för Best Practices Analyzer-rapporten från innehållscachen och returneras till webbläsaren. Beroende på inställningarna i webbläsaren hämtas den här rapporten automatiskt som en fil med standardnamnet `results.csv`.

Om cacheminnet har upphört att gälla genereras rapporten om innan CSV-filen skapas och hämtas.

Rapporten i CSV-format innehåller information som genereras med utdata från Pattern Detector och som sorteras och organiseras efter kategorityp, undertyp och viktighetsgrad. Formatet är lämpligt för visning och redigering i program som Microsoft Excel. Avsikten är att ge all sökinformation i ett upprepningsbart format, som kan vara användbar vid jämförelse av rapporter över tid för att mäta förloppet.

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

BPA har ett HTTP-gränssnitt som kan användas som ett alternativ till användargränssnittet i AEM. Gränssnittet har stöd för både HEAD- och GET-kommandon. Den kan användas för att generera BPA-rapporten och returnera den i ett av tre format: JSON, CSV och tabbseparerade värden (TSV).

Följande URL:er är tillgängliga för HTTP-åtkomst, där `<host>` är värdnamnet och porten, om det behövs, för servern där BPA är installerat:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` för JSON-format
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` för CSV-format
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` för TSV-format

### Köra en HTTP-begäran {#executing-http-request}

HTTP-gränssnittet kan användas på flera olika sätt.

Ett enkelt sätt är att öppna en webbläsarflik i den webbläsare där du har loggat in i AEM som administratör. Du kan ange URL-adressen på webbläsarfliken och låta webbläsaren visa eller hämta resultat.

Du kan också använda ett kommandoradsverktyg som `curl` eller `wget` och alla HTTP-klientprogram. Om du inte använder en webbläsarflik med en autentiserad session måste du ange ett administratörsanvändarnamn och lösenord som en del av kommentaren.

Nedan visas ett exempel på hur du gör det:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Sidhuvuden och parametrar {#http-headers-and-parameters}

Följande HTTP-sidhuvuden används i gränssnittet:

* `Cache-Control: max-age=<seconds>`: Anger livstid för cacheåtergivning i sekunder. (Se [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Anger att servern ska svara asynkront. (Se [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)
* `Prefer: return=minimal`: Anger att servern ska returnera ett minimalt svar. (Se [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2).)

Följande HTTP-frågeparametrar är praktiska när det är svårt att använda HTTP-sidhuvuden:

* `max-age` (tal, valfritt): Anger cachelivstiden i sekunder. Siffran måste vara 0 eller större. Standardlivstiden för färskhet är 86400 sekunder. Utan den här parametern eller motsvarande rubrik används ett nytt cacheminne för att hantera begäranden i 24 timmar, och då måste cacheminnet genereras om. Om du använder `max-age=0` tvingas cachen att rensas och en omgenerering av rapporten initieras, med den tidigare icke-nollvaraktigheten för det nyligen genererade cacheminnet.
* `respond-async` (booleskt, valfritt): Anger att svaret ska anges asynkront. Om `respond-async=true` används när cachen är inaktiv kommer servern att returnera svaret `202 Accepted` utan att vänta på att cachen ska uppdateras och att rapporten ska genereras. Om cacheminnet är uppdaterat har den här parametern ingen effekt. Standardvärdet är `false`. Utan den här parametern eller motsvarande rubrik kommer servern att svara synkront, vilket kan kräva mycket tid och en justering av den maximala svarstiden för HTTP-klienten.
* `may-refresh-cache` (booleskt, valfritt): Anger att servern kan uppdatera cachen som svar på en begäran om den aktuella cachen är tom, inaktuell eller snart inaktuell. Om `may-refresh-cache=true`, eller om det inte anges, kan servern initiera en bakgrundsuppgift som anropar mönsteravkännaren och uppdaterar cachen. Om `may-refresh-cache=false` startar servern inte någon uppdateringsåtgärd som annars skulle ha utförts om cachen är tom eller inaktuell. I så fall är rapporten tom. Uppdateringsaktiviteter som redan pågår påverkas inte av den här parametern.
* `return-minimal` (booleskt, valfritt): Anger att svaret från servern endast ska innehålla statusen som innehåller förloppsindikatorn och cachestatusen i JSON-formatet. Om `return-minimal=true` är svarstexten begränsad till statusobjektet. Om `return-minimal=false`, eller om det inte anges, ges ett fullständigt svar.
* `log-findings` (booleskt, valfritt): Anger att servern ska logga innehållet i cachen när den skapas eller uppdateras. Varje sökning från cachen loggas som en JSON-sträng. Denna loggning sker endast om `log-findings=true` och begäran genererar ett nytt cacheminne.

När det finns både ett HTTP-sidhuvud och motsvarande frågeparameter har frågeparametern företräde.

Ett enkelt sätt att initiera rapportgenereringen via HTTP-gränssnittet är med följande kommando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

När en begäran har skickats behöver klienten inte vara aktiv för att rapporten ska genereras. Rapportgenereringen kan initieras med en klient med en HTTP GET-begäran och när rapporten har genererats visas den från cachen med en annan klient eller med BPA-verktyget i AEM användargränssnitt.

### Svar {#http-responses}

Följande svarsvärden är möjliga:

* `200 OK`: Anger att svaret innehåller resultat från mönsteravkännaren som genererades under cachets aktualitetstid.
* `202 Accepted`: Används för att ange att cachen är inaktuell. När `respond-async=true` och `may-refresh-cache=true` anger det här svaret att en uppdateringsåtgärd pågår. När `may-refresh-cache=false` anger det här svaret helt enkelt att cachen är inaktuell.
* `400 Bad Request`: Anger att det uppstod ett fel med begäran. Ett meddelande i formatet Probleminformation (se [RFC 7807](https://tools.ietf.org/html/rfc7807)) innehåller mer information.
* `401 Unauthorized`: Anger att begäran inte har auktoriserats.
* `500 Internal Server Error`: Anger att ett internt serverfel uppstod. Ett meddelande i formatet Problem Details innehåller mer information.
* `503 Service Unavailable`: Anger att servern är upptagen med ett annat svar och inte kan hantera begäran i tid. Detta inträffar troligtvis bara när synkrona förfrågningar görs. Ett meddelande i formatet Problem Details innehåller mer information.

## Administratörsinformation

### Cache-livstidsjustering {#cache-adjustment}

Standardlivstiden för BPA-cache är 24 timmar. Med alternativet att uppdatera en rapport och återskapa cachen, både i AEM-instansen och i HTTP-gränssnittet, är det här standardvärdet troligtvis lämpligt för de flesta användningsområden för BPA. Om rapportgenereringstiden är särskilt lång för din AEM-instans kanske du vill justera cachelivstiden för att minimera omgenereringen av rapporten.

Livslängdsvärdet för cacheminnet lagras som egenskapen `maxCacheAge` på följande databasnod:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

Värdet för den här egenskapen är cachelivslängden i sekunder. Administratören kan justera cachelivslängden med CRX/DE Lite.

### Installera på AEM 6.1 {#installing-on-aem61}

BPA använder ett användarkonto för systemtjänsten med namnet `repository-reader-service` för att köra mönsteravkännaren. Det här kontot är tillgängligt på AEM 6.2 och senare. På AEM 6.1 måste det här kontot skapas *innan*-installationen av BPA utförs enligt följande:

1. Följ instruktionerna på [Skapa en ny tjänstanvändare](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) för att skapa en användare. Ange användar-ID till `repository-reader-service` och lämna den mellanliggande sökvägen tom. Klicka sedan på den gröna bockmarkeringen.

2. Följ instruktionerna i [Hantera användare och grupper](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups). Särskilt instruktionerna för hur man lägger till användare i en grupp för att lägga till `repository-reader-service`-användaren i `administrators`-gruppen.

3. Installera BPA-paketet via Package Manager på AEM-källinstansen. (Detta lägger till den nödvändiga konfigurationsändringen i konfigurationen ServiceUserMapper för `repository-reader-service`-systemtjänstanvändaren.)
