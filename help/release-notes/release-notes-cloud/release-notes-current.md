---
title: Adobe Experience Manager som Cloud Service Versionsinformation för 2020.7.0
description: Versionsinformation om Experience Manager för 2020.7.0
translation-type: tm+mt
source-git-commit: 74abf1c4cc6ae449a81e3e40d073bfcb23b056e8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Versionsinformation för AEM som Cloud Service 2020.7.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.7.0.

## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM som en Cloud Service version 2020.7.0.

### Releasedatum {#release-date}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.7.0 är 9 juli 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Miljösidan har gjorts om.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Molnhanterarens byggbehållare har nu stöd för både Java 8 och Java 11.

### Bug Fixes {#bug-fixes-cm}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Alternativen **Avbryt** och **Spara** på redigeringssidan för icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.