---
title: AEM för att skapa webbplatser snabbt
description: Börja här för en guidad resa med det lättanvända AEM snabbplatsverktyget som effektiviserar utvecklingen av AEM sajt och snabbt anpassar sajten utan någon AEM backend-kunskap.
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 1%

---

# AEM för att skapa webbplatser snabbt {#quick-site-creation-journey}

Börja här för en guidad resa med det lättanvända AEM snabbplatsverktyget som effektiviserar utvecklingen av AEM sajt och snabbt anpassar sajten utan någon AEM backend-kunskap.

## Introduktion {#introduction}

AEM Sites är en kraftfull verktygslåda för att skapa och hantera digitala upplevelser. Innehållsförfattare kan enkelt skapa digitala upplevelser med hjälp av webbplatsredigeraren och ordna innehållet med hjälp av webbplatskonsolen, samtidigt som de kan se innehållet live som det levereras av AEM till era målgrupper i alla kanaler.

Med AEM snabbverktyg kan andra användare snabbt skapa en ny webbplats från grunden med hjälp av webbplatsmallar. Med verktyget Skapa snabbwebbplats kan du snabbt anpassa temat och formatet för den AEM webbplatsen (JavaScript, CSS och statiska resurser). Detta gör att gränssnittsutvecklaren, som inte behöver ha någon kunskap om AEM, kan arbeta separat och parallellt med innehållsskaparna. Den AEM administratören laddar ned webbplatstemat och skickar det till den frontendutvecklare som anpassar det med sina favoritverktyg och sedan implementerar ändringarna i den AEM koddatabasen, som sedan distribueras.

Genom att eliminera all utvecklarkunskap för att skapa webbplatser, eliminera AEM kunskapsbehov för framtagning och låta temautvecklingen fortsätta parallellt med att innehåll skapas, snabbredigerar det AEM verktyget för framtagning av snabbwebbplatser avsevärt webbplatsens time-to-value och ökar möjligheten att anpassa och driftsätta webbplatsen.

## Videoöversikt {#video-overview}

