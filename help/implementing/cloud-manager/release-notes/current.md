---
title: Versionsinformation om Cloud Manager 2023.5.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.5.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4340b957cea86452f916ab615b383aabacc21676
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.5.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.5.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.5.0 i AEM as a Cloud Service är 11 maj 2023. Nästa version är planerad till den 8 juni 2023.

## Nyheter {#what-is-new}

* Stöd för produkt-, funktions- och gränssnittstestning har utökats till [testning av rörledningar som inte är avsedda för produktion.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
* Förutom att aktivera testning uppströms, [Stöd för gränssnittstestning har utökats till att omfatta även Cypress-testning.](/help/implementing/cloud-manager/ui-testing.md)
* [Självbetjäningskopia](/help/implementing/developing/tools/content-copy.md) är nu tillgängligt från en högre till en lägre miljö via användargränssnittet i Cloud Manager.
* Valideringssteget för pipeline-körning har förbättrats för att validera tillståndet för replikeringsköerna tidigt i körningsprocessen. Detta garanterar att distributionsstegen inte påverkas av blockerade köer som bör adresseras av AEM administratörsanvändare direkt i redigeringsmiljön.

## Felkorrigeringar {#bug-fixes}

* Miljöskapande misslyckas inte längre när flerbytetecken används i miljöns namn.
