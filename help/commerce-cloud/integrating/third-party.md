---
title: AEM och tredjeparts Commerce Integration med Commerce Integration Framework
description: Företag kan behöva ytterligare e-handelslösningar från tredje part för att göra sin butik tillgänglig. Commerce Integration Framework (CIF) kan användas i sådana integreringsscenarier för att ansluta en tredjepartslösning för e-handel till Adobe Experience Manager med hjälp av I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c
source-git-commit: 5311ba7f001201fc94c73fa52bc7033716c1ba78
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# AEM och tredjeparts Commerce Integration med Commerce Integration Framework {#aem-third-party}

Integrationen av lösningar från andra företag än Adobe Commerce är ett vanligt scenario för CIF. Tredjepartslösningar med olika API:er och scheman kopplas samman via ett integreringslager.

## Arkitektur {#architecture}

Den övergripande arkitekturen är följande:

![Översikt över arkitekturen AEM andra än Magento/tredje part](../assets//AEM_nonMagento_Architecture.png)

Syftet med detta integreringslager är att mappa tredjeparts-API:er och scheman mot de Adobe Commerce GraphQL-API:er och -scheman som stöds utanför Experience Manager. Tack vare den här inkapslingen kan integreringslogiken och -systemen uppdateras utan att koden i Experience Manager ändras.

## Lösningskrav för integrering

När Experience Manager hämtar data on-demand krävs realtids-API:er för produktkatalogen.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel [Adobe Commerce Open Source](https://business.adobe.com/products/magento/open-source.html).

Du behöver inte implementera hela GraphQL-schemat, bara schemats objekt för att aktivera de önskade användningsfallen.

## Användningsfall i serverdelen

CIF utökar Experience Manager med produktkatalogåtkomst i realtid och verktyg för hantering av produktupplevelser. Denna smidiga integrering gör att författare kan komma åt e-handelsdata med inbäddade användargränssnitt när det behövs utan att lämna innehållskontexten.

Integreringen av API:er för produktkataloger krävs för att låsa upp dessa användningsfall.

## Fallstudier

[AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) hämta och utbyta data via de CIF-stödda Adobe Commerce-API:erna. Om du vill återanvända komponenter måste respektive API implementeras.

Rekommendationen för prestandakrävande komponenter på klientsidan är att kommunicera direkt med tredjepartslösningen för att undvika latens.

## Utveckla en integrering {#develop-integration}

Adobe rekommenderar att du använder [Adobe Developer Runtime](https://developer.adobe.com/runtime/) för integreringslagret. Den ingår i CIF-tillägget för tredje parter. Eftersom det fungerar med en mikrotjänstliknande metod är det lämpligt att integrera flera lösningar på ett enkelt sätt.

The [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference) är en bra startpunkt för att bygga integreringen i e-handelslösningen. Även om det har stöd för GraphQL kan det även integreras med andra typer av API som REST.

Det här integreringslagret behövs inte om ett lager från tredje part är tillgängligt (till exempel Mulesoft) eller om integreringen byggs ovanpå tredjepartslösningen.

## Fördefinierade anslutningar {#connectors}

Kopplingar är en bra början för projekt. De levereras med en e-handelslösningsspecifik anslutning och standard-API-mappning. Dessa kontakter byggs av tredje part och underhålls inte av Adobe. Kontakta respektive partner för mer information.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), skapat av Diconium
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), skapat av Diconium

>[!TIP]
>
>Kopplingar hjälper till att snabba upp handelsintegreringen, men de är inte plug-in-play. E-handelslösningar för företag är mycket anpassade och kräver en anpassad integrering. Goda kunskaper om handelsplattformen, Adobe Commerce GraphQL scheman och Adobe I/O Runtime krävs.
