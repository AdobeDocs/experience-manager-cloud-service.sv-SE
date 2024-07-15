---
title: Versionsinformation för version 2020.3.0
description: "[!DNL Adobe Experience Manager] as a Cloud Service versionsinformation för 2020.3.0."
exl-id: 0393c789-3999-4e51-be83-269d6eabd3f3
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Versionsinformation om AEM as a Cloud Service 2020.3.0 {#release-notes}

På den här sidan beskrivs den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.3.0.

## Releasedatum {#release-date}

Releasedatum för Experience Manager as a Cloud Service 2020.3.0 är 5 mars 2020.

## Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM as a Cloud Service version 2020.3.0.

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
* I specifika projekt ska *ResourceResolver-objekten alltid vara stängda* vilket ger ett Null-pekarundantag. Detta påverkade emellertid inte pipelinekörningen.
