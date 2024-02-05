---
title: Fakturerbara API:er för transaktionsrapporter
description: Lista över alla API:er som räknas som transaktioner
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: a1a87a27d73d7472ec02de37621123bbdd3876b4
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Fakturerbara API:er för transaktionsrapporter {#transaction-reports-billable-apis}

AEM Forms har flera API:er för att skicka formulär, bearbeta dokument och återge dokument. Vissa API:er räknas som transaktioner och andra kan användas. Det här dokumentet innehåller en lista över alla API:er som har redovisats som transaktioner i en transaktionsrapport. Här är några vanliga scenarier där ett fakturerbart API används:

* Skicka ett anpassat formulär
* Konvertera ett dokument från ett format till ett annat
* Förenkla ett dynamiskt PDF-dokument
* Generera ett arkivdokument (med Forms Service eller Output Service)
* Sammanfoga ett interaktivt PDF-dokument med ett annat PDF-dokument
* Tilldela uppgiftssteg och steg i kommunikations-API för AEM arbetsflöden

Fakturerings-API:erna tar inte hänsyn till antalet sidor, längden på ett dokument eller formulär eller det återgivna dokumentets slutliga format. En transaktionsrapport delar upp transaktionerna i två kategorier: Forms Inskickat och Dokument återgivet.

* **Forms:** När data skickas in från någon typ av formulär som skapats med AEM Forms och data skickas till en datalagringsplats eller databas anses det som en formuläröverföring. Att skicka ett anpassat formulär eller en formuläruppsättning betraktas till exempel som att formulär skickas in. Om en formuläruppsättning har fem formulär, och när formuläruppsättningen skickas, räknas den som fem inskickade svar av transaktionsrapporteringstjänsten.

* **Återgivna dokument:** Generering av ett dokument genom att kombinera en mall och data, digitalt signera eller certifiera ett dokument, använda ett fakturerbart dokument-API:er för dokumenttjänster eller konvertering av ett dokument från ett format till ett annat, räknas som dokument som återges.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="Spårare för formuläröverföringar"
>abstract="Spåra enkelt inskickade blanketter i en samlad vy för totalt antal eller fördjupa er i instansspecifik information. Använd det intuitiva stapeldiagrammet för att identifiera trender, jämföra instanser och fatta välgrundade beslut snabbt."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="Spårare för formulärkonverteringar"
>abstract="Håll koll på formulärkonverteringarna smidigt genom en sammanfattning av det totala antalet eller utforska information för varje instans av AEM Forms. Det lättlästa stapeldiagrammet hjälper dig att identifiera trender, jämföra instanser och fatta snabba, välgrundade beslut."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="Genomsnittlig varaktighet för formulärgenerering"
>abstract="Diagrammet visar den genomsnittliga tiden det tar att skapa ett formulär. Varje stapel i diagrammet representerar ett specifikt formulär och stolpens höjd anger den genomsnittliga tid det tar att skapa formuläret under den tidsramen. Genom att analysera det här diagrammet blir det lättare för användarna att förstå hur effektivt och snabbt det är att skapa formulär under olika perioder eller i olika sammanhang, vilket ger insikter om möjliga förbättringar."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="Genomsnittlig varaktighet för att skapa formulär"
>abstract="Diagrammet visar den genomsnittliga tiden det tar att skapa och publicera ett formulär, mätt från den första dagen som formuläret öppnades för redigering. Varje stapel motsvarar en viss tidsram för ett formulär, där stapelhöjden anger den genomsnittliga tiden från början av formulärutvecklingen till dess slutförande och publicering."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="Ny Forms Tracker"
>abstract="Diagrammet innehåller information om antalet eller frekvensen av nyskapade formulär under specifika tidsperioder. Varje stapel i diagrammet representerar en separat måttenhet, till exempel dagar, veckor eller månader. Höjden på varje stapel anger antalet eller frekvensen för nya formulär som skapas under det aktuella intervallet."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="Publicerad Forms Tracker"
>abstract="Diagrammet ger information om antalet eller frekvensen av formulär som har publicerats under specifika tidsperioder. På så sätt kan ni förstå trender, mönster eller variationer i publiceringen av formulär över tiden, vilket underlättar övervakning av produktivitet, identifiering av perioder med hög publiceringstid eller utvärdering av hur väl ändringarna i publiceringsprocessen har lyckats."

<!-- 
>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Form Fragments Tracker"
>abstract="This graph helps you see how many form fragments people use in their forms. It gives you a sense of how popular or common these reusable parts are in form building."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Average Duration for Form Fragments Creation"
>abstract= "The graph displays the average time taken to create a form fragment, measured from the initial day the form fragment was opened for editing. Each bar corresponds to a specific time frame for a form fragment, with the bar height indicating the average time taken from the start of form fragment development to its finalization and publication."


<!-- 

>[!NOTE]
>
>Transaction Reports UI displays three categories: Forms Submitted, Documents Rendered, and Documents Processed. Both Documents Rendered and Documents Processed are accounted as Documents Rendered.
-->


<!--

## Billable Document Services APIs {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## Fakturerbara API:er för dokumenttjänster {#billable-document-services-apis}

### Generera tjänsten PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Beskrivning</td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#section/Before-you-start" target="_blank">createPDF</a></td>
   <td>Skapar ett PDF-dokument från en mall och sammanfogar data till den.</td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>Konverterar XDP-fil eller PDF-dokument till filtyper som stöds.</td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

### Output Service {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Beskrivning</td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutput" target="_blank">generatePDFOutput</a></td>
   <td>Sammanfogar data och mallar för att skapa ett PDF-dokument.</td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput (PDFOutputOptions)</a></td>
   <td>Sammanfogar data och mallar för att skapa ett PDF-dokument.</td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>Sammanfogar data och mallar för att skapa en uppsättning PDF-dokument.</td>
   <td>Bearbetade dokument</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>Konverterar XDP- och PDF-dokument till filformaten PostScript (PS), Printer Command Language (PCL) och ZPL. </td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput (PrintedOutputOptions)</a></td>
   <td>Konverterar XDP- och PDF-dokument till filformaten PostScript (PS), Printer Command Language (PCL) och ZPL. </td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Konverterar en uppsättning XDP- och PDF-dokument till en uppsättning PostScript- (PS), Printer Command Language (PCL) och ZPL-filformat. </td>
   <td>Bearbetade dokument</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
 </tbody>
</table>

### DocAssurance-tjänst {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Beskrivning</td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/docassurance/#tag/DocAssurance" target="_blank">secureDocument</a><br /> </td>
   <td>Med detta API kan du skydda ditt dokument. Du kan använda API:t för att signera, certifiera, utöka eller kryptera ett PDF-dokument.</td>
   <td>Bearbetade dokument</td>
   <td>Endast signerings- och certifieringsåtgärden för secureDocument faktureras.</td>
  </tr>
 </tbody>
</table>

### Tjänsten Document of Record (DOR) {#document-of-record-dor-forms-service-and-output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Beskrivning</td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td><a href="https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Generate-DoR/operation/generateDoR" target="_blank">återge</a></td>
   <td>Anropar den angivna återgivningsmetoden för att generera ett postdokument med angivna parametrar.</td>
   <td>Dokument som behandlas med Forms Service</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed using Output Service</td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

<!--

### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converts a Flat PDF file to PostScript format using the options specified in the option spec.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Decodes all the barcodes in a Document object and returns an org.w3c.dom.Document object that contains data that was retrieved from the barcode.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

### Assembler Service {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Beskrivning</td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX">invoke</a></td>
   <td>Kör DDX på de angivna indatadokumenten och returnerar ett objekt som innehåller resultatdokumenten</td>
   <td>Bearbetade dokument</td>
   <td>Följande operationer redovisas inte som transaktioner:
    <ul>
     <li>Skapa paket eller portfölj</li>
     <li>Välja ut flera XDP-filer </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">invoke</a></td>
   <td>Kör DDX på de angivna indatadokumenten och returnerar ett objekt som innehåller resultatdokumenten</td>
   <td>Bearbetade dokument</td>
   <td>Alla indatafilformat som stöds av PDF Generator-, Forms- och Output-tjänsterna har stöd för alla dessa format som utdatafilformat. </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA">toPDFA</a></td>
   <td>Konvertera ett angivet dokument till PDF/A med de angivna alternativen.</td>
   <td>Bearbetade dokument</td>
   <td> </td>
  </tr>
 </tbody>
</table>

API:ts användning räknas som en transaktion när du utför en eller flera av följande åtgärder:

1. Konvertering från andra format än PDF till PDF. <!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Konvertering från PDF till PDF/A-format.
1. Konvertering från PDF till andra format än PDF. Exempel omfattar omformningen från PDF till bildformat eller konverteringen från PDF till textformat.


>[!NOTE]
>
>* Anrop-API:t för sammansättartjänsten kan internt anropa ett fakturerbart API för en annan tjänst beroende på indata. Detta innebär att invoke-API:t kan redovisas som inga, enskilda eller flera transaktioner. Antalet transaktioner som räknas beror på indata och de interna API:erna som anropas.
>* Ett enda PDF-dokument som skapats med en monteringsfunktion kan redovisas som inga, enstaka eller flera transaktioner. Antalet transaktioner som räknas beror på den angivna koden.
>

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## Fakturerbara API:er för datainhämtning {#billable-data-capture-apis}

Alla överföringshändelser för adaptiva formulär redovisas som transaktioner. Som standard räknas inte inlämning av ett PDF-formulär som en transaktion. Använd den angivna [API för transaktionsregistrering](record-transaction-custom-implementation.md) för att registrera en PDF forms som en transaktion.

### Adaptiv Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Användningsfall</p> </td>
   <td>Beskrivning</td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td>Skicka ett anpassat formulär</td>
   <td>Skickar ett anpassat formulär till den konfigurerade skicka-åtgärden. </td>
   <td>Forms har skickats</td>
   <td>
    <ul>
     <li>Konto för slutförda överföringar för en eller två transaktioner. Antalet transaktioner som räknas beror på vilken typ av överföringsåtgärd som används för att skicka in. Du kan till exempel skicka PDF via e-poståtgärdskonton för att skicka två antal transaktioner. En transaktion för att skicka formulär och en annan för PDF som genereras med tjänsten Document of Record (DOR). </li>
     <li>När du använder det adaptiva formuläret i ett adaptivt formulär (adaptiv formuläruppsättning) utförs endast en transaktion. Du kan ha ett obegränsat antal anpassningsbara formulär i ett anpassat formulär.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

<!--

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Form set {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting a form set</td>
   <td>Submits form set to the submit URL configured in the form set.</td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
     <li>Every form in an HTML5 Forms form set accounts as a separate transaction. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

## Fakturerbara formulärbaserade AEM {#billable--form-centric-aem-workflows}

Tilldela uppgifter och dokumenttjänster steg i formulärbaserade AEM-arbetsflöden redovisas som transaktioner. Om ett arbetsflödessteg redovisar en transaktion och arbetsflödet inte kan slutföras, återförs inte antalet transaktioner.

<!--
Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.
-->


<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### Formulärbaserade AEM {#form-centric-aem-workflows}

<table>
 <tbody>
  <tr>
   <td><p>Använd skiftläge</p> </td>
   <td>Kategori för transaktionsrapport</td>
   <td>Ytterligare information</td>
  </tr>
  <tr>
   <td>Skicka ett steg för Tilldela uppgift</td>
   <td>Forms har skickats</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Skicka en startpunkt för ett arbetsflödesprogram </td>
   <td>Forms har skickats</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrera fakturerbara API:er som transaktioner för anpassad kod {#recording-billable-apis-as-transactions-for-custom-code}

Åtgärder som att skicka ett PDF-formulär, använda agentanvändargränssnittet för att förhandsgranska interaktiv kommunikation, skicka formulär som inte är standard och anpassade implementeringar räknas inte som transaktioner. AEM Forms tillhandahåller ett API för att spela in sådana åtgärder som transaktioner. Du kan anropa API:t från dina anpassade implementeringar till [spela in en transaktion](/help/forms/record-transaction-custom-implementation.md).

## Relaterade artiklar {#related-articles}

* [Registrera en transaktion för anpassade implementeringar](/help/forms/record-transaction-custom-implementation.md)
