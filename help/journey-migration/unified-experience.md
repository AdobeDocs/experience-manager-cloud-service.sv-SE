---
title: Enhetlig upplevelse för verktyg för kodkorrigering
description: Läs om Unified Experience for Code Refactoring Tools.
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Enhetlig upplevelse för verktyg för kodkorrigering {#unified-experience}

Vi har utvecklat verktyg för att automatisera några av de kodkorrigeringsuppgifter som krävs för att vara kompatibla med AEM as a Cloud Service. För att minska komplexiteten i samband med installation och konfiguration av olika verktyg för kodomfaktorisering har vi utvecklat ett plugin-program för att kombinera verktyg som fungerar med kod och databaser.

## Fördelar {#benefits}

Plugin-programmet för enhetlig upplevelse ger följande fördelar:

* Enhetliggör verktyg som fungerar med källkod i ett `node.js` program exponeras som `aio-cli ` plugin-program för att ge användaren en konsekvent användarupplevelse.

* Ger möjlighet att köra alla verktyg med ett enda kommando, samtidigt som den ger flexibilitet att köra specifika verktyg efter behov.

* Utbyggbart för att förenkla tillägg av nya verktyg, samtidigt som upplevelsen blir enhetlig.

## Om plugin-programmet {#understanding-plugin}

The `aio-cli-plugin-aem-cloud-service-migration` plugin-programmet består av två huvuddelar:

* **Användargränssnitt**

   * `aio-cli` kommandon för att köra ett eller flera verktyg för kodomfaktorisering (genom att kedja verktygen som ska köras sekventiellt).
   * `config.yaml` som har de indataparametrar som krävs.

* **Underliggande Code Refactoring Tool Suite**

  Kodomfaktoriseringsverktygen utför sina funktioner genom att:

   * Skanna in respektive avsnitt i kundens kod och ändra koden (baserat på bästa praxis för kodimplementering) för att skapa utdata som sedan kan valideras och distribueras.

   * Skapar en sammanfattningsrapport för att registrera de åtgärder som har utförts under körningen.

## Tillgänglighet {#availability}

Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) om du vill veta mer om användningen och hur du kan bidra till denna plugin-kod som är öppen från GitHub.

>[!NOTE]
>För närvarande är plugin-programmet integrerat med AEM Dispatcher Converter och Repository Modernizer.
