---
title: Vilka arbetsflödessteg kan användas i AEM Forms Cloud Service för att skapa ett arbetsflöde eller för automatisering av affärsprocesser (BPM)?
description: Med Forms-centrerade arbetsflöden kan du snabbt skapa adaptiva Forms-baserade arbetsflöden. Du kan använda Adobe Sign för att e-signera dokument, skapa formulärbaserade affärsprocesser, hämta och skicka data till flera datakällor och skicka e-postmeddelanden
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: Använd AEM-arbetsflöden, tilldela uppgiftssteg, konvertera till PDF/A-steg, generera dokument för inspelat steg, använda arbetsflöden, signera dokumentsteg, generera utskrift, generera icke-interaktiva PDF-utdata
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '6721'
ht-degree: 0%

---


# Använd Forms-centrerade AEM Workflows - Step Reference för att automatisera affärsprocesserna {#forms-centric-workflow-on-osgi-step-reference}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Du använder arbetsflödesmodeller. En modell hjälper dig att definiera och köra en serie steg. Du kan också definiera modellegenskaper, t.ex. om arbetsflödet är tillfälligt eller använder flera resurser. Du kan [inkludera olika AEM Workflow-steg i en modell för att uppnå affärslogiken](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE#extending-aem).

## Forms-centrerade steg {#forms-workflow-steps}

Forms-baserade arbetsflödessteg utför AEM Forms-specifika åtgärder i ett AEM-arbetsflöde. Med dessa steg kan du snabbt skapa ett adaptivt Forms-baserat Forms-baserat arbetsflöde i OSGi. Dessa arbetsflöden kan användas för att utveckla enkla arbetsflöden för granskning och godkännande, interna och övergripande affärsprocesser. Du kan även använda Forms Workflow steg för att:

* Skapa affärsprocesser, arbetsflöden efter inlämningen och serverbaserade arbetsflöden för att hantera registreringsprocesser.

* Skapa och tilldela uppgifter till en användare eller grupp.

* Använd [!DNL Adobe Sign] i ett AEM-arbetsflöde för att skicka ett dokument för signering.

* Generera ett dokument för registrering on demand eller när formulär skickas.

* Koppla samman en arbetsflödesmodell med olika datakällor för att enkelt spara och hämta data.

* Använd e-poststeget för att skicka e-postmeddelanden och andra bilagor när en åtgärd har slutförts och när arbetsflödet har påbörjats eller slutförts.

>[!NOTE]
>
>Om arbetsflödesmodellen är markerad för ett externt lagringsutrymme kan du för alla Forms Workflow-steg bara välja variabelalternativet för att lagra eller hämta datafiler och bilagor.

## Tilldela aktivitetssteg {#assign-task-step}

Tilldela ett arbetsobjekt och tilldelar det till en användare eller grupp. Förutom att tilldela uppgiften anger komponenten även den adaptiva formen eller icke-interaktiva PDF för uppgiften. Det adaptiva formuläret krävs för att kunna ta emot indata från användare och icke-interaktiva PDF eller ett skrivskyddat adaptivt formulär används endast för granskning.

Du kan också använda komponenten för att styra aktivitetens beteende. Du kan till exempel skapa ett automatiskt dokument för post, tilldela uppgiften till en viss användare eller grupp, ange sökvägen för skickade data, ange sökvägen för data som ska fyllas i i förväg och ange standardåtgärder. Tilldela uppgift-steget har följande egenskaper:

* **[!UICONTROL Title]**: Aktivitetens namn. Titeln visas i AEM Inbox.
* **[!UICONTROL Description]**: Förklaring av de åtgärder som utförs i aktiviteten. Den här informationen är användbar för andra processutvecklare när du arbetar i en delad utvecklingsmiljö.

* **[!UICONTROL Thumbnail Path]**: Sökväg till aktivitetsminiatyrbilden. Om ingen sökväg anges visas en standardminiatyrbild för ett adaptivt formulär och en standardikon för Postdokument.
* **[!UICONTROL Workflow Stage]**: Ett arbetsflöde kan ha flera steg. Dessa steg visas i AEM Inbox. Du kan definiera dessa steg i modellens egenskaper (Sidekick > Sida > Sidegenskaper > Steg).
* **[!UICONTROL Priority]**: Den valda prioriteten visas i AEM Inbox. De tillgängliga alternativen är Hög, Medium och Låg. Standardvärdet är Medium.
* **[!UICONTROL Due Date]**: Ange antalet dagar eller timmar efter vilka aktiviteten har markerats som försenad. Om du väljer **[!UICONTROL Off]** markeras aktiviteten aldrig som försenad. Du kan också ange en uttidshanterare för att utföra vissa åtgärder när åtgärden är försenad.

* **[!UICONTROL Days]**: Antalet dagar innan aktiviteten ska slutföras. Antalet dagar räknas efter att uppgiften har tilldelats en användare. Om en uppgift inte är fullständig och korsar det antal dagar som anges i fältet Dagar, aktiveras en timeout-hanterare efter förfallodatumet om den väljs.
* **[!UICONTROL Hours]**: Antalet timmar innan aktiviteten ska slutföras. Antalet timmar räknas efter att uppgiften har tilldelats en användare. Om en uppgift inte är slutförd och korsar det antal timmar som anges i fältet Timmar, aktiveras en timeout-hanterare efter de timmar som ska förfalla.
* **[!UICONTROL Time-out after Due Date]**: Välj det här alternativet om du vill aktivera markeringsfältet för Timeout-hanterare.
* **[!UICONTROL Timeout Handler]**: Välj det skript som ska köras när tilldelningsaktivitetssteget överskrider förfallodatumet. Skript som placeras i CRX-databasen på [apps]/fd/dashboard/scripts/timeoutHandler är tillgängliga för val. Den angivna sökvägen finns inte i crx-databasen. En administratör skapar sökvägen innan den används.
* **[!UICONTROL Highlight the action and comment from the last task in Task Details]**: Välj det här alternativet om du vill visa den senaste åtgärden som utfördes och kommentarer som togs emot i aktivitetsinformationsavsnittet för en uppgift.
* **[!UICONTROL Type]**: Välj vilken typ av dokument som ska fyllas i när arbetsflödet startas. Du kan välja ett adaptivt formulär, ett skrivskyddat adaptivt formulär, ett icke-interaktivt PDF-dokument.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Use Adaptive Form]**: Ange den metod som ska användas för att hitta det adaptiva indataformuläret. Det här alternativet är tillgängligt om du väljer Adaptivt formulär eller Skrivskyddat anpassat formulär i listrutan Typ. Du kan använda det adaptiva formulär som skickas till arbetsflödet, som finns på en absolut sökväg eller som finns på en sökväg i en variabel. Du kan använda en variabel av typen String för att ange sökvägen.\
  Du kan koppla flera adaptiva Forms till ett arbetsflöde. Det innebär att du kan ange ett adaptivt formulär i körningsmiljön med de tillgängliga indatametoderna.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Adaptive Form Path]**: Ange sökvägen för det adaptiva formuläret. Du kan använda det adaptiva formulär som skickas till arbetsflödet, finns på en absolut sökväg eller hämta det adaptiva formuläret från en sökväg som lagras i en variabel av strängdatatyp.
