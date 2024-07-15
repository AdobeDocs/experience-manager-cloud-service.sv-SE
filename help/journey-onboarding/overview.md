---
title: Introduktion till AEM as a Cloud Service onboarding Journey
description: Börja här för en översikt över den guidade resan genom introduktionsprocessen till AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 2%

---


# Onboardresa {#onboarding-journey}

Grattis till att du har valt AEM as a Cloud Service! Det här dokumentet är utgångspunkten för en guidad resa genom introduktionsprocessen. Oavsett om du ska driftsätta en ny applikation eller migrera en befintlig, säkerställer den här introduktionsresan att era team har konfigurerats och tillgång till AEM as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager är en kraftfull uppsättning sammanställningsbara innehållstjänster som snabbt levererar mycket slagkraftiga, personaliserade upplevelser över alla kanaler och frigör innehåll från alla kanaler. **Edge Delivery Services** är den senaste innovationen i Adobe Experience Manager som möjliggör extrem innehållshastighet och levererar enastående upplevelser. Läs om hur du kommer igång med Edge Delivery Services genom att gå till [den här sidan](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html). Mer information om hur du använder Edge Delivery Services finns på sidan [Utvecklarsjälvstudiekurs](https://www.hlx.live/developer/tutorial).

Onboarding är den process under vilken en systemadministratör konfigurerar AEM as a Cloud Service för din organisation. I den här processen ingår inledande etablering av molnresurser och tilldelning av användare till roller baserat på deras jobbansvar. Därför kan varje medlem logga in och komma åt sin resurs på AEM as a Cloud Service.

![Startresan](/help/journey-onboarding/assets/onboarding-journey.png)

Den här guiden leder dig igenom de viktigaste startämnena så att du har följande när du är klar:

* Full förståelse för de olika villkoren, tjänsterna och användarna som deltar i introduktionsprocessen.
* Gör det möjligt för teamet att komma igång och ta de första stegen i arbetet med att skapa och utveckla innehåll för AEM as a Cloud Service-programmen.

Resultatet blir:

* Ditt team är konfigurerat och har tillgång till molnresurser.
* AEM har tillgång till AEM as a Cloud Service och kan börja skapa innehåll.
* AEM utvecklare och distributionsansvariga har tillgång till AEM as a Cloud Service och kan börja skapa och distribuera anpassade program.

## Koncept och mål {#concepts}

Även om det kan verka som att det finns mycket att lära sig när man börjar med AEM as a Cloud Service finns det bara ett fåtal logiska delar.

* **Kontraktet** - Du måste känna till ditt Adobe-kontrakt eftersom det definierar aspekter av introduktionsprocessen.
* **Admin Console** - Där användare hanteras och roller tilldelas.
* **Cloud Manager** - Det verktyg som du använder för att konfigurera resurser som program och miljöer. Det är också där du får åtkomst till Git och skapar rörledningar för att hantera och distribuera din anpassade kod.

Dessa begrepp beskrivs i detalj i den här introduktionsresan. Målet är att du när resan är över:

* Har beviljat den nödvändiga användaren åtkomst till AEM as a Cloud Service.
* Har konfigurerat de första molnresurserna för ditt projekt.
* Lär dig hur du distribuerar din första kod och skapar ditt första innehåll.

I stort sett är det bara att köra ditt nya AEM as a Cloud Service-projekt!

## Målgrupp {#audience}

Startresan är specifikt skriven för **systemadministratören** för kundens nya AEM as a Cloud Service-användare och för AEM i allmänhet. Systemadministratören är den person som först kontaktas av Adobe efter att ditt AEM as a Cloud Service-kontrakt har undertecknats. De är oftast den första personen som får tillgång till och ställer in dina resurser på AEM as a Cloud Service. Om du läser det här avsnittet är det troligtvis du som är systemadministratör.

Systemadministratören hanterar alla aspekter av organisationens AEMaaCS-användare, från åtkomst till behörigheter. Systemadministratören måste dock interagera med andra profiler på vägen.

| Persona | Beskrivning | Roll på resan |
|---|---|---|
| Systemadministratör | Målet för den här resan är att tillhandahålla molnresurser initialt och att tilldela användare lämpliga roller baserat på deras arbetsuppgifter | Hanterar alla aspekter av användare från behörighet |
| Innehållsförfattare | Skapar och granskar innehåll i AEM | När de har fått tillstånd av systemadministratören kan författarna påbörja sin egen resa och skapa innehåll |
| Developer | Utvecklar AEM program som använder innehåll från olika källor | När systemadministratören har gett tillstånd kan utvecklarna påbörja sin egen resa med att utveckla lösningar |
| Distributionshanterare | Lägger till eller uppdaterar en miljö, kör pipelines och distribuerar kod AEM miljö eller kodkvalitet. | När systemadministratören har gett behörighet kan distributionscheferna påbörja sin egen resa med att hantera distributioner |

Den här introduktionsguiden visar den fullständiga processen för att komma igång som systemadministratör. Rollerna för AEM användare, utvecklare och driftsättningsansvariga utforskas kortfattat som ytterligare, valfria delar av kundresan.

>[!TIP]
>
>Om du inte har använt AEM as a Cloud Service tidigare och är bekant med AEM och migrerar från Managed Services på plats eller Adobe ska du ta en titt på [AEM as a Cloud Service migreringsresa](/help/journey-migration/getting-started.md).

## Översikt över introduktionsresan {#overview}

I följande artiklar beskrivs grundbegreppen för introduktion och ger dig grundläggande kunskaper i AEM as a Cloud Service. Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Om du inte är van vid att komma igång rekommenderar Adobe att du startar i början och fortsätter sekventiellt.

| # | Artikel | Beskrivning | Målgrupp |
|---|---|---|---|
| 0 | Onboardresa | Det här dokumentet | Systemadministratör |
| 1 | [Förberedelse för introduktion](preparation.md) | Innan introduktionsprocessen börjar finns det ett antal eller förberedande steg som systemadministratören måste förstå innan han eller hon loggar in på systemet. | Systemadministratör |
| 2 | [AEM as a Cloud Service Terminologi](terminology.md) | Innan du loggar in på AEMaaCS för första gången är det bra att förstå en del av terminologin i systemet och dess grundläggande struktur. | Systemadministratör |
| 3 | [Admin Console](admin-console.md) | Lär dig vad Admin Console är, hur du loggar in och hur du verifierar din profil som systemadministratör. | Systemadministratör |
| 4 | [Tilldelar Cloud Manager produktprofiler](assign-profiles-cloud-manager.md) | Granska Cloud Manager produktprofiler och lär dig hur du tilldelar teammedlemmar till Cloud Manager produktprofiler. | Systemadministratör |
| 5 | [Öppna Cloud Manager](cloud-manager.md) | Lär dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser. | Systemadministratör |
| 6 | [Skapa ett program](create-program.md) | Lär dig hur du skapar ett program med Cloud Manager. | Systemadministratör |
| 7 | [Skapa miljöer](create-environments.md) | Lär dig hur du skapar en miljö med Cloud Manager. | Systemadministratör |
| 8 | [Tilldelar AEM produktprofiler](assign-profiles-aem.md) | Läs om hur systemadministratören tilldelar teammedlemmarna produktprofiler i AEM as a Cloud Service. | Systemadministratör |
| 9 | [Aktiviteter för utvecklare och distributionsansvarig](developers.md) | Som utvecklare kan du läsa om hur du kan få åtkomst till och hantera Cloud Manager Git och hur du som distributionshanterare kan konfigurera pipelines och distribuera kod i Cloud Manager. | Utvecklare och driftsättningschefer |
| 10 | [AEM användaruppgifter](aem-users.md) | Valfritt - Som AEM kan du lära dig hur du kan komma åt AEM as a Cloud Service-instansen och lära dig hur du redigerar innehåll för AEM as a Cloud Service. | AEM |

## What&#39;s Next {#what-is-next}

Nu är du redo att påbörja din AEM as a Cloud Service introduktionsresa. Du uppmuntras att fortsätta till nästa del av resan och läsa artikeln [Förberedelser för introduktion](preparation.md)

## AEM dokumentationsresor {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) knyter ihop många olika, komplicerade ämnen och funktioner. Den innehåller en berättarröst som hjälper en läsare som är nybörjare att AEM förstå och lösa ett affärsproblem från början till slut, samtidigt som man antar minimala tidigare ämnesområden eller AEM kunskap.

Dokumentation Journeys bygger på principer för god praxis, grundade på Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe konsulter och återkoppling från kundprojekt.

Om du vill veta vad Adobe rekommenderar om hur du får ditt team att komma in i ditt nya AEM as a Cloud Service-program kan du börja här!

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Introduktion till AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding.html) - I den här korta videon visas en översikt över processen för att komma igång med Cloud Service för AEM.
