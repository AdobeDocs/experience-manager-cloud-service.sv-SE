---
title: Versionsinformation för version 2020.3.0
description: "[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.3.0."
exl-id: 0393c789-3999-4e51-be83-269d6eabd3f3
source-git-commit: 9ceec0401b91bba2408bda89d4f2c486e2d51eec
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---

# Versionsinformation för AEM as a Cloud Service 2020.3.0 {#release-notes}

På den här sidan finns en översikt över den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.3.0.

## Releasedatum {#release-date}

Releasedatum för Experience Manager as a Cloud Service 2020.3.0 är 5 mars 2020.

## Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM as a Cloud Service Release 2020.3.0.

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
* I specifika projekt *ResourceResolver-objekt ska alltid stängas* skulle generera ett Null-pekarundantag. Detta påverkade dock inte pipelinekörningen.
