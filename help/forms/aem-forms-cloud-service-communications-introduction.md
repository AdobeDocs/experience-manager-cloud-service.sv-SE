---
title: AEM Forms as a Cloud Service Communication APIs
description: Generera, hantera och skydda dokument med AEM Forms Communication API:er i molnet
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---


# AEM Forms as a Cloud Service Communication APIs {#communications-apis-overview}

> **Versionstillgänglighet**
>
> * **AEM 6.5**: [Översikt över AEM Document Services](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html)
> * **AEM as a Cloud Service**: Den här artikeln

## Introduktion

Med API:er för kommunikation i AEM Forms as a Cloud Service kan ni skapa varumärkesgodkända, personaliserade och standardiserade dokument för era affärsbehov. Med dessa kraftfulla API:er kan du generera, manipulera och skydda dokument programmatiskt, oavsett om det är vid behov eller i gruppprocesser med stora volymer.


### Viktiga fördelar

* **Effektiv dokumentgenerering** - Skapa anpassade dokument genom att sammanfoga mallar med kunddata
* **Kraftfull dokumentredigering** - Kombinera, ordna om och validera PDF-dokument via programmering
* **Flexibla distributionsalternativ** - Använd on-demand-API:er för låg latens eller batch-API:er för åtgärder med hög genomströmning
* **Förbättrat skydd** - Använd digitala signaturer, certifiering och kryptering för att skydda känsliga dokument
* **Molnbaserad arkitektur** - Utnyttja skalbar, säker molninfrastruktur utan extra kostnad för underhåll

## Nyckelfunktioner

API:er för kommunikation har en omfattande uppsättning funktioner för dokumentbearbetning som är organiserade i följande funktionsområden:


| Dokumentgenerering | Dokumentmanipulering | Extrahering av dokument | Dokumentkonvertering | Document Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| Generera skräddarsydda dokument genom att sammanfoga mallar med data i olika format, inklusive PDF och utskriftsformat. | Kombinera, ordna om och validera PDF-dokument programmatiskt för att skapa nya dokumentpaket. | Extrahera egenskaper, metadata och innehåll från PDF-dokument för vidare bearbetning. | Konvertera dokument mellan format, inklusive PDF/A-validering för arkiveringsbehov. | Använd digitala signaturer, certifiering och kryptering för att skydda och skydda dokument. |

## Dokumentgenerering

API:er för dokumentgenerering för kommunikation kombinerar mallar (XFA eller PDF) med kunddata (XML) för att skapa anpassade dokument i PDF och olika utskriftsformat (PS, PCL, DPL, IPL, ZPL).

### Hur dokumentgenerering fungerar

Det typiska arbetsflödet är:

1. Skapa en mall med [Designer](use-forms-designer.md)
2. Förbereda XML-data för att fylla i mallen
3. Använda kommunikations-API:er för att sammanfoga mallen med data
4. Generera utdatadokument i det format du önskar

![Arbetsflöde för dokumentgenerering för kommunikation](assets/communicaions-workflow.png)

### Skapa PDF-dokument

Med API:erna för dokumentgenerering kan du skapa icke-interaktiva PDF-dokument genom att sammanfoga XML-data med formulärmallar:

![Skapa PDF-dokument](assets/outPutPDF_popup.png)

Du kan leverera genererade PDF-filer till användare via nedladdningar, lagra dem i en databas eller överföra dem till Azure Blob Storage.

<span class="preview">Överför genererade PDF-filer till Azure Blob Storage är tillgängligt via [Tidigt Adobe-program](/help/forms/early-access-ea-features.md). Kontakta aem-forms-ea@adobe.com från din officiella e-postadress om du vill gå med.</span>

### Skapa dokument i utskriftsformat

Generera dokument i utskriftsformat som:
* PostScript (PS)
* PCL (Printer Command Language)
* Zebra Printing Language (ZPL)

De här formaten är idealiska för stora utskriftsvolymer och specialiserade utskriftsbehov.

### Gruppbearbetning för flera dokument

Bearbeta stora dokumentvolymer effektivt med batch-API:er:

![Gruppbearbetning av arbetsflöde](assets/ou_OutputBatchMany_popup.png)

Med batchbearbetning kan du:

* Generera separata dokument för varje post i en XML-datakälla
* Bearbeta dokument asynkront för bättre prestanda
* Konfigurera olika konverteringsparametrar för batchprocessen

## Dokumentmanipulering

API:er för dokumentredigering hjälper dig att kombinera, ordna om och omvandla PDF-dokument programmatiskt.

### Dokumentmontering

Slå ihop flera PDF- eller XDP-dokument till ett enda sammanhängande dokument:

![Sammanställa ett enkelt PDF-dokument från flera PDF-dokument](assets/as_document_assembly.png)

