---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2022.01.0
description: Det här är versionsinformationen för Cloud Manager i AEM as a Cloud Service release 2022.01.0.
feature: Release Information
exl-id: 2dfdc943-0518-40ea-8712-1dabb97eeaa9
source-git-commit: 6e394aaabcb123aea53fba49684aaade3e6c87a6
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager i Adobe Experience Manager as a Cloud Service 2022.01.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2022.01.0.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2022.01.0 är 20 januari 2022. Nästa version är planerad till den 10 februari 2022.

## Nyheter {#what-is-new}

* Cloud Manager kommer att [undvika att återskapa kodbasen när den upptäcker att samma Git-implementering används](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) i flera fullständiga pipeline-körningar.
* För att få åtkomst till AEM måste du **Distributionshanteraren** produktprofil. Användare utan den här profilen ser en inaktiverad knapp i användargränssnittet.
* Gränssnittet tillåter inte konfiguration av pipeline i gränssnittet för ett program där Sites inte är aktiverat som en lösning.
* När du genererar ett Git-lösenord visas förfallodatumet.

## Felkorrigeringar {#bug-fixes}

* Null-pekarundantag som påträffades i vissa frontendsdistributioner har korrigerats.
* Miljövariabler kan nu läggas till, uppdateras och tas bort när en miljö kör en gammal version av AEM.
* Steget för att skapa bilder markeras inte längre som FEL för rörledningar som i vissa sällsynta fall använde det schemalagda steget.
* För program med endast en databas visas databasens namn på körningsskärmen för pipeline.
