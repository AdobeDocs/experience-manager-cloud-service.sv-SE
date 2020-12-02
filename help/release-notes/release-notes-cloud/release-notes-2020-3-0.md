---
title: Versionsinformation för version 2020.3.0
description: Versionsinformation för version 2020.3.0
translation-type: tm+mt
source-git-commit: 3dc0d1d77595f7b3e890fb4b390eef5bcf84ecd8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---


# Versionsinformation för AEM som en Cloud Service 2020.3.0 {#release-notes}

På den här sidan beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.3.0.

## Releasedatum {#release-date}

Releasedatum för Experience Manager som Cloud Service 2020.3.0 är 5 mars 2020.

## Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM som en Cloud Service-version 2020.3.0.

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

