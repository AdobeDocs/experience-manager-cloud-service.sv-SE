---
title: Så här publicerar den universella redigeraren innehåll
description: Lär dig hur den universella redigeraren publicerar sitt innehåll, hur det skiljer sig från processen i Sites Console och hur du tar hänsyn till hur du utvecklar dina egna program för att arbeta med det.
feature: Developing
role: Admin, Developer
exl-id: 60f0bb4a-ee60-4f73-83ae-8568735474ad
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Så här publicerar den universella redigeraren innehåll {#publishing}

Lär dig hur den universella redigeraren publicerar sitt innehåll, hur det skiljer sig från processen i Sites Console och hur du tar hänsyn till hur du utvecklar dina egna program för att arbeta med det.

>[!TIP]
>
>I den här artikeln finns information om den universella redigerarens publiceringsprocess för utvecklaren. [Processen att publicera ditt innehåll beskrivs här för innehållsförfattaren.](/help/sites-cloud/authoring/universal-editor/publishing.md)

## Likheter med platskonsolprocessen {#similarities}

För användare av [AEM sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md) och [ webbplatskonsolen](/help/sites-cloud/authoring/sites-console/introduction.md) fungerar processen att publicera innehåll med den universella redigeraren som du är van vid: vid publicering i AEM replikeras innehållet från författartjänsten till publiceringstjänsten (eller till [förhandsgranskningstjänsten](/help/sites-cloud/authoring/sites-console/previewing-content.md) om den är tillgänglig och beroende på vilka alternativ författaren väljer vid publiceringen.)

## Skillnader {#differences}

Det som gör publicering med den universella redigeraren lite annorlunda är inte så mycket själva redigeraren, utan snarare den externa värdfunktionen för appen som den universella redigeraren gör möjlig.

När det finns en extern värd är det webappens sak att se till att innehåll läses in från författartjänsten när appen öppnas av författare i redigeraren, och att det läses in från publiceringstjänsten när besökarna öppnar appen.

## Identifiera tjänsten i appen {#detecting}

Avgör om författaren eller publiceringstjänsten ska vara tillgänglig genom en enkel villkorssats i appen och väljer lämplig författare eller publiceringsslutpunkt när den upptäcker att den öppnas i redigeraren.

Ett annat alternativ är att distribuera appen till två olika miljöer som är konfigurerade på olika sätt, så att man hämtar dess innehåll från redigeringstjänsten och hämtar det från publiceringstjänsten. För att författare ska kunna öppna den publicerade URL:en i Universell redigerare kan ett litet skript skapas för att&quot;konvertera&quot; URL:en för publiceringssidan till motsvarande URL:er i författarmiljön (t.ex. genom att en `author`-underdomän försätts), så att författarna automatiskt omdirigeras.

## Sammanfattning {#summary}

Målet för den universella redigeraren är att inte införa något visst mönster, så att implementeringen bäst kan uppnå sina mål på ett helt fristående sätt samtidigt som allt förblir enkelt och rakt framåt för implementeringen.

Det finns heller inga krav på hur ett visst projekt ska fungera när det gäller att avgöra från vilken tjänst innehållet ska levereras. Det ger snarare flera möjligheter och låter projektet avgöra vilken lösning som är bäst för sina egna behov.

## Ytterligare resurser {#additional-resources}

Mer information om de tekniska detaljerna i Universal Editor finns i dessa utvecklardokument.

* [Introduktion till universell redigering](/help/implementing/universal-editor/introduction.md) - Lär dig hur den universella redigeraren kan redigera alla delar av innehåll i alla implementeringar så att du kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.
* [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md) - Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM-program.
* [Universell redigeringsarkitektur](/help/implementing/universal-editor/architecture.md) - Lär dig mer om arkitekturen för den universella redigeraren och hur data flödar mellan dess tjänster och lager.
* [Attribut och typer](/help/implementing/universal-editor/attributes-types.md) - Lär dig mer om de dataattribut och datatyper som krävs för den universella redigeraren.
* [Autentisering av universell redigerare](/help/implementing/universal-editor/authentication.md) - Lär dig hur den universella redigeraren autentiseras.
