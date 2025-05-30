---
title: Versionsinformation för version 2021.11.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.11.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1058'
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

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2021.11.0) är 16 december 2021.
Följande version (2022.1.0) är den 3 februari 2022.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt för december 2021](https://video.tv.adobe.com/v/339278) om du vill se en sammanfattning av funktioner som lagts till i version 2021.11.0 (november 2021).

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Dynamic Media Image Smart Crop och Swatch drivs nu av de senaste Sensei-tjänsterna som genererar förbättrade beskärningar och färgrutor. Dessutom har en förbättring startats för att generera olika beskärningsinnehåll, med samma proportioner men med olika upplösningar. Dessutom behålls alla manuella redigeringar vid ombearbetningen om bredden och höjden inte ändras i bildprofilen.

### Nya funktioner i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

* [!DNL Dynamic Media] - Du kan nu använda AEM Dynamic Media-gränssnitt för att konfigurera allmänna inställningar och Publish-inställningar i stället för att behöva gå igenom Dynamic Media Classic skrivbordsprogram.

* [!DNL Dynamic Media] har nu stöd för hämtning, förhandsgranskning, uppspelning och publicering för MXF-videor. Anteckningar och videor som kan köpas för MXF-videor stöds ännu inte.

* När du har konfigurerat en anslutning mellan distributioner av fjärr-DAM och platser, blir resurserna på fjärr-DAM tillgängliga i Sites-distributionen. Du kan nu utföra [uppdaterings-, borttagnings-, namnbyt- och flyttåtgärderna](/help/assets/use-assets-across-connected-assets-instances.md) på fjärr-DAM-resurser eller -mappar. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **Gör AEM arbetsflödesdata externt för säker bearbetning**: Du kan lagra processdata AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga SPD-element (Personal Data) i en kundhanterad databas för säker bearbetning. Dataelementen och arbetsflödesvariablerna lagras inte i AEM och hämtas på begäran från en kundhanterad databas när arbetsflödet bearbetas.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=sv-SE) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   * Generera dokument genom att fylla i mallfiler (PDF och XDP) med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.

* **Anpassade teckensnitt för dokument med dokumentinformation och PDF som skapats med kommunikations-API:er**: Du kan nu använda teckensnitt som godkänts av varumärket i PDF-dokument som skapats med kommunikations-API:er för att anpassa dem efter organisationens krav.

* **Forms Portal**: Du kan använda [Forms Portal](/help/forms/configure-forms-portal.md) för att lista dina publicerade adaptiva formulär på en AEM Sites-sida. Det hjälper en besökare att hitta alla tillgängliga formulär. Dessutom kan besökaren använda formulärportalen för att spara och komma åt utkast av ett adaptivt formulär och titta på PDF-versionen av ett skickat adaptivt formulär.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Utökade myAccount-komponenter som baseras på Commerce utbyggbara Premiere-komponenter

![Utökade komponenter för mitt konto](/help/assets/CIF/extended-myAccount-components.png)

* Författare kan skapa ad hoc-produkter för Commerce Recommendations med hjälp av ytterligare rekommendationstyper

* Stöd för presentkort i AEM Storefront

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.11.0.

### Releasedatum {#release-date-cm-nov}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.11.0 är 4 november 2021.
Nästa version är planerad till 9 december 2021.

### Nyheter {#what-is-new-cm-nov}

* Användare kan nu använda nya frontledningslinjer för att exklusivt distribuera slutkod på ett accelererat sätt. Mer information finns i [Cloud Manager Front End Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end).

  >[!IMPORTANT]
  >Du måste ha AEM version `2021.10.5933.20211012T154732Z` eller senare för att kunna använda nya frontendpipelines.

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

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.22 är 1 december 2021.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka och rapportera vilken version av ACS-kommandon som används.
* Möjlighet att identifiera och rapportera antalet användare och undergrupper i en grupp.
* Möjlighet att identifiera och rapportera om egenskapsvärden för noder i MongoDB som överstiger 16 MB.

### Felkorrigeringar {#bug-fixes-bpa}

* Identifieringen av Foundation-komponenter förfinades för att minska falska negativ.
* För AEM Forms-kunder har BPA-meddelanden om att `EMAIL_PDF_SUBMIT_ACTION` inte är tillgänglig på AEM as a Cloud Service korrigerats.
