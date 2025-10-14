---
title: Hantera sidor
description: Lär dig hur du hanterar sidorna på din webbplats i AEM, inklusive flytt, kopiering och borttagning.
exl-id: 355b60c5-a82e-4bbb-98ea-bfcc0126b7fd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 45805d4baa8b93df2225b44152fee1457b421150
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Hantera sidor {#managing-pages}

Lär dig hur du hanterar sidorna på din webbplats i AEM, inklusive flytt, kopiering och borttagning.

>[!TIP]
>
>Innan du börjar hantera sidorna bör du bekanta dig med [hur sidorna är ordnade i AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md).

>[!TIP]
>
>Det finns flera [kortkommandon](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) som du kan använda från webbplatskonsolen för att ordna dina sidor mer effektivt.

## Åtkomstbehörigheter {#access-privileges}

Ditt konto behöver rätt behörighet för att kunna hantera sidor som att skapa, kopiera, flytta, redigera och ta bort.

Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

## Öppna en sida för redigering {#opening-a-page-for-editing}

När du har [skapat en sida](/help/sites-cloud/authoring/sites-console/creating-pages.md) eller navigerat till en befintlig sida med [konsolen **Platser**](/help/sites-cloud/authoring/sites-console/introduction.md) kan du öppna den för redigering.

1. Öppna [konsolen **Platser**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Navigera till sidan som du vill redigera.
1. Välj sida genom att använda något av följande:

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) och verktygsfältet

1. Tryck eller klicka på ikonen **Redigera** .

   ![Knappen Redigera](/help/sites-cloud/authoring/assets/edit.png)

1. Sidan öppnas och du kan redigera sidan efter behov. Beroende på hur den valda sidan skapades kommer åtgärden **Redigera** att öppna rätt redigerare.
   * [Sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md) - För sidor som skapats med AEM sidredigeraren
   * [Universell redigerare](/help/sites-cloud/authoring/universal-editor/authoring.md) - för sidor som skapats med den universella redigeraren

## Kopiera och klistra in en sida {#copying-and-pasting-a-page}

Du kan kopiera en sida och alla dess undersidor till en ny plats:

1. Öppna [konsolen **Platser**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Navigera till sidan som du vill kopiera.
1. Välj sida med hjälp av:

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) och verktygsfältet

1. Tryck eller klicka på sidikonen **Kopiera** .

   ![Kopiera](/help/sites-cloud/authoring/assets/copy.png)

1. Navigera till den nya kopians plats.
1. Välj ikonen **Klistra in** som blev tillgänglig.

   ![Klistra in](/help/sites-cloud/authoring/assets/paste.png)

1. Dialogrutan Klistra in innehåller en sammanfattning av inklistringstransaktionen och möjlighet att:
   * **Nytt platsnamn:** Ändra den inklistrade sidans namn
   * **Klistra in utan underordnade:** Utelämna de underordnade sidorna på den markerade sidan när du klistrar in (som standard klistras underordnade sidor in)

   ![Dialogrutan Klistra in](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Välj knappen **Klistra in** för att bekräfta inklistringstransaktionen och skapa nya sidor.

>[!NOTE]
>
>Om du kopierar sidan till en plats där det redan finns en sida med samma namn som originalet, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` till exempel redan finns blir en ny sida med namnet `beach` `beach1`.

>[!NOTE]
>
>Om du startar inklistringsåtgärden i markeringsläget avslutas den automatiskt så fort sidan kopieras.

## Flytta eller byta namn på en sida {#moving-or-renaming-a-page}

Proceduren för att flytta eller byta namn på en sida är i princip densamma och båda åtgärderna hanteras av guiden Flytta sida. Med den här guiden kan du

* Byt namn på en sida utan att flytta den.
* Flytta sidan utan att byta namn på den.
* Flytta och byt namn samtidigt.

I AEM finns funktioner för att uppdatera interna länkar som refererar till sidan som byter namn/flyttas. Detta kan göras sida för sida för att ge full flexibilitet.

1. Öppna [konsolen **Platser**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Navigera till sidan som du vill flytta.
1. Välj sida med hjälp av:

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) och verktygsfältet

1. Tryck eller klicka på sidikonen **Flytta** för att öppna guiden Flytta sida.

   ![Flytta-knapp](/help/sites-cloud/authoring/assets/move.png)

1. I steget **Byt namn** i guiden får du **information** om sidan, inklusive skapandedatum, sökväg och antal direkta referenser. Här kan du antingen:

   * Ange det namn du vill att sidan ska ha efter att den har flyttats och välj sedan **Nästa** för att fortsätta.
   * **Avbryt** om du vill avbryta processen.

   ![Flytta och byta namn på sidan](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * Sidnamnet kan vara detsamma om du bara flyttar sidan.

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` till exempel redan finns blir en ny sida med namnet `beach` `beach1`.

1. I steget **Välj mål** i guiden kan du antingen:

   * Använd [kolumnvyn](/help/sites-cloud/authoring/basic-handling.md#column-view) för att navigera till sidans nya plats:

      * Markera målet genom att klicka på målets miniatyrbild.
      * Klicka på **Nästa** för att fortsätta.

   * Använd **Tillbaka** för att återgå till sidnamnsspecifikationen.

   >[!NOTE]
   >
   >Som standard är den överordnade sidan till sidan som du flyttar eller byter namn på markerad som mål.

   ![Välj mål för sidflyttning](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` till exempel redan finns blir `winter` `winter1`.

1. Om sidan är länkad till eller refererad, eller har publicerats, visas informationen i steget **Justera/Publicera igen**.

   * Du kan ange vilka som ska justeras och/eller publiceras på nytt efter behov.

   >[!NOTE]
   >
   >* Om sidan varken är länkad till eller refererad är det här steget inte tillgängligt.
   >* I det här steget visas både direkta och indirekta referenser. Detta kan skilja sig från mängden som rapporteras i steget **Byt namn** i guiden samt referenserna som rapporteras av referenslinjen, där båda endast rapporterar direkta referenser av prestandaskäl.

   ![Publicera om sida vid flytt](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Tryck eller klicka på **Flytta** för att definiera när flyttåtgärden ska utföras.

   * **Nu** utlöser ett [asynkront jobb](#asynchronous-actions) för att flytta sidan omedelbart.
   * **Senare** låter dig schemalägga ett datum för flytten som ska bearbetas.

   ![Definierar när &#x200B;](assets/managing-pages-move-page-now-later.png) ska flyttas

1. Tryck eller klicka på **Fortsätt** för att slutföra sidflytten.

>[!NOTE]
>
>Om sidan redan har publicerats, kommer den att återpubliceras automatiskt när du flyttar den. Som standard publiceras den om när flytten är klar, men detta kan ändras genom att du avmarkerar fältet **Publicera igen** i steget **Justera/Publicera igen**.

>[!NOTE]
>
>Om du byter namn på en sida gäller även [Sidnamngivningskonventioner](#page-naming-conventions) när du anger det nya sidnamnet.

>[!NOTE]
>
>En sida kan bara flyttas till en plats där mallen som sidan baseras på tillåts. Mer information finns i [Malltillgänglighet](/help/implementing/developing/components/templates.md#template-availability).

### Asynkrona åtgärder {#asynchronous-actions}

Åtgärder för att flytta sidor bearbetas alltid asynkront, vilket gör att användaren kan fortsätta att redigera i gränssnittet utan hinder.

Status för asynkrona jobb kan kontrolleras på kontrollpanelen [**Async Jobs Status**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) på **Global Navigation** > **Tools** > **Operations** > **Jobs**

>[!TIP]
>
>Mer information om asynkron jobbbearbetning och hur du konfigurerar gränsen för åtgärder för att flytta/byta namn på sidor finns i dokumentet [Asynkrona jobb](/help/operations/asynchronous-jobs.md) i användarhandboken för åtgärder.

### Ta bort en sida {#deleting-a-page}

1. Öppna [konsolen **Platser**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Navigera till sidan som du vill ta bort.
1. Använd [markeringsläget](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) för att markera önskad sida och använd sedan **Ta bort** i verktygsfältet:

   ![Ta bort-knapp](/help/sites-cloud/authoring/assets/delete.png)

1. En dialogruta där du tillfrågas om bekräftelse.

   ![Ta bort dialogruta](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Vill du arkivera sidor före borttagning?** - Om det här alternativet är markerat skapas versioner av de sidor som har markerats för borttagning vid borttagning.
      * [Versioner kan återställas vid ett senare datum](/help/sites-cloud/authoring/sites-console/page-versions.md).
      * Det går inte att återställa sidor som tagits bort utan tidigare versioner.
1. Tryck eller klicka på **Avbryt** för att avbryta åtgärden eller på **Ta bort** för att bekräfta åtgärden.
   * Om sidan inte har några referenser tas sidan bort.
   * Om sidan har referenser visas en meddelanderuta om att det finns referenser till **en eller flera sidor.** Du kan välja **Tvinga borttagning** eller **Avbryt**.

>[!NOTE]
>
>Om en sida redan är publicerad kommer den automatiskt att avpubliceras innan den tas bort.

### Låsa en sida {#locking-a-page}

Du kan [låsa/låsa upp en sida](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page) från en konsol eller när du redigerar en enskild sida. Information om huruvida en sida är låst visas också på båda platserna.

![Lås-knapp](/help/sites-cloud/authoring/assets/lock.png)
![&#x200B; Knappen Lås upp &#x200B;](/help/sites-cloud/authoring/assets/unlock.png)

### Skapa en ny mapp {#creating-a-new-folder}

Du kan skapa mappar som hjälper dig att ordna dina filer och sidor.

1. Öppna [konsolen **Platser**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Navigera till önskad plats.
1. Välj **Skapa** i verktygsfältet för att öppna alternativlistan
1. Välj **Mapp** för att öppna dialogrutan. Här kan du ange **Namn** och **Titel**:

   ![Skapa mapp](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Välj **Skapa** för att skapa mappen.

>[!NOTE]
>
>* Mappar omfattas också av [Sidnamngivningskonventioner](#page-naming-conventions) när du anger det nya mappnamnet.
>* Mappar kan bara skapas direkt under **Platser** eller under andra mappar. De kan inte skapas under en sida.
>* Standardåtgärderna för att flytta, kopiera, klistra in, ta bort, publicera, avpublicera och visa/redigera egenskaper kan utföras på en mapp.
>* Det går inte att välja mappar i en live-kopia.
