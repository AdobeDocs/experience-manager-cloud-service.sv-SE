---
title: Redigera sidinnehåll med AEM sidredigeraren
description: Den AEM sidredigeraren är ett kraftfullt verktyg för att skapa innehåll.
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 2%

---


# Redigera sidinnehåll med AEM sidredigeraren {#edit-content}

Den AEM sidredigeraren är ett kraftfullt verktyg för att skapa en sidas innehåll. Lär dig hur du använder den för att dra och släppa innehåll och redigera innehåll på plats.

## Ökning {#overview}

Det finns tre grundläggande åtgärder som du kan utföra i sidredigeraren för att redigera ditt innehåll:

1. [Lägga till nya komponenter](#adding-components) genom att dra och släppa dem på sidan.
1. [Lägga till nya resurser](#adding-asset) genom att dra och släppa dem på sidan.
1. [Redigera komponenter på plats](#edit-in-place) som redan finns på sidan.

Den AEM sidredigeraren har ett intuitivt användargränssnitt för att utföra dessa uppgifter samt ger åtkomst till mer avancerade funktioner.

Dessutom kan du ordna det befintliga innehållet på sidan genom att låta dig

* [Flytta komponenter](#moving-components)
* [Redigera komponentlayout](#editing-component-layout)
* [Redigera komponentarv](#inherited-components)

## Lägga till komponenter {#adding-components}

Du kan dra och släppa nya komponenter på sidan genom att välja dem i [komponentwebbläsare på sidopanelen](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) och släppa dem i en komponentplatshållare.

### Komponentplatshållare {#component-placeholder}

Komponentplatshållaren är en indikator som visar var en komponent placeras när du släpper den. Den har två utseenden.

* När du lägger till en ny komponent på sidan (drar från komponentwebbläsaren) visas den som en grå ruta med information om komponenten som du monterar.

  ![Platshållare när en ny komponent läggs till på en sida](assets/edit-content-component-placeholder.png)

* När [flytta en befintlig komponent,](#movging-components) den visas som en blå kvadrat.

  ![Platshållare när en befintlig komponent flyttas på en sida](assets/edit-content-move-placeholder.png)

I båda fallen visas det markerade målet som en blå kontur under komponenten som du drar. Målet om komponenten ska placeras när du släpper den.

### Lägga till en komponent från komponentwebbläsaren {#adding-a-component-from-the-components-browser}

Du kan lägga till en ny komponent med [komponentwebbläsare](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser). The [platshållare för komponent](#component-placeholder) visar var du placerar komponenten.

1. Kontrollera att sidredigeraren är i [**Redigera** läge.](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. Öppna [komponentwebbläsare.](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
1. Dra den önskade komponenten till [obligatorisk position](#component-placeholder) och släppa.
1. [Redigera](#edit-content) den nyplacerade komponenten.

>[!NOTE]
>
>Komponentwebbläsaren fyller hela skärmen på en mobil enhet. När du börjar dra en komponent stängs webbläsaren och sidan visas igen så att du kan montera komponenten.

### Lägga till en komponent från styckesystemet {#adding-a-component-from-the-paragraph-system}

Du kan lägga till en ny komponent med **Dra komponenter hit** platshållare för styckesystemet:

1. Kontrollera att sidredigeraren är i [**Redigera** läge.](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. Det finns två sätt att markera och lägga till en ny komponent från styckesystemet:

   * Välj **Infoga komponent** (+) i verktygsfältet för en befintlig komponent eller **Dra komponenter hit** box.

     ![Infoga en komponent](assets/edit-content-drag-components-here.png)

   * Om du använder en stationär enhet kan du dubbelklicka på **Dra komponenter hit** box.

1. The **Infoga ny komponent** öppnas så att du kan välja önskad komponent. Tryck eller klicka på komponenten som du vill lägga till.

   * Använd sökfiltren för att hitta komponenten.
   * Använd informationsikonen bredvid komponentnamnen för att ta reda på mer om komponenten.

   ![Infoga ny komponent, dialogruta](assets/edit-content-insert-component.png)

1. Den markerade komponenten läggs till i det valda målet. [Redigera](#edit-content) komponenten efter behov.

## Lägga till en resurs {#adding-asset}

Du kan också lägga till en ny komponent på sidan genom att dra en resurs från [resurshanteraren.](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) Då skapas automatiskt en komponent av lämplig typ (och som innehåller resursen).

Det här beteendet kan konfigureras för din installation. Se dokumentet [Referenshandbok för komponenter](/help/implementing/developing/components/reference.md#component-placeholders) för mer information.

Så här skapar du en komponent genom att dra en av resurstyperna ovan:

1. Kontrollera att sidan finns i [**Redigera** läge.](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. Öppna [resursläsare](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser).
1. Dra den önskade resursen till önskad position. The [platshållare för komponent](#component-placeholder) visar var komponenten är placerad och ett mål visas där den kommer att infogas.
1. Släpp resursen på målet. En lämplig komponent för resurstypen skapas på den önskade plats som innehåller den valda resursen.
1. [Redigera](#edit-content) komponenten, om det behövs.

>[!NOTE]
>
>På en mobil enhet fyller resursläsaren hela skärmen. När du börjar dra en resurs stängs webbläsaren och sidan visas igen så att du kan montera resursen.

Om du behöver göra en snabb ändring i en resurs när du bläddrar bland resurserna kan du starta [tillgångsredigerare](/help/assets/manage-digital-assets.md) direkt från webbläsaren genom att klicka på redigeringsikonen bredvid resursens namn.

## Redigera komponenter på plats {#edit-in-place}

Om du väljer en komponent öppnas komponentens verktygsfält. Detta ger åtkomst till olika åtgärder som kan utföras på komponenten.

![Komponentverktygsfältet](assets/edit-content-component-toolbar.png)

De åtgärder som är tillgängliga i komponentverktygsfältet är lämpliga för den valda komponenten. Beroende på vilken komponent du har valt kan du se fler eller färre bilder. De beskrivs eventuellt inte här.

* **Redigera** gör att du kan ändra innehållet i komponenten, ofta på plats. Dess beteende beror på komponenten.

  ![Knappen Redigera](assets/edit-content-edit.png)

* **Konfigurera** gör att du kan ändra vissa parametrar för komponenten som inte är direkt relaterade till dess innehåll, vanligtvis i en dialogruta. Dess beteende beror på komponenten.

  ![Knappen Konfigurera](assets/edit-content-configure.png)

* **Kopiera** kopierar komponenten till Urklipp för att klistra in någon annanstans. Den ursprungliga komponenten ändras inte.

  ![Knappen Kopiera](assets/edit-content-copy.png)

* **Klipp ut** kopierar komponenten till Urklipp. Den ursprungliga komponenten tas bort.

  ![Klipp ut, knapp](assets/edit-content-cut.png)

* **Ta bort** tar bort komponenten från sidan med din bekräftelse.

  ![Knappen Ta bort](assets/edit-content-delete.png)

* **Infoga komponent** öppnar dialogrutan för att [lägga till en ny komponent.](#adding-a-component-from-the-paragraph-system)

  ![Infoga, knapp](assets/edit-content-insert-component.png)

* **Klistra in** klistrar in komponenten från Urklipp på sidan. Om originalet finns kvar beror på om du använt det **Kopiera** eller **Klipp ut**.

   * Du kan klistra in på samma sida eller på en annan sida.
   * Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste du uppdatera sidan för att se det inklistrade innehållet.
   * Det inklistrade objektet klistras in ovanför objektet där du väljer åtgärden Klistra in.
   * Åtgärden Klistra in visas bara om det finns innehåll i Urklipp.

  ![Knappen Klistra in](assets/edit-content-paste.png)

* **Grupp** Med kan du markera flera komponenter samtidigt. Samma sak kan man göra på en stationär enhet med **Ctrl+klicka** eller **Kommando+klicka**.

  ![Gruppera, knapp](assets/edit-content-group.png)

* **Överordnad** markerar den markerade komponentens överordnade komponent.

  ![Överordnad knapp](assets/edit-content-parent.png)

* **Layout** låter dig ändra [layout](#editing-component-layout) för den markerade komponenten.

   * Detta gäller bara den markerade komponenten och aktiverar inte [Layoutläge](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) för hela sidan.

  ![Knappen Layout](assets/edit-content-layout.png)

* **Konvertera till en upplevelsefragmentvariation** kan du skapa en [upplevelsefragment](/help/sites-cloud/authoring/fragments/content-fragments.md) från den markerade komponenten eller lägg till den i ett befintligt upplevelsefragment.

  ![Knappen Konvertera till Experience Fragment](assets/edit-content-convert.png)

### Komponentredigeringsdialogruta {#component-edit-dialog}

Vissa komponenter erbjuder fler redigeringsalternativ än vad som finns på plats. Du kan öppna en komponents redigeringsdialogruta i [Ikonen Redigera (penna) i komponentens verktygsfält](#component-toolbar) för att få tillgång till ytterligare konfigurationsalternativ.

De exakta redigeringsalternativen beror på komponenten. För vissa komponenter [vissa åtgärder är bara tillgängliga i helskärmsläge](#edit-content-full-screen-mode). Till exempel:

* Textkomponent

  ![Textkomponentens verktygsfält](assets/edit-content-text-component.png)

* Bildkomponent

  ![Verktygsfält för bildkomponenten](assets/edit-content-image-component.png)

### Redigera komponenter i helskärmsläge {#edit-content-full-screen-mode}

Många komponenter har ett helskärmsläge för redigering som du kan komma åt med den här knappen.

![Knappen Helskärm](/help/sites-cloud/authoring/assets/editing-full-screen.png)

Med helskärmsredigering kan du visa fler redigeringsalternativ än med redigeraren på plats, t.ex. för bildkomponenten.

![Bildkomponent i helskärmsläge](assets/edit-content-image-component-full-screen.png)

Använd **Minimera** för helskärmsläge.

![Knappen Minimera](assets/edit-content-minimize.png)

## Flytta komponenter {#moving-components}

Flytta en komponent:

1. Markera den komponent som ska flyttas genom att trycka och hålla ned eller klicka och hålla ned.
1. Dra komponenten till den nya platsen.

   * Sidredigeraren anger komponentens position med en [platshållare](#component-placeholder) och var stycket kan tas bort med ett mål.

   ![Flytta en komponent](assets/edit-content-move-placeholder.png)

1. Släpp den på önskad plats.

>[!TIP]
>
>Du kan också använda [Klipp ut och klistra in](#component-toolbar) för att flytta en komponent.

## Redigera komponentlayout {#editing-component-layout}

I stället för att växla från redigeringsläge till [layoutläge](/help/sites-cloud/authoring/page-editor/responsive-layout.md) gång på gång för att justera en komponent, kan du välja åtgärden **Layout** för en komponent när du vill ändra dess layout och spara tid eftersom du slipper lämna redigeringsläget.

1. När **Redigera** platskonsolens läge. Välj en komponent för att visa komponentens verktygsfält.

1. Välj **Layout** åtgärd för att justera komponentens layout.

   ![Knappen Layout i komponentverktygsfältet](assets/edit-content-layout.png)

1. När Layout-åtgärden är markerad kan du ändra komponentens layout på samma sätt som i [layoutläge.](/help/sites-cloud/authoring/page-editor/responsive-layout.md#defining-layouts-layout-mode)

   * Storlekshandtagen för komponentvisningen.
   * Emulatorverktygsfältet visas högst upp på skärmen.
   * Layoutåtgärder i stället för standardredigeringsåtgärder visas i komponentverktygsfältet.

   ![En komponent i layoutläge](assets/edit-content-layout-mode.png)

1. När du har gjort nödvändiga layoutändringar trycker du eller klickar på **Stäng** på komponentens åtgärdsmeny om du vill sluta ändra komponentens layout och komponentens verktygsfält återgår till det normala redigeringsläget.

   ![Komponentverktygsfältet för en sidkomponent](assets/edit-content-layout-close.png)

>[!TIP]
>
>Layoutåtgärden är begränsad i omfång till den markerade komponenten. Om du till exempel redigerar layouten för en komponent och sedan klickar på en annan komponent, visas standardverktygsfältet för redigering (inte verktygsfältet för layout) för den nyligen markerade komponenten och storleksändringshandtagen och emulatorns verktygsfält försvinner.
>
>Om du behöver redigera sidans övergripande layout, vilket påverkar flera komponenter, växlar du till [layoutläge](/help/sites-cloud/authoring/page-editor/responsive-layout.md).

## Redigera komponentarv {#inherited-components}

Arv är den mekanism där innehåll kan länkas så att om du ändrar det ena ändras det andra automatiskt. Ärvda komponenter kan vara produkten av olika scenarier, bland annat:

* [Hantering av flera webbplatser](/help/sites-cloud/administering/msm/overview.md)
* [Launches](/help/sites-cloud/authoring/launches/overview.md)

Du kan avbryta och återaktivera arvet. Beroende på vilken komponent det är, är dessa alternativ tillgängliga från komponentens verktygsfält, om komponenten är en del av en live-kopia eller startar.

* **Avbryt arv**

  ![Knappen Avbryt arv](assets/edit-content-cancel-inheritance.png)

* **Återaktivera arv** om arvet redan har annullerats

  ![Återaktivera arv, knapp](assets/edit-content-re-enable-inheritance.png)

* **Utrullning** finns även i planen eller i Live Copy-källan

  ![Knappen Över](assets/edit-content-rollout.png)
