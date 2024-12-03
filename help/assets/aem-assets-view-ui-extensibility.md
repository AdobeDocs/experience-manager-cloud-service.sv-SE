---
title: Utbyggbarhet för användargränssnittet i AEM Assets View
description: Läs mer om UI Extensibility-funktionen i AEM Assets View. Med användargränssnittet i AEM Assets View kan du lägga till anpassade användargränssnittskomponenter som uppfyller specifika affärsbehov.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: bbb183470e12c0fc81c821fc2e0c1e7d77c33707
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Utbyggbarhet för användargränssnittet i AEM Assets View{#AEM-Assets-View-UI-Extensibility}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

AEM Assets View har UI Extensibility-funktioner. Med den här funktionen kan användare lägga till anpassade gränssnittskomponenter i användargränssnittet i Assets View för att uppfylla specifika affärsbehov som inte uppfylls av AEM Assets View-vyns färdiga funktioner. Den här utökningsfunktionen förbättrar flexibiliteten i AEM Assets View, som gör det möjligt att anpassa gränssnittet efter specifika arbetsflöden och krav.
Du kan lägga till dina tillägg på resursnivå, mapp- och samlingsnivå. Det tillagda tillägget visas i en dedikerad panel på sidan Resurs, Samling eller Mappinformation.

>[!IMPORTANT]
>
> * AEM Assets View UI Extensibility är tillgängligt med [Assets Ultimate](/help/assets/assets-ultimate-overview.md).
> * [Skapa och skicka ett kundsupportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) från Adobe  om du vill få åtkomst till Assets-vyns UI-utökningsbarhet.
> * Du kan ge feedback genom att utöka alternativen för Detaljerad feedback och klicka på Rapportera ett problem.

## <a id="1"></a> Så här kommer du åt Assets View

Öppna vyn Assets på följande sätt:
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## Var visas gränssnittstillägg i användargränssnittet för Assets-vyn? {#ui-extensibility-panel-assets-view}

I Assets View (Visa) går du till sidan Details (Detaljer) för en resurs, mapp eller samling. Den här informationssidan har en dedikerad panel som visar det tillagda gränssnittstillägget.
![min arbetsyta](/help/assets/assets/my-workspace-assets-view3.png)


## Krav för att lägga till utökningskomponenten

* [Åtkomst till Assets View](#1).
* Åtkomst till appverktyget [Adobe](https://developer.adobe.com/app-builder/docs/overview/).
* Har rätt till rollen som systemadministratör för utvecklare inom organisationen. Mer information finns i [this](https://developer.adobe.com/uix/docs/guides/get-access/).
* Adobe IO-kommandoradsverktyget (AIO CLI) måste vara installerat på dina lokala datorer. Det här verktyget är nödvändigt för att skapa och distribuera tilläggsprojekt. Mer information finns i [this](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up).
* Bra insikt i JavaScript, Node.js och React-tekniken.

## Lägga till UI-utökningskomponent i användargränssnittet för Assets-vyn{#Adding-UI-Extensibility-Component-on-Assets-View}

1. Se [Komma igång](https://developer.adobe.com/uix/docs/getting-started/) för viktig information om gränssnittstillägg och Adobe App Builder-ramverket. Läs om hur UI Extensibility möjliggör integrering av anpassad logik och gränssnitt i Adobe Experience Cloud-tjänster och förstå arkitekturen och arbetsflödet för implementering av UI-tillägg.
1. Se [Stödlinjer](https://developer.adobe.com/uix/docs/guides/) för allmän information om UI-utökningsmöjligheter, inklusive lokal miljöinställning, lokal förhandsgranskning, publicering och hantering.
1. Se [Vanliga koncept i Skapa tillägg](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) för att förstå grunderna som krävs för att utveckla ett gränssnittstillägg för AEM Assets-vyn.
1. Lägg till anpassade sidopaneler i Assets View-gränssnittet. Värdprogrammet (Assets View) hanterar dessa paneler för att hantera gränssnittsinteraktioner som växlingar och djuplänkning. Tillägg använder tilläggspunkten `aem/assets/details/1` för att integrera anpassade paneler som anger egenskaper, till exempel panel-ID, rubrik och innehålls-URL. Utvecklare registrerar anpassade paneler med metoden `getPanels()` och skapar vägar för att visa anpassat innehåll. Detaljerad implementering, inklusive API-referenser och kodexempel, finns i [Detaljvy](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Konfigurera din lokala miljö och upplev processen att utveckla gränssnittstillägg i Assets-vyn först genom att skapa ditt första gränssnittstillägg. Mer information finns i [Steg-för-steg-AEM Assets View Extension Development](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/).
1. Konfigurera appen med AIO CLI för att generera den grundläggande tilläggsstrukturen och den nödvändiga koden. Mer information finns i [Kodgenerering för AEM Assets-vyn](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/).
1. Testa tilläggen lokalt för att kontrollera att de fungerar som förväntat före distributionen. Kör tillägget i en helt isolerad miljö eller med partiell isolering och anslut tillägget till produktionen i AEM Assets View för testning. Mer information finns i [Felsökning - AEM Assets View Extensibility](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/).
