---
title: AEM Forms as a Cloud Service - kommunikation
description: Sammanfoga data automatiskt med XDP- och PDF-mallar eller generera utdata i formaten PCL, ZPL och PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: ed46b0be25dabcea69be29e54000a4eab55e2836
workflow-type: tm+mt
source-wordcount: '2247'
ht-degree: 0%

---


# Använda AEM Forms as a Cloud Service Communications API:er {#frequently-asked-questions}

**Kommunikationsfunktionen är i betaversion.**

Med API:er för kommunikation kan du kombinera XDP-mallar, XDP-baserade PDF-dokument och Acrobat Forms (AcroForm) med XML-data för att generera utskriftsdokument i olika format och skapa program som gör att du kan:

- Generera dokument genom att fylla i mallfiler med XML-data.

- Generera formulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.

- Generera PDF från XFA-PDF.

- Generera PDF-, PostScript-, PCL- och ZPL-dokument genom att sammanfoga flera datauppsättningar med källmallar.

Tänk dig ett scenario där du har en eller flera mallar och flera poster med XML-data för varje mall. Du kan använda API:er för kommunikation för att generera ett utskriftsdokument för varje post. <!-- You can also combine the records into a single document. --> Resultatet är ett icke-interaktivt PDF-dokument. Ett icke-interaktivt PDF-dokument tillåter inte att användare anger data i sina fält.

The [API-referensdokumentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) innehåller detaljerad information om alla API:er, parametrar, autentiseringsmetoder och olika tjänster som tillhandahålls av API:er. API-referensdokumentationen finns också i .yaml-format. Du kan ladda ned .yaml för [Grupp-API:er](assets/batch-api.yaml) eller [non-Batch API.yaml](assets/non-batch-api.yaml) och ladda upp den till postman för att kontrollera API:ernas funktionalitet.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Överför en .yaml-fil för kommunikation till postman för att kontrollera API:ernas funktioner.

>[!NOTE]
>
>Endast medlemmar i gruppen med formuläranvändare har åtkomst till kommunikationsAPI:er.

## Aktivera kommunikation

Så här aktiverar du kommunikation för din as a Cloud Service Forms-miljö:

1. Logga in på Cloud Manager och öppna din as a Cloud Service AEM Forms-instans.

1. Öppna alternativet Redigera program, gå till fliken Lösningar och tillägg och välj **[!UICONTROL Forms - Communications]** alternativ.

   <!-- ![Communications](assets\communications.png)

    If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option.  

    <!-- ![Addon](assets\add-on.png) -->

1. Klicka på **[!UICONTROL Update]**.

1. Kör byggprocessen.

När byggpiplexin är klar aktiveras kommunikations-API:er för din miljö.

## Använda kommunikations-API:er {#workflows}

Vanligtvis skapar du en mall med [Designer](use-forms-designer.md) och använda API:er för kommunikation för att

- Konvertera mallarna till olika format, bland annat PDF, PostScript, ZPL och PCL.
- Sammanfoga XML-formulärdata med en formulärdesign för att generera ett dokument.
- Skapa ett dokument utan att sammanfoga XML-formulärdata i dokumentet. Det primära arbetsflödet sammanfogar emellertid data i dokumentet.

Sedan sparas utdatadokumentet i en fil. Du kan utforma egna arbetsflöden för att skicka filen till en nätverksskrivare, en lokal skrivare eller till ett lagringssystem för arkivering. Ett typiskt exempel och anpassade arbetsflöden ser ut så här:

![Kommunikationsarbetsflöde](assets/communicaions-workflow.png)

### Skapa PDF-dokument {#create-pdf-documents}

Du kan använda _generatePDFOutput_ API för att skapa PDF-dokument som baseras på en formulärdesign och XML-formulärdata. Utdata är ett icke-interaktivt PDF-dokument. Användarna kan alltså inte ange eller ändra formulärdata. Ett grundläggande arbetsflöde är att sammanfoga XML-formulärdata med en formulärdesign för att skapa ett PDF-dokument. Följande bild visar hur du sammanfogar en formulärdesign och XML-formulärdata för att skapa ett PDF-dokument.

