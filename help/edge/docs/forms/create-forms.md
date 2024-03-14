---
title: Komma igång med AEM Forms Edge Delivery Service. Skapa ett formulär.
description: Skapa perfekta formulär, snabbt! ⚡ AEM Forms Edge Delivery, dokumentbaserad framtagning = blixtsnabb och SEO-anpassade formulär för nöjdare användare och sökmotorer.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: f4cf79e2cd71a390741987cfcf034e6eed02432d
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Skapa ett formulär med Adaptiv Forms Block

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

AEM Forms Edge Delivery innehåller ett block, Adaptive Forms Block, som gör det enkelt att skapa formulär för inhämtning och lagring av inhämtade data. Du kan [skapa ett nytt AEM projekt förkonfigurerat med Adaptive Forms Block](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) eller [lägga till det adaptiva Forms-blocket i ett befintligt AEM](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft SharePoint för att enkelt bearbeta inlämnade data eller starta ett befintligt arbetsflöde.

![Dokumentbaserat redigeringssystem](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## Förutsättningar

Kontrollera att du har utfört följande steg innan du börjar:

* Konfigurera en [AEM projekt med AEM Forms standardmall](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) eller [har lagt till Adaptive Forms Block i ditt befintliga AEM](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) och klona motsvarande GitHub-databas på din lokala dator.
I det här dokumentet kallas den lokala mappen i ditt Edge Delivery Services-projekt (EDS) `[EDS Project repository]`.
* Se till att du har tillgång till Google Sheets eller Microsoft SharePoint. Information om hur du konfigurerar Microsoft SharePoint som innehållskälla finns i [Så här använder du SharePoint](https://www.aem.live/docs/setup-customer-SharePoint).



## Skapa ett formulär

<!-- 

+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
1. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

1. on your local machine and copy the `form` folder. 
1. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

* **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

* **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project.

+++

-->

+++ Steg 1: Skapa ett formulär med Microsoft Excel eller Google Sheet.

Istället för att navigera i komplexa processer kan du enkelt skapa ett formulär med hjälp av ett kalkylblad. Du kan definiera de rader och kolumner som ska utgöra formulärstrukturen. Varje rad representerar en individ [formulärfält](/help/edge/docs/forms/form-components.md#available-components) och kolumnrubrikerna definierar motsvarande [fältegenskaper](/help/edge/docs/forms/form-components.md#components-properties).

Ta till exempel följande kalkylblad, där rader ger konturfält för ett `enquiry` formulär- och kolumnrubriker definierar deras egenskaper:

![Kalkylblad för förfrågan](/help/edge/assets/enquiry-form-spreadsheet.png)

Så här fortsätter du med att skapa formulär:

1. Gå till projektmappen AEM Edge Delivery på Microsoft SharePoint eller Google Drive.

1. Skapa en Microsoft Excel-arbetsbok eller ett Google-blad var som helst i AEM Edge Delivery-projektkatalog. Skapa till exempel ett kalkylblad med namnet `enquiry` på AEM Edge Delivery-projektkatalog på Google Drive.

   ![Exempelinnehåll på Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

1. Se till att bladet delas med rätt AEM (till exempel `helix@adobe.com`) [enligt de konfigurationer som har angetts för ditt projekt](https://www.aem.live/docs/setup-customer-SharePoint). Ge användaren redigeringsbehörighet för bladet.

1. Öppna det skapade kalkylbladet och ändra standardbladets namn till &quot;shared-default&quot;.

   ![ändra namn på standardblad till &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Om du vill lägga till formulärfälten infogar du rader och kolumnrubriker i bladet&quot;shared-default&quot;. Varje rad ska representera en [formulärfält](/help/edge/docs/forms/form-components.md#available-components), med kolumnrubriker som definierar motsvarande fält [egenskaper](/help/edge/docs/forms/form-components.md#components-properties).


   För att komma igång snabbt bör du överväga att kopiera innehållet i [Kalkylblad för förfrågan](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) i kalkylbladet. När du har kopierat innehållet sparar du kalkylbladet.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) om du vill förhandsgranska bladet.

   ![Använd AEM Sidekick för att förhandsgranska bladet](/help/edge/assets/preview-form.png)

   När du förhandsgranskar visas bladets innehåll i JSON-format på nya webbläsarflikar. Se till att du hämtar förhandsgransknings-URL:en eftersom detta krävs för att återge formuläret i nästa avsnitt. URL-formatet är följande:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` refererar till grenen i din GitHub-databas.
   * `<repository>` anger din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.

   Om projektets databas till exempel heter &quot;portal&quot;, finns den under kontot &quot;wkndforms&quot; och du använder huvudgrenen, ser URL:en ut så här:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ Steg 2: Förhandsgranska formuläret på EDS-sidan (Edge Delivery Services).


Till nu har du förberett formulärets struktur. Nu kan du förhandsgranska formuläret:

1. Öppna ditt Microsoft SharePoint- eller Google Drive-konto och gå till AEM Edge Delivery-projektkatalog.



1. Öppna en dokumentfil (t.ex. en indexfil) om du vill bädda in formuläret. Du kan också skapa ett nytt dokument.

1. Gå till önskad plats i dokumentet där du vill lägga till formuläret.

1. Skapa ett formulärblock som återger formuläret. Välj Infoga > Tabell och skapa en kolumn, en tabell med två rader. Ge tabellen namnet &quot;Formulär&quot; och klistra in URL:en för förhandsgranskning på den andra raden. Kontrollera att URL-adressen är formaterad som en hyperlänk, inte som oformaterad text, enligt bilden nedan:

   | Formulär |
   |---|
   | [https://main—weFinance—wkndforms.hlx.live/inquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |


   ![Lägg till adaptivt Forms-block på din webbsida](/help/edge/assets/add-adaptive-forms-block.png)

   Det här blocket fungerar som en platshållare där formuläret är inbäddat. Lägg till förhandsgransknings-URL:en på blockets andra rad `<form>.json` som en hyperlänk.

   >[!IMPORTANT]
   >
   >
   > Kontrollera att URL-adressen är formaterad som en hyperlänk i stället för att visas som oformaterad text.


1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) om du vill förhandsgranska dokumentet. Formuläret visas nu på sidan. Här är till exempel formuläret baserat på [frågekalkylblad](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Ett exempel på ett EDS-formulär](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Fyll i formuläret och klicka på skicka-knappen. Ett fel visas, ungefär som följande, eftersom kalkylbladet inte är inställt på att acceptera data än.

   ![fel vid inlämning av formulär](/help/edge/assets/form-error.png)

+++


## Nästa steg

[Förbered kalkylbladet](/help/edge/docs/forms/submit-forms.md) för att börja ta emot data när formulär skickas in.


## Se även

{{see-more-forms-eds}}
