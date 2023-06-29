---
title: Så här Live med ditt headless-program
description: I den här delen av AEM Headless Developer Journey lär du dig hur du distribuerar ett headless-program live genom att ta din lokala kod i Git och flytta den till Cloud Manager Git för CI/CD-pipeline.
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---

# Så här Live med ditt headless-program {#go-live}

I den här delen av [AEM Headless Developer Journey](overview.md)Lär dig hur du distribuerar ett headless-program direkt genom att ta din lokala kod i Git och flytta den till Cloud Manager Git för CI/CD-pipeline.

## Story hittills {#story-so-far}

I det föregående dokumentet om den AEM resan utan headless [Så här sätter du samman allt - din app och ditt innehåll i AEM utan rubriker](put-it-all-together.md) du lärde dig att använda de AEM utvecklingsverktygen för att sätta ihop alla aspekter av projektet.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du förbereder ett eget AEM headless-projekt för publicering.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå den AEM rubrikfria publiceringsprocessen och de prestandaöverväganden du måste vara medveten om innan du publicerar programmet.

* Säkra och skala programmet före start
* Övervaka prestanda och felsökning

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
Följ de bästa metoderna nedan för att göra ditt AEM headless-program klart för start.

## Säkra och skala ditt Headless-program innan det startas {#secure-and-scale-before-launch}

1. Konfigurera [Tokenbaserad autentisering](/help/headless/security/authentication.md) med dina GraphQL-förfrågningar
1. Konfigurera [Cachelagring](/help/implementing/dispatcher/caching.md).

## Modellstruktur jämfört med GraphQL Output {#structure-vs-output}

* Undvik att skapa frågor som genererar mer än 15 kB JSON (gzip-komprimerad). Långa JSON-filer är resurskrävande för att klientprogrammet ska kunna analysera.
* Undvik fler än fem kapslade nivåer av fragmenthierarkier. Ytterligare nivåer gör det svårt för innehållsförfattare att ta hänsyn till effekten av deras ändringar.
* Använd frågor med flera objekt i stället för att modellera frågor med beroendehierarkier i modellerna. På så sätt blir det flexiblare på lång sikt att strukturera om JSON-utdata utan att behöva göra många innehållsändringar.

## Maximera CDN-cacheträffrekvens {#maximize-cdn}

* Använd inte direkta GraphQL-frågor om du inte begär direktinnehåll från ytan.
   * Använd beständiga frågor när det är möjligt.
   * Tillhandahåll CDN TTL över 600 sekunder för att CDN ska cachelagra dem.
   * AEM kan beräkna effekten av en modelländring av befintliga frågor.
* Dela JSON-filer/GraphQL-frågor mellan låg och hög förändringsfrekvens för innehåll, så att du kan minska klienttrafiken till CDN och tilldela högre TTL. Detta minimerar antalet CDN som validerar JSON med den ursprungliga servern.
* Om du vill göra innehåll från CDN ogiltigt använder du Mjuk tömning. På så sätt kan CDN ladda ned innehållet på nytt utan att orsaka ett cacheminne.

## Förkorta nedladdningstiden för headless Content {#improve-download-time}

* Kontrollera att HTTP-klienter använder HTTP/2.
* Kontrollera att HTTP-klienter accepterar rubrikbegäran för gzip.
* Minimera antalet domäner som används som värd för JSON och refererade artefakter.
* Utnyttja `Last-modified-since` för att uppdatera resurser.
* Använd `_reference` i JSON-fil för att börja ladda ned resurser utan att behöva tolka fullständiga JSON-filer.

## Distribuera till produktion {#deploy-to-production}

När du har testat allt och fungerar som det ska kan du skicka koduppdateringarna till en [centraliserad Git-databas i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

När uppdateringarna har överförts till Cloud Manager kan de distribueras till AEM as a Cloud Service med [Cloud Managers pipeline för CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

Du kan börja distribuera koden genom att utnyttja Cloud Managers CI/CD-pipeline, som är omfattande och täcks [här](/help/implementing/deploying/overview.md).

## Prestandaövervakning {#performance-monitoring}

För att användarna ska få bästa möjliga upplevelse när de använder det AEM headless-programmet är det viktigt att du övervakar nyckeltal enligt beskrivningen nedan:

* Validera förhandsgransknings- och produktionsversioner av appen
* Verifiera AEM statussidor för den aktuella tjänsttillgänglighetsstatusen
* Få resultatrapporter
   * Leveransprestanda
      * CDN-prestanda (snabbt) - kontrollera antal anrop, cachehastighet, felfrekvens och nyttolasttrafik
      * Ursprungsservrar - antal anrop, felfrekvens, CPU-belastning, nyttolaststrafik
   * Författarprestanda
      * Kontrollera antal användare, förfrågningar och inläsning
* Åtkomst till program- och utrymmesspecifika prestandarappar
   * Kontrollera om de allmänna måtten är gröna/orange/röda när servern är på plats och identifiera sedan specifika appproblem
   * Öppna samma rapporter ovan filtrerade till program eller utrymme (t.ex. Photoshop desktop, paywall)
   * Använd API:er för Splunk-logg för att få åtkomst till service- och programprestanda
   * Kontakta kundsupport om det finns andra problem.

## Felsökning {#troubleshooting}

### Felsökning {#debugging}

Följ dessa metodtips som ett allmänt tillvägagångssätt vid felsökning:

* Validera funktionalitet och prestanda med förhandsgranskningsversionen av programmet
* Validera funktionalitet och prestanda med programmets produktionsversion
* Validera med JSON-förhandsvisningen i Content Fragment Editor
* Inspect JSON i klientprogrammet för att kontrollera om det finns problem med klientprogram eller leverans
* Inspect the JSON using GraphQL to check for the presence of issues related to cached content or AEM

### Logga ett fel med support {#logging-a-bug-with-support}

Så här loggar du effektivt ett fel med support om du behöver mer hjälp:

* Ta skärmbilder av problemet, om det behövs
* Dokumentera ett sätt att återskapa problemet
* Dokumentera innehållet som problemet återger med
* Logga ett problem via AEM supportportal med rätt prioritet

## Resan slutar - eller gör det? {#journey-ends}

Grattis! Du har slutfört AEM Headless Developer Journey! Nu bör du förstå:

* Skillnaden mellan headless och headful content delivery.
* AEM headless-funktioner.
* Organisera och AEM Headless-projekt.
* Skapa innehåll utan rubriker i AEM.
* Så här hämtar och uppdaterar du headless-innehåll i AEM.
* Så här lever du med ett AEM Headless-projekt.
* Vad du ska göra efter det att du är klar.

Antingen har du redan startat ditt första AEM Headless-projekt eller så har du nu all den kunskap du behöver för att göra det. Bra jobbat!

### Utforska Single Page-program {#explore-spa}

De headless butikerna i AEM behöver inte stanna här. Du kanske kommer ihåg i [Komma igång med en del av resan](getting-started.md#integration-levels) Vi diskuterade kortfattat hur AEM inte bara stöder headless-leverans och traditionella fullstacksmodeller, utan också kan stödja hybridmodeller som kombinerar fördelarna med båda.

Om den här typen av flexibilitet är något du behöver för ditt projekt kan du fortsätta med den valfria, extra delen av resan, [Skapa enkelsidiga program (SPA) med AEM.](create-spa.md)

## Ytterligare resurser {#additional-resources}

* [En översikt över distribuering till AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Använd Cloud Manager för att distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integrera Cloud Manager Git-databasen med en extern Git-databas och distribuera ett projekt till AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