![Skapa PDF-dokument](assets/outPutPDF_popup.png)

### Skapa PostScript-dokument (PS), skrivarkommandodokument (PCL), ZPL-dokument (Zebra Printing Language) {#create-PS-PCL-ZPL-documents}

Du kan använda API:er för kommunikation för att skapa dokument i formaten PostScript (PS), Printer Command Language (PCL) och Zebra Printing Language (ZPL) som baseras på en XDP-formulärdesign eller ett PDF-dokument. The _generatePrintedOutput_ API sammanfogar en formulärdesign med formulärdata för att generera ett dokument. Du kan spara dokumentet i en fil och utveckla en anpassad process för att skicka det till en skrivare.

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

- Interaktiva PDF-dokument skapade i Designer (som innehåller XFA-strömmar).

- Acrobat PDF forms

Om du försöker förenkla ett icke-interaktivt PDF-dokument inträffar ett undantag.

### Behåll formulärstatus {#retain-form-state}

Ett interaktivt PDF-dokument innehåller olika element som utgör ett formulär. Dessa element kan innehålla fält (för att acceptera eller visa data), knappar (för att utlösa händelser) och skript (kommandon som utför en viss åtgärd). Om du klickar på en knapp kan det utlösa en händelse som ändrar tillståndet för ett fält. Om du t.ex. väljer ett genusalternativ kan du ändra färgen på ett fält eller formulärets utseende. Detta är ett exempel på en manuell händelse som gör att formulärtillståndet ändras.

När ett sådant interaktivt PDF-dokument förenklas med API:erna för kommunikation behålls inte formulärets status. Ange det booleska värdet för att se till att formulärets status bevaras även efter att formuläret har förenklats _keepFormState_ till True för att spara och behålla formulärets status.

### Överväganden för kommunikations-API:er {#considerations-for-communications-apis}

#### Formulärdata {#form-data}

Kommunikations-API:er accepterar både en formulärdesign som vanligtvis skapas i Designer och XML-formulärdata som indata. Om du vill fylla i ett dokument med data måste det finnas ett XML-element i XML-formulärdata för varje formulärfält som du vill fylla i. XML-elementnamnet måste matcha fältnamnet. Ett XML-element ignoreras om det inte motsvarar ett formulärfält eller om XML-elementnamnet inte matchar fältnamnet. Det är inte nödvändigt att matcha den ordning i vilken XML-elementen visas. Den viktiga faktorn är att XML-elementen anges med motsvarande värden.

Ta följande exempel på låneansökningsformulär:

![Låneansökningsformulär](assets/loanFormData.png)

Om du vill sammanfoga data i den här formulärdesignen skapar du en XML-datakälla som motsvarar formuläret. Följande XML representerar en XML-datakälla som motsvarar exempelformuläret för låneansökan.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    - <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

#### Dokumenttyper som stöds {#supported-document-types}

Du bör använda en XDP-fil som indata för att få fullständig åtkomst till återgivningsfunktionerna i API:erna för kommunikation. I vissa fall kan en PDF-fil användas. Att använda en PDF-fil som indata har dock följande begränsningar:

- Ett PDF-dokument som inte innehåller en XFA-ström kan inte återges som PostScript, PCL eller ZPL. Kommunikations-API:er kan återge PDF-dokument med XFA-strömmar (d.v.s. formulär skapade i Designer) till laser- och etikettformat. Om PDF-dokumentet är signerat, certifierat eller innehåller användarrättigheter (som används med tjänsten AEM Forms Reader Extensions) kan det inte återges i dessa utskriftsformat.

<!-- * Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

#### Email support {#email-support}

For email functionality, you can create a process in AEM Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

#### Utskrivbara områden {#printable-areas}

