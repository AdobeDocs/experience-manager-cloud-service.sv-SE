---
title: Introduktion till AEM Commerce som Cloud Service
description: Experience Manager Commerce som Cloud Service består av Commerce Integration Framework (CIF), som Adobe rekommenderar för att integrera och utöka handelstjänster från Magento och andra tredjepartslösningar med Experience Cloud.
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 0%

---


# Introducing AEM Commerce as a Cloud Service {#commerce-intro}

Experience Manager Commerce som Cloud Service består av Commerce Integration Framework (CIF), som Adobe rekommenderar för att integrera och utöka handelstjänster från Magento och andra tredjepartslösningar med Experience Cloud. På så sätt kan Adobe-kunder leverera en unik och personaliserad shoppingupplevelse i flera kanaler baserat på den senaste tekniken.

Commerce Integration Framework är en tilläggsmodul för Experience Manager som Cloud Service och innehåller en uppsättning redigeringsverktyg, komponenter och en referensbutik som snabbar upp utvecklingen av integreringar mellan Experience Manager som en Cloud Services- och handelslösning.

## Fördelar med CIF {#cif-benefits}

De viktigaste fördelarna är:

* Integrationen är ett abstraktionslager som standardiserar och kapslar in integreringar med flera system.

* CIF har stöd för helkanalsupplevelser:

   * Single Page-program och flersidiga program
   * GraphQL-slutpunkter

* CIF erbjuder serverlösa, mikrotjänstbaserade processer och affärslogikskikt för anpassning och utbyggnad av handelstjänster.

* CIF har färdiga integreringar med Adobe-lösningar som AEM och Magento

## CIF-element {#cif-elements}

![CIF-element](/help/commerce-cloud/assets/cif-overview1.jpg)


### CIF-tillägg för redigeringsverktyg {#add-on-authoring-tools}

Tillägget CIF ger tillgång till redigeringsverktyg för e-handel, som produktkonsol, produkt- och kategoriväljare eller produktsökning för författare som kan ge dem möjlighet att skapa avancerat material för marknadsföring och handel. Tillägget hanterar även serverdelsanslutningen till Magento (eller alternativt handelssystem) via GraphQL. När tillägget har etablerats distribueras det automatiskt på AEM som en Cloud Service-miljö.

### AEM CIF-kärnkomponenter {#aem-cif-core}

De AEM CIF Core-komponenterna är renderade komponenter på serversidan och klientsidan med stöd för Magento GraphQL. De används för att skapa en statisk, cacheable och SEO-vänlig e-handelsbutik som bygger på AEM tekniker.

Det finns grundläggande komponenter som är gemensamma för alla handelsimplementationer, som produktinformation, produktlista, navigering, sökning osv. De kan användas som de är eller utökas.

