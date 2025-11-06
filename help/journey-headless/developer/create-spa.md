---
title: Valfritt - Så här skapar du SPA-program (Single Page Applications) med Adobe Experience Manager (AEM)
description: I den här valfria fortsättningen av AEM Headless Developer Journey får du lära dig hur AEM kan kombinera headless-leverans med traditionella CMS-funktioner i full hög och hur du kan skapa redigerbara SPA-program med AEM SPA Editor Framework.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# Skapa SPA-program (Single Page Applications) med AEM {#create-spa}

I den här valfria fortsättningen av [AEM Headless Developer Journey](overview.md) får du lära dig hur AEM kan kombinera headless-leverans med traditionella CMS-funktioner i full hög. Du får också lära dig hur du kan skapa redigerbara SPA-program med AEM SPA Editor och integrera externa SPA-program, vilket möjliggör redigeringsfunktioner efter behov.

## Story hittills {#story-so-far}

Nu ska du ha slutfört hela [AEM Headless Developer Journey](overview.md) och förstå grunderna för headless-leverans i AEM, inklusive en förståelse för:

* Skillnaden mellan headless och headful content delivery.
* AEM headless-funktioner.
* Så här organiserar du och AEM Headless-projekt.
* Så här skapar du headless-innehåll i AEM.
* Så här hämtar och uppdaterar du headless-innehåll i AEM.
* Så här lever du i ett AEM Headless-projekt.

Fram tills nu har du antingen gått live med ditt första AEM Headless-projekt eller haft vetskap om att göra det. Grattis!