Den icke utskrivbara standardmarginalen på 0,25 tum är inte exakt för etikettskrivare och varierar från skrivare till skrivare och från etikettstorlek till etikettstorlek. Vi rekommenderar att du behåller marginalen på 0,25 tum eller minskar den. Du bör dock inte öka marginalen som inte går att skriva ut. Annars skrivs inte informationen i det utskrivbara området ut korrekt.

Se alltid till att du använder rätt XDC-fil för skrivaren. Undvik till exempel att välja en XDC-fil för en skrivare med 300 dpi och skicka dokumentet till en skrivare med 200 dpi.

#### Skript {#scripts}

En formulärdesign som används med kommunikations-API:erna kan innehålla skript som körs på servern. Kontrollera att en formulärdesign inte innehåller skript som körs på klienten. Mer information om hur du skapar formulärdesignskript finns i Designer-hjälpen.

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

#### Teckensnittsmappning {#font-mapping}

Om ett teckensnitt är installerat på en klientdator är det tillgängligt i listrutan i Designer. Om teckensnittet inte är installerat måste du ange teckensnittsnamnet manuellt. Alternativet&quot;Ersätt ej tillgängliga teckensnitt permanent&quot; i Designer kan vara inaktiverat. I annat fall skrivs ersättningsteckensnittets namn till XDP-filen när XDP-filen sparas i Designer. Det innebär att det skrivarresidenta teckensnittet inte används.

Om du vill designa ett formulär som använder teckensnitt som finns i skrivaren, väljer du ett teckensnittsnamn i Designer som matchar teckensnitten som finns i skrivaren. En lista med teckensnitt som stöds för PCL eller PostScript finns i motsvarande enhetsprofiler (XDC-filer). Du kan också skapa teckensnittsmappning för att mappa teckensnitt som inte finns installerade på skrivaren till teckensnitt med ett annat teckensnittsnamn. I ett PostScript-scenario kan referenser till teckensnittet Arial® mappas till det skrivarresidenta Helvetica®-teckensnittet.

Det finns två typer av OpenType®-teckensnitt. En typ är ett TrueType OpenType®-teckensnitt som PCL stöder. Den andra är CFF OpenType®. PDF och PostScript-utdata har stöd för inbäddade Type-1-, TrueType- och OpenType®-teckensnitt. PCL-utdata stöder inbäddade TrueType-teckensnitt.

Type-1- och OpenType®-teckensnitt bäddas inte in i PCL-utdata. Innehåll som är formaterat med Type-1- och OpenType®-teckensnitt rastreras och genereras som en bitmappsbild som kan vara stor och långsammare att generera.

Hämtade eller inbäddade teckensnitt ersätts automatiskt när du genererar PostScript-, PCL- eller PDF-utdata. Det innebär att endast den deluppsättning av teckensnittstecknen som krävs för att det genererade dokumentet ska kunna återges korrekt inkluderas i det genererade utdata.

#### Arbeta med enhetsprofilfiler (XDC-fil) {#working-with-xdc-files}

En enhetsprofil (XDC-fil) är en skrivarbeskrivningsfil i XML-format. Den här filen gör det möjligt för kommunikations-API:erna att skriva ut dokument som laserskrivare eller etikettskrivarformat. Kommunikations-API:er använder XDC-filer som innehåller följande:

- hppcl5c.xdc

- hppcl5e.xdc

- ps_plain_level3.xdc

- ps_plain.xdc

- zpl300.xdc

- zpl600.xdc

- zpl300.xdc

- ipl300.xdc

- ipl400.xdc

- tpcl600.xdc

- dpl300.xdc

- dpl406.xdc

- dpl600.xdc

Du behöver inte ändra dessa filer för att skapa dokument. Du kan dock ändra dem så att de passar dina behov.

De här filerna är XDC-exempelfiler som har stöd för funktioner på vissa skrivare, som inbyggda teckensnitt, pappersfack och häftningsenheter. Syftet med dessa exempel är att hjälpa dig att förstå hur du konfigurerar egna skrivare med hjälp av enhetsprofiler. Proverna är också en utgångspunkt för liknande skrivare i samma produktserie.

