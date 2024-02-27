---
title: Hantera sidor
description: Lär dig hur du hanterar webbplatsens sidor i AEM, inklusive flyttning, kopiering och borttagning.
source-git-commit: faac7c803a5145f4207154bfb3c9aa06274bbb86
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---


# Hantera sidor {#managing-pages}

Lär dig hur du hanterar webbplatsens sidor i AEM, inklusive flyttning, kopiering och borttagning.

>[!TIP]
>
>Innan du börjar hantera sidorna bör du känna till [hur sidorna är ordnade i AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

>[!TIP]
>
>Det finns flera [kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) som du kan använda från webbplatskonsolen som gör det enklare att ordna sidorna.

## Åtkomstbehörigheter {#access-privileges}

Ditt konto behöver rätt behörighet för att kunna hantera sidor som att skapa, kopiera, flytta, redigera och ta bort.

Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

## Öppna en sida för redigering {#opening-a-page-for-editing}

Efter [skapa en sida](/help/sites-cloud/authoring/sites-console/creating-pages.md) eller navigera till en befintlig sida med [den **Webbplatser** konsol,](/help/sites-cloud/authoring/sites-console/introduction.md) kan du öppna den för redigering.

1. Öppna [den **Webbplatser** konsol.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till sidan som du vill redigera.
1. Välj sida genom att använda något av följande:

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) och verktygsfältet

1. Tryck eller klicka på **Redigera** -ikon.

   ![Knappen Redigera](/help/sites-cloud/authoring/assets/edit.png)

1. Sidan öppnas och du kan redigera sidan efter behov. Beroende på hur den valda sidan skapades visas **Redigera** öppnas rätt redigerare.
   * [Page Editor](/help/sites-cloud/authoring/page-editor/introduction.md) - För sidor som skapats med AEM sidredigeraren
   * [Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md) - För sidor som skapats med den universella redigeraren

## Kopiera och klistra in en sida {#copying-and-pasting-a-page}

Du kan kopiera en sida och alla dess undersidor till en ny plats:

1. Öppna [den **Webbplatser** konsol.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till sidan som du vill kopiera.
1. Välj sida med hjälp av:

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) och verktygsfältet

1. Tryck eller klicka på **Kopiera** sidikon.

   ![Kopiera](/help/sites-cloud/authoring/assets/copy.png)

1. Navigera till den nya kopians plats.
1. Välj **Klistra in** som blev tillgänglig.

   ![Klistra in](/help/sites-cloud/authoring/assets/paste.png)

1. Dialogrutan Klistra in innehåller en sammanfattning av inklistringstransaktionen och möjlighet att:
   * **Nytt platsnamn:** Ändra den inklistrade sidans namn
   * **Klistra in utan underordnade:** Utelämna de underordnade sidorna för den markerade sidan när du klistrar in (som standard klistras underordnade sidor in)

   ![Dialogrutan Klistra in](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Välj **Klistra in** för att bekräfta inklistringstransaktionen och skapa nya sidor.

>[!NOTE]
>
>Om du kopierar sidan till en plats där det redan finns en sida med samma namn som originalet, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` finns redan, en ny sida med namnet `beach` blir `beach1`.

>[!NOTE]
>
>Om du startar inklistringsåtgärden i markeringsläget avslutas den automatiskt så fort sidan kopieras.

## Flytta eller byta namn på en sida {#moving-or-renaming-a-page}

Proceduren för att flytta eller byta namn på en sida är i princip densamma och båda åtgärderna hanteras av guiden Flytta sida. Med den här guiden kan du

* Byt namn på en sida utan att flytta den.
* Flytta sidan utan att byta namn på den.
* Flytta och byt namn samtidigt.

I AEM finns funktioner för att uppdatera interna länkar som refererar till sidan som byter namn/flyttas. Detta kan göras sida för sida för att ge full flexibilitet.

1. Öppna [den **Webbplatser** konsol.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till sidan som du vill flytta.
1. Välj sida med hjälp av:

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) och verktygsfältet

1. Tryck eller klicka på **Flytta** sidikon för att öppna guiden Flytta sida.

   ![Knappen Flytta](/help/sites-cloud/authoring/assets/move.png)

1. Från **Byt namn** steg i guiden som du kan antingen:

   * Ange namnet som du vill att sidan ska ha efter att den har flyttats och välj sedan **Nästa** för att fortsätta.
   * **Avbryt** om du vill avbryta processen.

   ![Flytta och byta namn på sida](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * Sidnamnet kan vara detsamma om du bara flyttar sidan.

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` finns redan, en ny sida med namnet `beach` blir `beach1`.

1. Från **Välj mål** steg i guiden som du kan antingen:

   * Använd [kolumnvy](/help/sites-cloud/authoring/basic-handling.md#column-view) för att navigera till sidans nya plats:

      * Markera målet genom att klicka på målets miniatyrbild.
      * Klicka **Nästa** för att fortsätta.

   * Använd **Bakåt** för att återgå till sidnamnsspecifikationen.

   >[!NOTE]
   >
   >Som standard är den överordnade sidan till sidan som du flyttar eller byter namn på markerad som mål.

   ![Välj mål för flyttning av sida](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` finns redan, `winter` blir `winter1`.

1. Om sidan är länkad till eller refererad, eller har publicerats, visas informationen i **Justera/publicera igen** steg.

   * Du kan ange vilka som ska justeras och/eller publiceras på nytt efter behov.

   >[!NOTE]
   >
   >Om sidan varken är länkad till eller refererad är det här steget inte tillgängligt.

   ![Publicera om sidan när du flyttar](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Tryck eller klicka **Flytta** för att definiera när flyttåtgärden ska utföras.

   * **Nu** kommer att utlösa ett [asynkront jobb](#asynchronous-actions) om du vill flytta sidan direkt.
   * **Senare** Med kan du schemalägga ett datum för flytten som ska bearbetas.

   ![Definiera när flytten ska ske](assets/managing-pages-move-page-now-later.png)

1. Tryck eller klicka **Fortsätt** för att slutföra sidflytten.

>[!NOTE]
>
>Om sidan redan har publicerats, kommer den att återpubliceras automatiskt när du flyttar den. Som standard publiceras den om när flytten är klar, men detta kan ändras genom att avmarkera **Publicera igen** fältet i **Justera/publicera igen** steg.

>[!NOTE]
>
>Om du byter namn på en sida gäller även [Konventioner för sidnamngivning](#page-naming-conventions) när du anger det nya sidnamnet.

>[!NOTE]
>
>En sida kan bara flyttas till en plats där mallen som sidan baseras på tillåts. Se [Malltillgänglighet](/help/implementing/developing/components/templates.md#template-availability) för mer information.

### Asynkrona åtgärder {#asynchronous-actions}

Åtgärder för att flytta sidor bearbetas alltid asynkront, vilket gör att användaren kan fortsätta att redigera i gränssnittet utan hinder.

Status för asynkrona jobb kan kontrolleras i [**Status för asynkrona jobb** kontrollpanel](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) på **Global navigering** > **verktyg** > **Operationer** > **Jobb**

>[!TIP]
>
>Mer information om asynkron jobbbearbetning och hur du konfigurerar gränsen för åtgärder för att flytta/byta namn på sidor finns i [Asynkrona jobb](/help/operations/asynchronous-jobs.md) -dokument i användarhandboken för Operations.

### Ta bort en sida {#deleting-a-page}

1. Öppna [den **Webbplatser** konsol.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till sidan som du vill ta bort.
1. Använd [markeringsläge](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) för att välja önskad sida och sedan använda **Ta bort** från verktygsfältet:

   ![Knappen Ta bort](/help/sites-cloud/authoring/assets/delete.png)

1. En dialogruta där du tillfrågas om bekräftelse.

   ![Dialogrutan Ta bort](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Vill du arkivera sidor före borttagning?** - Om det här alternativet är markerat skapas versioner av de sidor som markerats för borttagning vid borttagning.
      * [Versioner kan återställas vid ett senare datum](/help/sites-cloud/authoring/sites-console/page-versions.md).
      * Det går inte att återställa sidor som tagits bort utan tidigare versioner.
1. Tryck eller klicka **Avbryt** om du vill avbryta åtgärden eller **Ta bort** för att bekräfta åtgärden.
   * Om sidan inte har några referenser tas sidan bort.
   * Om sidan innehåller referenser visas en meddelanderuta om att **En eller flera sidor refereras.** Du kan välja **Tvinga borttagning** eller **Avbryt**.

>[!NOTE]
>
>Om en sida redan är publicerad kommer den automatiskt att avpubliceras innan den tas bort.

### Låsa en sida {#locking-a-page}

Du kan [låsa/låsa upp en sida](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page) från en konsol eller när du redigerar en enskild sida. Information om huruvida en sida är låst visas också på båda platserna.

![Knappen Lås](/help/sites-cloud/authoring/assets/lock.png)
![Knappen Lås upp](/help/sites-cloud/authoring/assets/unlock.png)

### Skapa en ny mapp {#creating-a-new-folder}

Du kan skapa mappar som hjälper dig att ordna dina filer och sidor.

1. Öppna [den **Webbplatser** konsol.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navigera till önskad plats.
1. Om du vill öppna alternativlistan väljer du **Skapa** från verktygsfältet
1. Välj **Mapp** för att öppna dialogrutan. Här anger du **Namn** och **Titel**:

   ![Skapa mapp](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Välj **Skapa** för att skapa mappen.

>[!NOTE]
>
>* Mappar kan även användas i [Konventioner för sidnamngivning](#page-naming-conventions) när du anger det nya mappnamnet.
>* Mappar kan bara skapas direkt under **Webbplatser** eller under andra mappar. De kan inte skapas under en sida.
>* Standardåtgärderna för att flytta, kopiera, klistra in, ta bort, publicera, avpublicera och visa/redigera egenskaper kan utföras på en mapp.
>* Det går inte att välja mappar i en live-kopia.
