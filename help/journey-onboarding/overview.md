---
title: Introduktion till as a Cloud Service onboarding-resa
description: Börja här för en översikt över den guidade resan genom introduktionsprocessen till AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# Onboarding Journey {#onboarding-journey}

Grattis till AEM as a Cloud Service! Det här dokumentet är utgångspunkten för en guidad resa genom introduktionsprocessen. Oavsett om du distribuerar ett nytt program eller migrerar ett befintligt, säkerställer den här introduktionsresan att era team har konfigurerats och tillgång till AEM as a Cloud Service.

## Introduktion {#introduction}

Onboarding är den process under vilken en utsedd systemadministratör konfigurerar AEM as a Cloud Service för din organisation. Detta inkluderar inledande etablering av molnresurser och tilldelning av användare till roller baserat på deras jobbansvar. Det innebär att varje medlem kan logga in och komma åt sina AEM as a Cloud Service resurser.

![Startresan](/help/journey-onboarding/assets/onboarding-journey.png)

Den här guiden leder dig igenom de viktigaste startämnena så att du när allt är klart får:

* Full förståelse för de olika villkoren, tjänsterna och användarna som deltar i introduktionsprocessen.
* Gör det möjligt för teamet att komma igång och ta de första stegen mot att lära sig att skapa och utveckla innehåll för ditt AEM as a Cloud Service program.

Resultatet blir:

* Ditt team kommer att konfigureras och ha tillgång till molnresurser.
* AEM får tillgång till AEM as a Cloud Service och kan börja skapa innehåll.
* AEM utvecklare och distributionsansvariga får tillgång till AEM as a Cloud Service och kan börja skapa och distribuera anpassade program.

## Koncept och mål {#concepts}

Även om det kan verka finnas mycket att lära sig när man börjar med AEM as a Cloud Service finns det bara några få logiska delar.

* **Kontraktet** - Du måste känna till ditt Adobe-kontrakt eftersom det definierar aspekter av introduktionsprocessen.
* **Admin Console** - Här hanteras användare och roller tilldelas.
* **Cloud Manager** - Det här verktyget används för att konfigurera resurser som program och miljöer. Det är också där du får åtkomst till Git och skapar rörledningar för att hantera och distribuera din anpassade kod.

Dessa begrepp kommer att beskrivas i detalj i denna introduktionsresa. Målet är att du när resan är över:

* Har gett användarna åtkomst till AEMaaCS
* Har konfigurerat de första molnresurserna för ditt projekt
* Lär dig hur du distribuerar din första kod och skapar ditt första innehåll.

I princip kommer du att komma igång med ditt nya AEM as a Cloud Service projekt!

## Målgrupp {#audience}

Startresan är särskilt skriven för **systemadministratör** av kundens nya AEM as a Cloud Service och AEM i allmänhet. Systemadministratören är den person som först kontaktas av Adobe efter att ditt AEM as a Cloud Service kontrakt har undertecknats, och det är vanligtvis den första personen som får tillgång till och ställer in dina AEM as a Cloud Service resurser. Om du läser detta är det troligtvis du som är systemadministratör.

Systemadministratören hanterar alla aspekter av organisationens AEMaaCS-användare, från åtkomst till behörigheter. Systemadministratören måste dock interagera med andra profiler på vägen.

| Persona | Beskrivning | Roll på resan |
|---|---|---|
| Systemadministratör | Målet för den här resan är att tillhandahålla molnresurser initialt och att tilldela användare lämpliga roller baserat på deras arbetsuppgifter | Hanterar alla aspekter av användare från åtkomst till behörigheter |
| Innehållsförfattare | Skapar och granskar innehåll i AEM | När de har fått tillstånd av systemadministratören kan författarna påbörja sin egen resa och skapa innehåll |
| Developer | Utvecklar AEM program som använder innehåll från olika källor | När systemadministratören har gett tillstånd kan utvecklarna påbörja sin egen resa med att utveckla lösningar |
| Distributionshanterare | Lägger till eller uppdaterar en miljö, kör pipelines och distribuerar kod AEM miljö eller kodkvalitet. | När systemadministratören har gett behörighet kan distributionscheferna påbörja sin egen resa med att hantera distributioner |

