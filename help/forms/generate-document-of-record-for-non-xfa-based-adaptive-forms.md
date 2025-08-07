---
title: Hur skapar man ett urkunder för AEM Forms?
description: Lär dig att generera en mall för ett dokument för inspelning (DoR) för Adaptiv Forms.
feature: Adaptive Forms, Foundation Components
exl-id: 16d07932-3308-4b62-8fa4-88c4e42ca7b6
role: User, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 0%

---

# Generera arkivdokument för adaptiv Forms

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) |
| AEM as a Cloud Service | Den här artikeln |

## Ökning {#overview}

När ett formulär fylls i eller skickas kan du spara en post med formuläret, i utskrift eller i dokumentformat. Den här posten kallas dokumentarkivhandling (DoR). Det är en utskriftsvänlig kopia av det inskickade formuläret. Du kan också hänvisa till urkunder för den information de fyller i vid ett senare tillfälle eller använda arkiveringsdokumentet för att arkivera formulär och innehåll tillsammans i PDF-format.

![Postdokument](assets/document-of-record.png)

Om du vill skapa ett dokument med poster sammanfogas en XFA- eller Acrobat-baserad mall med data som samlats in via ett adaptivt formulär. Du kan generera ett dokument för inspelning automatiskt eller on-demand.
Med alternativet on-demand kan du ange en anpassad XFA- eller Acrobat-baserad mall som ger ett anpassat utseende till ditt postdokument.

Du kan:

