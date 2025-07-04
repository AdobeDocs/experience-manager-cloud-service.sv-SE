---
title: Startar för sidor
description: Lär dig hur du använder starter för sidor i Adobe Experience Manager as a Cloud Service. Med Launches kan du effektivt utveckla innehåll för en framtida release, samtidigt som du behåller de aktuella sidorna.
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 3859393b94680ac1c786bfe31950e6073650167f
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 3%

---

# Startar för sidor {#launches-for-pages}

I Adobe Experience Manager (AEM) as a Cloud Service kan du med Launches effektivt utveckla material för framtida releaser.

En *Launch* skapas så att du kan göra ändringar inför framtida publicering, samtidigt som du behåller det aktuella innehållet. För AEM-sidor innebär detta att du redigerar två versioner samtidigt: sidor som är publicerade och en version av dessa sidor som ska publiceras i framtiden. När tiden är inne kan du ersätta originalsidorna och publicera de nya versionerna.

<!--
>[!NOTE]
>
>Launches are also available for Content Fragments. The basic concepts are the same, but there are differences in how to manage them in AEM. 
>
>For full details see [Launches for Content Fragments](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).
-->

Du skapar en *Launch* och när du har redigerat och uppdaterat dina *Launch* -sidor *höjer du* dem tillbaka till *Source*. Du kan sedan aktivera dessa *Source*-sidor (översta nivån). Befordra duplicerar startinnehållet tillbaka till källsidorna och kan göras antingen manuellt eller automatiskt (beroende på fält som anges när du skapar och redigerar startsidan).

Till exempel kommer säsongsproduktsidorna i din onlinebutik att uppdateras kvartalsvis så att de aktuella produkterna passar den aktuella säsongen. Om du vill förbereda dig för nästa kvartalsvisa uppdatering kan du skapa en startsida med lämpliga webbsidor. Under hela kvartalet ackumuleras följande ändringar i startversionen:

* Ändringar av källsidorna som inträffar som ett resultat av normala underhållsåtgärder. Dessa ändringar dupliceras automatiskt på startsidorna.
* Redigeringar som utförs direkt på startsidorna inför nästa kvartal.

Du kan också:

* Navigera i startgrenen och lägg till eller ta bort sidor efter behov.
* Förhandsgranska hur publicerat innehåll ser ut på ett visst datum i framtiden.

När nästa kvartal anländer befordrar du startsidorna så att du kan publicera källsidorna (med det uppdaterade innehållet). Du kan antingen befordra alla sidor eller bara de som du har ändrat.

Startar kan också vara:

* Skapat för flera rotgrenar. Du kan skapa en start för hela webbplatsen (och göra ändringarna där), men det kan vara opraktiskt eftersom hela webbplatsen måste kopieras. När det gäller hundratals eller till och med tusentals sidor påverkas systemkraven och prestandan av både kopieringsåtgärden och senare jämförelserna som krävs för kampanjuppgifterna.
* Kapslad (en programstart inom en programstart) för att ge dig möjlighet att skapa en programstart från en befintlig programstart så att författare kan utnyttja redan gjorda ändringar i stället för att behöva göra samma ändringar flera gånger för varje programstart.

I det här avsnittet beskrivs hur du skapar, redigerar och befordrar (och vid behov [delete](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) startsidor från Sites-konsolen eller [startkonsolen](#the-launches-console):

* [Skapa startprogram](/help/sites-cloud/authoring/launches/creating.md)
* [Redigeringsövningar](/help/sites-cloud/authoring/launches/editing.md)
* [Hantera sidor i Launches](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Använda Timewarp för att förhandsgranska innehåll baserat på startprogram](/help/sites-cloud/authoring/launches/preview.md)
* [Befordra lanseringar](/help/sites-cloud/authoring/launches/promoting.md)

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
      * Befordra startinnehållet tillbaka till **Target** (källsidor) när det är klart för publicering.
      * Publicera innehållet från källsidorna (efter att ha befordrat dem).
      * Befordra antingen alla sidor eller endast ändrade sidor.
   * Automatiskt - det innebär följande:
      * Fältet **Starta**(**Live**) **date**: detta kan anges när du skapar eller redigerar en start.
      * Flaggan **Produktionsklar**: den kan bara anges när du redigerar en start.
      * Om flaggan **Production Ready** är inställd befordras starten automatiskt till produktionssidorna på den angivna **Launch**(**Live**) **date** . Efter kampanjen publiceras produktionssidorna automatiskt.\
        Om inget datum har angetts har flaggan ingen effekt.
* Uppdatera käll- och startsidor parallellt:
   * Ändringar av källsidorna implementeras automatiskt i startkopian (om den har konfigurerats som arv, d.v.s. som en live-kopia).
   * Du kan göra ändringar i startversionen utan att störa dessa automatiska uppdateringar eller källsidorna.

  ![Åtgärder parallellt](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Skapa en kapslad programstart](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - en programstart inom en programstart:
   * Källan är en befintlig start.
   * Du kan [befordra en kapslad start](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) till vilket mål som helst. Det kan vara en överordnad start eller källsidorna på den översta nivån (Produktion).

  ![En kapslad start](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >Om du tar bort en programstart tas själva programstarten och alla underordnade kapslade programstarter bort.

>[!NOTE]
>
>Du måste ha behörighet till `/content/launches` för att kunna skapa och redigera starter, precis som med standardgruppen `content-authors`.
>
>Kontakta systemadministratören om du får problem.

## Startar i referenser (platskonsolen) {#launches-in-references-sites-console}

1. Gå till startkällan i konsolen **Platser**.
1. Öppna listen **Referenser** och välj källsidan.
1. Välj **Startar**, de befintliga starterna visas tillsammans med åtkomst till **startarkonsolen**:

   ![Referenser till starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references.png)

1. Välj lämplig start. Listan över möjliga åtgärder visas:

   ![Åtgärder som ska vidtas vid starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## Startkonsolen {#the-launches-console}

<!--
>[!NOTE]
>
>This console is only for Launches for Pages. 
>
>To manage your Content Fragments see [Launches for Content Fragments](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).
-->

På startkonsolen får du en översikt över dina starter och kan agera på dem som visas.

![Starta konsolen - Hantera innehåll](/help/sites-cloud/authoring/assets/launches-navigate-launches-console.png)

Konsolen kan nås av:

* **Verktyg**-konsolen: **Verktyg**, **Allmänt**, **Startar**.

* **Startar konsolen** längst ned i avsnittet **Startar** i fältet **Referenser** när du navigerar i källinnehåll i webbplatskonsolen.

  ![Startar konsolen i referenser till starter i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-references.png)

* Knappen **Startar** längst upp till höger när du navigerar till startinnehåll i webbplatskonsolen:

  ![Startar alternativ i webbplatskonsolen](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)
