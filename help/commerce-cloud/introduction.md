---
title: Introduktion och översikt
description: Introduktion och översikt av innehåll och handel. Experience Manager Commerce Integration Framework (CIF) rekommenderas av Adobe för att integrera och utöka handelstjänster från Adobe Commerce och andra tredjepartslösningar med Experience Cloud.
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c,74e832f9-f8ff-4901-b4c2-6a2862c51411
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# Innehåll och handel {#content-commerce}

Med Adobe Experience Manager innehåll och e-handel kan varumärken skalas och utvecklas snabbare för att särskilja handelsupplevelser och fånga upp ökade webbutgifter. AEM Content and Commerce kombinerar de engagerande, flerkanaliga och personaliserade upplevelserna i Experience Manager med valfritt antal handelslösningar för att ge alla delar av kundresan olika upplevelser, minska tiden till värde och öka konverteringsgraden.

## Så kan innehåll och handel hjälpa kunderna att lyckas {#successful}

Med allt högre förväntningar på onlinehandelsupplevelser har varumärkena press på sig att leverera differentierade upplevelser och mer innehåll snabbare. Att implementera en plattform för innehållshantering kräver ofta stora tids- och budgetinvesteringar i utveckling av grundläggande element, som anpassade komponenter och redigeringsverktyg, och medför kostnader för underhåll och uppgraderingar. Experience Manager Sites erbjuder Content and Commerce som en tilläggsmodul för Experience Manager as a Cloud Service som tillhandahåller körklara kärnkomponenter för e-handel, redigeringsverktyg och en referensbutik som snabbar upp idriftsättningen, möjliggör smidigt samarbete mellan team och driver konverteringsprocessen framåt.

Varumärken kan integrera Experience Manager med Adobe Commerce, som ingår i Adobe Experience Cloud, samt valfri e-handelsmotor. Med Experience Manager Content and Commerce kan varumärken

* Skala och förnya snabbare
* Skräddarsy upplevelser och öka konverteringsgraden
* Skapa en gång och publicera överallt
* Berika och differentiera upplevelser för kunderna
* Effektivisera framtagningen av e-handelsdata

## Introducing AEM Commerce Integration Framework (CIF) {#cif-intro}

Eftersom dessa projekt måste ta itu med komplexiteten med att integrera en handelslösning. En e-handelslösning kan vara allt från en kommersiell lösning som Adobe Commerce Cloud till en uppsättning anpassade e-handelstjänster. Integrationen är mycket beroende av användningsfall och ekosystem. Den finns oftast på olika ställen och har många olika varianter:

* Integrering av ett komplext och dynamiskt ekosystem (exempel produktkataloger)
* Företag måste hantera produktinnehåll med sin egen livscykel på ett effektivt och flerkanaligt sätt
* Bygga komplexa och personaliserade kundresor för olika chefer
* Möjlighet att snabbt anpassa och förnya på baksidan och framsidan
* En skalbar och stabil E2E-infrastruktur som är byggd för bästa prestanda (försäljning i Flash, Black Friday, ...). Detta inkluderar enhetlig sökning och cachehantering.

Denna komplexitet öppnar dörren till potentiella felpunkter, ökad ägandekostnad, förseningar och minskad värdeutveckling. Dessa orsaker har lett till utvecklingen av Commerce Integration Framework (CIF), som är ett tillägg för Experience Manager. CIF utökar Experience Manager med handelsfunktioner och standardiserar integreringen med en handelsmotor. Resultatet är en framtidssäker, stabil och skalbar lösning med lägre total ägandekostnad. Den ger teknikinnovation och affärsinnovation med smidiga verktyg och smidigt integrerade funktioner som bygger övertygande handelsupplevelser.

![CIF-element](./assets/CIF/CIF_Overview.png)

## CIF har stött kunder sedan 2013 {#support}

CIF har med över 200 kunder etablerat sig som en framgångsrik ingrediens i ett framgångsrikt innehålls- och handelsprojekt. Detta ger värde för IT och företag både idag och i framtiden. I de senaste kundprojekten beskrivs CIF som en&quot;fantastisk accelerator och en enorm tidsbesparing med mycket värde&quot;.

## Fördelar med CIF {#cif-benefits}

CIF har färdiga affärskomponenter som minskar behovet av anpassad kod och snabbar upp time-to-market för varumärken. Alla kärnkomponenter integreras direkt med Adobe datalager på klientsidan för att utrusta kundprofiler, till exempel den enhetliga profilen. Den här profilen fångar i detalj en besökares beteende, som kan användas för att förutse och personalisera kundresan i realtid.

Tillägget CIF ger produktkontext i Experience Manager och innehåller redigeringsverktyg som produktkonsol och produkt-/kategoriväljare som ger marknadsföraren möjlighet att skapa och leverera köpbara upplevelser i Experience Manager utan att vara beroende av utvecklaren. Fördelar:

### Erfarenheter {#experiences}

Kraftfulla CIF-verktyg i AEM gör det möjligt för innehållsskapare att snabbt skapa avancerade och personaliserade e-handelsupplevelser på ett skalbart och oberoende sätt för att utnyttja affärsmöjligheter.

![CIF-element](./assets/CIF/CIF_Product_Experience_Management.png)

### Tid till värde (TTV) {#ttv}

Snabbare projektutveckling med [AEM kärnkomponenter](https://www.aemcomponents.dev/), [AEM Venia reference storefront](https://github.com/adobe/aem-cif-guides-venia), [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)och integreringsmönster för PWA (Headless content &amp; commerce).

CIF är skapat för kontinuerlig innovation med ett kontinuerligt uppdaterat tillägg som gör att kunden kan komma åt nya och förbättrade funktioner.

### Integreringar {#integrations}

Koppla samman ditt ekosystem (t.ex. en e-handelslösning) med Experience Cloud med  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), en serverfri PaaS som bygger på mikrotjänster, och [CIF:s referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Beprövade mönster och bästa praxis {#proven}

CIF stöder kunder med standardiserade integreringsmönster baserade på bästa praxis. Detta hjälper kunderna att bli framgångsrika idag och är flexibelt att växa med kunden och anpassa sig till framtida krav:

* Eliminerar vanliga problem med produktkatalogintegreringar som kan uppstå. Exempel:
   * Prestandaproblem med ökad katalogvolym eller komplexitet
   * Ingen åtkomst till mellanlagrade data
   * Behovet av produktdata och upplevelser i realtid
* En växande digital mognad leder till ett behov av upplevelsehantering. CIF har funktioner för hantering av produktupplevelser som kan införlivas stegvis utan ytterligare IT-arbete.
* Redo för alla kanaler: CIF har stöd för en mängd olika kontakttekniker (serversidan, hybrid, klientsidan) med mönster, acceleratorer och kärnkomponenter.

## Resa {#journey}

Om du följer en Commerce Journey, vänligen gå till nästa steg:

* The [AEM Innehållsförfattarens resa](/help/commerce-cloud/commerce-journeys/aem-commerce-content-author/getting-started.md)
