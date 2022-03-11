---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2020.11.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2020.11.0
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 2%

---

# Versionsinformation om Cloud Manager i Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2020.11.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2020.11.0 är 12 november 2020.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Ett nytt menyalternativ **Lokal inloggning** är nu tillgängligt för användare från miljömenyalternativen på miljökortets och miljösammanfattningens sidor.
Se [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md#login-locally) för mer information.

* The **Lär dig** i Cloud Manager har uppdaterats med nya bilder i användargränssnittet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Inläsningen av beroenden som gjorts före körningen av bygget krävde hämtning av ett Maven-plugin-program.
* Länken från molnhanterarens sidfot för att välja ett språk navigerar nu till rätt plats.
* Ibland startar inte SonarQube-processen under kodskanningen. Detta identifieras nu automatiskt och ett omstartsförsök görs.
* Alla befintliga produktionspipelinjer aktiveras automatiskt med Experience Audit-steget.
