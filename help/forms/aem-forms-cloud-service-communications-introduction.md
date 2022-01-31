---
title: En introduktion till Forms as a Cloud Service Communications
description: Sammanfoga data automatiskt med XDP- och PDF-mallar eller generera utdata i formaten PCL, ZPL och PostScript
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: dbc0ef92b0b61945ee195971aacab3bc8781b01c
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 2%

---

# Använd AEM Forms as a Cloud Service Communications {#frequently-asked-questions}

**AEM Forms as a Cloud Service Communications-funktionen är i betaversion.**

Med kommunikationsfunktioner kan ni skapa varumärkesorienterade, personaliserade och standardiserade dokument som affärskontakter, kontoutdrag, kravbrev, förmånsmeddelanden, månatliga räkningar eller välkomstpaket.


Du kan generera ett dokument på begäran eller skapa ett batchjobb för att generera flera dokument med definierade intervall. Kommunikations-API:er ger:

* smidiga funktioner för att generera on demand- och batchdokumentation

* HTTP-API:er för enklare integrering med befintliga system. Separata API:er för on demand-åtgärder (låg fördröjning) och batchåtgärder (högdataåtgärder) ingår. Det gör dokumentgenereringen till en effektiv uppgift.

* säker åtkomst till data. Kommunikations-API:er ansluter till och får endast åtkomst till data från kundutsedda datalager, gör inga lokala kopior av data, vilket gör kommunikationen mycket säker.

![Exempel på kreditkortsutdrag](assets/statement.png)
Du kan skapa ett kreditkortsutdrag med API:er för kommunikation. Det här exempelkontoutdraget använder samma mall men separata data för varje kund beroende på hur de använder kreditkortet.

## Hur fungerar det?

