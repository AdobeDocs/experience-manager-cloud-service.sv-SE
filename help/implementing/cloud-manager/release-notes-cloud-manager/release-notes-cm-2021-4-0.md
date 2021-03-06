---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.4.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.4.0
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.4.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.4.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.4.0 är 8 april 2021.
Nästa version är planerad till 6 maj 2021.

### Nyheter {#what-is-new-april}

* Gränssnittsuppdateringar i arbetsflödena för Lägg till och redigera program gör dem mer intuitiva.

* En användare med nödvändig behörighet kan nu skicka slutpunkten för e-handeln via användargränssnittet.

* Miljövariabler kan nu omfatta en viss tjänst, antingen författare eller publicerad. Kräver AEM `2021.03.5104.20210328T185548Z` eller senare.

* The **Hantera Git** knappen visas på pipelines-kortet även när inga rörledningar har konfigurerats.

* Den version av AEM projekttyp som används av Cloud Manager har uppdaterats till version 27.

* Projekt i Adobe I/O Developer Console som har skapats i Cloud Manager kan inte längre redigeras eller tas bort oavsiktligt.

* När en användare lägger till en ny miljö informeras de om att när en miljö väl har skapats kan den inte flyttas till en annan region.

* Miljövariabler kan nu omfatta en viss tjänst, antingen författare eller publicerad. Kräver AEM version 2021.03.5104.20210328T185548Z eller senare.

* Felmeddelandet när en pipeline startades när en miljö togs bort har klargjorts.

* OSGi-paket som tillhandahålls av Eclipse-projekt är nu undantagna från regeln `CQBP-84--dependencies`.

### Felkorrigeringar {#bug-fixes-cm-april}

* När du redigerar Experience Audit-sidan för en pipeline ska du ange en indatasökväg som börjar med ett snedstreck `( / )` kommer inte längre att resultera i att steget fastnar i väntande status.

* När en ny produktionspipeline skapas granskades inte standardstartsidan om användaren inte lägger till någon åsidosättning av innehållsgranskning.

* Problem med `CloudServiceIncompatibleWorkflowProcess` hade fel allvarlighetsgrad i CSV-filen för den hämtningsbara utgåvan.

* The `Runmode` kontrollen genererade falskt positiva värden på noder som inte finns i mappen.
