---
title: Versionsinformation om Adobe Experience Manager som molntjänst för 2020.5.0
description: Versionsinformation om Experience Manager för 2020.5.0
translation-type: tm+mt
source-git-commit: 8fe1f6f1c7c6a608ee1ca42836ee91e83487428d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Versionsinformation för AEM som molntjänst 2020.5.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som en molntjänst 2020.5.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] som molntjänst 2020.5.0 är 7 maj 2020.

## Nyheter i AEM Sites {#aem-sites}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för AEM Sites i AEM som en Cloud Service Release 2020.5.0.

* Detaljerad jobbinformation är nu tillgänglig efter bearbetning av flyttning av gruppsidor och utlöses som asynkrona jobb.
* När du kopierar/klistrar in ett sidträd kan du nu välja mellan att bara klistra in rotsidan eller även undersidorna i trädet.
* AEM Experience Fragments som exporteras till Adobe Target-arbetsytor visas nu som unika erbjudandetyper och erbjudandekällor i Target.
* MSM - med *publiceringsutlösaren* kan du nu ta bort borttagningshändelser för komponenter i live-kopieringskällan, det vill säga ta bort komponenter i en live-kopia som har tagits bort i live-kopiekällan.
* MSM - komponenterna för live-kopiering byter nu namn till *_msm_move* efter att samma komponent har rullats ut från live-kopiekälla.


## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM som en molntjänst 2020.5.0.

### What&#39;s New {#what-is-new}

* Sex ytterligare regler för kodkvalitet har lagts till för att hjälpa kunderna att identifiera potentiella problem när de planerar en migrering till molntjänsten.
* Ett nytt mått på *molntjänstkompatibilitet* har lagts till för att sammanfatta antalet kompatibilitetsrelaterade problem.
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

