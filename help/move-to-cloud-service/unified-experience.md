---
title: Enhetlig upplevelse för verktyg för kodkorrigering
description: Enhetlig upplevelse för verktyg för kodkorrigering
translation-type: tm+mt
source-git-commit: 9ef0681f93c8c25a1e5115cccb987d2db32c318e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Enhetlig upplevelse för verktyg för kodkorrigering {#unified-experience}

Med verktygen för enhetlig upplevelse av kodkorrigering förenas upplevelsen för körning av AEM som ett verktyg för omfaktorisering av Cloud Service som används för dispatcherfiler, kod och databaser.

Det här verktyget minskar komplexiteten med att använda verktyg för kodomfaktorisering, där varje verktyg har olika körningskrav när det gäller installation, konfiguration och körning.

![bild](/help/move-to-cloud-service/assets/unified-one.png)

## Fördelar {#benefits}

Med verktygen för enhetlig upplevelse av omfaktorisering anropas och verkställs alla verktyg för omfaktorisering av kod som fungerar på källkoden från samma plats.

Dessa verktyg tillsammans med de övriga databaserna gör att du kan:

* Alla verktyg som fungerar med källkodmigrering till ett `node.js` program som exponeras `aio-cli plugin` för att ge användaren en konsekvent användarupplevelse.

* Möjlighet att utföra den övergripande migreringen via ett enda kommando, samtidigt som det ger flexibilitet att köra ett visst verktyg efter behov.

* För att förenkla framtida tillägg av nya verktyg, som att lägga till nya verktyg i plugin-programmet, behöver du bara lägga till ett nytt kommando för utvecklaren och en enkel plugin-uppdatering för användaren, så att upplevelsen är konsekvent med mer värdetillägg.

## Om plugin-programmet {#understanding-plugin}

Kundernas kod, databasstruktur eller konfigurationer `aio-cli-plugin-aem-cloud-service-migration` omformas på kundens lokala dator. Den här sidan innehåller detaljerade krav och designbeslut för den enhetliga upplevelsen.
Det finns som en öppen källkod för communityn som kan utökas för anpassade användningsfall.

Med dessa verktyg kombineras alla verktyg för kodomfaktorisering i ett node.js-program som exponeras för `aio-cli plugin` att ge användaren en konsekvent användarupplevelse. Pluginen skannar kundens lokala kodbas och producerar AEM som en Cloud Service-kompatibel kod, konfigurationer och paket som sedan kan distribueras till Cloud Service.

Plugin-programmet består av två huvuddelar:

* **Användargränssnitt**

   `aio-cli` kommandon för att köra ett eller flera migreringsverktyg (genom att kedja verktygen som ska köras sekventiellt)`config.yaml` som tar med de indataparametrar som krävs

* **Underliggande migreringsverktyg**

   Migreringsverktygen utför sina funktioner genom att:

   * Skanna in respektive avsnitt i kundens kod och utför migreringen (baserat på bästa praxis för kodimplementering) för att skapa utdata som sedan kan valideras och distribueras.

   * Inspelning av åtgärder som utförts under migreringen, i en konsekvent ordning för att skapa en sammanfattningsrapport.

## Tillgänglighet {#availability}

Du kan installera och använda `aio-cli-plugin-aem-cloud-service-migration` via `aio-cli`.

>[!NOTE]
>För närvarande är det här verktyget bara integrerat med Dispatcher Converter.

Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) för att lära dig mer om användningen och hur du kan bidra till denna plugin-kod som är öppen från GitHub.