#### Arbeta med XCI-konfigurationsfilen {#working-with-xci-files}

Kommunikations-API:er använder en XCI-konfigurationsfil för att utföra åtgärder, till exempel kontrollera om utdata är en enskild panel eller sidnumrerad. Även om den här filen innehåller inställningar som kan anges är det normalt inte att ändra det här värdet. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Du kan skicka en ändrad XCI-fil när du använder ett kommunikations-API. När du gör det skapar du en kopia av standardfilen, ändrar bara de värden som behöver ändras för att uppfylla dina affärskrav och använder den ändrade XCI-filen.

Kommunikations-API:er börjar med XCI-standardfilen (eller den ändrade filen). Sedan tillämpas värden som anges med kommunikations-API:erna. Dessa värden åsidosätter XCI-inställningar.

I följande tabell anges XCI-alternativ.

| XCI-alternativ | Beskrivning |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| config/present/pdf/creator | Identifierar den som har skapat dokumentet med hjälp av posten Skapare i dokumentinformationsordlistan. Mer information om det här lexikonet finns i referenshandboken för PDF. |
| config/present/pdf/producer | Identifierar dokumenttillverkaren med hjälp av posten Producer i dokumentinformationsordlistan. Mer information om det här lexikonet finns i referenshandboken för PDF. |
| config/present/layout | Anger om utdata är en enda panel eller sidnumrerad. |
| config/present/pdf/compression/level | Anger den komprimeringsgrad som ska användas när ett PDF-dokument skapas. |
| config/present/pdf/scriptModel | Styr om XFA-specifik information ska inkluderas i utdata-PDF-dokumentet. |
| config/present/common/data/adjustData | Kontrollerar om XFA-programmet justerar data efter sammanslagningen. |
| config/present/pdf/renderPolicy | Kontrollerar om genereringen av sidinnehåll görs på servern eller skjuts upp till klienten. |
| config/present/common/locale | Anger standardspråket som används i utdatadokumentet. |
| config/present/destination | Anger utdataformatet när det finns i ett aktuellt element. Anger vilken åtgärd som ska utföras när dokumentet öppnas i en interaktiv klient när det finns i ett openAction-element. |
| config/present/output/type | Anger vilken typ av komprimering som ska användas för en fil eller vilken typ av utdata som ska skapas. |
| config/present/common/temp/uri | Anger formulär-URI. |
| config/present/common/template/base | Anger en basplats för URI:er i formulärdesignen. När det här elementet saknas eller är tomt används platsen för formulärdesignen som bas. |
| config/present/common/log/to | Styr platsen dit loggdata eller utdata skrivs. |
| config/present/output/to | Styr platsen dit loggdata eller utdata skrivs. |
| config/present/script/currentPage | Anger den inledande sidan när dokumentet öppnas. |
| config/present/script/exclude | Informerar AEM Forms server-/Communications API:er om vilka händelser som ska ignoreras. |
| config/present/pdf/linearized | Anger om utdatadokumentet för PDF är linjärt. |
| config/present/script/runScripts | Styr vilken uppsättning skript AEM Forms kör. |
| config/present/pdf/tagged | Styr om taggar ska tas med i utdatadokumentet för PDF. Taggar i PDF är ytterligare information som ingår i ett dokument för att visa dokumentets logiska struktur. Taggar underlättar hjälpmedelsanvändningen och formateringen. Ett sidnummer kan till exempel taggas som en artefakt så att skärmläsaren inte omsluter den mitt i texten. Även om märkord gör ett dokument mer användbart, ökar de även storleken på dokumentet och bearbetningstiden för att skapa det. |
| config/present/pdf/version | Anger vilken version av PDF-dokument som ska genereras. |

<!-- Using API

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as HTTP endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document. -->
