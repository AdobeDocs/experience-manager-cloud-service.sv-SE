---
title: Introduktion till as a Cloud Service onboarding-resa
description: Börja här för en översikt över den guidade resan genom introduktionsprocessen till AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
source-git-commit: 98618765b405316b18110182c221ddd968c70e96
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 2%

---


# Onboardresa {#onboarding-journey}

Grattis till AEM as a Cloud Service! Det här dokumentet är utgångspunkten för en guidad resa genom introduktionsprocessen. Oavsett om du distribuerar ett nytt program eller migrerar ett befintligt, säkerställer den här introduktionsresan att era team har konfigurerats och tillgång till AEM as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager är en kraftfull uppsättning sammanställningsbara innehållstjänster som snabbt levererar mycket slagkraftiga, personaliserade upplevelser över alla kanaler och frigör innehåll från alla kanaler. **Edge Delivery Services** är den senaste innovationen i Adobe Experience Manager som möjliggör extremt snabb innehållshantering och levererar exceptionella upplevelser. Kom igång med Edge Delivery Services genom att besöka [den här sidan](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html). Mer information om hur du använder Edge Delivery Services finns i [Självstudiekurs för utvecklare](https://www.hlx.live/developer/tutorial) sida.

Onboarding är den process under vilken en utsedd systemadministratör konfigurerar AEM as a Cloud Service för din organisation. I den här processen ingår inledande etablering av molnresurser och tilldelning av användare till roller baserat på deras jobbansvar. Det innebär att varje medlem kan logga in och komma åt sin resurs på AEM as a Cloud Service.

![Startresan](/help/journey-onboarding/assets/onboarding-journey.png)

Den här guiden leder dig igenom de viktigaste startämnena så att du har följande när du är klar:

* Full förståelse för de olika villkoren, tjänsterna och användarna som deltar i introduktionsprocessen.
* Gör det möjligt för teamet att komma igång och ta de första stegen mot att lära sig att skapa och utveckla innehåll för ditt AEM as a Cloud Service program.

Resultatet blir:

* Ditt team är konfigurerat och har tillgång till molnresurser.
* AEM författare har tillgång till AEM as a Cloud Service och kan börja skapa innehåll.
* AEM utvecklare och distributionsansvariga har tillgång till AEM as a Cloud Service och kan börja skapa och distribuera anpassade program.

## Koncept och mål {#concepts}

Även om det kan verka finnas mycket att lära sig när man börjar med AEM as a Cloud Service finns det bara några få logiska delar.

* **Kontraktet** - Du måste känna till ditt Adobe-kontrakt eftersom det definierar aspekter av introduktionsprocessen.
* **Admin Console** - Där användare hanteras och roller tilldelas.
* **Cloud Manager** - Verktyget för att ställa in resurser som program och miljöer. Det är också där du får åtkomst till Git och skapar rörledningar för att hantera och distribuera din anpassade kod.

Dessa begrepp beskrivs i detalj i den här introduktionsresan. Målet är att du när resan är över:

* Har beviljat den nödvändiga användaren åtkomst till AEM as a Cloud Service.
* Har konfigurerat de första molnresurserna för ditt projekt.
* Lär dig hur du distribuerar din första kod och skapar ditt första innehåll.

I stort sett igång med ditt nya AEM as a Cloud Service projekt!

## Målgrupp {#audience}

Startresan skrivs specifikt för **systemadministratör** av kundens nya AEM as a Cloud Service och AEM i allmänhet. Systemadministratören är den person som först kontaktas av Adobe efter att ditt AEM as a Cloud Service kontrakt har undertecknats. De är oftast den första personen som får tillgång till och ställer in dina resurser på AEM as a Cloud Service. Om du läser det här avsnittet är det troligtvis du som är systemadministratör.

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
>Om du är nybörjare AEM as a Cloud Service och bekant med AEM och migrerar från Managed Services på plats eller Adobe ska du titta på [AEM as a Cloud Service migreringsresa](/help/journey-migration/getting-started.md).

## Översikt över introduktionsresan {#overview}

I följande artiklar beskrivs grundbegreppen för introduktion och du får grundläggande kunskaper i AEM as a Cloud Service. Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Om du inte är van vid att komma igång rekommenderar Adobe att du startar i början och fortsätter sekventiellt.

| # | Artikel | Beskrivning | Målgrupp |
|---|---|---|---|
| 0 | Onboardresa | Det här dokumentet | Systemadministratör |
| 1 | [Förberedelse för introduktion](preparation.md) | Innan introduktionsprocessen börjar finns det ett antal eller förberedande steg som systemadministratören måste förstå innan han eller hon loggar in på systemet. | Systemadministratör |
| 2 | [AEM as a Cloud Service terminologi](terminology.md) | Innan du loggar in på AEMaaCS för första gången är det bra att förstå en del av terminologin i systemet och dess grundläggande struktur. | Systemadministratör |
| 3 | [Admin Console](admin-console.md) | Lär dig vad Admin Console är, hur du loggar in och hur du verifierar din profil som systemadministratör. | Systemadministratör |
| 4 | [Tilldela Cloud Manager-produktprofiler](assign-profiles-cloud-manager.md) | Granska produktprofiler för Cloud Manager och lär dig hur du tilldelar teammedlemmar till produktprofiler för Cloud Manager. | Systemadministratör |
| 5 | [Access Cloud Manager](cloud-manager.md) | Lär dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser. | Systemadministratör |
| 6 | [Skapa ett program](create-program.md) | Lär dig hur du skapar ett program med Cloud Manager. | Systemadministratör |
| 7 | [Skapa miljöer](create-environments.md) | Lär dig hur du skapar en miljö med Cloud Manager. | Systemadministratör |
| 8 | [Tilldela AEM produktprofiler](assign-profiles-aem.md) | Läs om hur systemadministratören tilldelar teammedlemmar produktprofiler på AEM as a Cloud Service. | Systemadministratör |
| 9 | [Uppgifter för utvecklare och distributionsansvarig](developers.md) | Som utvecklare kan du läsa om hur du kan få åtkomst till och hantera Cloud Manager Git och hur du som distributionshanterare kan konfigurera pipelines och distribuera kod i Cloud Manager. | Utvecklare och driftsättningschefer |
| 10 | [AEM användaruppgifter](aem-users.md) | Valfritt - Som AEM kan du lära dig hur du kan komma åt AEM as a Cloud Service instansen och lära dig hur du redigerar innehåll för AEM as a Cloud Service. | AEM |

## What&#39;s Next {#what-is-next}

Du är nu redo att påbörja din AEM as a Cloud Service introduktionsresa. Du uppmanas att fortsätta till nästa del av resan och läsa artikeln [Förberedelse för introduktion](preparation.md)

## AEM dokumentationsresor {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) binder samman många olika, komplicerade ämnen och funktioner. Den innehåller en berättarröst som hjälper en läsare som är nybörjare att AEM förstå och lösa ett affärsproblem från början till slut, samtidigt som man antar minimala tidigare ämnesområden eller AEM kunskap.

Dokumentation Journeys bygger på principer för god praxis, grundade på Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe konsulter och återkoppling från kundprojekt.

Om du vill veta vad Adobe rekommenderar om hur du ska få ditt team att komma in i ditt nya AEM as a Cloud Service program kan du börja här!

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Onboarding to AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding.html) - Den här korta videon ger en översikt över Cloud Servicens introduktionsprocess för AEM.
