---
title: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.2.0
description: Versionsinformation för Cloud Manager i AEM som Cloud Service version 2021.2.0
translation-type: tm+mt
source-git-commit: 32557b3f25e4d4f4cb652f19cff4dae58638e07b
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager som Cloud Service 2021.2.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.2.0.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.2.0 är 11 februari 2021.

## Cloud Manager {#cloud-manager}

### Nyheter {#what-is-new}

* Resurskunder kan nu välja när och var de ska distribuera sin Brand Portal-instans på ett självbetjäningssätt via användargränssnittet i Cloud Manager. För ett vanligt (icke-sandlådeprogram) program med Assets-lösning kan Brand Portal nu etableras i produktionsmiljön. Etableringen kan bara göras en gång i produktionsmiljön.

* Den AEM Project Archetype som används i Project och Sandbox Creation har uppdaterats till version 25.

* Listan med föråldrade API:er som identifieras vid kodskanning har förfinats så att den innehåller ytterligare klasser och metoder som har tagits bort i den senaste SDK-versionen av Cloud Servicen.

* SonarQube-profilen för Cloud Manager har uppdaterats för att ta bort Sonar-regelbläckfisk:S2142. Detta kommer inte längre att orsaka en konflikt med kontrollerna för trådavbrott.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan lägga till/uppdatera domännamn för tillfället eftersom den associerade miljön antingen har en pågående pipeline kopplad till sig eller som väntar på godkännande.

* Egenskaper som angetts i kundens `pom.xml`-filer som har prefixats med sonar kommer nu att tas bort dynamiskt för att undvika problem med bygg- och kvalitetsskanning.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* Ytterligare regler för kodkvalitet har lagts till för att täcka problem med Cloud Servicens kompatibilitet.

### Felkorrigeringar {#bug-fixes}

* Det är inte längre skiftlägeskänsligt att matcha SSL-certifikat mot ett domännamn.

* Molnhanterarens användargränssnitt informerar nu en användare om att certifikatets privata nycklar inte uppfyller 2 048-bitarsgränsen med ett felmeddelande.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* I vissa fall kan ett internt problem leda till att miljön tas bort.

* En del pipeline-fel rapporterades felaktigt som pipeline-fel.
