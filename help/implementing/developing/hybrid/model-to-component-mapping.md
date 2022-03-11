---
title: Dynamisk mappning av modell till komponent för SPA
description: I den här artikeln beskrivs hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Dynamisk mappning av modell till komponent för SPA {#dynamic-model-to-component-mapping-for-spas}

I det här dokumentet beskrivs hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM.

## ComponentMapping-modul {#componentmapping-module}

The `ComponentMapping` -modulen tillhandahålls som ett NPM-paket till frontendprojektet. Det lagrar komponenter för användargränssnitt och tillhandahåller ett sätt för Single Page Application att mappa komponenter för användargränssnitt till AEM resurstyper. Detta aktiverar en dynamisk upplösning för komponenter när JSON-modellen för programmet analyseras.

Varje objekt i modellen innehåller en `:type` fält som visar en AEM resurstyp. När den är monterad kan den främre komponenten återge sig själv med det fragment av modellen som den har fått från de underliggande biblioteken.

Se [SPA Blueprint](blueprint.md) -dokument om du vill ha mer information om modellparsning och frontdelens åtkomst till modellen.

Se även npm-paketet: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Modellstyrt Single Page-program {#model-driven-single-page-application}

Single Page-program som använder Javascript SPA SDK för AEM är modelldrivna:

1. Front-end-komponenter registrerar sig för [Komponentmappningsarkiv](#componentmapping-module).
1. Sedan [Behållare](blueprint.md#container), efter att ha fått en modell av [Modellprovider](blueprint.md#the-model-provider), itererar över sitt modellinnehåll (`:items`).

1. För en sida, dess underordnade sidor (`:children`) hämta först en komponentklass från [Komponentmappning](blueprint.md#componentmapping) och sedan instansiera den.

## Programinitiering {#app-initialization}

Varje komponent utökas med funktionerna i [`ModelProvider`](blueprint.md#the-model-provider). Initieringen har därför följande allmänna form:

1. Varje modellprovider initierar sig själv och lyssnar efter ändringar som gjorts i den del av modellen som motsvarar dess inre komponent.
1. The [`PageModelManager`](blueprint.md#pagemodelmanager) måste initieras så som representeras av [initieringsflöde](blueprint.md).

1. När sidmodellhanteraren har lagrats returnerar den hela appmodellen.
1. Den här modellen skickas sedan till frontendroten [Behållare](blueprint.md#container) -komponenten i programmet.
1. Delar av modellen sprids slutligen till varje enskild underordnad komponent.

![Initiering av appmodell](assets/app-model-initialization.png)
