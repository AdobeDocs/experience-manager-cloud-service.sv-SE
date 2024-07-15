---
title: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.7.0
description: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.7.0
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 1%

---

# Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.7.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.7.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.30 är 27 juli 2022.

### Nyheter {#what-is-new-bpa}

* BPA kan nu identifiera och rapportera den totala flyttbara Lucene-indexstorleken, som är Total Lucene-index exklusive `/oak:index/lucene` och `/oak:index/damAssetLucene`.
* Ett nytt mönster har lagts till i BPA för att identifiera och rapportera användningen av den anpassade i18n-ordlistan. Translator.html är inte tillgängligt i AEM as a Cloud Service och en anpassad i18n-ordlista måste distribueras från Git via Cloud Manager CI/CD-pipeline.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA rapporterade om saknade ursprungliga återgivningar för innehållsfragment. Eftersom innehållsfragment inte har några återgivningar hoppas den här kontrollen över innehållsfragment.
* Alternativet att filtrera ACS Commons-resultat saknades i BPA-gränssnittet. Den här har åtgärdats.

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v2.0.12 är 19 juli 2022.

### Nyheter {#what-is-new-ctt}

* Användare som är inloggade via LDAP kan nu köra funktionerna Kontrollera storlek och Användarmappning i CTT.
* För att hjälpa till att felsöka SSL-/TLS-anslutningsproblem under extraheringar kan användarna nu aktivera SSL-loggning.
* För att underlätta felsökningen av källanslutningsproblem skrivs nu underdomännamn ut i loggarna när anslutningen till Azure misslyckas.
* För att felsöka problem under förkopiering läggs AzCopy-loggar nu till i extraheringsloggarna när förkopieringen misslyckas.
* För att undvika inaktuella resultat av typen Kontrollera storlek kan användare bara köra Kontrollera storlek igen när en tidigare kontrollstorlek har slutförts.

### Felkorrigeringar {#bug-fixes-ctt}

* Tidigare extraheringsloggar visas efter att en migreringsuppsättning har tagits bort och återskapats. Den här har åtgärdats.
* Åtgärdsknappen Visa förlopp var inte tillgänglig för migreringsuppsättningar med statusen STOPPED. Den här har åtgärdats.
* Åtgärdsknappen Ta bort var inte tillgänglig för migreringsuppsättningar med en extraheringsnyckel som har gått ut. Den här har åtgärdats.
* Flera gränssnittsfel har åtgärdats.

## Cloud Acceleration Manager {#cam-release}

### Releasedatum {#release-date-cam}

Releasedatum för Cloud Acceleration Manager är 15 juli 2022.

### Nyheter {#what-is-new-cam}

* Cloud Acceleration Manager ger nu användare möjlighet att hämta migreringstoken manuellt för att kunna starta ett intag när automatisk hämtning misslyckas. Automatisk hämtning kan misslyckas om kunderna har konfigurerat en IP-lista som blockerar CAM eller om en icke-admin-användare försöker starta ett intag. Mer information finns i [Felsökning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting).
* Långa tabeller på sidan Migreringskomplexitet är nu komprimerbara för att underlätta användningen.
