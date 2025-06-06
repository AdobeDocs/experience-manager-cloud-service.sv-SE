---
title: Introduktion och översikt
description: Lär dig hur du använder och administrerar Experience Manager Content and Commerce as a Cloud Service.
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 1%

---


# Innehåll och Commerce {#content-commerce}

Med Adobe Experience Manager innehåll och e-handel kan varumärken skalas och utvecklas snabbare för att särskilja handelsupplevelser och fånga upp ökade webbutgifter. AEM Content och Commerce kombinerar de engagerande, flerkanaliga och personaliserade upplevelserna i Experience Manager med ett obegränsat antal e-handelslösningar för att ge alla delar av kundresan olika upplevelser, minska time to value och öka konverteringsgraden.

## Hur innehåll och Commerce hjälper kunderna att lyckas {#successful}

Med allt högre förväntningar på onlinehandelsupplevelser har varumärkena press på sig att leverera differentierade upplevelser och mer innehåll snabbare. Att implementera en plattform för innehållshantering kräver ofta stora tids- och budgetinvesteringar i utveckling av grundläggande element, som anpassade komponenter och redigeringsverktyg, och medför kostnader för underhåll och uppgraderingar. Experience Manager Sites erbjuder Content och Commerce som en tilläggsmodul för Experience Manager as a Cloud Service som innehåller färdiga komponenter för e-handel, redigeringsverktyg och en referensbutik som snabbar upp användningen, möjliggör smidigt samarbete mellan team och driver konverteringsprocessen framåt.

Varumärken kan integrera Experience Manager med Adobe Commerce, en del av Adobe Experience Cloud och valfri e-handelsmotor. Med Experience Manager Content och Commerce kan varumärken

* Skala och förnya snabbare
* Skräddarsy upplevelser och öka konverteringsgraden
* Skapa en gång och publicera överallt
* Berika och differentiera upplevelser för kunderna
* Effektivisera framtagningen av e-handelsdata

## Introduktion AEM Commerce integration framework (CIF) {#cif-intro}

Eftersom dessa projekt måste ta itu med komplexiteten med att integrera en handelslösning. En handelslösning kan vara allt från en kommersiell lösning som Adobe Commerce Cloud till en uppsättning anpassade e-handelstjänster. Integrationen är mycket beroende av användningsfall och ekosystem. Den finns oftast på olika ställen och har många olika varianter:

* Integrering av komplexa och dynamiska ekosystem (exempel produktkataloger)
* Företag måste hantera produktinnehåll med sin egen livscykel på ett effektivt och flerkanaligt sätt
* Bygga komplexa och personaliserade kundresor för olika chefer
* Möjlighet att snabbt anpassa och förnya på baksidan och framsidan
* En skalbar och stabil E2E-infrastruktur som är byggd för bästa prestanda (Flash, Black Friday, ...). Detta inkluderar enhetlig sökning och cachehantering.

Denna komplexitet öppnar dörren till potentiella felpunkter, ökad ägandekostnad, förseningar och minskad värdeutveckling. Dessa orsaker har lett till utvecklingen av Commerce integrationa frameworken (CIF) som är ett tillägg för Experience Manager. CIF utökar Experience Manager med e-handelsfunktioner och standardiserar integreringen med en e-handelsmotor. Resultatet är en framtidssäker, stabil och skalbar lösning med lägre total ägandekostnad. Den ger teknikinnovation och affärsinnovation med smidiga verktyg och smidigt integrerade funktioner som bygger övertygande handelsupplevelser.

![CIF Elements](./assets/CIF/CIF_Overview.png)

## CIF har stött kunder sedan 2013 {#support}

Med över 200 kunder har CIF etablerat sig som en framgångsrik ingrediens i ett framgångsrikt innehålls- och handelsprojekt. Detta ger värde för IT och företag både idag och i framtiden. I de senaste kundprojekten beskrivs CIF som en&quot;fantastisk accelerator och en enorm tidsbesparing med mycket värde&quot;.

## CIF {#cif-benefits}

CIF tillhandahåller färdiga e-handelskomponenter som minskar behovet av anpassad kod och snabbar upp time-to-market för varumärken. Alla huvudkomponenter är integrerade med Adobe datalager på klientsidan för att ge bättre överblick över kundprofiler, som den enhetliga profilen. Den här profilen fångar i detalj en besökares beteende, som kan användas för att förutse och personalisera kundresan i realtid.

Tillägget CIF ger produktkontext i Experience Manager och innehåller redigeringsverktyg som produktkonsol och produkt-/kategoriväljare som ger marknadsföraren möjlighet att skapa och leverera köpbara upplevelser i Experience Manager utan att vara beroende av utvecklaren. Fördelar:

### Erfarenheter {#experiences}

Kraftfulla CIF i AEM gör det möjligt för innehållsskapare att snabbt skapa komplexa och personaliserade e-handelsupplevelser på ett skalbart och oberoende sätt för att utnyttja affärsmöjligheter.

![CIF Elements](./assets/CIF/CIF_Product_Experience_Management.png)

### Tid till värde (TTV) {#ttv}

Snabbar upp projektutvecklingen med [AEM Core Components](https://www.aemcomponents.dev/), [AEM Venia reference storefront](https://github.com/adobe/aem-cif-guides-venia), [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE) och integreringsmönster för PWA (Headless content &amp; commerce).

CIF har tagits fram för kontinuerlig innovation med ett kontinuerligt uppdaterat tillägg som ger kunden tillgång till nya och förbättrade funktioner.

### Integreringar {#integrations}

Koppla ditt ekosystem (till exempel en e-handelslösning) till Experience Cloud med [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), en icke-serverbaserad PaaS utan mikrotjänst och [CIF referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Beprövade mönster och bästa praxis {#proven}

CIF stöder kunder med standardiserade integreringsmönster baserade på bästa praxis. Detta hjälper kunderna att bli framgångsrika idag och är flexibelt att växa med kunden och anpassa sig till framtida krav:

* Eliminerar vanliga problem med produktkatalogintegreringar som kan uppstå. Exempel:
   * Prestandaproblem med ökad katalogvolym eller komplexitet
   * Ingen åtkomst till mellanlagrade data
   * Behovet av produktdata och upplevelser i realtid
* En växande digital mognad leder till ett behov av upplevelsehantering. CIF har funktioner för hantering av produktupplevelser som kan införlivas stegvis utan ytterligare IT-arbete.
* Redo för flera kanaler: CIF har stöd för en mängd olika kontaktytor (serversidan, hybrid, klientsidan) med mönster, acceleratorer och kärnkomponenter.

## Resa {#journey}

Om du följer en Commerce Journey, gå till nästa steg:

* Resan [AEM Innehållsförfattare](/help/commerce-cloud/commerce-journeys/aem-commerce-content-author/getting-started.md)
