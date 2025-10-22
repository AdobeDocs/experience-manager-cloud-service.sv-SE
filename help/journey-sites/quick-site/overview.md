---
title: AEM Quick Site Creation-resa
description: Börja här för en guidad resa med det lättanvända verktyget AEM Quick Site Creation som effektiviserar framtagningen av AEM Site och snabbt anpassar sajten utan kunskaper om AEM bakgrunder.
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 1%

---


# AEM Quick Site Creation-resa {#quick-site-creation-journey}

{{traditional-aem}}

Börja här för en guidad resa med det lättanvända verktyget AEM Quick Site Creation som effektiviserar framtagningen av AEM Site och snabbt anpassar sajten utan kunskaper om AEM bakgrunder.

## Introduktion {#introduction}

AEM Sites är en kraftfull verktygslåda för att skapa och hantera digitala upplevelser. Innehållsförfattare kan enkelt skapa digitala upplevelser med hjälp av webbplatsredigeraren och ordna innehållet med hjälp av webbplatskonsolen, samtidigt som de kan se innehållet live när det levereras av AEM till era målgrupper i alla kanaler.

Med verktyget AEM Quick Site Creation kan man snabbt skapa en helt ny webbplats med hjälp av mallar. Med verktyget Skapa snabbwebbplats kan du snabbt anpassa temat och formatet för AEM-webbplatsen (JavaScript, CSS och statiska resurser). Detta gör att den som inte har någon kunskap om AEM kan arbeta separat och parallellt med de som skapar materialet. AEM-administratören laddar bara ned webbplatstemat och skickar det till den frontutvecklare som anpassar det med sina favoritverktyg och sedan implementerar ändringarna i AEM koddatabas, som sedan distribueras.

Genom att eliminera all utvecklarkunskap för att skapa webbplatser, eliminera AEM kunskapskrav för framtagning och låta temautvecklingen fortsätta parallellt med att innehåll skapas, snabbar AEM snabbverktyg upp utvecklingen av webbplatsen och ökar flexibiliteten för webbplatsanpassning och driftsättning.

## Videoöversikt {#video-overview}

[Du kan se den här fem minuter långa introduktionen](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw) om du vill få en snabb översikt av den här funktionen.

Den här dokumentationsresan tar dig igenom alla funktioner i videon steg för steg och i detalj så att du förstår arbetsflödet och kan återskapa processen i din egen miljö.

## AEM Documentation Journeys {#documentation-journeys}

[En dokumentationsresa](/help/journey-documentation/documentation-journeys.md) knyter ihop många olika, komplicerade ämnen och funktioner genom att tillhandahålla en berättarröst som hjälper läsaren, som kan vara nybörjare på AEM, att förstå och lösa ett affärsproblem från början till slut, samtidigt som man utgår från minimala tidigare ämnesområden eller AEM kunskaper.

Dokumentationsresor har utformats utifrån principer för god praxis som bygger på Adobe senaste forskning, beprövade implementeringserfarenheter från Adobe konsulter och feedback från kundprojekt.

Om du vill veta hur Adobe rekommenderar dig att lösa webbplatsaffärsärenden med AEM är AEM Sites Journeys startpunkt.

## Målgrupp {#audience}

Den här resan innehåller krav, steg och tillvägagångssätt för att anpassa AEM Sites-teman. Dess främsta målgrupp är frontutvecklaren, som inte behöver några kunskaper om AEM. För att illustrera hela processen arbetar man dock med administratörer som antas ha grundläggande kunskaper i AEM Sites och Cloud Manager. I praktiken kan flera personer betjäna flera roller och den här resan stöder perspektiv både från administratörer och gränssnittsutvecklare.

