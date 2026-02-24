---
title: Grundläggande hantering
description: Bekanta dig med navigeringen i AEM och dess grundläggande användning
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# Grundläggande hantering {#basic-handling}

Det här dokumentet är avsett att ge en översikt över grundläggande hantering när du använder AEM redigeringsmiljö.

>[!TIP]
>
>Kortkommandon finns i hela AEM. Särskilt när [använder webbplatskonsolen](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) och [sidredigeraren](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md).

## Ett pekaktiverat användargränssnitt {#a-touch-enabled-ui}

AEM användargränssnitt är aktiverat för pekskärmar. Med ett pekaktiverat gränssnitt kan du använda touchfunktioner för att interagera med programmet med gester som att trycka, trycka och hålla ned och svepa. Eftersom användargränssnittet i AEM är pekaktiverat kan du använda pekgester på enheter med pekskärm, till exempel mobiltelefoner och surfplattor. Det finns dock även musåtgärder på en traditionell stationär enhet, vilket ger dig flexibilitet när det gäller hur du väljer att skapa ditt innehåll.

## Steg 1 {#first-steps}

Omedelbart efter inloggningen kommer du till [navigeringspanelen](#navigation-panel). Om du väljer något av alternativen öppnas respektive konsol.

![Navigeringspanelen](assets/basic-handling-navigation.png)

För att få en god förståelse för den grundläggande användningen av AEM är det här dokumentet baserat på konsolen **Platser**. Välj på **Webbplatser** för att komma igång.

## Produktnavigering {#product-navigation}

När en användare först kommer åt en konsol startas en produktnavigeringssjälvstudie. Ta en minut att gå igenom och få en bra översikt över AEM grundläggande hantering.

![Navigeringsgenomgång](assets/basic-handling-tutorial.png)

Välj **Nästa** om du vill gå vidare till nästa sida i översikten. Välj **Stäng** eller välj utanför översiktsdialogrutan för att stänga.

Översikten startas om nästa gång du öppnar en konsol, såvida du inte antingen visar alla bilder eller markerar alternativet **Visa inte detta igen**.

## Global navigering {#global-navigation}

Du kan navigera mellan konsolerna med den globala navigeringspanelen. Detta aktiveras som en listruta i helskärmsläge när du väljer länken **Adobe Experience Manager** längst upp till vänster på skärmen.

Du kan stänga den globala navigeringspanelen genom att klicka eller trycka på **Stäng** för att gå tillbaka till föregående plats.

![Navigeringspanelens övre fält](assets/basic-handling-navigation-options.png)

Global navigering har två paneler, som representeras av ikoner i skärmens vänstra marginal:

* **[Navigering](#navigation-panel)** - Representeras av en kompass och standardpanelen när du loggar in på AEM
* **[Verktyg](#tools-panel)** - motsvaras av en hammare

De alternativ som är tillgängliga på dessa paneler beskrivs nedan.

### Navigeringspanel {#navigation-panel}

Panelen **Navigering**:

![Navigeringspanelen](assets/basic-handling-navigation.png)

Titeln på webbläsarfliken uppdateras för att återspegla din position när du navigerar genom konsolerna och innehållet.

Följande konsoler finns i Navigation:

| Konsol | Syfte |
|---|---|
| Projekt | Med projektkonsolen får du direktåtkomst till dina projekt. [Projekt är virtuella instrumentpaneler](/help/sites-cloud/authoring/projects/overview.md) som kan användas för att skapa ett team. Sedan kan ni ge teamet tillgång till resurser, arbetsflöden och uppgifter och på så sätt låta andra arbeta mot ett gemensamt mål. |
| Sites | [Med platskonsolen](/help/sites-cloud/authoring/sites-console/introduction.md) kan du skapa, visa och hantera webbplatser som körs på din AEM-instans. Med den här konsolen kan du skapa, redigera, kopiera, flytta och ta bort sidor, starta arbetsflöden och publicera sidor. |
| Upplevelsefragment | En [Experience Fragment](/help/sites-cloud/authoring/fragments/content-fragments.md) är en fristående upplevelse som kan återanvändas i olika kanaler och ha variationer, vilket sparar problem med att kopiera och klistra in upplevelser eller delar av upplevelser upprepade gånger. |
| Assets | Med Assets-konsolen kan du importera och hantera [digitala resurser som bilder, videoklipp, dokument och ljudfiler](/help/assets/overview.md). Dessa resurser kan sedan användas av alla webbplatser som körs på samma AEM-instans. Du kan också skapa och hantera [innehållsfragment](/help/assets/content-fragments/content-fragments.md) från Assets-konsolen. |
| Personalisering | Den här konsolen innehåller ett ramverk med verktyg för [att skapa riktat innehåll och presentera personaliserade upplevelser](/help/sites-cloud/authoring/personalization/overview.md). |
| Innehållsfragment | [Med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) kan du utforma, skapa, strukturera och publicera sidoberoende innehåll. De gör att du kan ta fram strukturerat innehåll som är klart för användning på flera platser/i flera kanaler, och som är idealiskt för både sidutveckling och headless-leverans. |
| Generera variationer | [Generate Variations](/help/generative-ai/generate-variations.md) använder generativ artificiell intelligens (AI) för att skapa innehållsvariationer baserat på uppmaningar. Dessa uppmaningar tillhandahålls antingen av Adobe eller skapas, och hanteras av användare. |

## Panelen Verktyg {#tools-panel}

Panelen **Verktyg** har en sidopanel som innehåller ett urval kategorier, som grupperar liknande konsoler. **Verktygskonsolerna** ger åtkomst till flera specialiserade verktyg och konsoler som hjälper dig att administrera dina webbplatser, digitala resurser och andra aspekter av innehållsdatabasen.

![Verktygspanelen](assets/basic-handling-tools.png)

## Sidhuvudet {#the-header}

Rubriken visas alltid längst upp på skärmen. De flesta alternativen i huvudet är desamma oavsett var du befinner dig i systemet, men vissa är sammanhangsspecifika.

![Navigeringsrubrik](/help/sites-cloud/authoring/assets/basic-handling-navigation-bar.png)

* [Global navigering](#global-navigation) - Välj länken **Adobe Experience Manager** för att navigera mellan konsoler.

  ![Global navigering](/help/sites-cloud/authoring/assets/basic-handling-global-navigation.png)

* Feedback

  ![Feedback-knapp](/help/sites-cloud/authoring/assets/basic-handling-feedback.png)

* Din IMS-organisation - välj att ändra om det behövs.

* [Lösningar](https://www.adobe.com/experience-cloud.html) - Välj det här om du vill få tillgång till dina andra Adobe-lösningar.

  ![Knappen Lösningar](/help/sites-cloud/authoring/assets/basic-handling-solutions.png)

* [Sök](/help/sites-cloud/authoring/search.md) - Du kan även använda [kortkommandot](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `/` (snedstreck) för att starta sökning från en konsol.

  ![Ikon för sökning](/help/sites-cloud/authoring/assets/basic-handling-search-icon.png)

* [Hjälp](#accessing-help)

  ![Hjälp-knapp](/help/sites-cloud/authoring/assets/basic-handling-help-icon.png)

* [Meddelanden](/help/sites-cloud/authoring/inbox.md) -   Den här ikonen är märkt med antalet för närvarande tilldelade ofullständiga meddelanden.

  ![Knappen Meddelanden](/help/sites-cloud/authoring/assets/basic-handling-notifications.png)

* [Användaregenskaper](/help/sites-cloud/authoring/account-environment.md) - Välj det här om du vill ändra dina användarinställningar.

  ![Knappen Användaregenskaper](/help/sites-cloud/authoring/assets/basic-handling-user-properties.png)

## Få hjälp {#accessing-help}

Det finns ett antal hjälpresurser och några sätt att komma åt dem.

* **Verktygsfält** - Beroende på var du befinner dig öppnar ikonen **Hjälp** lämpliga resurser:

  ![Hjälpikon](assets/basic-handling-help.png)

* **Konsol** - Första gången du navigerar i systemet, [en serie bilder innehåller AEM-navigering](#product-navigation).

  ![Självstudiekurs](assets/basic-handling-console-tutorial.png)

* **Sidredigeraren** - Första gången du redigerar en sida visas sidredigeraren i en serie bilder.

  ![Självstudiekurs för redigerare](assets/basic-handling-editor-tutorial.png)

   * Navigera i den här översikten på samma sätt som du gör med [produktnavigeringsöversikten](#product-navigation) när du först öppnar en konsol.
   * På menyn [**Sidinformation** kan du när som helst välja **Hjälp**](#accessing-help) för att visa detta igen.

* **Verktygskonsol** - Från **Verktyg**-konsolen kan du även komma åt de externa **resurserna**:

   * **Dokumentation** - Visa dokumentationen för Web Experience Management
   * **Resurser för utvecklare** - Resurser och nedladdningar för utvecklare

>[!TIP]
>
>Du kan när som helst få tillgång till en översikt över kortkommandon med snabbtangenten `?` (frågetecken) i en konsol.
>
>En översikt över alla kortkommandon finns i följande dokumentation:
>
>* [Kortkommandon för sidredigering](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
>* [Kortkommandon för konsoler](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)
