---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.7.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.7.0
feature: Release Information
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.7.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.7.0.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v2.0.12 är 19 juli 2022.

### Nyheter {#what-is-new-ctt}

* Användare som är inloggade via LDAP kan nu köra funktionerna Kontrollera storlek och Användarmappning i CTT.
* För att hjälpa till att felsöka SSL-/TLS-anslutningsproblem under extraheringar kan användarna nu aktivera SSL-loggning.
* För att underlätta felsökningen av källanslutningsproblem skrivs nu underdomännamn ut i loggarna när anslutningen till Azure misslyckas.
* För att felsöka problem under förkopiering läggs AzCopy-loggar nu till i extraheringsloggarna när förkopieringen misslyckas.
* För att undvika inaktuella resultat av typen Kontrollera storlek kan användarna köra kontrollstorlek igen först när en tidigare kontrollstorlek är klar.

### Felkorrigeringar {#bug-fixes-ctt}

* Tidigare extraheringsloggar visas efter att en migreringsuppsättning har tagits bort och återskapats. Den här har åtgärdats.
* Åtgärdsknappen Visa förlopp var inte tillgänglig för migreringsuppsättningar med statusen STOPPED. Den här har åtgärdats.
* Åtgärdsknappen Ta bort var inte tillgänglig för migreringsuppsättningar med en extraheringsnyckel som har gått ut. Den här har åtgärdats.
* Flera gränssnittsfel har åtgärdats.

## Cloud Acceleration Manager {#cam-release}

### Releasedatum {#release-date-cam}

Releasedatum för Cloud Acceleration Manager är 15 juli 2022.

### Nyheter {#what-is-new-cam}

* Molnaccelerationshanteraren ger nu användare möjlighet att hämta migreringstoken manuellt för att kunna påbörja ett intag när automatisk hämtning misslyckas. Automatisk hämtning kan misslyckas om kunderna har konfigurerat en IP-lista som blockerar CAM eller om en icke-admin-användare försöker starta ett intag. Se [Felsökning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) för mer information.
* Långa tabeller på sidan Migreringskomplexitet är nu komprimerbara för att underlätta användningen.

