---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 23b06ce1f3c49b2a63c71d53fdc6c26ad02160f5
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2021.10.0) är 4 november 2021.
Följande version (2021.11.0) är den 16 december 2021.

## Släpp video {#release-video}

Ta en titt på [Oktober 2021 versionsöversikt](https://video.tv.adobe.com/v/338253) video med en sammanfattning av tillagda funktioner.

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Ny funktion i [!DNL Sites] {#sites-features}

* Modeller för innehållsfragment ställs nu automatiskt in i skrivskyddat läge när de har publicerats, så att du inte oavsiktligt kan bryta aktiva API-frågor efter att ha publicerat om en redigerad modell. Användarna får en varning när de försöker redigera en publicerad modell. Du kan redigera när du har godkänt varningen.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] har nu stöd för automatisk generering av texttranskript från ljud- och videomaterial som stöds, med en inbyggd koppling till [!DNL Azure Media Services]. The [filtyper som stöds](/help/assets/file-format-support.md#audio-video-transcription-formats) transkriberas automatiskt och texten lagras i WebVTT-format. WebVTT-bildtexter används för effektivare sökning, bildtext eller översättning. Funktionen förbättrar också tillgängligheten, identifieringen och lokaliseringen av resurserna.

### Ny funktion i [!DNL Assets] prerelease channel {#assets-prerelease-features}

* [!DNL Dynamic Media] Image Smart Crop och Swatch bygger nu på de senaste Sensei-tjänsterna som genererar förbättrade beskärningar och färgrutor. Dessutom har en förbättring startats för att generera olika beskärningsinnehåll, med samma proportioner men med olika upplösningar. Dessutom bevaras alla manuella redigeringar vid ombearbetningen om bredden och höjden inte ändras i bildprofilen.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics för Adaptive Forms**: Nu kan du fånga in och spåra beteenden hos både inloggade och ej inloggade (anonyma) via Adobe Analytics för Adaptive Forms för att samla in slutanvändarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms-oct-2021}

* **Externt AEM arbetsflödesdata för säker bearbetning**: Du kan lagra AEM arbetsflödesdata (AEM data från arbetsflödesvariabler) som innehåller känsliga dataelement (SPD) i en kundhanterad databas för säker bearbetning. Dataelementen och arbetsflödesvariablerna lagras inte i AEM och hämtas på begäran från en kundhanterad databas när arbetsflödet bearbetas.

### Betafunktioner i [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   * Generera dokument genom att fylla i mallfiler (PDF och XDP) med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att anmäla dig till betaprogrammet.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* CIF-tillägget stöder den senaste Commerce v2.4.3 med nya GraphQL API:er och scheman

* Författare kan lägga till länkar till produkt- och katalogsidor i textfält med textredigeraren. En CIF-ikon har lagts till i verktygsfältet för textredigering som öppnar väljarna för att snabbt söka efter och välja produkten eller kategorin utan att lämna sammanhanget.

* Befintlig snabbkundvagn och utcheckning har ersatts med dedikerade AEM- och utcheckningssidor. Komponenterna på dessa sidor byggs med Magento utökningsbara Premiere-komponenter

* Handlare kan dölja vissa produktkatalogkategorier i navigeringen med Commerce-serverdelen. CIF Navigation Core Component (kärnkomponent för CIF-navigering) respekterar e-handelsserverdelens konfiguration &quot;include in menu&quot; för att visa/dölja kategorier i navigering

* AEM Storefront Venia returnerar HTTP 404-fel om kategori eller produktsida inte hittas

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.10.0.

### Releasedatum {#release-date-cm-nov}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.11.0 är 4 november 2021.
Nästa version är planerad till 9 december 2021.

### Nyheter {#what-is-new-cm-nov}

* Användare kan nu utnyttja nya frontledningslinjer för att exklusivt distribuera frontendkod snabbare. Se [Front End Pipelines för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) om du vill veta mer.

   >[!IMPORTANT]
   >Du måste ha AEM version `2021.10.5933.20211012T154732Z` för att utnyttja nya frontledningslinjer.

* Varaktigheten i bildrutorna för kodkvalitet minskar avsevärt genom att utföra kodanalysen på ett mer effektivt sätt utan att behöva skapa en hel AEM. Denna förändring rullar ut progressivt under de veckor som följer efter releasen.

* Git-implementerings-ID visas nu i körningsinformationen för pipeline, vilket gör det enklare att spåra koden som skapades.

* Nu kan du skapa program via offentligt exponerade API:er.

* Miljöskapande är nu tillgängligt via offentligt exponerade API.

* The `x-request-id` svarshuvudet är nu synligt i API-uppspelningen på [www.adobe.io](https://www.adobe.io/). Det här huvudet är användbart när du skickar in kundvårdsproblem för felsökning.

* Som användare ser jag att Pipeline-kortet med noll rörledningar ger mig lämplig vägledning.

* Det finns nu en ny aktivitetssida där aktiviteter som pipeline och kodkörningar kan visas tillsammans med tillhörande information. Med tiden kommer de aktiviteter som listas på den här sidan att utvidgas tillsammans med de angivna detaljerna.

* Nu finns det en ny sida med Pipelines (Pipelines) med en statuspekare som du kan använda när du hovrar för att enkelt visa sammanfattningen av detaljer. Pipeline-körningar kan visas tillsammans med tillhörande information.

* API:t Redigera pipeline har nu stöd för att ändra miljön som används i distributionsfaserna.

* En optimering i OakPal-skanningsprocessen har införts för stora paket.

* CSV-filen för kvalitetsutgåva kommer nu att innehålla tidsstämpeln för varje kvalitetsproblem.

### Felkorrigeringar {#bug-fixes-nov}

* Vissa oortodoxa byggkonfigurationer resulterade i att onödiga filer sparades i Pipelins Maven-artefaktcache, vilket resulterade i överflödig nätverks-I/O när byggbehållaren startades och stoppades.

* Pipeline PATCH API misslyckas om det inte finns någon distributionsfas.

* The `ClientlibProxyResourceCheck` kvalitetsregeln genererade falskt positiva problem när det fanns klientbibliotek med gemensamma grundsökvägar.

* Felmeddelandet när det maximala antalet databaser har uppnåtts specificerade inte orsaken till felet.

* I sällsynta fall misslyckades rörledningar på grund av olämplig hantering av vissa svarskoder.


## Releasedatum {#release-date-cm-oct}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.10.0 är 14 oktober 2021.

### Nyheter {#what-is-new-cm-oct}

* Som en förberedelse för vissa kommande ändringar kommer befintliga distributionsrutnät nu att refereras och märkas i användargränssnittet som **Hel hög** rörledningar.

* Pipelinekortet har uppdaterats så att det nu visas ett enda, integrerat ansikte som visar både pipelines för produktion och icke-produktion, och användaren kan välja Kör/Pausa/Fortsätt direkt på den åtgärdsmeny som är kopplad till varje pipeline.

* En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via gränssnittet.

* Lägg till och redigera rörliga upplevelser har uppdaterats för att nu använda välbekanta, moderna moduler.

* Användare av Cloud Manager kan nu skicka feedback direkt från användargränssnittet via **Feedback** överst till höger på landningssidan.

* Årliga SLA-diagram kan nu hämtas från användargränssnittet i Cloud Manager.

* Kodkvalitet och icke-produktionsrelaterade pipeline-körningar kommer nu att använda en mer effektiv, ytlig kloningsprocess under byggsteget, vilket ger en snabbare byggtid för kunder med särskilt stora Git-databaser.

* Guiden Lägg till IP Tillåtelselista informerar nu användaren om maximalt tillåtet antal IP-Tillåtelselista har uppnåtts.

* API-dokumentationen för Cloud Manager innehåller nu en interaktiv spelningsmiljö som gör att inloggade användare kan experimentera med API:t från sin webbläsare. Se [API-spelning för Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) för mer information.

* Verktygstipset på programkortet blir mer beskrivande om ett markeringsalternativ under Navigera till är inaktiverat. Nu visas&quot;En produktionsmiljö finns inte&quot;.

### Felkorrigeringar {#bug-fixes-cm-oct}

* I sällsynta fall, när en Adobe-personal skulle återställa en kunds miljö, ansågs återställningen vara fullständig innan miljön var helt i drift.

* Vissa interna begäranden som gjordes när miljön skapades har inte gjorts om.

* Om ett distributionsfel uppstår efter domännamnsverifiering har felmeddelandet korrigerats för att begära att kunden kontaktar sin Adobe-representant.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa-latest}

Releasedatum för Best Practices Analyzer v2.1.20 är 5 oktober 2021.

### Nyheter {#what-is-new}

* Möjlighet att identifiera och rapportera nodnamnets längd.

* Möjlighet att identifiera och rapportera om den totala indexstorleken.

* Möjlighet att upptäcka och rapportera resurser som saknar sin ursprungliga återgivning.


## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.22 är 1 december 2021.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka och rapportera vilken version av ACS-kommandon som används.
* Möjlighet att identifiera och rapportera antalet användare och undergrupper i en grupp.
* Möjlighet att identifiera och rapportera om egenskapsvärden för noder i MongoDB som överstiger 16 MB.

### Felkorrigeringar {#bug-fixes-bpa}

* Identifieringen av Foundation-komponenter förfinades för att minska falska negativ.
* För AEM Forms-kunder gäller BPA-meddelanden `EMAIL_PDF_SUBMIT_ACTION` som inte är tillgänglig på AEM as a Cloud Service har åtgärdats.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.7.10 är 8 december 2021.

### Nyheter {#what-is-new-ctt}

* Växla som lagts till i inmatningsfasen i verktyget Innehållsöverföring så att användarna kan inaktivera [förkopia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) under intag. För optimal överföringshastighet bör pre-copy under intag inaktiveras för små migreringsuppsättningar eller om endast ett fåtal bloggar har lagts till sedan det senaste intaget.
* Användarmappning har uppdaterats för att använda ett förbättrat API för användarhantering som gör att 2 000 användare kan hämtas samtidigt, vilket avsevärt förbättrar prestandan.
