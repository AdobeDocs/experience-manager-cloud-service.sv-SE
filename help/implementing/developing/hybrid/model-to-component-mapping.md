---
title: Dynamisk mappning av modell till komponent för SPA
description: I den här artikeln beskrivs hur den dynamiska mappningen av modell till komponent sker i JavaScript SPA SDK för AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Dynamisk mappning av modell till komponent för SPA {#dynamic-model-to-component-mapping-for-spas}

I det här dokumentet beskrivs hur den dynamiska mappningen av modell till komponent sker i JavaScript SPA SDK för AEM.

## ComponentMapping-modul {#componentmapping-module}

Modulen `ComponentMapping` tillhandahålls som ett NPM-paket till frontendprojektet. Det lagrar komponenter för användargränssnitt och tillhandahåller ett sätt för Single Page Application att mappa komponenter för användargränssnitt till AEM resurstyper. Modulen aktiverar en dynamisk upplösning för komponenter när JSON-modellen för programmet analyseras.

Varje objekt i modellen innehåller ett `:type`-fält som visar en AEM resurstyp. När den är monterad kan den främre komponenten återge sig själv med det fragment av modellen som den har fått från de underliggande biblioteken.

Mer information om modellparsning och åtkomst för komponenter i gränssnittet finns i dokumentet [SPA utkast](blueprint.md) .

Se även nPM-paketet: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Modellstyrt Single Page-program {#model-driven-single-page-application}

Single Page-program som använder JavaScript SPA SDK för AEM är modelldrivna:

1. Front-end-komponenter registrerar sig själva för [Component Mapping Store](#componentmapping-module).
1. Sedan itererar [behållaren](blueprint.md#container), när den har tillhandahållits med en modell av [modellprovidern](blueprint.md#the-model-provider), över sitt modellinnehåll (`:items`).

1. Om det finns en sida hämtar dess underordnade sidor (`:children`) först en komponentklass från [ Component Mapping](blueprint.md#componentmapping) och instansierar den sedan.

## Programinitiering {#app-initialization}

Varje komponent utökas med funktionerna i [`ModelProvider`](blueprint.md#the-model-provider). Initieringen har därför följande allmänna form:

1. Varje modellprovider initierar sig själv och lyssnar efter ändringar som gjorts i den del av modellen som motsvarar dess inre komponent.
1. [`PageModelManager`](blueprint.md#pagemodelmanager) måste initieras så som den representeras av [initieringsflödet](blueprint.md).

1. När sidmodellhanteraren har lagrats returnerar den hela appmodellen.
1. Den här modellen skickas sedan till rotkomponenten [Container](blueprint.md#container) i början av programmet.
1. Delar av modellen sprids slutligen till varje enskild underordnad komponent.

![Initiering av appmodell](assets/app-model-initialization.png)
