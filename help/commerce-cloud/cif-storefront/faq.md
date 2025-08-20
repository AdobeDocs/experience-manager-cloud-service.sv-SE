---
title: AEM - Commerce Integration med Commerce integration framework - frågor och svar
description: AEM - Commerce Integration med Commerce integration framework - frågor och svar
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
feature: Commerce Integration Framework
role: Admin, Architect, User
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# AEM - Commerce Integration med Commerce integration framework - frågor och svar

## &#x200B;1. Används CIF GraphQL endast för e-handel eller kommer detta att vara tillgängligt för frågor som skapats i AEMs JCR? {#faq-1}

Adobe har antagit Adobe Commerce GraphQL API:er som sitt officiella e-handels-API för alla e-handelsrelaterade data. Därför använder AEM GraphQL för att utbyta affärsdata med Adobe Commerce och med alla e-handelsmotorer via I/O Runtime. Det här GraphQL-API:t är oberoende av AEM GraphQL-API för att få åtkomst till innehållsfragment.

## &#x200B;2. Kan produktresurser (bilder) lagras och refereras från AEM via Adobe Commerce Admin? Hur kan resurser från Dynamic Media förbrukas? {#faq-2}

Det finns ingen officiell integrering med AEM Assets - Adobe Commerce. Det finns en partnerkoppling tillgänglig på [Marketplace.](https://commercemarketplace.adobe.com)

Som en tillfällig lösning kan du lagra produktresurser (bilder) i AEM Assets, men du måste lagra resursens URL-adresser manuellt i Adobe Commerce. Dynamic Media är nu en del av AEM Assets och fungerar på samma sätt.

## &#x200B;3. Spelar det någon roll var e-handelslösningen används? (Lokalt eller i molnet) {#faq-3}

Nej, det spelar ingen roll var er handelslösning är installerad. CIF och AEM Store fungerar oavsett distributionsmodell. Om lösningen distribueras med den rekommenderade E2E-referensarkitekturen kan E2E-tester köras mot nyckeltal för prestanda som representerar en typisk företagsprofil. Denna metod ger ytterligare information som kan användas som riktmärke.

## &#x200B;4. Hur skapas katalogsidor eller produktsidor i AEM? Hur kvarstår de i AEM? {#faq-4}

Katalogsidor och produktsidor skapas och cachelagras dynamiskt i AEM baserat på generiska katalog- och produktsidmallar. Inga produkt- eller katalogdata importeras och lagras i AEM.

## &#x200B;5. När ni uppdaterar produktdata i er e-handelslösning, är det en realtidspress till AEM? Eller är det en gruppbearbetning? {#faq-5}

CIF-tillägget som används med AEM Cloud-tjänsten gör att data kan flöda från e-handelslösningen till AEM on-demand. Detta är alltså inte en push- eller batchprocess i realtid när det finns en uppdatering i e-handelslösningen.

## &#x200B;6. Vilken katalogstorlek stöder AEM med CIF? {#faq-6}

Detta beror på några andra aspekter som du måste tänka på. Hur stor är cachekvoten för katalogdata och sidor? Hur många samtidiga förfrågningar förväntar du dig under högtider? Hur skalbar är API:erna för era e-handelslösningar?

## &#x200B;7. Hur fungerar PIM i detta ramverk? {#faq-7}

PIM-data exponeras för AEM och kunder via GraphQL-förfrågningar. Vi rekommenderar att PIM integreras med e-handelsmotorn (Adobe Commerce eller andra) så att PIM-data kan hämtas från e-handelsmotorn.

## &#x200B;8. Cachelagra även priser och andra data via Dispatcher. Blir det ofta en cachedomål? {#faq-8}

Dynamiska data som pris eller lager cachelagras inte på Dispatcher. Dynamiska data hämtas på klientsidan med webbkomponenter direkt via GraphQL API:er. Endast statiska data (som produkt- eller kategoridata) cachelagras på Dispatcher. Om produktdata ändras måste cacheminnet ogiltigförklaras.

## &#x200B;9. Hur fungerar cacheminnet för AEM Dispatcher tillsammans med AEM och e-handel? {#faq-9}

Adobe rekommenderar att du ställer in TTL-baserad cacheogiltigförklaring för sidor som cachelagrats på Dispatcher. För dynamisk information som pris eller aktie rekommenderar Adobe att du återger data på klientsidan. Mer information om ogiltigförklaring av TTL-baserad cache finns i [Optimera Dispatcher-cachen.](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=sv-SE)

## &#x200B;10. Finns det någon rekommendation om enhetlig sökning i AEM-innehåll med Commerce? {#faq-10}

En referensimplementering av produktsökningar tillhandahålls, men ingen enhetlig sökning med innehåll. Den här funktionen är kundspecifik och bättre på projektspecifik nivå.

## &#x200B;11. Hur fungerar Search med AEM och e-handel med CIF? {#faq-11}

CIF innehåller komponenterna Sökfält och Sökresultat. Sökfältskomponenten skickar en GraphQL-begäran med söktermen till e-handelslösningen som sedan returnerar en produktlista som innehåller produktnamn, pris, SLUG och så vidare. Sökresultatkomponenten visar sedan sökresultaten i en gallerivy på en sökresultatsida som skapats i AEM. Sökfunktionen har stöd för grundläggande textsökning. Vi använder SLUG/url-tangenten för att skapa en referens till PDP.

## &#x200B;12. Hur kan produktdata användas i MSM eller översättningar? {#faq-12}

Produktdata är redan översatta i PIM eller Adobe Commerce. AEM - Adobe Commerce Integration har stöd för anslutning till flera Adobe Commerce butiker och butiksvyer. I en MSM-konfiguration är vanligtvis en AEM-webbplats länkad till en Adobe Commerce Store-vy.

## &#x200B;13. Finns det något sätt att förbättra produktinformationen med kommersiell text? Var gör du det här? I AEM eller i e-handelslösningen? {#faq-13}

Adobe rekommenderar att man hanterar marknadsföringsrelaterade data och marknadsföringsrelaterat innehåll i AEM. Dekorera produktdata från er e-handelslösning med ytterligare attribut med hjälp av innehållsfragment eller skapa och länka Experience Fragments för ostrukturerat innehåll till era produkter.

## &#x200B;14. Hur kan PCI-kompatibilitet säkerställas när AEM används för hela presentationslagret? {#faq-14}

Adobe rekommenderar att du använder abstrakta betalningsmetoder. Detta innebär att webbläsarklienten kommunicerar direkt med betalgatewayleverantören så att varken Adobe eller e-handelslösningarna lagrar eller skickar kortinnehavardata. Den här metoden kräver endast en nivå 3 PCI-kompatibilitet. Det finns dock ytterligare saker att tänka på som helt PCI-kompatibla, till exempel hur medarbetarna interagerar med systemet och data. Mer information om Adobe Commerce PCI-kompatibilitet finns i [Krav för PCI-kompatibilitet.](https://business.adobe.com/products/magento/pci-compliance.html)

## &#x200B;15. Om jag använder molnversionerna av AEM och Adobe Commerce, är denna gemensamma lösning PCI-kompatibel? {#faq-15}

Ja, självutvärderingsformulär D och försäkran om överensstämmelse finns tillgängliga på begäran.

## &#x200B;16. Hur begär jag en I/O Runtime-licens? {#faq-16}

Mer information om hur du begär en utvärderingslicens för att använda I/O-miljön finns i [Få åtkomst](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/).
