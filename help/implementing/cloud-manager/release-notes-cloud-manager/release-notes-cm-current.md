---
title: Versionsinformation om Cloud Manager 2022.3.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2022.3.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2022.3.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager 2022.3.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2022.3.0 i AEM as a Cloud Service 10 mars 2022. Nästa version är planerad till den 7 april 2022.

## Nyheter {#what-is-new}

* En användare med **Utvecklare** rollen har nu åtkomst till AEM.
* [The `reliability_rating` kritiskt mått](/help/implementing/cloud-manager/code-quality-testing.md) har inaktiverats.
* En användare kan nu sortera kolumnerna i **Pipelines** i Cloud Manager.

## Felkorrigeringar {#bug-fixes}

* En delmängd av manuellt skapade Git-databaser hade felaktiga namnvärden som påverkades [återanvändningsfunktionen för build-felaktigheter.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) Namnen på dessa databaser har ändrats och användarna ser det korrigerade namnet i Cloud Manager API/UI.
* [När du lägger till eller redigerar en pipeline för kodkvalitet](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) den **Beteende vid viktiga måttfel** visas inte längre.
* Oväntade rörliga variabelkonfigurationer orsakar inte längre fel i byggsteget.
