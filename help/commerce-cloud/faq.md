---
title: AEM - Magento-integrering med Commerce Integration Framework - frågor och svar
description: AEM - Magento-integrering med Commerce Integration Framework - frågor och svar
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# AEM - Magento-integrering med Commerce Integration Framework - frågor och svar


## 1. Används GraphQL bara för Magento eller kommer det att vara tillgängligt för frågor som har skapats i AEM JCR?

Adobe har antagit Magento&#39;s GraphQL API:er som dess officiella e-handels-API för alla handelsrelaterade data. Därför använder AEM GraphQL för att utbyta affärsdata med Magento och med valfri e-handelsmotor via I/O Runtime.

## 2. Hur kommer Adobe I/O till spel? Pratar AEM med Magento direkt?

AEM kan ansluta direkt till Magento utan ett I/O-körningslager. Om det finns ett behov av att integrera en icke-Magento-e-handelsserver (tredjepartslösning) med AEM kan I/O-körtidsplattformen användas som värd för mappningslagret för att ansluta API:erna för Magento GraphQL till andra tredjepartslösningar-API:er. Mer information finns i denna [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference). För lösningar som inte är Magento konfigureras AEM att peka mot I/O-körningens slutpunkt.

I/O Runtime-plattformen kan också användas för att utöka eller anpassa e-handelstjänster. För den här typen av användningsfall anropar du I/O Runtime-slutpunkten som sedan är värd för en anpassad implementering av respektive tjänst. Användningsfall för integrering och tillägg kan kombineras.

## 3. Kan produktresurser (bilder) lagras och refereras från AEM via Magento Admin? Hur kan resurser från Dynamic Media förbrukas?

Det finns för närvarande ingen integrering mellan AEM Assets och Magento. Som en tillfällig lösning kan du lagra produktresurser (bilder) i AEM Assets, men du måste lagra resursens URL:er manuellt i Magento. Dynamic Media ingår nu i AEM Assets och fungerar på samma sätt.

## 4. Spelar det någon roll var Magento är i drift? (Lokalt eller i molnet)

Det spelar ingen roll var Magento är i drift. Integrationen och den nya AEM Venia store fungerar oavsett distributionsmodell. Om den distribueras baserat på den godkända E2E-referensarkitekturen körs E2E-tester mot nyckeltal för prestanda som samlats in och som representerar en företagskunds profil. Detta ger dig ytterligare information som du kan använda som riktmärke.

## 5. Hur skapas katalogsidor eller produktsidor i AEM? Hur kvarstår de i AEM?

Katalogsidor och produktsidor skapas och cachelagras dynamiskt i AEM baserat på generiska katalog- och produktsidmallar. Inga produkt- eller katalogdata importeras och lagras i AEM.

## 6. Cachelagra även priser och andra data via Dispatcher. Blir det ofta en cachedomål?

Dynamiska data som pris eller lager cachelagras inte i Dispatcher. Dynamiska data hämtas på klientsidan med webbkomponenter direkt via GraphQL API:er. Endast statiska data (som produkt- eller kategoridata) cachelagras i Dispatcher. Om produktdata ändras måste cacheminnet ogiltigförklaras.

## 7. Hur fungerar cacheogiltigförklaring för AEM Dispatcher med AEM-Magento?

