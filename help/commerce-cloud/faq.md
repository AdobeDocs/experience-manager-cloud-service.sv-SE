---
title: AEM - Commerce Integration med Commerce Integration Framework - frågor och svar
description: AEM - Commerce Integration med Commerce Integration Framework - frågor och svar
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
translation-type: tm+mt
source-git-commit: 36a598961081b7c2229065a031ad163a5336ee43
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# AEM - Commerce Integration med Commerce Integration Framework - frågor och svar

## 1. Används CIF GraphQL endast för handel eller kommer det att vara tillgängligt för frågor som har skapats i AEM JCR?

Adobe har antagit Magento&#39;s GraphQL API:er som dess officiella e-handels-API för alla handelsrelaterade data. Därför använder AEM GraphQL för att utbyta affärsdata med Magento och med valfri e-handelsmotor via I/O Runtime. Detta GraphQL-API är oberoende av AEM GraphQL-API för åtkomst till innehållsfragment.

## 2. Kan produktresurser (bilder) lagras och refereras från AEM via Adobe Commerce (Magento)-administratören? Hur kan resurser från Dynamic Media förbrukas?

Det finns ingen officiell integrering mellan AEM Assets och Magento. Det finns en partnerkoppling tillgänglig på [marknadsplatsen](https://marketplace.magento.com/bounteous-dam.html).

Som en tillfällig lösning kan du lagra produktresurser (bilder) i AEM Assets, men du måste lagra resursens URL:er manuellt i Magento. Dynamic Media är nu en del av AEM Assets och kommer att fungera på samma sätt.

## 3. Spelar det någon roll var e-handelslösningen används? (Lokalt eller i molnet)

Nej, det spelar ingen roll var er handelslösning är installerad. CIF och den AEM butiken fungerar oavsett distributionsmodell. Om lösningen distribueras med den rekommenderade E2E-referensarkitekturen kan E2E-tester köras mot nyckeltal för prestanda som representerar en typisk företagsprofil. Detta kommer att ge ytterligare information som kan användas som riktmärke.

## 4. Hur skapas katalogsidor eller produktsidor i AEM? Hur kvarstår de i AEM?

Katalogsidor och produktsidor skapas och cachelagras dynamiskt i AEM baserat på generiska katalog- och produktsidmallar. Inga produkt- eller katalogdata importeras och lagras i AEM.

## 5. När ni uppdaterar produktdata i er e-handelslösning, är det en reell satsning på AEM? Eller är det en gruppbearbetning?

Det CIF-tillägg som används med AEM Cloud Service gör att data kan flöda från e-handelslösningen till AEM on-demand. Detta är alltså inte en push- eller batchprocess i realtid när det finns en uppdatering i e-handelslösningen.

## 6. Vilken katalogstorlek AEM med CIF-stöd?

Detta beror på några ytterligare aspekter du måste tänka på. Hur stor är cachekvoten för katalogdata och sidor? Hur många samtidiga förfrågningar förväntar du dig under högtider? Hur skalbar är API:erna för era e-handelslösningar?

## 7. Hur spelar PIM in i detta ramverk?

PIM-data exponeras för AEM och klienter via GraphQL-begäranden. Vi rekommenderar att PIM integreras med e-handelsmotorn (Magento eller andra) så att PIM-data kan hämtas från handelsmotorn.

## 8. Cachelagra även priser och andra data via Dispatcher. Blir det ofta en cachedomål?

Dynamiska data som pris eller lager cachelagras inte i Dispatcher. Dynamiska data hämtas på klientsidan med webbkomponenter direkt via GraphQL API:er. Endast statiska data (som produkt- eller kategoridata) cachelagras i Dispatcher. Om produktdata ändras måste cacheminnet ogiltigförklaras.

## 9. Hur fungerar cacheminnet för AEM Dispatcher med AEM och e-handel?

Vi rekommenderar att du konfigurerar en TTL-baserad cacheogiltigförklaring för sidor som cachelagrats på Dispatcher. För dynamisk information som pris eller aktie rekommenderar vi att du återger datumet på klientsidan. Mer information om TTL-baserad cacheogiltigförklaring finns i [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 10. Finns det någon rekommendation om enhetlig sökning i allt AEM innehåll med Commerce?

En referensimplementering av produktsökningar tillhandahålls, men ingen enhetlig sökning med innehåll. Den här funktionen är vanligtvis mycket kundspecifik och bättre på en projektspecifik nivå.

## 11. Hur fungerar sökningen med AEM och e-handel med CIF?

CIF innehåller komponenterna Sökfält och Sökresultat. Sökfältskomponenten skickar en GraphQL-begäran med söktermen till e-handelslösningen som sedan returnerar en produktlista som innehåller produktnamn, pris, SLUG osv. Sökresultatkomponenten visar sedan sökresultaten i en gallerivy på en sökresultatsida som skapats i AEM. Sökfunktionen stöder grundläggande textsökning. Vi använder SLUG/url-tangenten för att skapa en referens till PDP.

## 12. Hur kan produktdata användas i MSM eller översättningar?

Produktdata är vanligtvis redan översatta i PIM eller Magento. AEM - Magento-integrering stöder anslutningen till flera Magento butiker och butiksvyer. I en MSM-konfiguration är vanligtvis en AEM plats länkad till en Magento store-vy.

## 13. Finns det något sätt att förbättra produktdata med kommersiell text? Var gör du det här? I AEM eller i e-handelslösningen?

Vi rekommenderar att ni hanterar marknadsföringsrelaterade data och innehåll i AEM. Dekorera produktdata från er e-handelslösning med ytterligare attribut med hjälp av innehållsfragment eller skapa och länka Experience Fragments för ostrukturerat innehåll till era produkter.

## 14. Hur kan vi säkerställa PCI-kompatibilitet när vi använder AEM för hela presentationslagret?

Vi rekommenderar att du använder abstrakta betalningsmetoder. Detta innebär att webbläsarklienten kommunicerar direkt med betalgatewayleverantören så att varken Adobe eller e-handelslösningarna lagrar eller skickar kortinnehavardata. Den här metoden kräver endast en nivå 3 PCI-kompatibilitet. Det finns dock ytterligare saker att tänka på som helt PCI-kompatibla, till exempel hur medarbetarna interagerar med systemet och data. Mer information om Magento PCI-kompatibilitet finns i <https://magento.com/pci-compliance>

## 15. Om jag använder AEM och Magento molnversioner, är denna gemensamma lösning PCI-kompatibel?

Ja, självutvärderingsformulär D och försäkran om överensstämmelse finns tillgängliga på begäran.

## 16. Hur begär jag en I/O Runtime-testlicens?

Du kan begära en testlicens att använda I/O Runtime [här](https://adobeio.typeform.com/to/obqgRm).
