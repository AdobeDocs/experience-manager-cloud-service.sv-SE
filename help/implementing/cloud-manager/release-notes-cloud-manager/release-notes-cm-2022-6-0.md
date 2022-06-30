---
title: Versionsinformation om Cloud Manager 2022.6.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2022.6.0 i AEM as a Cloud Service.
feature: Release Information
source-git-commit: 5200ee315ad88dae4b52c0ea904489e73f62a8a0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2022.6.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

På den här sidan visas versionsinformation för Cloud Manager 2022.6.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2022.6.0 i AEM as a Cloud Service är 9 juni 2022. Nästa version är planerad till 30 juni 2022.

## Nyheter {#what-is-new}

* Molnhanterarens gränssnitt tillåter nu [självbetjäning för innehållsåterställning](/help/operations/backup.md) till ett välkänt tillstånd i AEM molnmiljö.
   * Den här funktionen kommer att introduceras stegvis under de veckor som följer efter version 2022.06.0.
* Ett nytt välkomstkort på Cloud Managers landningssida ger användarna snabb tillgång till självstudiekurser och förloppsstatistik för klientorganisationen.
   * Den här funktionen kommer att introduceras stegvis under veckan efter version 2022.06.0.
* Användare med nödvändig behörighet kan komma åt en ny [Licenspanelen](/help/implementing/cloud-manager/license-dashboard.md) på landningssidan för Cloud Manager för att visa information om berättiganden som är tillgängliga för klientorganisationen.
   * AEM Sites är den första lösningen för vilken tillgänglighet och användning levereras via kontrollpanelen Cloud Manage.
   * Den här funktionen kommer att introduceras stegvis under de veckor som följer efter version 2022.06.0.
* [New Relic subaccount and self-service user management](/help/implementing/cloud-manager/user-access-new-relic.md) är nu tillgängligt via användargränssnittet i Cloud Manager.
   * Den här funktionen kommer att introduceras stegvis under de veckor som följer efter version 2022.06.0.
* Nu finns det en ny Go Live-widget på startsidan i Cloud Service-produktionsprogrammen som är till hjälp när du vill skapa en lyckad upplevelse.
* [Artefakter kan nu återanvändas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) när Git-spegling används.

## API-ändringar {#api-changes}

* The [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API har tagits bort och [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) ska användas istället.
   * `List Programs` fortsätter att fungera, men användningen genererar varningsmeddelanden i loggar.
   * Det kommer inte längre att stödjas efter tre månader.

