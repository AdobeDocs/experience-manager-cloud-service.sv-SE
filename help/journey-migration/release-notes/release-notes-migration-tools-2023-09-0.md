---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.09.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.09.0
feature: Release Information
exl-id: 484a60d4-a439-43d6-a23e-4a3b45ef4160
source-git-commit: 95871cb435499b941cf9648fa2e8930049c8171c
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 3%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.09.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2023.09.0.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v3.0.0 är 7 september 2023.

### Nyheter {#what-is-new-ctt}

Verktyget Innehållsöverföring har förbättrats och ger följande fördelar:

* Minskad överföringstid vid migrering av en delmängd av en innehållsdatabas genom att använda AzCopy för att endast kopiera de blob-ID som behövs, i stället för att kopiera alla blob-ID:n.
* Snabbare tillägg av differentiellt innehåll med Oak-upgrade.
* Förbättrad tillförlitlighet genom att separera indexeringsprocessen från innehållsöverföringsprocessen. Om indexeringen misslyckas behöver innehållet inte hämtas igen. Det är bara indexeringen som startar om automatiskt, vilket sparar både tid och kraft.
