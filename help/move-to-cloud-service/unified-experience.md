---
title: Enhetlig upplevelse för verktyg för kodkorrigering
description: Enhetlig upplevelse för verktyg för kodkorrigering
translation-type: tm+mt
source-git-commit: d6fa0d8bb7d5e251e51a3e4ffd93d6aaa1c7980c
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Enhetlig upplevelse för verktyg för kodkorrigering {#unified-experience}

Vi har utvecklat verktyg för att automatisera några av de kodkorrigeringsuppgifter som krävs för att vara kompatibel med AEM som en Cloud Service. För att minska komplexiteten i samband med installation och konfiguration av olika verktyg för kodomfaktorisering har vi utvecklat ett plugin-program för att kombinera verktyg som fungerar med kod och databaser.

## Fördelar {#benefits}

Plugin-programmet för enhetlig upplevelse ger följande fördelar:

* Enhetliggör verktyg som fungerar med källkod i ett `node.js` program som visas som `aio-cli ` plugin-program för att ge användaren en konsekvent användarupplevelse.

* Ger möjlighet att köra alla verktyg med ett enda kommando, samtidigt som den ger flexibilitet att köra specifika verktyg efter behov.

* Utbyggbart för att förenkla tillägg av nya verktyg, samtidigt som upplevelsen blir enhetlig.

## Om plugin-programmet {#understanding-plugin}

Plugin- `aio-cli-plugin-aem-cloud-service-migration` programmet består av två huvuddelar:

* **Användargränssnitt**

   * `aio-cli` kommandon för att köra ett eller flera verktyg för kodomfaktorisering (genom att kedja verktygen som ska köras sekventiellt).
   * `config.yaml` som har de indataparametrar som krävs.

* **Underliggande Code Refactoring Tool Suite**

   Kodomfaktoriseringsverktygen utför sina funktioner genom att:

   * Skanna in respektive avsnitt i kundens kod och ändra koden (baserat på bästa praxis för kodimplementering) för att skapa utdata som sedan kan valideras och distribueras.

   * Skapar en sammanfattningsrapport för att registrera de åtgärder som utförts under körningen.

## Tillgänglighet {#availability}

Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) för att lära dig mer om användningen och hur du kan bidra till denna plugin-kod som är öppen från GitHub.

>[!NOTE]
>För närvarande är det bara Dispatcher Converter som är integrerad med plugin-programmet.