Den här introduktionsguiden visar den fullständiga processen för att komma igång som systemadministratör. Rollerna för AEM användare, utvecklare och driftsättningsansvariga utforskas kortfattat som ytterligare, valfria delar av kundresan.

>[!TIP]
>
>Om du inte AEM as a Cloud Service tidigare, men redan är bekant med AEM och migrerar från Adobes hanterade tjänster på plats, ska du kolla in [AEM as a Cloud Service migreringsresa.](/help/journey-migration/getting-started.md)

## Översikt över introduktionsresan {#overview}

I följande artiklar beskrivs grundbegreppen för introduktion och du får grundläggande kunskaper i AEM as a Cloud Service. Även om du kan gå direkt till en viss del av resan bygger många koncept på en del i tidigare artiklar. Därför rekommenderar vi att du startar i början och fortsätter sekventiellt om du inte är nybörjare.

| # | Artikel | Beskrivning | Målgrupp |
|---|---|---|---|
| 0 | Onboarding Journey | Det här dokumentet | Systemadministratör |
| 1 | [Förberedelse för introduktion](preparation.md) | Innan introduktionsprocessen börjar finns det ett antal eller förberedande steg som systemadministratören måste förstå innan han eller hon loggar in på systemet. | Systemadministratör |
| 2 | [AEM as a Cloud Service terminologi](terminology.md) | Innan du loggar in på AEMaaCS för första gången är det bra att förstå en del av terminologin i systemet och dess grundläggande struktur. | Systemadministratör |
| 3 | [Admin Console](admin-console.md) | Lär dig vad Admin Console är, hur du loggar in och hur du verifierar din profil som systemadministratör. | Systemadministratör |
| 4 | [Tilldela Cloud Manager-produktprofiler](assign-profiles-cloud-manager.md) | Granska produktprofiler för Cloud Manager och lär dig hur du tilldelar teammedlemmar till produktprofiler för Cloud Manager. | Systemadministratör |
| 5 | [Access Cloud Manager](cloud-manager.md) | Lär dig hur du får tillgång till Cloud Manager så att du kan konfigurera dina projektresurser. | Systemadministratör |
| 6 | [Skapa ett program](create-program.md) | Lär dig hur du skapar ett program med Cloud Manager. | Systemadministratör |
| 7 | [Skapa miljöer](create-environments.md) | Lär dig hur du skapar en miljö med hjälp av Cloud Manager. | Systemadministratör |
| 8 | [Tilldela AEM produktprofiler](assign-profiles-aem.md) | Lär dig hur systemadministratören tilldelar teammedlemmar AEM as a Cloud Service produktprofiler. | Systemadministratör |
| 9 | [Uppgifter för utvecklare och distributionsansvarig](developers.md) | Valfritt - Lär dig hur du som utvecklare kan komma åt och hantera Cloud Manager Git och hur du som distributionshanterare kan konfigurera pipelines och distribuera kod i Cloud Manager. | Utvecklare och driftsättningschefer |
| 10 | [AEM användaruppgifter](aem-users.md) | Valfritt - Lär dig hur du som AEM kan komma åt AEM as a Cloud Service instansen och bekanta dig med redigeringsinnehåll för AEM as a Cloud Service. | AEM |

## What&#39;s Next {#what-is-next}

Du är nu redo att påbörja din AEM as a Cloud Service introduktionsresa. Vi rekommenderar att du fortsätter till nästa del av resan och läser artikeln [Förberedelse för introduktion](preparation.md)

## AEM dokumentationsresor {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) binder samman många olika och kanske komplicerade ämnen och funktioner genom att tillhandahålla en berättarröst som hjälper läsaren, som kan vara ny att AEM, förstå och lösa ett affärsproblem från början till slut, samtidigt som man antar minimala tidigare ämnesområden eller AEM kunskap.

Dokumentation Journeys bygger på principer för god praxis, grundade på Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe konsulter och återkoppling från kundprojekt.

Om du vill veta hur Adobe rekommenderar att ditt team kommer in i ditt nya AEM as a Cloud Service program är det här du börjar!
