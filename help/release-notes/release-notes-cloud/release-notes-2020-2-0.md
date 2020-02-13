---
title: Versionsinformation för version 2020.2.0
description: Versionsinformation för version 2020.2.0
translation-type: tm+mt
source-git-commit: 157809fb4aacf45358db6412dea04398a7f12495

---


# Versionsinformation för AEM som molntjänst 2020.2.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som en molntjänst 2020.2.0.

Releasedatum är 13 februari 2020.

## Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager version 2020.2.0.

### Nyheter {#what-is-new}

* Adobe Experience Managers arkivtypsversion har uppdaterats till version 22.
* Scen- och produktionsmiljöerna i sandbox-/demoprogrammen kan nu uppdateras via användargränssnittet i Cloud Manager.
* URL:er som används i Experience Cloud-meddelanden har optimerats för att undvika en extra omdirigering.
* Körningssteg för pipeline som nådde tidsgränsen anger nu uttryckligen detta.
* Kodsökningssteget har nu en hämtningsbar logg.
* Kalkylbladet som innehåller problem som upptäcks vid kodskanning har nu en kolumn med en länk till dokumentationen för den specifika regeln.

### Felkorrigeringar {#bug-fixes}

* Säkerhetsprofiler för webbläsare kan ibland förhindra att vissa knappar i pipeline-körningsskärmen fungerar som de ska.
* Länkarna Översikt, Miljö och Aktivitet var ibland tillgängliga på landningssidan för Cloud Manager.
* Vissa fel vid distributionen kan felaktigt förhindra att nya rörledningar skapas.