---
title: Funktionstestning
description: Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 0%

---


# Introduktion {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Funktionstestning"
>abstract="Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet."

Läs mer om de olika gaten som finns i [AEM as a Cloud Service distributionsprocess](/help/implementing/cloud-manager/deploy-code.md), de olika typerna av funktionstestning som är inbyggda, hur du kan bidra och hur du bäst kan använda dem i en övergripande teststrategi.

## Ökning

Följande diagram ger en översikt på hög nivå över tillgängliga rörledningar inom ramen för en övergripande teststrategi och [AEM as a Cloud Service distributionsprocess](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Service kvalitetsportar för driftsättning](assets/functional-testing/quality-gates-compact.svg)

## Syfte

Syftet med AEM Cloud Service pipelines för driftsättning är att underlätta stabil och säker driftsättning i olika faser av livscykeln för utveckling och AEM. Dessa rörledningar innehåller flera kvalitetsportar på olika nivåer för att säkerställa integriteten och säkerheten för distributioner för både AEM programändringar och AEM produktuppdateringar.

Adobe har flera inbyggda portar för kvalitet, medan andra kräver att du gör något för att implementera och konfigurera. Dessa kvalitetsportar är mångsidiga, och vissa kan användas i olika faser av livscykeln och till och med integreras i din egen utvecklingsmiljö och CI/CD-processer.

De inbyggda kvalitetsportarna validerar i första hand funktionaliteten hos AEM produkt i ditt AEM program. De anpassade kvalitetsportar du ställer in är däremot utformade för att verifiera att programmets kritiska funktioner och användarinteraktioner fungerar som de ska. Tillsammans fungerar dessa två kvalitetsportar tillsammans för att säkerställa robust och säker automatiserad driftsättning för både kodändringar och AEM produktuppdateringar.

Det är viktigt att notera att dessa kvalitetsportar inte är avsedda att vara ett omfattande testramverk för hela er teststrategi. Den AEM produkten genomgår omfattande testning innan den AEM driftsättningsprocessen för molntjänster inleds. På samma sätt bör ditt program redan vara av hög kvalitet innan det når distributionsfasen. Detta tillvägagångssätt garanterar att kvaliteten fokuserar på det primära målet att skydda driftsättningsprocessen, i stället för att ersätta en fullständig testregim.

## Kvalitetsportar

Följande diagram ger en detaljerad bild av tillgängliga kvalitetsgater och hur de används i den övergripande testningsstrategin samt [AEM as a Cloud Service distributionsprocess](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Service kvalitetsportar för driftsättning](assets/functional-testing/quality-gates-overview.svg)

### Sammanfattning av kundtillhandahållna kvalitetsportar

|                               | Enhetstester | Egen<br/> Funktionstester | Egen<br/> UI-tester | Kund<br/> Valideringar | Manuell<br/> Testning |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Produktionspipeline** | Ja<br/>Blockera<br/> | Ja<br/>Blockera<br/>60 m timeout | Ja<br/>Blockera<br/>60 m timeout | Nej | Nej |
| **Icke-produktionsförlopp** | Ja<br/>Blockera<br/> | Anmäl dig<br/>Blockera<br/>60 m timeout | Anmäl dig<br/>Blockera<br/>60 m timeout | Nej | Nej |
| **Adobe Internal Validation** | Ja<br/>Blockera<br/> | Ja<br/>Blockera<br/>60 m timeout | Ja<br/>Blockera<br/>60 m timeout | Nej | Nej |
| **Kundens CI/CD** | Ja | Ja | Ja | Ja | Ja |
| **Lokal utvecklare** | Ja | Ja | Ja | Ja | Ja |

### Enhetstest

Du uppmanas att tillhandahålla enhetstesterna för ditt AEM, som utgör grunden för varje teststrategi. De är avsedda att köras snabbt och ofta och ge snabb och snabb feedback. De är nära integrerade i utvecklararbetsflödena, din egen CI/CD och de AEM molntjänsternas distributionssystem.

De implementeras med JUnit och avrättas med Maven. Se [huvudmodulen för AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/core.html#unit-tests) för ett exempel på enhetstest för AEM och komma igång.

### Kodkvalitet

Den här kvalitetsporten är konfigurerad i körklart läge och kör en statisk kodanalys på AEM programkod.

Se [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md) och [Anpassade regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md) för mer information.

### Produkttester

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) av kärnfunktionalitet i AEM som redigerings- och replikeringsuppgifter. Adobe tillhandahåller och underhåller dem färdiga. De är avsedda att förhindra att ändringar i anpassad programkod distribueras om de bryter grundfunktionerna i AEM.

