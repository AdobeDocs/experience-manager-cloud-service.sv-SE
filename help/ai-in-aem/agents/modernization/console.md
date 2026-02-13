---
title: Experience Modernization Console
description: Referenshandbok för gränssnittet och funktionerna i Experience Modernization Console
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 43d8c124-fc87-4cec-a91d-ab12255ae321
source-git-commit: 76c0f41acb5c2e4e0f0a292f8205b0b9de5cda81
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---


# Experience Modernization Console {#console-reference}

Referenshandbok för gränssnittet och funktionerna i Experience Modernization Console

>[!NOTE]
>
>Om du är intresserad av att använda Experience Modernization Console kan du begära åtkomst för att få en smidig introduktionsupplevelse.

## Ökning {#overview}

Experience Modernization Console är en värdbaserad, AI-assisterad utvecklingsmiljö för Edge Delivery Services som visas som ett webbgränssnitt på [`aemcoder.adobe.io`.](https://aemcoder.adobe.io) När du har anslutit till deras GitHub-projekt kan du omedelbart börja fråga efter ändringar i naturligt språk utan ytterligare konfiguration eller lokal miljökonfiguration.

>[!TIP]
>
>Om du vill komma igång direkt med konsolen går du till dokumentet [Komma igång med Experience Modernization Agent.](/help/ai-in-aem/agents/modernization/getting-started.md)

## Funktioner {#capabilities}

Konsolens kärnfunktioner:

* Interaktiv chattpanel med agenten och dess färdigheter
* Live AEM Preview för direkt visuell feedback på ändringar
* Content file browser and markdown viewer
* Innehållssynkronisering med [Dokumentredigering](https://da.live)
* Kodwebbläsaren och diff-läsaren för att granska ändringar som gjorts
* GitHub-integrering med möjlighet att skapa pull-begäranden från ändringar

Utvecklarna har full kontroll över vilka fartyg som levereras. Alla ändringar som görs via konsolen kräver granskning och godkännande före driftsättning, vilket säkerställer en enhetlig styrning, varumärkestrohet och säkerhet.

## Navigering {#navigation}

När du har loggat in på konsolen på [`aemcoder.adobe.io` ](https://aemcoder.adobe.io) kommer du till hemskärmen på konsolen.

![Startskärmen för konsolen](assets/console-home.png)

### Menyrad {#menu-bar}

Den övre menyraden innehåller:

* En **Öppna-meny** till vänster om du vill expandera och komprimera detaljerna i den vänstra panelen
* Knappen **Konto** till höger om du vill växla till mörkt läge och logga ut från konsolen

### Vänster sidospalt {#sidebar}

Den vänstra sidofältet ger snabb åtkomst till viktiga vyer av konsolen.

* **[Hemvy](#home-view)** (intern ikon) - Startpunkt för konsolen
* **[Innehållsvy](#content-view)** (filikon) - Innehåll som du har importerat
* **[Kodvy](#code-view)** (`</>` ikon) - kod för den webbplats du arbetar med
* **[Inställningsvy](#settings-view)** (kugghjulsikon) - Konsolens inställningar

## Hemvy {#home-view}

Vyn **Hem** är startpunkten för konsolen.

* Överst finns en [promptpanel](#prompt-panel) som gör begäranden från konsolen.
* Här nedan visas uppmaningar om att starta projektet.

### Frågepanelen {#prompt-panel}

Frågepanelen innehåller kontroller för interaktion med AI.

* **Planerings-/körningslägen** (glödlampor och trollstavsikoner): Växla mellan planerings- och körningslägen
   * **Planeringsläge**: AI analyserar begäranden och sammanställer en strategi utan att göra ändringar, vilket är användbart för att förstå strategi innan implementering.
   * **Körningsläge**: AI utför planen och utför faktiska filändringar.
* **Bifoga filer** (pappersklippsikon): Överför och bifoga filer till uppmaningen om ytterligare kontext (t.ex. referensdesign, skärmbilder, specifikationer)
* **Inställningar** (kugghjulsikon): Välj att hoppa över bekräftelsefrågor från AI
* **Rensa chatt**: Detta återställer konversationen och rensar kontextfönstret i AI. Använd det här alternativet när du startar en ny uppgift som inte hör till den tidigare konversationen.

## Innehållsvy {#content-view}

I **innehållsvyn** finns verktyg för att bläddra bland och förhandsgranska innehåll. Vyn delas som standard upp i tre paneler, från vänster till höger:

* Fråga panelen för interaktion med konsolen och projektet
* En översikt över dina innehållsfiler i filläsaren (växla om du vill visa den här panelen med ikonen för att markera)
* Panelen Förhandsgranska för att visualisera innehåll som valts i filläsaren

![Innehållsvy](assets/content-imported.png)

Det finns tre lägen i förhandsvisningspanelen:

* **Förhandsgranska** (dokument med förstoringsglaset) om du vill visa det återgivna HTML-innehållet
* **HTML-vy** (dokumentikon) om du vill visa den underliggande innehållsstrukturen för dokumentredigering
* **Designläge** (penselikon) om du vill välja element på sidan för kontext för prompten

Du kan alltid klicka på ikonen **Uppdatera förhandsvisning** för att uppdatera förhandsvisningspanelen.

Knappen **Överför innehåll** öppnar ett modalt fönster där du kan överföra filer till AEM Document Authoring.

* Fälten **Organisation** och **Databas** är förifyllda om projektet har en `fstab.yaml`-fil
* Filmarkering ger redigerbara målsökvägar
* Överföring till JCR (för Universal Editor) stöds inte

![Överför innehåll](assets/upload-content.png)

## Kodvyn {#code-view}

I **kodvyn** finns verktyg för att bläddra i kod och hantera kodändringar. Vyn är uppdelad i tre paneler, från vänster till höger:

* Fråga panelen för interaktion med konsolen och projektet
* I filläsaren finns en översikt över dina kodfiler eller ändringar som skillnader
* Panelen Förhandsgranska för att visa en kodfil eller diff-markering i filläsaren

![Kodvyn](assets/code-view.png)

Det finns två olika lägen i förhandsvisningspanelen:

* **Workspace-filer** om du vill bläddra bland kodfilerna på den aktuella arbetsytan
* **Git-ändringar** för att visa skillnaderna mellan filändringar som har skapats i ditt arbete i projektet
   * Klicka på ikonen `+` för att mellanlagra den ändrade filen
   * Klicka på pilikonen för att ta bort den ändrade filen

Ikonen **Information** visar ditt GitHub-konto och -projekt som du är ansluten till för tillfället.

Menyn **GitHub-åtgärder** (överst till höger) innehåller databasåtgärder.

* **Anslut/återanslut**: Initierar GitHub OAuth
* **Växla databas**: Ersätter arbetsytan med en annan databas. Alla arbeten som inte har implementerats går förlorade.
* **Växla gren**: Växlar grenar inom samma databas
* **Synkronisera**: Tar bort de senaste ändringarna från fjärrkällan
* **Tryck**: Öppnar en modal för att överföra arbetsyteändringar till GitHub
* **Utloggning**: Kopplar från GitHub

När du gör ändringar måste du först ha mellanlagrade ändringar som ska ingå i push-åtgärden. När du trycker kan du välja att skapa en ny PR eller direkt till den aktuella grenen

![Push-ändringar](assets/push-changes.png)

## Inställningsvy {#settings-view}

I inställningsvyn kan du hantera konsolens grundläggande inställningar.

![Inställningsvyn](assets/settings-view.png)

* Med **Autentiseringsuppgifter** kan du ange en personlig åtkomsttoken för Figma så att konsolen kan komma åt designblock för ditt projekt.
* **Återställ arbetsyta** återställer konsolen till startläget och alla ändringar som inte har skickats eller inte har överförts går förlorade.