* **[!UICONTROL Select input PDF using]**: Ange sökvägen till ett icke-interaktivt PDF-dokument. Fältet är tillgängligt när du väljer ett icke-interaktivt PDF-dokument i typfältet. Du kan välja indata-PDF med hjälp av sökvägen som är relativ till nyttolasten, sparad med en absolut sökväg eller med hjälp av en variabel av datatypen Document. Exempel: [Payload_Directory]/Workflow/PDF/credit-card.pdf. Sökvägen finns inte i crx-databasen. En administratör skapar sökvägen innan den används. Du måste ha alternativet Dokument för post aktiverat eller formulärmallsbaserad Adaptiv Forms för att kunna använda alternativet PDF Path.
* **[!UICONTROL For completed task, render the Adaptive Form as]**: När en uppgift har markerats som slutförd kan du återge det adaptiva formuläret som ett skrivskyddat adaptivt formulär eller ett PDF-dokument. Du måste ha alternativet Dokument för post aktiverat eller formulärmallsbaserad Adaptiv Forms för att kunna återge det adaptiva formuläret som Dokument för post.
* **[!UICONTROL Pre-populated]**: Följande fält i listan nedan fungerar som indata för uppgiften:

   * **[!UICONTROL Select input data file using]**: Sökväg till indatafil (.json, .xml, .doc eller formulärdatamodell (FDM)). Du kan hämta indatafilen med en sökväg som är relativ till nyttolasten eller hämta filen som lagras i en variabel av datatypen Document, XML eller JSON. Filen innehåller till exempel data som skickats för formuläret via ett AEM Inbox-program. En exempelsökväg är [Payload_Directory]/workflow/data.
   * **[!UICONTROL Select input attachments using]**: Bifogade filer som är tillgängliga på platsen bifogas till formuläret som är associerat med uppgiften. Sökvägen kan vara relativ till nyttolasten eller hämta den bifogade filen som lagras i en variabel i ett dokument. En exempelsökväg är [Payload_Directory]/attachments/. Du kan ange bifogade filer som placeras i förhållande till nyttolasten eller använda en dokumenttypsvariabel (Array list > Document) för att ange en bifogad indatafil för det adaptiva formuläret.

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Request Attribute Mapping]**: Använd avsnittet Mappning av attribut för begäran för att definiera [namnet och värdet för attributet ](work-with-form-data-model.md#bindargument) för begäran. Hämta informationen från datakällan baserat på attributnamnet och värdet som anges i begäran. Du kan definiera ett attributvärde för begäran med hjälp av ett literalt värde eller en variabel av datatypen String.

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Submitted information]**: Följande fält i listan nedan fungerar som utdataplatser för uppgiften:

   * **[!UICONTROL Save output data file using]**: Spara datafilen (.json, .xml, .doc eller formulärdatamodell (FDM)). Datafilen innehåller information som skickas via det associerade formuläret. Du kan spara utdatafilen med en sökväg som är relativ till nyttolasten eller lagra den i en variabel av datatypen Document, XML eller JSON. Exempel: [Payload_Directory]/Workflow/data, där data är en fil.
   * **[!UICONTROL Save attachments using]**: Spara formulärbilagorna som anges i en uppgift. Du kan spara de bifogade filerna med en sökväg som är relativ till nyttolasten eller lagra den i en variabel i arraylistan med dokumentdatatypen.
   * **[!UICONTROL Save Document of Record using]**: Sökväg för att spara en postdokumentfil. Exempel: [Payload_Directory]/DocumentofRecord/credit-card.pdf. Du kan spara postdokumentet med en sökväg som är relativ till nyttolasten eller lagra det i en variabel av dokumentdatatypen. Om du väljer alternativet **[!UICONTROL Relative to Payload]** genereras inte postdokumentet om sökvägsfältet lämnas tomt. Det här alternativet är bara tillgängligt om du väljer Adaptivt formulär i listrutan Typ.

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Assignee]** > **[!UICONTROL Assign options]**: Ange den metod som ska användas för att tilldela en användare uppgiften. Du kan dynamiskt tilldela uppgiften till en användare eller en grupp med skriptet för deltagarväljaren eller tilldela uppgiften till en viss AEM-användare eller grupp.
* **[!UICONTROL Participant Chooser]**: Alternativet är tillgängligt när alternativet **[!UICONTROL Dynamically to a user or group]** har valts i fältet Tilldela alternativ. Du kan använda ett ECMAScript eller en tjänst för att dynamiskt välja en användare eller grupp. Mer information finns i [Skapa ett anpassat Adobe Experience Manager Dynamic Participant-steg](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=sv-SE&CID=RedirectAEMCommunityKautuk).

* **[!UICONTROL Participants]**: Fältet är tillgängligt när alternativet **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** har valts i fältet **[!UICONTROL Participant Chooser]**. I fältet kan du välja användare eller grupper för alternativet RandomParticipantChooser.

* **[!UICONTROL Assignee]**: Fältet är tillgängligt när **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** har valts i fältet **[!UICONTROL Participant Chooser]**. I fältet kan du välja en variabel av datatypen String för att definiera den som tilldelas.

* **[!UICONTROL Arguments]**: Fältet är tillgängligt när ett annat skript än skriptet RandomParticipantChoose har valts i fältet Deltagarväljare. I fältet kan du ange en lista med ett kommaavgränsat argument för det skript som valts i fältet Deltagare.

* **[!UICONTROL User or Group]**: Uppgiften tilldelas en vald användare eller grupp. Alternativet är tillgängligt när **[!UICONTROL To a specific user or group option]** har valts i fältet **[!UICONTROL Assign options]**. I fältet visas alla användare och grupper i gruppen [!DNL workflow-users].\
  I listrutan **[!UICONTROL User or Group]** visas de användare och grupper som den inloggade användaren har åtkomst till. Visningen av användarnamn beror på om du har åtkomstbehörighet till noden **[!UICONTROL users]** i crx-databasen för den aktuella användaren.

* **[!UICONTROL Send Notification Email]**: Välj det här alternativet om du vill skicka e-postmeddelanden till den som tilldelats. Dessa meddelanden skickas när en uppgift tilldelas en användare eller grupp. Du kan använda alternativet **[!UICONTROL Recipient Email Address]** för att ange vilken mekanism som ska användas för att hämta e-postadressen.

