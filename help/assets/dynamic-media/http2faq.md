---
title: Vanliga frågor om leverans av innehåll med HTTP2
description: Läs mer om HTTP2-innehållsleverans.
role: Administrator,Business Practitioner
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
translation-type: tm+mt
source-git-commit: 1ad89be4ebddec0705c6f557fed3d697b9f1f3a7
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Vanliga frågor om leverans av innehåll med HTTP2{#http-delivery-of-content-faq}

Adobe är glada över att kunna meddela att HTTP/2-leverans av innehåll är tillgänglig. När du använder HTTP/2 ökar prestanda totalt.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga Content Delivery Network som medföljer Adobe Experience Manager - Dynamic Media. Andra anpassade leveransnätverk stöds inte med den här funktionen.

## Vad är HTTP/2? {#what-is-http}

HTTP/2 förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger snabbare överföring av information samtidigt som man minskar behovet av processorkraft.

Webbplatsartikeln [Det du måste känna till om HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html) beskriver HTTP/2 och dess fördelar på ett kort och enkelt sätt.

## Vilka är de viktigaste fördelarna med att gå över till HTTP/2 för innehållsleverans? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Prestandaförbättringen varierar mycket eftersom den baseras på olika faktorer. Till exempel webbplatsens kod, hur du använder Dynamic Media, konsumentens enhet, skärm och plats.

Adobe testning gav följande resultat:

* För bilder har svarstiden förbättrats med 7 %-28 % beroende på enhet och webbläsare. De mest betydande prestandavinster gjordes på iOS-enheter.
* För tittarna har lästiden förbättrats med 15 %.

I följande exempel visas skillnaden mellan HTTP/1 och HTTP/2-inläsning:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Är jag berättigad att växla över till HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Om du vill använda HTTP/2 måste du uppfylla följande krav:

* Använd säker HTTPS för multimedieförfrågningar.
* Använd det Adobe-paketerade CDN (Content Delivery Network) som en del av din Dynamic Media Classic-licens.
* Använd en dedikerad domän (d.v.s. `images.company.com` eller `mycompany.scene7.com`), inte en generisk Dynamic Media-domän (d.v.s. `s7d1.scene7.com`, `s7d2.scene7.com` eller `s7d13.scene7.com`).

   Om du vill hitta dina domäner öppnar du [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och loggar sedan in på ditt konto.

   Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet **Publicerat servernamn**. Om du för närvarande använder en allmän Dynamic Media-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.

## Hur aktiverar jag HTTP/2 för mitt Dynamic Media-konto? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Använd Admin Console för att skapa ett supportärende ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) och begära att gå över till HTTP/2. det görs inte automatiskt åt dig.

1. Ange följande information i ditt supportärende:

   * Primärt kontaktnamn, e-postadress och telefonnummer.
   * Alla domäner som ska överföras till HTTP2. Det vill säga `images.company.com` eller `mycompany.scene7.com`.

   Om du vill hitta dina domäner öppnar du [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och loggar sedan in på ditt konto.

   Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet **[!UICONTROL Published Server Name]**.

   * Verifiera att du använder säkra HTTPS för multimedieförfrågningar.
   * Kontrollera att du använder CDN via Adobe och inte hanteras med en direkt relation.
   * Kontrollera att du använder en dedikerad domän. Det vill säga `images.company.com` eller `mycompany.scene7.com` är inte en allmän Dynamic Media-domän som `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Om du vill hitta dina domäner öppnar du [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och loggar sedan in på ditt konto.

   Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet **[!UICONTROL Published Server Name]**. Om du för närvarande använder en allmän Dynamic Media-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.

   1. Teknisk support lägger till dig i HTTP/2-väntelistan baserat på i vilken ordning förfrågningarna skickades.
   1. När Adobe är redo att hantera din begäran kontaktar kundtjänst dig för att koordinera övergången och ange ett måldatum.
   1. Du får ett meddelande när du är klar och du kan verifiera en lyckad övergång till HTTP2.



## När kan jag förvänta mig att gå över till HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Förfrågningar behandlas i den ordning som de tas emot av teknisk support.

>[!NOTE]
>
>Det finns en lång ledtid eftersom övergången till HTTP/2 innebär att cacheminnet rensas. Därför kan bara ett fåtal kundövergångar hanteras åt gången.

## Vilka är riskerna med att gå över till HTTP/2? {#what-are-the-risks-with-moving-to-http}

Övergången till HTTP/2 tar bort ditt cacheminne vid CDN eftersom det handlar om att gå över till en ny CDN-konfiguration.

Det icke-cachelagrade innehållet träffar direkt på Adobe-servrar tills cachen återskapas. På grund av detta planerar Adobe att hantera några kundövergångar i taget. Med den här metoden säkerställs att godtagbara prestanda upprätthålls när begäranden dras från ursprungsläget.

## Hur kan du verifiera om en URL eller webbplats är aktiverad med HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Ladda ned ett tillägg som du kan använda med webbläsaren. För Firefox och Chrome finns det ett tillägg som heter **[!UICONTROL HTTP/2 and SPDY Indicator]**. Webbläsare stöder bara säkert HTTP/2, så det är nödvändigt att anropa en URL med HTTPS för att verifiera. Om HTTP/2 stöds anges det av tillägget i form av en blå Flash-symbol och rubriken&quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
