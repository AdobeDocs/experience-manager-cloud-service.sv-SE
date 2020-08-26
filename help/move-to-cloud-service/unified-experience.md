---
title: Enhetlig upplevelse för verktyg för kodkorrigering
description: Enhetlig upplevelse för verktyg för kodkorrigering
translation-type: tm+mt
source-git-commit: c00b10b4d564e05099740b9ff991624db4f37a3d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Enhetlig upplevelse för verktyg för kodkorrigering {#unified-experience}

Flera verktyg med olika interaktionspunkter för kunderna skapar en osammanhängande upplevelse och ökar komplexiteten i att använda verktyg, där var och en har olika körningskrav vad gäller installation, konfiguration och utförande.

## Fördelar {#benefits}

Unified Experience for Code Refactoring Tools anropar och kör alla verktyg för kodomfaktorisering som fungerar på källkoden från samma plats.

Med verktygen för enhetlig upplevelse av omfaktorisering och tillhörande databaser kan du:

* Sammanställ alla verktyg som arbetar med källkodsmigrering till ett `node.js` program som exponeras som `aio-cli plugin` för att ge användaren en konsekvent användarupplevelse.

* Möjlighet att utföra den övergripande migreringen via ett enda kommando, samtidigt som det ger flexibilitet att köra ett visst verktyg efter behov.

* Förenkla framtidens tillägg av nya verktyg som att lägga till nya verktyg i plugin-programmet genom att lägga till ett nytt kommando för utvecklare och en enkel plugin-uppdatering för användaren, så att upplevelsen blir mer enhetlig med mer värdetillägg.

### Programdesignen

Med dessa verktyg kombineras alla verktyg för kodomfaktorisering i ett node.js-program som exponeras för `aio-cli plugin` att ge användaren en konsekvent användarupplevelse.

Plugin-programmet består av två huvuddelar:

* **Användargränssnitt**

   `aio-cli` kommandon för att köra ett eller flera migreringsverktyg (genom att kedja verktygen som ska köras sekventiellt)`config.yaml` som tar med de indataparametrar som krävs

* **Underliggande migreringsverktyg**

   Migreringsverktygen utför sina funktioner genom att:

   * Skanna in respektive avsnitt i kundens kod och utför migreringen (baserat på bästa praxis för kodimplementering) för att skapa utdata som sedan kan valideras och distribueras.

   * Inspelning av åtgärder som utförts under migreringen, i en konsekvent ordning för att skapa en sammanfattningsrapport.

## Använda plugin-programmet {#using-plugin}

Kundernas kod, databasstruktur eller konfigurationer `aio-cli-plugin-aem-cloud-service-migration` omformas på kundens lokala dator. Den här sidan innehåller detaljerade krav och designbeslut för den enhetliga upplevelsen.
Det finns som en öppen källkod för communityn som kan utökas för anpassade användningsfall.

## Tillgänglighet {#availability}

Du kan installera och använda `aio-cli-plugin-aem-cloud-service-migration` via `aio-cli` (som för närvarande bara är integrerat med dispatcherns konverterare).

Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) för att lära dig mer om användningen och hur du kan bidra till det här verktyget.

Plugin-koden har öppnats i Github.

