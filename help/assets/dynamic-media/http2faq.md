---
title: Vanliga frågor om leverans av innehåll med HTTP2
description: Läs mer om HTTP2-innehållsleverans.
translation-type: tm+mt
source-git-commit: 24d929702fd9eb31b95fdd6d97c7b9978d919804
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---


# Vanliga frågor om leverans av innehåll med HTTP2{#http-delivery-of-content-faq}

Adobe är glada över att kunna meddela att HTTP/2-leverans av innehåll är tillgänglig. När du använder HTTP/2 kommer du att märka en generell prestandaökning.

## Vad är HTTP/2? {#what-is-http}

HTTP/2 förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger snabbare överföring av information samtidigt som man minskar behovet av processorkraft.

På följande webbplats beskrivs HTTP/2 och dess fördelar på ett kort och enkelt sätt:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Vilka är de viktigaste fördelarna med att gå över till HTTP/2 för innehållsleverans? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Prestandaförbättringarna varierar mycket beroende på faktorer som webbplatsens kod, hur du använder Scene7, konsumentens enhet, skärm och plats och så vidare.

Adobe testning gav följande resultat:

* För bilder har svarstiden förbättrats med 7 %-28 % beroende på enhet och webbläsare. De mest betydande prestandavinster gjordes på iOS-enheter.
* För tittarna har lästiden förbättrats med 15 %.

I följande exempel visas skillnaden mellan HTTP/1 och HTTP/2-inläsning:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Är jag berättigad att växla över till HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Om du vill använda HTTP/2 måste du uppfylla följande krav:

* Använd säker HTTPS för multimedieförfrågningar.
* Använd det Adobe-paketerade CDN (content delivery network) som en del av din Dynamic Media Classic-licens.
* Använd en dedikerad domän (d.v.s. `images.company.com` eller `mycompany.scene7.com`), som inte är en allmän Dynamic Media Classic-domän (d.v.s. `s7d1.scene7.com`, `s7d2.scene7.com`eller `s7d13.scene7.com`).

   Om du vill hitta dina domäner [loggar du in på din instans av Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) för varje företagskonto.

   Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet **Publicerat servernamn**. Om du för närvarande använder en allmän Scene7-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.

## Hur aktiverar jag HTTP/2 för mitt Dynamic Media Classic-konto? {#what-is-the-process-for-enabling-http-for-my-scene-account}

Du måste [använda Admin Console för att skapa ett supportärende](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) och begära att gå över till HTTP/2; det görs inte automatiskt åt dig.

1. Ange följande information i ditt supportärende:

   * Primärt kontaktnamn, e-postadress och telefonnummer.
   * Alla domäner som ska överföras till HTTP2. Det vill säga, `images.company.com` eller `mycompany.scene7.com`.

   Om du vill hitta dina domäner [loggar du in på din instans av Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) för varje företagskonto.

   Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet som är märkt **[!UICONTROL Published Server Name]**.

   * Verifiera att du använder säkra HTTPS för multimedieförfrågningar.
   * Kontrollera att du använder CDN via Adobe och inte hanteras med en direkt relation.
   * Kontrollera att du använder en dedikerad domän. Det vill säga `images.company.com` eller `mycompany.scene7.com`inte en allmän Scene7-domän som `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Om du vill hitta dina domäner [loggar du in på din instans av Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) för varje företagskonto.

   Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet som är märkt **[!UICONTROL Published Server Name]**. Om du för närvarande använder en allmän Scene7-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.

   1. Teknisk support lägger till dig i HTTP/2-väntelistan baserat på i vilken ordning förfrågningarna skickades.
   1. När Adobe är redo att hantera din begäran kontaktar supporten dig för att koordinera övergången och ange ett måldatum.
   1. Du får ett meddelande när du är klar och du kan verifiera en lyckad övergång till HTTP2.



## När kan jag förvänta mig att gå över till HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Förfrågningar behandlas i den ordning som de tas emot av teknisk support.

>[!NOTE]
>
>Det kan finnas lång ledtid eftersom övergången till HTTP/2 innebär att cachen rensas. Därför kan bara ett fåtal kundövergångar hanteras åt gången.

## Vilka är riskerna med att gå över till HTTP/2? {#what-are-the-risks-with-moving-to-http}

Övergången till HTTP/2 tar bort ditt cacheminne vid CDN eftersom det handlar om att gå över till en ny CDN-konfiguration.

Det icke-cachelagrade innehållet träffar direkt på Adobe-servrar tills cachen återskapas. På grund av detta planerar Adobe att hantera ett fåtal kundövergångar i taget så att godtagbara prestanda upprätthålls när vi drar in förfrågningar från vårt ursprung.

## Hur kan du verifiera om en URL eller webbplats är aktiverad med HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Du måste ladda ned en extern version för att kunna använda den i webbläsaren. För Firefox och Chrome finns ett tillägg som kallas **[!UICONTROL HTTP/2 and SPDY Indicator]**. Webbläsare stöder bara säkert HTTP/2, så det är nödvändigt att anropa en URL med HTTPS för att verifiera. Om HTTP/2 stöds anges detta av tillägget i form av en blå Flash-symbol och rubriken&quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
