---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.3.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2020.3.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2020.3.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2020.3.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.3.0 är 5 mars 2020.

### Nyheter {#what-is-new}

* Loggen för byggsteget är nu tillgänglig medan byggsteget körs.
* Vissa av meddelandena på informationssidan för pipeline-körning har redigerats för tydlighet.

### Felkorrigeringar {#bug-fixes}

* Det gick inte att hämta loggfiler för anpassade och funktionella teststeg via användargränssnittet.
* När Git-databasen för ett Cloud Service-program inte kunde skapas kunde användare med rollen Distributionshanterare ibland inte återställas från det här felet.
* Vissa användaraktiviteter när ett sandlådeprogram skapas kan göra att det inte går att skapa programmet innan icke-produktionsflödet skapas.
* Den tillfälliga SonarQube-instansen som användes i byggsteget misslyckades ibland att starta inom den konfigurerade tidsgränsen.
* Samtidig generering av dev-miljöer i samma Cloud Service-program kan stöta på ett villkor där endast en kunde skapas.
* Meddelanden från Experience Cloud om program för Cloud Service togs inte emot konsekvent.
* I specifika projekt ska *ResourceResolver-objekten alltid vara stängda* vilket ger ett Null-pekarundantag. Detta påverkade dock inte genomförandet av pipeline.