---
title: Introduktion till AEM as a Cloud Service onboarding Journey
description: Börja här för en översikt över den guidade resan genom introduktionsprocessen till AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 2%

---


# Onboardresa {#onboarding-journey}

Grattis till att du har valt AEM as a Cloud Service! Det här dokumentet är utgångspunkten för en guidad resa genom introduktionsprocessen. Oavsett om du distribuerar ett nytt program eller migrerar ett befintligt, kommer den här introduktionsresan att skapa era team. Det garanterar att de har tillgång till AEM as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager (AEM) ger flexibilitet i både innehållsleverans och redigering, så att teamen kan välja den bästa modellen för sina behov.

Använd [Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/overview) för snabb, iterativ redigering och snabb innehållshastighet, eller använd den traditionella publiceringstjänsten för en robust företagspubliceringsmodell. Med båda metoderna kan organisationer leverera exceptionella digitala upplevelser på det sätt som passar dem bäst. Om du vill komma igång med Edge Delivery Services kan du utforska [Edge Delivery Services Overview](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/overview) och läsa mer om moderna redigeringsalternativ i [redigeringshandboken](https://www.aem.live/docs/authoring-guide).

Onboarding är den process under vilken en systemadministratör konfigurerar AEM as a Cloud Service för din organisation. I den här processen ingår inledande etablering av molnresurser och tilldelning av användare till roller baserat på deras jobbansvar. Därför kan varje medlem logga in och komma åt sin resurs på AEM as a Cloud Service.

![Startresan](/help/journey-onboarding/assets/onboarding-journey.png).

Den här guiden leder dig igenom de viktigaste startämnena så att du har följande när du är klar:

* Full förståelse för de olika villkoren, tjänsterna och användarna som deltar i introduktionsprocessen.
* Gör det möjligt för teamet att komma igång och ta de första stegen i arbetet med att skapa och utveckla innehåll för AEM as a Cloud Service-programmen.

Resultatet blir:

* Ditt team är konfigurerat och har tillgång till molnresurser.
* AEM författare har tillgång till AEM as a Cloud Service och kan börja skapa innehåll.
* AEM utvecklare och driftsättningsansvariga har tillgång till AEM as a Cloud Service och kan börja skapa och distribuera anpassade program.

## Koncept och mål {#concepts}

<!-- Although there may appear to be a lot to learn when getting started with AEM as a Cloud Service, conceptually there are only a few, logical pieces.-->

Startresan för AEM as a Cloud Service har följande centrala element:

* **Kontrakt** - Granska ditt Adobe-kontrakt om du vill veta mer om viktiga detaljer i introduktionsprocessen.
* **Experience Hub** - Använd [experience.adobe.com](https://experience.adobe.com/) som central startpunkt för AEM-funktioner. Experience Hub anpassar sig efter era personuppgifter och rättigheter så att ni kan arbeta effektivt. Navigera härifrån till:
   * **Admin Console** - Hantera användare och tilldela roller.
   * **Cloud Manager** - Konfigurera program och miljöer, få tillgång till Git och skapa pipelines för att hantera och distribuera anpassad kod.
   * **Webbplatser** - Skapa, hantera och leverera digitala upplevelser. (Licensbaserat berättigande)
   * **Assets** - Ordna, lagra och distribuera dina digitala resurser. (Licensbaserat berättigande)
   * **Forms** - Skapa och hantera adaptiva och responsiva formulär. (Licensbaserat berättigande)

Dessa begrepp beskrivs i detalj i den här introduktionsresan. Målet är att du kan göra följande i slutet av resan:

* Ge den användare som behövs åtkomst till AEM as a Cloud Service.
* Konfigurera de första molnresurserna för ditt projekt.
* Lär dig hur du distribuerar din första kod och skapar ditt första innehåll.

I stort sett är det bara att köra ditt nya AEM as a Cloud Service-projekt!

## Målgrupp {#audience}

Startresan är specifikt skriven för **systemadministratören** för kunder som inte är tidigare än AEM as a Cloud Service och för AEM i allmänhet. Systemadministratören är den person som Adobe kontaktar först efter det att ditt AEM as a Cloud Service-kontrakt har undertecknats. De är oftast den första personen som får tillgång till och ställer in dina resurser på AEM as a Cloud Service. Om du läser det här avsnittet är det troligtvis du som är systemadministratör.

Systemadministratören hanterar alla aspekter av organisationens AEMaaCS-användare, från åtkomst till behörigheter. Systemadministratören måste dock interagera med andra profiler på vägen.

| Persona | Beskrivning | Roll på resan |
| --- | --- | --- |
| Systemadministratör | Målet för den här resan är att tillhandahålla molnresurser initialt och att tilldela användare till lämpliga roller baserat på deras arbetsuppgifter. | Med den här rollen kan du hantera alla aspekter av användare från åtkomst till behörigheter. |
| Innehållsförfattare | Skapar och granskar innehåll i AEM. | När de har fått tillstånd av systemadministratören kan författarna själva börja skapa innehåll. |
| Developer | Utvecklar AEM-program som använder innehåll från olika källor. | När systemadministratören har gett tillstånd kan utvecklarna själva börja utveckla lösningar. |
| Distributionshanterare | Lägger till eller uppdaterar en miljö, kör pipelines och distribuerar kod till AEM-miljön eller kodkvaliteten. | När de har tilldelats behörigheter av systemadministratören kan distributionscheferna påbörja sin egen resa med att hantera distributioner. |

Den här introduktionsguiden visar den fullständiga processen för att komma igång som systemadministratör. Rollerna för AEM-användare, utvecklare och driftsättningsansvariga utforskas kortfattat som ytterligare, valfria delar av kundresan.

>[!TIP]
>
>Om du inte har använt AEM as a Cloud Service tidigare och är bekant med AEM och migrerar från en lokal eller Adobe Managed Services ska du titta på [AEM as a Cloud Service migreringsresa](/help/journey-migration/getting-started.md).

## Översikt över introduktionsresan {#overview}

I följande artiklar beskrivs grundbegreppen för introduktion och ger dig grundläggande kunskaper i AEM as a Cloud Service. Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Om du inte är van vid att komma igång rekommenderar Adobe att du startar i början och fortsätter sekventiellt.

| | Artikel | Beskrivning | Målgrupp |
| --- | --- | --- | --- |
| 0 | Onboardresa | Det här dokumentet | Systemadministratör |
| 1 | [Förberedelse för introduktion](preparation.md) | Innan introduktionsprocessen börjar finns det ett antal eller förberedande steg som systemadministratören måste förstå innan han eller hon loggar in på systemet. | Systemadministratör |
| 2 | [AEM as a Cloud Service Terminologi](terminology.md) | Innan du loggar in på AEMaaCS för första gången är det bra att förstå en del av terminologin i systemet och dess grundläggande struktur. | Systemadministratör |
| 3 | [Admin Console](admin-console.md) | Lär dig vad Admin Console är, hur du loggar in och hur du verifierar din profil som systemadministratör. | Systemadministratör |
| 4 | [Tilldelar Cloud Manager produktprofiler](assign-profiles-cloud-manager.md) | Läs om Cloud Manager produktprofiler och hur du tilldelar teammedlemmar till Cloud Manager produktprofiler. | Systemadministratör |
| 5 | [Öppna Experience Hub](/help/experience-hub.md) | Använd Experience Hub som fungerar som en enhetlig, personlig ingångspunkt till AEM ekosystem. | AEM-användare |
| 6 | [Öppna Cloud Manager](cloud-manager.md) | Lär dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser. | Systemadministratör |
| 7 | [Skapa ett program](create-program.md) | Lär dig hur du skapar ett program med Cloud Manager. | Systemadministratör |
| 8 | [Skapa miljöer](create-environments.md) | Lär dig hur du skapar en miljö med Cloud Manager. | Systemadministratör |
| 9 | [Tilldelar AEM produktprofiler](assign-profiles-aem.md) | Läs om hur systemadministratören tilldelar teammedlemmar produktprofiler i AEM as a Cloud Service. | Systemadministratör |
| 10 | [Aktiviteter för utvecklare och distributionsansvarig](developers.md) | Valfritt - Som utvecklare kan du lära dig hur du kommer åt och hanterar Cloud Manager Git. Som driftsättningshanterare får du lära dig hur du konfigurerar pipelines och distribuerar kod i Cloud Manager. | Utvecklare och driftsättningschefer |
| 11 | [AEM användaruppgifter](aem-users.md) | Valfritt - Som AEM-författare kan du lära dig hur du kan komma åt AEM as a Cloud Service-instansen och lära dig hur du redigerar innehåll för AEM as a Cloud Service. | AEM-användare |

## Vad kommer härnäst? {#what-is-next}

Nu är du redo att påbörja din AEM as a Cloud Service introduktionsresa. Du uppmuntras att fortsätta till nästa del av resan och läsa artikeln [Förberedelser för introduktion](preparation.md)

## AEM dokumentationsresor {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) knyter ihop många olika, komplicerade ämnen och funktioner. Det innehåller en berättarröst som hjälper läsare som är nybörjare på AEM att förstå och lösa ett affärsproblem från början till slut, samtidigt som man utgår från minimala tidigare ämnesområden eller AEM kunskaper.

Dokumentationsresor är utformade utifrån principer för bästa praxis. De får information med hjälp av Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe konsulter och feedback från kundprojekt.

Börja här om du vill veta vad Adobe rekommenderar om hur du får ditt team att komma in i ditt nya AEM as a Cloud Service-program.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Onboarding to AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding) - I den här korta videon ges en översikt över Cloud Service introduktionsprocess för AEM.
