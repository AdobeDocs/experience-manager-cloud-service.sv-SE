---
title: Versionsinformation om Cloud Manager 2022.12.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2022.12.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: aa7f2175e2a43a318a6171e622d292ed3a8e958b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2022.12.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager 2022.12.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2022.12.0 i AEM as a Cloud Service är 29 november 2022. Nästa version är planerad till den 19 januari 2023.

## Nyheter {#what-is-new}

* Meddelanden för [AEM](/help/overview/what-is-new-and-different.md#aem-updates) visas i användargränssnittet för Cloud Manager. Denna förändring introduceras stegvis under veckorna efter version 2022.12.0.
* Vid intag via [Verktyget Innehållsöverföring (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) pågår visas miljöstatusen i både utvecklarkonsolen och i Cloud Manager som `Ingestion in Progress`.
* Förbättringar av tillgänglighet och tillförlitlighet för [Molnhanterarens pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) var gjorda.

## Felkorrigeringar {#bug-fixes}

* En ändring gjordes för att förhindra [rörledningar](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) från att köras medan en pipeline-körning pågår i samma miljö.
* En ändring gjordes för att förhindra `PATCH /program//environment//variables` för miljöer med `FAILED` status.