Funktioner för dokumentsammanställning:
* Skapa enkla PDF-dokument från olika källor
* Bygger PDF Portfolios
* Sammanställa krypterade dokument
* Lägga till Bates-numrering för juridiska dokument
* Förenkla och sammanfoga interaktiva formulär

### Dokumentdemontering

Dela upp stora PDF-dokument i mindre, mer hanterbara komponenter:

![Dela upp ett källdokument baserat på bokmärken i flera dokument](assets/as_intro_pdfsfrombookmarks.png)

Med dokumentdemontering kan du:
* Extrahera specifika sidor från källdokument
* Dela dokument baserat på bokmärken
* Skapa logiska dokumentuppsättningar från större kompileringar

>[!NOTE]
>
> AEM Forms innehåller många inbyggda teckensnitt som är helt integrerade med PDF-filer. [Klicka här](/help/forms/supported-out-of-the-box-fonts.md) om du vill se en fullständig lista över teckensnitt som stöds.

## Extrahering av dokument

<span class="preview">Dokumentextraheringen är tillgänglig via [Tidigt Adobe-program](/help/forms/early-access-ea-features.md). Kontakta aem-forms-ea@adobe.com från din officiella e-postadress om du vill gå med.</span>

Med API:er för dokumentextrahering kan du hämta information från PDF-dokument, inklusive:

* Dokumentegenskaper (är det ett ifyllbart formulär, har det bifogade filer osv.)
* Användningsrättigheter och behörigheter
* Metadatainformation med Adobe Extensible Metadata Platform (XMP)

Den här funktionen är särskilt användbar för dokumenthanteringssystem, arkiveringslösningar och automatisering av arbetsflöden.

## Dokumentkonvertering

### Konvertering och validering av PDF/A

Konvertera PDF-dokument till PDF/A-format för långtidsarkivering:

* Stöd för standarderna PDF/A-1a, 1b, 2a, 2b, 3a och 3b
* Verifiering av PDF/A-överensstämmelse
* Bevara dokumentens integritet med inbäddade teckensnitt och okomprimerat innehåll

### Konvertering av PDF till XDP

<span class="preview">Konvertering från PDF till XDP är tillgängligt via [Tidigt Adobe-program](/help/forms/early-access-ea-features.md). Kontakta aem-forms-ea@adobe.com från din officiella e-postadress om du vill gå med.</span>

Konvertera PDF-dokument som innehåller XFA-strömmar till XDP-format för mallredigering och återanvändning.

## Document Assurance {#doc-assurance}

Document Assurance innehåller API:er för signatur och kryptering för att skydda dina dokument under hela deras livscykel.

### Signatur-API:er

Skydda PDF-dokument med digitala signaturer och certifiering:

* Lägg till synliga eller osynliga signaturfält
* Signera signaturfält digitalt
* Certifiera dokument för integritet
* Ta bort signaturer från dokument
* Ta bort signaturfält från dokument

<span class="preview">Borttagning av signaturer och borttagning av signaturfält är tillgängligt via [Tidigt Adobe-program](/help/forms/early-access-ea-features.md). Kontakta aem-forms-ea@adobe.com från din officiella e-postadress om du vill gå med.</span>

### Krypterings-API:er

Skydda dokumentinnehåll med kryptering:

* Kryptera PDF-dokument med lösenord
* Ta bort lösenordsbaserad kryptering
* Fastställa dokumentskyddstyper
* Hämta säkerhetsinformation från skyddade dokument

### Dokumentverktyg {#doc-utility}

Dokumentverktygen har ytterligare funktioner för att arbeta med PDF-dokument:

#### API:er för användningsrättigheter (Reader Extension)

<span class="preview">Användningsrättigheter (Reader-tillägg) är tillgängliga via [Tidigt Adobe-program](/help/forms/early-access-ea-features.md). Kontakta aem-forms-ea@adobe.com från din officiella e-postadress om du vill gå med.</span>

Utöka funktionaliteten i Adobe Reader genom att lägga in användarrättigheter i PDF-dokument, vilket ger funktioner som:

* Fylla i och spara formulär
* Lägga till kommentarer och anteckningar
* Digital signering
* Bifogade filer
* Import/export av formulärdata
* Tillgång till webbtjänster och databaser

Tillgängliga användningsrättigheter:

* **Formulärinteraktion**: Formulärfyllning, Importera/exportera formulärdata, dynamiska formulärfält/sidor
* **Anteckningar**: Kommentarer (online och offline), digitala signaturer
* **Dokumenthantering**: Inbäddade filer, fristående skickning, avkodning av streckkoder
* **Onlinetjänster**: Forms online, tillgång till webbtjänster

## Olika typer av kommunikations-API:er {#types}

Kommunikationen innehåller två typer av API:er som passar olika användningsområden:

### Synkrona API:er

