---
title: Versionsinformation om Cloud Manager 2023.7.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.7.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1b46f763903a1b103837ed7e8cc498ad08ce64f1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.7.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.7.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.7.0 i AEM as a Cloud Service är 29 juni 2023. Nästa version är planerad till den 10 augusti 2023.

## Nyheter {#what-is-new}

* Kort på landningssidan för Cloud Manager anger nu om [förbättrad säkerhet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) är aktiverat för sina program.
* Om en utveckling [pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) innehåller inga teststeg, användare har nu möjlighet att inkludera teststeg när de [starta rörledningen.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * Detta kommer att introduceras stegvis.
* När [avbryta utförande,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) godkännandesteget för pipeline-körningen ber nu användaren ange en orsak till att den avbryts.
   * Detta kommer att introduceras stegvis.

## Felkorrigeringar {#bug-fixes}

* När du navigerar till redigeringsgränssnittet från Cloud Manager går det inte längre att omdirigera till Unified Shell efter inloggningen.
* När du redigerar live-datumet via GoLive-widgeten navigerar du nu till **Go Live** i stället för **Förbättrat skydd** -fliken.
* När en kopieringsåtgärd startas kan en användare inte längre välja en miljö där en kopieringsåtgärd redan har anropats.
