---
title: Introduktion till Universal Editor
description: Läs om hur du i Universell redigerare kan redigera vad du vill - se - vad du får (WYSIWYG) oavsett vilken headlessupplevelse du har. Förstå hur det kan hjälpa innehållsförfattare att leverera enastående upplevelser, öka innehållets hastighet och hur det ger en toppmodern utvecklarupplevelse.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a77bff14b34f1e433ba185b19f0f0d61728b7c7a
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---


# Introduktion till Universal Editor {#introduction}

Universal Editor är en mångsidig visuell editor som ingår i Adobe Experience Manager Sites. Man kan redigera det man redan gjort - se-is-what-you-get (WYSIWYG) - oavsett om det handlar om headless eller headful experience. Förstå hur det kan hjälpa innehållsförfattare att leverera enastående upplevelser och hur det erbjuder oöverträffad frihet för utvecklare.

## Bakgrund {#background}

Universell redigerare ger en effektiv och intuitiv kontextredigeringsfunktion som kräver minimal utbildning. Med det kan författare hantera sitt innehåll direkt i webbupplevelsen, precis så som det kommer att se ut för besökarna. Eftersom den är en riktig redigerare som en tjänst och generellt sett mer flexibel kommer den att ersätta sidredigeraren.

Den universella redigeraren har stor flexibilitet eftersom den har stöd för samma visuella redigering för alla typer av AEM: redigering på plats och layoutdisposition är möjlig både för innehållsfragment och sidkomponenter. De två typerna av innehåll kan till och med redigeras när de visas sida vid sida i en webbupplevelse, utan att författarna behöver ändra sitt sammanhang. Detta är en enorm förbättring jämfört med tidigare redigerare i AEM som bara stöder en viss typ av innehåll.

Utvecklarna drar nytta av universella redigerares mångsidighet eftersom den även stöder en sann frikoppling av implementeringen. Det gör att utvecklare kan använda praktiskt taget vilket ramverk eller vilken arkitektur de vill, utan att införa några begränsningar för SDK eller teknik. Den här flexibiliteten gör det även enkelt att instrumentera befintliga webbprogram för den universella redigeraren utan att behöva arkitekturera om dem.

## Helt universell {#universal}

Den universella redigeraren kan användas för alla implementeringar, för vilket innehåll som helst och för alla delar av innehållet.

![Vad gör den universell](assets/universal.png)

### Alla implementeringar {#any-implementation}

Eftersom upplevelser kan byggas på många olika sätt kan alla implementeringar använda den universella redigeraren så att författare kan redigera i sitt sammanhang.

Användare tror ofta att en headless-implementering begränsar författarens möjlighet att redigera allt innehåll i ett formulärbaserat användargränssnitt, men så är inte fallet med den universella redigeraren

Kraven för en implementering som ska använda den universella redigeraren är raka framifrån och stöder följande:

* **Valfri arkitektur** - Återgivning på serversidan, edge-side-återgivning, rendering på klientsidan osv.
* **Alla ramverk** - Vanilla-AEM eller andra tredjepartsramverk som React, Next.js, Angular och så vidare.
* **Valfri värdtjänst** - Kan lagras lokalt på AEM eller på en fjärrdomän

### Allt innehåll {#any-content}

En innehållsförfattare bör ha samma kraftfulla redigeringsupplevelse som den AEM sidredigeraren. Men den universella redigeraren tillåter innehållsförfattare att redigera **vilket**-innehåll som helst visuellt och i sitt sammanhang och stöder:

* **AEM sidstrukturer** - kapslade `cq:Components` av `cq:Pages`, inklusive Experience Fragments
* **AEM Innehållsfragment** - Redigera innehåll från innehållsfragment så som de visas i sammanhanget för upplevelsen.
* **Dokument** - Konceptkorrektur har visat att även Word-, Excel-, Google-dokument eller Markup-dokument kan redigeras på samma sätt (detta är Pågående arbete).

### Alla proportioner {#any-aspect}

Innehållet handlar inte bara om informationen som finns, utan även om hur det återges och tas emot. Innehållet innehåller ytterligare metadata och instrumenteringsregler som den universella redigeraren kan förstå och redigera, inklusive:

* **Använda layout och format** - Genom att använda ett formatsystem kan marknadsföraren och innehållsförfattaren tillämpa olika format på sitt innehåll och skapa olika layouter för innehåll som kolumner, karuseller, flikar, dragspel och så vidare.

## Värde {#value}

Genom att frikoppla redigeringsupplevelsen från ett visst innehållsleveranssystem blir redigeraren helt universell och flexibel så att innehållsförfattaren kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.

![Värdet för den universella redigeraren](assets/value.png)

* **Leverera exceptionella upplevelser** - För att yrkesverksamma ska kunna skapa en övertygande upplevelse för besökare kan de yrkesverksamma i den universella redigeraren skapa och redigera innehållet i förhandsvisningssammanhang. På så sätt kan de skapa innehåll som passar upplevelsens design och som utgör en meningsfull resa för besökarna.
* **Öka innehållshastigheten** - För att effektivisera administrationsarbetsflödet för granskare tillåter den universella redigeraren redigering av innehåll i förhandsgranskningen som vägledning för användarna genom att endast visa de alternativ som är relevanta för det sammanhanget och gör arbetsflödet oberoende av innehållskällorna.
* **Den senaste utvecklarupplevelsen** - För att stödja heterogena programlandskap i verkligheten är den universella redigeraren helt fristående och teknikberoende, vilket gör att utvecklare kan använda den teknologi de föredrar för att implementera upplevelsen.

## Universal Editor och Content Fragment Editor {#universal-editor-content-fragment-editor}

Vid första anblicken kan det verka som den universella redigeraren och Content Fragment Editor har liknande redigeringsfunktioner. Men de här redigerarna har mycket olika funktioner och de utför olika arbetsuppgifter för marknadsföringsavdelningen.

### Innehållsfragmentsredigerare {#content-fragment-editor}

En marknadsförare vill skapa innehåll utan att behöva bry sig om layouten, så att det kan återanvändas i många sammanhang av upplevelsen.

* Det underliggande jobbet är att skala innehållsstrategin.

### Universal Editor {#universal-editor}

En marknadsförare vill skapa innehåll som är skräddarsytt efter layouten i ett visst sammanhang för att leverera en exceptionell upplevelse.

* Det underliggande jobbet är att på ett övertygande sätt få kontakt med läsarna.

## Begränsningar {#limitations}

När du utforskar den universella redigeraren och fortsätter implementera den i dina egna projekt bör du tänka på följande begränsningar.

* Högst 25 AEM (innehållsfragment, sidor, Experience Fragments, Assets osv.) ska vara referenser som instrumentering på en enda sida.
* AEM as a Cloud Service är den enda AEM som stöds.
* AEM as a Cloud Service version `2023.8.13099` eller senare krävs.
* Innehållsförfattare måste ha sina egna Experience Cloud-konton.
* Chrome och Edge stöds

{{ue-ip-allow-lists}}

## Nästa steg {#next-steps}

Läs dokumentet [Universal Editor Use Case and Learning Paths](/help/implementing/universal-editor/use-cases.md) om du vill veta mer om vanliga användningsfall för Universal Editor och hitta rätt dokumentationsresurser för ditt projekt.
