---
title: AEM och tredjeparts Commerce Integration med Commerce Integration Framework
description: Företag kan behöva ytterligare e-handelslösningar från tredje part för att göra sin butik tillgänglig. Commerce Integration Framework (CIF) kan användas i sådana integreringsscenarier för att ansluta en tredjepartslösning för e-handel till Adobe Experience Manager med hjälp av I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c,42dd8922-540d-4a93-9e45-b5e83dc11e16
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# AEM och tredjeparts Commerce Integration med Commerce Integration Framework {#aem-third-party}

Integrationen av lösningar från andra företag än Adobe Commerce är ett vanligt scenario för CIF. Tredjepartslösningar med olika API:er och scheman kopplas samman via ett integreringslager.

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

[AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) hämta och utbyta data via de CIF-stödda Adobe Commerce-API:erna. För att återanvända komponenter måste respektive API:er implementeras.

Rekommendationen för prestandakrävande komponenter på klientsidan är att kommunicera direkt med tredjepartslösningen för att undvika latens.

## Utveckla en integrering {#develop-integration}

Vi rekommenderar att du använder [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) för integreringslagret. Det ingår i CIF-tillägget för tredje part. Eftersom det fungerar med en mikrotjänstliknande metod är det lämpligt att integrera flera lösningar på ett enkelt sätt.

The [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference) är en bra startpunkt för att bygga integreringen i e-handelslösningen. Även om det har stöd för GraphQL kan det även integreras med andra typer av API som REST.

Det här integreringslagret är inte nödvändigt om ett lager från tredje part är tillgängligt (till exempel Mulesoft) eller om integreringen byggs ovanpå en lösning från tredje part.

## Fördefinierade anslutningar {#connectors}

Kopplingar är en bra början för projekt. De levereras med en handelslösningsspecifik anslutning och standardmappning av API. Dessa kontakter byggs av tredje part och underhålls inte av Adobe. Kontakta respektive partner för mer information.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), skapat av Diconium
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), skapat av Diconium

>[!TIP]
>
>Kopplingar hjälper till att snabba upp handelsintegreringen, men de är inte plug-in-play. E-handelslösningar för företag är oftast mycket anpassade och kräver en anpassad integrering. Goda kunskaper om handelsplattformen, Adobe Commerce GraphQL-scheman och Adobe I/O Runtime krävs.
