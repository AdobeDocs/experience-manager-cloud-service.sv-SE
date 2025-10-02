---
title: Funktionstestning
description: Läs om de tre olika typerna av funktionstestning som är inbyggda i AEM as a Cloud Service-distributionsprocessen för att säkerställa kvaliteten och tillförlitligheten i koden.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---


# Introduktion {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Funktionstestning"
>abstract="Läs om de tre olika typer av funktionstestning som är inbyggda i AEM as a Cloud Service driftsättningsprocess. Testningen säkerställer att koden är både tillförlitlig och av hög kvalitet."

Upptäck vilka kvalitetsportar som är tillgängliga i [AEM as a Cloud Service-distributionsprocessen](/help/implementing/cloud-manager/deploy-code.md) och de olika typerna av inbyggd funktionstestning. Lär dig hur du kan bidra till och optimera användningen av dem inom ramen för en omfattande teststrategi.

## Om funktionstestning

I följande diagram visas en översikt på hög nivå över tillgängliga rörledningar i samband med en övergripande teststrategi och [AEM as a Cloud Service-distributionsprocessen](/help/implementing/cloud-manager/deploy-code.md).

![Kvalitetsgater för AEM Cloud-tjänstdistribution](assets/functional-testing/quality-gates-compact.svg)

## Syfte med funktionstestning

Syftet med driftsättningspipelines för AEM Cloud-tjänster är att underlätta robusta och säkra driftsättningar i olika faser av utvecklingsfasen och livscykeln för AEM produktlansering. Dessa rörledningar innehåller flera kvalitetsportar på olika nivåer för att säkerställa integriteten och säkerheten vid driftsättning för både AEM-ändringar och AEM produktuppdateringar.

Adobe har flera inbyggda portar med hög kvalitet, medan andra kräver att du gör något för att implementera och konfigurera. Dessa portar är mångsidiga och kan användas i olika faser av livscykeln och integreras direkt i utvecklingsmiljön och CI/CD-processerna.

De inbyggda kvalitetsportarna validerar i första hand funktionaliteten hos AEM-produkten i ditt AEM-program. De anpassade kvalitetsportar du ställer in är däremot utformade för att verifiera att programmets kritiska funktioner och användarinteraktioner fungerar som de ska. Tillsammans fungerar dessa två kvalitetsportar tillsammans för att säkerställa stabil och säker automatiserad driftsättning för både kodändringar och AEM produktuppdateringar.

Det är viktigt att notera att dessa kvalitetsportar inte är avsedda att vara ett omfattande testramverk för hela er teststrategi. AEM-produkten genomgår omfattande testning innan AEM driftsättningsprocess för molntjänster inleds. På samma sätt bör ditt program redan vara av hög kvalitet innan det når distributionsfasen. Detta tillvägagångssätt garanterar att kvaliteten fokuserar på det primära målet att skydda driftsättningsprocessen, i stället för att ersätta en fullständig testregim.

## Kvalitetsgaller vid testning

I följande diagram visas en detaljerad översikt över tillgängliga kvalitetsgates och deras användning i den övergripande testningsstrategin och i [AEM as a Cloud Service-distributionsprocessen](/help/implementing/cloud-manager/deploy-code.md).

![Kvalitetsgater för AEM Cloud-tjänstdistribution](assets/functional-testing/quality-gates-overview.svg)

### Sammanfattning av kundtillhandahållna kvalitetsportar

|                               | Enhetstester | Anpassade <br/>-funktionstester | Anpassade <br/>-gränssnittstester | Kund<br/> - valideringar | Manuell <br/>-testning |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Produktionspipeline** | Ja<br/>Blockerar<br/> | Ja<br/>Blockerar<br/>60m timeout | Ja<br/>Blockerar<br/>30m timeout | Nej | Nej |
| **Icke-produktionsförlopp** | Ja<br/>Blockerar<br/> | Opt-In<br/>Blocking<br/>60m Timeout | Opt-In<br/>Blocking<br/>30m Timeout | Nej | Nej |
| **Adobe Internal Validation** | Ja<br/>Blockerar<br/> | Ja<br/>Blockerar<br/>60m timeout | Ja<br/>Blockerar<br/>30m timeout | Nej | Nej |
| **Kundens CI/CD** | Ja | Ja | Ja | Ja | Ja |
| **Kund, lokal utvecklare** | Ja | Ja | Ja | Ja | Ja |

### Enhetstest

Du uppmanas att tillhandahålla enhetstesterna för ditt AEM-program, som utgör grunden för varje teststrategi. De är avsedda att köras snabbt och ofta och ge snabb och snabb feedback. De är nära integrerade i utvecklararbetsflödena, din egen CI/CD och AEM molntjänster.

