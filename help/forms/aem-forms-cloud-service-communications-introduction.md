---
title: AEM Forms as a Cloud Service Communication APIs
description: Generera, hantera och skydda dokument med AEM Forms Communication API:er i molnet
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a5bbcd19b41b3aeff94f900da13e98de65651f8c
workflow-type: tm+mt
source-wordcount: '2488'
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

## API Capabilities Overview

API:er för kommunikation har en omfattande uppsättning funktioner för dokumentbearbetning som är organiserade i följande funktionsområden:

| Dokumentgenerering | Dokumentmanipulering | Extrahering av dokument | Dokumentkonvertering | Document Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| Generera skräddarsydda dokument genom att sammanfoga mallar med data i olika format, inklusive PDF och utskriftsformat. | Kombinera, ordna om och validera PDF-dokument programmatiskt för att skapa nya dokumentpaket. | Extrahera egenskaper, metadata och innehåll från PDF-dokument för vidare bearbetning. | Konvertera dokument mellan format, inklusive PDF/A-validering för arkiveringsbehov. | Använd digitala signaturer, certifiering och kryptering för att skydda och skydda dokument. |

[API-referensdokumentationen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) innehåller detaljerad information om alla parametrar, autentiseringsmetoder och olika tjänster som tillhandahålls av API:er. API-referensdokumentationen finns också i .yaml-format. Du kan hämta .yaml-filen och överföra den till Postman för att kontrollera API:ernas funktioner.

## Dokumentgenerering

