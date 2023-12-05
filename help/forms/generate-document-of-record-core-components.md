---
title: Hur skapar man urkunder för Adaptive Forms?
description: Lär dig att generera en mall för ett dokument för inspelning (Document of Record, DoR) för adaptiva Forms Core-komponenter.
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3006'
ht-degree: 0%

---

# Generera urkunder för adaptiva Forms (kärnkomponenter)

## Ökning {#overview}

När ett formulär fylls i eller skickas kan du spara en post med formuläret, i utskrift eller i dokumentformat. Den här posten kallas dokumentarkivhandling (DoR). Det är en utskriftsvänlig kopia av det inskickade formuläret. Du kan också hänvisa till urkunder för den information de fyller i vid ett senare tillfälle eller använda arkiveringsdokumentet för att arkivera formulär och innehåll tillsammans i PDF-format.

![Dokument för registrering](assets/document-of-record.png)

Om du vill skapa ett dokument med poster sammanfogas en XFA- eller Acrobat-baserad mall med data som samlats in via ett adaptivt formulär. Du kan generera ett dokument för inspelning automatiskt eller on-demand. Med alternativet on-demand kan du ange en anpassad XFA- eller Acrobat-baserad mall som ger ett anpassat utseende till ditt postdokument.

Du kan:

* [Generera ett XFA-baserat arkivdokument](#generate-an-XFA-based-document-of-record)
* [Generera ett Acrobat-baserat (Acrobat Form PDF) arkivdokument](#generate-an-Acroform-based-document-of-record)
* [Generera ett postdokument automatiskt](#auto-generate-a-document-of-record)

## Innan du börjar {#components-to-automatically-generate-a-document-of-record}

Innan du börjar lära dig mer och förbereder de resurser som krävs för ett dokument:

**Basmall:** En XFA-mall (XDP-fil) som skapats i Forms Designer eller ett Acrobat-formulär (AcroForm). [Basmall](#base-template-of-a-document-of-record) används för att ange formaterings- och varumärkesinformation för ett arkivdokument. Överför din XFA-mall (XDP-fil) till din AEM Forms-instans tidigare.

**Adaptiv form:** Ett anpassat formulär som postdokumentet ska skapas för.

## Generera ett XFA-baserat arkivdokument {#generate-an-XFA-based-document-of-record}

Överför din XFA-mall (XDP-fil) till din AEM Forms-instans. Utför följande steg för att konfigurera ett adaptivt formulär så att XFA-mallen (XDP-filen) används som mall för postdokument:

1. I författarinstansen av Experience Manager klickar du på **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents].**
1. Välj ett formulär eller Skapa ett anpassat formulär och klicka på **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Form Model]**.
1. På  **[!UICONTROL Form Model]** -fliken, i **[!UICONTROL Select From]** nedrullningsbar meny, välja **[!UICONTROL Form Data Model]**, **[!UICONTROL Schema]** eller **[!UICONTROL None]**. Du kan också välja en formulärmodell när du skapar ett formulär.
1. I avsnittet Dokumentmall på fliken Formulärmodell väljer du **Associera formulärmall som postdokumentmall**. När du väljer det här alternativet visas alla XFA-mallar (XDP-filer) som är tillgängliga på datorn. Välj lämplig fil. Se även till att samma schema (dataschema) används för Adaptivt formulär och vald XFA-mall (XDP-fil).
1. Klicka **[!UICONTROL Done.]**

Ditt adaptiva formulär är nu konfigurerat att använda en XDP-fil som mall för postdokument. Nästa steg är att [binda adaptiva formulärkomponenter till motsvarande mallfält](#bind-adaptive-form-components-with-template-fields).

## Generera ett Acrobat-baserat arkivdokument {#generate-an-Acroform-based-document-of-record}

Överför Adobe Acrobat PDF (Acrobat) till din AEM Forms-instans. Utför följande steg för att konfigurera ett adaptivt formulär så att det använder Adobe Acrobat PDF (Acrobat) som mall för arkivdokument:

1. I författarinstansen av Experience Manager klickar du på **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents].**
1. Välj ett formulär eller **[!UICONTROL Create an Adaptive Form]** och klicka **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Form Model]**.
1. På  **[!UICONTROL Form Model]** -fliken, i **[!UICONTROL Select From]** nedrullningsbar meny, välja **[!UICONTROL Form Data Model]**, **[!UICONTROL Schema]** eller **[!UICONTROL None]**. Du kan också välja en formulärmodell när du skapar ett formulär.
1. I avsnittet Dokumentmall på fliken Formulärmodell väljer du **Associera formulärmall som postdokumentmall**. När du väljer det här alternativet visas alla Acrobat-PDF (Acrobat) som är tillgängliga på datorn. Markera den Acrobat som du vill använda.
1. Klicka **[!UICONTROL Done.]**

Ditt adaptiva formulär är nu konfigurerat att använda en Acrobat som mall för arkivdokument. Nästa steg är att [binda adaptiva formulärkomponenter till motsvarande mallfält](#bind-adaptive-form-components-with-template-fields).

## Generera ett arkivdokument automatiskt {#auto-generate-a-document-of-record}

När ett anpassat formulär konfigureras för att automatiskt generera ett dokument för registrering uppdateras dess dokument omedelbart varje gång ett formulär ändras. Om ett fält till exempel tas bort från ett befintligt anpassat formulär, tas motsvarande fält också bort och visas inte i postdokumentet. Det finns många andra fördelar med att automatiskt generera arkivdokument:

* Formulärutvecklare behöver inte hantera databindningar manuellt. Automatiskt genererat arkivdokument tar hand om databindningsrelaterade uppdateringar.
* Formulärutvecklare behöver inte manuellt dölja fält som är markerade som exkluderade från postdokumentet. Automatiskt genererat postdokument är förkonfigurerat för att exkludera sådana fält.
* Med det automatiskt genererade alternativet Dokument i post sparar du tid som krävs för att skapa en formulärmall för Dokument i post.
* Med det automatiskt genererade alternativet Dokument för post kan du använda olika format och utseenden med olika basmallar. Det hjälper er att välja det bästa formatet och utseendet för arkivdokument för er organisation. Om du inte anger någon formatering anges systemformaten som standard.
* Automatiskt genererat arkivdokument säkerställer att alla ändringar i formuläret omedelbart återspeglas i arkivdokumentet.

Så här konfigurerar du ett anpassat formulär så att det automatiskt genererar ett postdokument:

1. I författarinstansen av Experience Manager klickar du på **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents].**
1. Välj ett formulär eller Skapa ett anpassat formulär och klicka på **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Form Model]**.
1. På  **[!UICONTROL Form Model]** -fliken, i **[!UICONTROL Select From]** nedrullningsbar meny, välja **[!UICONTROL Form Data Model]**, **[!UICONTROL Schema]** eller **[!UICONTROL None]**. Du kan också välja en formulärmodell när du skapar ett formulär.
1. I avsnittet Dokumentmall på fliken Formulärmodell väljer du **Generera postdokument**.
1. Klicka **[!UICONTROL Done.]**