CIF-komponenterna [](https://github.com/adobe/aem-core-cif-components) AEM fungerar som [AEM Sites Core-komponenterna](https://github.com/adobe/aem-core-wcm-components) men är avsedda för handelsspecifika användningsområden.

De viktigaste fördelarna är:

* De är enkla att använda i dina projekt.
* De kan användas i befintligt skick eller med mycket små ändringar.
* De ger bästa praxis för att ansluta till Magento via API:er för GraphQL eller REST API:er

Komponenter som Product Teaser och Product Carousel tillhandahålls för att göra det möjligt för AEM Authors att skapa Experience pages in AEM, vilket kombinerar marknadsförings- och e-handelsinnehåll. Dessa komponenter kan enkelt dras och släppas på en innehållssida som skapats i AEM och länkas till specifika produkter eller kategorier med CIF-redigeringsverktyg som produktväljaren eller kategoriväljaren i Cloud Servicen.

Alla komponenter är öppna från [GitHub](https://github.com/adobe/aem-core-cif-components). Detta visar fullständig genomskinlighet i kommande ändringar och gör att du enkelt kan få den senaste versionen. Du kan också tillhandahålla pull-begäranden om förbättringar och felkorrigeringar som kan införlivas.

### AEM Venia Storefront {#aem-venia-storefront}

Den [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia) är en modern produktionsklar referensbutik som visar upp en grundläggande B2C-handelsresa. Det kan användas för att starta affärsprojekt och snabba upp projekt med AEM, CIF och Magento. Här visas de bästa sätten att integrera AEM och Magento och hur du använder [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) och [AEM Sites Core Components](https://github.com/adobe/aem-core-wcm-components) och stöder Adobe Commerce GraphQL-slutpunkter. Den innehåller också en referensplats för att demonstrera integreringen mellan AEM och Magento.

AEM Venia Storefront är ett blandat program där AEM äger glaset och Magento driver handelsbackend på ett headless sätt. Både serversidesrendering och klientsidesrendering används i butiken. Återgivning på serversidan används för att leverera statiskt innehåll och återgivning på klientsidan används för att leverera dynamiskt innehåll.

Produkt- och katalogsidor är relativt statiska och återges på serversidan med AEM CIF Core Components som Product Detail och Product List för generiska mallar som skapats i AEM. Dessa komponenter hämtar data från Magento via GraphQL API:er.
Dessa sidor skapas dynamiskt, återges på servern, cachelagras i AEM och skickas sedan till webbläsaren.
För mer dynamiska attribut som lager och pris används däremot komponenter på klientsidan. Komponenter på klientsidan eller webbkomponenter hämtar data direkt från Magento via API:er för GraphQL och innehållet återges sedan i webbläsaren.

#### Utcheckning {#checkout}

I den här referensbutiken används en kundsidesvagnskomponent som renderar kundvagnen och kassaformuläret för att demonstrera ett fullständigt upplevelseintegreringsmönster där du kan leverera upplevelser där Magento kör på ett helt headless sätt och AEM äger glaset. Vi rekommenderar att du använder de angivna abstrakta betalningsmetoderna. Detta placerar webbläsarklienten i direkt kommunikation med betalgatewayleverantören så att varken Adobe- eller Magento-moln rymmer eller skickar PCI-känsliga data.

#### Kontohantering {#account-management}

Kontohanteringen hanteras av Magento och referensarkivet använder React-baserade komponenter på klientsidan för att AEM ska kunna återge upplevelsen för följande funktioner: Skapa konto, logga in och Glömt lösenord.

Projektet AEM Venia Storefront har öppen källkod och mer information finns i [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia).

### AEM Project Archetype {#aem-project-archtype}

Den [AEM projekttypen](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html) kan användas för att skapa ett minimalt, metodbaserat Adobe Experience Manager-projekt som utgångspunkt för dina egna AEM. Om du vill kan du [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) inkluderas i ett nyskapat projekt.

### CIF-tilläggslager {#cif-extension}

CIF-tilläggslagret är ett mellanlager som hanterar komplex affärslogik. Det körs på Adobe I/O Runtime-plattformen som är Adobe serverless. Det gör att du kan utöka hela servicesamtal genom att lägga in affärslogik och processlogik på mikrotjänstnivå. Affärslogiken skulle till exempel vara att använda plats och kanal för att fastställa en lagerstrategi. Processlogiken skulle till exempel vara att hämta personaliserad information.

### CIF-integreringslager {#cif-integration-layer}

Integreringslagret CIF används för att standardisera integreringar med andra handelslösningar. Det körs på Adobe I/O Runtime-plattformen, som är Adobe serverless, och möjliggör integrering på mikrotjänstnivå genom att mappa tredjeparts-API:er mot Adobe Commerce-API:er. För att hjälpa dig att komma igång med att bygga tredjepartsintegreringar med AEM har vi skapat en [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference) som visar hur en icke-Magento-handelsserver kan integreras via API:er för Adobe Commerce (Magento GraphQL).

## AEM för handelsintegrering {#aem-commerce-integration}

Nedan visas några av de vanligaste integreringsmönstren AEM Commerce.

![AEM CIF-integreringsmönster](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Integreringsmönster 1 {#integration-pattern-one}

Detta är vårt rekommenderade integreringsmönster där AEM äger hela glaset och integrerar handelstjänster via Adobe Commerce GraphQL API:er. Det här mönstret frigör AEM flexibilitet för att skräddarsy multimediewebbplatser för olika enheter. Integrationsmönstret stöds av CIF som en färdig lösning.


### Integreringsmönster 2 {#integration-pattern-two}

Det här mönstret visar ett helt headless sätt att leverera innehåll och handel. Leveransen sker helt på klientsidan. I det här mönstret levereras innehåll via API och HTML, och data från Commerce levereras via GraphQL. Det här mönstret stöds för närvarande inte av ej ifyllda CIF.


### Integreringsmönster 3 {#integration-pattern-three}

I det här mönstret äger Magento glaset och bäddar in AEM innehåll. Det AEM innehållet kan levereras via Experience Fragments eller Content Fragments. Det här integreringsmönstret kräver projektspecifikt arbete och kan inte implementeras direkt med CIF.


### Integreringsmönster 4 {#integration-pattern-four}

Detta är ett vanligt integreringsmönster där glaset eller presentationsskiktet delas mellan AEM och en Commerce-lösning. Vanligtvis levererar Commerce-lösningen icke-marknadsföringssidor som utcheckning och mitt konto och AEM marknadsföringssidor och butikskataloger. I det här mönstret måste du se till att kundvagnar och användarsessioner hanteras på rätt sätt mellan de två systemen för att undvika en osammanhängande användarupplevelse. Magento lagrar till exempel kundvagnen och användarsessionen i en cookie som kan delas mellan AEM &amp; Magento. Det här mönstret kräver projektspecifikt arbete och kan inte implementeras direkt med CIF.