Vi rekommenderar att du konfigurerar en TTL-baserad cacheogiltigförklaring för sidor som cachelagrats på Dispatcher. För dynamisk information som pris eller aktie rekommenderar vi att du återger datumet på klientsidan. Mer information om TTL-baserad cacheogiltigförklaring finns i [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 8. Varför använder du inte We.Retail?

Temat Venia (som utvecklats av Magento) används som är mobilt först och i linje med Magento’s PWA. Temat Venia representerar de senaste villkoren för CSS-format och AEM kärnkomponenter.

## 9. När ni uppdaterar produktdata i Magento, är det en reell satsning på AEM? Eller är det en gruppbearbetning?

Det CIF-tillägg som används med AEM Cloud Service gör att data kan flöda från Magento till AEM on demand. Detta är alltså inte en push-process i realtid eller en batchprocess när det finns en uppdatering i Magento.

## 10. Finns det någon rekommendation om enhetlig sökning i allt AEM innehåll med Commerce?

En referensimplementering av produktsökningar tillhandahålls, men ingen enhetlig sökning med innehåll. Den här funktionen är vanligtvis mycket kundspecifik och bättre på en projektspecifik nivå.

## 11. Hur fungerar sökningen med AEM-Magento med CIF?

CIF innehåller komponenterna Sökfält och Sökresultat. Sökfältskomponenten skickar en GraphQL-begäran med söktermen till Magento. Magento returnerar sedan en produktlista som innehåller produktnamn, pris, SLUG osv. Sökresultatkomponenten visar sedan sökresultaten i en gallerivy på en sökresultatsida som skapats i AEM. Sökfunktionen stöder grundläggande textsökning. Vi använder SLUG/url-tangenten för att skapa en referens till PDP.

## 11. Hur kan produktdata användas i MSM eller översättningar?

Produktdata är vanligtvis redan översatta i PIM eller Magento. AEM - Magento-integrering stöder anslutningen till flera Magento butiker och butiksvyer. I en MSM-konfiguration är vanligtvis en AEM plats länkad till en Magento store-vy.

## 13. Hur fungerar CIF tillsammans med andra handelsplattformar?

Integrering med tredjepartslösningar som andra e-handelslösningar (ej Magento) görs via I/O Runtime-plattformen.  Vi har byggt en [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference) för att visa hur detta görs. Detta gör det möjligt att återanvända [AEM CIF Cloud Connector](https://github.com/adobe/commerce-cif-connector) och [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) genom att visa Magento GraphQL API:t ovanpå valfri tredjepartsplattform. För att erbjuda maximal flexibilitet och skalbarhet används detta integreringslager på [Adobe I/O Runtime serverlösa](https://www.adobe.io/apis/experienceplatform/runtime.html)plattform.

## 14. Finns det något sätt att förbättra produktdata med kommersiell text? Var gör du det här? I AEM eller i Magento?

Det finns flera sätt att uppnå detta och det beror på användningsfallet. Ett sätt är att arbeta med anpassade attribut. Tillåt AEM att mutera dessa fält i AEM produktredigerare och synkronisera data tillbaka till PIM. Ett annat alternativ är att utnyttja AEM Experience Fragments som läggs in på produktsidorna.

## 15. Kommer integreringen mellan AEM-Magento att förändras när Adobe I/O Runtime-plattformen används?

Kunder som vill utöka e-handelstjänsterna kan använda samma integrerings- och skrivåtgärdssekvenser som finns på I/O Runtime-plattformen för att mata in affärslogik och berika e-handelstjänsterna.

## 16. Eftersom AEM skapar produkt- och katalogsidor dynamiskt baserat på en allmän mall i AEM, vad skulle jag se om jag skulle öppna CRXDE Lite och kontrollera under innehållet? Skulle jag kunna se ett helt produktträd baserat på produkterna i Magento? Om inte, hur skulle en författare förbättra dessa sidor?

Det finns inga JCR-kataloger eller produktsidor längre. Se fråga 12.

## 17. Lagrar SPA förarbete med AEM SPA?

AEM kan användas som redigeringsverktyg för alla typer av butiker. Hybridåtergivning används för närvarande för den nya butikens framsida. I framtiden kommer AEM att användas för att skapa med SPA och PWA.

## 18. Hur spelar PIM in i detta ramverk?

PIM-data exponeras för AEM och klienter via GraphQL-begäranden. Vi rekommenderar att PIM integreras med e-handelsmotorn (Magento eller annan) så att PIM-data kan hämtas från handelsmotorn.

## 19. Hur kan vi säkerställa PCI-kompatibilitet när vi använder AEM för hela presentationslagret?

När du använder AEM på AMS- och Magento-molndistribution är det obligatoriskt att använda abstrakta betalningsmetoder. Detta innebär att webbläsarklienten kommunicerar direkt med betalgatewayleverantören så att varken molnen Adobe eller Magento rymmer eller skickar kortinnehavardata. Den här metoden täcker PCI-kompatibilitet för tekniska stackar och datacenter. Det finns dock ytterligare saker att tänka på som helt PCI-kompatibla, till exempel hur medarbetarna interagerar med systemet och data. Mer information om Magento PCI-kompatibilitet finns på https://magento.com/pci-compliance

## 20. Hur begär jag en I/O Runtime-testlicens?

Du kan begära en testlicens att använda I/O Runtime [här](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md).



