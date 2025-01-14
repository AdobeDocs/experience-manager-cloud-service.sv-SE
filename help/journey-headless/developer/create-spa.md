---
title: Valfritt - Så här skapar du enkelsidiga program (SPA) med Adobe Experience Manager (AEM)
description: I den här valfria förlängningen av AEM Headless Developer Journey får du lära dig hur AEM kan kombinera headless-leverans med traditionella CMS-funktioner i full hög och hur du kan skapa redigerbara SPA med hjälp av AEM SPA Editor-ramverk.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: a69658d5657f4e1a4feed20cf7eda5e9899aaa3d
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# Skapa enkelsidiga program (SPA) med AEM {#create-spa}

I den här valfria förlängningen av [AEM Headless Developer Journey](overview.md) får du lära dig hur AEM kan kombinera headless-leverans med traditionella CMS-funktioner i full hög. Du får också lära dig hur du kan skapa redigerbara SPA med AEM SPA Editor-ramverket och integrera externa SPA, vilket möjliggör redigeringsfunktioner efter behov.

## Story hittills {#story-so-far}

Nu ska du ha slutfört hela [AEM Headless Developer Journey](overview.md) och förstå grunderna för headless delivery i AEM, inklusive en förståelse för:

* Skillnaden mellan headless och headful content delivery.
* AEM headless-funktioner.
* Organisera och AEM Headless-projekt.
* Skapa innehåll utan rubriker i AEM.
* Så här hämtar och uppdaterar du headless-innehåll i AEM.
* Så här lever du med ett AEM Headless-projekt.

Fram tills nu har du antingen gått live med ditt första AEM Headless-projekt eller så har du kunskapen om att göra det. Grattis!

