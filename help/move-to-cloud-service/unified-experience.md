---
title: Enhetlig upplevelse för verktyg för kodkorrigering
description: Enhetlig upplevelse för verktyg för kodkorrigering
translation-type: tm+mt
source-git-commit: 5d2b14c827603297a59cba7180fc1a68de0c841a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Enhetlig upplevelse för verktygen för kodkorrigering {#unified-experience}

Vi har utvecklat verktyg för att automatisera några av de kodkorrigeringsuppgifter som krävs för att vara kompatibel med AEM som en Cloud Service. För att minska komplexiteten i samband med installation och konfiguration av olika verktyg för kodomfaktorisering har vi utvecklat ett plugin-program för att kombinera verktyg som fungerar med kod och databaser.

## Fördelar {#benefits}

Plugin-programmet för enhetlig upplevelse ger följande fördelar:

* Enhetliggör verktyg som arbetar med källkod i ett `node.js`-program som visas som `aio-cli `-plugin-program för att ge användaren en konsekvent användarupplevelse.

* Ger möjlighet att köra alla verktyg med ett enda kommando, samtidigt som den ger flexibilitet att köra specifika verktyg efter behov.

* Utbyggbart för att förenkla tillägg av nya verktyg, samtidigt som upplevelsen blir enhetlig.

## Plugin-programmet {#understanding-plugin}

Plugin-programmet `aio-cli-plugin-aem-cloud-service-migration` består av två huvuddelar:

* **Användargränssnitt**

   * `aio-cli` kommandon för att köra ett eller flera verktyg för kodomfaktorisering (genom att kedja verktygen som ska köras sekventiellt).
   * `config.yaml` som har de indataparametrar som krävs.

* **Underliggande Code Refactoring Tool Suite**

   Kodomfaktoriseringsverktygen utför sina funktioner genom att:

   * Skanna in respektive avsnitt i kundens kod och ändra koden (baserat på bästa praxis för kodimplementering) för att skapa utdata som sedan kan valideras och distribueras.

   * Skapar en sammanfattningsrapport för att registrera de åtgärder som utförts under körningen.

## Tillgänglighet {#availability}

Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) om du vill veta mer om användningen och hur du kan bidra till den plugin-kod som är öppen från GitHub.

>[!NOTE]
>För närvarande är plugin-programmet integrerat med AEM Dispatcher Converter och Repository Modernizer.
