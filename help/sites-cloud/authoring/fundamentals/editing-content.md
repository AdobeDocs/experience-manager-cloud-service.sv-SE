---
title: Redigera sidinnehåll
description: När sidan har skapats kan du redigera innehållet för att göra de uppdateringar du behöver
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2978'
ht-degree: 4%

---


# Redigera sidinnehåll{#editing-page-content}

När sidan har skapats (antingen ny eller som en del av en lansering eller en live-kopia) kan du redigera innehållet för att få de uppdateringar du behöver.

Innehåll läggs till med [komponenter](/help/sites-cloud/authoring/features/components-console.md) (anpassat till innehållstypen) som kan dras till sidan. Du kan sedan redigera dem på plats, flytta eller ta bort dem.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att kunna redigera sidor.
>
>Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>Om sidan och/eller mallen har konfigurerats korrekt kan du använda [responsiv layout](/help/sites-cloud/authoring/features/responsive-layout.md) vid redigering.

>[!TIP]
>
>När **Redigera** -läget är länkar i innehållet synliga, men **inte tillgänglig**. Använd [Förhandsgranskningsläge](#previewing-pages) om du vill navigera med hjälp av länkarna i ditt innehåll.

{{edge-delivery-authoring}}

## Verktygsfältet Sida {#page-toolbar}

Verktygsfältet för sidan ger tillgång till lämplig funktionalitet, beroende på sidkonfigurationen.

![Verktygsfältet Sida](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

Verktygsfältet har många alternativ. Beroende på ditt aktuella sammanhang och din konfiguration kanske vissa alternativ inte är tillgängliga.

* **Växla sidopanel**

  Då öppnas/stängs sidopanelen som innehåller [Resursläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), [Komponentbläddraren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)och [Innehållsträd](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![Växla sidopanel](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **Sidinformation**

  Ger åtkomst till [Sidinformation](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) meny med sidinformation och åtgärder som kan vidtas på sidan, inklusive visning och redigering av sidinformation, visning av sidegenskaper samt publicering/avpublicering av sidan.

  ![Sidinformation, knapp](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **Emulator**

  Växlar [emulatorverktygsfält](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate), som används för att emulera sidans utseende och känsla på en annan enhet. Detta aktiveras automatiskt i layoutläge.

  ![Emulatorknapp](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  Öppnar [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). Endast tillgängligt i förhandsgranskningsläget.

  ![Knappen Kontextnav](/help/sites-cloud/authoring/assets/context-hub.png)

* **Sidrubrik**

  Detta är enbart informativt.

  ![Sidrubrik](/help/sites-cloud/authoring/assets/page-title.png)

* **Lägesväljare**

  Visar aktuell [läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) och låter dig välja ett annat läge, t.ex. redigering, layout, tidsförvrängning eller målinriktning.

  ![Lägesväljare, knapp](/help/sites-cloud/authoring/assets/mode-selector.png)

* **Förhandsgranska**

  Aktiverar [förhandsgranskningsläge](#preview-mode). Då visas sidan som den kommer att se ut när den publiceras.

  ![Knappen Förhandsgranska](/help/sites-cloud/authoring/assets/preview.png)

* **Anteckna**

  Gör att du kan lägga till [anteckningar](/help/sites-cloud/authoring/fundamentals/annotations.md) till sidan när du granskar en sida. Efter den första anteckningen växlar ikonen till ett nummer som anger antalet anteckningar på sidan.

  ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotations.png)

### Statusmeddelande {#status-notification}

Om en sida är en del av en [arbetsflöde](/help/sites-cloud/authoring/workflows/overview.md) för flera arbetsflöden visas den här informationen i ett meddelandefält högst upp på skärmen när sidan redigeras.

![Meddelande om arbetsflöde](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>Statusfältet är bara synligt för användarkonton med lämplig behörighet.

I meddelandet visas arbetsflödet som körs mot sidan. Om användaren är involverad i det aktuella arbetsflödessteget kan du välja [påverka arbetsflödets status](/help/sites-cloud/authoring/workflows/participating.md) och det finns även mer information om arbetsflödet:

* **Complete** - Öppnar **Slutför arbetsuppgift** dialog
* **Delegera** - Öppnar **Slutför arbetsuppgift** dialog
* **Visa detaljer** - Öppnar **Information** arbetsflödets fönster

Att slutföra och delegera arbetsflödessteg via meddelandefältet fungerar som när [delta i arbetsflöden](/help/sites-cloud/authoring/workflows/participating.md) från meddelandeinkorgen.

Om sidan har flera arbetsflöden visas antalet arbetsflöden till höger om meddelandet tillsammans med pilknapparna så att du kan bläddra igenom arbetsflödena.

![Flera arbetsflödesmeddelanden](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## Komponentplatshållare {#component-placeholder}

Komponentplatshållaren är en indikator som visar var en komponent placeras när du släpper den - ovanför den komponent som du håller pekaren över.

* När du lägger till en ny komponent på sidan (drar från komponentwebbläsaren):

  ![Platshållare när en ny komponent läggs till på en sida](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* När en befintlig komponent flyttas:

  ![Platshållare när en befintlig komponent flyttas på en sida](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## Infoga en komponent {#inserting-a-component}

### Infoga en komponent från komponentwebbläsaren {#inserting-a-component-from-the-components-browser}

Du kan lägga till en ny komponent med [komponentwebbläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). The [platshållare för komponent](#component-placeholder) visar var komponenten är placerad:

1. Kontrollera att sidan finns i [**Redigera** läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. Öppna [komponentwebbläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. Dra den önskade komponenten till [obligatorisk position](#component-placeholder).
1. [Redigera](#edit-content) komponenten.

>[!NOTE]
>
>Komponentwebbläsaren fyller hela skärmen på en mobil enhet. När du börjar dra en komponent stängs webbläsaren och sidan visas igen så att du kan montera komponenten.

### Infoga en komponent från styckesystemet {#inserting-a-component-from-the-paragraph-system}

Du kan lägga till en ny komponent med **Dra komponenter hit** styckesystemets ruta:

1. Kontrollera att sidan finns i [**Redigera** läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. Det finns två sätt att markera och lägga till en ny komponent från styckesystemet:

   * Välj **Infoga komponent** (+) i verktygsfältet för en befintlig komponent eller **Dra komponenter hit** box.

     ![Infoga en komponent](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * Om du använder en stationär enhet kan du dubbelklicka på **Dra komponenter hit** box.

   * The **Infoga ny komponent** öppnas en dialogruta där du kan välja önskad komponent:

     ![Infoga ny komponent, dialogruta](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. Den markerade komponenten läggs till längst ned på sidan. [Redigera](#edit-content) komponenten efter behov.

### Infoga en komponent med Resursläsaren {#inserting-a-component-using-the-assets-browser}

Du kan också lägga till en ny komponent på sidan genom att dra en resurs från [resurshanterare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). Då skapas automatiskt en ny komponent av lämplig typ (och som innehåller resursen).

Det här beteendet kan konfigureras för din installation. Mer information finns i Konfigurera ett styckesystem så att en komponentinstans skapas när du drar en resurs. <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

Så här skapar du en komponent genom att dra en av resurstyperna ovan:

1. Kontrollera att sidan finns i [**Redigera** läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. Öppna [resursläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. Dra den önskade resursen till önskad position. The [platshållare för komponent](#component-placeholder) visar var komponenten är placerad.

   En komponent som passar för resurstypen skapas på den önskade platsen - den innehåller den valda resursen.

1. [Redigera](#edit-content) komponenten om det behövs.

>[!NOTE]
>
>På en mobil enhet fyller resursläsaren hela skärmen. När du börjar dra en resurs stängs webbläsaren och sidan visas igen så att du kan montera resursen.

Om du behöver göra en snabb ändring i en resurs när du bläddrar bland resurserna kan du starta [tillgångsredigerare](/help/assets/manage-digital-assets.md) direkt från webbläsaren genom att klicka på redigeringsikonen bredvid resursens namn.

![Knappen Resursredigering](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Komponentverktygsfältet {#component-toolbar}

När du väljer en komponent öppnas verktygsfältet. Detta ger åtkomst till olika åtgärder som kan utföras på komponenten.

De faktiska åtgärder som är tillgängliga för användaren visas som lämpliga och alla åtgärder kan inte beskrivas här.

![Komponentverktygsfältet](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **Redigera**

  [Beroende på komponenttypen](/help/sites-cloud/authoring/fundamentals/components.md)så kan du [redigera innehållet i komponenten](#edit-content). Ofta finns det ett verktygsfält.

  ![Knappen Redigera](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **Konfigurera**

  [Beroende på komponenttypen](/help/sites-cloud/authoring/fundamentals/components.md)kan du redigera och konfigurera komponentens egenskaper. Ofta öppnas en dialogruta.

  ![Knappen Konfigurera](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **Kopiera**

  Komponenten kopieras då till Urklipp. När inklistringsåtgärden är klar finns den ursprungliga komponenten kvar.

  ![Knappen Kopiera](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **Klipp ut**

  Komponenten kopieras då till Urklipp. Efter inklistringsåtgärden tas den ursprungliga komponenten bort.

  ![Klipp ut, knapp](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **Ta bort**

  Då tas komponenten bort från sidan med din bekräftelse.

  ![Knappen Ta bort](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **Infoga komponent**

  Dialogrutan öppnas [lägga till en ny komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![Infoga, knapp](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **Klistra in**

  Komponenten klistras in från Urklipp till sidan. Om originalet finns kvar beror på om du har använt kopian eller klippet.

   * Du kan klistra in på samma sida eller på en annan sida.
   * Det inklistrade objektet klistras in ovanför objektet där du väljer åtgärden Klistra in.
   * Åtgärden Klistra in visas bara om det finns innehåll i Urklipp.

  ![Knappen Klistra in](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste du uppdatera sidan för att se det inklistrade innehållet.

* **Grupp**

  På så sätt kan du markera flera komponenter samtidigt. Samma sak kan man göra på en stationär enhet med **Ctrl+klicka** eller **Kommando+klicka**.

  ![Gruppera, knapp](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **Överordnad**

  På så sätt kan du markera den överordnade komponenten för den markerade komponenten.

  ![Överordnad knapp](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **Layout**

  På så sätt kan du ändra [layout](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) för den markerade komponenten. Detta gäller bara den markerade komponenten och aktiverar inte [Layoutläge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) för hela sidan.

  ![Knappen Layout](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **Konvertera till en upplevelsefragmentvariation**

  Detta gör att du kan skapa en ny [upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) från den markerade komponenten eller lägg till den i ett befintligt upplevelsefragment.

  ![Knappen Konvertera till Experience Fragment](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## Redigera innehåll {#edit-content}

Det finns två sätt att lägga till och/eller redigera innehåll i komponenter:

* Öppna [komponentdialogruta för redigering](#component-edit-dialog).
* [Dra och släpp en resurs](#drag-and-drop-assets-into-component) från resursläsaren för att lägga till innehåll direkt.

### Komponentredigeringsdialogruta {#component-edit-dialog}

Du kan öppna en komponent och redigera innehållet med ikonen [Redigera (penna) i komponentverktygsfältet](#component-toolbar).

De exakta redigeringsalternativen beror på komponenten. För vissa komponenter [alla åtgärder är endast tillgängliga i helskärmsläge](#edit-content-full-screen-mode). Till exempel:

* Textkomponent

  ![Textkomponentens verktygsfält](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* Bildkomponent

  ![Verktygsfält för bildkomponenten](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >Redigering fungerar inte på en tom bildkomponent.
  >
  >Du måste dra eller överföra en bild till komponenten innan du kan börja redigera den.

* Bildkomponent - helskärm

  [Gå in i helskärmsläge](#edit-content-full-screen-mode) för bildkomponenten ger mer utrymme för att redigera bilden och visa extra redigeringsalternativ som **Starta karta** och **Återställ zoomning**. I helskärmsläget kan du dessutom välja förinställningar för beskärning.

  ![Bildkomponentens helskärmsläge](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* Komponenter som har konstruerats av mer än en grundläggande komponent ber dig först bekräfta vilken uppsättning redigeringsalternativ du vill ha:

### Dra och släpp resurser till komponent {#drag-and-drop-assets-into-component}

För specifika komponenttyper (t.ex. bilder) kan du dra och släppa resurser från resursläsaren direkt till komponenten för att uppdatera innehållet.

## Redigera innehåll i helskärmsläge {#edit-content-full-screen-mode}

För alla komponenter kan helskärmsläget nås med (och avslutas från):

![Knappen Helskärm](/help/sites-cloud/authoring/assets/editing-full-screen.png)

Till exempel **Text** komponent:

![Textkomponent i helskärmsläge](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>För vissa komponenter har helskärmsläget fler alternativ än den grundläggande redigeraren på plats.

## Flytta en komponent {#moving-a-component}

Så här flyttar du en styckekomponent:

1. Markera det stycke som ska flyttas genom att trycka och hålla ned eller klicka och hålla ned.
1. Dra stycket till den nya platsen. AEM anger var stycket kan placeras. Släpp den där du vill.

   ![Flytta en komponent](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. Stycket flyttas.

>[!TIP]
>
>Du kan också använda [Klipp ut och klistra in](#component-toolbar) för att flytta en komponent.

## Redigera komponentlayout {#edit-component-layout}

I stället för att växla från redigeringsläge till [layoutläge](/help/sites-cloud/authoring/features/responsive-layout.md) gång på gång för att justera en komponent, kan du välja åtgärden **Layout** för en komponent när du vill ändra dess layout och spara tid eftersom du slipper lämna redigeringsläget.

1. När **Redigera** platskonsolens läge. Om du väljer en komponent visas komponentens verktygsfält.

   ![Komponentverktygsfältet för en sidkomponent](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   Klicka eller tryck på **Layout** åtgärd för att justera komponentens layout.

   ![Knappen Layout i komponentverktygsfältet](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. När Layout-åtgärden är markerad:

   * Storlekshandtagen för komponentvisningen.
   * Emulatorverktygsfältet visas högst upp på skärmen.
   * Layoutåtgärder i stället för standardredigeringsåtgärder visas i komponentverktygsfältet.

   ![En komponent i layoutläge](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   Nu kan du ändra komponentens layout på samma sätt som i [layoutläge](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. När du har gjort nödvändiga layoutändringar klickar du på **Stäng** på komponentens åtgärdsmeny om du vill sluta ändra komponentens layout. Komponentens verktygsfält återgår till det normala redigeringsläget.

   ![Komponentverktygsfältet för en sidkomponent](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>Layoutåtgärden är begränsad i omfång till den markerade komponenten. Om du till exempel redigerar layouten för en komponent och sedan klickar på en annan komponent, visas standardverktygsfältet för redigering (inte verktygsfältet för layout) för den nyligen markerade komponenten och storleksändringshandtagen och emulatorns verktygsfält försvinner.
>
>Om du behöver redigera sidans övergripande layout, vilket påverkar flera komponenter, växlar du till [layoutläge](/help/sites-cloud/authoring/features/responsive-layout.md).

## Ärvda komponenter {#inherited-components}

Arv är den mekanism där innehåll automatiskt kan skickas från en komponent till en annan. Ärvda komponenter kan vara produkten av olika scenarier, bland annat:

* [Hantering av flera webbplatser](/help/sites-cloud/administering/msm/overview.md)
* [Startar](/help/sites-cloud/authoring/launches/overview.md) (baserat på live-kopia).

Du kan avbryta (och sedan återaktivera) arvet. Beroende på vilken komponent det är kan den här funktionen vara tillgänglig från komponentens verktygsfält, om komponenten finns på en sida som är en del av en live-kopia eller en livestart (baserad på en live-kopia).

![Ett komponentverktygsfält som visar arvsrelation](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

Till exempel:

* Avbryt arv

  ![Knappen Avbryt arv](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* Återaktivera arv (om arv redan har avbrutits)

  ![Återaktivera arv, knapp](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* Utrullningsåtgärden är även tillgänglig i ritningen eller i Live Copy-källan

  ![Knappen Över](/help/sites-cloud/authoring/assets/editing-rollout.png)

## Redigera sidmallen {#editing-the-page-template}

Du kan enkelt växla till [mallredigeraren](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) genom att välja **Redigera mall** på menyn [Sidinformation](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information).

Du kan enkelt se vilken mall sidan baseras på när du markerar sidan i [kolumnvyn](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) eller [listvyn](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view).

## Live Copy-status {#live-copy-status}

The [Sidläget Live Copy-status](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ger dig en snabb översikt över live-kopians status och vilka komponenter som ärvs/inte ärvs:

* Grön kant: Ärvd
* Rosa kantlinje: Arvet har avbrutits

Till exempel:

![Exempel på live-kopia som visas](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## Lägga till anteckningar {#adding-annotations}

[Anteckningar](/help/sites-cloud/authoring/fundamentals/annotations.md) kan granskare och andra författare ge feedback på ditt innehåll. De används ofta för granskning och validering.

## Förhandsgranska sidor {#previewing-pages}

Det finns två alternativ för att förhandsgranska en sida:

* [Förhandsgranskningsläge](#preview-mode) - en snabb förhandsgranskning på plats
* [Visa som publicerad](#view-as-published) - en fullständig förhandsgranskning som öppnar sidan på en ny flik

>[!TIP]
>
>* Länkarna i innehållet är synliga, men inte tillgängliga i redigeringsläget.
>* Använd något av förhandsvisningsalternativen om du vill navigera med hjälp av länkarna.
>* Använd [kortkommando](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` om du vill växla mellan förhandsvisning och det senast markerade läget.

>[!NOTE]
>
>WCM-lägets cookie är inställd för båda förhandsvisningsalternativen.

### Förhandsgranskningsläge {#preview-mode}

När du redigerar innehåll kan du förhandsgranska sidan med förhandsgranskningen [läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). Det här läget:

* Döljer olika redigeringsmekanismer så att du snabbt kan se hur sidan kommer att se ut vid publiceringen.
* Gör att du kan använda länkar för att navigera.
* Gör **not** uppdatera sidinnehållet.

Vid redigering är förhandsgranskningsläget tillgängligt med hjälp av ikonen längst upp till höger i sidredigeraren:

![Knappen Förhandsgranska](/help/sites-cloud/authoring/assets/preview.png)

### Visa som publicerad {#view-as-published}

The **Visa som publicerad** är tillgängligt från [Sidinformation](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) -menyn. Sidan öppnas på en ny flik, innehållet uppdateras och sidan visas exakt som den kommer att visas i publiceringsmiljön.

## Låsa en sida {#locking-a-page}

AEM kan du låsa en sida så att ingen annan kan redigera innehållet. Det här låset är användbart när du gör flera ändringar på en viss sida, eller när du behöver frysa en sida en kort stund.

En sida kan låsas från:

* **Webbplatser** konsol

   1. Markera sidan med [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. Välj låsikonen.

      ![Knappen Lås](/help/sites-cloud/authoring/assets/lock.png)

* **Page Editor**

   1. Välj **Sidinformation** -ikonen för att öppna menyn.
   1. Välj **Lås sida** alternativ.

När konsolvyn är låst uppdateras informationen och när du redigerar en låssymbol visas den i verktygsfältet.

![Exempel på en låst sida](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>Du kan låsa en sida när du personifierar en användare. En sida som är låst på det här sättet kan bara låsas upp (av kunder) med den användare som personifierats.
>
>Sidorna kan inte låsas upp genom att den användare som låste sidan personifieras.
>
>Om användaren som låste sidan inte är tillgänglig för att låsa upp sidan, kontaktar du kundsupport för att utvärdera alternativen för att ta bort låset.

## Låsa upp en sida {#unlocking-a-page}

Låsa upp en sida påminner mycket om [låsa sidan](#locking-a-page). När sidan är låst ersätts låsalternativen av upplåsningsåtgärder.

På menyn Sidinformation visas **Lås upp** som ett alternativ och låsikonen på Sites-konsolen ersätts av en **Lås upp**-ikon.

![Knappen Lås upp](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>Du kan låsa en sida när du personifierar en användare. En sida som är låst på det här sättet kan bara låsas upp (av kunder) med den användare som personifierats.
>
>Sidorna kan inte låsas upp genom att den användare som låste sidan personifieras.
>
>Om användaren som låste sidan inte är tillgänglig för att låsa upp sidan, kontaktar du kundsupport för att utvärdera alternativen för att ta bort låset.

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages cannot be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## Ångra och göra om sidredigeringar {#undoing-and-redoing-page-edits}

Med följande ikoner kan du ångra eller göra om en åtgärd. Dessa visas i verktygsfältet när det är lämpligt:

![Knapparna Ångra och Gör om](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* The [kortkommando](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` kan även ångra sidredigeringsåtgärder.
>* Kortkommandot `Ctrl-Y` är även tillgängligt för att göra om sidredigeringsåtgärder.

>[!NOTE]
>
>Se [Ångra och göra om sidredigeringar - The Theory](#undoing-and-redoing-page-edits-the-theory) om du vill ha fullständig information om vad som är möjligt när du ångrar och gör om sidredigeringar.

## Ångra och göra om sidredigeringar - The Theory {#undoing-and-redoing-page-edits-the-theory}

AEM lagrar en historik över åtgärder som du utför och den sekvens i vilken du utförde dem, så att du kan ångra flera åtgärder i den ordning som du utförde dem och göra om dem för att återanvända en eller flera av åtgärderna om det behövs.

Om ett element på innehållssidan är markerat (till exempel en textkomponent) gäller kommandot ångra och gör om det markerade objektet.

Funktionen för kommandona ångra och gör om liknar den i andra program. Använd kommandona för att återställa webbsidans senaste status när du fattar beslut om innehållet. Om du till exempel flyttar ett textstycke till en annan plats på sidan kan du använda kommandot Ångra för att flytta tillbaka stycket. Om du sedan bestämmer dig för att den föregående positionen var bättre använder du kommandot gör om för att ångra.

Du kan till exempel:

* Gör om åtgärder så länge du inte har gjort någon sidredigering sedan du använde Ångra.
* Ångra högst 20 redigeringsåtgärder (standardinställning).
* Använd även [Kortkommandon](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) för att ångra och göra om.

Du kan använda Ångra och Gör om för följande typer av sidändringar:

* Lägga till, redigera, ta bort och flytta stycken
* Redigera styckeinnehåll direkt
* Kopiera, klippa ut och klistra in objekt på en sida

>[!NOTE]
>
>* Särskilda behörigheter krävs för att ångra och göra om ändringar i filer och bilder.
>* Historiken för ändringar av filer och bilder varar i minst tio timmar. Efter den här gången kan du dock inte ångra ändringarna. Administratören kan ändra standardtiden på tio timmar.
>* Systemadministratören kan konfigurera olika aspekter av funktionerna Ångra/Gör om enligt kraven för din instans.
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
