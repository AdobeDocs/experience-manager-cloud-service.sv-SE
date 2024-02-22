---
title: Komma igång med AEM Forms Edge Delivery Service
description: Skapa perfekta formulär, snabbt! ⚡ AEM Forms Edge Delivery, dokumentbaserad framtagning = blixtsnabb och SEO-anpassade formulär för nöjdare användare och sökmotorer.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# Skapa ett formulär för AEM Forms Edge Delivery Service

I dagens digitala samhälle är det viktigt för alla företag att skapa användarvänliga formulär. Med AEM Forms Edge Delivery kan du skapa formulär med välbekanta verktyg som Word eller Google Docs.

Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft Sharepoint för att enkelt bearbeta inskickade data eller starta ett befintligt arbetsflöde.


## Förutsättningar

Kontrollera att du har utfört följande steg innan du börjar:

* Konfigurera och klona EDS-projektet (Edge Delivery Service). Se [självstudiekurs för utvecklare](https://www.aem.live/developer/tutorial) för mer information. Den lokala mappen i Edge Delivery Service-projektet (EDS) refereras som `[EDS Project repository]` i det här dokumentet.
* Klona [Forms Block-arkiv](https://github.com/adobe/afb). Den innehåller koden som återger formuläret på en EDS-webbsida. Den lokala mappen i Forms Block-databasen refereras som `[Forms Block repository]` i det här dokumentet.
* Se till att du har tillgång till Google Sheets eller Microsoft SharePoint.


## Skapa ett formulär

+++ Steg 1: Lägg till formulärblocket i Edge Delivery Service-projektet (EDS).

AEM Forms Edge Delivery innehåller ett formulärblock som hjälper dig att enkelt skapa formulär för att hämta in och lagra inhämtade data. Så här inkluderar du formulärblocket i ditt Edge Delivery Service-projekt:

1. Navigera till `[Forms Block repository]/blocks` och kopiera `forms` mapp.

1. Navigera till `[EDS Project repository]/blocks/` och klistra in `forms` mapp.

   >[!VIDEO](https://video.tv.adobe.com/v/3427487?quality=12&learn=on)

1. Checka in `form` mapp och underliggande filer till Edge Delivery Service-projektet på GitHub.

   Formulärblocket läggs till i din EDS-projektdatabas på Github. Kontrollera att Github-bygget inte misslyckas:

   * Om du får felmeddelandet&quot;Det går inte att matcha sökvägen till modulen &quot;&#39;../../scripts/lib-franklin.js&#39;&quot; öppnar du `[EDS Project]/blocks/forms/form.js` -fil. Ersätt `lib-franklin.js` filen med `aem.js` -fil.

   * Om du råkar ut för några lintingfel kan du ignorera dem. Öppna `[EDS Project]\package.json` och uppdatera lint-skriptet från `"lint": "npm run lint:js && npm run lint:css"` till `"lint": "echo 'skipping linting for now'"`. Spara filen och implementera den i ditt GitHub-projekt.

Nu kan du skapa ett formulär och lägga till det på webbplatsen.

+++

+++ Steg 2: Skapa ett formulär med Microsoft Excel eller Google Sheet.

I stället för komplexa processer kan du enkelt skapa ett formulär med hjälp av ett kalkylblad. Du kan börja med att lägga till rader och kolumnrubriker i ett kalkylblad, där varje rad definierar ett formulärfält och varje kolumnrubrik definierar egenskaperna för motsvarande formulärfält.

I följande kalkylblad definierar t.ex. rader fälten för `contact us` form- och kolumnrubriken definierar egenskaperna för motsvarande fält.

![kontakta oss, kalkylblad](/help/edge/assets/contact-us-form-spreadsheet.png)

Så här skapar du ett formulär:

1. Öppna projektmappen AEM Edge Delivery i Microsoft SharePoint eller Google Drive.

1. Skapa en Microsoft Excel-arbetsbok eller ett Google-blad var som helst i projektkatalogen AEM Edge Delivery. Skapa till exempel ett kalkylblad med namnet `contact-us` på AEM Edge Delivery-projektkatalog på Google Drive.

1. Se till att bladet delas med AEM användare (till exempel `helix@adobe.com`) [konfigurerad för ditt projekt](https://www.aem.live/docs/setup-customer-sharepoint) och användaren har redigeringsbehörighet för bladet.

1. Öppna det kalkylblad som du har skapat och ändra namnet på standardbladet till &quot;shared-default&quot;.

   ![ändra namn på standardblad till &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Om du vill lägga till fälten i formuläret lägger du till raderna och kolumnrubrikerna i `shared-default` blad, där varje rad definierar ett formulärfält och varje kolumnrubrik definierar [egenskaper](/help/edge/docs/forms/eds-form-field-properties)) för motsvarande formulärfält.

   Om du snabbt vill börja kopierar du innehållet i [kontakta oss, kalkylblad](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) i kalkylbladet.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera bladet.

   ![Använd AEM Sidekick för att förhandsgranska och publicera bladet](/help/edge/assets/preview-form.png)

   Vid förhandsgranskning och publicering öppnas nya flikar i webbläsaren som visar bladets innehåll i JSON-format. Observera att live-URL:en är nödvändig för att återge formuläret senare.

   URL-formatet är:

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ Steg 3: Förhandsgranska formuläret på EDS-sidan (Edge Delivery Service).


Fram tills nu har du lagt till formulärblocket i EDS-projektet och förberett formulärets struktur. Nu kan du förhandsgranska formuläret:

1. Gå till ditt Microsoft SharePoint- eller Google Drive-konto och öppna AEM Edge Delivery-projektkatalog.

1. Öppna en dokumentfil för att bädda in formuläret i den. Öppna till exempel indexfilen. Du kan också skapa en ny dokumentfil.

1. Navigera till önskad plats i dokumentet där du vill lägga till formuläret.

1. Lägg till ett block med namnet &#39;Form&#39; i filen, liknande det som visas nedan.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   På den andra raden tar du med den URL som du registrerade i föregående avsnitt som hyperlänk. Använd URL:en för förhandsgranskning (.page URL) för utvecklings- eller teständamål, eller publicerings-URL:en (.live) för produktion.

   >[!IMPORTANT]
   >
   >
   > Kontrollera att URL-adressen är hyperlänkad i stället för att visas som oformaterad text.


1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska sidan. Formuläret visas nu på sidan.

   Här är till exempel formuläret baserat på [kontakta oss, kalkylblad](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![Ett exempel på ett EDS-formulär](/help/edge/assets/eds-form.png)

   Fyll i formuläret och klicka på skicka-knappen. Ett fel visas, ungefär som följande, eftersom kalkylbladet inte är inställt på att acceptera data än.

   ![fel vid inlämning av formulär](/help/edge/assets/form-error.png)

+++


## Nästa steg

[Förbered kalkylbladet](/help/edge/docs/forms/submit-forms.md) för att börja ta emot data när formulär skickas in.



## Se mer

* [Egenskaper för formulärfält](/help/edge/docs/forms/eds-form-field-properties)
* [Skapa och förhandsgranska ett formulär](/help/edge/docs/forms/create-forms.md)
* [Aktivera formulär för att skicka data](/help/edge/docs/forms/submit-forms.md)
* [Publicera ett formulär på webbplatssidan](/help/edge/docs/forms/publish-eds-forms.md)
* [Lägga till valideringar i formulärfält](/help/edge/docs/forms/validate-forms.md)
* [Ändra teman och format för formulär](/help/edge/docs/forms/style-theme-forms.md)