* [Generera ett XFA-baserat arkivdokument](#generate-an-XFA-based-document-of-record)
* [Skapa ett Acrobat-baserat (Acrobat Form PDF) arkivdokument](#generate-an-Acroform-based-document-of-record)
* [Generera ett postdokument automatiskt](#auto-generate-a-document-of-record)

## Innan du börjar {#components-to-automatically-generate-a-document-of-record}

Innan du börjar lära dig mer och förbereder de resurser som krävs för ett dokument:

**Basmall:** En XFA-mall (XDP-fil) skapad i Forms Designer eller ett Acrobat-formulär (AcroForm). [Basmallen](#base-template-of-a-document-of-record) används för att ange formaterings- och varumärkesinformation för ett postdokument. Överför din XFA-mall (XDP-fil) till din AEM Forms-instans innan

**Anpassat formulär:** Ett anpassat formulär som postdokumentet ska skapas för.

## Generera ett XFA-baserat arkivdokument {#generate-an-XFA-based-document-of-record}

Överför din XFA-mall (XDP-fil) till din AEM Forms-instans. Utför följande steg för att konfigurera ett adaptivt formulär så att XFA-mallen (XDP-filen) används som mall för postdokument:

1. I Experience Manager-författarinstans klickar du på **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents].**
1. Markera ett formulär och klicka på **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Form Model]** i fönstret Egenskaper.
1. Välj **[!UICONTROL Form Model]** eller **[!UICONTROL Select From]** i listrutan **[!UICONTROL Schema]** på fliken **[!UICONTROL None]**. Du kan också välja en formulärmodell när du skapar ett formulär.
1. Välj **Associera formulärmall som postmall** i avsnittet Dokumentmall på fliken Formulärmodell. När du väljer det här alternativet visas alla XFA-mallar (XDP-filer) som är tillgängliga på datorn. Välj lämplig fil. Se även till att samma schema (dataschema) används för Adaptivt formulär och vald XFA-mall (XDP-fil).
1. Klicka på **[!UICONTROL Done]**

Ditt adaptiva formulär är nu konfigurerat att använda en XDP-fil som mall för postdokument. Nästa steg är att [binda adaptiva formulärkomponenter till motsvarande mallfält](#bind-adaptive-form-components-with-template-fields).

## Generera ett Acrobat-baserat arkivdokument {#generate-an-Acroform-based-document-of-record}

Överför din Adobe Acrobat PDF (Acrobat) till din AEM Forms-instans. Följ de här stegen för att konfigurera ett adaptivt formulär så att det använder Adobe Acrobat PDF (Acrobat) som mall för arkivdokument:

1. I Experience Manager-författarinstans klickar du på **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents].**
1. Markera ett formulär och klicka på **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Form Model]** i fönstret Egenskaper.
1. Välj **[!UICONTROL Form Model]** eller **[!UICONTROL Select From]** i listrutan **[!UICONTROL Schema]** på fliken **[!UICONTROL None]**. Du kan också välja en formulärmodell när du skapar ett formulär.
1. Välj **Associera formulärmall som postmall** i avsnittet Dokumentmall på fliken Formulärmodell. När du väljer det här alternativet visas alla Acrobat PDF (Acrobat) som är tillgängliga på datorn. Välj lämplig fil.
1. Klicka på **[!UICONTROL Done]**

Ditt adaptiva formulär är nu konfigurerat att använda en Acrobat som mall för arkivdokument. Nästa steg är att [binda adaptiva formulärkomponenter till motsvarande mallfält](#bind-adaptive-form-components-with-template-fields).

## Generera ett arkivdokument automatiskt {#auto-generate-a-document-of-record}

När ett anpassat formulär konfigureras för att automatiskt generera ett dokument för registrering uppdateras dess dokument omedelbart varje gång ett formulär ändras. Om ett fält till exempel tas bort från ett befintligt anpassat formulär, tas motsvarande fält också bort och visas inte i postdokumentet. Det finns många andra fördelar med att automatiskt generera arkivdokument. :

* Formulärutvecklare behöver inte hantera databindningar manuellt. Automatiskt genererat arkivdokument tar hand om databindningsrelaterade uppdateringar.
* Formulärutvecklare behöver inte manuellt dölja fält som är markerade som exkluderade från postdokumentet. Automatiskt genererat postdokument är förkonfigurerat för att exkludera sådana fält.
* Med det automatiskt genererade alternativet Dokument i post sparar du tid som krävs för att skapa en formulärmall för Dokument i post.
* Med det automatiskt genererade alternativet Dokument för post kan du använda olika format och utseenden med olika basmallar. Det hjälper er att välja det bästa formatet och utseendet för arkivdokument för er organisation. Om du inte anger någon formatering anges systemformaten som standard.
* Automatiskt genererat arkivdokument säkerställer att alla ändringar i formuläret omedelbart återspeglas i arkivdokumentet.

Så här konfigurerar du ett anpassat formulär så att det automatiskt genererar ett postdokument:

1. I Experience Manager-författarinstans klickar du på **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents].**
1. Markera ett formulär och klicka på **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Form Model]** i fönstret Egenskaper.
1. Välj **[!UICONTROL Form Model]** eller **[!UICONTROL Select From]** i listrutan **[!UICONTROL Schema]** på fliken **[!UICONTROL None]**. Du kan också välja en formulärmodell när du skapar ett formulär.
1. Välj **Generera postdokument** i avsnittet Dokumentmall på fliken Formulärmodell.
1. Klicka på **[!UICONTROL Done]**

## Bind adaptiva formulärkomponenter till mallfält {#bind-adaptive-form-components-with-template-fields}

Bind adaptiva formulärfält med mallfält för att visa hämtade formulärdata i motsvarande dokumentationsfält. Så här binder du adaptiva formulärkomponenter till motsvarande dokument i postmallsfält:

1. Öppna det adaptiva formuläret, som är konfigurerat att använda en anpassad formulärmall för redigering.

1. Markera en adaptiv formulärkomponent och klicka på ikonen Konfigurera ![Konfigurera](assets/Smock_Wrench_18_N.svg). Egenskapsläsaren öppnas.

1. Bläddra och markera ett fält i egenskapswebbläsaren.

   * (För AcroForm-mall) egenskapen **[!UICONTROL Document of Record Bind Reference field]**.
   * (För XFA-mall) egenskapen **[!UICONTROL Data Model Bind Reference]**.