## Bind adaptiva formulärkomponenter till mallfält {#bind-adaptive-form-components-with-template-fields}

Bind adaptiva formulärfält med mallfält för att visa hämtade formulärdata i motsvarande dokumentationsfält. Så här binder du adaptiva formulärkomponenter till motsvarande dokument i postmallsfält:

1. Öppna det adaptiva formuläret, som är konfigurerat att använda en anpassad formulärmall för redigering.

1. Markera en adaptiv formulärkomponent och klicka på Konfigurera ![Konfigurera](assets/Smock_Wrench_18_N.svg) -ikon. Egenskapsläsaren öppnas.

1. Bläddra och markera ett fält i egenskapswebbläsaren.

   * (För AcroForm-mall) **[!UICONTROL Document of Record Bind Reference field]** -egenskap.
   * (För XFA-mall) **[!UICONTROL Data Model Bind Reference]** -egenskap.

1. Klicka på **[!UICONTROL Save]**.

<!-- 
In the following video, Adaptive Form components are bound with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

Du kan använda skicka-åtgärder som&quot;Skicka e-post&quot;,&quot;Anropa ett AEM&quot;,&quot;Anropa ett Power Automate-flöde&quot; och andra [Skicka funktionsmakron](configuring-submit-actions.md) för att få ett dokument.
![Bildöverföringsåtgärder](/help/forms/assets/submit-actions-img.png)



