---
title: Licensieringspanel
description: Cloud Manager har en kontrollpanel där du enkelt kan se vilka AEMaaCS-produkträttigheter som är tillgängliga för din organisation eller hyresgäst.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: eae5c75e1bf4f7201fe2c01d08737d36489ca3e4
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 0%

---


# Licensieringspanel {#license-dashboard}

Cloud Manager har en kontrollpanel där du enkelt kan se vilka AEMaaCS-produkträttigheter som är tillgängliga för din organisation eller hyresgäst.

>[!IMPORTANT]
>
>Kontrollpanelen för licenser gäller endast AEM as a Cloud Service-programmen. [AMS-program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction) ingår inte i kontrollpanelen för licenser.
>
>Information om vilken typ av tjänst ditt program har (AMS eller AEMaaCS) finns i dokumentet [Navigera i Cloud Manager-gränssnittet.](/help/implementing/cloud-manager/navigation.md#program-cards)

## Ökning {#overview}

Cloud Manager License Dashboard ger enkel åtkomst till följande information:

1. Du har tillgång till lösningsrättigheter i alla program, inklusive vad som används och vad som är tillgängligt
1. Förbrukningsstatistik för innehållsbegäran trendade per månad för webbplatslösningen

## Använda License Dashboard {#using-dashboard}

Följ de här stegen för att få åtkomst till din kontrollpanel för licenser.

>[!NOTE]
>
>En användare i rollen **Affärsägare** måste vara inloggad för att kunna visa kontrollpanelen för licenser.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** trycker eller klickar du på menyknappen för hamburgaren i [Cloud Manager Header.](/help/implementing/cloud-manager/navigation.md#cloud-manager-header) Flikarna visas.
1. Tryck eller klicka på alternativet **Licens** på fliken.

![Licensinstrumentpanel](assets/license-dashboard.png)

Kontrollpanelen är uppdelad i tre avsnitt som visar dig:

* **Lösningar** - I det här avsnittet sammanfattas vilka lösningar som du har licensierat, till exempel Sites eller Assets.
* **Tillägg** - I det här avsnittet sammanfattas vilka tillägg till dina licensierade lösningar som du har tillgängliga.
* **Andra berättiganden** - I det här avsnittet sammanfattas vilken sandlåda och vilken dev-miljö som används samt andra berättiganden som kan användas i din klientorganisation.

I varje avsnitt sammanfattas vad som är tillgängligt och hur det används, om något alls. För närvarande visas bara Sites- och Assets-lösningar även om det finns andra lösningar i klienten.

* Kolumnen **Status** visar antalet ej använda berättiganden jämfört med det totala antalet tillgängliga för klienten.
* Kolumnen **Konfigurerad** anger de program som lösningsberättigandet har tillämpats på.
   * Ett berättigande anses bara användas när en produktionsmiljö har skapats eller om det finns en sådan, om en uppdateringspipeline har körts på den.
   * Endast ett begränsat antal program listas individuellt i kolumnen där resten representeras av en `+x`-post.
   * Håll muspekaren över posten `+x` för ett popup-fönster med information om alla program.
* I kolumnen **Användning** visas en **[Visa användningsinformation](#view-usage-details)**-knapp som visar användningsstatistik för lösningen.

>[!TIP]
>
>Mer information om hur du hanterar dina Adobe-berättiganden i hela organisationen från Admin Console finns i [Admin Console-översikten](https://helpx.adobe.com/enterprise/using/admin-console.html).

## Visa användningsinformation {#view-usage-details}

Knappen **Visa användningsinformation** ger åtkomst till den valda lösningens **användningsinformationsfönster**. I det här fönstret finns en detaljerad beskrivning med diagram som visar hur lösningen används. Hur detta mäts beror på den valda lösningen.

### Information om webbplatsanvändning {#sites-usage-details}

Fönstret **Webbplatsanvändningsinformation** innehåller diagram som ger en översikt över användningen av dina platslicenser baserat på [innehållsbegäranden.](#what-is-a-content-request)

![Fönstret med användningsinformation för webbplatser](assets/sites-usage-details.png)

Den vänstra sidan av fönstret innehåller ett cirkeldiagram som visar kontraktsuppdelningen för det kontraktsår som valts i listrutan **Visa kontraktår**.

På den högra sidan av fönstret visas ett ytdiagram som visar användningen uppdelad efter program över tid för det valda kontraktsåret. En hovring visar ett popup-fönster med information per program för den valda tidpunkten.

### Information om användning av Assets {#assets-usage-details}

Fönstret **Assets-användningsinformation** innehåller diagram med en översikt över användningen av dina Assets-licenser baserat på [lagring](#storage) och [standardanvändare.](#standard-users) Välj lämplig flik för att växla mellan vyerna.

För både lagrings- och standardanvändarvyer kan du använda listrutan **Miljötyp** för att växla mellan produktions-, scen- och utvecklingsmiljöer.

#### Lagring {#storage}

![Fönstret med användningsinformation för Assets för lagring](assets/assets-usage-details-storage.png)

Den vänstra sidan av fönstret innehåller ett cirkeldiagram som visar kontraktsuppdelningen för det kontraktsår som valts i listrutan **Visa kontraktår**.

På den högra sidan av fönstret visas ett ytdiagram som visar användningen uppdelad efter program över tid för det valda kontraktsåret. En hovring visar ett popup-fönster med information per program för den valda tidpunkten.

#### Standardanvändare {#standard-users}

![Fönstret med användningsinformation för Assets för standardanvändare](assets/assets-usage-details-standard-users.png)

Den vänstra sidan av fönstret innehåller ett cirkeldiagram som visar kontraktsuppdelningen för det kontraktsår som valts i listrutan **Visa kontraktår**.

På den högra sidan av fönstret visas ett ytdiagram som visar användningen uppdelad efter program över tid för det valda kontraktsåret. En hovring visar ett popup-fönster med information per program för den valda tidpunkten.

## Vanliga frågor {#faq}

### Vad är en innehållsförfrågan? {#what-is-a-content-request}

En innehållsbegäran är en begäran som kommer in i AEM Sites eller något annat kundtillhandahållet cachelagringssystem, t.ex. ett leveransnätverk, för att leverera innehåll eller data i antingen HTML-format som en sidvy eller i JSON-format som ett API-anrop.

En innehållsbegäran räknas för varje sidvy eller för var femte API-anrop, mätt i ingressen till det första cachelagringssystemet som tar emot en innehållsbegäran. Innehållsbegäranden räknas endast mot produktionsmiljöer.

Innehållsförfrågningar exkluderar förfrågningar eller aktiviteter som initierats av eller på uppdrag av Adobe enbart i syfte att tillhandahålla produkter och tjänster. Användaragenttrafik som identifieras av Adobe från botar, crawler och spindlar som hör till vanliga sökmotorer och tjänster inom sociala medier är också utesluten.

Se även [Förstå förfrågningar om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).

### Hur mäter Adobe Experience Manager förfrågningar om innehåll? {#how-are-content-requests-measured}

Innehållsbegäranden spåras på AEM as a Cloud Service edge-servrar. Ursprungstrafiken räknas inte med i innehållsförfrågningar. Det CDN som är inbyggt i AEM as a Cloud Service spårar giltiga förfrågningar från HTML och JSON.

AEM har också regler för att utesluta välkända organ, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

Se även [Förstå förfrågningar om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).

### Varför visar min analysrapport andra resultat än AEM innehållsförfrågningar? {#why-are-reports-different}

Innehållsförfrågningar kan innehålla avvikelser med en organisations analysrapporteringsverktyg. Mer information finns i [Förstå förfrågningar om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).

### Vad gör jag om jag vill veta mer om min innehållsförfrågningsvolym? {#current-request-volumes}

Om du vill ha ytterligare insikter om hur många innehållsförfrågningar som visas på License Dashboard kan ditt Adobe-team tillhandahålla en rapport som visar de viktigaste volymdrivrutinerna för innehållsförfrågningar. Kontakta ert Adobe-team eller Adobe kundsupport för att få en rapport över de viktigaste användningsområdena.

### Vad händer om jag använder mitt eget CDN? {#using-own-cdn}

På kontrollpanelen för licenser visas endast data som spåras av Cloud Servicens CDN. Om du väljer att ta med ditt eget CDN (BYOCDN) rapporterar du antalet innehållsförfrågningar till Adobe på årsbasis, vilket framgår av ditt avtal.
