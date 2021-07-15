---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.7.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.7.0
feature: Versionsinformation
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 673ac234f0e9bfc0f5e6878abf5d01d38cbe918f
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2021.6.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.7.0.

>[!NOTE]
>Om du vill visa den aktuella versionsinformationen för Adobe Experience Manager som en Cloud Service klickar du [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.7.0 är 15 juli 2021.
Nästa version är planerad till den 12 augusti 2021.

### Nyheter {#what-is-new}

* Kunderna kan nu använda Azul 8 och 11 JDK:er för sina Cloud Manager-byggprocesser och kan antingen välja att använda en av dessa JDK:er för verktygskedjor-kompatibla Maven-plugins *eller* hela Maven-processkörningen.

* IP för utgående utgång loggas nu i loggfilen för byggsteget.

* Scen- och produktionsmiljöer som kör gamla versioner av AEM rapporterar nu statusen&quot;Uppdatering tillgänglig&quot;.

* Det högsta antalet SSL-certifikat som stöds har ökat till 20 per program.

* Öka det högsta antalet domäner som kan konfigureras har ökat till 500 per miljö.

* Knapparna Hantera Git har fått namnet Åtkomst till Git-information och dialogrutan har uppdaterats visuellt.

### Felkorrigeringar {#bug-fixes}

* I vissa situationer var Förhandsvisning inte ett tillgängligt alternativ när en IP-Tillåtelselista skulle bindas till en miljö.

* Manuell navigering till sidan med körningsinformation för en körning som inte finns visade inte på något fel, bara en oändlig inläsningsskärm.

* Felmeddelandet som visades när det maximala antalet SSL-certifikat nåddes var inte till någon hjälp.

* I vissa fall kan det finnas en diskrepans i den version av produkten som visas på pipeline-kortet på översiktssidan.

* Guiden Lägg till program angav felaktigt att namnet inte kan ändras efter att det har skapats.

* I vissa situationer var Förhandsvisning inte ett tillgängligt alternativ när en IP-Tillåtelselista skulle bindas till en miljö.

### Kända fel {#known-issues}

Kunder som byter till Azul JDK bör vara medvetna om att inte alla befintliga program kompileras utan fel i Azul JDK. Vi rekommenderar att du testar lokalt innan du byter.

