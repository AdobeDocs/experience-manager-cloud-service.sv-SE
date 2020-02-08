---
title: Migrera till molntjänsten från Adobe Experience Manager 6.x
description: Migrera till molntjänsten från Adobe Experience Manager 6.x
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Gå över till Adobe Experience Manager Assets som en molntjänst {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## Om migreringsverktyget {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

Med migreringsverktyget kan du uppnå följande:

* Konvertera befintliga arbetsflödesmodeller till bearbetningsprofiler som fungerar med tjänsten Resurser Compute.
* Ta bort steg som inte stöds från arbetsflödesmodellerna.
* Inaktivera startprogram för arbetsflöden.
* Sammanfoga konfigurationerna, efter användarbekräftelse/validering, i den befintliga källkoden.

Migreringsverktyget skapar bearbetningsprofiler i en Maven-modul som användare kan använda på följande två sätt:

* Sammanfoga i ett av deras befintliga projekt.
* Lägg till modulen som en ny undermodul.

Migreringsverktyget ger en rapport över de ändringar som gjorts och information om ändringarna.

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## Migrera innehåll till en ny distribution {#content-migration-across-deployments}
