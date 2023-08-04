---
title: Versionsinformation om Adobe Experience Manager as a Cloud Service 2020.5.0
description: "[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.5.0."
exl-id: 8570d2c3-6d55-4914-94b2-f5d162e0c285
source-git-commit: 9ceec0401b91bba2408bda89d4f2c486e2d51eec
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Versionsinformation för AEM as a Cloud Service 2020.5.0 {#release-notes}

På den här sidan finns en översikt över den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.5.0.

## Releasedatum {#release-date}

Utgivningsdatum för [!DNL Experience Manager] as a Cloud Service 2020.5.0 är 7 maj 2020.

## Nyheter i AEM Sites {#aem-sites}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för AEM Sites i AEM as a Cloud Service Release 2020.5.0.

* Detaljerad jobbinformation är nu tillgänglig efter bearbetning av flyttning av gruppsidor och utlöses som asynkrona jobb.
* När du kopierar/klistrar in ett sidträd kan du nu välja mellan att bara klistra in rotsidan eller även undersidorna i trädet.
* AEM Experience Fragments som exporteras till Adobe Target-arbetsytor visas nu som unika erbjudandetyper och erbjudandekällor i Target.
* MSM - använder *publicera* utlösaren har nu tagit bort borttagningshändelser för komponenter i en live-kopieringskälla, d.v.s. tagit bort komponenter i en live-kopia som har tagits bort i live-kopieringskällan.
* MSM - komponenterna för live-kopiering byter nu namn till *_msm_move* efter att samma komponent har rullats ut från live-kopieringskälla.


## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM as a Cloud Service Release 2020.5.0.

### Nyheter {#what-is-new}

* Sex ytterligare regler för kodkvalitet har lagts till för att hjälpa kunderna att identifiera potentiella problem när de planerar en migrering till Cloud Service.
* Ett nytt mått *Kompatibilitet med Cloud Service* har lagts till för att sammanfatta antalet kompatibilitetsrelaterade frågor.
* Miljöer som inte har skapats tas nu bort automatiskt cirka 24 timmar efter att de har skapats, om de inte redan har tagits bort.
* Prestanda för aktivitetssidan och Pipeline Executions List API har förbättrats.
* Loggen för kodkvalitet innehåller nu fullständiga stackspår för undantag.

### Felkorrigeringar  {#bug-fixes}

* Ett missvisande kort visades på översiktssidan när produktionsflödet kördes.
* The *DontImplementOrExtendProviderTypesPomCheck* Regeln för kodkvalitet kan ibland generera ett Null-pekarundantag.
* Vissa dokumentationslänkar från översiktssidan fungerade inte korrekt.
* Dialogrutan Skapa miljö renderades inte korrekt i Safari.
* Vissa kort på översiktssidan visade inte enhetsnamn korrekt.
* I vissa fall kommer Build Image inte att kunna hämta kundpaket.
