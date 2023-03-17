---
title: Introduktion till Universal Editor
description: Se hur den universella redigeraren kan redigera alla delar av innehållet i alla implementeringar för att leverera enastående upplevelser, öka innehållets hastighet och ge en toppmodern utvecklarupplevelse.
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---


# Introduktion till Universal Editor {#introduction}

Se hur den universella redigeraren kan redigera alla delar av innehållet i alla implementeringar för att leverera enastående upplevelser, öka innehållets hastighet och ge en toppmodern utvecklarupplevelse.

## Bakgrund {#background}

Det kraftfullaste verktyget för den som skapar AEM innehåll är sidredigeraren. Sidredigeraren är en intuitiv, visuell, sammanhangsberoende WYSIWYG-redigeringsfunktion som kräver minimal utbildning och som visar författarna exakt hur innehållet kommer att se ut.

Men sidredigeraren kan bara redigera AEM sidinnehåll, struktur och de komponenter som ingår i den. Dagens innehåll hämtas dock sällan från ett och samma ställe. Den universella redigeraren erbjuder samma redigeringsupplevelse på plats som sidredigeraren, men för alla delar av innehållet i alla implementeringar.

## Helt universell {#universal}

Den universella redigeraren kan användas för alla implementeringar, för vilket innehåll som helst och för alla delar av innehållet.

![Vad gör den universell](assets/universal.png)

### Alla implementeringar {#any-implementation}

Eftersom upplevelserna kan byggas på många olika sätt kan alla implementeringar utnyttja den universella redigeraren så att författarna kan redigera i sitt sammanhang.

Användare tror ofta att en headless-implementering begränsar författarens möjlighet att redigera allt innehåll i ett formulärbaserat användargränssnitt, men detta stämmer inte med den universella redigeraren

Kraven för att implementeringen ska kunna utnyttja den universella redigeraren är mycket enkla och har stöd för:

* **Valfri arkitektur** - Återgivning på serversidan, edge-side-återgivning, rendering på klientsidan osv.
* **Alla ramverk** - Vanilla AEM, eller andra ramverk från tredje part som React, Next.js, Angular osv.
* **Alla värdtjänster** - Kan lagras lokalt på AEM eller på en fjärrdomän

### Allt innehåll {#any-content}

En innehållsförfattare bör ha samma kraftfulla redigeringsupplevelse som den AEM sidredigeraren. Men med den universella redigeraren kan skribenterna redigera **alla** innehåll visuellt och i sitt sammanhang och har stöd för

* **AEM sidstrukturer** - Kapslad `cq:Components` av `cq:Pages`, inklusive Experience Fragments
* **AEM innehållsfragment** - Redigera innehåll från innehållsfragment när de visas i sitt sammanhang
* **Dokument** - Word, Excel, Google Docs, Markdown eller t.o.m. normal HTML beständig, t.ex. på GitHub
* **Innehåll från tredje part** - Ett plugin-system gör att det går att redigera externa innehållskällor.

### Alla proportioner {#any-aspect}

Innehållet handlar inte bara om informationen som finns, utan även om hur det återges och tas emot. Innehållet innehåller ytterligare metadata och instrumenteringsregler som den universella redigeraren kan förstå och redigera, inklusive:

* **Använda layout och format** - Genom att använda ett formatsystem kan marknadsförare och innehållsförfattare tillämpa olika format på sitt innehåll och skapa olika layouter som kolumner, bildspel, flikar, dragspel osv.
* **Utföra experiment** - Genom att publicera en ny innehållsversion som utmanar det befintliga innehållet kan marknadsföraren experimentera med innehållsförbättringar och mäta effekten.
* **Anpassa variationer** - Genom att skapa och hantera innehållsvariationer som är specifika för en viss målgrupp kan marknadsförare personalisera det innehåll som levereras.

## Värde {#value}

Genom att frikoppla redigeringsupplevelsen från ett visst innehållsleveranssystem blir redigeraren helt universell och flexibel så att innehållsförfattaren kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.

![The value of the Universal Editor](assets/value.png)

* **Leverera exceptionella upplevelser** - För att yrkesutövare ska kunna skapa en övertygande upplevelse för besökarna kan de som arbetar med den universella redigeraren skapa och redigera innehållet i förhandsgranskningssammanhang. På så sätt kan de skapa innehåll som passar upplevelsens design och som utgör en meningsfull resa för besökarna.
* **Öka innehållshastigheten** - För att effektivisera yrkesutövarnas arbetsflöde tillåter den universella redigeraren redigering av innehåll i förhandsgranskningen som vägledning för användarna genom att endast visa de alternativ som är relevanta för det sammanhanget och som gör arbetsflödet oberoende av innehållskällorna.
* **Avancerad utvecklarupplevelse** - För att stödja heterogena applikationslandskap i verkligheten är den universella redigeraren helt fristående och teknikberoende, vilket gör att utvecklare kan använda den teknologi de föredrar för att implementera upplevelsen.

## Universal Editor och Content Fragment Editor {#universal-editor-content-fragment-editor}

Vid första anblicken kan det verka som den universella redigeraren och Content Fragment Editor har liknande redigeringsfunktioner. Men de här redigerarna har mycket olika funktioner och de utför olika arbetsuppgifter för marknadsföringsavdelningen.

### Innehållsfragmentsredigerare {#content-fragment-editor}

En marknadsförare vill skapa innehåll utan att behöva bry sig om layouten, så att det kan återanvändas i många sammanhang av upplevelsen.

* Det underliggande jobbet är att skala innehållsstrategin.

### Universal Editor {#universal-editor}

En marknadsförare vill skapa innehåll som är skräddarsytt efter layouten i ett visst sammanhang för att leverera en exceptionell upplevelse.

* Det underliggande jobbet är att på ett övertygande sätt få kontakt med läsarna.

## Vägkarta {#road-map}

Det är viktigt att komma ihåg att den universella redigeraren är ett pågående arbete och att funktionerna i det här dokumentet är en vision för den slutliga redigeraren och inte nödvändigtvis dess nuvarande funktioner.

Kontakta din Adobe-kontakt för mer information om kommande funktioner som planeras för den universella redigeraren

## Ytterligare resurser {#additional-resources}

Mer information om Universal Editor finns i de här dokumenten.

* [Skapa innehåll med den universella redigeraren](authoring.md) - Lär dig hur enkelt och intuitivt det är för skribenter att skapa innehåll med den universella redigeraren.
* [Komma igång med Universal Editor i AEM](getting-started.md) - Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.
* [Universal Editor Architecture](architecture.md) - Lär dig mer om arkitekturen i den universella redigeraren och hur data flödar mellan tjänster och lager.
* [Attribut och typer](attributes-types.md) - Läs mer om de dataattribut och datatyper som krävs för den universella redigeraren.
* [Autentisering av universell redigerare](authentication.md) - Lär dig hur den universella redigeraren autentiseras.