* **[!UICONTROL Recipient Email Address]**: Du kan lagra en e-postadress i en variabel, använda en litteral för att ange en permanent e-postadress eller använda den förvalda e-postadressen för den som har angetts i profilen för den som tilldelats. Du kan använda literalen eller en variabel för att ange en grupps e-postadress. Variabelalternativet är användbart när du dynamiskt vill hämta och använda en e-postadress. Alternativet **[!UICONTROL Use default email address of the assignee]** är endast för en tilldelad. I det här fallet används den e-postadress som lagras i användarprofilen för tilldelade användare.

* **[!UICONTROL HTML Email Template]**: Välj e-postmall för e-postmeddelandet. Om du vill redigera en mall ändrar du filen på /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt i crx-databasen.
* **[!UICONTROL Allow Delegation To]**: I AEM Inbox finns ett alternativ för den inloggade användaren att delegera det tilldelade arbetsflödet till en annan användare. Du får delegera inom samma grupp eller till arbetsflödesanvändaren i en annan grupp. Om uppgiften har tilldelats en enskild användare och alternativet **[!UICONTROL allow delegation to members of the assignee group]** har valts går det inte att delegera uppgiften till en annan användare eller grupp.
* **[!UICONTROL Share Settings]**: AEM Inbox innehåller alternativ för att dela en eller alla uppgifter i inkorgen med en annan användare:
   * När alternativet **[!UICONTROL Allow assignee to share explicitly in inbox]** är markerat kan användaren markera uppgiften i AEM Inbox och dela den med en annan AEM-användare.
   * När alternativet **[!UICONTROL Allow assignee to share via inbox sharing]** är markerat och användarna delar sina inkorgsobjekt eller tillåter andra användare att få åtkomst till sina inkorgsobjekt, delas endast uppgifter med det tidigare nämnda alternativet.
   * När **[!UICONTROL Allow assignee to delegate using 'Out of Office' settings]** har valts. Uppdragaren kan aktivera alternativet att delegera uppgiften till andra användare tillsammans med andra frånvaroalternativ. Alla nya uppgifter som tilldelas till användaren utanför kontoret delegeras automatiskt (tilldelas) till de användare som anges i inställningarna utanför kontoret.

  Det gör att andra användare kan välja tilldelningsuppgifter när de inte är på kontoret och inte kan arbeta med tilldelade uppgifter.

* **[!UICONTROL Actions]** > **[!UICONTROL Default Actions]**: Utanför rutan finns åtgärderna Skicka, Spara och Återställ. Som standard är alla standardåtgärder aktiverade.
* **[!UICONTROL Route Variable]**: Namn på flödesvariabeln. Vägvariabeln hämtar anpassade åtgärder som en användare väljer i AEM Inbox.
* **[!UICONTROL Routes]**: En aktivitet kan förgrena till olika vägar. När du väljer det här alternativet i AEM Inbox returneras ett värde och arbetsflödesgrenarna baserat på det valda flödet. Du kan antingen lagra vägar i en variabel av datatypen String eller välja **[!UICONTROL Literal]** om du vill lägga till vägar manuellt.

* **[!UICONTROL Route Title]**: Ange ruttens titel. Den visas i AEM Inbox.
* **[!UICONTROL Coral Icon]**: Ange ett HTML-attribut för en korallikon. Adobe CorelUI-biblioteket innehåller en mängd ikoner som sätter fokus först. Du kan välja och använda en ikon för rutten. Den visas tillsammans med titeln i AEM Inbox. Om du lagrar rutterna i en variabel använder rutterna en taggikon.
* **[!UICONTROL Allow assignee to add comment]**: Välj det här alternativet om du vill aktivera kommentarer för uppgiften. En tilldelad kan lägga till kommentarerna inifrån AEM Inbox när uppgiften skickas.
* **[!UICONTROL Save comment in variable]**: Spara kommentaren i en variabel av datatypen String. Det här alternativet visas bara om du markerar kryssrutan **[!UICONTROL Allow assignee to add comment]**.

* **[!UICONTROL Allow assignee to add attachments to the task]**: Välj det här alternativet om du vill aktivera bilagor för uppgiften. En tilldelad kan lägga till de bifogade filerna inifrån AEM Inbox när uppgiften skickas. Du kan också begränsa den maximala storleken **[!UICONTROL (Maximum File Size)]** för en bifogad fil. Standardstorleken är 2 MB.

* **[!UICONTROL Save output task attachments using]**: Ange platsen för den bifogade mappen. Du kan spara bilagor för utdatauppgifter med en relativ sökväg till nyttolasten eller med en variabel av en array med dokumentdatatyper. Det här alternativet visas bara om du markerar kryssrutan **[!UICONTROL Allow assignee to add attachments to the task]** och väljer **[!UICONTROL Adaptive Form]**, **[!UICONTROL Read-only Adaptive Form]** eller **[!UICONTROL Non-interactive PDF document]** i listrutan **[!UICONTROL Type]** på fliken **[!UICONTROL Form/Document]**.

* **[!UICONTROL Use custom metadata]**: Välj det här alternativet om du vill aktivera det anpassade metadatafältet. Anpassade metadata används i e-postmallar.
* **[!UICONTROL Custom Metadata]**: Välj anpassade metadata för e-postmallarna. Anpassade metadata är tillgängliga i crx-databaser på apparna/fd/dashboard/scripts/metadataScripts. Den angivna sökvägen finns inte i crx-databasen. En administratör skapar sökvägen innan den används. Du kan också använda en tjänst för anpassade metadata. Du kan också utöka gränssnittet `WorkitemUserMetadataService` för att tillhandahålla anpassade metadata.
* **[!UICONTROL Show Data from Previous Steps]**: Välj det här alternativet om du vill aktivera tilldelningar för att visa tidigare tilldelningar, åtgärder som redan har vidtagits för uppgiften, kommentarer som har lagts till i uppgiften och dokumentdokument för den slutförda uppgiften, om tillgängligt.
* **[!UICONTROL Show Data from Subsequent Steps]**: Välj det här alternativet om du vill aktivera den aktuella tilldelade personen för att visa den åtgärd som vidtagits och de kommentarer som lagts till i uppgiften av efterföljande tilldelningar. Den aktuella tilldelaren kan även visa en dokumentfil för den slutförda uppgiften, om en sådan finns.
* **[!UICONTROL Visibility of data type]**: Som standard kan en tilldelad visa ett dokument för registrering, tilldelningar, åtgärd och kommentarer som tidigare och efterföljande tilldelningar har lagt till. Använd datatypsalternativet för synlighet för att begränsa vilken typ av data som är synlig för de tilldelade.

>[!NOTE]
>
>Alternativen för att spara steget Tilldela uppgift som utkast och för att hämta historiken för steget Tilldela uppgift inaktiveras när du konfigurerar en arbetsflödesmodell för AEM för extern datalagring. I Inkorgen är dessutom alternativet att spara inaktiverat.

## Konvertera till PDF/A {#convert-pdfa}

