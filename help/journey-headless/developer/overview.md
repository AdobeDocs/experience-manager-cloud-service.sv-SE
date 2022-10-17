---
title: AEM Headless Developer Journey
description: Lär dig utveckla projekt för headless content delivery med Adobe Experience Manager (AEM) som Headless CMS. Lär dig hur du använder funktioner som innehållsmodeller, innehållsfragment och ett GraphQL-API för att skapa headless-upplevelser.
landing-page-description: Få en förståelse för innehållsleverans och implementering utan problem. Läs mer om hur ni utvecklar er strategi inom ert företag.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 2d0856b7370b6b50935378ad26c7361e95820f4d
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# AEM Headless Developer Journey {#aem-headless-developer-journey}

Börja här för en guidad resa genom [!DNL Adobe Experience Manager as a Cloud Service] (AEM) när det används som ett CMS-system (Headless Content Management System). Lär dig mer om de kraftfulla och flexibla headless-funktionerna, deras funktioner och hur du kan utnyttja dem i ditt första headless-utvecklingsprojekt. Den här resan ger dig all information du behöver för att utveckla din första headless-applikation.

## Introduktion {#introduction}

Vid den Headless-implementeringen av AEM används Content Fragments-modeller och Content Fragments för att fokusera på att skapa strukturerade, kanalneutrala och återanvändbara fragment av innehåll och deras flerkanalsleverans. För att uppnå detta glömmer man att hantera sidor och komponenter på samma sätt som man gör i helstackslösningar. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av digitala upplevelser.

Den här guiden leder dig igenom de mest rubrikfria implementeringsämnena i AEM så att du när du är klar:

* Få en fullständig förståelse för vad headless content delivery är och dess fördelar.
* Förstå AEM headless-funktioner och hur de fungerar tillsammans för att leverera en headless-upplevelse.
* Har möjlighet att ta de första stegen för att implementera ditt första AEM headless-projekt.

## AEM dokumentationsresor {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) binder samman många olika och kanske komplicerade ämnen och funktioner genom att tillhandahålla en berättarröst som hjälper läsaren, som kan vara ny att AEM, förstå och lösa ett affärsproblem från början till slut, samtidigt som man antar minimala tidigare ämnesområden eller AEM kunskap.

Dokumentation Journeys bygger på principer för god praxis, grundade på Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe-konsulter och återkoppling från kundprojekt.

Om du vill veta hur Adobe rekommenderar att man löser problem med headless business case med AEM, [AEM Headless Journeys](/help/journey-documentation/documentation-journeys.md) var du ska börja.