1. Klicka på **[!UICONTROL Save]**.

<!-- 
In the following video, Adaptive Form components are bound with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

Du kan använda Skicka e-post, Skicka i Experience Manager-arbetsflöde tillsammans med steget [Dokument i post och andra skicka-åtgärder](configuring-submit-actions.md) för att ta emot ett dokument i inspelningen.

## Inkrementella uppdateringar av dokumentmallen {#document-of-record-template-incremental-updates}

Anpassningsbara formulär och motsvarande dokument med postmallar kan utvecklas under en längre tid. Du kan välja att lägga till, ta bort eller ändra fält i ett adaptivt formulär eller en dokumentmall.

När du ändrar en dokumentmall och överför den ändrade dokumentmallen till AEM Forms, identifierar den adaptiva Forms-redigeraren automatiskt de ändrade bindningarna och informerar dig om adaptiva formulärkomponenter som kräver nya bindningar. Du kan göra inkrementella uppdateringar i en dokumentmall.

En organisation, *We.Retail*, har till exempel en AcroForm-baserad dokumentmall, *we-retail-invoice.pdf*. Mallen ser ut så här:

![Ursprunglig mall](assets/we-retail-invoice.png)

Efter att ha använt mallen ett tag bestämmer sig organisationen för att byta namn på fältet `invoice-number` till fältet `bill-number` och hämta e-postadressen till köparna. En utvecklare uppdaterar namnet på fältet `invoice-number` och lägger till ett e-postfält i mallen. Han skapar också en ny version av mallen *we-retail-invoice-v2.pdf*.

![Uppdaterad mall](assets/we-retail-new-invoice.png)

Utvecklaren överför och tillämpar på den uppdaterade mallen på det adaptiva formuläret. Det adaptiva formuläret identifierar och visar automatiskt en lista med fält där bindningen har ändrats.

![Bindningsfel](assets/we-retail-binding-error.png)

Formulärutvecklaren binder adaptiva Forms-fält med motsvarande dokumentmall.

>[!VIDEO](assets/we-retail-binding.mp4)

När det adaptiva formuläret skickas skapas nu ett uppdaterat arkivdokument.

![Uppdaterad-](assets/we-retail-new-invoice-sent-to-customer.png)

## Viktiga saker att tänka på när du arbetar med arkivdokument {#key-considerations-when-working-with-document-of-record}

Tänk på följande när du arbetar med arkivhandlingar för Adaptiv Forms.

* Dokumentmallar stöder inte RTF-text. Därför visas all RTF-text i det statiska adaptiva formuläret eller i den information som användaren fyller i som oformaterad text i postdokumentet.
* Dokumentfragment i ett anpassat formulär visas inte i postdokumentet. Adaptiva formulärfragment stöds dock.
* Innehållsbindning i dokument för post som genererats för XML-schemabaserat anpassat formulär stöds inte.
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
   <td>Klottersignatur</td>
   <td>Signature Scribble</td>
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
   <td>Lösenordsruta</td>
   <td>Lösenordsfält</td>
   <td>false</td>
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
   <td>Villkor</td>
   <td> </td>
   <td>true</td>
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
   <td>Delformulär <br /> </td>
   <td>Upprepningsbara panelmappar till repeterbara delformulär.</td>
  </tr>
 </tbody>
</table>

### Statiska komponenter {#static-components}

| Adaptiv Form-komponent | Motsvarande XFA-komponent | Anteckningar |
|---|---|---|
| Bild | Bild | Komponenterna TextDraw och Image, oavsett om de är bundna eller obundna, visas alltid i registreringsdokumentet för ett XSD-baserat anpassat formulär, såvida de inte utelämnas med inställningarna för postdokument. |

### Tabeller {#tables}

