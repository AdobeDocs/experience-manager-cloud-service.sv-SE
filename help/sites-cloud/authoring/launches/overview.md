---
title: Launches
description: Med lanseringar kan du effektivt utveckla innehåll för en framtida release. De gör att du kan göra ändringar redo för framtida publicering, samtidigt som du behåller dina aktuella sidor
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# Launches {#launches}

Med lanseringar kan du effektivt utveckla innehåll för en framtida release.

En startsida skapas så att du kan göra ändringar redo för framtida publicering (samtidigt som du behåller dina aktuella sidor). När du har redigerat och uppdaterat startsidorna befordrar du dem tillbaka till källan och aktiverar sedan källsidorna (översta nivån). Befordra duplicerar startinnehållet tillbaka till källsidorna och kan göras antingen manuellt eller automatiskt (beroende på fält som anges när du skapar och redigerar startsidan).

Till exempel kommer säsongsproduktsidorna i din onlinebutik att uppdateras kvartalsvis så att de aktuella produkterna passar den aktuella säsongen. Om du vill förbereda dig för nästa kvartalsvisa uppdatering kan du skapa en startsida med lämpliga webbsidor. Under hela kvartalet ackumuleras följande ändringar i startversionen:

* Ändringar av källsidorna som inträffar som ett resultat av normala underhållsåtgärder. Dessa ändringar dupliceras automatiskt på startsidorna.
* Redigeringar som utförs direkt på startsidorna inför nästa kvartal.

Du kan också:

* Navigera i startgrenen och lägg till eller ta bort sidor efter behov.
* Förhandsgranska hur publicerat innehåll ser ut på ett specifikt datum/tid i framtiden.

När nästa kvartal anländer befordrar du startsidorna så att du kan publicera källsidorna (med det uppdaterade innehållet). Du kan antingen befordra alla sidor eller bara de som du har ändrat.

Startar kan också vara:

* Skapat för flera rotgrenar. Du kan skapa en start för hela webbplatsen (och göra ändringarna där), men det kan vara opraktiskt eftersom hela webbplatsen måste kopieras. När det gäller hundratals eller till och med tusentals sidor påverkas systemkraven och prestandan av både kopieringsåtgärden och senare jämförelserna som krävs för kampanjuppgifterna.
* Kapslad (en programstart inom en programstart) för att ge dig möjlighet att skapa en programstart från en befintlig programstart så att författare kan utnyttja redan gjorda ändringar i stället för att behöva göra samma ändringar flera gånger för varje programstart.

I det här avsnittet beskrivs hur du skapar, redigerar och befordrar (och om det behövs) [delete](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) starta sidor från Sites-konsolen eller [startkonsolen](#the-launches-console):

* [Skapa Launches](/help/sites-cloud/authoring/launches/creating.md)
* [Redigera Launches](/help/sites-cloud/authoring/launches/editing.md)
* [Hantera sidor i Launches](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Använda Timewarp för att förhandsgranska innehåll baserat på startprogram](/help/sites-cloud/authoring/launches/preview.md)
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
      * Befordra ert startmaterial tillbaka till **Mål** (källsidor) när den är klar att publiceras.
      * Publicera innehållet från källsidorna (efter att ha befordrat dem).
      * Befordra antingen alla sidor eller endast ändrade sidor.
   * Automatiskt - det innebär följande:
      * The **Starta**(**Live**) **datum** fält: detta kan anges när du skapar eller redigerar en start.
      * The **Produktionsklar** flagga: detta kan bara anges när du redigerar en start.
      * Om **Produktionsklar** -flaggan är inställd, lanseringen befordras automatiskt till produktionssidorna på den angivna **Starta**(**Live**) **datum**. Efter kampanjen publiceras produktionssidorna automatiskt.\
        Om inget datum har angetts har flaggan ingen effekt.
* Uppdatera käll- och startsidor parallellt:
   * Ändringar av källsidorna implementeras automatiskt i startkopian (om den har konfigurerats som arv, d.v.s. som en live-kopia).
   * Du kan göra ändringar i startversionen utan att störa dessa automatiska uppdateringar eller källsidorna.

  ![Parallella åtgärder](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Skapa en kapslad start](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - en programstart inom en programstart:
   * Källan är en befintlig start.
   * Du kan [befordra en kapslad lansering](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) till vilket mål som helst. Det kan vara en överordnad start eller källsidorna på den översta nivån (Produktion).

  ![En kapslad start](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >Om du tar bort en programstart tas själva programstarten och alla underordnade kapslade programstarter bort.

>[!NOTE]
>
>Att skapa och redigera starter kräver åtkomsträttigheter till `/content/launches` - som med standardgruppen `content-authors`.
>
>Kontakta systemadministratören om du får problem.

## Startar i referenser (platskonsolen) {#launches-in-references-sites-console}

1. I **Webbplatser** navigera till startkällan (startfilerna).
1. Öppna **Referenser** och välj källsidan.
1. Välj **Startar**, listas de befintliga starterna tillsammans med tillgång till **Startar konsolen**:

   ![Referenser till starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references.png)

1. Välj lämplig start. Listan över möjliga åtgärder visas:

   ![Åtgärder som ska vidtas vid starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## Startkonsolen {#the-launches-console}

På startkonsolen får du en översikt över dina starter och kan vidta åtgärder för dem som visas. Konsolen kan nås av:

* The **verktyg** Konsol: **verktyg**, **Webbplatser**, **Startar**.

* **Startar konsolen** längst ned i **Startar** i **Referenser** när du navigerar i källinnehåll i webbplatskonsolen.

  ![Startar konsolen i referenser till starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references.png)

* The **Startar** längst upp till höger när du navigerar till startinnehåll i webbplatskonsolen:

  ![Startar alternativ i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)

* Eller direkt, till exempel med:
  `https://<host>:<port>/libs/launches/content/launches.html`