| Persona | Beskrivning | Roll på resan |
|---|---|---|
| Front-End Developer | Anpassar webbplatstemat | Använd temat från AEM-administratören och anpassa det så att det kan distribueras till AEM webbplats. |
| Innehållsförfattare | Skapar och hanterar innehåll som levereras som webbplatser | Innehållsförfattare skapar innehåll på AEM som renderas med det tema som anpassats av den som utvecklar innehållet. |
| AEM-administratör | Skapar en ny AEM-webbplats | AEM-administratören skapar en ny webbplats baserad på en mall och ger sedan frontendutvecklaren ett tema som kan anpassas. |
| Cloud Manager Administrator | Skapar rörledningar och beviljar åtkomst | Cloud Manager Administrator skapar frontendinje och ger frontendutvecklare åtkomst så att de kan implementera anpassningar i AEM Git-databasen. |

## AEM Quick Site Creation-resa {#the-journey}

Du kommer att utforska många ämnen under den här resan. I följande artiklar får du grundläggande kunskaper om hur du skapar och anpassar AEM-webbplatser med verktyget Skapa snabbt och länkar till detaljerad teknisk dokumentation.

| # | Artikel | Beskrivning | Ansvarig roll |
|---|---|---|--|
| 0 | AEM Quick Site Creation-resa | Det här dokumentet | Administratörer för AEM och Cloud Manager |
| 1 | [Förstå Cloud Manager och arbetsflödet för att skapa snabbwebbplatser](cloud-manager.md) | Läs om Cloud Manager och hur det knyter ihop den nya processen för att skapa snabbwebbplatser. | AEM-administratör |
| 2 | [Skapa webbplats från mall](create-site.md) | Lär dig hur du snabbt skapar en AEM-webbplats med hjälp av en webbplatsmall. | AEM-administratör |
| 3 | [Konfigurera din pipeline](pipeline-setup.md) | Skapa en pipeline för frontend för att hantera anpassningen av webbplatsens tema. | Cloud Manager Administrator |
| 4 | [Bevilja åtkomst till frontendutvecklaren](grant-access.md) | Anlita gränssnittsutvecklarna till Cloud Manager så att de får tillgång till AEM webbplats via lagringsplats och pipeline. | Cloud Manager Administrator |
| 5 | [Hämta åtkomstinformation för Git-databasen](retrieve-access.md) | Läs om hur frontendutvecklaren använder Cloud Manager för att få åtkomst till Git-databasinformation. | Front-End Developer |
| 6 | [Anpassa webbplatstemat](customize-theme.md) | Lär dig hur ett webbplatstema byggs, hur du anpassar det och hur du testar det med AEM Live-innehåll. | Front-End Developer |
| 7 | [Distribuera ditt anpassade tema](deploy-theme.md) | Lär dig hur du distribuerar webbplatstemat med hjälp av pipeline. | Front-End Developer |

## What&#39;s Next {#what-is-next}

Nu är du redo att komma igång med din resa Adobe Quick Site Creation.

* Om du är AEM- eller Cloud Manager-administratör, eller om du har både avancerade utvecklings- och administratörsroller, eller om du bara vill förstå hela processen i AEM, börjar du i början av resan med [Förstå Cloud Manager](cloud-manager.md) enligt nedan.
* Om du bara ansvarar för frontendutvecklingen och kommer att interagera med AEM- och Cloud Manager-administratörer kan du hoppa direkt till [Hämta Git-databasåtkomstinformation](retrieve-access.md) för att få tillgång till AEM Git-databasen och börja anpassa.
* Om du redan är insatt i att AEM Sites och Cloud Manager arbetar tillsammans och vill börja direkt med konfigurationen, kan du [hoppa direkt till att skapa en webbplats från en mall](create-site.md).

## Ytterligare resurser {#additional-resources}

Här finns mer information om hur AEM kraftfulla funktioner fungerar tillsammans.

* [AEM as a Cloud Service tekniska dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - Om du redan har en god förståelse för AEM kan det vara bra att läsa de detaljerade tekniska dokumenten direkt.
* [Dokumentation för webbplatsadministration](/help/sites-cloud/administering/site-creation/create-site.md) - Mer information om funktionerna i verktyget Skapa snabbwebbplats finns i de tekniska dokumenten för att skapa webbplatser.
