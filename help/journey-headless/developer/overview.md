---
title: AEM Headless CMS Developer Journey
description: Läs om headless-utveckling med Adobe Experience Manager (AEM) som Headless CMS. Lär dig hur du använder funktioner som innehållsmodeller, innehållsfragment och ett GraphQL-API för att leverera headless-innehåll.
landing-page-description: Få en förståelse för innehållsleverans och implementering utan problem. Läs mer om hur ni utvecklar er strategi inom ert företag.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: ae873f8d61f3f6b79f09df100d62714e41e3b849
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 1%

---

# AEM Headless CMS Developer Journey {#aem-headless-developer-journey}

Välkommen till dokumentationen för utvecklare som inte använder Adobe Experience Manager headless CMS!

Läs om de kraftfulla och flexibla headless-funktionerna, deras funktioner och hur du använder dem i ditt första headless-utvecklingsprojekt. Den här resan ger dig all information du behöver för att utveckla din första headless-applikation.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="AEM Headless-resurser för utvecklare och avancerad dokumentation"
>abstract="Allt du behöver veta om AEM headless CMS och skapa och leverera bättre program och snabbare upplevelser."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html" text="AEM Headless developer resources"

## Introduktion {#introduction}

Den Headless-implementeringen av AEM använder Content Fragments Models och Content Fragments för att fokusera på att skapa strukturerade, kanalneutrala och återanvändbara fragment av innehåll och deras flerkanalsleverans. För att uppnå detta glömmer man att hantera sidor och komponenter på samma sätt som man gör i helstackslösningar. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av digitala upplevelser.

Den här guiden leder dig igenom headless-frågor om implementering i AEM så att du kan:

* Få en fullständig förståelse för vad headless content delivery är och dess fördelar.
* Förstå AEM headless-funktioner och hur de fungerar tillsammans för att leverera en headless-upplevelse.
* Ta de första stegen för att implementera ditt första headless-projekt från AEM.

