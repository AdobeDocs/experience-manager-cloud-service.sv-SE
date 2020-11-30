---
title: Introduktion till Adobe Experience Manager as a Cloud Service – terminologi
description: 'Introduktion till Adobe Experience Manager as a Cloud Service – terminologi. '
translation-type: tm+mt
source-git-commit: 465172db5bbc3b1dc3b42164d759a45e0ff13a8e
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service – terminologi {#adobe-experience-manager-as-a-cloud-service-terminology}

Följande termer används i samband med Adobe Experience Manager (AEM) as a Cloud Service:

## Produkter {#products}

| Produkt | Beskrivning |
|---|---|
| AEM as a Cloud Service | Det molnbaserade sättet att utnyttja AEM-programmen |
| AEM Assets as a Cloud Service | DAM-funktioner (Digital Asset Management) som molnbaserad, skalbar lösning för import, bearbetning och hantering av digitala resurser, samtidigt som de integreras med det bredare ekosystemet i Adobe Experience Cloud och Adobe Creative Cloud. |
| AEM Sites as a Cloud Service | En instans av AEM as a Cloud Service med programmet AEM Sites. |

## Instanser och pipelines {#instances-and-pipelines}

| Instans | Beskrivning |
|---|---|
| Adobe Pipeline | En mekanism för publicering av innehåll, från redigering till publicering. |
| AEM-redigeringsnivå | Redigeringsmiljön i Sites och Assets. |
| AEM-publiceringsnivå | Publiceringsmiljön i Sites. |


<!-- This section of the table must be alphabetic -->

## Terminologi {#terminology}

| Term | Beskrivning |
|---|---|
| AEM-bild | En distribuerbar artefakt som innehåller AEM-produktkoden tillsammans med kundkoden. |
| Asset-mikrotjänster | Molnbaserade tjänster för bearbetning av digitala resurser som är anpassade till olika användningsområden, t.ex. återgivningsgenerering, PDF-processer, hantering av underresurser, textextrahering osv. Mer information finns i [översikten över mikrotjänster för Assets](/help/assets/asset-microservices-overview.md). |
| Git-databas för Cloud Manager | Där kunderna lagrar kod och konfigurationsinställningar. |
| Molnleverantör | AEM as a Cloud Service har för närvarande stöd för Azure. Stöd för AWS finns planerat. |
| Content Delivery Network (CDN) | AEM as a Cloud Service levereras med ett CDN som standard. Dess huvudsakliga syfte är att minska latensen genom att leverera tillgängligt innehåll från CDN-noder nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program. |
| Innehållsdatabas | Plats där innehåll lagras. |
| Oberoende företagsinstanser | Varje instans av AEM as a Cloud Service isoleras från andra instanser. |
| Huvudnod | En AEM-publiceringsnivå. |
| Orkestreringsmotor | AEM as a Cloud Service använder en orkestreringsmotor för att säkerställa att alla redigerings- och publiceringstjänster skalas efter behov. |
