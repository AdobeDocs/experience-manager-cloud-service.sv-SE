---
title: Versionsinformation om Cloud Manager 2022.3.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2022.3.0 i AEM as a Cloud Service.
feature: Release Information
source-git-commit: 437be8c82a4dee6c9e56af09afa7e9048c8cb3c0
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# Versionsinformation om Cloud Manager 2022.3.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager 2022.3.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2022.3.0 i AEM as a Cloud Service 10 mars 2022. Nästa version är planerad till den 7 april 2022.

## Nyheter {#what-is-new}

* Åtkomst AEM miljöloggen kan göras med rollen Utvecklare.

## Felkorrigeringar {#bug-fixes}

* En delmängd av Git-databaser som skapats manuellt hade ett felaktigt namnvärde, vilket hindrade återanvändningsfunktionen för build-felaktigheter från att vara effektiv. Namnen på dessa databaser har ändrats och användarna ser det korrigerade namnet i Cloud Manager API/UI.
* Artefakter från rörledningar som inte är avsedda för produktion återanvänds på ett olämpligt sätt i rörledningar för hela produktionen.
* När du lägger till eller redigerar en pipeline för kodkvalitet visas inte längre alternativen för att hantera måttfel.
* En del oväntade pipelinevariabelkonfigurationer kan orsaka i byggsteget.