Varför läser du den här extra, valfria fortsatta resan? I [Getting Started](getting-started.md#integration-levels) diskuterades hur AEM inte bara stöder headless-leverans och traditionella helstacksmodeller, utan även hybridmodeller som kombinerar fördelarna med båda. Även om det inte är den traditionella headless-modellen kan sådana hybridmodeller ge oöverträffad flexibilitet till vissa projekt.

Den här artikeln bygger på dina kunskaper om AEM Headless genom att ingående utforska hur du kan skapa egna SPA-program (single page applications) som kan redigeras i AEM. På så sätt kan du skapa innehåll och leverera det utan problem till en SPA, men SPA kan fortfarande redigeras i AEM.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur Single Page-program utvecklas med AEM SPA Editor. När du har läst det här dokumentet bör du:

* Förstå SPA-redigerarens grundläggande funktioner.
* Ta reda på vad som krävs för att skapa en fullt redigerbar SPA för AEM.
* Förstå hur externa SPA kan integreras i AEM.
* Förstå hur rendering på serversidan kan eller inte kan implementeras.

## Krav och krav {#requirements-prerequisites}

Det finns flera krav innan du börjar arbeta med SPA i AEM.

### Kunskap {#knowledge}

* Utvecklingserfarenhet som skapar SPA med React- eller Angular-ramverk
* AEM grundläggande kunskaper i att skapa innehållsfragment och använda redigeraren
* Läs dokumentet [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) så att du kan förstå de olika nivåerna av SPA-integrering.

### verktyg {#tools}

* Sandlådeåtkomst för testning av driftsättning av ditt projekt
* Lokal utvecklingsinstans för datamodellering och -testning
* Befintlig extern SPA (valfritt, beroende på vilken integrationsmodell som väljs)
* AEM Project Archetype

## Vad är en SPA? {#what-is-a-spa}

Ett SPA-program (single-page application) skiljer sig från en konventionell sida genom att det återges på klientsidan och i första hand är JavaScript-styrt, beroende på att Ajax anropar för att läsa in data och dynamiskt uppdatera sidan. Det mesta, eller allt, innehållet hämtas en gång på en sida och ytterligare resurser läses in asynkront efter behov, baserat på användarinteraktionen med sidan.

Den här funktionen minskar behovet av uppdatering av sidor och ger användaren en upplevelse som är smidig, snabb och som känns mer som en appupplevelse.

Med AEM SPA Editor kan gränssnittsutvecklare skapa SPA som kan integreras i en AEM-webbplats, vilket gör att innehållsförfattarna kan redigera SPA-innehållet lika enkelt som annat AEM-innehåll.

## Varför en SPA? {#why-spa}

Genom att vara snabbare, smidigare och mer som ett systemspecifikt program blir SPA en attraktiv upplevelse. Det passar inte bara besökaren på webbsidan, utan även marknadsförare och utvecklare på grund av hur SPA fungerar.

En fullständig beskrivning av SPA och varför du skulle använda dem finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## Hur AEM hanterar SPA

Utveckla single page-applikationer på AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om ni som frontendutvecklare följer dessa allmänna bästa metoder och några AEM-specifika principer, kan er SPA fungera med AEM och dess funktioner för innehållsutveckling.

* **Portabilitet** - Precis som med andra komponenter bör SPA-komponenterna byggas så att de är så portabla som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **AEM Drives Site Structure** - front-end-utvecklaren skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **Dynamisk återgivning** - All återgivning ska vara dynamisk.
* **Dynamisk routning** - SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

En fullständig beskrivning av hur AEM hanterar SPA finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## AEM SPA Editor {#aem-spa-editor}

Webbplatser som byggts med vanliga SPA-ramverk, som React och Angular, läser in sitt innehåll med hjälp av dynamisk JSON. De innehåller inte den HTML-struktur som krävs för att sidredigeraren i AEM ska kunna placera redigeringskontroller.

Om du vill kunna redigera SPA-filer i AEM måste du mappa mellan JSON-utdata för SPA och innehållsmodellen i AEM-databasen så att du kan spara ändringar i innehållet.

Stöd för SPA i AEM introducerar ett tunt JavaScript-lager som interagerar med SPA JavaScript-koden när den läses in i sidredigeraren som händelser kan skickas med. Du kan aktivera platsen för redigeringskontrollerna för att tillåta kontextredigering. Den här funktionen bygger på API-slutpunktskonceptet för innehållstjänster eftersom innehållet från SPA måste läsas in via innehållstjänster.

En fullständig beskrivning av AEM SPA Editor finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer utförlig dokumentation.

## Anpassa befintliga SPA {#existing-spas}

Om du har ett befintligt SPA-program kan AEM bädda in det i AEM så att det blir synligt för dina innehållsförfattare i AEM Editor. Den här funktionen kan vara användbar för att visa innehållet som de skapar med hjälp av innehållsfragment i slutprogrammet där det används.

Med endast små ändringar kan du dessutom aktivera vissa redigeringsmöjligheter för den externa SPA-filen i AEM Editor.

RemotePage-komponenten tillåter återgivning av en extern SPA i AEM.

En fullständig beskrivning av hur du gör en extern SPA redigerbar i AEM finns i avsnittet [ytterligare resurser](#additional-resources) för länkar till mer ingående dokumentation.

## What&#39;s Next {#what-is-next}

Kom igång med att utveckla egna SPA för AEM genom att läsa följande dokument:

* [SPA WKND - självstudiekurs](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Komma igång med React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Komma igång med Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Om du måste anpassa en befintlig SPA för att använda den i AEM kan du läsa följande dokument:

* [RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)
* [Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Nedan finns [ytterligare resurser](#additional-resources) som kan fördjupa dig i SPA-ämnen i AEM.

## Ytterligare resurser {#additional-resources}

Nedan följer ytterligare resurser som ger en djupdykning i några koncept som nämns i det här dokumentet.

* [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) - A description of the different delivery models available in AEM
* [SPA-introduktion och genomgång](/help/implementing/developing/hybrid/introduction.md) - en bra introduktion till SPA i AEM.
* [Utveckla SPA för AEM](/help/implementing/developing/hybrid/developing.md) - Riktlinjer för hur du utvecklar SPA för AEM
* [Översikt över SPA-redigeraren](/help/implementing/developing/hybrid/editor-overview.md) - Information om hur SPA-redigeraren fungerar
* [SPA-referensdokument](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript API-referenser och länkar till AEM SPA GitHub-projekt med öppen källkod
* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments) - Skapa innehållsfragment
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE) - Maven-mall som skapar ett minimalt, metodbaserat Adobe Experience Manager-projekt (AEM) som utgångspunkt för din webbplats
