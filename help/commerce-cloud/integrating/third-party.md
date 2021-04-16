---
title: AEM och tredjeparts Commerce Integration med Commerce Integration Framework
description: Företag kan behöva ytterligare e-handelslösningar från tredje part för att göra sin butik tillgänglig. Commerce Integration Framework (CIF) kan användas i sådana integreringsscenarier för att ansluta en tredjepartslösning för e-handel till Adobe Experience Manager med hjälp av I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: 42dd8922-540d-4a93-9e45-b5e83dc11e16
translation-type: tm+mt
source-git-commit: c0a79d9ffefba06b64d48aed79e9a00baa4987df
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# AEM och tredjeparts Commerce Integration med Commerce Integration Framework {#aem-third-party}

Integrationen av en icke-Adobe-handelslösning är ett vanligt scenario för CIF. Tredjepartslösningar med olika API:er och scheman kopplas samman via ett integreringslager.

## Arkitektur {#architecture}

Den övergripande arkitekturen är följande:

![Översikt över arkitekturen AEM andra än Magento/tredje part](../assets//AEM_nonMagento_Architecture.png)

Syftet med detta integreringslager är att mappa tredjeparts-API:er och scheman mot de Adobe Commerce GraphQL-API:er och scheman som stöds utanför Experience Manager. Tack vare den här inkapslingen kan integreringslogiken och -systemen uppdateras utan att koden i Experience Manager ändras.

## Lösningskrav för integrering

När Experience Manager hämtar data on-demand krävs realtids-API:er för produktkatalogen.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel [Magento öppen källkod](https://magento.com/products/magento-open-source).

Du behöver inte implementera hela GraphQL-schemat, bara schemats objekt för att aktivera de önskade användningsfallen.

## Användningsfall i serverdelen

CIF utökar Experience Manager med produktkatalogåtkomst i realtid och verktyg för hantering av produktupplevelser. Denna smidiga integrering gör att författare kan komma åt e-handelsdata med inbäddade användargränssnitt när det behövs utan att lämna innehållskontexten.

Integreringen av programmeringsgränssnitt för produktkataloger krävs för att låsa upp dessa användningsfall.

## Fallstudier

[AEM CIF Core ](https://github.com/adobe/aem-core-cif-components) Components hämtar och utbyter data via de CIF-API:er som stöds i Adobe Commerce. För att återanvända komponenter måste respektive API:er implementeras.

Rekommendationen för prestandakrävande komponenter på klientsidan är att kommunicera direkt med tredjepartslösningen för att undvika latens.

## Utveckla en integrering {#develop-integration}

Vi rekommenderar att du använder [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) för integreringslagret. Det ingår i CIF-tillägget för tredje part. Eftersom det fungerar med en mikrotjänstliknande metod är det lämpligt att integrera flera lösningar på ett enkelt sätt.

[referensimplementeringen](https://github.com/adobe/commerce-cif-graphql-integration-reference) är en bra utgångspunkt för att bygga integreringen med din e-handelslösning. Även om det har stöd för GraphQL kan det även integreras med andra typer av API som REST.

Det här integreringslagret är inte nödvändigt om ett lager från tredje part är tillgängligt (t.ex. Mulesoft) eller om integreringen byggs ovanpå tredjepartslösningen.
