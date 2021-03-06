---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2020.3.0
description: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2020.3.0
feature: Release Information
exl-id: 2ff62ba5-a657-4739-b646-1e948332bf79
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager i Adobe Experience Manager as a Cloud Service 2020.3.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2020.3.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2020.3.0 är 5 mars 2020.

### Nyheter {#what-is-new}

* Loggen för byggsteget är nu tillgänglig medan byggsteget körs.
* Vissa av meddelandena på informationssidan för pipeline-körning har redigerats för tydlighet.

### Felkorrigeringar  {#bug-fixes}

* Det gick inte att hämta loggfiler för anpassade och funktionella teststeg via användargränssnittet.
* När Git-databasen för ett Cloud Service-program inte kunde skapas kunde användare med rollen Distributionshanterare ibland inte återställas från det här felet.
* Vissa användaraktiviteter när ett sandlådeprogram skapas kan göra att det inte går att skapa programmet innan icke-produktionsflödet skapas.
* Den tillfälliga SonarQube-instansen som användes i byggsteget misslyckades ibland att starta inom den konfigurerade tidsgränsen.
* Samtidig generering av dev-miljöer i samma Cloud Service-program kan stöta på ett villkor där endast en kunde skapas.
* Meddelanden från Experience Cloud om program för Cloud Service togs inte emot konsekvent.
* I specifika projekt *ResourceResolver-objekt ska alltid stängas* skulle generera ett Null-pekarundantag, Detta påverkade dock inte genomförandet av pipeline.
