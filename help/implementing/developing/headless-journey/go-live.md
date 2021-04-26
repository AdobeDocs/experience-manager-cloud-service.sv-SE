---
title: Så här Live med ditt headless-program
description: I den här delen av AEM Headless Developer Journey lär du dig hur du distribuerar ett headless-program live genom att ta din lokala kod i Git och flytta den till Cloud Manager Git för CI/CD-pipeline.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 9fb18dbe60121f46dba1e11d4133e5264a6d538d
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---


# Så här Live med ditt Headless-program {#go-live}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) lär du dig hur du distribuerar ett headless-program live genom att ta din lokala kod i Git och flytta den till Cloud Manager Git för CI/CD-pipeline.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet om den AEM resan utan rubriker, [How to Put All Together - Your App and Your Content in AEM Headless](put-it-all-together.md), lärde du dig att förbereda ett eget AEM headless-projekt för publicering, och du bör nu:

* Förstå kraven för att publicera.

Den här artikeln bygger vidare på dessa grundläggande funktioner så att du förstår hur du faktiskt gör ditt AEM Headless-projekt tillgängligt.

## Mål {#objective}

Det här dokumentet hjälper dig att förstå den AEM headless-publiceringskanalen och de prestandaöverväganden du behöver känna till innan du publicerar programmet.

* Förstå AEM innehållsreplikering och cachning
* Konfigurera de verktyg som krävs för att simulera live-användning för ditt headless-program
* Säkra och skala programmet före start
* Övervaka prestanda och felsökning

## Grundläggande om innehållsreplikering och cachelagring {#content-replication-and-caching}

En komplett AEM består av en författare, en publiceringsversion och en utskicksare.

* **I författartjänsten** kan interna användare skapa, hantera och förhandsgranska innehåll.

* **Publiceringstjänsten** betraktas som Live-miljön och är vanligtvis den slutanvändare interagerar med. Innehåll som har redigerats och godkänts av författartjänsten distribueras till publiceringstjänsten.

* **Dispatcher** är en statisk webbserver som utökas med AEM. Den cachelagrar webbsidor som skapats av publiceringsinstansen för att förbättra prestandan.

Det vanligaste distributionsmönstret med AEM headless-program är att ha produktionsversionen av programmet ansluten till en AEM Publish-tjänst.

## Krav och konfiguration {#requirements-and-configuration}

1. Konfigurera en [lokal körningsmiljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#install-java) med [AEM som en molntjänst-SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
2. Installera [WKND-exempelinnehåll](/help/implementing/developing/introduction/develop-wknd-tutorial.md) och efterföljande GraphQL-slutpunkter
3. Distribuera och konfigurera en [statisk nodserver](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/production-deployment.html?lang=en#static-server).

## Säkra och skala ditt Headless-program innan du startar {#secure-and-scale-before-launch}

1. Konfigurera [tokenbaserad autentisering](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
2. Säkra webbhooks
3. Konfigurera cachelagring och skalbarhet

## Distribuera till produktion {#deploy-to-production}

### Modellstruktur jämfört med GraphQL-utdata {#structure-vs-output}

* Undvik att skapa frågor som genererar mer än 15 kB JSON (gzip-komprimerad). Långa JSON-filer är resurskrävande för att klientprogrammet ska kunna analysera.
* Undvik fler än fem kapslade nivåer av fragmenthierarkier. Ytterligare nivåer gör det svårt för innehållsförfattare att ta hänsyn till effekten av deras ändringar.
* Använd frågor med flera objekt i stället för att modellera frågor med beroendehierarkier i modellerna. På så sätt blir det flexiblare på lång sikt att omstrukturera JSON-utdata utan att man behöver göra en massa innehållsändringar.

### Maximera CDN-cacheträffrekvens {#maximize-cdn}

* Använd inte direkta GraphQL-frågor, såvida du inte begär direktinnehåll från ytan.
   * Använd i stället beständiga frågor.
   * Tillhandahåll CDN TTL över 600 sekunder så att CDN kan cachelagra dem.
   * AEM kan beräkna effekten av en modelländring av befintliga frågor.
* Dela JSON-filer/GraphQL-frågor mellan låg och hög förändringsfrekvens för innehåll för att minska klienttrafiken till CDN och tilldela högre TTL. Detta minimerar antalet CDN som validerar JSON med den ursprungliga servern.
* Om du vill göra innehåll från CDN ogiltigt använder du Mjuk tömning. På så sätt kan CDN ladda ned innehållet på nytt utan att orsaka ett cacheminne.

### Förbättra tiden för nedladdning av Headless-innehåll {#improve-download-time}

* Kontrollera att HTTP-klienter använder HTTP/2.
* Kontrollera att HTTP-klienter accepterar rubrikbegäran för gzip.
* Minimera antalet domäner som används som värd för JSON och refererade artefakter.
* Använd `Last-modified-since` för att uppdatera resurser.
* Använd `_reference`-utdata i JSON-fil för att börja hämta resurser utan att behöva tolka fullständiga JSON-filer.

## Övervakning {#monitoring}

### Kontrollera övergripande prestanda {#check-overall-performance}

* Validera förhandsgransknings- och produktionsversioner av appen
* Verifiera AEM statussidor för den aktuella tjänsttillgänglighetsstatusen
* Få resultatrapporter
   * Leveransprestanda
      * Snabbt (CDN) - kontrollera antal anrop, cachehastighet, felfrekvens, nyttolasttrafik
      * Ursprungsservrar - antal anrop, felfrekvens, CPU-belastning, nyttolaststrafik
   * Författarprestanda
      * Kontrollera antal användare, förfrågningar och inläsning
* Åtkomst till program- och utrymmesspecifika prestandarapporter
   * Kontrollera om de allmänna måtten är gröna/orange/röda när servern är på plats och identifiera sedan specifika appproblem
   * Öppna samma rapporter ovan filtrerade till program/space (t.ex. Photoshop desktop, paywall osv.)
   * Använd API:er för Splunk-logg för att få åtkomst till service- och programprestanda
   * Kontakta kundsupport om det finns andra problem.

## Felsökning {#troubleshooting}

### Felsökning {#debugging}

För att programmet ska fungera korrekt före start rekommenderar vi att du följer dessa steg som en allmän metod för felsökning:

* Validera funktionalitet och prestanda med förhandsgranskningsversionen av programmet
* Validera funktionalitet och prestanda med programmets produktionsversion
* Validera med JSON-förhandsvisningen i Content Fragment Editor
* Inspect JSON i klientprogrammet för att kontrollera om det finns problem med klientprogram eller leverans
* Inspect JSON använder GraphQL för att kontrollera om det finns problem med cachelagrat innehåll eller AEM

### Logga ett fel med stöd för {#logging-a-bug-with-support}

Följ stegen nedan för att effektivt logga ett fel med support om du behöver mer hjälp:

* Ta skärmbilder av problemet, om det behövs
* Dokumentera ett sätt att återskapa problemet
* Dokumentera innehållet som problemet återger med
* Logga ett problem via AEM supportportal med rätt prioritet

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey ska du:

* Förstå AEM innehållsreplikering och cachning.
* Lär dig hur du konfigurerar de verktyg som krävs för att simulera publicering för ditt headless-program.
* Lär dig hur du skyddar och skalar programmet innan du startar programmet.
* Lär dig övervaka prestanda- och felsökningsproblem.

Du bör fortsätta din AEM resa utan att ta hjälp av dokumentet [Post Launch](post-launch.md) där du får lära dig hur du kan behålla din headless-upplevelse.

## Ytterligare resurser {#additional-resources}
