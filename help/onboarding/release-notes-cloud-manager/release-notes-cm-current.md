---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.4.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.4.0
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
translation-type: tm+mt
source-git-commit: 69694f2067c53667803d38bbf7bc752f3b3afac6
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2021.4.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.4.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.4.0 är 8 april 2021.
Nästa version är planerad till 6 maj 2021.

### Nyheter {#what-is-new-april}

* Gränssnittsuppdateringar i arbetsflödena för Lägg till och redigera program gör dem mer intuitiva.

* En användare med nödvändig behörighet kan nu skicka slutpunkten för e-handeln via användargränssnittet.

* Miljövariabler kan nu omfatta en viss tjänst, antingen författare eller publicerad. Kräver AEM version `2021.03.5104.20210328T185548Z` eller senare.

* Knappen **Hantera Git** visas på pipelines-kortet även när inga rörledningar har konfigurerats.

* Den version av AEM projekttyp som används av Cloud Manager har uppdaterats till version 27.

* Projekt i Adobe I/O Developer Console som har skapats i Cloud Manager kan inte längre redigeras eller tas bort oavsiktligt.

* När en användare lägger till en ny miljö informeras de om att när en miljö väl har skapats kan den inte flyttas till en annan region.

* Miljövariabler kan nu omfatta en viss tjänst, antingen författare eller publicerad. Kräver AEM version 2021.03.5104.20210328T185548Z eller senare.

* Felmeddelandet när en pipeline startades när en miljö togs bort har klargjorts.

* OSGi-paket som tillhandahålls av Eclipse-projekt undantas nu från regeln `CQBP-84--dependencies`.

### Felkorrigeringar {#bug-fixes-cm-april}

* När du redigerar Experience Audit-sidan för en pipeline kommer en indatasökväg som börjar med ett snedstreck `( / )` inte längre att resultera i att steget fastnar i väntande status.

* När en ny produktionspipeline skapas granskades inte standardstartsidan om användaren inte lägger till någon åsidosättning av innehållsgranskning.

* Problem för `CloudServiceIncompatibleWorkflowProcess` hade fel allvarlighetsgrad i den hämtningsbara CSV-filen för utgåvan.

* `Runmode`-kontrollen genererade falskt positiva värden på noder som inte finns i mappen.