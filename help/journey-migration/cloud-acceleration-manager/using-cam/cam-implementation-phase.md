---
title: Implementeringsfas i Cloud Acceleration Manager
description: Den här sidan innehåller en översikt över implementeringsfasen i Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: cba5dccd3b66220bbcd6d3b4dd5298702902b0e5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Implementeringsfas i Cloud Acceleration Manager {#implementation-phase-cam}

Implementeringsfasen omfattar:

* [Lokal utveckling](#local-development)
* [Omstrukturering av kod](#code-refactoring)
* [AEM as a Cloud Service driftsättning](#aem-as-a-cloud-service-deployment)
* [Innehållsöverföring](#content-transfer)


Klicka på projektkortet för att öppna projektstartsidan och navigera till **Implementering** som visas i figuren nedan.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Se [Skapa och hantera ett projekt i Cloud Acceleration Manager](getting-started-cam.md#create-project) om du vill veta mer.


## Använda lokalt utvecklingskort {#local-development}

Det lokala utvecklingskortet tillhandahåller allt relevant innehåll som hjälper dig att konfigurera den lokala AEM utvecklingsmiljön när du påbörjar implementeringsfasen av migreringsresan.

Följ det här avsnittet för att utforska aktivitetskortet för lokal utveckling:

1. Klicka på **Visa** från **Lokal utveckling** kort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. En innehållskarusell visar relevant information för den här fasen av migreringsresan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Använda omfaktoriseringskort {#code-refactoring}

Aktivitetskortet Code Refactoring innehåller all relevant information och markerar de områden för kodomfaktorisering som du behöver granska och lösa när du går till AEM as a Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för kodkorrigering:

1. Klicka på **Granska** från **Kodomfaktorisering** aktivitetskort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. På sidan visas en lista med kodomfaktoriseringsaktiviteter ordnade efter allvarlighetsgrad. Du kan lära dig mer genom att klicka på de två markerade ikonerna.

   På sidan visas alla aspekter av kodomfaktorisering på tre olika flikar:

   * Översikt
   * Dispatcher
   * Testning

>[!NOTE]
>Granska innehållet på de här flikarna för att få en förståelse för ytterligare områden som inte omfattas av Best Practices Analyzer.

The **Dispatcher** På -fliken finns information om hur du strukturerar de AEM as a Cloud Service Apache- och Dispatcher-konfigurationerna samt om hur du validerar och kör dem lokalt innan du distribuerar dem till molnmiljöer. Det beskriver även felsökning i molnmiljöer.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

The **Testning** -fliken innehåller information om funktioner, Experience Audit och UI-testning.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Använda AEM as a Cloud Service distributionskort {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service driftsättningskort innehåller allt relevant innehåll som hjälper dig att distribuera koden till AEM as a Cloud Service.

Följ det här avsnittet för att utforska AEM aktivitetskort för as a Cloud Service distributionskort:

1. Klicka på **Visa** från **AEM as a Cloud Service driftsättning** aktivitetskort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. En innehållskarusell visar relevant information för den här fasen av migreringsresan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Använda innehållsöverföringskort {#content-transfer}

Med kortet för innehållsöverföring kan du starta och hantera innehållsöverföring från den aktuella AEM till AEM as a Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för innehållsöverföring:

1. Klicka på **Granska** från **Innehållsöverföring** aktivitetskort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Om du vill starta en innehållsöverföring måste du skapa en migreringsuppsättning. Klicka på **Skapa migreringsuppsättning**. Med en migreringsuppsättning kan innehåll överföras till AEM as a Cloud Service.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Observera att ett migreringsset kommer att upphöra efter en längre inaktivitetsperiod. Granska [Förfallotid för migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) för mer information.

   >[!NOTE]
   >Granska [krav](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html) och [bästa praxis och riktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) innan du använder verktyget Innehållsöverföring.

1. Du måste hämta och installera verktyget för innehållsöverföring för att fylla i migreringsuppsättningen och slutföra extraheringsfasen av innehållsöverföringen. Granska [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html) om du vill lära dig hur du använder verktyget Innehållsöverföring.

1. Om du vill importera innehåll från migreringsuppsättningen till en miljö på AEM as a Cloud Service måste du påbörja ett intag. Navigera till **Inmatningsjobb** och klicka på **Nytt intag**. Granska [Infoga innehåll i mål](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) om du vill lära dig hur du slutför överföringsfasen av innehåll.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in i Cloud Acceleration Manager och hur du använder implementeringsfasen är du nu redo att gå vidare till nästa steg i [Go Live Phase](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
