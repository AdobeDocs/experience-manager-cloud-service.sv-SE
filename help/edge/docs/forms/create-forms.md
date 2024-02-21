---
title: Komma igång med AEM Forms Edge Delivery Service
description: Skapa perfekta formulär, snabbt! ⚡ AEM Forms Edge Delivery, dokumentbaserad framtagning = blixtsnabb och SEO-anpassade formulär för nöjdare användare och sökmotorer.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Skapa ett formulär för AEM Forms Edge Delivery Service

I dagens digitala samhälle är det viktigt för alla företag att skapa användarvänliga formulär. Med AEM Forms Edge Delivery kan du skapa formulär med välbekanta verktyg som Word eller Google Docs.

Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft Sharepoint för att enkelt bearbeta inskickade data eller starta ett befintligt arbetsflöde.

## Förutsättningar

* Du har ett Github-konto.
* Du har tillgång till Google Sheets eller Microsoft SharePoint.
* Du förstår grunderna i Git, HTML, CSS och JavaScript.
* Du har installerat Node och NPM för lokal utveckling.

## Innan du börjar

* Konfigurera och klona ett EDS-projekt (Edge Delivery Service). Se [självstudiekurs för utvecklare](https://www.aem.live/developer/tutorial) för mer information.
* Klona [Forms Block-arkiv](https://github.com/adobe/afb). Den innehåller det formulärblock som behövs för att återge formuläret.

![Getting Started with Edge Delivery Forms](/help/edge/assets/getting-started-with-eds-forms.png)

## Lägg till formulärblocket i Edge Delivery Service-projektet (EDS) {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery innehåller ett formulärblock som hjälper dig att enkelt skapa formulär för att hämta in och lagra inhämtade data. Så här inkluderar du formulärblocket i ditt Edge Delivery Service-projekt:

1. Navigera till projektmappen Edge Delivery Service (EDS) i den lokala utvecklingsmiljön.


   ```Shell
   cd [EDS Project folder]
   ```

1. Skapa en mapp med namnet `form` under EDS-projektkatalogen. Till exempel, under katalogen för EDS-projektet med namnet `Portal`, skapa en mapp med namnet `form`.

   ```Shell
   mkdir form
   ```


1. Lägg till [Forms Block](https://github.com/adobe/afb/tree/main/blocks/form) till mappen &#39;form&#39;.

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. Checka in mappen &#39;form&#39; och underliggande filer i ditt Edge Delivery Service-projekt på GitHub.

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   Du kan nu återge ett EDS-formulär.

   >[!NOTE]
   >
   > * Om din pull-begäran/byggs upp av projekt misslyckas och du får ett fel som är relaterat till importen av `franklin-lib.js` uppdaterar du importsatsen så att den refererar till `aem.js` i stället för `franklin-lib.js` -fil.
   > * Om du råkar ut för några lintingfel kan du ignorera dem. Navigera till filen package.json och uppdatera lint-skriptet från om du vill kringgå lintingkontrollerna `"lint": "npm run lint:js && npm run lint:css"` till `"lint": "echo 'skipping linting for now'"`. Verkställ sedan ändringarna i filen package.json.

## Skapa ett formulär med Microsoft Excel eller Google Sheet {#create-a-form-for-an-eds-project}

Det kan vara praktiskt att låta webbutvecklare skapa formulär och välja vilken information som ska samlas in från webbplatsens besökare. Istället för komplexa processer kan man enkelt skapa blanketter med hjälp av ett kalkylblad. De måste lägga till rätt kolumnrubriker och sedan använda ett formulärblock för att visa det på webbplatsen utan krångel. Så här skapar du ett formulär:

1. Skapa en Microsoft Excel-arbetsbok eller ett Google-blad var som helst under AEM Edge Delivery-projektkatalog på Microsoft SharePoint eller Google Drive.

1. Se till att AEM användare (till exempel `helix@adobe.com`) som konfigurerats för ditt projekt har redigeringsbehörighet för bladet.

1. Öppna arbetsboken som du har skapat och ändra namnet på standardbladet till &quot;shared-default&quot;.

   ![ändra namn på standardblad till &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-helix-default.png)

1. Kopiera innehållet i [kontakta oss, kalkylblad](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) till ditt eget kalkylblad.

   ![kontakta oss, kalkylblad](/help/edge/assets/contact-us-form-spreadsheet.png)

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera bladet.

   Vid förhandsgranskning och publicering öppnas nya flikar i webbläsaren som visar bladets innehåll i JSON-format. Observera att live-URL:en är nödvändig för att återge formuläret senare.

   URL-formatet är:

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## Förhandsgranska formuläret på EDS-sidan (Edge Delivery Service) {#add-a-form-to-your-eds-page}

Fram tills nu har du aktiverat formulärblocket för ditt EDS-projekt och förberett formulärets struktur. Nu ska du ta med formuläret på din EDS-sida och återge det:

1. Gå till projektkatalogen AEM Edge Delivery på Microsoft SharePoint eller Google Drive.

1. Om du vill lägga till formuläret på en sida öppnar du motsvarande dokumentfil. Öppna till exempel indexfilen.

1. Navigera till önskad plats i dokumentet där du vill lägga till formuläret.

1. Lägg till ett block med namnet &#39;Form&#39; i filen, liknande det som visas nedan.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   På den andra raden tar du med den URL som du märkte i föregående avsnitt som en hyperlänk.

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera sidan. Formuläret återges.

   Här är till exempel formuläret baserat på [kontakta oss, kalkylblad](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![kontakta oss (EDS-formulär)](/help/edge/assets/eds-form.png)

   Formulärblocket återger formuläret, men det är inte klart att ta emot data än. När du klickar på skicka-knappen inträffar ett fel som liknar följande:

   ![fel vid inlämning av formulär](/help/edge/assets/form-error.png)

   [Förbered bladet för att ta emot data](/help/edge/docs/forms/submit-forms.md). Du kan skicka data till bladet när du förbereder dem för att ta emot data.


## Se mer

* [Skapa och förhandsgranska ett formulär](/help/edge/docs/forms/create-forms.md)
* [Aktivera formulär för att skicka data](/help/edge/docs/forms/submit-forms.md)
* [Publicera ett formulär på webbplatssidan](/help/edge/docs/forms/publish-eds-forms.md)
* [Lägga till valideringar i formulärfält](/help/edge/docs/forms/validate-forms.md)
* [Ändra teman och format för formulär](/help/edge/docs/forms/style-theme-forms.md)