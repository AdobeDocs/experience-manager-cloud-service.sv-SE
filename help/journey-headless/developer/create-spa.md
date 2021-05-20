---
title: Valfritt - Så här skapar du enkelsidiga program (SPA) med AEM
description: I den här valfria fortsättningen av den AEM Headless Developer Journey får du lära dig hur AEM kan kombinera headless-leverans med traditionella CMS-funktioner i full hög och hur du kan skapa redigerbara SPA med hjälp av AEM ramverk för SPA.
source-git-commit: ddd320ae703225584d4a2055d0f882d238d60987
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---


# Skapa enkelsidiga program (SPA) med AEM {#create-spa}

I den här valfria fortsättningen av [AEM Headless Developer Journey,](overview.md), får du lära dig hur AEM kan kombinera headless-leverans med traditionella CMS-funktioner i full-stack och hur du kan skapa redigerbara SPA med hjälp av AEM ramverk för SPA Editor, samt integrera externa SPA, vilket möjliggör redigeringsfunktioner efter behov.

## Berättelsen hittills {#story-so-far}

Nu ska du ha slutfört hela [AEM Headless Developer Journey](overview.md) och förstå grunderna för headless delivery i AEM inklusive en förståelse av:

* Skillnaden mellan headless och headful content delivery.
* AEM headless-funktioner.
* Organisera och AEM Headless-projekt.
* Skapa innehåll utan rubriker i AEM.
* Så här hämtar och uppdaterar du headless-innehåll i AEM.
* Så här lever du med ett AEM Headless-projekt.

Så du har nu antingen gått live med ditt första AEM Headless-projekt eller har all den kunskap som behövs för att göra det. Grattis!

