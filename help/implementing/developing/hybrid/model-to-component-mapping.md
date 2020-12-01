---
title: Dynamisk mappning av modell till komponent för SPA
description: I den här artikeln beskrivs hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM.
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Dynamisk mappning av modell till komponent för SPA {#dynamic-model-to-component-mapping-for-spas}

I det här dokumentet beskrivs hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM.

## ComponentMapping Module {#componentmapping-module}

Modulen `ComponentMapping` tillhandahålls som ett NPM-paket till frontendprojektet. Det lagrar komponenter för användargränssnitt och tillhandahåller ett sätt för Single Page Application att mappa komponenter för användargränssnitt till AEM resurstyper. Detta aktiverar en dynamisk upplösning för komponenter när JSON-modellen för programmet analyseras.

Varje objekt i modellen innehåller ett `:type`-fält som visar en AEM resurstyp. När den är monterad kan den främre komponenten återge sig själv med det fragment av modellen som den har fått från de underliggande biblioteken.

Läs [SPA Blueprint](blueprint.md)-dokumentet om du vill ha mer information om modellparsning och åtkomst till modellens front-end-komponent.

Se även npm-paketet: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Modellstyrt Single Page-program {#model-driven-single-page-application}

Single Page-program som använder Javascript SPA SDK för AEM är modelldrivna:

1. Front-end-komponenter registrerar sig för [Component Mapping Store](#componentmapping-module).
1. Sedan itererar [behållaren](blueprint.md#container), när den har fått en modell av [modellprovidern](blueprint.md#the-model-provider), över sitt modellinnehåll (`:items`).

1. För en sida hämtar dess underordnade (`:children`) först en komponentklass från [komponentmappningen](blueprint.md#componentmapping) och instansierar den sedan.

## Programinitiering {#app-initialization}

Varje komponent utökas med funktionerna i [`ModelProvider`](blueprint.md#the-model-provider). Initieringen har därför följande allmänna form:

1. Varje modellprovider initierar sig själv och lyssnar efter ändringar som gjorts i den del av modellen som motsvarar dess inre komponent.
1. [`PageModelManager`](blueprint.md#pagemodelmanager) måste initieras så som den representeras av [initieringsflödet](blueprint.md).

1. När sidmodellhanteraren har lagrats returnerar den hela appmodellen.
1. Den här modellen skickas sedan till frontendroten [Container](blueprint.md#container)-komponenten i programmet.
1. Delar av modellen sprids slutligen till varje enskild underordnad komponent.

![Initiering av appmodell](assets/app-model-initialization.png)
