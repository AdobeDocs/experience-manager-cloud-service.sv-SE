---
title: Komma igång med AEM Forms Edge Delivery Service. Skapa ett formulär.
description: Skapa perfekta formulär, snabbt! ⚡ AEM Forms Edge Delivery, dokumentbaserad framtagning = blixtsnabb och SEO-anpassade formulär för nöjdare användare och sökmotorer.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Skapa ett formulär med adaptivt formulärblock

I dagens digitala samhälle är det viktigt för alla företag att skapa användarvänliga formulär. Med AEM Forms Edge Delivery kan du skapa formulär med välbekanta verktyg som Word eller Google Docs.

Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft Sharepoint för att enkelt bearbeta inskickade data eller starta ett befintligt arbetsflöde.

![Dokumentbaserat redigeringssystem](/help/edge/assets/document-based-authoring-workflow-create-form.png)

AEM Forms Edge Delivery innehåller ett block, som kallas adaptivt formulärblock, som hjälper dig att enkelt skapa formulär för att hämta in och lagra inhämtade data. Du kan inkludera det adaptiva formulärblocket i ditt AEM EDS-projekt för att börja skapa ett formulär. Låt oss börja:


## Förutsättningar

Kontrollera att du har utfört följande steg innan du börjar:

* Konfigurera Edge Delivery Services (EDS) i GitHub-projekt med hjälp AEM standardmall och klona motsvarande GitHub-databas på den lokala datorn. Se [självstudiekurs för utvecklare](https://www.aem.live/developer/tutorial) för mer information. I det här dokumentet kallas den lokala mappen i ditt Edge Delivery Services-projekt (EDS) `[EDS Project repository]` .
* Se till att du har tillgång till Google Sheets eller Microsoft SharePoint. Information om hur du konfigurerar Microsoft SharePoint som innehållskälla finns i [Så här använder du Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## Skapa ett formulär

+++ Steg 1: Lägg till det adaptiva formulärblocket i Edge Delivery Services-projektet.

Adaptiv ger användarna möjlighet att skapa formulär för en Edge Delivery ServicesSite. Det här blocket ingår dock inte i AEM standardmallsida (används för att skapa ett projekt för Edge Delivery Services). Så här integrerar du det adaptiva formulärblocket i ditt Edge Delivery Services-projekt:

1. **Klona databasen för adaptiva formulärblock**: Klona [Databas för adaptiva formulärblock](https://github.com/adobe-rnd/form-block) på din lokala dator. Den innehåller koden som återger formuläret på en EDS-webbsida. I det här dokumentet kallas den lokala mappen i din Forms-blockdatabas för `[Adaptive Form Block repository]`.
1. **Leta reda på databasen för adaptiva formulärblock:** Öppna [Databas för adaptiva formulärblock]/blocks/src-mapp och kopiera dess innehåll.

1. på din lokala dator och kopiera `form` mapp.
1. **Klistra in koden för det adaptiva formulärblocket i ditt EDS-projekt:**
Navigera till [EDS-projektdatabas]/blocks/ mapp på den lokala datorn och skapa en &#39;form&#39;-mapp. Klistra in `[Adaptive Form Block repository]/blocks/src content`, kopierat i föregående steg till `[EDS Project repository]/blocks/form` mapp.
1. **Verkställ ändringar i GitHub:** Checka in `[EDS Project repository]/blocks/form` -mappen och dess underliggande filer till ditt Edge Delivery Services-projekt på GitHub.

När du har utfört de här stegen läggs det adaptiva formulärblocket till i projektdatabasen för Edge Delivery Services (EDS) på GitHub. Nu kan du skapa och lägga till formulär på en EDS-sida.


**Felsökning av byggproblem med GitHub**

Se till att GitHub-byggprocessen blir smidig genom att åtgärda potentiella problem:

* **Lösning av modulsökvägsfel:**
Om du får felmeddelandet&quot;Det går inte att matcha sökvägen till modulen &quot;&#39;../../scripts/lib-franklin.js&#39;&quot; går du till [EDS-projekt]/blocks/forms/form.js fil. Uppdatera importsatsen genom att ersätta filen lib-franklin.js med filen aem.js.

* **Hantera lintingfel:**
Om du skulle stöta på ett lintingfel kan du kringgå dem. Öppna [EDS-projekt]/package.json och ändra &quot;lint&quot;-skriptet från &quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot; till &quot;lint&quot;: &quot;echo &#39;skipping linting for now&#39;&quot;. Spara filen och implementera ändringarna i GitHub-projektet.

+++

+++ Steg 2: Skapa ett formulär med Microsoft Excel eller Google Sheet.

Istället för att navigera i komplexa processer kan du enkelt skapa ett formulär med hjälp av ett kalkylblad. Du kan definiera de rader och kolumner som ska utgöra formulärstrukturen. Varje rad representerar en individ [formulärfält](/help/edge/docs/forms/form-components.md#available-components) och kolumnrubrikerna definierar motsvarande [fältegenskaper](/help/edge/docs/forms/form-components.md#components-properties).

Ta till exempel följande kalkylblad, där rader ger konturfält för ett `enquiry` formulär- och kolumnrubriker definierar deras egenskaper:

![Kalkylblad för förfrågan](/help/edge/assets/enquiry-form-spreadsheet.png)

Så här fortsätter du med att skapa formulär:

1. Gå till projektmappen AEM Edge Delivery på Microsoft SharePoint eller Google Drive.

1. Skapa en Microsoft Excel-arbetsbok eller ett Google-blad var som helst i AEM Edge Delivery-projektkatalog. Skapa till exempel ett kalkylblad med namnet `enquiry` på AEM Edge Delivery-projektkatalog på Google Drive.

1. Se till att bladet delas med rätt AEM (till exempel `helix@adobe.com`) [enligt de konfigurationer som har angetts för ditt projekt](https://www.aem.live/docs/setup-customer-sharepoint). Ge användaren redigeringsbehörighet för bladet.

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

+++ Steg 3: Förhandsgranska formuläret på EDS-sidan (Edge Delivery Services).


Fram tills nu har du lagt till det adaptiva formulärblocket i ditt EDS-projekt och förberett formulärets struktur. Nu kan du förhandsgranska formuläret:

1. **Åtkomst till din projektkatalog:** Öppna ditt Microsoft SharePoint- eller Google Drive-konto och gå till AEM Edge Delivery-projektkatalog.

1. **Bädda in formuläret i ett dokument:** Öppna en dokumentfil (t.ex. en indexfil) om du vill bädda in formuläret. Du kan också skapa ett nytt dokument.

1. **Navigera till önskad plats:** Gå till önskad plats i dokumentet där du vill lägga till formuläret.

1. **Lägg till det adaptiva formulärblocket:** Skapa ett formulärblock som återger formuläret. Välj Infoga > Tabell och skapa en kolumn, en tabell med två rader. Ge tabellen namnet &quot;Formulär&quot; och klistra in URL:en för förhandsgranskning på den andra raden. Kontrollera att URL-adressen är formaterad som en hyperlänk, inte som oformaterad text, enligt bilden nedan:

   | Formulär |
   |---|
   | [https://main—portal—wkndforms.hlx.live/inquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

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