## Inkrementella uppdateringar av dokumentmallen {#document-of-record-template-incremental-updates}

Anpassningsbara formulär och motsvarande dokument med postmallar kan utvecklas under en längre tid. Du kan välja att lägga till, ta bort eller ändra fält i ett adaptivt formulär eller en dokumentmall.

När du ändrar en dokumentmall och överför den ändrade dokumentmallen till AEM Forms, identifierar den adaptiva Forms-redigeraren automatiskt de ändrade bindningarna och informerar dig om adaptiva formulärkomponenter som kräver nya bindningar. Du kan göra inkrementella uppdateringar i en dokumentmall.

Exempel: en organisation *Vi.butik* har en AcroForm-baserad dokumentmall, *we-retail-invoice.pdf*. Mallen ser ut så här:

![Ursprunglig mall](assets/we-retail-invoice.png)

Efter att ha använt mallen ett tag bestämmer sig organisationen för att byta namn `invoice-number` fält till `bill-number` fält och e-postadress för inhämtning av köpare. En utvecklare uppdaterar namnet på `invoice-number` och lägger till ett e-postfält i mallen. Han skapar också en ny version av mallen som kallas  *we-retail-invoice-v2.pdf*.

![Uppdaterad mall](assets/we-retail-new-invoice.png)

<!--

The developer uploads and applies to the updated template to the adaptive form. The adaptive form automatically detects and displays list of fields where binding has changed.

![Binding Error](assets/we-retail-binding-error.png)

The form developer binds Adaptive Forms fields with corresponding Document of Record template.

-->

>[!VIDEO](assets/we-retail-binding.mp4)

När det adaptiva formuläret skickas genereras nu ett uppdaterat arkivdokument.

![Uppdaterad](assets/we-retail-new-invoice-sent-to-customer.png)

## Viktiga saker att tänka på när du arbetar med postdokumentet {#key-considerations-when-working-with-document-of-record}

Tänk på följande när du arbetar med arkivdokumentet för Adaptiv Forms.

* Dokumentmallar stöder inte RTF-text. Därför visas all RTF-text i det statiska adaptiva formuläret eller i den information som användaren fyller i som oformaterad text i postdokumentet.
* Dokumentfragment i ett anpassat formulär visas inte i postdokumentet. Adaptiva formulärfragment stöds dock.
* Det finns inte stöd för innehållsbindning i det postdokument som genererats för XML-schemabaserade adaptiva formulär.
* Lokaliserad version av Document of Record skapas vid behov för en språkinställning när användaren begär återgivningen av Document of Record. Lokalisering av arkivdokument sker tillsammans med lokalisering av adaptiv form. <!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!-- ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration). -->

## Mappning av adaptiva formulärelement {#mapping-of-adaptive-form-elements}

I följande tabell beskrivs adaptiva formulärkomponenter och motsvarande XFA-komponenter, och om de visas i ett dokument med poster.

### Fält {#fields}

<table>
 <tbody>
  <tr>
   <th>Adaptiv Form-komponent</th>
   <th>Motsvarande XFA-komponent</th>
   <th>Ingår som standard i dokumentpostmall?</th>
   <th>Anteckningar</th>
  </tr>
  <tr>
   <td>Knapp</td>
   <td>Knapp</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Kryssruta</td>
   <td>Kryssruta</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Datumväljaren</td>
   <td>Datum-/tidsfält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nedrullningsbar lista</td>
   <td>Listruta</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Numerisk ruta</td>
   <td>Numeriskt fält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Alternativknapp</td>
   <td>Alternativknapp</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Textruta</td>
   <td>Textfält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Knappen Återställ</td>
   <td>Återställ knapp</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skicka-knapp</td>
   <td><p>E-postknapp</p> <p>HTTP-sändningsknapp</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Bifogad fil</td>
   <td> </td>
   <td>false</td>
   <td>Inte tillgängligt i dokumentmallen. Endast tillgängligt i arkivdokument via bifogade filer.</td>
  </tr>
 </tbody>
