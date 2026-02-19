---
title: Sammanhangsberoende experiment i AEM as a Cloud Service
description: Lär dig hur du använder plugin-programmet för experiment för att lägga till experimentella funktioner på din webbplats.
feature: Administering
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: 420f8d5e-27f9-4081-b174-b2d7752779f7
source-git-commit: ef20e6df5e19596ea742e6ac267b1f37b7517cfa
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 0%

---

# Sammanhangsberoende experiment i AEM as a Cloud Service {#contextual-experimentation}

>[!NOTE]
>För närvarande är funktionen för kontextexperiment bara tillgänglig via betaprogrammet. Kontakta antingen Adobe support eller din kontoansvarige för att få tillgång till betaprogrammet.

Experimentera är att testa webbplatsens design, funktioner och kod för att förbättra prestandan och göra webbplatsen effektivare och smidigare. Detta uppnås genom att ändra antingen innehåll eller funktionalitet, jämföra resultaten med en tidigare version och välja de förbättringar som har mätbara effekter.

När det görs på rätt sätt är det ett kraftfullt mönster för att förbättra konverteringar, engagemang och besökarupplevelse. I allmänhet finns det ett par saker du bör undvika när du vill använda metoden:

* **För lite**: De flesta företag experimenterar inte tillräckligt och när de gör det experimenterar de med för lite trafik för att få meningsfulla resultat.
* **För långsamt**: Många experimentramverk gör webbplatsen så långsam att de potentiella nya konverteringarna inte kan kompensera för den trafik som går förlorad och studsar på grund av långsam återgivning.
* **För komplex**: Om det tar för lång tid att konfigurera ett nytt experiment körs färre försök.

För webbplatser som körs på Adobe Experience Manager finns det ett **plugin-program för experiment** som gör att utvecklare kan lägga till en experimenteringsfunktion på sina webbplatser. Tre saker skiljer den här metoden från andra experimentmiljöer:

* Det är enkelt att konfigurera tester med de verktyg som författarna redan är bekanta med och ingen separat inloggning behövs.
* Den är nära integrerad i AEM leveranssystem, tar inte längre tid att leverera och är flexibel när det gäller kodändringar och innehåll.
* Det gör det möjligt att testa enkla innehållsändringar och experimentera med design, funktioner och kod.

## Innan du börjar {#before-start}

