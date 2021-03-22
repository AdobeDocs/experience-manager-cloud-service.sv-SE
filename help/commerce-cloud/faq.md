---
title: AEM - Commerce Integration med Commerce Integration Framework - frågor och svar
description: AEM - Commerce Integration med Commerce Integration Framework - frågor och svar
translation-type: tm+mt
source-git-commit: ad831b2cc3657666678662eeff0eaf371ce4da49
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# AEM - Commerce Integration med Commerce Integration Framework - frågor och svar


## 1. Används CIF GraphQL endast för handel eller kommer det att vara tillgängligt för frågor som har skapats i AEM JCR?

Adobe har antagit Magento&#39;s GraphQL API:er som dess officiella e-handels-API för alla handelsrelaterade data. Därför använder AEM GraphQL för att utbyta affärsdata med Magento och med valfri e-handelsmotor via I/O Runtime. Detta GraphQL-API är oberoende av AEM GraphQL-API för åtkomst till innehållsfragment.

## 2. Hur spelar Adobe I/O? Pratar AEM med Magento direkt?

AEM kan ansluta direkt till Magento utan ett I/O-körningslager. Om det finns ett behov av att integrera en icke-Magento-e-handelsserver (tredjepartslösning) med AEM kan I/O-körtidsplattformen användas som värd för mappningslagret för att ansluta API:erna för Magento GraphQL till andra tredjepartslösningar-API:er. Mer information finns i [referensimplementeringen](https://github.com/adobe/commerce-cif-graphql-integration-reference). För lösningar som inte är Magento konfigureras AEM att peka mot I/O-körningens slutpunkt.

I/O Runtime-plattformen kan också användas för att utöka eller anpassa e-handelstjänster. För den här typen av användningsfall anropar du I/O Runtime-slutpunkten som sedan är värd för en anpassad implementering av respektive tjänst. Användningsfall för integrering och tillägg kan kombineras.

## 3. Kan produktresurser (bilder) lagras och refereras från AEM via Magento Admin? Hur kan resurser från Dynamic Media förbrukas?

Det finns för närvarande ingen integrering mellan AEM Assets och Magento. Som en tillfällig lösning kan du lagra produktresurser (bilder) i AEM Assets, men du måste lagra resursens URL:er manuellt i Magento. Dynamic Media är nu en del av AEM Assets och kommer att fungera på samma sätt.

## 4. Spelar det någon roll var e-handelslösningen används? (Lokalt eller i molnet)

Det spelar ingen roll var er handelslösning är driftsatt. Integrationen och den nya AEM Venia store fungerar oavsett distributionsmodell. Om den distribueras baserat på den godkända E2E-referensarkitekturen körs E2E-tester mot nyckeltal för prestanda som samlats in och som representerar en företagskunds profil. Detta ger dig ytterligare information som du kan använda som riktmärke.

## 5. Hur skapas katalogsidor eller produktsidor i AEM? Hur kvarstår de i AEM?

Katalogsidor och produktsidor skapas och cachelagras dynamiskt i AEM baserat på generiska katalog- och produktsidmallar. Inga produkt- eller katalogdata importeras och lagras i AEM.

## 6. När ni uppdaterar produktdata i er e-handelslösning, är det en reell satsning på AEM? Eller är det en gruppbearbetning?

Det CIF-tillägg som används med AEM Cloud Service gör att data kan flöda från e-handelslösningen till AEM on-demand. Detta är alltså inte en push- eller batchprocess i realtid när det finns en uppdatering i e-handelslösningen.

## 7. Vilken katalogstorlek AEM med CIF-stöd?

Detta beror på några ytterligare aspekter du måste tänka på. Hur stor är cachekvoten för katalogdata och sidor? Hur många samtidiga förfrågningar förväntar du dig under högtider? Hur skalbar är API:erna för era e-handelslösningar?

## 8. Hur spelar PIM in i detta ramverk?

PIM-data exponeras för AEM och klienter via GraphQL-begäranden. Vi rekommenderar att PIM integreras med e-handelsmotorn (Magento eller andra) så att PIM-data kan hämtas från handelsmotorn.

## 9. Cachelagra även priser och andra data via Dispatcher. Blir det ofta en cachedomål?

Dynamiska data som pris eller lager cachelagras inte i Dispatcher. Dynamiska data hämtas på klientsidan med webbkomponenter direkt via GraphQL API:er. Endast statiska data (som produkt- eller kategoridata) cachelagras i Dispatcher. Om produktdata ändras måste cacheminnet ogiltigförklaras.

## 10. Hur fungerar cacheminnet för AEM Dispatcher med AEM och e-handel?

Vi rekommenderar att du konfigurerar en TTL-baserad cacheogiltigförklaring för sidor som cachelagrats på Dispatcher. För dynamisk information som pris eller aktie rekommenderar vi att du återger datumet på klientsidan. Mer information om TTL-baserad cacheogiltigförklaring finns i [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 11. Finns det någon rekommendation om enhetlig sökning i allt AEM innehåll med Commerce?

En referensimplementering av produktsökningar tillhandahålls, men ingen enhetlig sökning med innehåll. Den här funktionen är vanligtvis mycket kundspecifik och bättre på en projektspecifik nivå.

## 12. Hur fungerar sökningen med AEM och e-handel med CIF?

CIF innehåller komponenterna Sökfält och Sökresultat. Sökfältskomponenten skickar en GraphQL-begäran med söktermen till e-handelslösningen som sedan returnerar en produktlista som innehåller produktnamn, pris, SLUG osv. Sökresultatkomponenten visar sedan sökresultaten i en gallerivy på en sökresultatsida som skapats i AEM. Sökfunktionen stöder grundläggande textsökning. Vi använder SLUG/url-tangenten för att skapa en referens till PDP.

## 13. Hur kan produktdata användas i MSM eller översättningar?

Produktdata är vanligtvis redan översatta i PIM eller Magento. AEM - Magento-integrering stöder anslutningen till flera Magento butiker och butiksvyer. I en MSM-konfiguration är vanligtvis en AEM plats länkad till en Magento store-vy.

## 14. Hur fungerar CIF tillsammans med andra plattformar än Magento?

Integrering med tredjepartslösningar som andra e-handelslösningar (ej Magento) görs via I/O Runtime-plattformen.  Vi har byggt en [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference) för att visa hur detta görs. Detta gör att du kan återanvända [AEM CIF Cloud Connector](https://github.com/adobe/commerce-cif-connector) och [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) genom att visa Magento GraphQL API:t ovanpå en tredjepartsplattform. För att erbjuda maximal flexibilitet och skalbarhet distribueras det här integreringslagret på den serverlösa [Adobe I/O Runtime-plattformen](https://www.adobe.io/apis/experienceplatform/runtime.html).

## 15. Finns det något sätt att förbättra produktdata med kommersiell text? Var gör du det här? I AEM eller i e-handelslösningen?

Vi rekommenderar att ni hanterar marknadsföringsrelaterade data och innehåll i AEM. Dekorera produktdata från er e-handelslösning med ytterligare attribut med hjälp av innehållsfragment eller skapa och länka Experience Fragments för ostrukturerat innehåll till era produkter.

## 16. Kommer integreringen mellan AEM-Magento att förändras när Adobe I/O Runtime-plattformen används?

Kunder som vill utöka e-handelstjänsterna kan använda samma integrerings- och skrivåtgärdssekvenser som finns på I/O Runtime-plattformen för att mata in affärslogik och berika e-handelstjänsterna.

## 17. Lagrar SPA förarbete med AEM SPA?

AEM kan användas som redigeringsverktyg för alla typer av butiker. För närvarande används server- och klientåtergivning (hybrid) i AEM. Vi kommer att släppa PWA stöd för headless och headful content authoring senare under 2021.


## 18. Hur kan vi säkerställa PCI-kompatibilitet när vi använder AEM för hela presentationslagret?

Vi rekommenderar att du använder abstrakta betalningsmetoder. Detta innebär att webbläsarklienten kommunicerar direkt med betalgatewayleverantören så att varken Adobe eller e-handelslösningarna lagrar eller skickar kortinnehavardata. Den här metoden kräver endast en nivå 3 PCI-kompatibilitet. Det finns dock ytterligare saker att tänka på som helt PCI-kompatibla, till exempel hur medarbetarna interagerar med systemet och data. Mer information om Magento PCI-kompatibilitet finns på https://magento.com/pci-compliance

## 19. Om jag använder AEM och Magento molnversioner, är denna gemensamma lösning PCI-kompatibel?

Ja, självutvärderingsformulär D och försäkran om överensstämmelse finns tillgängliga på begäran.


## 20. Hur begär jag en I/O Runtime-testlicens?

Du kan begära en testlicens att använda I/O Runtime [här](https://adobeio.typeform.com/to/obqgRm).
