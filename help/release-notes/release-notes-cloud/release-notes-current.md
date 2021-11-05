---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a0bf314ff8f994dd77c2c124db1ab604dcae74b6
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

The following section outlines the general Release Notes for the current (latest) version of [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2021.10.0) är 4 november 2021.
Följande version (2021.11.0) är den 2 december 2021.

## Släpp video {#release-video}

Ta en titt på [Oktober 2021 versionsöversikt](https://video.tv.adobe.com/v/338253) video med en sammanfattning av tillagda funktioner.

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Ny funktion i [!DNL Sites] {#sites-features}

* Modeller för innehållsfragment anges nu automatiskt i skrivskyddat läge när de har publicerats, för att undvika att direktsända API-frågor bryts efter att en redigerad modell har publicerats om. Användarna får en varning när de försöker redigera en publicerad modell. Du kan redigera när du har godkänt varningen.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] har nu stöd för automatisk generering av texttranskript från ljud- och videomaterial som stöds, med en inbyggd koppling till [!DNL Azure Media Services]. The supported files are automatically transcribed and the text is stored in WebVTT format. The WebVTT captions are used for more effective searching, captioning, or translation. Funktionen förbättrar också tillgängligheten, identifieringen och lokaliseringen av resurserna.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

* [!DNL Dynamic Media] Image Smart Crop och Swatch bygger nu på de senaste Sensei-tjänsterna som genererar förbättrade beskärningar och färgrutor. Dessutom har en förbättring startats för att generera olika beskärningsinnehåll, med samma proportioner men med olika upplösningar. Dessutom bevaras alla manuella redigeringar vid ombearbetningen om bredden och höjden inte ändras i bildprofilen.

* Smarta taggar tillämpas automatiskt på resurserna med hjälp av resursmikrotjänster i stället för med smarta innehållstjänster. Den underliggande modellen uppdateras för att förbättra taggningsresultaten och minska bias. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**: You can now capture and track behavior of both logged-in and not logged-in (Anonymous) via Adobe Analytics for Adaptive Forms to gather end user insights. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms-oct-2021}

* **Externt AEM arbetsflödesdata för säker bearbetning**: Du kan lagra AEM arbetsflödesdata (AEM data från arbetsflödesvariabler) som innehåller känsliga dataelement (SPD) i en kundhanterad databas för säker bearbetning. Dataelementen och arbetsflödesvariablerna lagras inte i AEM och hämtas på begäran från en kundhanterad databas när arbetsflödet bearbetas.

### Betafunktioner i [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   * Generera dokument genom att fylla i mallfiler (PDF och XDP) med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.

You can write to [!DNL formscsbeta@adobe.com] to sign up for the beta program.

## CIF Add-on {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* CIF-tillägget stöder den senaste Commerce v2.4.3 med nya GraphQL API:er och scheman

* Författare kan lägga till länkar till produkt- och katalogsidor i textfält med textredigeraren. En CIF-ikon har lagts till i verktygsfältet för textredigering som öppnar väljarna för att snabbt söka efter och välja produkten eller kategorin utan att lämna sammanhanget.

* Befintlig snabbkundvagn och utcheckning har ersatts med dedikerade AEM- och utcheckningssidor. Komponenterna på dessa sidor byggs med Magento utökningsbara Premiere-komponenter

* Handlare kan dölja vissa produktkatalogkategorier i navigeringen med Commerce-serverdelen. CIF Navigation Core Component (kärnkomponent för CIF-navigering) respekterar e-handelsserverdelens konfiguration &quot;include in menu&quot; för att visa/dölja kategorier i navigering

* AEM Storefront Venia returnerar HTTP 404-fel om kategori eller produktsida inte hittas

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.10.0.

### Releasedatum {#release-date-cm-nov}

The Release Date for Cloud Manager in AEM as a Cloud Service 2021.11.0 is November 04, 2021.
Nästa version är planerad till 9 december 2021.

### Nyheter {#what-is-new-cm-nov}

* Users can now leverage new Front End pipelines to exclusively deploy front end code in an accelerated manner. Se [Front End Pipelines för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) om du vill veta mer.

   >[!IMPORTANT]
   >You must be on AEM version `2021.10.5933.20211012T154732Z` to leverage new Front End pipelines.

* Varaktigheten i bildrutorna för kodkvalitet minskar avsevärt genom att utföra kodanalysen på ett mer effektivt sätt utan att behöva skapa en hel AEM. Denna förändring rullar ut progressivt under de veckor som följer efter releasen.

* The Git Commit ID will now be displayed in the pipeline execution details making it easier to track the code that was built.

* Nu kan du skapa program via offentligt exponerade API:er.

* Miljöskapande är nu tillgängligt via offentligt exponerade API.

* The `x-request-id` svarshuvudet är nu synligt i API-uppspelningen på [www.adobe.io](https://www.adobe.io/). Det här huvudet är användbart när du skickar in kundvårdsproblem för felsökning.

* Som användare ser jag att Pipeline-kortet med noll rörledningar ger mig lämplig vägledning.

* Det finns nu en ny aktivitetssida där aktiviteter som pipeline och kodkörningar kan visas tillsammans med tillhörande information. Med tiden kommer de aktiviteter som listas på den här sidan att utvidgas tillsammans med den information som ges.

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

* Users of Cloud Manager can now submit feedback directly from the user interface via the **Feedback** button on top right of the landing page.

* Årliga SLA-diagram kan nu hämtas från användargränssnittet i Cloud Manager.

* Kodkvalitet och icke-produktionsrelaterade pipeline-körningar kommer nu att använda en mer effektiv, ytlig kloningsprocess under byggsteget, vilket ger en snabbare byggtid för kunder med särskilt stora Git-databaser.

* Guiden Lägg till IP Tillåtelselista informerar nu användaren om maximalt tillåtet antal IP-Tillåtelselista har uppnåtts.

* API-dokumentationen för Cloud Manager innehåller nu en interaktiv spelningsmiljö som gör att inloggade användare kan experimentera med API:t från sin webbläsare. Se [API-spelning för Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) för mer information.

* Verktygstipset på programkortet blir mer beskrivande om ett markeringsalternativ under Navigera till är inaktiverat. Nu visas&quot;En produktionsmiljö finns inte&quot;.

### Felkorrigeringar {#bug-fixes-cm-oct}

* I sällsynta fall, när en Adobe-personal skulle återställa en kunds miljö, ansågs återställningen vara fullständig innan miljön var helt i drift.

* Certain internal requests made during environment creation were not being retried.

* Om ett distributionsfel uppstår efter domännamnsverifiering har felmeddelandet korrigerats för att begära att kunden kontaktar sin Adobe-representant.

## Best Practices Analyzer {#best-practices-analyzer}

### Release Date {#release-date-bpa-latest}

The Release Date for Best Practices Analyzer v2.1.20 is October 05, 2021.

### Nyheter {#what-is-new}

* Möjlighet att identifiera och rapportera nodnamnets längd.

* Möjlighet att identifiera och rapportera om den totala indexstorleken.

* Möjlighet att upptäcka och rapportera resurser som saknar sin ursprungliga återgivning.