Plugin-programmet för experimenterande används i kontexten för [Edge Delivery Services](/help/edge/overview.md) så du behöver ett Github-konto, en innehållsdatabas som SharePoint eller Google Drive, och du behöver även [AEM Sidekick](https://www.aem.live/docs/sidekick). Se även självstudiekursen [Komma igång - Universal Editor Developer Tutorial ](https://www.aem.live/developer/tutorial) och [Getting Started - Developer Tutorial](https://www.aem.live/developer/tutorial).

När du har konfigurerat allt kan du **titta på den här videon** med titeln [Direktexperiment](https://business.adobe.com/products/experience-manager/sites/testing-optimization.html) för att få en kort demonstration om hur plugin-programmet för experiment fungerar.

## Vanliga termer {#frequently-used-terms}

Innan du följer resten av guiden för att konfigurera ditt första experiment finns det några vanliga termer som du bör känna till:

* **Kontroll**: upplevelsen innan experimentet körs. Alla experiment försöker testa och visa en förbättring av kontrollupplevelsen.
* **Challenger**: En upplevelse som skiljer sig från kontrollupplevelsen och som&quot;testas&quot; mot eller tillsammans med den.
* **Varianter**: Kontroller och utmanare är alla varianter av ett experiment.
* **Statistisk signifikans**: Utvärderar om utmanaren är bättre än kontrollen. Genom att beräkna statistisk signifikans kan ni utesluta otur och koncentrera er på resultaten som har en verklig effekt.

## Experimentera med varianter och allmänna arbetsflöden {#experiment-variants-workflow}

När du skapar ett experiment använder du i allmänhet en befintlig sida som kontrollsida. Sedan skapar du en utmanarsida som ersätter kontrollsidan för några av dina besökare. På utmanarsidan kan du testa olika saker som innehållsvarianter, olika sidlayouter, call-to-action (CTA) och så vidare. Du kan konfigurera dessa experimentella varianter genom att lägga till metadataparametrar på kontrollsidan (se nedan).

Tjänsten [Operational Telemetry ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) samlar sedan in data, till exempel antalet besökare på kontrollsidan jämfört med utmanarsidan. Sedan använder du dessa data för att välja de nödvändiga förbättringarna för din webbplats. Så länge du håller dig till det språk som webbplatsen är skriven på och använder den befintliga blockfunktionen bör du kunna skapa en experimentvariant och skicka den till produktion på några minuter.

>[!NOTE]
>Tänk på att plugin-programmet inte använder, och att det inte innehåller, några slutanvändardata som kan leda till att de identifieras. Inget slutanvändardeltagande eller cookie-samtycke krävs när standardkonfigurationen som använder tjänsten [Operational Telemetry i AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) används.

### Experimentera-ID {#experiment-identifier}

Innan du börjar bör varje experiment ha en egen identifierare för spårnings- och analysändamål. En bra startpunkt är att hitta en bra, unik identifierare för ditt experiment, som blir &quot;Experiment-ID&quot;. Experimenten numreras ofta linjärt eller i korrelation till sitt Issue ID i ett system för ärendespårning eller -hantering. Experiment-ID:n använder ofta ett prefix för projektet, till exempel: `OPT-0134`, `EXP0004` eller `CCX0076`.

### Skapa din kundsida {#create-challenger-page}

Vi rekommenderar att du skapar en mapp med ett gement experiment-ID i `/experiments/ folder` (till exempel /experiment/ccx0076/). Alla sidor för utmanarvarianterna finns i den här mappen. Du skapar den här mappen i din lokala databas, till exempel SharePoint eller Goggle Drive.

Din experimentmapp bör se ut ungefär så här:

![experiment-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

När mappen har skapats placerar du en kopia av kontrollsidan i den mappen och tillämpar ändringarna på sidan som du vill testa som en del av experimentvarianten (se videon ovan). Låt oss anta att vi har följande sida på webbplatsen som vi vill experimentera med:

![kontrollsida](/help/sites-cloud/administering/assets/control-page.png)

Din kopia av utmanaren i mappen `experiments/<experiment-id>` kan se ut så här:

![utmanarsida](/help/sites-cloud/administering/assets/challenger-page.png)

Förhandsgranska och publicera utmanarsidan med hjälp av sidbrytaren och när du är klar med att skapa utmanarsidan. URL:en till den publicerade utmanaren kommer att användas i nästa avsnitt - att konfigurera experimentet.

### Konfigurera experimentet {#configure-experiment}

Så snart utmanarsidorna är klara måste du gå tillbaka till kontrollsidan och lägga till metadata som anger att sidan/sidorna nu är en del av testet.

Det finns två metadatarader som måste läggas till för en experimentell variant.

* **Experimentera**: innehåller ditt experiment-ID.

* **Experimentera varianter**: innehåller URL:er för alla utmanare på den här sidan, avgränsade med radbrytningar om du har fler än en utmanare.

Se exemplet nedan:

![metadatasida](/help/sites-cloud/administering/assets/metadata-page.png)

För varje experiment delas trafiken upp mellan alla varianter (kontroll och utmanare) och ställs automatiskt in på en jämn fördelning. Om du har en utmanare blir det automatiskt en delning på 50/50 mellan kontroll och utmanare. Om ni har två utmanare ser ni automatiskt en tredjedel av den trafik som är tilldelad till kontroll och varje utmanare osv.

Du kan åsidosätta trafikdelningen genom att konfigurera metadata. Mer information om hur du kan anpassa metadata som används i dina experiment finns på följande [sida](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Förhandsgranska och placera dina experimentella varianter {#preview-stage-experiment}

När du är redo att förhandsgranska och mellanlagra ditt experiment klickar du på Förhandsgranska från sidosparken i den övre vänstra delen. När du förhandsgranskar en sida som innehåller ett pågående experiment visas experimenteringsövertäckningen i förhandsvisningsmiljön för `.aem.page`. Med experimenteringsövertäckningen kan du växla mellan experimentvarianterna och även tillhandahålla trafikdata.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

Datainsamlingen för att mäta effektiviteten hos varje variant baseras på den [operativa telemetritjänsten i AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

### Skicka din experimentvariant till produktion {#production-experiment}

Välj experimentsidorna och klicka på Publicera från sidokickningen för att göra både kontrollen och utmanarvarianten/utmanarna synliga.

### Exempel på användningsfall {#use-case-examples}

Nedan finns flera exempel på olika användningsområden för olika experimentella varianter. I allmänhet kommer arbetsflödet att likna det som beskrivs ovan, med särskilda ändringar för varje användningsfall (som antalet utmanarsidor eller metadataändringar).

#### Full Page Experiment {#full-page}

Du använder ett helsidesexperiment för att testa mellan två varianter av samma sida. Detta är en fullsidig variant av ett a/b-test där du har en kontroll och en utmanarsida. Du kommer att ersätta hela innehållet på den&quot;ursprungliga&quot; kontrollsidan i utmanarvarianten med en annan typ av innehåll. Tänk på att kundtrafiken som standard delas jämnt (50/50), men du kan skapa anpassade uppdelningar om du vill.

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## Andra överväganden {#other-considerations}

Nedan visas flera andra aspekter som du bör tänka på när du använder kontextexperiment.

### Konvertering {#conversion}

Experimentella inställningar används för konvertering (spårar klickbara element på sidan). Alla experiment måste definieras för följande:

* Experimentera
* Vilka upplevelseblock som experimentet ska gälla för
* Hur många varianter kommer experimentet att innehålla
* Hur ser varje variant ut?

### Kontrollera att Experimentvarianter inte är indexerade {#experiment-not-indexed}

När du kör experiment är det oftast bäst att utesluta varianterna från webbplatskartan och se till att de inte indexeras av sökmotorer. Detta beror på att variantsidan kan ses som duplicerat innehåll och påverka SEO negativt.

Du kan göra detta på något av följande två sätt:

* Om du centraliserar alla experiment i en dedikerad mapp, som `/experiments`: se till att bulkbladet `metadata.xlsx` innehåller en rad med `/experiments/**` som sökväg och en robotkolumn med värdena `noindex`, `nofollow`.
* Om du behåller experimentkontrollen och varianterna med det reguljära innehållet: lägg till en robotpost i sidans metadata för varje variant, med värdet `noindex`, `nofollow`.

## Resurser för utvecklare och tekniker {#dev-resources}

Adobe Experience Manager använder [Operational Telemetry]&#x200B;(/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)

) för att samla in driftdata som är absolut nödvändiga för att upptäcka och åtgärda funktions- och prestandaproblem på webbplatser som drivs av Adobe Experience Manager. Operativa telemetridata kan användas för att diagnostisera prestandaproblem. Operativ telemetri bevarar besökarnas integritet genom stickprov (endast en liten del av alla sidvisningar övervakas).

### Integritet {#privacy-experimentation}

[Operativ telemetritjänst i AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) är utformad för att bevara besökarnas sekretess och minimera datainsamlingen. Som besökare innebär detta att Adobe inte kommer att försöka samla in personuppgifter om dig eller information som kan spåras tillbaka till dig. Som webbplatsoperatör kan du granska de dataobjekt som samlas in nedan för att förstå om de kräver samtycke.
AEM Operational Telemetry använder inte något klientläge eller ID, som cookies eller `localStorage`, `sessionStorage` eller liknande, för att samla in användningsstatistik. Data skickas transparent via ett `Navigator.sendBeacon`-anrop, inte via pixlar eller liknande tekniker. Det finns inga&quot;fingeravtryck&quot; på enheter eller enskilda personer via deras IP-adress, användaragentsträng eller andra data för att hämta samplade data.

Det är inte tillåtet att lägga till några personuppgifter i den operativa telemetridatainsamlingen och inte heller att använda telemetridata för användning som går utöver vad som är absolut nödvändigt.

### Vanliga frågor {#faq}

Nedan finns en lista med vanliga frågor och svar:

F: Kan jag justera delningsförhållandet mellan varianterna i mitt experiment, till exempel 10 % på kontrollen och 90 % på utmanaren?

Ja, delningsförhållandet kan konfigureras via [metadata](#configure-experiment).

F: Kan jag experimentera med både text och bilder?

Ja, varianten kan vara en helt annan sida, så du kan till och med testa layoutändringar.
