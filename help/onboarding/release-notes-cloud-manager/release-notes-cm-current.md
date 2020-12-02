---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service 2020.11.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service 2020.11.0
translation-type: tm+mt
source-git-commit: 727dfd1d16a80620fba6db00289021ee5efae0fc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 2%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.11.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.11.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.11.0 är 12 november 2020.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Ett nytt menyalternativ **Lokal inloggning** är nu tillgängligt för användare från miljömenyalternativen på miljökortets och miljösammanfattningens sidor.
Mer information finns i [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md##login-locally).

* Fliken **Lär dig** i Cloud Manager har uppdaterats med nya bilder i användargränssnittet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Inläsningen av beroenden som gjorts före körningen av bygget krävde hämtning av ett Maven-plugin-program.
* Länken från molnhanterarens sidfot för att välja ett språk navigerar nu till rätt plats.
* Ibland startar inte SonarQube-processen under kodskanningen. Detta identifieras nu automatiskt och ett omstartsförsök görs.
* Alla befintliga produktionspipelinjer aktiveras automatiskt med Experience Audit-steget.