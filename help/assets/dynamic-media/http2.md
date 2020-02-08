---
title: HTTP2-leverans av innehåll
description: HTTP/2 förbättrar kommunikationen mellan webbläsare och servrar, vilket ger snabbare överföring av information samtidigt som man minskar behovet av processorkraft.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# HTTP2-leverans av innehåll {#http-delivery-of-content}

Adobe är mycket glada över att kunna meddela att det finns HTTP/2-leverans av innehåll, vilket ger bättre prestanda.

## Vad är HTTP/2? {#what-is-http}

HTTP/2 förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger snabbare överföring av information samtidigt som man minskar behovet av processorkraft.

På följande webbplats beskrivs HTTP/2 och dess fördelar på ett kort och enkelt sätt:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Vilka är de viktigaste fördelarna med att gå över till HTTP/2 för innehållsleverans? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Prestandaförbättringarna varierar mycket beroende på faktorer som webbplatsens kod, hur du använder Dynamic Media, konsumentens enhet, skärm och plats och så vidare.

Adobes egna tester gav följande resultat:

* För bilder har svarstiden förbättrats med 7 %-28 % beroende på enhet och webbläsare. De mest betydande prestandavinster gjordes på iOS-enheter.
* För tittarna har lästiden förbättrats med 15 %.

I följande exempel visas skillnaden mellan HTTP/1 och HTTP/2-inläsning:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Är jag berättigad att växla över till HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Om du vill använda HTTP/2 måste du uppfylla följande krav:

* Använd säker HTTPS för multimedieförfrågningar.
* Använd det Adobe-paketerade CDN (content delivery network) som en del av din Dynamic Media-licens.
* Använd en dedikerad domän (non-company-h.assetsadobe#.com).

   Om du redan har en dedikerad domän kan du anmäla dig via teknisk support.

   Om du inte har någon dedikerad domän schemalägger Adobe din övergång till HTTP/2 under 2018.

## Hur aktiverar jag HTTP/2 för mitt Dynamic Media-konto? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Du måste initiera begäran om att växla över till HTTP/2; det görs inte automatiskt åt dig.

1. Initiera en begäran om teknisk support för att växla till HTTP2. Se [Åtkomst till AEM Support Portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Ange följande information i din supportförfrågan:

      1. Primärt kontaktnamn, e-postadress, telefon.
      1. Alla domäner som ska överföras till HTTP2.
      1. Kontrollera att du använder säkra HTTPS för multimedieförfrågningar.
      1. Kontrollera att du använder CDN via Adobe och inte hanteras med en direkt relation.
      1. Kontrollera att du använder en dedikerad domän. Om du använder Dynamic Media använder du redan en dedikerad domän.
   1. Teknisk support lägger till dig i HTTP/2-väntelistan baserat på i vilken ordning förfrågningar skickades.
   1. När Adobe är redo att hantera din förfrågan kontaktar supporten dig för att koordinera övergången och ange ett måldatum.
   1. Du får ett meddelande när du är klar och du kan verifiera att övergången har slutförts till HTTP2.

      Eftersom webbläsaren inte anger detta måste du hämta ett tillägg.

      För Firefox och Chrome finns ett tillägg som heter HTTP/2 och SPDY Indicator. Webbläsarna stöder bara http/2 säkert, så det är nödvändigt att anropa en URL med https för att verifiera. Om det finns stöd för http/2 indikeras detta av tillägget i form av en blå Flash-symbol och rubriken&quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.


## När kan jag förvänta mig att gå över till HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Förfrågningar kommer att behandlas i den ordning som de tas emot av teknisk support.

>[!NOTE]
>
>Det kan finnas lång ledtid eftersom övergången till HTTP/2 innebär att cachen rensas. Därför kan bara ett fåtal kundövergångar hanteras åt gången.

## Vilka är riskerna med att gå över till HTTP/2? {#what-are-the-risks-with-moving-to-http}

Övergången till HTTP/2 tar bort ditt cacheminne vid CDN eftersom det handlar om att gå över till en ny CDN-konfiguration.

Det icke-cachelagrade innehållet träffar direkt på Adobes originalservrar tills cachen återskapas. På grund av detta planerar Adobe att hantera ett fåtal kundövergångar i taget så att godtagbara prestanda upprätthålls när vi drar in förfrågningar från vårt ursprung.

## Hur kan du verifiera om en URL eller webbplats är aktiverad med HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Eftersom webbläsaren inte anger detta måste du hämta ett tillägg.

För Firefox och Chrome finns ett tillägg som heter HTTP/2 och SPDY Indicator. Webbläsarna stöder bara http/2 säkert, så det är nödvändigt att anropa en URL med https för att verifiera. Om det finns stöd för http/2 indikeras detta av tillägget i form av en blå Flash-symbol och rubriken&quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