PDF/A är ett arkiveringsformat för långtidsbevaring av dokumentets innehåll, genom att bädda in teckensnitten och dekomprimera filen. Därför är ett PDF/A-dokument vanligtvis större än ett vanligt PDF-dokument. Du kan använda steget ***Konvertera till PDF/A*** i ett AEM-arbetsflöde för att konvertera dina PDF-dokument till PDF/A-format.

Konvertera till PDF/A-steget har följande egenskaper:

**[!UICONTROL Input Document]**: Indatadokumentet kan vara relativt till nyttolasten, ha en absolut sökväg, kan anges som en nyttolast eller lagras i en variabel av dokumentdatatypen.

**[!UICONTROL Conversion Options]**: Med den här egenskapen anges inställningarna för konvertering av PDF-dokument till PDF/A-dokument. De olika alternativ som är tillgängliga under den här fliken är:
* **[!UICONTROL Compliance]**: Anger den standard som utdata-PDF/A-dokumentet måste uppfylla. Det stöder olika PDF-standarder som PDF/A-1b, PDF/A-2b eller PDF/A-3b.
* **[!UICONTROL Result Level]**: Anger resultatnivån som PassFail, Summary eller Detailed för konverteringsutdata.
* **[!UICONTROL Color Space]**: Anger den fördefinierade färgrymden som S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED eller SWOP, som kan användas för utdata i PDF/A-filer.
* **[!UICONTROL Optional Content]**: Tillåt att specifika grafiska objekt och/eller anteckningar visas i utdata-PDF/A-dokument endast när en angiven uppsättning villkor uppfylls.

**[!UICONTROL Output Documents]**: Anger platsen där utdatafilen ska sparas. Utdatafilen kan sparas på en plats som är relativ till nyttolasten, skriver över nyttolasten, om nyttolasten är en fil eller i en variabel av dokumentdatatypen.


## Skicka e-poststeg {#send-email-step}

