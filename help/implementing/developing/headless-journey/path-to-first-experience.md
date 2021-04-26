---
title: Vägen till din första upplevelse med AEM utan headless
description: I den här delen av den AEM Headless Developer Journey kommer du att förstå hur du implementerar din första headless-upplevelse i AEM, inklusive planeringsöverväganden, och också lära dig bästa praxis för att göra din väg så smidig som möjligt.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 9fb18dbe60121f46dba1e11d4133e5264a6d538d
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 0%

---


# Sökväg till din första upplevelse med AEM Headless {#path-to-first-experience}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey,](overview.md), kommer du att förstå hur du implementerar din första headless-upplevelse av AEM, inklusive planeringsöverväganden, och även lära dig bästa praxis för att göra din väg så smidig som möjligt.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet om den AEM resan utan huvud, [Getting Started with AEM Headless as a Cloud Service](getting-started.md), lärde du dig den grundläggande teorin om vad ett headless CMS är och du bör nu:

* Förstå grunderna i AEM headless-funktioner.
* Lär känna förutsättningarna för AEM headless-funktioner.
* Tänk på AEM integrationsnivåer utan motstycke.
* Du kan definiera projektet utifrån dess omfång.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du förbereder ett eget AEM headless-projekt.

## Mål {#objective}

Det här dokumentet hjälper dig att förstå de steg som krävs för att implementera ditt första projekt. Efter att ha läst den bör du:

* Förstå viktiga planeringsöverväganden när du utformar ditt innehåll.
* Förstå stegen för att implementera headless i AEM.
* Ha koll på vilka verktyg och AEM som krävs.
* Lär dig de bästa sätten att göra den enkla resan smidig, hålla innehållsgenereringen effektiv och se till att innehållet levereras snabbt.

## Krav {#requirements}

Innan du fortsätter med det här dokumentet måste du kontrollera att du har granskat det tidigare dokumentet i AEM Headless Developer Journey, [Getting Started with AEM Headless as a Cloud Service](getting-started.md) och se till att du:

* Uppfyll de angivna kraven.
* Har tänkt på din egen projektdefinition, inklusive omfång, roller och prestanda.

## Planering för lyckat {#planning-for-success}

För att starta ditt första AEM headless-projekt måste ni se till att ni har en innehållsmodell som stöder den personalisering och de uppdateringar ni vill göra i alla era kanaler.

Förutom AEM vill du också se till att du har en korrekt utvecklingsmiljö konfigurerad om du skapar ett klientprogram så att du kan testa klienten mot API-anrop som ska AEM som en Cloud Service.

### Definiera innehållsmodeller och API:er {#defining-models}

Ni vill skapa en enhetlig upplevelse och hantera personaliserade kampanjer i alla kanaler, så att ni kan se varje enskild kanal och yta som sin egen innehållsstruktur att leverera till. Det är dock en utmaning att behålla varje kanal med en egen innehållsmodell.

Istället bör ni överväga hur innehåll på olika ytor är relaterat till en organiseringsprincip som varumärken och produkthierarkier, kategorier av varor eller ytor, eller steg i kundresan. Om du till exempel har en uppsättning ytor som stöder ett visst varumärke med bilar som du tillverkar, kanske du vill börja med en innehållsmodell för allmän information som skulle vara sann för hela bilen och sedan ha mer sammanhangsberoende specifika element, till exempel innehåll som behövs när bilen startar vid serviceproblem. En sådan modell kommer att genomdriva ett arv av allmänt varumärkesinnehåll samtidigt som den möjliggör förändringar baserat på det specifika sammanhang som behövs. Det hjälper även till med framtida hantering av uppdateringar av det här innehållet eftersom ni kan tillämpa kontroll baserat på roller som den övergripande marknadsföraren eller produktchefen för hela varumärket jämfört med en författare som ansvarar för upplevelsen av att starta bilen.

När du har innehållsmodellen och en tydlig vy över de olika klienter som innehållet ska visas för, måste du se till att de GraphQL/API:er som är kopplade till åtkomsten till olika innehållsmodeller publiceras till alla klienter som behöver det här innehållet. Det finns olika sätt att komma åt visst innehåll. Du kan begära ett visst statiskt innehåll som möjliggör cachelagring av innehållet och högre prestanda. Du kan också begära dynamiskt genererat innehåll som kräver mer bearbetning. Se till att kunderna utnyttjar de API:er som är mest effektiva för deras affärsbehov.

