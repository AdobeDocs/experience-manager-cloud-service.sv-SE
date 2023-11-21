---
title: Vad är Forms API:er för as a Cloud Service Communication?
description: Använd kommunikations-API:er för att signera, certifiera eller skydda dina dokument, för att automatisera PDF-genereringsprocesser och för att konvertera PDF-dokument till ett annat format.
Keywords: How to generate document?, Generate PDF document, Manipulation PDF documents, Assembling PDF documents, Validating PDF document, APIs used in encrypting or decrypting PDFs
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 1%

---

# Introduktion till AEM Forms as a Cloud Service Communications {#frequently-asked-questions}


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html) |
| AEM as a Cloud Service | Den här artikeln |

Med kommunikationsfunktioner kan ni skapa varumärkesgodkända, personaliserade och standardiserade dokument som affärskontakter, kontoutdrag, kravbrev, förmånsmeddelanden, månatliga fakturor eller välkomstpaket.

Funktionen ger API:er för att generera och hantera dokument. Du kan generera eller ändra ett dokument on demand eller skapa ett batchjobb för att generera flera dokument med definierade intervall. Kommunikations-API:er ger:

* smidiga funktioner för att generera on demand- och batchdokumentation.

* möjlighet att kombinera, ordna om och validera PDF-dokument on-demand.

* HTTP-API:er för enklare integrering med externa system. Separata API:er för on demand-åtgärder (låg fördröjning) och batchåtgärder (högdataåtgärder) ingår.

* säker åtkomst till data. Kommunikations-API:er ansluter till och får endast åtkomst till data från kundutsedda datalager, vilket gör kommunikationen mycket säker.

![Exempel på kreditkortsutdrag](assets/statement.png)
Du kan skapa ett kreditkortsutdrag med API:er för kommunikation. Det här exempelkontoutdraget använder samma mall men separata data för varje kund beroende på hur de använder kreditkortet.

## Dokumentgenerering