>[!TIP]
>
> Om du föredrar att **lära sig göra** och tekniskt sett finns med på självstudiekurserna AEM Headless, som är ordnade i API och ramverk och finns i [Avsnittet Ytterligare resurser](#additional-resources) i slutet av det här dokumentet.

## Målgrupp {#audience}

Den här resan är utformad för utvecklarprofiler och innehåller krav, steg och tillvägagångssätt för ett AEM Headless-projekt ur utvecklarens perspektiv. Resan definierar ytterligare personligheter som utvecklaren måste interagera med för ett framgångsrikt projekt, men utgångspunkten för resan är utvecklarens.

Följande personer interagerar på den här resan.

| Persona | Beskrivning | Roll på den här resan |
|---|---|---|
| Utvecklare (målgrupp) | Har erfarenhet av att utveckla headless-program som använder innehåll från olika källor | Målgrupp för den här resan |
| Innehållsförfattare | Skapar och hanterar innehåll som levereras utan problem | Innehållsförfattare skapar innehåll som utvecklaren själv levererar. |
| Administratör | Hanterar AEM grundinställningar och konfiguration | Utvecklaren arbetar tillsammans med administratören för att göra de konfigurationsändringar som behövs för utvecklingen. |
| Innehållsarkitekt | Analyserar kraven för de data som måste levereras utan huvud och definierar strukturen för dessa data | Utvecklarna arbetar tillsammans med innehållsarkitekten för att förstå datastrukturen och kraven för att kunna leverera den utan problem. |

Information i den här resan kan vara användbar för alla personer, men viss information kanske inte behövs för vissa roller. Stanna kvar på [kommande resor som omfattar ytterligare roller.](/help/journey-documentation/documentation-journeys.md#journeys)

## The Headless Developer Journey {#the-journey}

Du kommer att utforska många ämnen under den här resan. I följande artiklar får du grundläggande kunskaper om AEM och länkar till detaljerad teknisk dokumentation.

Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Om du inte är van vid AEM rekommenderar vi att du börjar i början och fortsätter sekventiellt.

| # | Artikel | Beskrivning |
|---|---|---|
| 0 | AEM Headless Developer Journey | Det här dokumentet |
| 1 | [Läs om CMS Headless Development](learn-about.md) | Läs mer om Headless Technology och när du ska använda den. |
| 2 | [Komma igång med AEM Headless as a Cloud Service](getting-started.md) | Läs om AEM Headless-krav |
| 3 | [Vägen till din första upplevelse med AEM Headless](path-to-first-experience.md) | Konfigurera utvecklingsmiljön och lär dig hur du integrerar en enkel app med AEM Headless |
| 4 | [Så här modellerar du innehåll](model-your-content.md) | Lär dig modellera innehållsstrukturen. Förverkliga sedan strukturen för Adobe Experience Manager (AEM) med Content Fragments Models och Content Fragments, för återanvändning i alla kanaler. |
| 5 | [Få åtkomst till ditt innehåll via AEM-API:er](access-your-content.md) | Lär dig hur du använder GraphQL-frågor för att komma åt innehållet i innehållsfragment. |
| 6 | [Så här uppdaterar du innehåll via AEM Assets API:er](update-your-content.md) | Lär dig hur du använder REST API för att komma åt och uppdatera innehåll i innehållsfragment. |
| 7 | [Sammanställ allt - appen och ditt innehåll i AEM Headless](put-it-all-together.md) | Lär dig hur du tar ditt AEM och förbereder det för publicering med AEM Headless SDK. |
| 8 | [Så här lever du med ditt headless-program](go-live.md) | Lär dig hur du distribuerar program live och tar din lokala kod i Git och flyttar den till Cloud Manager Git för CI/CD-pipeline. |
| 9 | [Valfritt - Så här skapar du enkelsidiga program (SPA) med AEM](create-spa.md) | När du väl förstår AEM headless-funktioner kan du testa hur du kombinerar headful och headless-leverans och lära dig hur du kan skapa redigerbara SPA med hjälp av AEM SPA Editor-ramverk. |

## What&#39;s Next {#what-is-next}

Du är nu redo att sätta igång med din resa utan Adobe Headless. Vi rekommenderar att du fortsätter till nästa del av resan och läser artikeln [Läs om CMS Headless Development.](learn-about.md)

### Välj egen Adventure {#choose-your-path}

Adobe vill dock att du ska lyckas när du börjar med AEM Headless-projekt, oavsett vilken typ av utbildning du använder. Överväg därför dessa två alternativ.

* Om du föredrar att fortsätta **lära sig om headless-koncept och AEM headless-teknik** bör du fortsätta din AEM resa utan att ha något att göra, enligt vad som rekommenderas i nästa granskning av dokumentet [Så här modellerar du innehåll som AEM innehållsmodeller](model-your-content.md) där du lär dig att utforma innehållsstrukturen i AEM.
* Om du föredrar att **lära sig göra** går du till [Komma igång med AEM självstudiekurs utan hörn](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) där du kommer att gå direkt in i AEM Headless-utveckling genom att implementera ett enkelt projekt som visar AEM headless-innehåll.

## Ytterligare resurser {#additional-resources}

Dokumentationsresor visar hur AEM löser ett affärsproblem genom att tillhandahålla en berättelse som vägleder dig genom komplexa, sammanhörande processer och funktioner. En resa visar hur flera funktioner fungerar tillsammans för att tillgodose ett enda affärsbehov.

Som sådana resor är utformade för att stå på egen hand. Ett antal av dem kan dock vara relaterade till varandra. Kolla in de här extra resorna för mer information om hur AEM kraftfulla funktioner fungerar tillsammans.

* [AEM Headless-självstudiekurser](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Om du föredrar att lära dig genom att göra något och är tekniskt inriktad kan du ta del av våra praktiska självstudiekurser ordnade efter API och ramverk, som utforskar att skapa och använda program som bygger på AEM Headless.
* [AEM Headless Translation Journey](/help/journey-headless/translation/overview.md) - Den här dokumentationsresan ger er en bred förståelse för headless-teknik, hur AEM levererar headless-innehåll och hur ni kan översätta det.
* [Headless Authoring Journey](/help/journey-headless/author/overview.md) - Börja här för att få en guidad resa genom de kraftfulla och flexibla headless-funktionerna i AEM, deras funktioner och hur du modellerar ditt innehåll i ditt första headless-projekt.
* [Headless Architect Journey](/help/journey-headless/architect/overview.md) - Börja här för att få en introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager as a Cloud Service och hur du skapar material för ditt projekt.
* [AEM as a Cloud Service teknisk dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - Om du redan har en god förståelse för AEM och headless-teknik kan du behöva läsa våra detaljerade tekniska dokument direkt.