## Förstå dina miljöer {#understanding-environments}

Inom AEM finns det tre typer av miljöer: utveckling, staging och produktion.

Utvecklingsmiljöerna (du kan ha flera) är en säker plats att experimentera med och testa idéer på. Under projektets inledande fas rekommenderar Adobe att utvecklingsmiljöerna används för att testa olika varianter av innehållsmodellerna och för att se vilka som ger de avsedda resultaten för ytorna.

Mellanlagringsmiljön för headless-projekt används för att validera nya AEM produktreleaser innan de börjar producera. Håll en uppdaterad lista över produktionsinnehållsmodellerna där och en delmängd av innehållet, så att du kan få JSON-filer renderade för att jämföra dem som fortfarande ger samma utdata, när du gör ändringar eller AEM gör ändringar

Det är i produktionen som innehållsförfattare skapar och hanterar sitt faktiska innehåll. Modellförändringar i produktionen måste genomföras med försiktighet och bakåtkompatibilitet i åtanke.

Under utvecklingsfasen rekommenderar vi att du arbetar med en utvecklings- och staging-miljö. När du går över till prestandatestning vill du gå över till produktionsmiljön.

### Samarbete mellan utvecklare och innehållsförfattare {#cooperation}

Utvecklarna behöver en AEM utvecklingsmiljö som är anpassad efter de populära innehållsmodellerna. Utvecklaren utvecklar klienten som konsumerar innehåll från AEM headless eftersom innehållsförfattarna fortfarande skapar innehållet. Därför är API-definitionerna mycket viktiga. Genom att utnyttja AEM SDK kan utvecklaren skapa en testkrok så att klient- och enhetstester kan skapas för att säkerställa att klienten kan återge innehållet på rätt sätt.

Innehållsförfattare skapar innehåll baserat på de innehållsmodeller som har definierats i mellanlagringsmiljön. Med hjälp av utvecklingsverktyget för innehållsfragment kan författaren skapa ett nytt innehållsfragment eller redigera ett befintligt innehållsfragment. Innan den publiceras kan författaren förhandsgranska hur den kommer att se ut i klienten genom att arbeta med utvecklaren för att överföra innehållsmodellen till utveckling eller konfigurera en utvecklingsmiljö enbart för att författarna ska kunna se hur den skulle se ut i klienten.

## Konfigurera {#setup}

