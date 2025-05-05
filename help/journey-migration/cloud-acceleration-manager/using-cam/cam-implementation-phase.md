---
title: Implementeringsfas i Cloud Acceleration Manager
description: På den här sidan finns en översikt över implementeringsfasen i Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
feature: Migration
role: Admin
source-git-commit: f86d681c8f8cb6d602058ef30b648c53ff7bad69
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# Implementeringsfas i Cloud Acceleration Manager {#implementation-phase-cam}

Implementeringsfasen omfattar:

* [Lokal utveckling](#local-development)
* [Kodomfaktorisering](#code-refactoring)
* [Driftsättning av AEM as a Cloud Service](#aem-as-a-cloud-service-deployment)
* [Innehållsöverföring](#content-transfer)


Klicka på ditt projektkort så att du kan öppna projektstartsidan och navigera till avsnittet **Implementering**, vilket visas i följande bild.

![Projektstartsida - implementering](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Mer information finns i [Skapa och hantera ett projekt i Cloud Acceleration Manager](getting-started-cam.md#create-project).


## Använda lokalt utvecklingskort {#local-development}

Det lokala utvecklingskortet innehåller allt relevant innehåll som kan hjälpa dig att konfigurera den lokala AEM utvecklingsmiljön när du startar implementeringsfasen av migreringsresan.

Följ det här avsnittet för att utforska aktivitetskortet för lokal utveckling:

1. Klicka på **Visa** på kortet **Lokal utveckling**.

   ![Lokalt utvecklingskort](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. En innehållskarusell visar relevant information för den här fasen av migreringsresan.

   ![Lokal utvecklingsCarousel](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Använda omfaktoriseringskort {#code-refactoring}

Aktivitetskortet Code Refactoring innehåller all relevant information och markerar de områden för kodomfaktorisering som ska granskas och åtgärdas när man går över till AEM as a Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för kodkorrigering:

1. Klicka på **Granska** på aktivitetskortet **Kodkorrigering**.

   ![Kodomfaktoriseringskort](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. På sidan visas en lista med kodomfaktoriseringsaktiviteter ordnade efter allvarlighetsgrad. Du kan lära dig mer genom att klicka på de två markerade ikonerna.

   På sidan visas alla aspekter av kodomfaktorisering på tre olika flikar:

   * Ökning
   * Dispatcher
   * Testning

>[!NOTE]
>Granska innehållet på de här flikarna för att förstå några andra områden som inte omfattas av Best Practices Analyzer.

Fliken **Dispatcher** innehåller information om hur du strukturerar AEM as a Cloud Service Apache- och Dispatcher-konfigurationer och hur du validerar och kör den lokalt innan du distribuerar den till molnmiljöer. Det beskriver även felsökning i molnmiljöer.

![Fliken Dispatcher](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

Fliken **Testing** innehåller information om funktioner, Experience Audit och UI-testning.

![Testfliken](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Använda AEM as a Cloud Service distributionskort {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service driftsättningskort innehåller allt relevant innehåll som hjälper dig att driftsätta koden i AEM as a Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för AEM as a Cloud Service Deployment Card:

1. Klicka på **Visa** på aktivitetskortet för **AEM as a Cloud Service-distribution**.

   ![AEM as a Cloud Service-distribution - kort](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. En innehållskarusell visar relevant information för den här fasen av migreringsresan.

   ![AEM as a Cloud Service Deployment - carousel](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Använda innehållsöverföringskort {#content-transfer}

Med kortet för innehållsöverföring kan du starta och hantera innehållsöverföring från den aktuella AEM till AEM as a Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för innehållsöverföring:

1. Klicka på **Granska** på aktivitetskortet **Innehållsöverföring**.

   ![Innehållsöverföring - granskning](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Om du vill starta en innehållsöverföring måste du skapa en migreringsuppsättning. Klicka på **Skapa migreringsuppsättning**. Med en migreringsuppsättning kan innehåll överföras till AEM as a Cloud Service.

   ![Skapa migreringsuppsättning](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Ett migreringsset upphör att gälla efter en längre inaktivitetsperiod. Mer information finns i [Förfallotid för migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry).

   >[!NOTE]
   >Se [förutsättningarna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=sv-SE) och [bästa praxis och riktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=sv-SE) innan du använder verktyget Innehållsöverföring.

1. Hämta och installera verktyget Innehållsöverföring för att fylla i migreringsuppsättningen och slutföra extraheringsfasen av innehållsöverföringen. Granska [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=sv-SE) om du vill veta mer om hur du använder verktyget Innehållsöverföring.

1. Om du vill importera innehåll från migreringsuppsättningen till en miljö på AEM as a Cloud Service måste du påbörja ett intag. Navigera till **Inmatningsjobb** och klicka på **Nytt intag**. Granska [Inkluderande innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) så att du kan lära dig hur du slutför innehållsöverföringsfasen.

   ![Inmatningsjobb](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![Content Transfer Tool calculator](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in på Cloud Acceleration Manager och hur du använder implementeringsfasen är du redo att gå vidare till nästa steg i [Go Live Phase](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=sv-SE).