Om du vill få en snabb översikt över den här funktionen i praktiken [kan du se den här fem minuter långa introduktionen.](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

Den här dokumentationsresan tar dig igenom alla funktioner i videon steg för steg och i detalj så att du förstår arbetsflödet och kan återskapa processen i din egen miljö.

## AEM dokumentationsresor {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) binder samman många olika och kanske komplicerade ämnen och funktioner genom att tillhandahålla en berättarröst som hjälper läsaren, som kan vara ny att AEM, förstå och lösa ett affärsproblem från början till slut, samtidigt som man antar minimala tidigare ämnesområden eller AEM kunskap.

Dokumentation Journeys bygger på principer för god praxis, grundade på Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe konsulter och återkoppling från kundprojekt.

Om du vill veta hur Adobe rekommenderar hur man löser webbplatsaffärsärenden med AEM, är AEM Sites Journeys där man ska börja.

## Målgrupp {#audience}

Den här resan innehåller krav, steg och tillvägagångssätt för att anpassa AEM Sites-teman. Dess främsta målgrupp är den främsta utvecklaren, som inte behöver någon kunskap om AEM. För att illustrera hela processen använder man administratörer som antas ha grundläggande kunskaper i AEM Sites och Cloud Manager. I praktiken kan flera personer betjäna flera roller och den här resan stöder perspektiv både från administratörer och gränssnittsutvecklare.

| Persona | Beskrivning | Roll på resan |
|---|---|---|
| Front-End Developer | Anpassar webbplatstemat | Tar temat från AEM administratör och anpassar det så att det kan distribueras till den AEM webbplatsen. |
| Innehållsförfattare | Skapar och hanterar innehåll som levereras som webbplatser | Innehållsförfattare skapar innehåll på AEM som renderas med det tema som anpassats av den som utvecklar innehållet. |
| AEM-administratör | Skapar en ny AEM | Den AEM administratören skapar en ny webbplats som bygger på en mall och förser sedan frontendutvecklaren med ett tema som kan anpassas. |
| Administratör för Cloud Manager | Skapar rörledningar och beviljar åtkomst | Cloud Manager-administratören skapar frontendriet och ger frontendutvecklare åtkomst så att de kan implementera anpassningar i AEM Git-databasen. |

## Den AEM snabbaste vägen för webbplatsskapande {#the-journey}

Du kommer att utforska många ämnen under den här resan. I följande artiklar får du grundläggande kunskaper om hur du skapar och anpassar AEM webbplatser med verktyget Skapa snabbwebbplats och länkar till detaljerad teknisk dokumentation.

| # | Artikel | Beskrivning | Ansvarig roll |
|---|---|---|--|
| 0 | AEM för att skapa webbplatser snabbt | Det här dokumentet | Administratörer för AEM &amp; Cloud Manager |
| 1 | [Förstå Cloud Manager och arbetsflödet för att skapa snabbwebbplatser](cloud-manager.md) | Lär dig mer om Cloud Manager och hur det knyter ihop den nya processen för att skapa snabbwebbplatser. | AEM-administratör |
| 2 | [Skapa webbplats från mall](create-site.md) | Lär dig hur du snabbt skapar en ny AEM med hjälp av en webbplatsmall. | AEM-administratör |
| 3 | [Konfigurera din pipeline](pipeline-setup.md) | Skapa en pipeline för frontend för att hantera anpassningen av webbplatsens tema. | Administratör för Cloud Manager |
| 4 | [Bevilja åtkomst till klientutvecklaren](grant-access.md) | Anlita gränssnittsutvecklare i Cloud Manager så att de får tillgång till era AEM och er pipeline. | Administratör för Cloud Manager |
| 5 | [Hämta åtkomstinformation för Git-databasen](retrieve-access.md) | Läs om hur frontendutvecklaren använder Cloud Manager för att få åtkomst till Git-databasinformation. | Front-End Developer |
| 6 | [Anpassa webbplatstemat](customize-theme.md) | Lär dig hur ett webbplatstema byggs, hur du anpassar det och hur du testar det med AEM innehåll. | Front-End Developer |
| 7 | [Distribuera ditt anpassade tema](deploy-theme.md) | Lär dig hur du distribuerar webbplatstemat med hjälp av pipeline. | Front-End Developer |

## What&#39;s Next {#what-is-next}

Du är nu redo att komma igång med din Adobe-resa för att skapa snabbwebbplatser.

* Om du är administratör för AEM eller Cloud Manager, eller om du har både avancerade utvecklings- och administratörsroller, eller om du bara vill förstå hela processen i AEM, börjar du i början av resan med [Förstå Cloud Manager](cloud-manager.md) enligt nedan.
* Om du bara ansvarar för frontend-utvecklingen och kommer att interagera med administratörerna för AEM och Cloud Manager kan du hoppa direkt till [Hämta åtkomstinformation för Git-databasen](retrieve-access.md) för att få åtkomst till AEM Git-databasen och börja anpassa.
* Om du redan är insatt i att AEM Sites och Cloud Manager fungerar ihop och vill börja direkt med konfigurationen kan du [gå direkt till att skapa en ny plats från en mall.](create-site.md)

## Ytterligare resurser {#additional-resources}

Här finns mer information om hur AEM kraftfulla funktioner fungerar tillsammans.

* [AEM as a Cloud Service teknisk dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - Om du redan har en god förståelse för AEM kan du behöva läsa de detaljerade tekniska dokumenten direkt.
* [Dokumentation för webbplatsadministration](/help/sites-cloud/administering/site-creation/create-site.md) - Läs de tekniska dokumenten om hur du skapar webbplatser för mer information om funktionerna i verktyget Skapa snabbwebbplats.