API:er för dokumentgenerering för kommunikation hjälper dig att kombinera en mall (XFA eller PDF) med kunddata (XML) för att generera dokument i PDF och utskriftsformat som PS, PCL, DPL, IPL och ZPL. Dessa API:er använder PDF- och XFA-mallar med [XML-data](communications-known-issues-limitations.md#form-data) för att generera ett enda dokument on demand eller flera dokument med hjälp av ett batchjobb.

Vanligtvis skapar du en mall med [Designer](use-forms-designer.md) och använda API:er för kommunikation för att sammanfoga data med mallen. Programmet kan skicka utdatadokumentet till en nätverksskrivare, en lokal skrivare eller till ett lagringssystem för arkivering. Ett typiskt exempel och anpassade arbetsflöden ser ut så här:

![Arbetsflöde för generering av kommunikationsdokument](assets/communicaions-workflow.png)

Beroende på hur de används kan du även göra dessa dokument tillgängliga för hämtning via din webbplats eller en lagringsserver.

Några exempel på API:er för dokumentgenerering är:

### Skapa PDF-dokument {#create-pdf-documents}

Du kan använda API:erna för dokumentgenerering för att skapa ett PDF-dokument som baseras på en formulärdesign och XML-formulärdata. Utdata är ett icke-interaktivt PDF-dokument. Användarna kan alltså inte ange eller ändra formulärdata. Ett grundläggande arbetsflöde är att sammanfoga XML-formulärdata med en formulärdesign för att skapa ett PDF-dokument. I följande bild visas sammanslagningen av en formulärdesign och XML-formulärdata för att skapa ett PDF-dokument.

![Skapa PDF-dokument](assets/outPutPDF_popup.png)
Bild: Vanligt arbetsflöde för att skapa ett PDF-dokument

### Skapa PostScript-dokument (PS), skrivarkommandodokument (PCL), ZPL-dokument (Zebra Printing Language) {#create-PS-PCL-ZPL-documents}

Du kan använda API:er för dokumentgenerering för att skapa dokument i formaten PostScript (PS), Printer Command Language (PCL) och Zebra Printing Language (ZPL) som baseras på en XDP-formulärdesign eller ett PDF-dokument. Dessa API:er hjälper till att sammanfoga en formulärdesign med formulärdata för att generera ett dokument. Du kan spara dokumentet i en fil och utveckla en anpassad process för att skicka det till en skrivare.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Bearbeta gruppdata för att skapa flera dokument {#processing-batch-data-to-create-multiple-documents}

Du kan använda API:er för dokumentgenerering för att skapa separata dokument för varje post i en XML-batchdatakälla. Du kan generera dokument i både gruppläge och asynkront läge. Du kan konfigurera olika parametrar för konverteringen och sedan starta gruppbearbetningen.

![Skapa PDF-dokument](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## Dokumentmanipulering

API:er för dokumentbearbetning i kommunikation hjälper dig att kombinera, ordna om och validera PDF-dokument. Vanligtvis skapar du en DX och skickar den till dokumenthanterings-API:er för att montera eller ordna om ett dokument. The [DDX-dokument](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) innehåller instruktioner om hur du använder källdokumenten för att skapa en uppsättning med obligatoriska dokument. DDX-referensdokumentationen innehåller detaljerad information om alla åtgärder som stöds. Några exempel på dokumentbearbetning är:

### Sammanställa dokument från PDF

Du kan använda API:erna för dokumentmanipulering för att sammanfoga två eller flera PDF- eller XDP-dokument till ett enda PDF-dokument eller PDF Portfolio. Här är några sätt att sammanställa PDF-dokument:

* Sammanställa ett enkelt PDF-dokument
* Skapa en PDF Portfolio
* Sammanställa krypterade dokument
* Sammanställa dokument med Bates-numrering
* Förenkla och sammanställ dokument

![Sammanställa ett enkelt PDF-dokument från flera PDF-dokument](assets/as_document_assembly.png)
Bild: Sammanställa ett enkelt PDF-dokument från flera PDF-dokument

### Disassemblera PDF-dokument

Du kan använda API:erna för dokumentbearbetning för att demontera ett PDF-dokument. API:erna kan extrahera sidor från källdokumentet eller dela upp ett källdokument baserat på bokmärken. Vanligtvis är den här uppgiften användbar om PDF-dokumentet ursprungligen skapades från många enskilda dokument, till exempel en samling programsatser.

* Hämta sidor från ett källdokument
* Dela upp ett källdokument baserat på bokmärken

![Dela upp ett källdokument baserat på bokmärken i flera dokument](assets/as_intro_pdfsfrombookmarks.png)
Bild: Dela upp ett källdokument baserat på bokmärken i flera dokument

### Konvertera till och validera dokument som följer PDF/A

Du kan använda API:erna för dokumentbearbetning för att konvertera ett PDF-dokument till ett PDF/A-kompatibelt dokument och för att avgöra om ett PDF-dokument är PDF/A-kompatibelt. PDF/A är ett arkiveringsformat som är avsett för långtidsarkivering av dokumentets innehåll. Teckensnitten bäddas in i dokumentet och filen är okomprimerad. Därför är ett PDF/A-dokument vanligtvis större än ett PDF-standarddokument. Ett PDF/A-dokument innehåller inte heller ljud- och videoinnehåll.

<!-- 

## Document utilities

Document utilities synchronous APIs helps you convert documents between PDF and XDP file formats, and query information about a PDF document. For example, you can determine whether a PDF document contains comments or attachments. 

### Retrieve PDF document properties

You can [query a PDF document](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Extraction/) for the following information:

* Is a PDF Document: Check whether the source document is a PDF document.
* Is a fillable form: Check whether the source PDF document is a fillable form.
* Form Type: Retrieve the form type of the document.
* Check for Attachments: Check whether the source PDF document has any attachments.
* Check for Comments: Check whether the source PDF document has any review comments.
* Is a PDF Package: Check whether the document is a PDF package.
* Get the PDF Version: Retrieve the [version of the PDF document](https://en.wikipedia.org/wiki/History_of_PDF).
* Recommended Acrobat Version: Retrieve the required version of Acrobat (Reader) to open the PDF document.
* Is an XFA Document: Check whether the source PDF document is an XFA-based PDF document.
* Is Shell PDF: Check whether the source PDF document is shell PDF. A shell PDF contains only an XFA stream, font and image resources, and one page that is either blank or contains a warning that the document must be opened using Acrobat or Adobe Reader. The shell PDF is used with PDF transformation to optimize delivery of PDFForm transformations only.
* Get the XFA Version: Retrieve the [XFA Version for an XFA-based PDF document](https://en.wikipedia.org/wiki/XFA#XFA_versions).

### Convert PDF Documents into XDP Documents

The [PDF to XDP API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Conversion) converts a PDF document to an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the dictionary. -->

## Dokumentsäkerhet {#doc-assurance}

Tjänsten DocAssurance innehåller API:erna för signatur och kryptering:

### Signatur-API:er

Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument. Eftersom säkerhetsfunktionerna tillämpas på själva dokumentet förblir dokumentet säkert och styrs under hela sin livscykel. Ett dokument förblir säkert även utanför brandväggen när det laddas ned offline och när det skickas tillbaka till organisationen. Du kan utföra följande uppgifter med signatur-API:erna:

* Lägg till ett signaturfält i ett PDF-dokument.
* Signera det angivna signaturfältet i ett PDF-dokument.
* Certifiera ett PDF-dokument

### Krypterings-API:er

Med krypterings-API:erna kan du kryptera och dekryptera dokument. När ett dokument är krypterat blir innehållet oläsligt. En behörig användare kan dekryptera dokumentet för att få åtkomst till innehållet. Om ett PDF-dokument är krypterat med ett lösenord måste användaren ange det öppna lösenordet innan dokumentet kan visas i Adobe Reader eller Adobe Acrobat. Om ett PDF-dokument är krypterat med ett certifikat måste användaren dekryptera PDF-dokumentet med den offentliga nyckel som motsvarar det certifikat (privat nyckel) som användes för att kryptera PDF-dokumentet.

Du kan utföra följande uppgifter med krypterings-API:erna:

* Kryptera ett PDF-dokument med ett lösenord.
* Ta bort lösenordsbaserad kryptering från ett PDF-dokument.
* Hämta den typ av skydd som används för ett PDF-dokument.

Både signatur-API:er och krypterings-API:er [Synkrona API:er](#types-of-communications-apis-types).


## Typer av API:er för kommunikation {#types}

Kommunikationen tillhandahåller HTTP-API:er för on demand- och batchdokumentgenerering:

* **[Synkrona API:er](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** lämpar sig för dokumentgenerering on-demand, låg latens och en post. Dessa API:er lämpar sig bättre för användaråtgärdsbaserade användningsfall. Du kan till exempel skapa ett dokument när en användare har fyllt i ett formulär.

* **[Batch-API:er (asynkrona API:er)](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** är lämpliga för schemalagda, höga genomströmningsscenarier och flera dokumentgenereringsscenarier. Dessa API:er genererar dokument gruppvis. Till exempel telefonräkningar, kontoutdrag och förmånsräkningar som genereras varje månad.

## Onboarding

Kommunikationskapaciteten är tillgänglig som en fristående modul och tilläggsmodul för as a Cloud Service Forms-användare. Du kan kontakta Adobe säljteam eller din Adobe-representant för att begära åtkomst. Adobe aktiverar åtkomst för organisationen och tillhandahåller behörigheter åt den person som utses till administratör i organisationen. Administratören kan ge Forms as a Cloud Service utvecklare (användare) tillgång till organisationens API:er.

Efter introduktionen, för att aktivera kommunikationsfunktioner för din as a Cloud Service Forms-miljö:

1. Logga in på Cloud Manager och öppna din as a Cloud Service AEM Forms-instans.

1. Öppna alternativet Redigera program, gå till fliken Lösningar och tillägg och välj **[!UICONTROL Forms - Communications]** alternativ.

   ![Kommunikation](assets/communications.png)

   Om du redan har aktiverat **[!UICONTROL Forms - Digital Enrollment]** väljer du **[!UICONTROL Forms - Communications Add-On]** alternativ.

   ![Addon](assets/add-on.png)

1. Klicka på **[!UICONTROL Update]**.

1. Kör byggprocessen. När byggprocessen är klar aktiveras API:er för kommunikation för din miljö.

>[!NOTE]
>
> Om du vill aktivera och konfigurera API:er för dokumentbearbetning lägger du till följande regel i [Dispatcher-konfiguration](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service lets you generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on an XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## Se även {#see-also}

* [Kommunikationsbearbetning - Synkrona API:er](/help/forms/aem-forms-cloud-service-communications.md)
* [Kommunikationsbearbetning - batch-API:er](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [AEM Forms as a Cloud Service Architecture for Adaptive Forms and Communication APIs](/help/forms/aem-forms-cloud-service-architecture.md)