>[!TIP]
>
> Om du föredrar att **lära dig genom att göra** och har befintliga kunskaper om AEM går du till AEM Headless-självstudiekurserna, som är ordnade enligt API och ramverk och som finns tillgängliga i [Additional Resources section](#additional-resources) (Ytterligare resurser) i slutet av det här dokumentet.

## Målgrupp {#audience}

Den här resan är utformad för utvecklare och innehåller krav, steg och tillvägagångssätt för ett AEM Headless-projekt ur utvecklarens perspektiv. Resan definierar ytterligare personligheter som utvecklaren måste interagera med för ett framgångsrikt projekt, men utgångspunkten för resan är utvecklarens.

Följande personer interagerar på den här resan.

| Persona | Beskrivning | Roll på den här resan |
|---|---|---|
| Utvecklare (målgrupp) | Har erfarenhet av att utveckla headless-program som använder innehåll från olika källor | Målgrupp för den här resan |
| Innehållsförfattare | Skapar och hanterar innehåll som levereras utan problem | Innehållsförfattare skapar innehåll som utvecklaren själv levererar. |
| Administratör | Hanterar grundkonfiguration och konfiguration av AEM | Utvecklaren arbetar tillsammans med administratören för att göra de konfigurationsändringar som behövs för utvecklingen. |
| Innehållsarkitekt | Analyserar kraven för de data som måste levereras utan huvud och definierar strukturen för dessa data | Utvecklarna arbetar tillsammans med innehållsarkitekten för att förstå datastrukturen och kraven för att kunna leverera den utan problem. |

## The Headless Developer Journey {#the-journey}

Vi kommer att ta upp många ämnen på den här resan, som kommer att ge dig grundläggande kunskaper om headless i AEM.

Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Adobe rekommenderar att du börjar i början och fortsätter sekventiellt.

| # | Artikel | Beskrivning |
|---|---|---|
| 0 | AEM Headless Developer Journey | Det här dokumentet |
| 1 | [Läs om CMS Headless Development](learn-about.md) | Läs mer om Headless Technology och när du ska använda den. |
| 2 | [Komma igång med AEM Headless as a Cloud Service](getting-started.md) | Läs om kraven för AEM Headless |
| 3 | [Sökväg till din första upplevelse med AEM Headless](path-to-first-experience.md) | Konfigurera utvecklingsmiljön och lär dig hur du integrerar en enkel app med AEM Headless |
| 4 | [Så här modellerar du innehåll](model-your-content.md) | Lär dig modellera innehållsstrukturen. |
| 5 | [Åtkomst till ditt innehåll via AEM-API:er](access-your-content.md) | Lär dig hur du använder GraphQL-frågor för att komma åt innehåll i innehållsfragment. |
| 6 | [Så här uppdaterar du innehåll via AEM Assets API:er](update-your-content.md) | Lär dig hur du använder REST API för att komma åt och uppdatera innehåll i innehållsfragment. |
| 7 | [Så här sätter du samman allt - din app och ditt innehåll i AEM Headless](put-it-all-together.md) | Lär dig hur du tar ditt AEM-projekt och förbereder det för publicering med AEM Headless SDK. |
| 8 | [Så här publicerar du med ditt headless-program](go-live.md) | Lär dig hur du distribuerar programmet live och tar din lokala kod i Git och flyttar den till Cloud Manager Git för CI/CD. |
| 9 | [Valfritt - Så här skapar du SPA-program (single page applications) med AEM](create-spa.md) | Lär dig hur du kombinerar headful och headless-leverans och hur du kan skapa redigerbara SPA med AEM SPA Editor. |

{style="table-layout:auto"}

## What&#39;s Next {#what-is-next}

Kom igång genom att checka ut nästa artikel: [Läs mer om CMS Headless Development](learn-about.md),

### Välj din egen Adventure {#choose-your-path}

Föredrar du att lära dig i din egen takt? Kolla in följande alternativ:

* Om du föredrar att **lära dig mer om headless-koncept och AEM headless-tekniker** bör du fortsätta din AEM-resa så som du rekommenderas i nästa granskning av dokumentet [Så här modellerar du ditt innehåll som AEM Content Models](model-your-content.md) där du får lära dig att modellera din innehållsstruktur i AEM.
* Om du föredrar att **lära dig genom att göra** kan du gå direkt till självstudiekursen [Komma igång med AEM Headless ](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) där du kommer direkt till AEM Headless-utvecklingen genom att implementera ett enkelt projekt för att visa AEM headless-innehåll.

## Ytterligare resurser {#additional-resources}

Dokumentationsresor visar hur AEM löser ett affärsproblem genom att tillhandahålla en berättelse som vägleder dig genom närliggande processer och funktioner. En resa visar hur flera funktioner fungerar tillsammans för att tillgodose ett enda affärsbehov.

På de här extraresorna finns mer information om hur AEM kraftfulla funktioner fungerar tillsammans.

* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM Headless-självstudiekurser](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Om du föredrar att lära dig genom att göra och ha kunskap om AEM kan du ta del av våra praktiska självstudiekurser ordnade efter API och ramverk, som utforskar hur du skapar och använder program som bygger på AEM Headless.
* [AEM Headless Translation Journey](/help/journey-headless/translation/overview.md) - Den här dokumentationsresan ger dig en bred förståelse för headless-teknik, hur AEM fungerar som headless-innehåll och hur du kan översätta det.
* [Headless Authoring Journey](/help/journey-headless/author/overview.md) - Börja här för en guidad resa med de kraftfulla och flexibla headless-funktionerna i AEM, deras funktioner och hur du modellerar ditt innehåll i ditt första headless-projekt.
* [Headless Architect Journey](/help/journey-headless/architect/overview.md) - Börja här för en introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager as a Cloud Service och hur du modellerar innehåll för ditt projekt.
* [AEM as a Cloud Service tekniska dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - Om du redan har en god förståelse för AEM och headless-teknik kan du läsa våra detaljerade tekniska dokument.
   * [Introduktion till AEM som Headless CMS](/help/headless/introduction.md)
