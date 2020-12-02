---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.7.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.7.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.7.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.7.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.7.0 är 9 juli 2020.

## Nyheter {#whats-new-cloud-manager}

* Miljösidan har gjorts om.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Antalet miljövariabler per miljö har ökat till 200.

* Molnhanterarens pipelines har nu stöd för kundspecifika variabler och hemligheter.

   Mer information finns i [Pipeline Variables](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables).

* Stöd finns nu för autentiseringsbundna privata Maven-databaser.

* Molnhanterarens byggbehållare har nu stöd för både Java 8 och Java 11.
Mer information finns i [Använda Java 11-stöd](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

### Felkorrigeringar {#bug-fixes-cm}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Alternativen **Avbryt** och **Spara** på redigeringssidan för icke-produktionsförlopp är inte alltid synliga.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.

### Kända fel {#known-issues}

* På grund av en förändring i hur kodens täckning beräknas är versionen *minimum* av Jacoco-pluginprogrammet nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.