---
title: Versionsinformation om Cloud Manager 2023.6.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.6.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 80a5f58119dc304161d324491cd65c50e981ccd4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.6.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.6.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.6.0 i AEM as a Cloud Service är 8 juni 2023. Nästa version är planerad till den 6 juli 2023.

## Nyheter {#what-is-new}

* När du skapar en ny [program eller miljö,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) Namnet är nu begränsat till att endast innehålla alfanumeriska tecken och en begränsad uppsättning specialtecken.
* När en [Produktionspipeline.](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) En bekräftelsedialogruta visas nu i steget Godkänn.
* För **[Funktionstester från kunder](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** och **[Testning av anpassat användargränssnitt](/help/implementing/cloud-manager/ui-testing.md)** pipeline-steg, en ny `INCOMPLETE` status är nu möjlig, vilket anger att sådana tester inte fanns och därför inte utfördes.
   * I sådana fall misslyckas inte rörledningen och fortsätter till nästa steg.

## Felkorrigeringar {#bug-fixes}

* The [pipeline för konfiguration av webbnivå](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) är inte längre felaktigt aktiverade för program som bara innehåller resurser.
* Mer robust validering lades till för att förhindra vissa typer av fel under miljöetableringen.
