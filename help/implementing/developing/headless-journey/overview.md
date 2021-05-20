---
title: AEM Headless Developer Journey
description: Börja här för en guidad resa med de kraftfulla och flexibla headless-funktionerna i AEM, deras funktioner och hur du kan utnyttja dem i ditt första utvecklingsprojekt.
hide: true
hidefromtoc: true
index: false
exl-id: 4524c92a-8f19-497a-b4f2-c3e23f555d37
source-git-commit: 9e06419f25800199dea92b161bc393e6e9670697
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# AEM Headless Developer Journey {#aem-headless-developer-journey}

>[!CAUTION]
>
>UTDATERAD - Det här utkastinnehållet har ersatts av den nya [Headless Developer Journey-dokumentationen.](/help/journey-headless/developer/overview.md)

Börja här för en guidad resa med de kraftfulla och flexibla headless-funktionerna i AEM, deras funktioner och hur du kan utnyttja dem i ditt första headless-utvecklingsprojekt.

## Introduktion {#introduction}

Headless-implementering blir allt viktigare för att ni ska kunna leverera upplevelser till er målgrupp, oavsett var de finns och kanal.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter på samma sätt som traditionella lösningar med fullständiga stackar och fokuserar på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

Den här guiden leder dig igenom de viktigaste avsnitten så att du när du är klar:

* Få en fullständig förståelse för vad headless content delivery är och dess fördelar.
* Förstå AEM headless-funktioner och hur de fungerar tillsammans för att leverera en headless-upplevelse.
* Har möjlighet att ta de första stegen för att implementera ditt första AEM headless-projekt.

## Målgrupp {#audience}

Den här resan är utformad för utvecklarprofiler och innehåller krav, steg och tillvägagångssätt för ett AEM Headless-projekt ur utvecklarens perspektiv. Resan kommer att definiera ytterligare personligheter som utvecklaren måste interagera med för ett framgångsrikt projekt, men utgångspunkten för resan är utvecklarens.

Information i den här resan kan förstås vara användbar för andra personer, men viss information kommer att vara överflödig för vissa roller. Stanna kvar och vänta på kommande resor som omfattar fler roller.

## Headless Developer Journey {#the-journey}

Du kommer att utforska många ämnen under den här resan. I följande artiklar får du grundläggande kunskaper om AEM och länkar till detaljerad teknisk dokumentation.

Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Om du inte är van vid AEM rekommenderar vi att du börjar i början och fortsätter sekventiellt.

| # | Artikel | Beskrivning |
|---|---|---|
| 0 | AEM Headless Developer Journey | Det här dokumentet |
| 1 | [Läs om CMS Headless Development](learn-about.md) | Läs mer om Headless Technology och när du ska använda den. |
| 2 | [Komma igång med AEM Headless som Cloud Service](getting-started.md) | Läs om AEM Headless-krav |
| 3 | [Vägen till din första upplevelse med AEM Headless](path-to-first-experience.md) | Konfigurera utvecklingsmiljön och lär dig hur du integrerar en enkel app med AEM Headless |
| 4 | [Så här modellerar du innehåll](model-your-content.md) | Lär dig modellera innehållsstrukturen. Förverkliga sedan strukturen för Adobe Experience Manager (AEM) med Content Fragments Models och Content Fragments, för återanvändning i alla kanaler. |
| 5 | [Få åtkomst till ditt innehåll via AEM-API:er](access-your-content.md) | Lär dig hur du använder GraphQL-frågor för att komma åt innehållet i innehållsfragment. |
| 6 | [Så här uppdaterar du innehåll via AEM resurser-API:er](update-your-content.md) | Lär dig hur du använder REST API för att komma åt och uppdatera innehåll i innehållsfragment. |
| 7 | [Sammanställ allt - appen och ditt innehåll i AEM Headless](put-it-all-together.md) | Lär dig hur du tar ditt AEM, inklusive innehållsfragment, dina GraphQL-anrop, dina REST API-anrop och programmet, och förbereder det för live-publicering. |
| 8 | [Så här lever du med ditt headless-program](go-live.md) | Lär dig hur du distribuerar program live och tar din lokala kod i Git och flyttar den till Cloud Manager Git för CI/CD-pipeline. |
| 9 | [Valfritt - Så här skapar du enkelsidiga program (SPA) med AEM](create-spa.md) | När du väl förstår AEM headless-funktioner kan du testa hur du kombinerar headful och headless-leverans och lära dig hur du kan skapa redigerbara SPA med hjälp av AEM SPA Editor-ramverk. |

## What&#39;s Next {#what-is-next}

Du är nu redo att sätta igång med din resa utan Adobe Headless. Vi rekommenderar att du fortsätter till nästa del av resan och läser artikeln [Lär dig mer om CMS Headless Development.](learn-about.md)

### Välj din egen äventyr {#choose-your-path}

Adobe vill dock att du ska lyckas när du börjar med AEM Headless-projekt, oavsett vilken typ av utbildning du använder. Överväg därför dessa två alternativ.

* Om du föredrar att fortsätta **lära dig mer om headless-koncept och AEM headless-tekniker** bör du fortsätta din AEM resa utan arbetspass enligt rekommendationerna i nästa steg i dokumentet [Så här modellerar du ditt innehåll som AEM innehållsmodeller](model-your-content.md) där du lär dig att modellera din innehållsstruktur i AEM.
* Om du föredrar att **lära dig genom att göra** kan du hoppa till självstudiekursen [Komma igång med AEM Headless-on](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) där du kommer att gå direkt till AEM Headless-utveckling genom att implementera ett enkelt projekt för att visa AEM headless-innehåll.
