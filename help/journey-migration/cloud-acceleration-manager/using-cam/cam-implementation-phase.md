---
title: Implementeringsfas i Cloud Acceleration Manager
description: Den här sidan innehåller en översikt över implementeringsfasen i Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 24331b974ded34ef949cc3d6fb157b124c145dee
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 2%

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
>Se [Skapa och hantera ett projekt i Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) om du vill veta mer.


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
   >Granska [krav](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) och [bästa praxis och riktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) innan du använder verktyget Innehållsöverföring.

1. Du måste hämta och installera verktyget för innehållsöverföring för att fylla i migreringsuppsättningen och slutföra extraheringsfasen av innehållsöverföringen. Granska [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) om du vill lära dig hur du använder verktyget Innehållsöverföring.

1. Om du vill importera innehåll från migreringsuppsättningen till en miljö på AEM as a Cloud Service måste du påbörja ett intag. Navigera till **Inmatningsjobb** och klicka på **Nytt intag**. Granska [Infoga innehåll i mål](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) om du vill lära dig hur du slutför överföringsfasen av innehåll.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

### Beräknar överföringstid för innehåll {#calculating}

En verktygskalkylator för innehållsöverföring har tillhandahållits för att beräkna hur lång tid det kan ta att slutföra innehållsöverföringsaktiviteten. Du kan använda storleksreglaget för innehållsdatabas för att välja den storlek som gäller för ditt projekt. Överföringstiden varierar för extraherings- och intagsfaserna.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

>[!NOTE]
>Dessa tider är bara uppskattningar. Faktor som nätverkshastigheter och tid att skala upp instanser har inte tagits med i dessa uppskattningar.

Om du vill beräkna storleken på AEM kan du köra rapporten Diskanvändning under `http://HOST:PORT/etc/reports/diskusage.html`.

Du kan också beräkna storleken på specifika databassökvägar med hjälp av `path` parameter, till exempel `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in i Cloud Acceleration Manager och hur du använder implementeringsfasen är du nu redo att gå vidare till nästa steg i [Go Live Phase](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