</table>

### Behållare {#containers}

<table>
 <tbody>
  <tr>
   <th>Adaptiv Form-komponent</th>
   <th>Motsvarande XFA-komponent</th>
   <th>Anteckningar</th>
  </tr>
  <tr>
   <td>Panel<br /> </td>
   <td>Delformulär<br /> </td>
   <td>Upprepningsbara panelmappar till repeterbara delformulär.</td>
  </tr>
 </tbody>
</table>

### Statiska komponenter {#static-components}

| Adaptiv Form-komponent | Motsvarande XFA-komponent | Anteckningar |
|---|---|---|
| Bild | Bild | Komponenterna TextDraw och Image, oavsett om de är bundna eller obundna, visas alltid i registreringsdokumentet för ett XSD-baserat anpassat formulär, såvida de inte utelämnas med inställningarna för postdokument. |
| Text | Text |

### Tabeller {#tables}

Tabellkomponenterna i Adaptiv Forms, t.ex. sidhuvud, sidfot och radmappning, till motsvarande XFA-komponenter. Du kan mappa repeterbara paneler till tabeller i Dokumentdokument.

## Basmall för ett postdokument {#base-template-of-a-document-of-record}

Basmallen innehåller formaterings- och utseendeinformation för arkivhandlingar. Du kan anpassa standardutseendet för automatiskt genererade dokument för post. Du kan t.ex. använda en basmall för att lägga till företagets logotyp i sidhuvudet och copyrightinformationen i sidfoten i dokumentfönstret.

Mallsidan från en basmall används som mallsida för dokumentmallen. Huvudsidan kan innehålla information som sidhuvud, sidfot och sidnummer som du kan använda i postdokumentet. Du kan använda den här informationen på postdokumentet med hjälp av basmallen för automatisk generering av postdokumentet. Om du använder en basmall kan du ändra standardegenskaperna för fält.