De implementeras med JUnit och avrättas med Maven. Se kärnmodulen [i AEM Project Archetype](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/developing/archetype/using#unit-tests) för ett exempel på enhetstest för AEM och hur du kommer igång.

### Kodkvalitet

Den här kvalitetsporten är konfigurerad och kör en statisk kodanalys på din AEM-programkod.

Mer information finns i [Testa kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md) och [Anpassade regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md).

### Produkttester

Funktionstester för produkter är stabila HTTP-integrationstester (IT) för AEM kärnfunktioner, inklusive redigerings- och replikeringsuppgifter. Adobe tillhandahåller och underhåller dem färdiga. De är avsedda att förhindra att ändringar i anpassad programkod driftsätts om de bryter grundfunktionerna i AEM-produkten.

De använder JUnit för implementering, körs med Maven och förlitar sig på officiella [AEM Testing Clients](https://github.com/adobe/aem-testing-clients). Produkttestsviten underhålls som
ett [öppen källkodsprojekt](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) följer bästa praxis och kan anses vara en bra startpunkt för implementeringen av dina tester.

### Anpassade funktionstester

På samma sätt som produkttesterna är kundfunktionstester HTTP-integreringstester (IT) som implementeras med JUnit, körs med Maven och byggs ovanpå de officiella [AEM Testing Clients](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>Anpassade funktionstester körs i både produktionssystem och icke-produktionssystem (opt-in) som används för AEM-driftsättning av programändringar och AEM push-uppdateringar av produkter. De spelar en viktig roll för att säkerställa att applikationen fungerar som den ska och för att förbättra säkerheten för releaser. Kundens funktionstester utförs också i interna verifieringssystem för förhandsversioner för varje kund, vilket gör det lättare att ge tidig feedback.

Adobe rekommenderar att man fokuserar på nyckelfunktioner och primära användarinteraktionsflöden för att få en funktionstestmiljö på upp till 15 minuter för att behålla effektiva pipeline-körningar. Kompletta funktionstestsviter som överskrider denna tid bör utföras som en del av de allmänna kundvalideringsstegen under utvecklingsprocessen.

Exempel finns i [open-sourced product tests](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) eller [it.tests-modulen i AEM Projects Archetype](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests).

Mer information finns i [Java Functional Tests](/help/implementing/cloud-manager/java-functional-testing.md).

### Anpassade gränssnittstester

För att maximera riskkontrollen för er kundspecifika utveckling rekommenderar Adobe att ni hämtar in viktiga gränssnittstester i AEM as a Cloud Service. Behåll dem begränsade men fokusera på att maximera deras påverkan på kundupplevelsen.

Testerna är förpackade i en Docker-bild som är utformad för att vara så beständig som möjligt (med stöd för Cypress, Playwright, Selenium, Java och JavaScript). De följer samma egenskaper och syften som de anpassade funktionstesterna.

>[!NOTE]
>
>Anpassade användargränssnittstester utförs i både produktionssystem och icke-produktionssystem (opt-in) som används för AEM-programändringsdistributioner och AEM produktpush-uppdateringar. De är nödvändiga för att ditt program ska fungera väl och för att öka säkerheten för releaser. Kundens användargränssnittstester utförs också i interna verifieringsövningar före lanseringen för varje kund, vilket bidrar till att ge tidig feedback.
>
>Icke-selenbehållare bör köra tester med en HTTP-proxy som baseras på miljövariablerna i [UI-testavsnittet](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing).

Adobe rekommenderar att man fokuserar på viktiga funktioner och de viktigaste interaktionsflödena för att få en effektiv hantering av pipeline. Fullständiga testsviter för användargränssnitt som överskrider denna kvalitetsport ska köras som en del av de allmänna kundvalideringskanalerna. Lägg in dem i kundens utvecklingsprocess.

Se [exempel på tester med öppen källkod](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) eller [ui.tests-modulen i AEM Projects Archetype](/help/implementing/cloud-manager/ui-testing.md) för exempel.

Mer information finns i [Testning av anpassat användargränssnitt](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing).

### Upplevelsegranskning

Gaten för upplevelsegranskningskvalitet utför [Google Lightroom](https://developer.chrome.com/docs/lighthouse/overview/)-granskningar mot kundens webbsida.

Den här kvalitetsporten tillhandahålls av AEM när det är klart, men blockerar inte distributionsledningarna. Som standard utförs en granskning mot rotsidan (`/`) för publiceringsinstansen. Du kan bidra genom att konfigurera upp till 25 anpassade sökvägar som ska användas för granskningar.

Mer information finns i [Experience Audit Testing](/help/implementing/cloud-manager/reports/report-experience-audit.md).

### Kundvalideringar

Kundens kvalitetsportal för validering är en platshållare för kundens egen testningsstrategi och -insats, som utförs innan kundens programändringar når AEM molndistributionssystem.

Här kan du välja de verktyg och ramverk du vill ha. Till skillnad från kundfunktionstester och anpassade användargränssnittstester finns det inga AEM as a Cloud Service-relaterade begränsningar. Därför rekommenderar Adobe att du utför långvariga funktions- och gränssnittstestningar här.

Du kan välja vilket verktyg och ramverk som helst, men Adobe föreslår att HTTP-baserad integrering och gränssnittstester anpassas till de verktyg och ramverk som används i de anpassade funktions- och gränssnittstestkvalitetsportarna. Dessutom rekommenderar Adobe att du inkluderar [Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) i din lokala testningsstrategi för att spegla AEM molnmiljöer noggrant.

### Manuell provning

Den manuella kvalitetsporten är en platshållare för kunder som utför manuell testning. Eftersom AEM molnledningar inte har stöd för manuell testning måste det ingå i er lokala testningsstrategi.

För manuell testning kan det vara användbart att integrera med en ytterligare AEM Cloud-utvecklingsmiljö.