Använd e-poststeget för att skicka ett e-postmeddelande, till exempel ett e-postmeddelande med ett postdokument, en länk till ett anpassat formulär <!-- , link of an interactive communication--> eller med ett bifogat PDF-dokument. Skicka e-post-steget stöder [HTML-e-post](https://en.wikipedia.org/wiki/HTML_email). HTML e-postmeddelanden är responsiva och anpassar sig efter mottagarnas e-postklient och skärmstorlek. Du kan använda en e-postmall från HTML för att definiera utseendet, färgschemat och beteendet för e-postmeddelandet.

I e-poststeget används Day CQ Mail Service för att skicka e-postmeddelanden. Kontrollera att e-posttjänsten är konfigurerad innan du använder e-poststeget. E-poststöd är som standard bara för HTTP- och HTTP-protokoll. [Kontakta supportteamet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=sv-SE#sending-email) om du vill aktivera portar för att skicka e-post och aktivera SMTP-protokoll för din miljö. Begränsningen bidrar till att förbättra plattformens säkerhet.

E-poststeget har följande egenskaper:

**[!UICONTROL Title]**: Stegen för steget hjälper dig att identifiera steget i arbetsflödesredigeraren.

**[!UICONTROL Description]**: Förklaring är användbar för andra processutvecklare när du arbetar i en delad utvecklingsmiljö.

**[!UICONTROL Email Subject]**: Ämne kan hämtas från ett arbetsflödes-metadata, anges manuellt eller hämtas från värdet som lagras i en variabel. Välj bland följande alternativ:

* **[!UICONTROL Literal]** Ange ett ämne manuellt.
* **[!UICONTROL Retrieve from Workflow metadata]** - Hämta ämnet från en metadataegenskap.
* **[!UICONTROL Variable]** - Hämta ämnet från värdet som lagras i en variabel av strängdatatyp.

**[!UICONTROL HTML Email Template]**: HTML-mall för e-postmeddelandet. Du kan ange variabler i en e-postmall. E-poststeget extraheras och visar alla variabler som ingår i en mall för indata.

**[!UICONTROL Email Template Metadata]**: Värdet för e-postmallvariablerna kan vara ett användarspecificerat värde, sökvägen till en resurs på författaren eller publiceringsservern, bilden eller en metadataegenskap för arbetsflödet.

* **[!UICONTROL Literal]**: Använd alternativet när du känner till det exakta värdet som ska anges. Exempel: [example@example.com](mailto:example@example.com).

* **[!UICONTROL Workflow Metadata]**: Använd alternativet när värdet som ska användas sparas i en metadataegenskap för arbetsflöde. När du har valt alternativet anger du metadataegenskapens namn i den tomma textrutan under alternativet Metadata för arbetsflöde. Till exempel emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Image]**: Använd alternativet för att bädda in en bild i e-postmeddelandet. När du har valt alternativet bläddrar du och väljer bilden. Bildalternativet är bara tillgängligt för de bildtaggar (&lt;img src=&quot;&#42;&quot;/>) som är tillgängliga i e-postmallen.

**[!UICONTROL Sender's / Recipient's Email Address]**: Välj alternativet **[!UICONTROL Literal]** om du vill ange en e-postadress manuellt eller välj alternativet **[!UICONTROL Retrieve from Workflow metadata]** om du vill hämta e-postadressen från en metadataegenskap. Du kan också ange en lista med egenskapsmatriser för metadata för alternativet **[!UICONTROL Retrieve from Workflow metadata]**. Välj alternativet **[!UICONTROL Variable]** om du vill hämta e-postadressen från värdet som lagras i en variabel av strängdatatyp.

* **[!UICONTROL File Attachment]**: Den tillgängliga resursen på den angivna platsen är kopplad till e-postmeddelandet. Resursens sökväg kan vara relativ till nyttolasten eller den absoluta sökvägen. En exempelsökväg är [Payload_Directory]/attachments/.

Välj alternativet **[!UICONTROL Variable]** om du vill hämta den bifogade filen som lagras i en variabel av datatypen Dokument, XML eller JSON.

**[!UICONTROL File Name]**: Namnet på e-postbilagefilen. E-poststeget ändrar det ursprungliga filnamnet för den bifogade filen till det angivna filnamnet. Namnet kan anges manuellt eller hämtas från en metadataegenskap eller variabel i arbetsflödet. Använd alternativet **[!UICONTROL Literal]** när du vet exakt vilket värde du ska ange. Använd alternativet **[!UICONTROL Variable]** för att hämta filnamnet från värdet som lagras i en variabel av strängdatatyp. Använd alternativet **[!UICONTROL Retrieve from a Workflow Metadata]** när värdet som ska användas sparas i en metadataegenskap för arbetsflöde.

## Generera dokumentarkivhandlingssteget {#generate-document-of-record-step}

När ett formulär fylls i eller skickas kan du spara en post med formuläret, i utskrift eller i dokumentformat. Den här posten kallas dokumentarkivhandling (DoR). Du kan använda steget Skapa dokument för post för att skapa en skrivskyddad eller interaktiv PDF-version av ett anpassat formulär. PDF-versionen innehåller information som fylls i i formuläret tillsammans med layouten för det adaptiva formuläret.

Dokumentsteget har följande egenskaper:

**[!UICONTROL Use Adaptive Form]**: Ange den metod som ska användas för att hitta det adaptiva indataformuläret. Du kan använda det adaptiva formulär som skickas till arbetsflödet, som finns på en absolut sökväg eller som finns på en sökväg i en variabel. Du kan använda en variabel av datatypen String för att ange sökvägen i fältet **[!UICONTROL Select variable to resolve]**.\
Du kan koppla flera adaptiva Forms till ett arbetsflöde. Det innebär att du kan ange ett adaptivt formulär i körningsmiljön med de tillgängliga indatametoderna.

**[!UICONTROL Adaptive Form Path]**: Ange sökvägen för det adaptiva formuläret. Fältet är tillgängligt när du väljer alternativet **[!UICONTROL Available at an absolute path]** i fältet **[!UICONTROL Use Adaptive Form]**.

**[!UICONTROL Select Input data using]**: Sökväg till indata för det adaptiva formuläret. Du kan behålla data på en plats i förhållande till nyttolasten, ange en absolut sökväg till data eller hämta data som lagras i en variabel av datatypen Document, JSON eller XML. Indata sammanfogas med det adaptiva formuläret för att skapa ett postdokument.

**[!UICONTROL Select Input attachment path using]**: Sökväg till de bifogade filerna. De här bifogade filerna ingår i dokumentdokumentet. Du kan behålla de bifogade filerna på en plats i förhållande till nyttolasten, ange en absolut sökväg för de bifogade filerna eller hämta bifogade filer som lagras i en variabel av dokumentdatatypen.

Om du anger sökvägen till en mapp, till exempel bilagor, bifogas alla filer som är direkt tillgängliga i mappen till Dokument för post. Om det finns filer i de mappar som är direkt tillgängliga i den angivna sökvägen inkluderas filerna i Postdokument som bilagor. Om det finns mappar i direkt tillgängliga mappar hoppas de mapparna över.

**[!UICONTROL Save Generated Document of Record using below options]**: Ange platsen för att behålla en postdokumentfil. Du kan välja att skriva över nyttolastmappen, placera postdokumentet på en plats i nyttolastkatalogen eller lagra postdokumentet i en variabel av dokumentdatatypen.

**[!UICONTROL Locale]**: Ange språk för postdokumentet. Välj **[!UICONTROL Literal]** om du vill välja språkområde från en nedrullningsbar lista eller välj **[!UICONTROL Variable]** om du vill hämta språkområdet från det värde som lagras i en variabel av strängdatatyp. Definiera språkkoden medan värdet för språkinställningen lagras i en variabel. Ange till exempel **en_US** för engelska och **fr_FR** för franska.

## Anropa DDX-steg {#invokeddx}

Document Description XML (DDX) är ett deklarativt kodspråk vars element representerar byggstenar av dokument. Dessa byggstenar innehåller PDF- och XDP-dokument och andra element som kommentarer, bokmärken och formaterad text. DDX definierar en uppsättning åtgärder som kan tillämpas på ett eller flera indatadokument för att generera ett eller flera utdatadokument. Ett enda DX kan användas med ett antal olika källdokument. Du kan använda steget ***Anropa DDX*** i ett AEM-arbetsflöde för att utföra olika åtgärder, som att samla ihop disassemblerande dokument, skapa och ändra Acrobat och XFA Forms, och andra som beskrivs i [DDX-referensdokumentationen](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

Anropa DDX-steget har följande egenskaper:

**[!UICONTROL Input Documents]**: Används för att ange egenskaper för ett indatadokument. De olika alternativ som är tillgängliga under den här fliken är:
* **[!UICONTROL Specify DDX Using]**: Anger indatadokumentet relativt till nyttolasten, har en absolut sökväg, kan anges som nyttolast eller lagras i en variabel av dokumentdatatypen.
* **[!UICONTROL Create Map from Payload]**: Lägg till alla dokument under nyttolastmappen i Input Document&#39;s Map för invoke API i Assembler. Nodnamnet för varje dokument används som en nyckel på kartan.
* **[!UICONTROL Input Document's Map]**: Alternativet används för att lägga till flera poster med knappen **[!UICONTROL ADD]**. Varje post representerar dokumentets nyckel på kartan och dokumentets källa.

**[!UICONTROL Environment Options]**: Det här alternativet används för att ange bearbetningsinställningar för anrop-API. De olika alternativ som är tillgängliga under den här fliken är:
* **[!UICONTROL Validate Only]**: Kontrollerar giltigheten för indata-DDX-dokumentet.
* **[!UICONTROL Fail on Error]**: Ett booleskt värde som anger om API-anropstjänsten misslyckas, om ett fel uppstår eller inte. Som standard är värdet Falskt.
* **[!UICONTROL First Bates Number]**: Anger talet, som ökar automatiskt. Det här självökande numret visas automatiskt på varje sida i följd.
* **[!UICONTROL Default Style]**: Anger standardformatet för utdatafilen.

>[!NOTE]
>
>Miljöalternativen hålls synkroniserade med HTTP-API:er.

**[!UICONTROL Output Documents]**: Anger platsen där utdatafilen ska sparas. De olika alternativ som är tillgängliga under den här fliken är:
* **[!UICONTROL Save Output in Payload]**: Sparar utdatadokument under nyttolastmappen, eller skriver över nyttolasten om nyttolasten är en fil.
* **[!UICONTROL Output Document's Map]**: Anger platsen där varje dokumentfil ska sparas explicit genom att lägga till en post per dokument. Varje post representerar dokumentet och platsen där det ska sparas. Om det finns flera utdatadokument används det här alternativet.

## Anropa tjänststeget i FDM (Form Data Model) {#invoke-form-data-model-service-step}

Du kan använda [[!DNL AEM Forms] Dataintegrering](data-integration.md) för att konfigurera och ansluta till olika datakällor. Dessa datakällor kan vara en webbtjänst, REST-tjänst, OData-tjänst och CRM-lösning. Med dataintegrering i [!DNL AEM Forms] kan du skapa en formulärdatamodell (FDM) som omfattar olika tjänster för att utföra datahämtnings-, additions- och uppdateringsåtgärder för den konfigurerade databasen. Du kan använda **[!UICONTROL Invoke Data Model Service step]** för att välja en formulärdatamodell (FDM) och använda FDM-tjänsterna för att hämta, uppdatera eller lägga till data i olika datakällor.

Följande databastabell och JSON-filen används som exempel för att förklara indata för stegfält:

**[!UICONTROL Sample CustomerDetails table]**

<table>
 <tbody> 
  <tr> 
   <td>Egenskap</td> 
   <td>Värde <br /> </td> 
  </tr> 
  <tr> 
   <td>FirstName<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>LastName</td> 
   <td>ros</td> 
  </tr> 
  <tr> 
   <td>Kund-ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>E-postadress <br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL Sample JSON file]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

FDM-tjänststeget (Invoke Form Data Model) innehåller följande listade fält som underlättar FDM-åtgärder (Form Data Model):

* **[!UICONTROL Title]**: Stegen är titel. Det hjälper till att identifiera stegen i arbetsflödesredigeraren.
* **[!UICONTROL Description]**: Förklaring är användbar för andra processutvecklare när du arbetar i en delad utvecklingsmiljö.

* **[!UICONTROL Form Data Model Path]**: Bläddra och välj en formulärdatamodell (FDM) som finns på servern.

* **[!UICONTROL Errors and Validations]**: Med alternativet kan du hämta felmeddelanden och ange valideringsalternativ för data som hämtas och skickas till datakällor. Med dessa ändringar kan du se till att data som skickas till FDM-tjänststeget (Invoke Form Data Model) följer de databegränsningar som definieras av datakällan. Mer information finns i [Automatisk validering av indata](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Validation level]**: Det finns tre valideringskategorier: Basic, Full och OFF:

   * Fullständig: Alla begränsningar valideras.
   * Grundläggande: Endast obligatoriska och nullbara begränsningar
   * AV: Ingen validering sker.

* **[!UICONTROL Terminate Workflow on Failure]**: När en begränsning inte kan valideras stoppas arbetsflödet.

* **[!UICONTROL Store Error Code in Variable]**: Du kan lagra en felkod i en [String-typvariabel](variable-in-aem-workflows.md).

* **[!UICONTROL Store Error Message in Variable]**: Du kan lagra ett felmeddelande i en [String-typvariabel](variable-in-aem-workflows.md).

* **[!UICONTROL Store Error Details in Variable]**: Du kan lagra en feldetalj i en [JSON-typvariabel](variable-in-aem-workflows.md).

* **[!UICONTROL Service]**: Lista över tjänster som den valda FDM (Form Data Model) tillhandahåller.
* **[!UICONTROL Input for services]** > **[!UICONTROL Provide input data using literal, variable, or workflow metadata, and a JSON file]**: En tjänst kan ha flera argument. Välj alternativet för att hämta värdet för tjänstargumenten från en metadataegenskap för arbetsflöde, ett JSON-objekt, en variabel eller ange värdet direkt i textrutan:

   * **[!UICONTROL Literal]**: Använd alternativet när du känner till det exakta värdet som ska anges. Exempel: srose@we.info.
   * **[!UICONTROL Variable]**: Använd alternativet för att hämta värdet som lagras i en variabel.
   * **[!UICONTROL Retrieve from Workflow Metadata]**: Använd alternativet när värdet som ska användas sparas i en metadataegenskap för arbetsflöde. Till exempel emailAddress.

   * **[!UICONTROL Relative to Payload]**: Använd alternativet för att hämta den bifogade filen som har sparats på en sökväg i förhållande till nyttolasten. Markera alternativet och ange antingen mappnamnet som innehåller den bifogade filen eller ange namnet på den bifogade filen i textrutan.

     Om till exempel mappen Relativt till nyttolast i CRX-databasen innehåller en bifogad fil på platsen `attachment\attachment-folder` anger du `attachment\attachment-folder` i textrutan efter att du har valt alternativet **[!UICONTROL Relative to Payload]**.

   * **[!UICONTROL JSON Dot Notation]**: Använd alternativet när värdet som ska användas finns i en JSON-fil. Till exempel försäkring.customerDetails.emailAddress. Alternativet JSON-punktnotation är bara tillgängligt om du har valt kartinmatningsfält från alternativet JSON för inmatning.
   * **[!UICONTROL Map input fields from input JSON]**: Ange sökvägen till en JSON-fil för att hämta indatavärdet för vissa tjänstargument från JSON-filen. Sökvägen till JSON-filen kan vara relativ till nyttolasten, en absolut sökväg eller så kan du välja ett JSON-inmatningsdokument med variabeln JSON eller Form Data Model (FDM).

* **[!UICONTROL Input for services]** > **[!UICONTROL Provide input data using variable or a JSON file]**: Välj alternativet för att hämta värden för alla argument från en JSON-fil som har sparats med en absolut sökväg, med en sökväg som är relativ till nyttolasten eller i en variabel.
* **[!UICONTROL Select Input JSON document using]**: JSON-filen innehåller värden för alla tjänstargument. JSON-filens sökväg kan vara **[!UICONTROL relative to the payload]** eller **[!UICONTROL absolute path]**. Du kan också hämta JSON-indata med hjälp av en variabel av datatypen JSON eller Form Data Model (FDM).

* **[!UICONTROL JSON Dot Notation]**: Lämna fältet tomt om du vill använda alla objekt i den angivna JSON-filen som indata för tjänstargument. Om du vill läsa ett specifikt JSON-objekt från den angivna JSON-filen som indata för serviceargument anger du punktnotation för JSON-objektet, till exempel, om du har en JSON som liknar den som anges i början av avsnittet, anger du försäkring.customerDetails för att ge all information om en kund som indata till tjänsten.
* **[!UICONTROL Output of service]** > **[!UICONTROL Map and write output values to variable or metadata]**: Välj alternativet att spara utdatavärdena som egenskaper för arbetsflödesinstansens metadatanod i crx-databasen. Ange namnet på metadataegenskapen och välj det motsvarande tjänstutdataattribut som ska mappas med metadataegenskapen, till exempel mappa det telefonnummer som returneras av utdatatjänsten med egenskapen phone_number för arbetsflödets metadata. På samma sätt kan du lagra utdata i en variabel med datatypen Long. När du väljer en egenskap för alternativet **[!UICONTROL Service output attribute to be mapped]** fylls endast variabler som kan lagra data för den valda egenskapen i för alternativet **[!UICONTROL Save the output to]**.

* **[!UICONTROL Output of service]** > **[!UICONTROL Save output to variable or a JSON file]**: Välj alternativet att spara utdatavärdena i en JSON-fil med en absolut sökväg, med en sökväg som är relativ till nyttolasten eller i en variabel.
* **[!UICONTROL Save Output JSON document using below options]**: Spara JSON-utdatafilen. Sökvägen till JSON-utdatafilen kan vara relativ till nyttolasten eller en absolut sökväg. Du kan också spara JSON-utdatafilen med en variabel av datatypen JSON eller Form Data Model (FDM).



## Underteckna dokumentsteg {#sign-document-step}

Med steget Signera dokument kan du använda [!DNL Adobe Sign] för att signera dokument. När du använder arbetsflödessteget [!DNL Adobe Sign] för att signera ett anpassat formulär, kan formuläret skickas mellan mottagare i taget eller skickas till alla mottagare samtidigt, beroende på arbetsflödesstegets konfiguration. [!DNL Adobe Sign]-aktiverade adaptiva Forms skickas till Experience Manager Forms Server först när alla mottagare har slutfört signeringsprocessen.

Som standard kontrollerar tjänsten [!DNL Adobe Sign] Scheduler (enkäter) mottagarens svar efter var 24:e timme. Du kan [ändra standardintervallet för din miljö](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status).

Stegen Signera dokument har följande egenskaper:

* **[!UICONTROL Agreement Name]**: Ange avtalets namn. Avtalsnamnet blir en del av ämnet och brödtexten i det e-postmeddelande som skickas till signerarna. Du kan antingen lagra namnet i en variabel av datatypen String eller välja **[!UICONTROL Literal]** om du vill lägga till namnet manuellt.

* **[!UICONTROL Locale]**: Ange språk för alternativen för e-post och verifiering. Du kan antingen lagra språkinställningen i en variabel av datatypen String eller välja **[!UICONTROL Literal]** för att välja språkinställningen i listan med tillgängliga alternativ. Du måste definiera språkkoden medan du lagrar värdet för språkinställningen i en variabel. Ange till exempel **[!UICONTROL en_US]** för engelska och **[!UICONTROL fr_FR]** för franska.

* **[!UICONTROL Adobe Sign Cloud Configuration]**: Välj en [!DNL Adobe Sign] molnkonfiguration. Om du inte har konfigurerat [!DNL Adobe Sign] för [!DNL AEM Forms] läser du [Integrera Adobe Sign med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Select Document to be signed using]**: Du kan välja ett dokument från en plats som är relativ till nyttolasten, använda nyttolasten som dokument, ange en absolut sökväg för dokumentet eller hämta dokumentet som lagras i en variabel av dokumentdatatypen.
* **[!UICONTROL Days Until Deadline]**: Ett dokument markeras som förfallet (passerat tidsgräns) efter det att aktiviteten inte har någon aktivitet för det antal dagar som anges i fältet **[!UICONTROL Days Until Deadline]**. Antalet dagar räknas efter att dokumentationen har tilldelats en användare för signering.
* **[!UICONTROL Reminder Email Frequency]**: Du kan skicka en påminnelse via e-post varje dag eller vecka. Veckan räknas från den dag som dokumentationen tilldelas en användare för signering.
* **[!UICONTROL Signature Process]**: Du kan välja att signera ett dokument i en sekventiell eller parallell ordning. I sekventiell ordning tar en signerare emot dokumentet i taget för signering. När den första signeraren har slutfört signeringen av dokumentet skickas dokumentet till den andra signeraren och så vidare. Flera signerare kan signera ett dokument samtidigt i parallell ordning.
* **[!UICONTROL Redirection URL]**: Ange en URL för omdirigering. När dokumentet har signerats kan du dirigera om den som tilldelats till en URL. Oftast innehåller denna URL ett tackmeddelande eller ytterligare instruktioner.
* **[!UICONTROL Workflow Stage]**: Ett arbetsflöde kan ha flera steg. Dessa steg visas i AEM Inbox. Du kan definiera dessa steg i modellens egenskaper ( **[!UICONTROL Sidekick]** > **[!UICONTROL Page]** > **[!UICONTROL Page Properties]** > **[!UICONTROL Stages]**).
* **[!UICONTROL Select Recipients]**: Ange metoden för att välja mottagare för dokumentet. Du kan dynamiskt tilldela arbetsflödet till en användare eller en grupp eller manuellt lägga till information om en mottagare. När du väljer Manuellt i listrutan lägger du till mottagarinformation som e-post, roll och autentiseringsmetod.

  >[!NOTE]
  >
  >* I rollavsnittet kan du ange mottagarrollen som signerare, godkännare, godkännare, certifierad mottagare, formulärifyllare och delegerande.
  >* Om du väljer Delegerande i alternativet Roll kan delegeraren tilldela signeringsaktiviteten till en annan mottagare.
  >* Om du har konfigurerat en autentiseringsmetod för [!DNL Adobe Sign], baserat på din konfiguration, väljer du en autentiseringsmetod som telefonbaserad autentisering, social identitet, kunskapsbaserad autentisering, myndighetsidentitetsbaserad autentisering.

* **[!UICONTROL Script or service to select recipients]**: Alternativet är bara tillgängligt om du väljer alternativet Dynamiskt i fältet Välj mottagare. Du kan ange ett ECMAScript eller en tjänst för att välja signerare och verifieringsalternativ för ett dokument.
* **[!UICONTROL Recipient Details]**: Alternativet är bara tillgängligt om alternativet Manuellt är markerat i fältet Välj mottagare. Ange en e-postadress och välj en valfri verifieringsmekanism. Innan du väljer en verifieringsmekanism i två steg ska du kontrollera att motsvarande verifieringsalternativ är aktiverat för det konfigurerade [!DNL Adobe Sign]-kontot. Du kan använda en variabel av datatypen String för att definiera värden för fälten E-post, Landskod och Telefonnummer. Fälten Landskod och Telefonnummer visas bara om du väljer Telefonverifiering i den 2-stegsvisa verifieringslistan.
* **[!UICONTROL Signed Document]**: Du kan spara statusen för det signerade dokumentet till Variabel. Om du vill lägga till en elektronisk signaturgranskningsversion för att öka säkerheten och lagligheten i det signerade dokumentet kan du inkludera revideringsrapport. Du kan spara det signerade dokumentet med hjälp av variabeln eller nyttolastmappen.

  >[!NOTE]
  >
  > Revideringsrapporten läggs till den sista sidan i det signerade dokumentet.

<!--
## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).
 
### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## Generera utskriftssteg {#generatePrintedOutput}

Steget genererar ett PCL-, PostScript-, ZPL-, IPL-, TPCL- eller DPL-utdata som genereras av en formulärdesign och datafil. Datafilen sammanfogas med formulärdesignen och formateras för utskrift. De utdata som genereras i det här steget kan skickas direkt till en skrivare eller sparas som en fil. Vi rekommenderar att du använder det här steget när du vill använda formulärdesigner eller data från ett program. Om formulärdesignerna finns i nätverket, det lokala filsystemet eller på HTTP-platsen använder du åtgärden generatePrintedOutput.

Programmet kräver till exempel att du sammanfogar en formulärdesign med en datafil. Informationen innehåller hundratals poster. Dessutom krävs att utdata skickas till en skrivare som stöder ZPL. Formulärdesignen och dina indata finns i ett program. Använd åtgärden generatePrintedOutput för att sammanfoga varje post med en formulärdesign och skicka utdata till en skrivare som stöder ZPL.

Stegen Generera utskrift har följande egenskaper:

**[!UICONTROL Input properties]**

* **[!UICONTROL Select template file using]**: Ange sökvägen för mallfilen. Du kan välja mallfilen med hjälp av sökvägen som är relativ till nyttolasten, sparad med en absolut sökväg eller med hjälp av en variabel av datatypen Dokument. Exempel: [Payload_Directory]/Workflow/data.xml. Om sökvägen inte finns i crx-databasen kan en administratör skapa sökvägen innan den används. Dessutom kan du acceptera nyttolasten som indatafil.

* **[!UICONTROL Select data document using]**: Ange sökvägen till en indatafil. Du kan markera indatafilen med den sökväg som är relativ till nyttolasten, som har sparats med en absolut sökväg eller med en variabel av dokumentdatatypen. Exempel: [Payload_Directory]/Workflow/data.xml. Om sökvägen inte finns i crx-databasen kan en administratör skapa sökvägen innan den används.

* **[!UICONTROL Printer Format]**: Ett värde för utskriftsformat som anger vilket sidbeskrivningsspråk som ska användas när ingen XDC-fil anges för att generera utdataströmmen. Om du anger ett literalt värde väljer du något av följande värden:

   * **[!UICONTROL color PCL]**: Använd alternativet för att ange en XDC-fil för PCL.
   * **[!UICONTROL Generic PostScript]**: Använd alternativet för att ange en allmän XDC-fil för PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: Använd ZPL 300 DPI. Zpl300.xdc används.
   * **[!UICONTROL ZPL 600 DPI]**: Använd ZPL 600 DPI. Filen zpl600.xdc används.
   * **[!UICONTROL IPL 300 DPI]**: Använd IPL 300 DPI. ipl300.xdc används.
   * **[!UICONTROL IPL 400 DPI]**: Använd IPL 400 DPI. Filen ipl400.xdc används.
   * **[!UICONTROL TPCL 600 DPI]**: Använd TPCL 600 DPI. Filen tpcl600.xdc används.
   * **[!UICONTROL PostScript Plain]**: Använd alternativet för att ange en XDC-fil med oformaterad text för PostScript.
   * **[!UICONTROL DPL300DPI]**: Använd DPL 300 DPI. dpl300.xdc används.
   * **[!UICONTROL DPL400DPI]**: Använd DPL 400 DPI. dpl400.xdc används.
   * **[!UICONTROL DPL600DPI]**: Använd DPL 600 DPI. dpl600.xdc används.
   * **[!UICONTROL HP_PCL_5e]**: Använd alternativet för att stödja flera Canon-enheter.


**[!UICONTROL Output Properties]**

* **[!UICONTROL Save output document using]**: Ange platsen där utdatafilen ska sparas. Du kan spara utdatafilen på en plats som är relativ till nyttolasten, i en variabel eller ange en absolut plats att spara utdatafilen på. Om sökvägen inte finns i crx-databasen kan en administratör skapa sökvägen innan den används.

**[!UICONTROL Advanced Properties]**

* **[!UICONTROL Select Content Root location using]**: Innehållsroten är ett strängvärde som anger URI, absolut referens eller plats i databasen för att hämta relativa resurser som används i formulärdesignen. Om formulärdesignen till exempel refererar till en bild relativt, som `../myImage.gif`, måste `myImage.gif` vara vid `repository://`. Standardvärdet är `repository://`, vilket pekar på databasens rotnivå.

  När du väljer en resurs från ditt program måste innehållsrots-URI-sökvägen ha rätt struktur. Om ett formulär till exempel hämtas från ett program med namnet SampleApp och placeras på `SampleApp/1.0/forms/Test.xdp` måste innehållets rot-URI anges som `repository://administrator@password/Applications/SampleApp/1.0/forms/` eller `repository:/Applications/SampleApp/1.0/forms/` (när behörigheten är null). När innehållets rot-URI anges på det här sättet matchas sökvägarna för alla refererade resurser i formuläret mot denna URI.

* **[!UICONTROL Select XCI file using]**: XCI-filer används för att beskriva teckensnitt och andra egenskaper som används för formulärdesignelement. Du kan behålla en XCI-fil i förhållande till nyttolasten, på en absolut sökväg eller med en variabel av dokumentdatatypen.

* **[!UICONTROL Locale]**: Anger vilket språk som ska användas för att generera PDF-dokumentet. Om du anger ett literalt värde väljer du ett språk i listan eller något av dessa värden:
   * **[!UICONTROL To use server default]**:
(Standard) Använd språkinställningen som är konfigurerad på [!DNL AEM Forms] -servern. Inställningen Språk konfigureras med administrationskonsolen. (Se [Hjälp om Designer](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL To use custom value]**:
Skriv språkkoden i den litterala rutan eller välj en strängvariabel som innehåller språkkoden. En fullständig lista över språkkoder som stöds finns på https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copies]**: Ett heltalsvärde som anger antalet kopior som ska genereras för utdata. Standardvärdet är 1.

* **[!UICONTROL Duplex Printing]**: Ett sidnumreringsvärde som anger om dubbelsidig utskrift eller enkelsidig utskrift ska användas. Skrivare som stöder PostScript och PCL använder det här värdet. Om du anger ett literalt värde väljer du något av följande värden:
   * **[!UICONTROL Duplex Long Edge]**: Använd dubbelsidig utskrift och utskrift med hjälp av sidnumrering med lång kant.
   * **[!UICONTROL Duplex Short Edge]**: Använd dubbelsidig utskrift och utskrift med hjälp av kortkantssidnumrering.
   * **[!UICONTROL Simplex]**: Använd enkelsidig utskrift.

## Generera icke-interaktiva PDF Output step   {#generatePDFdocuments}

1. Dra arbetsflödet Generera icke-interaktiva PDF Output under fliken Forms Workflow i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, utdatadokument och ytterligare parametrar i dialogrutan Redigera komponent och klicka sedan på **[!UICONTROL OK]**.

### Indatadokument {#input-documents-3}

* **Mallfil**: Anger platsen för XDP-mallen. Det är ett obligatoriskt fält.

* **Datadokument**: Anger platsen för XML-data som måste sammanfogas med mallen.

### Utdatadokument {#output-document}

**Utdatadokument**: Anger namnet på det genererade PDF-formuläret.

### Ytterligare parametrar {#additional-parameters-1}

* **Innehållsrot**: Anger sökvägen till mappen i databasen där fragment eller bilder som används i XDP-indatamallen lagras.
* **Språk**: Anger standardspråk för genererat PDF-formulär.
* **Acrobat Version**: Anger målversionen för Acrobat för det genererade PDF-formuläret.
* **Linjär PDF**: Anger om den genererade PDF ska optimeras för webbvisning.
* **Taggad PDF**: Anger om den genererade PDF-filen ska vara tillgänglig.
* **XCI-dokument**: Anger sökvägen till XCI-filen.

## Se även {#see-also}

* [Variabler i Forms-centrerade AEM-arbetsflöden](/help/forms/variable-in-aem-workflows.md)
* [Konfigurera frånvaroinställningar](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->