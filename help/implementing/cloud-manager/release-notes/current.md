---
title: Versionsinformation om Cloud Manager 2023.4.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.4.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---


# Versionsinformation om Cloud Manager 2023.4.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.4.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.4.0 i AEM as a Cloud Service är 13 april 2023. Nästa version är planerad till den 11 maj 2023.

## Nyheter {#what-is-new}

* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) har uppdaterats till version 41.

## Felkorrigeringar {#bug-fixes}

* När en [certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) upphör, [domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md) och [IP-tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) som är kopplade till certifikatet kommer inte längre att tas bort från CDN.  I sådana fall kan webbplatsen fortfarande nås.
* Molnhanterarens användargränssnitt innehåller mer synliga avancerade varningar om att [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) upphör snart att gälla.
* En sällsynt situation har korrigerats där kunderna inte kunde skapa en ny miljö eller ta bort en miljö.
