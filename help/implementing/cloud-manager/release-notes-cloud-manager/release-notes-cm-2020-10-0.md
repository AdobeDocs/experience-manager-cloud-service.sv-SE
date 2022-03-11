---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2020.10.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2020.10.0
feature: Release Information
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Versionsinformation om Cloud Manager i Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2020.10.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2020.10.0 är 1 oktober 2020.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Miljösidan har fått en ny design.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Molnhanterarens byggbehållare har nu stöd för kompilering av projekt med antingen Java 8 eller Java 11. Stöd för Java 11 finns i Maven ToolChain System.

* Antalet miljövariabler per miljö har ökat till 200.

* Miljökortet på sidan Översikt visar nu upp till tre miljöer. Användarna kan välja **Visa alla** för att navigera till miljösammanfattningssidan för att visa en tabell med en fullständig lista över miljöer.
Se [Visningsmiljö](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) för mer information.


### Felkorrigeringar {#bug-fixes-cloud-manager}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Knapparna Avbryt och Spara på sidan Redigering av icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.
