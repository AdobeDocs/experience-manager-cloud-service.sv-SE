---
title: Implementeringsfas i Cloud Acceleration Manager
description: Den här sidan innehåller en översikt över implementeringsfasen i Cloud Acceleration Manager.
source-git-commit: 4041e3fd9a479a64ed38e2bf1a6251fda39e55c2
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Implementeringsfas i Cloud Acceleration Manager {#implementation-phase-cam}

Implementeringsfasen omfattar:

* [Lokal utveckling](#local-development)
* [Omstrukturering av kod](#code-refactoring)
* [AEM som Cloud Service](#aem-as-a-cloud-service-deployment)
* [Innehållsöverföring](#content-transfer)


Klicka på projektkortet för att öppna projektstartsidan och navigera till avsnittet **Implementering**, som visas i bilden nedan.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Mer information finns i [Skapa och hantera ett projekt i Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project).


## Använda lokalt utvecklingskort {#local-development}

Det lokala utvecklingskortet tillhandahåller allt relevant innehåll som hjälper dig att konfigurera den lokala AEM utvecklingsmiljön när du påbörjar implementeringsfasen av migreringsresan.

Följ det här avsnittet för att utforska aktivitetskortet för lokal utveckling:

1. Klicka på knappen **Visa** på kortet **Lokal utveckling**.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. En innehållskarusell med relevant information för den här fasen av migreringsresan visas.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## Använda omfaktoriseringskort {#code-refactoring}

Aktivitetskortet Code Refactoring ger all relevant information och markerar de områden för kodomfaktorisering som du behöver granska när du går till AEM som en Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för kodkorrigering:

1. Klicka på knappen **Granska** på aktivitetskortet **Kodkorrigering**.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. På sidan visas en lista med kodomfaktoriseringsaktiviteter ordnade efter allvarlighetsgrad. Du kan lära dig mer genom att klicka på de två markerade ikonerna.

   >[!NOTE]
   >Granska dessutom innehållet på flikarna på sidan för att få reda på ytterligare områden som inte omfattas av Best Practices Analyzer.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## Använda AEM som distributionskort för Cloud Service {#aem-as-a-cloud-service-deployment}

AEM som driftsättningskort för Cloud Service innehåller allt relevant innehåll som hjälper dig att distribuera koden till AEM som en Cloud Service.

Följ det här avsnittet för att utforska AEM som aktivitetskort för driftsättningskort för Cloud Service:

1. Klicka på knappen **Visa** på **AEM som aktivitetskort för Cloud Service Deployment**.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. En innehållskarusell med relevant information för den här fasen av migreringsresan visas.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Använda innehållsöverföringskort {#content-transfer}

Aktivitetskortet för innehållsöverföring innehåller riktlinjer och överväganden som ska granskas när du använder verktyget Innehållsöverföring för att flytta innehåll från den aktuella AEM till AEM som en Cloud Service.

Följ det här avsnittet för att utforska aktivitetskortet för innehållsöverföring:

1. Klicka på knappen **Visa** på aktivitetskortet **Innehållsöverföring**.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. En innehållskarusell med relevant information för den här fasen av migreringsresan visas.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >Granska [förutsättningarna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) och [god praxis och riktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) innan du använder verktyget Innehållsöverföring.

### Aktivitet för verktyget Innehållsöverföring beräknas {#calculating}

En ny verktygskalkylator för innehållsöverföring har tillhandahållits för att beräkna hur lång tid det kan ta att slutföra innehållsöverföringsaktiviteten. Du kan använda storleksreglaget för innehållsdatabas för att välja den storlek som gäller för ditt projekt. Överföringstiden varierar för extraherings- och intagsfaserna.

Du kan beräkna storleken på AEM databas genom att köra rapporten Diskanvändning under `http://HOST:PORT/etc/reports/diskusage.html`.

Du kan också beräkna storleken på specifika databassökvägar med parametern `path`, till exempel `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in i Cloud Acceleration Manager och hur du använder implementeringsfasen är du nu redo att gå vidare till nästa steg, [Använda Go Live Phase](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
