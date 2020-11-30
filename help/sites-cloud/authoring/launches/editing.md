---
title: Redigera Launches
description: 'När du har skapat en startsida för sidan (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna. '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 19%

---


# Redigera Launches {#editing-launches}

## Redigera startsidor {#editing-launch-pages}

När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.

1. Öppna [Starta från referenser (Sites-konsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder.
1. Välj **Gå till sidan** för att öppna sidan för redigering.

### Redigera startsidor som är beroende av en Live-kopia {#editing-launch-pages-subject-to-a-live-copy}

Om lanseringen baseras på en live-kopia kommer du att: <!--If your launch is based upon a [live copy](/help/sites-administering/msm.md) then you will:-->

* Se låsa symboler (små hänglås) när du redigerar en komponent (innehåll och/eller egenskaper).
* Se fliken **Live-kopia** i **Sidegenskaper**

En live-kopia används för att synkronisera innehåll *från* källgrenen *till* startgrenen (för att hålla startsidan uppdaterad med ändringarna i källan).

Du kan göra ändringar på samma sätt som du kan redigera en vanlig Live-kopia; till exempel:

* Om du klickar på ett stängt hänglås bryts synkroniseringen och du kan göra nya uppdateringar av innehållet när du startar programmet. När du har låst upp (öppet hänglås) skrivs inte ändringarna över av ändringar som gjorts på samma plats i källgrenen.
* **Gör uppehåll i** (och **återuppta**) arv för en viss sida.

Mer information finns i Ändra Live Copy-innehåll. <!--See [Changing Live Copy Content](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) for further information.-->

## Jämföra en startsida med dess källsida {#comparing-a-launch-page-to-its-source-page}

Om du vill spåra de ändringar du har gjort kan du visa startsidan i **Referenser** och jämföra startsidan med dess källsida:

1. Gå **till startsidan i konsolen** Platser [och markera den](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Öppna panelen **[Referenser](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** och välj **Starta**.
1. Välj en specifik start och sedan **Jämför med källa**:

   ![Jämför start med källa](/help/sites-cloud/authoring/assets/launches-compare.png)

1. De två sidorna (start och källa) öppnas sida vid sida.

   Mer information om hur du använder den här funktionen finns i [Sidskillnad](/help/sites-cloud/authoring/features/page-diff.md).

## Ändra använda källsidor {#changing-the-source-pages-used}

Du kan när som helst lägga till eller ta bort sidor till/från intervallet med källsidor för en start:

1. Öppna och välj programstart från:
   * The [Launches console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Välj **Redigera**.
   * [Referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder:
      * Välj **Redigera start**.
      * Källsidorna visas.
1. Gör önskade ändringar och bekräfta sedan med **Spara**.

>[!NOTE]
>
>Om du vill lägga till sidor i en programstart måste de ligga under en gemensam språkrot. dvs. inom en enda plats.

## Redigera en startkonfiguration {#editing-a-launch-configuration}

Du kan när som helst redigera egenskaperna för en start:

1. Öppna och välj programstart från:
   * konsolen [](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)Launches:
      * Välj **Egenskaper**.
   * [Referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder:
      * Select **Edit Properties**.
      * Detaljerna visas.
1. Gör önskade ändringar och bekräfta sedan med **Spara**.
   * Avsnittet [Startsidor och händelseordning](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) innehåller information om syftet med och interaktionen mellan fälten **Startdatum** och **Produktionsklar**.

## Identifiera startstatus för en sida {#discovering-the-launch-status-of-a-page}

Statusen visas när du väljer en viss start på fliken Inställningar (se [Starta i Referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Identifierar startstatus](/help/sites-cloud/authoring/assets/launches-status.png)
