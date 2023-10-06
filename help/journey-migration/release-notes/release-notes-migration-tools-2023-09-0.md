---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.09.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.09.0
feature: Release Information
source-git-commit: 08e9f21022a3dcf0edfbc0ebbf76c9253b730fac
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.09.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.09.0.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v3.0.0 är 7 september 2023.

### Nyheter {#what-is-new-ctt}

Verktyget Innehållsöverföring har förbättrats avsevärt och ger följande fördelar:
* Minskad överföringstid vid migrering av en delmängd av en innehållsdatabas genom att använda AzCopy för att endast kopiera de blob-ID som krävs i stället för att kopiera alla blob-ID:n
* Snabbare uppdatering av differentiellt innehåll med Oak-upgrade
* Förbättrad tillförlitlighet genom att separera indexeringsprocessen från innehållsöverföringsprocessen. Om indexeringen misslyckas behöver innehållet inte importeras igen. Endast indexeringen startar om automatiskt, vilket sparar både tid och pengar
