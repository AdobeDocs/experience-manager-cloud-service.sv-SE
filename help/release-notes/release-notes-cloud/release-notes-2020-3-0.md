---
title: Versionsinformation för version 2020.3.0
description: Versionsinformation för version 2020.3.0
translation-type: tm+mt
source-git-commit: 27225bf4b918f39892ac9ab6f46deb97479f08e8

---


# Versionsinformation för AEM som molntjänst 2020.3.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som en molntjänst 2020.3.0.


## Releasedatum {#release-date}

Releasedatum för Experience Manager som molntjänst 2020.3.0 är 5 mars 2020.

## Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM som en molntjänst 2020.3.0.

### Nyheter {#what-is-new}

* Loggen för byggsteget är nu tillgänglig medan byggsteget körs.
* Vissa av meddelandena på informationssidan för pipeline-körning har redigerats för tydlighet.

### Felkorrigeringar {#bug-fixes}

* Det gick inte att hämta loggfiler för anpassade och funktionella teststeg via användargränssnittet.
* När Git-databasen för ett molntjänstprogram inte kunde skapas kunde användare i distributionshanterarrollen ibland inte återställas från det här felet.
* Vissa användaraktiviteter när ett sandlådeprogram skapas kan göra att det inte går att skapa programmet innan icke-produktionsflödet skapas.
* Den tillfälliga SonarQube-instansen som användes i byggsteget misslyckades ibland att starta inom den konfigurerade tidsgränsen.
* Samtidig generering av dev-miljöer i samma molntjänstprogram kunde stöta på ett villkor där endast en kunde skapas.
* Experience Cloud-meddelanden för molntjänstprogram togs inte emot konsekvent.
* I specifika projekt ska *ResourceResolver-objekten alltid stängas* vilket ger ett Null-pekarundantag. Detta påverkade dock inte genomförandet av pipeline.

