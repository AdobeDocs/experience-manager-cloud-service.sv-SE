---
title: Licensieringspanel
description: Cloud Manager har en kontrollpanel där du enkelt kan se vilka AEMaaCS-produkträttigheter som är tillgängliga för din organisation eller hyresgäst.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Kontrollpanel för licenser {#license-dashboard}

Cloud Manager har en kontrollpanel där du enkelt kan se vilka AEMaaCS-produkträttigheter som är tillgängliga för din organisation eller hyresgäst.

>[!IMPORTANT]
>
>Kontrollpanelen för licenser gäller endast AEM as a Cloud Service-programmen. [AMS-program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction) ingår inte i kontrollpanelen för licenser.
>
>Information om vilken typ av tjänst ditt program har (AMS eller AEMaaCS) finns i [Navigera i användargränssnittet för Cloud Manager](/help/implementing/cloud-manager/navigation.md#program-cards).

## Ökning {#overview}

Cloud Manager License Dashboard ger enkel åtkomst till tillgängliga lösningsrättigheter i alla program, inklusive vad som används och vad som är tillgängligt. Och innehållet begär konsumtionsstatistik trendad på månad för webbplatslösningen.

## Åtkomst till kontrollpanelen för licenser {#using-dashboard}

>[!NOTE]
>
>En användare i rollen **Affärsägare** måste vara inloggad för att kunna visa kontrollpanelen för licenser.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på ![Visa menyikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) på [Cloud Manager Header](/help/implementing/cloud-manager/navigation.md#cloud-manager-header). Den här åtgärden visar flikarna.
1. Klicka på alternativet **Licens** på fliken.

![Licensinstrumentpanel](assets/license-dashboard.png)

Kontrollpanelen är uppdelad i tre avsnitt som visar dig:

* **Lösningar** - Vilka lösningar har du licensierat?
* **Tillägg** - Vilka tillägg till dina licensierade lösningar som du har tillgängliga.
* **Andra berättiganden** - Vilken sandlåda, vilken dev-miljö och andra berättiganden som kan användas i din klientorganisation.

I varje avsnitt sammanfattas vad som är tillgängligt och hur det används, om något alls. För närvarande visas bara Sites- och Assets-lösningar även om det finns andra lösningar i klienten.

* Kolumnen **Status** visar antalet ej använda berättiganden jämfört med det totala antalet tillgängliga för klienten.
* Kolumnen **Konfigurerad** anger de program som lösningsberättigandet har tillämpats på.
   * Ett berättigande anses bara användas när en produktionsmiljö skapas. Eller, om det finns någon, om en uppdateringspipeline har körts på den.
   * Endast ett begränsat antal program listas individuellt i kolumnen där resten representeras av en `+x`-post.
   * Håll muspekaren över posten `+x` om du vill se ett popup-fönster med information om alla program.
* I kolumnen **Användning** visas en **[Visa användningsinformation](#view-usage-details)**-knapp som visar användningsstatistik för lösningen.

>[!TIP]
>
>Mer information om hur du hanterar dina Adobe-berättiganden i hela organisationen från Admin Console finns i [Admin Console-översikten](https://helpx.adobe.com/enterprise/using/admin-console.html).

## Visa användningsinformation {#view-usage-details}

<!--
The **View usage details** button gives access to the chosen solution's **Usage Details** window. This window gives a detailed breakdown including charts to show your solution's usage. How that usage is measured depends on the chosen solution. -->

Knappen **Visa användningsinformation** i licensområdet för Cloud Manager innehåller en detaljerad beskrivning av din aktuella resursanvändning. När du klickar på den öppnas en rapport eller kontrollpanel med viktig information om din licens. <!-- ADD THIS SENTENCE IF ASSETS USAGE DETAILS GETS REINSTATED ", such as the number of users, storage consumption, or bandwidth usage, depending on the type of services you're using." --> Den här funktionen hjälper dig att övervaka och se till att du ligger inom avtalsgränserna samtidigt som du erbjuder insikter för bättre resursplanering och optimering.

### Information om webbplatsanvändning {#sites-usage-details}

Fönstret **Webbplatsanvändningsinformation** innehåller diagram som ger en översikt över hur webbplatslicenserna används baserat på [innehållsbegäranden](#what-is-a-content-request).

![Fönstret med användningsinformation för webbplatser](assets/sites-usage-details.png)

Den vänstra sidan av fönstret innehåller ett cirkeldiagram som visar kontraktsuppdelningen för det kontraktsår som valts i listrutan **Visa kontraktår**.

På den högra sidan av fönstret visas ett ytdiagram som visar användningen uppdelad efter program över tid för det valda kontraktsåret. En hovring visar ett popup-fönster med information per program för den valda tidpunkten.

<!-- REMOVED AS PER CQDOC-21983
### Assets usage details {#assets-usage-details}

The **Assets usage details** window, presents graphs giving an overview of the usage of your Assets licenses based on [storage](#storage) and [standard users](#standard-users). Select the appropriate tab to toggle between the views.

For both storage and standard users views, you can use the **Environment Type** dropdown to toggle the view between production, stage, and development environments.

#### Storage {#storage}

![Assets usage details window for storage](assets/assets-usage-details-storage.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time.

#### Standard Users {#standard-users}

![Assets usage details window for standard-users](assets/assets-usage-details-standard-users.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time. -->

## Frågor och svar {#faq}

+++**Vad är en innehållsförfrågan?** {#what-is-a-content-request}

En innehållsbegäran är en begäran som riktas till AEM Sites eller ett cachelagringssystem som kunden tillhandahåller, till exempel ett leveransnätverk. Det hämtar innehåll eller data i HTML-format för sidvisningar. Eller i JSON-format för API-anrop.

En innehållsbegäran räknas för varje sidvy eller för var femte API-anrop, mätt i ingressen till det första cachelagringssystemet som tar emot en innehållsbegäran. Innehållsbegäranden räknas endast mot produktionsmiljöer.

Innehållsförfrågningar exkluderar förfrågningar eller aktiviteter som initierats av eller på uppdrag av Adobe enbart i syfte att tillhandahålla produkter och tjänster. Användaragenttrafik som identifieras av Adobe från botar, crawler och spindlar som hör till vanliga sökmotorer och tjänster inom sociala medier är också utesluten.

Se även [Förstå innehållsförfrågningar från Cloud Service](/help/implementing/cloud-manager/content-requests.md).
+++

+++**Hur mäter Adobe Experience Manager innehållsförfrågningar?** {#how-are-content-requests-measured}

Innehållsbegäranden spåras på AEM as a Cloud Service edge-servrar. Ursprungstrafiken räknas inte med i innehållsförfrågningar. Det CDN som är inbyggt i AEM as a Cloud Service spårar giltiga förfrågningar från HTML och JSON.

AEM har också regler för att utesluta välkända organ, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

Se även [Förstå förfrågningar om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).
+++

+++**Varför visar min analysrapport andra resultat än AEM innehållsförfrågningar?** {#why-are-reports-different}

Innehållsförfrågningar kan innehålla avvikelser med en organisations analysrapporteringsverktyg. Mer information finns i [Förstå förfrågningar om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).
+++

+++**Vad gör jag om jag vill veta mer om min volym för innehållsförfrågan?** {#current-request-volumes}

Om du vill ha ytterligare insikter om hur många innehållsförfrågningar som visas på kontrollpanelen för licenser kan ditt Adobe-team tillhandahålla en rapport som visar de viktigaste volymdrivrutinerna för innehållsförfrågningar. Kontakta ert Adobe-team eller Adobe kundsupport för att få en rapport över de viktigaste användningsområdena.
+++

+++**Vad händer om jag använder mitt eget CDN?** {#using-own-cdn}

På kontrollpanelen för licenser visas endast data som spåras av Cloud Servicens CDN. Om du väljer att ta med ditt eget CDN (BYOCDN) rapporterar du antalet innehållsförfrågningar till Adobe på årsbasis, vilket framgår av ditt avtal.
+++