Varför läser du den här extra, valfria fortsatta resan? I [Getting Started](getting-started.md#integration-levels) diskuterade vi troligen kortfattat hur AEM inte bara stöder headless-leverans och traditionella fullstacksmodeller, utan också stöder hybridmodeller som kombinerar fördelarna med båda. Även om det inte är den traditionella headless-modellen kan sådana hybridmodeller ge oöverträffad flexibilitet till vissa projekt.

Den här artikeln bygger på dina kunskaper om AEM Headless genom att ingående utforska hur du kan skapa egna ensidiga program (SPA) som faktiskt kan redigeras i AEM. På så sätt kan du skapa innehåll och skicka det direkt till en SPA, men det SPA fortfarande redigerbart i AEM.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur Single Page-program utvecklas med AEM ramverk för SPA. När du har läst det här dokumentet bör du:

* Förstå den grundläggande funktionen i SPA Editor.
* Lär dig grunderna för att skapa en fullt redigerbar SPA för AEM.
* Förstå hur externa SPA kan integreras i AEM.
* Förstå hur återgivning på serversidan ska implementeras eller inte.

## Krav och krav {#requirements-prerequisites}

Det finns ett antal krav innan du börjar arbeta med SPA i AEM.

### Kunskap {#knowledge}

* Utvecklingserfarenhet som skapar SPA med React- eller Angular-ramverk
* Grundläggande AEM att skapa innehållsfragment och använda redigeraren
* Läs dokumentet [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) för att förstå de olika nivåerna av SPA.

### Verktyg {#tools}

* Sandlådeåtkomst för testning av driftsättning av ditt projekt
* Lokal utvecklingsinstans för datamodellering och -testning
* Befintliga externa SPA (valfritt, beroende på vilken integrationsmodell som väljs)
* AEM Project Archetype

## Vad är en SPA? {#what-is-a-spa}

Ett enkelsidigt program (SPA) skiljer sig från en konventionell sida på så sätt att det återges på klientsidan och i huvudsak är Javascript-drivet, beroende på Ajax-anrop för att läsa in data och dynamiskt uppdatera sidan. Det mesta eller allt innehåll hämtas en gång på en sida, och ytterligare resurser läses in asynkront efter behov baserat på användarinteraktionen med sidan.

Detta minskar behovet av siduppdatering och ger användaren en upplevelse som är smidig, snabb och som känns mer som en appupplevelse.

Med AEM SPA Editor kan gränssnittsutvecklare skapa SPA som kan integreras i en AEM webbplats, vilket gör att innehållsförfattarna kan redigera SPA innehåll lika enkelt som annat AEM.

## Varför en SPA? {#why-spa}

Genom att vara snabbare, smidigare och mer som ett systemspecifikt program blir en SPA en mycket attraktiv upplevelse inte bara för besökaren på webbsidan, utan även för marknadsförare och utvecklare på grund av hur SPA fungerar.

En fullständig beskrivning av SPA och varför du skulle använda dem finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## Hur AEM hanterar SPA

Utveckla single page-applikationer AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om du som frontendutvecklare följer dessa allmänna bästa metoder samt några AEM-specifika principer, kommer din SPA att fungera med AEM och dess innehållsredigeringsfunktioner.

* **Portabilitet**  - Precis som med andra komponenter bör de SPA komponenterna vara så portabla som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **AEM Drives Site Structure**  (Webbplatsstruktur) - Utvecklaren på fronten skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **Dynamisk återgivning**  - All återgivning ska vara dynamisk.
* **Dynamisk routning**  - SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

En fullständig beskrivning av hur AEM hanterar SPA finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## AEM SPA Editor {#aem-spa-editor}

Webbplatser som byggts med vanliga SPA ramverk som React och Angular läser in sitt innehåll via dynamisk JSON och tillhandahåller inte den HTML-struktur som krävs för att den AEM sidredigeraren ska kunna placera redigeringskontroller.

Om du vill kunna redigera SPA i AEM måste du mappa mellan JSON-utdata för SPA och innehållsmodellen i den AEM databasen för att kunna spara ändringar i innehållet.

SPA i AEM innehåller ett tunt JS-lager som interagerar med den SPA JS-koden när den läses in i sidredigeraren. Händelser kan skickas med och platsen för redigeringskontrollerna kan aktiveras för redigering i sitt sammanhang. Den här funktionen bygger på API-slutpunktskonceptet för innehållstjänster eftersom innehållet från SPA måste läsas in via innehållstjänster.

En fullständig beskrivning av AEM SPA Editor finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## Hämtar befintlig SPA {#existing-spas}

Om du har en befintlig SPA har AEM stöd för att bädda in den i AEM så att den är synlig för innehållsförfattarna i AEM redigerare. Det här kan vara användbart om du vill visa innehållet som de skapar via innehållsfragment i slutprogrammet där det kommer att användas.

Dessutom kan du, med endast små ändringar, aktivera vissa redigeringsmöjligheter för de externa SPA i AEM redigerare.

RemotePage-komponenten tillåter återgivning av en extern SPA i AEM.

En fullständig beskrivning av hur du gör en extern SPA ändringsbar i AEM finns i [avsnittet ](#additional-resources) ytterligare resurser för länkar till mer utförlig dokumentation.

## What&#39;s Next {#what-is-next}

Kom igång med att utveckla en egen SPA för AEM genom att läsa följande dokument:

* [SPA WKND - självstudiekurs](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Komma igång med React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Komma igång med Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Om du behöver anpassa en befintlig SPA för att använda den i AEM, ska du läsa följande dokument:

* [RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)
* [Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Nedan finns [ytterligare resurser](#additional-resources) som kan fördjupa dig SPA ämnen i AEM.

## Ytterligare resurser {#additional-resources}

Nedan följer ytterligare resurser som ger en djupdykning i några koncept som nämns i det här dokumentet.

* [Headless and Headless in AEM](/help/implementing/developing/headful-headless.md) - A description of the different delivery models available in AEM
* [SPA introduktion och genomgång.](/help/implementing/developing/hybrid/introduction.md) - En bra introduktion till SPA i AEM
* [Utveckla SPA för AEM](/help/implementing/developing/hybrid/developing.md)  - Riktlinjer för hur du utvecklar SPA för AEM
* [Översikt över](/help/implementing/developing/hybrid/editor-overview.md)  SPA - Information om hur SPA redigeraren fungerar
* [Återgivning](/help/implementing/developing/hybrid/ssr.md)  på serversidan - Så här konfigurerar du SSR för AEM SPA
* [SPA referensdokument](/help/implementing/developing/hybrid/reference-materials.md)  - JavaScript API-referenser och länkar till AEM öppen källkod SPA GitHub-projekt
* [Content Fragments](/help/assets/content-fragments/content-fragments.md)  - How to create Content Fragments
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - Maven template that create a minimum, best-practices based Adobe Experience Manager (AEM) project as a starting point for your website
