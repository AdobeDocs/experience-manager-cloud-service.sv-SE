---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.5.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.5.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.5.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.5.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.5.0 är 7 maj 2020.

## Nyheter {#whats-new-cloud-manager}

* Sex ytterligare regler för kodkvalitet har lagts till för att hjälpa kunderna att identifiera potentiella problem när de planerar en migrering till Cloud Service.
* En ny metrisk *Cloud Service-kompatibilitet* har lagts till för att sammanfatta antalet kompatibilitetsrelaterade problem.
* Miljöer som inte har skapats tas nu bort automatiskt cirka 24 timmar efter att de har skapats, om de inte redan har tagits bort.
* Prestanda för aktivitetssidan och Pipeline Executions List API har förbättrats.
* Loggen för kodkvalitet innehåller nu fullständiga stackspår för undantag.

### Bug Fixes  {#bug-fixes}

* Ett missvisande kort visades på översiktssidan när produktionsflödet kördes.
* Kodkvalitetsregeln *DontImplementOrExtendProviderTypesPomCheck* kan ibland generera ett Null-pekarundantag.
* Vissa dokumentationslänkar från översiktssidan fungerade inte korrekt.
* Dialogrutan Skapa miljö renderades inte korrekt i Safari.
* Vissa kort på översiktssidan visade inte enhetsnamn korrekt.
* I vissa fall kommer Build Image inte att kunna hämta kundpaket.