Varför läser du den här extra, valfria fortsatta resan? I [Getting Started](getting-started.md#integration-levels) diskuterades hur AEM inte bara stöder headless-leverans och traditionella helstacksmodeller, utan även hybridmodeller som kombinerar fördelarna med båda. Även om det inte är den traditionella headless-modellen kan sådana hybridmodeller ge oöverträffad flexibilitet till vissa projekt.

Den här artikeln bygger på dina kunskaper om AEM Headless genom att ingående utforska hur du kan skapa egna single-page-program (SPA) som kan redigeras i AEM. På så sätt kan du skapa innehåll och leverera det direkt till en SPA, men det SPA fortfarande redigerbart i AEM.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur Single Page-program utvecklas med AEM ramverk för SPA. När du har läst det här dokumentet bör du:

* Förstå den grundläggande funktionen i SPA.
* Lär dig grunderna för att skapa en fullt redigerbar SPA för AEM.
* Förstå hur externa SPA kan integreras i AEM.
* Förstå hur rendering på serversidan kan eller inte kan implementeras.

## Krav och krav {#requirements-prerequisites}

Det finns flera krav innan du börjar arbeta med SPA i AEM.

### Kunskap {#knowledge}

* Utvecklingserfarenhet som skapar SPA med React- eller Angular-ramverk
* Grundläggande AEM att skapa innehållsfragment och använda redigeraren
* Granska dokumentet [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) så att du kan förstå de olika nivåerna av SPA.

### verktyg {#tools}

* Sandlådeåtkomst för testning av driftsättning av ditt projekt
* Lokal utvecklingsinstans för datamodellering och -testning
* Befintliga externa SPA (valfritt, beroende på vilken integrationsmodell som väljs)
* AEM Project Archettype

## Vad är en SPA? {#what-is-a-spa}

Ett enkelsidigt program (SPA) skiljer sig från en konventionell sida på så sätt att det återges på klientsidan och i första hand är JavaScript-drivet, beroende på Ajax-anrop för att läsa in data och dynamiskt uppdatera sidan. Det mesta, eller allt, innehållet hämtas en gång på en sida och ytterligare resurser läses in asynkront efter behov, baserat på användarinteraktionen med sidan.

Den här funktionen minskar behovet av uppdatering av sidor och ger användaren en upplevelse som är smidig, snabb och som känns mer som en appupplevelse.

Med AEM SPA Editor kan gränssnittsutvecklare skapa SPA som kan integreras i en AEM webbplats, vilket gör att innehållsförfattarna kan redigera SPA innehåll lika enkelt som annat AEM.

## Varför en SPA? {#why-spa}

Genom att vara snabbare, smidigare och mer som ett systemspecifikt program blir en SPA en attraktiv upplevelse. Det passar inte bara besökaren på webbsidan, utan även marknadsförare och utvecklare på grund av hur SPA fungerar.

En fullständig beskrivning av SPA och varför du skulle använda dem finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## Hur AEM hanterar SPA

Utveckla single page-applikationer AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om du som frontendutvecklare följer dessa allmänna bästa metoder och några AEM-specifika principer fungerar dina SPA med AEM och dess innehållsredigeringsfunktioner.

* **Portabilitet** - Precis som med andra komponenter ska SPA byggas så att de blir så portabla som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **AEM Drives Site Structure** - Front-end-utvecklaren skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **Dynamisk återgivning** - All återgivning ska vara dynamisk.
* **Dynamisk routning** - SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

En fullständig beskrivning av hur AEM hanterar SPA finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## AEM SPA Editor {#aem-spa-editor}

Webbplatser som byggts med vanliga SPA, som React och Angular, läser in sitt innehåll med hjälp av dynamisk JSON. De innehåller inte den HTML-struktur som behövs för att AEM sidredigeraren ska kunna placera redigeringskontroller.

Om du vill aktivera redigering av SPA i AEM måste du mappa mellan JSON-utdata för SPA och innehållsmodellen i den AEM databasen så att du kan spara ändringar i innehållet.

SPA i AEM innehåller ett tunt JavaScript-lager som interagerar med den SPA JavaScript-koden när den läses in i sidredigeraren som händelser kan skickas med. Du kan aktivera platsen för redigeringskontrollerna för att tillåta kontextredigering. Den här funktionen bygger på API-slutpunktskonceptet för innehållstjänster eftersom innehållet från SPA måste läsas in via innehållstjänster.

En fullständig beskrivning av AEM SPA Editor finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## Antar befintliga SPA {#existing-spas}

Om du har en befintlig SPA har AEM stöd för att bädda in den i AEM så att den är synlig för innehållsförfattarna i AEM Editor. Den här funktionen kan vara användbar för att visa innehållet som de skapar med hjälp av innehållsfragment i slutprogrammet där det används.

Om du bara gör små ändringar kan du dessutom aktivera vissa redigeringsmöjligheter för de externa SPA i AEM Editor.

RemotePage-komponenten tillåter återgivning av en extern SPA i AEM.

En fullständig beskrivning av hur du gör en extern SPA redigerbar i AEM finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer detaljerad dokumentation.

## What&#39;s Next {#what-is-next}

Kom igång med att utveckla en egen SPA för AEM genom att läsa följande dokument:

* [SPA WKND - självstudiekurs](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Komma igång med React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Komma igång med Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Om du måste anpassa en befintlig SPA för att använda den i AEM, ska du granska följande dokument:

* [RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)
* [Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Nedan finns [ytterligare resurser](#additional-resources) som kan fördjupa dig SPA ämnen i AEM.

## Ytterligare resurser {#additional-resources}

Nedan följer ytterligare resurser som ger en djupdykning i några koncept som nämns i det här dokumentet.

* [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) - A description of the different delivery models available in AEM
* [SPA Introduktion och genomgång](/help/implementing/developing/hybrid/introduction.md) - en bra introduktion till SPA i AEM.
* [Utveckla SPA för AEM](/help/implementing/developing/hybrid/developing.md) - Riktlinjer för hur du utvecklar SPA för AEM
* [SPA Översikt över redigeraren](/help/implementing/developing/hybrid/editor-overview.md) - Information om hur SPA redigeraren fungerar
* [SPA Referensdokument](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript API-referenser och länkar till öppna AEM SPA GitHub-projekt
* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments) - Skapa innehållsfragment
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - Maven-mall som skapar ett minimalt, metodbaserat Adobe Experience Manager-projekt (AEM) som utgångspunkt för din webbplats