Följ alltid [Grundmallskonventioner](#base-template-conventions) när du utformar en basmall.

## Grundmallskonventioner {#base-template-conventions}

En basmall används för att definiera sidhuvud, sidfot, format och utseende för ett dokument för post. Sidhuvudet och sidfoten kan innehålla information som företagets logotyp och copyrighttext. Den första mallsidan i basmallen kopieras och används som mallsida för postdokumentet, som innehåller ett sidhuvud, en sidfot, ett sidnummer eller annan information som ska visas på alla sidor i postdokumentet. Om du använder en basmall som inte överensstämmer med basmallskonventionerna, används den första mallsidan från basmallen fortfarande i dokumentmallen. Vi rekommenderar att du utformar din basmall enligt dess konventioner och använder den för automatisk generering av dokumentdokument.

**Konventioner för mallsidor**

* I basmallen ger du rotdelformuläret namnet `AF_METATEMPLATE` och mallsidan som `AF_MASTERPAGE`.

* Mallsidan med namnet `AF_MASTERPAGE` som finns under `AF_METATEMPLATE` rotdelformulär är att föredra när du vill extrahera sidhuvud, sidfot och formatinformation.

* If `AF_MASTERPAGE` saknas används den första mallsidan i basmallen.

**Formatkonventioner för fält**

* Om du vill använda format på fälten i postdokumentet innehåller basmallen fält som finns i `AF_FIELDSSUBFORM` under `AF_METATEMPLATE` rotdelformulär.

* Egenskaperna för dessa fält används för fälten i postdokumentet. Dessa fält ska följa `AF_<name of field in all caps>_XFO` namnkonvention. Fältnamnet för kryssrutan bör till exempel vara `AF_CHECKBOX_XFO`.

Så här skapar du en basmall i Forms Designer.

1. Klicka **[!UICONTROL File]** > **[!UICONTROL New]**.
1. Välj **[!UICONTROL Based on a template]** alternativ.

1. Välj **[!UICONTROL Forms - Document of Record]** kategori.
1. Välj **[!UICONTROL DoR Base Template]**.
1. Klicka **[!UICONTROL Next]** och tillhandahålla den information som krävs.

1. (Valfritt) Ändra format och utseende på fält som du vill använda i fälten i postdokumentet.
1. Spara formuläret.
   ![Grundläggande egenskaper](/help/forms/assets/form-designer-dor-img.png)

Du kan nu använda det sparade formuläret som en basmall för ett postdokument. Ändra eller ta inte bort några skript i basmallen.

**Ändra basmall**

* Använd ingen formatering över fält i basmallen. Du bör ta bort dessa fält från basmallen så att eventuella uppgraderingar av basmallen automatiskt hämtas.
* När du ändrar basmallen ska du inte ta bort, lägga till eller ändra skript.

Följ noga de konventioner och instruktioner som nämns ovan för att utforma en basmall.

## Anpassa varumärkesinformationen i arkivdokumentet {#customize-the-branding-information-in-document-of-record}

När du genererar ett dokument för registrering kan du ändra profileringsinformationen för postdokumentet på fliken Dokument för post. Fliken Dokument för post innehåller alternativ som logotyp, utseende, layout, sidhuvud och sidfot, ansvarsfriskrivning och huruvida du vill ta med omarkerade kryssrutor och alternativknappar eller inte.

Om du vill lokalisera den varumärkesinformation som du anger på fliken Dokument av post kontrollerar du att webbläsarens språkområde är korrekt inställt. Så här anpassar du profileringsinformationen i Document of Record:

1. Markera en panel (rotpanelen) i postdokumentet och välj sedan ![konfigurera](assets/configure.png).
1. Välj ![dortab](assets/dortab.png). Fliken Dokument för post visas.
1. Välj antingen standardmallen eller en anpassad mall för återgivning av postdokumentet. Om du väljer standardmallen visas en miniatyrförhandsvisning av postdokumentet under listrutan Mall.
1. Beroende på om du väljer en standardmall eller en anpassad mall visas några av följande egenskaper, eller alla egenskaper, på fliken Dokument för post. Ange nedanstående egenskaper för att definiera utseendet på postdokumentet:

   1. **Grundläggande egenskaper**:
      * **Mall**: Om du vill välja en anpassad mall bläddrar du och väljer en XDP-fil på din [!DNL AEM Forms] server. Om du vill använda en mall som inte är tillgänglig på din [!DNL AEM Forms] ska du först överföra XDP-filen till din [!DNL AEM Forms] server.
      * **Dekorfärg**: Den färg i vilken rubriktext och avgränsningslinjer återges i postdokumentet PDF.
      * **Font Family**: Teckensnittsfamilj för texten i PDF på dokumentationssidan.

      * **Inkludera formulärobjekt som inte är bundna till datamodell**: Att ställa in egenskapen inkluderar obundna fält från schemabaserade adaptiva formulär i postdokumentet.

      <!-- **Exclude hidden fields from the Document of Record**: Setting the property identifies the hidden fields for exclusion from Document of Record.-->

      * **Dölj beskrivning av paneler**: Om du anger egenskapen utesluts beskrivningen av panelen/tabellen från postdokumentet. Gäller för panel och tabell.



   1. **Egenskaper för formulärfält**:
      * **Visa endast de valda värdena för komponenterna Kryssruta och Alternativknapp**: Om du ställer in egenskapen visas endast markerade värden för kryssrutor och alternativknappar i [!UICONTROL Document of Record].
      * **Avgränsare för flera värden**: Du kan välja valfri avgränsare, t.ex. komma eller radbrytning, om du vill visa flera värden.
      * **Justering**: Du kan välja önskad justering (Vågrät, Lodrät, Samma som adaptiv form) för att ange justeringen för fält som kryssruta eller alternativknapp som ska visas på [!UICONTROL Document of Record]. Som standard är den lodräta justeringen inställd för fälten i [!UICONTROL Document of Record]. Ställa in egenskaperna från [!UICONTROL Form Field Properties] av DoR skriver över egenskaperna som anges i [!UICONTROL Item Alignment] för fälten i ett adaptivt formulär. Om du vill välja [!UICONTROL Same as Aaptive form] -alternativet används justeringen som den har konfigurerats i en instans av adaptiv formulärförfattare för [!UICONTROL Document of Record] fält.
      * **Antal alternativ för vågrät justering**:Du kan ange hur många alternativ som ska visas i postdokumentet för den vågräta justeringen.



   1. **Egenskaper för mallsida**:
      * **Logotypbild**: Du kan antingen välja att använda logotypbilden från det adaptiva formuläret, välja en från DAM eller överföra en från datorn.
      * **Formulärtitel**: Titel på DoR.
      * **Sidhuvudstext**: Text som visas i rubrikavsnittet i postdokumentet.
      * **Ansvarsfriskrivning**: Ansvarsfriskrivning.
      * **Ansvarsfriskrivning**: Text som anger omfattningen av rättigheter och skyldigheter i registreringsdokumentet.
      * **Ansvarsfriskrivning**: Ansvarsfriskrivning.

      ![Egenskaper för mallsida](/help/forms/assets/dorpropertiesimg.png)

   >[!NOTE]
   >
   >Om du använder en mall för adaptiva formulär som skapats med en tidigare version av Designer än 6.3, för att egenskaperna för dekorfärg och teckensnittsfamilj ska fungera, kontrollerar du att följande finns i mallen för adaptiva formulär under rotdelformuläret:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Om du vill spara varumärkeskonfigurationen väljer du **[!UICONTROL Done]**.



## Tabell- och kolumnlayouter för paneler i dokumentformat {#table-and-column-layouts-for-panels-in-document-of-record}

Det anpassade formuläret kan vara långt och innehålla flera formulärfält. Du kanske inte vill spara ett postdokument som en exakt kopia av det anpassade formuläret. Nu kan du välja en tabell- eller kolumnlayout för att spara en eller flera adaptiva formulärpaneler på PDF i Dokumentformat.

Innan du genererar ett postdokument väljer du Layout för postdokumentet för den panelen som Tabell eller Kolumn i inställningarna för en panel. Fälten i panelen ordnas därefter i postdokumentet.

![Fält i en panel återges i en tabellayout i postdokumentet](assets/dortablelayout.png)

Fält i en panel återges i en tabellayout i postdokumentet

![Fält i en panel återges i en kolumnlayout i postdokumentet](assets/dorcolumnlayout.png)

Fält i en panel återges i en kolumnlayout i postdokumentet

## Dokumentinställningar {#document-of-record-settings}

Med dokumentinställningar kan du välja vilka alternativ du vill inkludera i postdokumentet. En bank godkänner till exempel namn, ålder, personnummer och telefonnummer i ett formulär. Formuläret genererar ett bankkontonummer och filialinformation. Du kan välja att bara visa namn, personnummer, bankkonto och filialinformation i registreringsdokumentet.

Inställningen för dokumentkomponenten är tillgänglig under dess egenskaper. Om du vill komma åt egenskaperna för en komponent markerar du komponenten och klickar på ![cmppr](assets/cmppr.png) i övertäckningen. Egenskaperna listas i sidlisten och du hittar följande inställningar i den.

**Fältnivåinställningar**

* **Exkludera från postdokument**: Om egenskapen true anges exkluderas fältet från postdokumentet. Det här är en skriptbar egenskap med namnet `excludeFromDoR`. Dess beteende beror på **Uteslut fält från DoR om de är dolda** formulärnivåegenskap.

* **Visa panelen som tabell:** Om du ställer in egenskapen visas panelen som tabell i Postdokument om panelen innehåller färre än 6 fält. Gäller endast för panelen.
* **Exkludera rubrik från arkivdokument:** Om du anger egenskapen utesluts panelens/tabellens namn från Postdokument. Gäller endast för panel och tabell.
* **Exkludera beskrivning från postdokument:** Om du ställer in egenskapen utesluts beskrivningen av panelen/tabellen från Postdokument. Gäller endast för panel och tabell.

**Inställningar för formulärnivå**

* **Inkludera obundna fält i DoR:** När du anger egenskapen inkluderas obundna fält från schemabaserade adaptiva formulär i postdokumentet. Som standard är det sant.

## Se även {#see-also}

{{see-also}}


<!-- 

**Exclude fields from DoR if hidden:** Set the property to exclude the hidden fields from Document of Record at form submission. When you enable [Revalidate on server](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), the server recomputes the hidden fields before excluding those fields from the Document of Record.

!->>