Kommunikationen utnyttjar [PDF och XFA-mallar](#supported-document-types) med [XML-data](#form-data) för att generera ett enda dokument on demand eller flera dokument med hjälp av ett batchjobb vid angivet intervall.

Ett kommunikations-API hjälper till att kombinera en mall (XFA eller PDF) med kunddata ([XML-data](#form-data)) för att generera dokument i PDF och utskriftsformat som PS, PCL, DPL, IPL och ZPL.

Vanligtvis skapar du en mall med [Designer](use-forms-designer.md) och använda API:er för kommunikation för att sammanfoga data med mallen. Programmet kan skicka utdatadokumentet till en nätverksskrivare, en lokal skrivare eller till ett lagringssystem för arkivering. Ett typiskt exempel och anpassade arbetsflöden ser ut så här:

![Kommunikationsarbetsflöde](assets/communicaions-workflow.png)

Beroende på hur de används kan du även göra dessa dokument tillgängliga för hämtning via din webbplats eller en lagringsserver.

## Kommunikations-API:er

Kommunikationen tillhandahåller HTTP-API:er för on demand- och batchdokumentgenerering:

* **[Synkrona API:er](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/)** lämpar sig för dokumentgenerering on-demand, låg latens och en post. Dessa API:er lämpar sig bättre för användaråtgärdsbaserade användningsfall. Du kan till exempel skapa ett dokument när en användare har fyllt i ett formulär.

* **[Batch-API:er (asynkrona API:er)](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/batch/)** är lämpliga för schemalagda, höga genomströmningsscenarier och flera dokumentgenereringsscenarier. Dessa API:er genererar dokument gruppvis. Till exempel telefonräkningar, kreditkortsräkningar och förmånsräkningar som genereras varje månad.

Några av de viktigaste användningsområdena för API:er för kommunikation är:

### Skapa PDF-dokument {#create-pdf-documents}

Du kan använda kommunikations-API:er för att skapa ett PDF-dokument som baseras på en formulärdesign och XML-formulärdata. Utdata är ett icke-interaktivt PDF-dokument. Användarna kan alltså inte ange eller ändra formulärdata. Ett grundläggande arbetsflöde är att sammanfoga XML-formulärdata med en formulärdesign för att skapa ett PDF-dokument. Följande bild visar hur du sammanfogar en formulärdesign och XML-formulärdata för att skapa ett PDF-dokument.

![Skapa PDF-dokument](assets/outPutPDF_popup.png)

### Skapa PostScript-dokument (PS), skrivarkommandodokument (PCL), ZPL-dokument (Zebra Printing Language) {#create-PS-PCL-ZPL-documents}

Du kan använda API:er för kommunikation för att skapa dokument i formaten PostScript (PS), Printer Command Language (PCL) och Zebra Printing Language (ZPL) som baseras på en XDP-formulärdesign eller ett PDF-dokument. Dessa API:er hjälper till att sammanfoga en formulärdesign med formulärdata för att generera ett dokument. Du kan spara dokumentet i en fil och utveckla en anpassad process för att skicka det till en skrivare.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Bearbeta gruppdata för att skapa flera dokument {#processing-batch-data-to-create-multiple-documents}

Du kan skapa separata dokument för varje post i en XML-batchdatakälla. Du kan generera dokument i både gruppläge och asynkront läge. Du kan konfigurera olika parametrar för konverteringen och sedan starta gruppbearbetningen. <!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. -->

### Förenkla interaktiva PDF-dokument {#flatten-interactive-pdf-documents}

Du kan använda API:erna för kommunikation för att omvandla ett interaktivt PDF-dokument (till exempel ett formulär) till ett icke-interaktivt PDF-dokument. Med ett interaktivt PDF-dokument kan användare ange eller ändra data som finns i dokumentfälten i PDF. Processen att omforma ett interaktivt PDF-dokument till ett icke-interaktivt PDF-dokument kallas för förenkling. När ett PDF-dokument förenklas kan användaren inte ändra de data som finns i dokumentets fält. Ett skäl till att förenkla ett PDF-dokument är att se till att data inte kan ändras.

Du kan förenkla följande typer av PDF-dokument:

* Interaktiva PDF-dokument skapade i Designer (som innehåller XFA-strömmar).

* Acrobat PDF forms

Om du försöker förenkla ett icke-interaktivt PDF-dokument inträffar ett undantag.

### Behåll formulärstatus {#retain-form-state}

Ett interaktivt PDF-dokument innehåller olika element som utgör ett formulär. Dessa element kan innehålla fält (för att acceptera eller visa data), knappar (för att utlösa händelser) och skript (kommandon som utför en viss åtgärd). Om du klickar på en knapp kan det utlösa en händelse som ändrar tillståndet för ett fält. Om du t.ex. väljer ett genusalternativ kan du ändra färgen på ett fält eller formulärets utseende. Detta är ett exempel på en manuell händelse som gör att formulärtillståndet ändras.

När ett sådant interaktivt PDF-dokument förenklas med API:erna för kommunikation behålls inte formulärets status. Ange det booleska värdet för att se till att formulärets status bevaras även efter att formuläret har förenklats _keepFormState_ till True för att spara och behålla formulärets status.


## Onboarding

Kommunikation finns som fristående modul och tilläggsmodul för as a Cloud Service användare av Forms. Du kan kontakta Adobe säljteam eller din Adobe-representant för att begära åtkomst.

Adobe aktiverar åtkomst för organisationen och tillhandahåller behörigheter åt den person som utses till administratör i organisationen. Administratören kan ge AEM Forms-utvecklare (användare) i organisationen åtkomst till API:erna.

Efter introduktionen, för att aktivera kommunikation för din as a Cloud Service Forms-miljö:

1. Logga in på Cloud Manager och öppna din as a Cloud Service AEM Forms-instans.

1. Öppna alternativet Redigera program, gå till fliken Lösningar och tillägg och välj **[!UICONTROL Forms - Communications]** alternativ.

   ![Kommunikation](assets/communications.png)

   Om du redan har aktiverat **[!UICONTROL Forms - Digital Enrollment]** väljer du **[!UICONTROL Forms - Communications Add-On]** alternativ.

   ![Addon](assets/add-on.png)

1. Klicka på **[!UICONTROL Update]**.

1. Kör byggprocessen.

När byggpiplexin är klar aktiveras kommunikations-API:er för din miljö.


<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service allows you to generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

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

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on a XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.



### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->