**Bäst för**: Generering av enstaka dokument på begäran, låg latens
**Användningsexempel**: Dokumentgenerering som aktiveras av användaren, interaktiva program
**Dokumentation**: [Synkron API-referens](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

### Batch-API:er (asynkrona)

**Bäst för**: Schemalagd, hög genomströmning, generering av flera dokument
**Användningsfall**: Månadssatser, växlar, meddelanden, schemalagda rapporter
**Dokumentation**: [API-referens för batch](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

## Komma igång med kommunikations-API:er

### Onboarding-process

Kommunikation finns som fristående modul eller tillägg för användare av Forms as a Cloud Service:

1. Kontakta Adobe direktförsäljning eller din Adobe-representant för att få åtkomst
2. Adobe ger åtkomst till din organisation och ger administratörsbehörighet
3. Din administratör kan sedan bevilja utvecklare i din organisation åtkomst

### Aktivera kommunikation i din miljö

Följ de här stegen för att aktivera kommunikation för din Forms as a Cloud Service-miljö:

1. Logga in på Cloud Manager och öppna AEM Forms as a Cloud Service Instance
2. Öppna alternativet Redigera program och gå till fliken Lösningar och tillägg
3. Välj alternativet **[!UICONTROL Forms - Communications]**

   ![Kommunikation](assets/communications.png)

   Om du redan har aktiverat **[!UICONTROL Forms - Digital Enrollment]** väljer du alternativet **[!UICONTROL Forms - Communications Add-On]** i stället.

   ![Lägg till](assets/add-on.png)

4. Klicka på **[!UICONTROL Update]**
5. Kör byggprocessen - Kommunikations-API:er aktiveras när det är klart

>[!NOTE]
>
> Om du vill aktivera API:er för dokumentbearbetning lägger du till följande regel i [Dispatcher-konfigurationen](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## API-referensdokumentation {#api-reference}

Kommunikations-API:er är ordnade i flera funktionskategorier, var och en med detaljerad referensdokumentation. Dessa API-referenser innehåller omfattande information om slutpunkter, parametrar, fråge-/svarsformat och autentiseringskrav.

### API för dokumentgenerering

| API | Beskrivning | Referenslänk |
|-----|-------------|----------------|
| Dokumentgenerering - synkron | Generera dokument on demand med låg latens för interaktiva scenarier | [API-referens](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/) |
| Dokumentgenerering - batch | Bearbeta stora dokumentvolymer asynkront för schemalagda åtgärder | [API-referens](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/) |

### API:er för dokumenthantering

| API | Beskrivning | Referenslänk |
|-----|-------------|----------------|
| Dokumentmanipulering - synkron | Kombinera, dela och omvandla PDF-dokument med DDX-anvisningar | [API-referens](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/) |

### Dokument-API:er för Assurance

| API | Beskrivning | Referenslänk |
|-----|-------------|----------------|
| DocAssurance - synkron | Använd digitala signaturer, certifiering, kryptering och läsartillägg | [API-referens](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/docassurance/) |

### Vanliga API-parametrar

Varje API-kategori har specifika parametrar, men några vanliga parametrar är:

#### Parametrar för dokumentgenerering

| Parameter | Typ | Obligatoriskt | Beskrivning |
|-----------|------|----------|-------------|
| `template` | Sträng | Ja | Sökväg till XDP- eller PDF-mallfilen |
| `data` | Sträng | Nej | XML-data som ska sammanfogas med mallen |
| `outputOptions` | Objekt | Nej | Konfigurationsalternativ för utdatadokumentet |

#### Parametrar för dokumentmanipulering

| Parameter | Typ | Obligatoriskt | Beskrivning |
|-----------|------|----------|-------------|
| `ddx` | Sträng | Ja | DDX-instruktioner för dokumentmontering eller dokumentdemontering |
| `inputDocuments` | Objekt | Ja | Karta över indatadokument som ska bearbetas |
| `outputOptions` | Objekt | Nej | Konfigurationsalternativ för utdatadokumentet |

#### Assurance-parametrar för dokument

| Parameter | Typ | Obligatoriskt | Beskrivning |
|-----------|------|----------|-------------|
| `inputPDF` | Sträng | Ja | Indata i PDF-dokument som ska skyddas eller signeras |
| `certificateAlias` | Sträng | Villkorlig | Alias för certifikatet för signeringsåtgärder |
| `credentialPassword` | Sträng | Villkorlig | Lösenord för de autentiseringsuppgifter som används vid signering |

Fullständig parameterinformation, autentiseringskrav och exempelbegäranden/svar finns i den specifika API-referensdokumentation som är länkad i tabellerna ovan.

## Ytterligare resurser {#see-also}

* [Kommunikationsbearbetning - Synkrona API:er](/help/forms/aem-forms-cloud-service-communications.md)
* [Kommunikationsbearbetning - batch-API:er](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [AEM Forms as a Cloud Service Architecture](/help/forms/aem-forms-cloud-service-architecture.md)
* [API-referensdokumentation](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [Tidiga funktioner i Adobes program](/help/forms/early-access-ea-features.md)
