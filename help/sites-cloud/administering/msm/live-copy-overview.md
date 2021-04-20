---
title: Översiktskonsol för Live Copy
description: Lär dig mer om grunderna i Live Copy Overview Console där du snabbt kan förstå statusen för dina Live-kopior för att kunna synkronisera innehåll.
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# Översiktskonsol för Live-kopia {#live-copy-overview-console}

Med konsolen **Live Copy Overview** kan du:

* Visa/hantera arv på en webbplats.
   * Visa det blå trädet och motsvarande Live Copy-struktur, tillsammans med deras arvsstatus
   * Ändra arvsstatus, till exempel att avbryta och återuppta
   * Visa egenskaper för utkast och Live Copy
* Utför utrullningsåtgärder.

## Öppnar Live Copy-översikt {#opening-the-live-copy-overview}

Du kan öppna Live-kopieringsöversikt från:

* [Panelen Referenser till en översiktssida (Sites console)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Egenskaper för en ritningssida](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Referenser till en designsida {#references-to-a-blueprint-page}

Översikt över Live-kopian **kan öppnas från panelen** Referenser **i konsolen** Platser **:**

1. I konsolen **Platser**, [navigerar du till din designsida och markerar den.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Öppna **[referenserna](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** och välj **Live-kopior**.

   ![Live Copy from references rail](../assets/live-copy-references.png)

   >[!TIP]
   >
   >Du kan också öppna referenser först och sedan välja en plan.

1. Välj **Översikt över Live-kopia** om du vill visa och använda översikten över alla Live-kopior som hör till den valda planen.
1. Använd **Stäng** för att avsluta och återgå till konsolen **Platser**.

### Egenskaper för en blå sida {#properties-of-a-blueprint-page}

**Översikt över Live-kopian** kan öppnas när du visar egenskaper för en översiktssida:

1. Öppna **Egenskaper** för lämplig ritningssida.
1. Öppna fliken **Design** - alternativet **Live Copy Overview** visas i det övre verktygsfältet:

   ![Egenskaper för utkast, flik](../assets/live-copy-blueprint-tab.png)

1. Välj **Översikt över Live-kopia** om du vill visa och använda översikten över alla Live-kopior som hör till den aktuella planen.

1. Använd **Stäng** för att avsluta och återgå till konsolen **Platser**.

## Använda Live Copy-översikt {#using-the-live-copy-overview}

Fönstret **Översikt över Live-kopia** innehåller en översikt över statusen för de Live-kopior som hör till den valda sidan.

![Live Copy Overview](../assets/live-copy-overview.png)

En utrullning beror på de synkroniseringsåtgärder som har definierats i den specifika utrullningskonfigurationen. Vissa åtgärder är beroende av ändringar i innehållet. Men det finns också många åtgärder som inte är beroende av ändringar i innehållet, men som är beroende av händelser som till exempel sidaktivering. Sådana händelser ändrar inte innehållet, men ändrar de interna egenskaperna som är relaterade till innehållet.

Statusfälten är också beroende av de synkroniseringsåtgärder som har definierats i den specifika rollout-konfigurationen och anger om det finns några sådana åtgärder för antingen utkast eller Live Copy sedan den senaste lyckade utrullningen. Ett statusfält återspeglar bara åtgärderna i den specifika utrullningskonfigurationen. Om ingen lyckad utrullning har utförts på en Live-kopia visas alltid statusen aktuell.

En utrullningskonfiguration definieras till exempel som `targetActivate`. Därför är en utrullning endast beroende av aktiveringshändelser. Statusfältet anger bara om några aktiveringshändelser har inträffat sedan den senaste utrullningen.

**Översikt över Live-kopian** kan även användas för att utföra åtgärder i Live-kopian:

1. Öppna **Live Copy Overview**.
1. Välj önskad plan- eller Live Copy-sida så uppdateras verktygsfältet så att de tillgängliga åtgärderna visas. Vilka [åtgärder](overview.md#terms-used) som är tillgängliga beror på om du väljer en [ritning](#actions-for-a-blueprint-page)- eller [Live Copy](#actions-for-a-live-copy-page)-sida.

### Åtgärder för en blå sida {#actions-for-a-blueprint-page}

När du väljer en ritningssida är följande åtgärder tillgängliga:

![Live Copy Overview-åtgärder för en plan](../assets/live-copy-overview-actions-blueprint.png)

* **Redigera**  - Öppna ritningssidan för redigering.
* **[Rollout](overview.md#rollout-and-synchronize)**  - Utför en utrullning för att föra över ändringar från källan till Live Copy.

### Åtgärder för en Live Copy-sida {#actions-for-a-live-copy-page}

När du väljer en Live Copy-sida är följande åtgärder tillgängliga:

![Live Copy Overview-åtgärder för en Live Copy](../assets/live-copy-overview-actions.png)

* **Redigera**  - Öppna Live Copy-sidan för redigering.
* **[Relationsstatus](#relationship-status)**  - Visa information om status och arv.
* **[Synkronisera](overview.md#rollout-and-synchronize)**  - Synkronisera en Live-kopia för att dra ändringar från källan till Live-kopian.
* **[Återställ](creating-live-copies.md#resetting-a-live-copy-page)**  - Återställ en Live Copy-sida om du vill ta bort alla arvsannulleringar och återställa sidan till samma läge som källsidan.
* **[Gör uppehåll](overview.md#suspending-and-cancelling-inheritance-and-synchronization)**  - Inaktiverar tillfälligt relationen mellan en Live Copy och dess designsida.
* **[Återuppta](creating-live-copies.md#resuming-inheritance-for-a-page)**  - Med Återuppta kan du återskapa en pausad relation.
* **[Koppla loss](overview.md#detaching-a-live-copy)**  - Tar permanent bort den aktiva relationen mellan en Live-kopia och dess designsida.

## Relationsstatus {#relationship-status}

Konsolen **Relationsstatus** har två flikar med en rad funktioner.

* [Relationsstatus](#relationship-status-tab)
* [Live Copy](#live-copy-tab)

### Relationsstatus {#relationship-status-tab}

Fliken innehåller detaljerad information om statusen för relationen mellan ritningen och Live Copy.

![Fliken Relationsstatus](../assets/live-copy-relationship-status.png)

### Live-kopia {#live-copy-tab}

På den här fliken kan du visa och redigera Live Copy-konfigurationen.

![Fliken Live Copy](../assets/live-copy-relationship-status-live-copy.png)
