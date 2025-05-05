---
title: Versionsinformation för version 2021.10.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.10.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2021.10.0) är 4 november 2021.
Följande version (2021.11.0) är den 2 december 2021.

## Släpp video {#release-video}

Titta på videon [Oktober 2021 Release Overview](https://video.tv.adobe.com/v/338253) för en sammanfattning av de funktioner som lagts till.

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Ny funktion i [!DNL Sites] {#sites-features}

* Modeller för innehållsfragment ställs nu automatiskt in i skrivskyddat läge när de har publicerats, så att du inte oavsiktligt kan bryta aktiva API-frågor efter att ha publicerat om en redigerad modell. Användarna får en varning när de försöker redigera en publicerad modell. Du kan redigera när du har godkänt varningen.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] har nu stöd för automatisk generering av texttranskript från ljud- och videoresurser som stöds, med en inbyggd koppling till [!DNL Azure Media Services]. De [filtyper](/help/assets/file-format-support.md#audio-video-transcription-formats) som stöds transkriberas automatiskt och texten lagras i WebVTT-format. WebVTT-bildtexterna används för effektivare sökning, bildtext eller översättning. Funktionen förbättrar också tillgängligheten, identifieringen och lokaliseringen av resurserna.

### Ny funktion i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

* [!DNL Dynamic Media] Image Smart Crop och Swatch drivs nu av de senaste Sensei-tjänsterna som genererar förbättrade beskärningar och färgrutor. Dessutom har en förbättring startats för att generera olika beskärningsinnehåll, med samma proportioner men med olika upplösningar. Dessutom behålls alla manuella redigeringar vid ombearbetningen om bredden och höjden inte ändras i bildprofilen.

* Smarta taggar tillämpas automatiskt på resurserna med hjälp av resursmikrotjänster i stället för med smarta innehållstjänster. Den underliggande modellen uppdateras för att förbättra taggningsresultaten och minska bias. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**: Nu kan du samla in och spåra beteenden hos både inloggad och ej inloggad (anonym) med Adobe Analytics for Adaptive Forms för att samla in användarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Gör AEM arbetsflödesdata externt för säker bearbetning**: Du kan lagra processdata AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga SPD-element (Personal Data) i en kundhanterad databas för säker bearbetning. Dataelementen och arbetsflödesvariablerna lagras inte i AEM och hämtas på begäran från en kundhanterad databas när arbetsflödet bearbetas.

### Beta-funktioner i [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=sv-SE) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   * Generera dokument genom att fylla i mallfiler (PDF och XDP) med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Tillägget CIF stöder den senaste versionen av Commerce v2.4.3 med nya GraphQL API:er och scheman

* Författare kan lägga till länkar till produkt- och katalogsidor i textfält med textredigeraren. En CIF ikon har lagts till i verktygsfältet som öppnar väljarna för att snabbt söka efter och välja produkten eller kategorin utan att lämna sammanhanget.

* Befintlig snabbkundvagn och utcheckning har ersatts med dedikerade AEM- och utcheckningssidor. Komponenterna på dessa sidor byggs med Adobe Commerce utökningsbara Premiere-komponenter

* Marknadsförare kan dölja vissa produktkatalogkategorier i navigeringen med hjälp av Commerce serverdel. Den CIF kärnkomponenten för navigering respekterar e-handelsserverdelens konfiguration &quot;include in menu&quot; för att visa/dölja kategorier i navigering

* AEM Storefront Venia returnerar HTTP 404-fel om kategori eller produktsida inte hittas

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.10.0.

### Releasedatum {#release-date-cm-nov}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.11.0 är 4 november 2021.
Nästa version är planerad till 9 december 2021.

### Nyheter {#what-is-new-cm-nov}

* Användare kan nu använda nya frontledningslinjer för att exklusivt distribuera slutkod på ett accelererat sätt. Mer information finns i [Cloud Manager Front End Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end).

  >[!IMPORTANT]
  >Du måste ha AEM version `2021.10.5933.20211012T154732Z` för att kunna använda nya frontendpipelines.

* Varaktigheten i bildrutorna för kodkvalitet minskar avsevärt genom att utföra kodanalysen på ett mer effektivt sätt utan att behöva skapa en hel AEM. Denna förändring rullar ut progressivt under de veckor som följer efter releasen.

* Git-implementerings-ID visas nu i körningsinformationen för pipeline, vilket gör det enklare att spåra koden som skapades.

* Nu kan du skapa program via offentligt exponerade API.

* Miljöskapande är nu tillgängligt via offentligt exponerade API.

* Svarshuvudet `x-request-id` visas nu i API-spelarvyn på [www.adobe.io](https://www.adobe.io/). Det här huvudet är användbart när du skickar in kundvårdsproblem för felsökning.

* Som användare ser jag att Pipeline-kortet med noll rörledningar ger mig lämplig vägledning.

* Det finns nu en ny aktivitetssida där aktiviteter som pipeline och kodkörningar kan visas tillsammans med tillhörande information. Med tiden kommer de aktiviteter som listas på den här sidan att utvidgas tillsammans med de angivna detaljerna.

* Nu finns det en ny sida med Pipelines (Pipelines) med en statuspekare som du kan använda när du hovrar för att enkelt visa sammanfattningen av detaljer. Pipeline-körningar kan visas tillsammans med tillhörande information.

* API:t Redigera pipeline har nu stöd för att ändra miljön som används i distributionsfaserna.

* En optimering i OakPal-skanningsprocessen har införts för stora paket.

* CSV-filen för kvalitetsutgåva kommer nu att innehålla tidsstämpeln för varje kvalitetsproblem.

### Felkorrigeringar {#bug-fixes-nov}

* Vissa oortodoxa byggkonfigurationer resulterade i att onödiga filer sparades i Pipelins Maven-artefaktcache, vilket resulterade i överflödig nätverks-I/O när byggbehållaren startades och stoppades.

* Pipeline PATCH API misslyckas om det inte finns någon distributionsfas.

* Kvalitetsregeln `ClientlibProxyResourceCheck` gav upphov till falskt positiva problem när det fanns klientbibliotek med gemensamma grundsökvägar.

* Felmeddelandet när det maximala antalet databaser har uppnåtts specificerade inte orsaken till felet.

* I sällsynta fall misslyckades rörledningar på grund av olämplig hantering av vissa svarskoder.


## Releasedatum {#release-date-cm-oct}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.10.0 är 14 oktober 2021.

### Nyheter {#what-is-new-cm-oct}

* Som förberedelse för vissa kommande ändringar kommer befintliga distributionspipelines nu att refereras och märkas i användargränssnittet som **fullständigt stackade**-pipelines.

* Pipelinekortet har uppdaterats så att det nu visas ett enda, integrerat ansikte som visar både pipelines för produktion och icke-produktion, och användaren kan välja Kör/Pausa/Fortsätt direkt på den åtgärdsmeny som är kopplad till varje pipeline.

* En användare i rollen Distributionshanterare kan nu ta bort produktionsflödet via självbetjäning via gränssnittet.

* Lägg till och redigera rörliga upplevelser har uppdaterats för att nu använda välbekanta, moderna moduler.

* Cloud Manager-användare kan nu skicka feedback direkt från användargränssnittet via knappen **Feedback** överst till höger på landningssidan.

* Årliga SLA-diagram kan nu hämtas från Cloud Manager användargränssnitt.

* Kodkvalitet och icke-produktionsrelaterade pipeline-körningar kommer nu att använda en mer effektiv, ytlig kloningsprocess under byggsteget, vilket ger en snabbare byggtid för kunder med särskilt stora Git-databaser.

* Guiden Lägg till IP Tillåtelselista informerar nu användaren om maximalt tillåtet antal IP-Tillåtelselista har uppnåtts.

* Cloud Manager API-dokumentationen innehåller nu en interaktiv spelningsmiljö som gör att inloggade användare kan experimentera med API:t från sin webbläsare. Mer information finns i [Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/).

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