API:er för dokumentgenerering för kommunikation hjälper dig att kombinera en mall (XFA eller PDF) med kunddata (XML) för att generera dokument i PDF och utskriftsformat som PS, PCL, DPL, IPL och ZPL. Dessa API:er använder PDF- och XFA-mallar med [XML-data](communications-known-issues-limitations.md#form-data) för att generera ett enda dokument vid behov eller flera dokument med hjälp av ett batchjobb.

Vanligtvis skapar du en mall med [Designer](use-forms-designer.md) och använder kommunikationsAPI:er för att sammanfoga data med mallen. Programmet kan skicka utdatadokumentet till en nätverksskrivare, en lokal skrivare eller till ett lagringssystem för arkivering. Ett typiskt exempel och anpassade arbetsflöden ser ut så här:

![Arbetsflöde för dokumentgenerering för kommunikation](assets/communicaions-workflow.png)

Beroende på hur de används kan du även göra dessa dokument tillgängliga för hämtning via din webbplats eller en lagringsserver.

### Nyckelfunktioner för dokumentgenerering

#### Skapa PDF-dokument {#create-pdf-documents}

Du kan använda API:erna för dokumentgenerering för att skapa ett PDF-dokument som baseras på en formulärdesign och XML-formulärdata. Utdata är ett icke-interaktivt PDF-dokument. Användarna kan alltså inte ange eller ändra formulärdata. Ett grundläggande arbetsflöde är att sammanfoga XML-formulärdata med en formulärdesign för att skapa ett PDF-dokument. I följande bild visas hur du sammanfogar en formulärdesign och XML-formulärdata för att skapa ett PDF-dokument.

![Skapa PDF-dokument](assets/outPutPDF_popup.png)
Bild: Vanligt arbetsflöde för att skapa ett PDF-dokument

API:t för dokumentgenerering returnerar det genererade PDF-dokumentet. Du kan också överföra de genererade PDF-filerna till Azure Blob Storage.

<span class="preview"> Överför genererade PDF-filer med hjälp av dokumentgenererings-API:t till Azure Blob Storage-funktionen under [Tidigt Adobe-program](/help/forms/early-access-ea-features.md). Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

#### Skapa dokument för PostScript (PS), Printer Command Language (PCL) och Zebra Printing Language (ZPL) {#create-PS-PCL-ZPL-documents}

Du kan använda API:er för dokumentgenerering för att skapa dokument i formaten PostScript (PS), Printer Command Language (PCL) och Zebra Printing Language (ZPL) som baseras på en XDP-formulärdesign eller ett PDF-dokument. Dessa API:er hjälper till att sammanfoga en formulärdesign med formulärdata för att generera ett dokument. Du kan spara dokumentet i en fil och utveckla en anpassad process för att skicka det till en skrivare.

#### Bearbeta gruppdata för att skapa flera dokument {#processing-batch-data-to-create-multiple-documents}

Du kan använda API:er för dokumentgenerering för att skapa separata dokument för varje post i en XML-batchdatakälla. Du kan generera dokument i både gruppläge och asynkront läge. Du kan konfigurera olika parametrar för konverteringen och sedan starta gruppbearbetningen.

![Skapa PDF-dokument](assets/ou_OutputBatchMany_popup.png)

## Dokumentmanipulering

API:er för dokumentbearbetning (Document Transformation) hjälper dig att kombinera och ordna om PDF-dokument. Vanligtvis skapar du en DX och skickar den till dokumenthanterings-API:er för att montera eller ordna om ett dokument. [DDX-dokumentet](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) innehåller instruktioner om hur du använder källdokumenten för att skapa en uppsättning med obligatoriska dokument. DDX-referensdokumentationen innehåller detaljerad information om alla åtgärder som stöds.

### Funktioner för hantering av nyckeldokument

#### Sammanställa PDF-dokument

Du kan använda API:erna för dokumentmanipulering för att samla ihop två eller flera PDF- eller XDP-dokument till ett enda PDF-dokument eller PDF Portfolio. Här är några sätt att sammanställa PDF-dokument:

* Sammanställa ett enkelt PDF-dokument
* Skapa en PDF Portfolio
* Sammanställa krypterade dokument
* Sammanställa dokument med Bates-numrering
* Förenkla och sammanställ dokument

![Sammanställa ett enkelt PDF-dokument från flera PDF-dokument](assets/as_document_assembly.png)
Bild: Sammanställa ett enkelt PDF-dokument från flera PDF-dokument

#### Disassemblera PDF-dokument

Du kan använda API:erna för dokumentbearbetning för att demontera ett PDF-dokument. API:erna kan extrahera sidor från källdokumentet eller dela upp ett källdokument baserat på bokmärken. Vanligtvis är den här uppgiften användbar om PDF-dokumentet ursprungligen skapades från många enskilda dokument, till exempel en samling programsatser.

* Hämta sidor från ett källdokument
* Dela upp ett källdokument baserat på bokmärken

![Dela upp ett källdokument baserat på bokmärken i flera dokument](assets/as_intro_pdfsfrombookmarks.png)
Bild: Dela upp ett källdokument baserat på bokmärken i flera dokument

>[!NOTE]
>
> AEM Forms har en mängd inbyggda teckensnitt som är sömlöst integrerade med PDF-filer. [Klicka här](/help/forms/supported-out-of-the-box-fonts.md) om du vill visa en lista över teckensnitt som stöds.

## Extrahering av dokument

<span class="preview"> Funktionen för dokumentextrahering är under Tidiga Adobe-program. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Med dokumentextraheringstjänsten kan du hämta egenskaperna för ett PDF-dokument, t.ex. användarbehörighet, PDF-egenskaper och metadata. Extraheringsfunktionerna är:

* Hämtar egenskaperna för ett PDF-dokument, t.ex. om PDF har bilagor, kommentarer, Acrobat-version och många andra.
* Extrahera användningsrättigheterna som är aktiverade i ett PDF-dokument och få åtkomst till användningsrättigheterna som är aktiverade eller inaktiverade i ett PDF-dokument för Adobe Acrobat Reader-utbyggbarhet.
* Hämta metadatainformationen som finns i ett PDF-dokument. Metadata är information om dokumentet (som skiljer sig från dokumentets innehåll, som text och bilder). Adobe Extensible Metadata Platform (XMP) är en standard för hantering av dokumentmetadata. XMP Utilities kan hämta XMP-metadata från PDF-dokument och exportera XMP-metadata till PDF-dokument.

[API-referensdokumentationen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) innehåller detaljerad information om alla parametrar, autentiseringsmetoder och tjänster som tillhandahålls av API:er. API-referensdokumentationen finns också i .yaml-format. Du kan hämta .yaml-filen och överföra den till Postman för att kontrollera API:ernas funktioner.

## Dokumentkonvertering

### Konvertera till och validera PDF/A-dokument

API:er för dokumentkonvertering för kommunikation hjälper till att konvertera ett PDF-dokument till PDF/A. Du kan använda API:erna för att konvertera ett PDF-dokument till ett PDF/A-kompatibelt dokument och även för att avgöra om ett PDF-dokument är PDF/A-kompatibelt. PDF/A är ett arkiveringsformat som används för långtidsarkivering av dokumentets innehåll. Teckensnitten bäddas in i dokumentet och filen är okomprimerad. Därför är ett PDF/A-dokument vanligtvis större än ett vanligt PDF-dokument. Ett PDF/A-dokument innehåller inte heller ljud- och videoinnehåll. De kompatibilitetsstandarder för PDF/A som stöds är PDF/A-1a, 1b, 2a, 2b, 3a och 3b.

### Konvertera PDF till XDP {#convert-pdf-to-xdp}

<span class="preview"> Funktionen för att konvertera PDF till XDP finns i Tidigt Adobe-program. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Konverterar PDF-dokument till XDP-filer. För att ett PDF-dokument ska kunna konverteras till en XDP-fil måste PDF-dokumentet innehålla en XFA-ström i ordlistan.

## Document Assurance {#doc-assurance}

Tjänsten DocAssurance innehåller API:erna för signatur och kryptering:

### Signatur-API:er

Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. <!--This service uses digital signatures and certification to ensure that only intended recipients can alter documents. --> Säkerhetsfunktionerna tillämpas på själva dokumentet. Dokumentet förblir säkert och styrs under hela livscykeln. Dokumentet förblir säkert även utanför brandväggen när det laddas ned offline och när det skickas tillbaka till organisationen. Du kan utföra följande uppgifter med signatur-API:erna:

* Lägg till ett synligt signaturfält i ett PDF-dokument.
* Lägg till ett osynligt signaturfält i ett PDF-dokument.
* Signera det angivna signaturfältet i ett PDF-dokument.
* Certifiera ett PDF-dokument
* Ta bort signaturen från det angivna signaturfältet i ett PDF-dokument
* Ta bort det angivna signaturfältet från ett PDF-dokument

<span class="preview"> Ta bort signaturen från det angivna signaturfältet och ta bort det angivna signaturfältet från ett PDF-dokument som är tillgängligt under det tidiga adopterprogrammet. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

### Krypterings-API:er

Med krypterings-API:erna kan du kryptera och dekryptera dokument. När ett dokument är krypterat blir innehållet oläsligt. En behörig användare kan dekryptera dokumentet för att få åtkomst till innehållet. Om ett PDF-dokument är krypterat med ett lösenord måste användaren ange det öppna lösenordet innan dokumentet kan visas i Adobe Reader eller Adobe Acrobat. <!-- Likewise, if a PDF document is encrypted with a certificate, the user must decrypt the PDF document with the public key that corresponds to the certificate (private key) that was used to encrypt the PDF document.-->

Du kan utföra följande uppgifter med krypterings-API:erna:

* Kryptera ett PDF-dokument med ett lösenord.
* Ta bort lösenordsbaserad kryptering från ett PDF-dokument.
* Hämta den typ av skydd som används för ett PDF-dokument.
* Returnera den säkerhetstyp som används i ett PDF-dokument.

Både signatur-API:er och krypterings-API:er är [synkrona API:er](#types-of-communications-apis-types).

### Dokumentverktyg {#doc-utility}

Dokumentverktyg med synkrona API:er hjälper dig att konvertera dokument mellan filformaten PDF och XDP. Använd användarrättigheter för ett dokument och extrahera de aktiverade användningsrättigheterna från ett dokument. Fråga om information om ett PDF-dokument. <!-- determines whether a PDF document contains comments or attachments and more, and use document transformation services for XMP utilities--> Information om API:er för användningsrättigheter anges nedan:

#### API:er för användningsrättigheter (Reader Extension)

<span class="preview"> Funktionen Användningsrättigheter (Reader Extension) finns under Tidiga Adobe-programmet. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Med rättigheten kan man enkelt utbyta interaktiva PDF-dokument genom att utöka funktionaliteten i Adobe Reader med ytterligare användarrättigheter. Tjänsten fungerar med Adobe Reader 7.0 eller senare och lägger in användarrättigheter i ett PDF-dokument. Den här åtgärden aktiverar funktioner som normalt inte är tillgängliga när ett PDF-dokument öppnas med Adobe Reader, t.ex. för att lägga till kommentarer i ett dokument, fylla i formulär och spara dokumentet.

När PDF-dokument har rätt användarbehörighet kan mottagarna göra följande i Adobe Reader:

* Fyll i PDF-dokument och -blanketter online eller offline så att mottagarna kan spara kopior lokalt och behålla den information de lagt in.
* Spara PDF-dokument på en lokal hårddisk om du vill behålla originaldokumentet och eventuella ytterligare kommentarer, data eller bilagor.
* Bifoga filer och medieklipp i PDF-dokument.
* Signera, certifiera och autentisera PDF-dokument genom att använda digitala signaturer med PKI-teknik (public key infrastructure) som är branschstandard.
* Skicka in ifyllda eller kommenterade PDF-dokument elektroniskt.
* Använd PDF dokument och blanketter som en intuitiv utvecklingsmiljö för interna databaser och webbtjänster.
* Utbyt PDF-dokument med andra så att granskarna kan kommentera med de intuitiva kommentarverktygen. Bland dessa verktyg finns elektroniska notisar, stämplar, högdagrar och textöverstrykning. Samma funktioner är tillgängliga i Acrobat.
* Support Barcoded Forms decoding.

Dessa specialfunktioner aktiveras automatiskt när ett rättighetsaktiverat PDF-dokument öppnas i Adobe Reader. När användaren är klar med ett rättighetsaktiverat dokument inaktiveras dessa funktioner igen i Adobe Reader. De är inaktiverade tills användaren får ett annat rättighetsaktiverat PDF-dokument.

#### Aktivera eller inaktivera användningsrättigheter

De olika funktionerna för användarrättigheter för att utöka PDF Reader tjänster är:

* **Streckkoder avkodas**: Om du vill avkoda streckkoder i PDF-dokumentet.

* **Kommentarer**: Om du vill kommentera offline i PDF-dokumentet.

* **Kommentarer online**: Om du vill kommentera online i PDF-dokumentet.

* **Digital signatur**: Så här lägger du till digitala signaturer i ett PDF-dokument.

* **Dynamiska formulärfält**: Lägga till formulärfält i ett PDF-dokument.

* **Dynamiska formulärsidor**: Så här lägger du till formulärsidor i ett PDF-dokument.

* **Inbäddade filer**: Om du vill bädda in filer i ett PDF-dokument.

* **Importera formulärdata**: Så här importerar du formulärdata till ett PDF-dokument.

* **Formulärdataexport**: Så här importerar du formulärdata till ett PDF-dokument.

* **Formulärfyllning**: Om du vill fylla i formulärfält i ett PDF-dokument.

* **Online Forms**: Så här kommer du åt en webbtjänst eller databas från ett PDF-dokument.

* **Skicka fristående**: Skicka formulärdata offline från ett PDF-dokument.

#### Andra funktioner

* **Meddelande**: Meddelandet som visas i Adobe Acrobat Reader när ett PDF-dokument öppnas med en eller flera användningsrättigheter.
* **Lås upp lösenord**: Lösenordet som krävs för att öppna ett krypterat PDF-dokument. Det här är vanligtvis lösenordet för dokumentöppning, men om PDF-dokumentet dessutom skyddas av ett behörighetslösenord kan det användas för att öppna det.

## Typer av API:er för kommunikation {#types}

Kommunikationen tillhandahåller HTTP-API:er för on demand- och batchdokumentgenerering:

* **[Synkrona API:er](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** är lämpliga för dokumentgenerering on demand, low latency och single record. Dessa API:er lämpar sig bättre för användaråtgärdsbaserade användningsfall. Du kan till exempel skapa ett dokument när en användare har fyllt i ett formulär.

* **[Batch-API:er (asynkrona API:er)](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** passar för schemalagda, höga genomströmningsscenarier och flera dokumentgenereringsscenarier. Dessa API:er genererar dokument gruppvis. Till exempel genereras telefonräkningar, kreditkortsräkningar och förmånsräkningar varje månad.

## Onboarding

Kommunikationsfunktioner finns som fristående modul och tilläggsmodul för användare av Forms as a Cloud Service. Du kan kontakta Adobe säljteam eller din Adobe-representant för att få åtkomst. Adobe aktiverar åtkomst för organisationen och tillhandahåller behörigheter åt den person som utses till administratör i organisationen. Administratören kan ge Forms as a Cloud Service-utvecklare (användare) i organisationen åtkomst till API:erna.

Efter introduktionen, för att aktivera kommunikationsfunktioner för din Forms as a Cloud Service-miljö:

1. Logga in på Cloud Manager och öppna AEM Forms as a Cloud Service Instance.

1. Öppna alternativet Redigera program, gå till fliken Lösningar och tillägg och välj alternativet **[!UICONTROL Forms - Communications]**.

   ![Kommunikation](assets/communications.png)

   Om du redan har aktiverat alternativet **[!UICONTROL Forms - Digital Enrollment]** väljer du alternativet **[!UICONTROL Forms - Communications Add-On]**.

   ![Lägg till](assets/add-on.png)

1. Klicka på **[!UICONTROL Update]**.

1. Kör byggprocessen. När byggprocessen är klar aktiveras API:er för kommunikation för din miljö.

>[!NOTE]
>
> Om du vill aktivera och konfigurera API:er för dokumentbearbetning lägger du till följande regel i [Dispatcher-konfigurationen](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Ytterligare resurser {#see-also}

* [Kommunikationsbearbetning - Synkrona API:er](/help/forms/aem-forms-cloud-service-communications.md)
* [Kommunikationsbearbetning - batch-API:er](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [AEM Forms as a Cloud Service Architecture](/help/forms/aem-forms-cloud-service-architecture.md)
* [API-referensdokumentation](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [Tidiga funktioner i Adobes program](/help/forms/early-access-ea-features.md)
