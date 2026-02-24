---
title: Redigeringsövningar
description: När du har skapat en startsida för sidan (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 16%

---

# Redigeringsövningar {#editing-launches}

## Redigera startsidor {#editing-launch-pages}

När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.

1. Gå till [Starta från referenser (Sites-konsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder.
1. Välj **Gå till sidan** om du vill öppna sidan för redigering.

När du redigerar sidan visas en indikering i det övre verktygsfältet tillsammans med alternativen **Lämna** och **Navigera** :

![Lämna och navigera vid start från sidredigeraren](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>Du får inte flytta en sida inom en start. Om du försöker utföra den här åtgärden utlöses ett varningsmeddelande:
>
>* Varning! Den här sidan är källan till en start. Det är inte tillåtet att flytta sidan.

### Redigera startsidor som är beroende av en Live-kopia {#editing-launch-pages-subject-to-a-live-copy}

Om din start baseras på en [Live-kopia](/help/sites-cloud/administering/msm/overview.md) gör du följande:

* Se låsa symboler (små hänglås) när du redigerar en komponent (innehåll och/eller egenskaper).
* Se fliken **Live-kopia** i **Sidegenskaper**

En live-kopia används för att synkronisera innehåll *från* källgrenen *till* startgrenen (för att hålla startsidan uppdaterad med ändringarna i källan).

Du kan göra ändringar på samma sätt som du kan redigera en vanlig Live-kopia, till exempel:

* Om du klickar på ett stängt hänglås bryts synkroniseringen och du kan göra nya uppdateringar av innehållet när du startar programmet. När du har låst upp (öppet hänglås) skrivs inte ändringarna över av ändringar som gjorts på samma plats i källgrenen.
* **Gör uppehåll i** (och **återuppta**) arv för en viss sida.

Mer information finns i [Ändra innehåll för Live-kopia](/help/sites-cloud/administering/msm/creating-live-copies.md).

## Jämföra en startsida med dess Source-sida {#comparing-a-launch-page-to-its-source-page}

Om du vill spåra de ändringar du har gjort kan du visa startsidan i **Referenser** och jämföra startsidan med dess källsida:

1. I konsolen **Platser** navigerar [till källsidorna för din start och väljer en](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna panelen **[Referenser](/help/sites-cloud/authoring/basic-handling.md#references)** och välj **Startar**.
1. Välj en specifik start och **Jämför med Source**:

   ![Jämför start med källa](/help/sites-cloud/authoring/assets/launches-compare.png)

1. De två sidorna (start och källa) öppnas sida vid sida.

   Mer information om hur du använder den här funktionen finns i [Sidskillnad](/help/sites-cloud/authoring/sites-console/page-diff.md).

## Ändra använda Source-sidor {#changing-the-source-pages-used}

Du kan när som helst lägga till eller ta bort sidor till/från intervallet med källsidor för en start:

1. Öppna och välj programstart från:
   * [Startar konsolen](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Välj **Redigera**.
   * [Referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder:
      * Välj **Redigera start**.
      * Källsidorna visas.
1. Gör önskade ändringar och bekräfta sedan med **Spara**.

>[!NOTE]
>
>Om du vill lägga till sidor i en programstart måste de ligga under en gemensam språkrot, det vill säga inom en enda plats.

## Redigera en startkonfiguration {#editing-a-launch-configuration}

Du kan när som helst redigera egenskaperna för en start:

1. Öppna och välj programstart från:
   * [Startar konsolen](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Välj **Egenskaper**.
   * [Referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder:
      * Välj **Redigera egenskaper**.
      * Detaljerna visas.
1. Gör önskade ändringar och bekräfta sedan med **Spara**.
   * Avsnittet [Startsidor och händelseordning](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) innehåller information om syftet med och interaktionen mellan fälten **Startdatum** och **Produktionsklar**.

## Identifiera startstatus för en sida {#discovering-the-launch-status-of-a-page}

Statusen visas när du väljer en specifik start på fliken Inställningar (se [Startar i Referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Identifierar startstatus](/help/sites-cloud/authoring/assets/launches-status.png)
