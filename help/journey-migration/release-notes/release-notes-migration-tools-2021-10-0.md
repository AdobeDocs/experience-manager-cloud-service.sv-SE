---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.10.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.11.0
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2021.10.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html) om du vill se den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Cloud Acceleration Manager {#cam-release}

### Releasedatum {#release-date-cam}

Releasedatum för Cloud Acceleration Manager är 25 oktober 2021.

### Nyheter {#what-is-new-cam}

Cloud Acceleration Manager ger nu användare möjlighet att visa historiska BPA-rapporter i en trendlinjerapport. Med den här rapporten kan man se hur arbetet fortskrider i en grafisk representation som är enkel att ta del av. Mer information finns i [Använda Visa trendlinje](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#trendline-view-cam).

### Releasedatum {#release-date-october-cam}

Releasedatum för Cloud Acceleration Manager är 4 oktober 2021.

### Nyheter {#what-is-new-cam-oct}

Cloud Acceleration Manager ger nu användare möjlighet att visa BPA-rapporterna i en förhandsgranskning som går att skriva ut, vilket gör det enkelt att skriva ut eller skriva ut till PDF för att det ska vara enkelt att dela dem. Se Steg 6 och 7 i [Använda analyskort för metodtips](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#best-practices-analysis).


## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för innehållsöverföringsverktyget v1.6.0 är 4 oktober 2021.

### Nyheter {#what-is-new-ctt-oct}

* Förbättrat verktyg för användarmappning med en förenklad användarupplevelse, inklusive följande funktioner som listas nedan. Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html).
   * Testa anslutningen till API:t för användarhantering innan du kör användarmappningen
   * Hoppa över fel utan problem och fortsätt med aktiviteten Användarmappning
   * Användarmappning misslyckas inte längre om **åtkomsttoken** upphör att gälla efter 24 timmar. Användarmappning kan köras igen från den plats där den senast stoppades.

* Om du vill öka tillförlitligheten för verktyget Innehållsöverföring kan du importera innehåll till antingen Author-instansen eller Publish-instansen åt gången. Mer information finns i [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html).

* När versioner inkluderas inkluderas sökvägen `/var/audit` automatiskt för att migrera granskningshändelser.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa-latest}

Releasedatum för Best Practices Analyzer v2.1.20 är 5 oktober 2021.

### Nyheter {#what-is-new-bpa-oct}

* Möjlighet att identifiera och rapportera nodnamnets längd.

* Möjlighet att identifiera och rapportera om den totala indexstorleken.

* Möjlighet att upptäcka och rapportera resurser som saknar sin ursprungliga återgivning.
