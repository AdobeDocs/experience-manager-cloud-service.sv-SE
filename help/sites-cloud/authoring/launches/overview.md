---
title: Launches
description: Med lanseringar kan du effektivt utveckla innehåll för en framtida release. De gör att du kan göra ändringar redo för framtida publicering, samtidigt som du behåller dina aktuella sidor
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 6%

---


# Launches {#launches}

Med lanseringar kan du effektivt utveckla innehåll för en framtida release.

En startsida skapas så att du kan göra ändringar redo för framtida publicering (samtidigt som du behåller dina aktuella sidor). När du har redigerat och uppdaterat startsidorna befordrar du dem tillbaka till källan och aktiverar sedan källsidorna (översta nivån). Befordra duplicerar startinnehållet tillbaka till källsidorna och kan göras antingen manuellt eller automatiskt (beroende på fält som anges när du skapar och redigerar startsidan).

Till exempel kommer säsongsproduktsidorna i din onlinebutik att uppdateras kvartalsvis så att de aktuella produkterna passar den aktuella säsongen. Om du vill förbereda dig för nästa kvartalsvisa uppdatering kan du skapa en startsida med lämpliga webbsidor. Under hela kvartalet ackumuleras följande ändringar i startversionen:

* Ändringar av källsidorna som inträffar som ett resultat av normala underhållsåtgärder. Dessa ändringar dupliceras automatiskt på startsidorna.
* Redigeringar som utförs direkt på startsidorna inför nästa kvartal.

När nästa kvartal anländer befordrar du startsidorna så att du kan publicera källsidorna (med det uppdaterade innehållet). Du kan antingen befordra alla sidor eller bara de som du har ändrat.

Startar kan också vara:

* Skapat för flera rotgrenar. Du kan skapa en start för hela webbplatsen (och göra ändringarna där), men det kan vara opraktiskt eftersom hela webbplatsen behöver kopieras. När det gäller hundratals eller till och med tusentals sidor påverkas systemkraven och prestandan av både kopieringsåtgärden och senare jämförelserna som krävs för kampanjuppgifterna.
* Kapslad (en programstart inom en programstart) för att ge dig möjlighet att skapa en programstart från en befintlig programstart så att författare kan utnyttja redan gjorda ändringar i stället för att behöva göra samma ändringar flera gånger för varje programstart.

I det här avsnittet beskrivs hur du skapar, redigerar och befordrar (och vid behov [tar](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)bort) startsidor i Sites-konsolen eller [i Launches-konsolen](#the-launches-console):

* [Skapa Launches](/help/sites-cloud/authoring/launches/creating.md)
* [Redigera Launches](/help/sites-cloud/authoring/launches/editing.md)
* [Marknadsföra Launches](/help/sites-cloud/authoring/launches/promoting.md)

## Startar - ordningen för händelser {#launches-the-order-of-events}

Med den här funktionen kan du effektivt utveckla innehåll för en framtida release av en eller flera aktiverade webbsidor.

Med Launes kan du:

* Skapa en kopia av källsidorna:
   * Kopian är startsida.
   * Källsidorna på den översta nivån kallas **Produktion**.
      * Källsidorna kan tas från flera (separata) grenar.
   ![Operationsordning för starter](/help/sites-cloud/authoring/assets/launches-order.png)

* Redigera startkonfigurationen:
   * Lägg till eller ta bort sidor och/eller grenar till/från starten.
   * Redigera startegenskaper, som flaggorna **Titel**, **Startdatum** och **Produktionsklar**.
* Du kan befordra och publicera innehållet antingen manuellt eller automatiskt:
   * Manuellt:
      * Befordra startinnehållet tillbaka till **Target** (källsidor) när det är klart att publiceras.
      * Publicera innehållet från källsidorna (efter att ha befordrat dem).
      * Befordra antingen alla sidor eller endast ändrade sidor.
   * Automatiskt - det innebär följande:
      * The **Launch**(**Live**) **date** field: this can be set when creating or editing a launch.
      * The **Production Ready** flag: detta kan bara anges när du redigerar en programstart.
      * If the **Production Ready** flag is set, the launch will be automatically promoted to the production pages on the specified **Launch**(**Live**) **date**. Efter kampanjen publiceras produktionssidorna automatiskt.\
         Om inget datum har angetts har flaggan ingen effekt.
* Uppdatera käll- och startsidor parallellt:
   * Ändringar av källsidorna implementeras automatiskt i startkopian (om den är konfigurerad som arv). dvs. som en live-kopia).
   * Du kan göra ändringar i startversionen utan att störa dessa automatiska uppdateringar eller källsidorna.
   ![Åtgärder parallellt](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Skapa en kapslad programstart](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - en programstart i en programstart:
   * Källan är en befintlig start.
   * Du kan [befordra en kapslad start](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) till vilket mål som helst; detta kan vara en överordnad start eller källsidorna på den översta nivån (Produktion).
   ![En kapslad start](/help/sites-cloud/authoring/assets/launches-nested.png)

   >[!CAUTION]
   >
   >Om du tar bort en programstart tas själva programstarten och alla underordnade kapslade programstarter bort.

>[!NOTE]
>
>Att skapa och redigera starter kräver åtkomsträttigheter till `/content/launches` - precis som med standardgruppen `content-authors`.
>
>Kontakta systemadministratören om du får problem.

### Startkonsolen {#the-launches-console}

På startkonsolen får du en översikt över dina starter och kan vidta åtgärder för dem som visas. Konsolen kan nås av:

* The **Tools** Console: **Verktyg**, **Webbplatser**, **Startar**.

* Eller direkt med `https://<host>:<port>/libs/launches/content/launches.html`

## Startar i referenser (platskonsolen) {#launches-in-references-sites-console}

1. Gå till startkällan i **Sites** Console.
1. Öppna **referenslisten** och välj källsidan.
1. Välj **Startar**. De befintliga starterna visas:

   ![Referenser till starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references.png)

1. Tryck/klicka på lämplig start så visas listan med möjliga åtgärder:

   ![Åtgärder som ska vidtas vid starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references-actions.png)
