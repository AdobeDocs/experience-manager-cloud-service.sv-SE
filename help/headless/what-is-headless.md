---
title: Vad är ett headless CMS?
description: Läs om Headless CMS. Hur fungerar de? Vilka är alternativen och skillnaderna? Varför vill du använda ett headless CMS?
source-git-commit: 35064ef7d9a4a3f2368667be02b11840b29d56f0
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# Vad är ett headless CMS? {#what-is-a-headless-cms}

Headless content management är en nyckelutveckling för dagens webbdesign som frigör klientapplikationer från serverdelen och fungerar som en länk till innehållshanteringssystemet. Ett headless CMS-system ansvarar därför för innehållshanteringstjänsterna (serverdelen) tillsammans med de mekanismer som gör det möjligt för (frontend)-programmen att komma åt innehållet.

Men vad betyder termen egentligen? Här erbjuder vi en (mycket snabb) introduktion till de viktigaste begreppen.

## Vad är ett CMS-system (Content Management System)? {#content-management-system}

Låt oss börja med grunderna - vad är ett innehållshanteringssystem?

Ett CMS-system (Content Management System) lagrar, hanterar och levererar det innehåll som används för att leverera onlineupplevelser.

## Traditionell CMS {#traditional-cms}

Traditionellt har ett CMS-system inkluderat både serverdelsfunktionaliteten för lagring och leverans av innehåll, tillsammans med klienttekniken som används för att återge markeringen för en upplevelse som webbläsaren visar (presentationslagret).

Mycket kraftfullt, vilket ger dig full kontroll över innehåll och formatering, men saknar en del av den flexibilitet som krävs i dagens snabbföränderliga miljö. till exempel vid interaktion med externa appar.

## Headless CMS {#headless-cms}

Med ett headless content management-system är serverdelen och klientdelen nu frikopplade.

Den headless delen är innehållets serverdel.

* &quot;*Ett headless innehållshanteringssystem, eller headless CMS, är ett CMS-system (back-end only content management system) som byggs från grunden som ett innehållsarkiv som gör innehållet tillgängligt via ett API för visning på vilken enhet som helst.*

   Se [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

FrontLine, som utvecklas och underhålls oberoende av varandra, hämtar innehåll från den headless-delen med ett Content Delivery API, vanligtvis i JSON-format. Detta kan till exempel vara ett React- eller Angular-program (Single Page Application (SPA)).

En headless CMS-serverdel kräver vanligtvis att innehållet är strukturerat, baserat på en modell eller ett schema. Detta underlättar för klientprogram som begär rätt innehåll för att återge en upplevelse. Vissa CMS-system kan visa både strukturerat och ostrukturerat innehåll i JSON-format.

En viktig egenskap i denna topologi är att innehåll som hanteras av det headless CMS i JSON-format är rent innehåll, utan design- eller layoutinformation. I en headless CMS-implementering bibehålls all formatering och layout av det fristående klientprogrammet.

En viktig fördel med en headless CMS-topologi är möjligheten att återanvända innehåll i flera kanaler, som kan använda olika klientimplementeringar. Detta kan effektivisera utvecklingsprocessen. Men det innebär också att utvecklingsprocessen för upplevelser kan bli mycket kods- och IT-inriktad, och IT-avdelningen äger i huvudsak upplevelsen.

## API:er för innehållsleverans {#content-delivery-apis}

Ett headless CMS-system kan tillhandahålla ett eller flera sätt att exponera innehåll för klientprogram. De flesta HTTP REST API:er, GraphQL API:er eller båda.

Även om ett REST API ofta verkar vara ett enklare sätt att begära innehåll (till exempel genom att tillhandahålla JSON för allt innehåll som uppfyller ett villkor), levererar de vanligtvis för mycket innehåll till ett klientprogram. Detta kan leda till att klienten måste analysera och filtrera bort det innehåll som faktiskt behövs för återgivningen.

GraphQL är däremot en mer fokuserad mekanism som gör det möjligt för klientapplikationer att fråga efter exakt det innehåll som behövs för att återge en upplevelse.

## CMS i fullhög {#fullstack-cms}

Ett CMS-system i full hög representerar vanligtvis den traditionella topologin för innehållshantering och innehållsleverans genom att inkludera tekniken för innehållsbackend och frontend för renderingsupplevelser. Leverans av innehåll i CMS-system i full hög sker vanligtvis via API:er för intern innehållsleverans. Gränssnittsfunktionaliteten är vanligtvis specifik för CMS-systemet i fullstacken. Den här kopplingen mellan klientteknik och innehållsbakgrund gör det möjligt att skapa WYSIWYG-upplevelser (what-you-see-is-what-you-get) som en viktig fördel.

## Hybrid-CMS {#hybrid-cms}

En modern utveckling av CMS-systemet i full hög kan vara ett hybrid-CMS-system. Syftet är att kombinera det bästa av två världar:

* effektiv frontend-utveckling i alla kanaler med moderna frontend-verktyg,
* samtidigt som man bevarar WYSIWYG-upplevelser för att ge icke-tekniska användare möjlighet, och för att undvika att IT blir en flaskhals för att kunna hantera innehåll och upplevelser i olika organisationer.

Detta uppnås genom att man använder sig av moderna frontramverk som React, men behåller ett viktigt minimum av koppling till innehållets serverdel.

## Kopplad CMS {#decoupled-cms}

Termen fristående CMS används ibland för att beskriva ett headless CMS-system genom att betona dess viktigaste egenskap att kopplas från klientens klientprogram.

## Huvudansvarig CMS {#headful-cms}

Detta är en annan term för ett traditionellt CMS-system.

## Ytterligare läsning {#further-reading}

Du kan läsa mer om hur du använder AEM i en headless CMS-topologi här:

* [Introduktion till Adobe Experience Manager som headless CMS](/help/headless/introduction.md)
