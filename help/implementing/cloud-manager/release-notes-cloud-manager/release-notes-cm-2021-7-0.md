---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.7.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.7.0
feature: Release Information
source-git-commit: 3542d5a6b89b8673444786e3f9062dae0d315946
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 1%

---

# Versionsinformation om Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.7.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.7.0.

>[!NOTE]
>Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html) om du vill se den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.7.0 är 15 juli 2021.


### Nyheter {#what-is-new}

* Kunderna kan nu använda Azul 8 och 11 JDK:er för sina Cloud Manager-byggprocesser och kan antingen välja att använda en av dessa JDK:er för verktygskedjor-kompatibla Maven-plugins *eller* hela Maven-processkörningen.

* IP för utgående utgång loggas nu i loggfilen för byggsteget.

* Scen- och produktionsmiljöer som kör äldre versioner av AEM rapporterar nu statusen **Tillgänglig uppdatering**.

* Det högsta antalet SSL-certifikat som stöds har ökat till 20 per program.

* Det maximala antalet domäner som kan konfigureras har ökat till 500 per miljö.

* Knapparna **Hantera Git** har ändrats till **Använd Git-information** och dialogrutan har uppdaterats visuellt.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 28.

### Felkorrigeringar {#bug-fixes}

* I vissa situationer var Förhandsgranskning inte ett tillgängligt alternativ när en IP-Tillåtelselista skulle bindas till en miljö.

* Manuell navigering till sidan med körningsinformation för en körning som inte finns visade inte på något fel, bara en oändlig inläsningsskärm.

* Felmeddelandet som visades när det maximala antalet SSL-certifikat nåddes var inte till någon hjälp.

* I vissa fall kan det finnas en diskrepans i releaseversionen som visas på pipeline-kortet på sidan **Översikt**.

* Guiden Lägg till program angav felaktigt att namnet inte kan ändras efter att det har skapats.

### Kända fel {#known-issues}

Kunder som byter till Azul JDK bör vara medvetna om att inte alla befintliga program kompileras utan fel i Azul JDK. Vi rekommenderar att du testar lokalt innan du byter.

