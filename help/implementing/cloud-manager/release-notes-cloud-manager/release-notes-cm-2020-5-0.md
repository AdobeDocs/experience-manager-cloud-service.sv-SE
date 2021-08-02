---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.5.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.5.0
feature: Versionsinformation
exl-id: 9f534858-d18f-4224-8b94-9583a05aed95
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.5.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.5.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.5.0 är 7 maj 2020.

## Nyheter {#whats-new-cloud-manager}

* Sex ytterligare regler för kodkvalitet har lagts till för att hjälpa kunderna att identifiera potentiella problem när de planerar en migrering till Cloud Service.
* Ett nytt mått *Cloud Service Compatibility* har lagts till för att sammanfatta antalet kompatibilitetsrelaterade problem.
* Miljöer som inte har skapats tas nu bort automatiskt cirka 24 timmar efter att de har skapats, om de inte redan har tagits bort.
* Prestanda för aktivitetssidan och Pipeline Executions List API har förbättrats.
* Loggen för kodkvalitet innehåller nu fullständiga stackspår för undantag.

### Felkorrigeringar  {#bug-fixes}

* Ett missvisande kort visades på översiktssidan när produktionsflödet kördes.
* Kodkvalitetsregeln *DontImplementOrExtendProviderTypesPomCheck* kan ibland generera ett Null-pekarundantag.
* Vissa dokumentationslänkar från översiktssidan fungerade inte korrekt.
* Dialogrutan Skapa miljö renderades inte korrekt i Safari.
* Vissa kort på översiktssidan visade inte enhetsnamn korrekt.
* I vissa fall kommer Build Image inte att kunna hämta kundpaket.