Tabellkomponenterna i Adaptiv Forms, t.ex. sidhuvud, sidfot och radmappning, till motsvarande XFA-komponenter. Du kan mappa repeterbara paneler till tabeller i Dokumentdokument.

## Basmall för ett postdokument {#base-template-of-a-document-of-record}

Basmallen innehåller formaterings- och utseendeinformation för arkivhandlingar. Du kan anpassa standardutseendet för automatiskt genererade dokument för post. Du kan till exempel använda basmallen för att lägga till företagets logotyp i sidhuvudet och copyrightinformationen i sidfoten i dokumentfönstret.

Mallsidan från basmallen används som mallsida för postdokumentmallen. Mallsidan kan innehålla information som sidhuvud, sidfot och sidnummer som du kan använda på postdokument. Du kan använda den här informationen på Dokument för post med hjälp av basmallen för automatisk generering av Dokument för post. Med hjälp av basmallen kan du ändra standardegenskaperna för fält.

Följ alltid [Basmallskonventioner](#base-template-conventions) när du utformar basmallen.

## Grundmallskonventioner {#base-template-conventions}

En basmall används för att definiera sidhuvud, sidfot, format och utseende för ett postdokument. Sidhuvudet och sidfoten kan innehålla information som företagets logotyp och copyrighttext. Den första mallsidan i basmallen kopieras och används som mallsida för postdokumentet, som innehåller sidhuvud, sidfot, sidnummer eller annan information som ska visas på alla sidor i postdokumentet. Om du använder en basmall som inte överensstämmer med basmallskonventioner, används den första mallsidan från basmallen fortfarande i dokumentmallen. Vi rekommenderar att du utformar din basmall enligt dess konventioner och använder den för automatisk generering av dokumentdokument.

**Konventioner för mallsidor**

* I basmallen ger du rotdelformuläret namnet `AF_METATEMPLATE` och huvudsidan namnet `AF_MASTERPAGE`.

* Huvudsidan med namnet `AF_MASTERPAGE` som finns under rotdelformuläret `AF_METATEMPLATE` är att föredra om du vill extrahera sidhuvud, sidfot och formatinformation.

* Om `AF_MASTERPAGE` saknas används den första mallsidan i basmallen.

**Formateringskonventioner för fält**

* Om du vill använda format på fälten i postdokumentet innehåller basmallen fält som finns i delformuläret `AF_FIELDSSUBFORM` under rotdelformuläret `AF_METATEMPLATE`.

* Egenskaperna för dessa fält används för fälten i postdokumentet. Dessa fält bör följa namnkonventionen för `AF_<name of field in all caps>_XFO`. Fältnamnet för kryssrutan bör till exempel vara `AF_CHECKBOX_XFO`.

Så här skapar du en basmall: Forms Designer.

1. Klicka på **[!UICONTROL File]** > **[!UICONTROL New]**.
1. Välj alternativet **[!UICONTROL Based on a template]**.

1. Välj kategorin **[!UICONTROL Forms - Document of Record]**.
1. Välj **[!UICONTROL DoR Base Template]**.
1. Klicka på **[!UICONTROL Next]** och ange nödvändig information.

1. (Valfritt) Ändra format och utseende på fält som du vill använda i fälten i postdokumentet.
1. Spara formuläret.

Du kan nu använda det sparade formuläret som en basmall för postdokument. Ändra eller ta inte bort några skript i basmallen.

**Ändrar basmall**

* Om du inte använder någon formatering över fält i basmallen bör du ta bort dessa fält från basmallen så att eventuella uppgraderingar av basmallen automatiskt hämtas.
* När du ändrar basmallen ska du inte ta bort, lägga till eller ändra skript.

Följ noga de konventioner och instruktioner som nämns ovan för att utforma en basmall.

## Anpassa varumärkesinformationen i arkivdokumentet {#customize-the-branding-information-in-document-of-record}

När du genererar ett dokument för registrering kan du ändra profileringsinformationen för postdokumentet på fliken Dokument för post. Fliken Dokument för post innehåller alternativ som logotyp, utseende, layout, sidhuvud och sidfot, ansvarsfriskrivning och huruvida du vill ta med omarkerade kryssrutor och alternativknappar eller inte.

Om du vill lokalisera den varumärkesinformation som du anger på fliken Dokument av post kontrollerar du att webbläsarens språkområde är korrekt inställt. Så här anpassar du profileringsinformationen i Document of Record:

1. Markera en panel (rotpanelen) i postdokumentet och välj sedan ![configure](assets/configure.png).
1. Välj ![dortab](assets/dortab.png). Fliken Dokument för post visas.
1. Välj antingen standardmallen eller en anpassad mall för återgivning av postdokumentet. Om du väljer standardmallen visas en miniatyrförhandsvisning av postdokumentet under listrutan Mall.
1. Beroende på om du väljer en standardmall eller en anpassad mall visas några av följande egenskaper, eller alla egenskaper, på fliken Dokument för post. Ange nedanstående egenskaper för att definiera utseendet på postdokumentet:

   1. **Grundläggande egenskaper**:
      * **Mall**: Om du väljer en anpassad mall bläddrar du till en XDP-fil på [!DNL AEM Forms]-servern. Om du vill använda en mall som inte redan finns på din [!DNL AEM Forms]-server bör du först överföra XDP-filen till din [!DNL AEM Forms]-server.
      * **Dekorfärg**: Den färg i vilken rubriktext och avgränsningslinjer återges i dokumentet eller posten PDF.
      * **Teckensnittsfamilj**: Teckensnittsfamilj för texten i PDF Document of Record.

        >[!NOTE]
        >
        > AEM Forms har en mängd inbyggda teckensnitt som är sömlöst integrerade med PDF-filer. [Klicka här](/help/forms/supported-out-of-the-box-fonts.md) om du vill visa en lista över teckensnitt som stöds.

      * **Inkludera formulärobjekt som inte är bundna till datamodell**: Inställning av egenskapen inkluderar obundna fält från schemabaserat anpassat formulär i postdokument.
      * **Uteslut dolda fält från postdokumentet**: Om du anger egenskapen identifieras dolda fält som ska uteslutas från postdokumentet.
      * **Dölj beskrivning av paneler**: Om egenskapen anges utesluts beskrivning av panelen/tabellen från Dokument för post. Gäller för panel och tabell.

      ![Grundläggande egenskaper](/help/forms/assets/basicpropertiesdor.png)

   2. **Egenskaper för formulärfält**:
      * **Visa endast de markerade värdena för komponenterna Kryssruta och Alternativknapp**: Om du anger egenskapen visas endast markerade värden för kryssrutor och alternativknappar i [!UICONTROL Document of Record].
      * **Avgränsare för flera värden**: Du kan välja en avgränsare, till exempel komma eller radbrytning, om du vill visa flera värden.
      * **Alternativ Justering**: Du kan välja önskad justering (Vågrät, Lodrät, Samma som adaptiv form) för att ange justeringen för fält som kryssruta eller alternativknapp som ska visas i [!UICONTROL Document of Record]. Som standard är den lodräta justeringen inställd för fälten i [!UICONTROL Document of Record]. Om du ställer in egenskaperna från [!UICONTROL Form Field Properties] i DoR skrivs egenskaperna som angetts i [!UICONTROL Item Alignment] för fälten i ett adaptivt formulär över. Om du väljer alternativet [!UICONTROL Same as Aaptive form] används justeringen som konfigurerats i en författarinstans för adaptiva formulär för [!UICONTROL Document of Record]-fält.
      * **Antal alternativ för vågrät justering**:You kan ange antalet alternativ som ska visas i postdokumentet för den vågräta justeringen.

      ![Egenskaper för formulärfält](/help/forms/assets/formfieldpropertiesdor.png)

   3. **Egenskaper för mallsida**:
      * **Logotypbild**: Du kan antingen välja att använda logotypbilden från det adaptiva formuläret, välja en från DAM eller överföra en från datorn.
      * **Formulärtitel**: Titel på DoR.
      * **Huvudtext**: Text som visas i rubrikavsnittet i postdokumentet.
      * **Ansvarsfriskrivning**: Etikett för friskrivning.
      * **Ansvarsfriskrivning**: Text som anger omfattningen av rättigheter och skyldigheter i dokumentdokumentet.
      * **Ansvarsfriskrivning**: Ansvarsfriskrivning.

      ![Egenskaper för mallsida](/help/forms/assets/masterpagepropertiesdor.png)

   >[!NOTE]
   >
   >Om du använder en mall för adaptiva formulär som har skapats med en tidigare version av Designer än 6.3 måste du se till att följande finns i mallen för adaptiva färger och teckensnittsfamiljer under rotdelformuläret:

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

1. Välj **[!UICONTROL Done]** om du vill spara profileringsändringarna.

>[!NOTE]
> 
> Om du vill visa en anpassad formulärtitel i ditt postdokument redigerar du den **anpassade formulärtiteln** i **Postdokument** > **Egenskaper för mallsida**. Den här anpassade titeln:
> 
> * Visas i rubriken för den genererade PDF
> * Visas som rubriken i PDF-dokumentegenskaperna
> * Visas som rubrik för den inledande vyn när PDF öppnas

## Dokumentstöd i anpassad formulärredigerare {#dor-support-in-adaptiveform}

Du kan konfigurera mallen [!UICONTROL Document of Record] direkt från den adaptiva formulärredigeraren eller den adaptiva formulärmallsredigeraren.

Utför följande steg från författarinstansen av redigeraren för adaptiva formulär:

1. Markera komponenten **[!UICONTROL Adaptive Form container (Root)]**.
1. Klicka på ikonen ![Konfigurera ikon](/help/forms/assets/configure-icon.svg) för att öppna behållaren **[!UICONTROL Properties]** för det adaptiva formuläret.
1. Öppna fliken **[!UICONTROL Document of Record Template]** och välj bland följande alternativ:
   * **[!UICONTROL None]**: När det här alternativet är markerat skapas ingen [!UICONTROL Document of Record]-mall för ditt adaptiva formulär.
   * **[!UICONTROL Associate Form Template as Document of Record Template]**:Whendet här alternativet är valt, XFA-formulär används som mall för postdokument.
   * **[!UICONTROL Generate Document of Record]**: När det här alternativet är markerat genereras mallen [!UICONTROL Document of Record] automatiskt för ditt adaptiva formulär.

1. Välj ![Spara](/help/forms/assets/check-button.png) om du vill spara egenskaperna.

![Stöd för postmallar för dokument](/help/forms/assets/dor-templatesupport.png)

>[!NOTE]
>
>När mallen [!UICONTROL Document of Record] skapas med en redigerare för anpassad formulärmall är endast två alternativ tillgängliga under [!UICONTROL Document of Record Template] tab as [!UICONTROL None] och [!UICONTROL Generate Document of Record].

## Tabell- och kolumnlayouter för paneler i dokumentformat {#table-and-column-layouts-for-panels-in-document-of-record}

Det anpassade formuläret kan vara långt och innehålla flera formulärfält. Du kanske inte vill spara ett postdokument som en exakt kopia av det anpassade formuläret. Nu kan du välja en tabell- eller kolumnlayout för att spara en eller flera adaptiva formulärpaneler i PDF Document of Record.

Innan du genererar ett postdokument väljer du Layout för postdokumentet för den panelen som Tabell eller Kolumn i inställningarna för en panel. Fälten i panelen ordnas därefter i postdokumentet.

![Fält i en panel återges i en tabelllayout i postdokumentet](assets/dortablelayout.png)

Fält i en panel återges i en tabellayout i postdokumentet

![Fält i en panel återges i en kolumnlayout i postdokumentet](assets/dorcolumnlayout.png)

Fält i en panel återges i en kolumnlayout i postdokumentet

## Dokumentinställningar {#document-of-record-settings}

Med dokumentinställningar kan du välja vilka alternativ du vill inkludera i postdokumentet. En bank godkänner till exempel namn, ålder, personnummer och telefonnummer i ett formulär. Formuläret genererar ett bankkontonummer och filialinformation. Du kan välja att bara visa namn, personnummer, bankkonto och filialinformation i registreringsdokumentet.

Inställningen för dokumentkomponenten är tillgänglig under dess egenskaper. Om du vill komma åt egenskaperna för en komponent markerar du komponenten och klickar på ![cmpr](assets/cmppr.png) i övertäckningen. Egenskaperna listas i sidlisten och du hittar följande inställningar i den.

**Fältnivåinställningar**

* **Uteslut från postdokument**: Om egenskapen true anges exkluderas fältet från postdokument. Det här är en skriptbar egenskap med namnet `excludeFromDoR`. Dess beteende beror på **Uteslut fält från DoR om egenskapen** för dold formulärnivå är aktiv.

* **Visa panelen som tabell:** Om egenskapen anges visas panelen som tabell i postdokument om panelen innehåller färre än 6 fält. Gäller endast för panelen.
* **Exkludera rubrik från postdokument:** Om egenskapen anges exkluderas panelens/tabellens namn från postdokumentet. Gäller endast för panel och tabell.
* **Uteslut beskrivning från postdokument:** Om egenskapen anges exkluderas beskrivning av panelen/tabellen från postdokument. Gäller endast för panel och tabell.

**Inställningar på formulärnivå**

* **Inkludera obundna fält i DoR:** Inställning av egenskapen inkluderar obundna fält från schemabaserat anpassat formulär i arkivdokumentet. Som standard är det sant.
* **Uteslut fält från DoR om de är dolda:** Ange att de dolda fälten ska exkluderas från Dokument för post när formuläret skickas. När du aktiverar [Uppdatera på servern](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), beräknas de dolda fälten på nytt innan de utesluts från postdokumentet.

## Använda en anpassad XCI-fil

En XCI-fil hjälper dig att ange olika egenskaper för ett dokument. Forms as a Cloud Service har en XCI-huvudfil. Du kan använda en anpassad XCI-fil för att åsidosätta en eller flera standardegenskaper som anges i huvud-XCI-filen. Du kan till exempel välja att bädda in ett teckensnitt i ett dokument eller aktivera taggad egenskap för alla dokument. Följande tabell anger XCI-alternativen:

| XCI-alternativ | Beskrivning |
|--- |--- |
| config/present/pdf/creator | Identifierar den som har skapat dokumentet med hjälp av posten Skapare i dokumentinformationsordlistan. Mer information om det här lexikonet finns i [referenshandboken för PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/pdf/producer | Identifierar dokumenttillverkaren med hjälp av posten Producer i dokumentinformationsordlistan. Mer information om det här lexikonet finns i [referenshandboken för PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/layout | Anger om utdata är en enda panel eller sidnumrerad. |
| config/present/pdf/compression/level | Anger den komprimeringsgrad som ska användas när ett PDF-dokument skapas. |
| config/present/pdf/fontInfo/embed | Styr teckensnittsinbäddning i utdatadokumentet. |
| config/present/pdf/scriptModel | Styr om XFA-specifik information ska inkluderas i utdata-PDF-dokumentet. |
| config/present/common/data/adjustData | Kontrollerar om XFA-programmet justerar data efter sammanslagningen. |
| config/present/pdf/renderPolicy | Kontrollerar om genereringen av sidinnehåll görs på servern eller skjuts upp till klienten. |
| config/present/common/locale | Anger den standardspråkinställning som används i utdatadokumentet. |
| config/present/destination | Anger utdataformatet när det finns i ett aktuellt element. Anger vilken åtgärd som ska utföras när dokumentet öppnas i en interaktiv klient när det finns i ett openAction-element. |
| config/present/output/type | Anger vilken typ av komprimering som ska användas för en fil eller vilken typ av utdata som ska skapas. |
| config/present/common/temp/uri | Anger formulär-URI. |
| config/present/common/template/base | Anger en basplats för URI:er i formulärdesignen. När det här elementet saknas eller är tomt används platsen för formulärdesignen som bas. |
| config/present/common/log/to | Styr platsen dit loggdata eller utdata skrivs. |
| config/present/output/to | Styr platsen dit loggdata eller utdata skrivs. |
| config/present/script/currentPage | Anger den inledande sidan när dokumentet öppnas. |
| config/present/script/exclude | Informerar Forms as a Cloud Service om vilka händelser som ska ignoreras. |
| config/present/pdf/linearized | Styr om utdata-PDF-dokumentet är linjärt. |
| config/present/script/runScripts | Styr vilken uppsättning skript Forms as a Cloud Service kör. |
| config/present/pdf/tagged | Styr om taggar ska tas med i utdata-PDF-dokumentet. Taggar i PDF-sammanhang är ytterligare information som ingår i ett dokument för att visa dokumentets logiska struktur. Taggar underlättar hjälpmedelsanvändningen och formateringen. Ett sidnummer kan till exempel taggas som en artefakt så att skärmläsaren inte omsluter den mitt i texten. Även om märkord gör ett dokument mer användbart, ökar de även storleken på dokumentet och bearbetningstiden för att skapa det. |
| config/present/pdf/fontInfo/alwaysEmbed | Anger ett teckensnitt som är inbäddat i utdatadokumentet. |
| config/present/pdf/fontInfo/neverEmbed | Anger ett teckensnitt som aldrig får bäddas in i utdatadokumentet. |
| config/present/pdf/pdfa/part | Anger versionsnumret för den PDF/A-specifikation som dokumentet uppfyller. |
| config/present/pdf/pdfa/amd | Anger ändringsnivån för PDF/A-specifikationen. |
| config/present/pdf/pdfa/conformance | Anger överensstämmelsenivå med PDF/A-specifikationen. |
| config/present/pdf/version | Anger vilken version av PDF-dokument som ska genereras |
| config/present/pdf/version/map | Anger dokumentets reservteckensnitt |

>[!NOTE]
>
> AEM Forms har en mängd inbyggda teckensnitt som är sömlöst integrerade med PDF-filer. [Klicka här](/help/forms/supported-out-of-the-box-fonts.md) om du vill visa en lista över teckensnitt som stöds.


### Använda en anpassad XCI-fil i Forms as a Cloud Service-miljön

1. Lägg till den anpassade XCI-filen i utvecklingsprojektet.
1. Ange följande [textbundna egenskap](/help/implementing/deploying/configuring-osgi.md):

   ```JSON
    {
     "xciFilePath": "[path of XCI file]"
    }
   ```

   Exempel:

   ```JSON
    {
     "xciFilePath": "/content/dam/formsanddocuments/customMinionProBoldAndTagged.xci"
    }
   ```

1. Driftsätt projektet i Cloud Service.

### Använd en anpassad XCI-fil i den lokala utvecklingsmiljön i Forms as a Cloud Service

1. Överför XCI-filen till den lokala utvecklingsmiljön.
1. Öppna konfigurationshanteraren för Cloud Service SDK. Standardwebbadressen är: <http://localhost:4502/system/console/configMgr>.
1. Leta reda på och öppna **[!UICONTROL Adaptive Forms and Interactive Communication Web Channel]**-konfigurationen.
1. Ange sökvägen till XCI-filen och klicka på **[!UICONTROL Save]**.


## Se även {#see-also}

{{see-also}}
