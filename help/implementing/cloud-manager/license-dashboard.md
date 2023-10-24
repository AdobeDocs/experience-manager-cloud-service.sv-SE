---
title: Licensieringspanel
description: Med Cloud Manager får du en kontrollpanel där du enkelt kan se vilka AEMaaCS-produkträttigheter som är tillgängliga för din organisation eller klientorganisation.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: fbfb5d3ee8dbc8bc4cbe118fd4ce97284f712bb4
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Licensieringspanel {#license-dashboard}

Med Cloud Manager får du en kontrollpanel där du enkelt kan se vilka AEMaaCS-produkträttigheter som är tillgängliga för din organisation eller klientorganisation.

## Översikt {#overview}

Licensinstrumentpanelen för Cloud Manager ger enkel åtkomst till följande information:

1. Du har tillgång till lösningsrättigheter i alla program, inklusive vad som används och vad som är tillgängligt
1. Förbrukningsstatistik för innehållsbegäran trendade per månad för webbplatslösningen

## Använda License Dashboard {#using-dashboard}

Följ de här stegen för att få åtkomst till din kontrollpanel för licenser.

>[!NOTE]
>
>En användare i **Företagsägare** rollerna måste vara inloggade för att du ska kunna se License Dashboard.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. På produktöversikten växlar du till **Licens** -fliken.

![Licensieringspanel](assets/license-dashboard.png)

Kontrollpanelen är uppdelad i tre avsnitt som visar dig:

* **Lösningar** - Här sammanfattas vilka lösningar du har licensierat, t.ex. Sites eller Assets.
* **Tillägg** - I det här avsnittet sammanfattas vilka tillägg till licensierade lösningar som du har tillgång till.
* **Sandbox &amp; Development Environment** - I det här avsnittet sammanfattas vilka miljöer du har.

I varje avsnitt sammanfattas vad som är tillgängligt och hur det används, om något alls. För närvarande visas bara platslösningar, även om det finns andra lösningar i klientorganisationen.

* The **Status** kolumn visar antalet oanvända berättiganden jämfört med det totala tillgängliga för klienten.
* The **Konfigurerad den** -kolumnen anger de program som lösningsberättigandet har tillämpats på.
   * Ett berättigande anses bara användas när en produktionsmiljö har skapats eller om det finns en sådan, om en uppdateringspipeline har körts på den.
* The **Användning** kolumn visas de innehållsbegäranden som har förbrukats under de senaste 12 månaderna som ett diagram när du klickar på det.

>[!TIP]
>
>Om du vill veta hur du hanterar dina Adobe-rättigheter i hela organisationen från Admin Console går du till [Admin Console - översikt](https://helpx.adobe.com/enterprise/using/admin-console.html).

## Vanliga frågor {#faq}

### Vad är en innehållsförfrågan? {#what-is-a-content-request}

En innehållsbegäran är en begäran som kommer in i AEM Sites eller något annat kundtillhandahållet cachelagringssystem, t.ex. ett leveransnätverk, för att leverera innehåll eller data i antingen HTML-format som en sidvy eller i JSON-format som ett API-anrop.

En innehållsbegäran räknas för varje sidvy eller för var femte API-anrop, mätt i ingressen till det första cachelagringssystemet som tar emot en innehållsbegäran. Innehållsbegäranden räknas endast mot produktionsmiljöer.

Innehållsförfrågningar exkluderar förfrågningar eller aktiviteter som initierats av eller på uppdrag av Adobe enbart i syfte att tillhandahålla produkter och tjänster. Användaragenttrafik som identifieras av Adobe från botar, crawler och spindlar som hör till vanliga sökmotorer och tjänster inom sociala medier är också utesluten.

Se även [Förstå begäranden om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).

### Hur mäter Adobe Experience Manager förfrågningar om innehåll? {#how-are-content-requests-measured}

Innehållsförfrågningar spåras på AEM as a Cloud Service edge-servrar. Ursprungstrafiken räknas inte med i innehållsförfrågningar. Det CDN som är inbyggt i AEM as a Cloud Service spårar giltiga begäranden om HTML och JSON.

AEM har också regler för att utesluta välkända organ, inklusive välkända tjänster som regelbundet besöker webbplatsen för att uppdatera deras sökindex eller tjänst.

Se även [Förstå begäranden om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).

### Varför visar min analysrapport andra resultat än AEM innehållsförfrågningar? {#why-are-reports-different}

Innehållsförfrågningar kan innehålla avvikelser med en organisations analysrapporteringsverktyg. Mer information finns i [Förstå begäranden om Cloud Service innehåll](/help/implementing/cloud-manager/content-requests.md).

### Vad gör jag om jag vill veta mer om min innehållsförfrågningsvolym? {#current-request-volumes}

Om du vill ha ytterligare insikter om hur många innehållsförfrågningar som visas på License Dashboard kan ditt Adobe-team tillhandahålla en rapport som visar de viktigaste volymdrivrutinerna för innehållsförfrågningar. Kontakta ert Adobe-team eller Adobe kundsupport för att få en rapport över de viktigaste användningsområdena.

### Vad händer om jag använder mitt eget CDN? {#using-own-cdn}

På kontrollpanelen för licenser visas endast data som spåras av Cloud Servicens CDN. Om du väljer att ta med ditt eget CDN (BYOCDN) rapporterar du antalet innehållsförfrågningar till Adobe på årsbasis, vilket framgår av ditt avtal.
