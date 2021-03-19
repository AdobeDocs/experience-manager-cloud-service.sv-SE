---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service 2020.10.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service 2020.10.0
feature: Versionsinformation
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 1%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.10.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.10.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.10.0 är 1 oktober 2020.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Miljösidan har fått en ny design.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Molnhanterarens byggbehållare har nu stöd för kompilering av projekt med antingen Java 8 eller Java 11. Stöd för Java 11 finns i Maven ToolChain System.

* Antalet miljövariabler per miljö har ökat till 200.

* Miljökortet på sidan Översikt visar nu upp till tre miljöer. Användare kan välja knappen **Visa alla** för att navigera till sammanfattningssidan för miljö och visa en tabell med en fullständig lista över miljöer.
Mer information finns i [Visningsmiljö](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).


### Felkorrigeringar {#bug-fixes-cloud-manager}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Knapparna Avbryt och Spara på sidan Redigering av icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.