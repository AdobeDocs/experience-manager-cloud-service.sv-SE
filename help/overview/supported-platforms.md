---
title: Klientplattformar som stöds
description: Lär dig vilka webbläsare som kan användas för att skapa innehåll med Adobe Experience Manager as a Cloud Service och komma åt webbplatser som publiceras med AEM.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Klientplattformar som stöds {#supported-platforms}

Lär dig vilka webbläsare som kan användas för att skapa innehåll med Adobe Experience Manager as a Cloud Service och komma åt webbplatser som publiceras med AEM.

>[!TIP]
>
>Det här dokumentet innehåller klientplattformar som stöds av AEM as a Cloud Service. Mer information om byggmiljön för utveckling av ditt AEM-projekt finns i dokumentet [Build Environment.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## Supportnivåer {#support-levels}

Adobe definierar följande supportnivåer för AEM klientplattformar.

| Supportnivå | Beskrivning |
|---|---|
| A: Stöds | Adobe ger fullständig support och underhåll för den här konfigurationen. Den här konfigurationen omfattas av Adobe kvalitetssäkringsprocess. |
| R: Begränsat stöd | Support kräver en formell begäran till Adobe om att kunna använda konfigurationen i ett projekt. När Adobe har bekräftats av Adobe ger det full support inom det begränsade supportprogrammet. Mer information får du av Adobe kundtjänst. |
| Z: Stöds inte | Konfigurationen stöds inte. Adobe har inga programsatser om huruvida konfigurationen fungerar eller inte. |

## Webbläsare som stöds för att skapa innehåll {#authoring}

AEM användargränssnitt är optimerat för större skärmar som finns i bärbara datorer, stationära datorer och surfplattor (som Apple iPad eller Microsoft Surface). Telefonformfaktorn stöds inte för redigeringssyften.

Adobe Experience Manager användargränssnitt fungerar med följande klientplattformar beroende på [redigeringsmetod.](/help/edge/overview.md#authoring-method)

* [Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [Page Editor](/help/sites-cloud/authoring/page-editor/introduction.md)
* [Dokumentbaserad redigering](/help/edge/docs/authoring.md) med [Sidekick](/help/edge/docs/sidekick.md)

Alla webbläsare testas med standarduppsättningen med plugin-program och tillägg.

| Webbläsare | Universell redigeringssupport | Stödnivå för sidredigeraren | Sidekick supportnivå |
|---|---|---|---|
| Google Chrome (evergreen) | A: Stöds | A: Stöds | A: Stöds |
| Microsoft Edge (evergreen) | A: Stöds | A: Stöds | Z: Stöds inte |
| Mozilla Firefox (evergreen) | A: Stöds | A: Stöds | Z: Stöds inte |
| Mozilla Firefox senaste ESR [1] | A: Stöds | A: Stöds | Z: Stöds inte |
| Safari på macOS (evergreen) | A: Stöds | A: Stöds | Z: Stöds inte |
| Safari på iOS (evergreen) [2] | Z: Stöds inte | A: Stöds | Z: Stöds inte |

1. Extended Support Release för Firefox ([läs mer om mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/))
1. Stöd endast för Apple iPad

>[!NOTE]
>
>**Stöd för webbläsare med snabba releasecykler:**
>
>Uppdateringar av Firefox, Chrome och Edge regelbundet. Adobe vill behålla den supportnivå som anges ovan för kommande versioner av dessa webbläsare.

## Webbläsare som stöds för webbplatser {#websites}

Webbläsarstöd för webbplatser som återges av AEM beror på implementeringen av AEM sidmallar, block, design och komponentutdata. Därför har utvecklare som implementerar ditt projekt kontrollen över webbplatsens kompatibilitet.

AEM [Project-mallen ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project) [Core Components,](/help/implementing/developing/components/overview.md#aem-core-components) och [WKND sample site](/help/implementing/developing/introduction/develop-wknd-tutorial.md) är alla kompatibla med alla moderna webbläsare.
