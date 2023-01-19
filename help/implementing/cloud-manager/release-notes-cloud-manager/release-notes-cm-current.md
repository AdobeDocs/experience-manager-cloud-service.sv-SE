---
title: Versionsinformation om Cloud Manager 2023.1.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2024.1.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.1.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.1.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.1.0 i AEM as a Cloud Service är 19 januari 2023. Nästa version är planerad till den 16 februari 2023.

## Nyheter {#what-is-new}

* Användbarhetsförbättringarna var att uppdatera markörstilar som skiljer mellan var användarna kan vidta åtgärder och standardpekaren.

* I listor över miljöer och pipeline-körningar kan du nu komma åt information genom att klicka på den enskilda raden.

* Testrapporter för anpassat användargränssnitt kopieras nu till molnhanterarens lagringsutrymme och kan nås via API-anrop till molnhanteraren.

* Användare kan nu växla mellan GoLive-widgetlägen med vänster-höger-pilar.

   ![GoLive-widgetövergångar](assets/go-live-transitions.gif)

* Självbetjäning [skapa HIPAA-aktiverade program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) är nu möjligt när motsvarande berättiganden och behörigheter är tillgängliga.

## Felkorrigeringar {#bug-fixes}

* Cloud Manager förhindrar att två pipelinekörningar startar samtidigt (eller nästan samtidigt), vilket undviker pipeline-fel.