De implementeras med Junit, körs med Maven och använder officiella [AEM testar klienter](https://github.com/adobe/aem-testing-clients). Produkttestsviten underhålls som en [öppen källkod-projekt](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke), följer bästa praxis och kan anses vara en bra utgångspunkt för implementeringen av dina tester.

### Egna funktionstester

I likhet med produkttesterna är kundfunktionstester HTTP-integrationstester (IT) och implementeras väl med Junit, utförs med Maven och byggs ovanpå den officiella [AEM testar klienter](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>Anpassade funktionstester körs i pipelines för produktion och icke-produktion (opt-in), som används av AEM programändringar, driftsättningar och AEM produktpush-uppdateringar, och är därför ett viktigt bidrag för att säkerställa att programmet fungerar korrekt och öka säkerheten för releaser. Kundens funktionstester utförs också i interna verifieringssystem för förhandsversioner för varje kund, vilket gör det lättare att ge tidig feedback.

Vi rekommenderar att du fokuserar på viktiga funktioner och de viktigaste interaktionsflödena för användare för att få ett effektivt flöde i pipeline. En körningstid på cirka 15 minuter eller mindre rekommenderas för funktionstester. Fullständiga funktionstestsviter som inte får plats i denna kundport rekommenderas att köras som en del av kundens allmänna valideringsflöde under kundens utvecklingsflöde.

Se [open-sourced product tests](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) eller [it.tests-modulen för AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/ittests.html) till exempel.

Se [Java Functional Tests](/help/implementing/cloud-manager/java-functional-testing.md) för mer information.

### Anpassade gränssnittstester

För att maximera riskkontrollen för er kundspecifika utveckling rekommenderar Adobe starkt att ni samlar in kritiska gränssnittstester i AEMCS. De är avsedda att vara relativt begränsade i antal, men med störst påverkan på kundupplevelsen.

Testerna är förpackade i en Docker-bild som är utformad för att vara så beständig som möjligt (med stöd för Cypress, Selenium, Java och Javascript). De följer samma egenskaper och syften som de anpassade funktionstesterna.

>[!NOTE]
>
>Anpassade användargränssnittstester utförs i pipelines för produktion och icke-produktion (opt-in) som används av AEM program ändrar driftsättningar och AEM push-uppdateringar av produkter och är därför ett viktigt bidrag för att säkerställa att programmet fungerar korrekt och öka säkerheten för releaser. Kundens användargränssnittstester utförs också i interna verifieringsövningar före lanseringen för varje kund, vilket bidrar till att ge tidig feedback.

Vi rekommenderar att du fokuserar på viktiga funktioner och de viktigaste interaktionsflödena för att få en effektiv hantering av pipeline. Fullständiga testsviter för användargränssnitt som inte får plats i den här kundporten rekommenderas att utföras som en del av allmänna kundvalideringsflöden under kundens utvecklingsflöde.

Se [exempeltester med öppen källkod](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) eller [ui.tests-modulen för AEM projekttyp](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uitests.html) till exempel.

Se [Anpassade gränssnittstestningar](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) för mer information.

### Experience Audit

Gaten för upplevelsegranskningskvalitet fungerar [Google Lighthuse](https://developer.chrome.com/docs/lighthouse/overview/) granskningar mot kundens webbsida.

Den här kvalitetsporten tillhandahålls av AEM som är färdig, men blockerar inte distributionsledningarna. Som standard görs en granskning mot rotsidan (`/`) av publiceringsinstansen utförs. Du kan bidra genom att konfigurera upp till 25 anpassade sökvägar som ska användas för granskningar.

Se [Testning av Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) för mer information.

### Kundvalideringar

Kundens kvalitetsportal för validering är en platshållare för kundens egen testningsstrategi och -insats, som utförs innan kundens programändringar når AEM i molnet.

Här kan du välja de verktyg och ramverk du vill ha. Till skillnad från kundfunktionstester och anpassade användargränssnittstester finns det inga AEM as a Cloud Service gränser, och vi rekommenderar därför att du utför långvariga funktions- och gränssnittstester här.

Du kan välja vilket verktyg och ramverk du vill, men vi rekommenderar att du anpassar HTTP-baserade integreringstester och gränssnittstester med de verktyg och ramverk som finns tillgängliga i anpassade funktionstester och anpassade kvalitetsportar för gränssnittstestning. Vi rekommenderar integrering [Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) i er lokala testningsstrategi för att testa så nära som möjligt AEM molnmiljöer.

### Manuell provning

Den manuella kvalitetsporten är en platshållare för kunder som utför manuell testning. AEM i molnet stöder inte manuell testning och därför måste detta ske som en del av er egen lokala teststrategi.

För manuell testning kan det vara användbart att integrera med en extra utvecklingsmiljö från AEM Cloud Service.
