---
title: Versionsinformation för 2020.10.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service Release Notes för 2020.10.0.'
translation-type: tm+mt
source-git-commit: eb4a567e7ae2aac7260aae28e2b91b088e42f945
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] Cloud Servicen 2020.10.0.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.10.0 är 2 oktober 2020.

### What is new in [!DNL Cloud Manager] {#what-is-new-cm}

* Miljösidan har fått en ny design.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Molnhanterarens byggbehållare har nu stöd för kompilering av projekt med antingen Java 8 eller Java 11. Stöd för Java 11 finns i Maven ToolChain System.

* Antalet miljövariabler per miljö har ökat till 200.

* Miljökortet på sidan Översikt visar nu upp till tre miljöer. Användare kan välja knappen **Visa alla** för att navigera till sammanfattningssidan för miljö och visa en tabell med en fullständig lista över miljöer.
Mer information finns i [Visningsmiljön](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) .

### Bug Fixes {#bug-fixes-cloud-manager}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Knapparna Avbryt och Spara på sidan Redigering av icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.
