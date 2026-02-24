---
title: Översiktskonsol för Live Copy
description: Lär dig grunderna i Live Copy Overview Console för att snabbt förstå statusen för dina Live-kopior för att synkronisera innehåll.
feature: Multi Site Manager
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: 3ef7fbce-10a1-4b21-8486-d3c3706e537c
solution: Experience Manager Sites
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# Översiktskonsol för Live Copy {#live-copy-overview-console}

Med konsolen **Live Copy Overview** kan du:

* Visa/hantera arv på en webbplats.
   * Visa det blå trädet och motsvarande Live Copy-struktur, tillsammans med deras arvsstatus
   * Ändra arvsstatus, till exempel att avbryta och återuppta
   * Visa egenskaper för utkast och Live Copy
* Utför utrullningsåtgärder.

## Öppna Live Copy-översikt {#opening-the-live-copy-overview}

Du kan öppna Live-kopieringsöversikt från:

* [Panelen Referenser till en översiktssida (Sites console)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Egenskaper för en ritningssida](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Referenser till en designsida {#references-to-a-blueprint-page}

Översikt över **Live-kopian** kan öppnas från sidopanelen **Referenser** i **Sites**-konsolen:

1. I konsolen **Platser** [navigerar du till din ritningssida och markerar den](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna listen **[Referenser](/help/sites-cloud/authoring/basic-handling.md#references)** och välj **Live-kopior**.

   ![Live Copy from references rail](../assets/live-copy-references.png)

   >[!TIP]
   >
   >Du kan också öppna referenser först och sedan välja en plan.

1. Välj **Översikt över Live-kopia** om du vill visa och använda översikten över alla Live-kopior som hör till den valda planen.
1. Använd **Close** för att avsluta och återgå till konsolen **Sites**.

### Egenskaper för en blå sida {#properties-of-a-blueprint-page}

Översikt över **Live-kopian** kan öppnas när du visar egenskaper för en ritningssida:

1. Öppna **Egenskaper** för lämplig ritningssida.
1. Öppna fliken **Utskrift** - alternativet **Översikt över Live-kopia** visas i det övre verktygsfältet:

   ![Egenskaper för utkast &#x200B;](../assets/live-copy-blueprint-tab.png)

1. Välj **Översikt över Live-kopia** om du vill visa och använda översikten över alla Live-kopior som hör till den aktuella planen.

1. Använd **Close** för att avsluta och återgå till konsolen **Sites**.

## Använda Live Copy-översikt {#using-the-live-copy-overview}

Fönstret **Live-kopieringsöversikt** innehåller en översikt över statusen för de Live-kopior som hör till den valda sidan.

![Live Copy Overview-fönstret](../assets/live-copy-overview.png)

En utrullning beror på de synkroniseringsåtgärder som har definierats i den specifika utrullningskonfigurationen. Vissa åtgärder är beroende av ändringar i innehållet. Men det finns också många åtgärder som inte är beroende av ändringar i innehållet, men som är beroende av händelser som till exempel sidaktivering. Sådana händelser ändrar inte innehållet, men ändrar de interna egenskaperna som är relaterade till innehållet.

Statusfälten är också beroende av de synkroniseringsåtgärder som har definierats i den specifika rollout-konfigurationen och anger om det finns några sådana åtgärder för antingen utkast eller Live Copy sedan den senaste lyckade utrullningen. Ett statusfält återspeglar bara åtgärderna i den specifika utrullningskonfigurationen. Om ingen lyckad utrullning har utförts på en Live-kopia visas alltid statusen aktuell.

En utrullningskonfiguration definieras till exempel som `targetActivate`. Därför är en utrullning endast beroende av aktiveringshändelser. Statusfältet anger bara om några aktiveringshändelser har inträffat sedan den senaste utrullningen.

Översikt över **Live-kopian** kan även användas för att utföra åtgärder på Live-kopian:

1. Öppna **Live Copy-översikten**.
1. Välj önskad plan- eller Live Copy-sida så uppdateras verktygsfältet så att de tillgängliga åtgärderna visas. Vilka [åtgärder](overview.md#terms-used) som är tillgängliga beror på om du väljer en [utkast](#actions-for-a-blueprint-page)- eller [Live Copy](#actions-for-a-live-copy-page)-sida.

### Åtgärder för en designsida {#actions-for-a-blueprint-page}

När du väljer en ritningssida är följande åtgärder tillgängliga:

![Live-kopia - översiktsåtgärder för en plan](../assets/live-copy-overview-actions-blueprint.png)

* **Redigera** - Öppna ritningssidan för redigering.
* **[Rollout](overview.md#rollout-and-synchronize)** - Utför en utrullning för att skicka ändringar från källan till Live-kopian.

### Åtgärder för en Live Copy-sida {#actions-for-a-live-copy-page}

När du väljer en Live Copy-sida är följande åtgärder tillgängliga:

![Live-kopia - översiktsåtgärder för en Live-kopia](../assets/live-copy-overview-actions.png)

* **Redigera** - Öppna sidan Live-kopia för redigering.
* **[Relationsstatus](#relationship-status)** - Visa information om status och arv.
* **[Synkronisera](overview.md#rollout-and-synchronize)** - Synkronisera en Live-kopia om du vill hämta ändringar från källan till Live-kopian.
* **[Återställ](creating-live-copies.md#resetting-a-live-copy-page)** - Återställ en Live Copy-sida om du vill ta bort alla arvsavbrott och återställa sidan till samma läge som källsidan.
* **[Gör uppehåll](overview.md#suspending-and-cancelling-inheritance-and-synchronization)** - Inaktiverar tillfälligt den aktiva relationen mellan en Live-kopia och dess designsida.
* **[Återuppta](creating-live-copies.md#resuming-inheritance-for-a-page)** - Med Återuppta kan du återskapa en pausad relation.
* **[Koppla loss](overview.md#detaching-a-live-copy)** - Tar permanent bort den aktiva relationen mellan en Live-kopia och dess designsida.

## Relationsstatus {#relationship-status}

Konsolen **Relationsstatus** har två flikar med en rad funktioner.

* [Relationsstatus](#relationship-status-tab)
* [Live Copy](#live-copy-tab)

### Relationsstatus {#relationship-status-tab}

Fliken innehåller detaljerad information om statusen för relationen mellan ritningen och Live Copy.

![Fliken Relationsstatus](../assets/live-copy-relationship-status.png)

### Live Copy {#live-copy-tab}

På den här fliken kan du visa och redigera Live Copy-konfigurationen.

![Fliken Live-kopia](../assets/live-copy-relationship-status-live-copy.png)