Innan du börjar använda headless i AEM måste du se till att alla nödvändiga funktioner är aktiverade. I det här avsnittet beskrivs vad som krävs. De faktiska stegen för att utföra dessa steg beskrivs senare i [AEM Headless Developer Journey.](#overview.md)

Du kan också gå till [ytterligare resurser](#additional-resources) om du vill ha mer information om de enskilda avsnitten.

### Konfiguration {#configuration}

1. Aktivera innehållsfragment
1. Aktivera GraphQL
1. Konfigurera Headless SDK

## Implementera din första AEM Headless-app

Detta är en översikt över vad som behövs för att implementera din första headless-app med AEM för att leverera ditt innehåll. Hur du utför dessa steg beskrivs i detalj i senare delar av den Headless Developer Journey.

1. Skapa modeller för innehållsfragment
1. Skapa innehållsfragment
1. Fråga innehåll med GraphQL

## Bästa praxis {#best-practices}

Ett headless-projekt är inte bara framgångsrikt på grund av den teknik som används, utan också på grund av god planering och projektledning. Här följer några tips som både författare och utvecklare kan använda när du planerar ditt projekt.

### Ordna ditt innehåll {#organizing-content}

* Gör strukturen så komplex som behövs, men gör den så enkel som möjligt. Enklare innehållsstrukturer effektiviserar innehållsstyrningen och förbättrar systemets prestanda.
* Prioritera återanvändning av innehåll i er strategi. Skapa undermodeller och innehållsreferenser som kan återanvändas i flera modeller och kanaler på högre nivå.
* Gör innehållsstrukturerna så självförklarande som möjligt så att skribenterna snabbt kan lära sig och anpassa sig till arbetsmomenten.
* Om du har åtkomstbegränsningar kan du försöka anpassa innehållsmodellen efter åtkomstkraven.
* När ni har åtkomstkrav bör de styra er innehållshierarki. Gruppera innehåll som redigeras av samma grupp av personer.
* Gruppera liknande innehåll i en mapp.
   * Det är troligare att en innehållsförfattare kopierar och klistrar in befintligt innehåll för att skapa nytt innehåll. Om du gör detta i samma mapp blir det därför effektivare.
   * AEM tillåter att tillåtna modeller anges per mapp så knappen **Skapa ny** bara visar de modeller som stöds på den platsen.
* Det går att förenkla skapandet av nya innehållsfragment i den infogade redigeraren för innehållsfragment om rotmappen är inställd i modellen. Sedan behöver inte administratören välja en plats, utan bara ange ett namn och kan börja redigera den nya referensen.

### Redigerar innehåll {#authoring}

* För kanalspecifika versioner av ditt innehåll bör du överväga att använda variationer för innehållsfragment. Variationer synkroniseras mot det överordnad innehållet för att effektivisera hanteringen av innehållsändringar.
* Bjud in andra innehållsproducenter att granska innehållet och ge feedback med anteckningar och kommentarer, som är tillgängliga i innehållsfragmentredigeraren och globalt över fragment i administratörskonsolen för innehållsfragment.
* Håll saker i rörelse med så få obligatoriska element som möjligt. Obligatoriska element kan blockera arbetsflödet.

### Skapar globalt innehåll {#localization}

* Upprätta regler och styrning för översättning av innehåll. Om du vill minska systembelastningen upprättar du en översättning som en asynkron process som kan köras i längre intervall. Ge tid åt kvalitetskontroll och felkorrigering av lokalisering.
* Utnyttja alla funktioner i översättningstekniksystemet som ni kan integrera med AEM som översättningsminnen.
* Förstå om multimediematerial, som bilder och videor, behöver lokaliseras.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey ska du:

* Förstå viktiga planeringsöverväganden när du utformar ditt innehåll.
* Förstå stegen för att implementera headless i AEM.
* Ha koll på vilka verktyg och AEM som krävs.
* Lär dig de bästa sätten att göra den enkla resan smidig, hålla innehållsgenereringen effektiv och se till att innehållet levereras snabbt.

Du bör fortsätta den AEM resan utan extra kostnad genom att nästa gång granska dokumentet [Så här modellerar du ditt innehåll som AEM innehållsmodeller](model-your-content.md) där du får lära dig att modellera din innehållsstruktur i AEM.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-utvecklingsresan genom att läsa dokumentet [How to Model Your Content as AEM Content Models,](model-your-content.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta den headless-resan.

* [Headless Development for AEM Sites as a Cloud Service](/help/implementing/developing/headless/introduction.md)  - En snabb introduktion som ger utvecklaren av AEM Headless de nödvändiga funktionerna
* [AEM Headless Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  - Använd dessa praktiska självstudiekurser för att utforska hur du kan använda de olika alternativen för att leverera innehåll till headless endpoints med AEM och välja vad som är rätt för dig.
* [Headless Content Management Using GraphQL APIs](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Följ den här kursen för en översikt över GraphQL API som implementerats i AEM. Autentisering via AdobeID krävs.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  - Det här GitHub-projektet innehåller exempelprogram som AEM GraphQL API:er.
* [Introduktion till arkitekturen i Adobe Experience Manager som Cloud Service](/help/core-concepts/architecture.md)  - En komplett översikt över AEM
* [Headless Getting Started Guide](/help/implementing/developing/headless/introduction.md#getting-started)  - En snabb introduktion till AEM headless-funktioner för användare som redan känner till AEM.
* [Skapa modeller](/help/assets/content-fragments/content-fragments-models.md)  för innehållsfragment - teknisk dokumentation om modeller för innehållsfragment
* [Skapa innehållsfragment](/help/assets/content-fragments/content-fragments.md)  - teknisk dokumentation om innehållsfragment
* [Fråga innehåll med GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)  - Teknisk dokumentation om GraphQL API
