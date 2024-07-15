---
title: Felsöka beständiga GraphQL-frågor
description: Lär dig felsöka problem med beständiga GraphQL-frågor i Adobe Experience Manager as a Cloud Service.
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Felsöka beständiga GraphQL-frågor {#troubleshoot-persisted-graphql-queries}

[Åtgärdscenter](/help/operations/actions-center.md) innehåller varningen **GraphQL persisted query error** . Det innebär att du får information när någon av dina GraphQL beständiga frågor genererar ett fel.

Den här sidan innehåller de *vanligaste* orsakerna till fel och anvisningar om hur du åtgärdar dem, så att du kan felsöka och lösa sådana problem.

## Ändringar i modellen för innehållsfragment {#changes-to-content-fragment-model}

En GraphQL-beständig fråga kan misslyckas när den baseras på GraphQL-typer som är föråldrade, ofta på grund av en ändring i de underliggande modellerna för innehållsfragment.

Sådana fel kan inträffa av flera olika orsaker. Exempel är (listan är inte uttömmande) när författaren till en modell för innehållsfragment:

* tar bort eller byter namn på ett fält
* uppdaterar **modelltypen** som definierar vilka modeller som tillåts för fragmentreferensen
* Tar bort publicering av en modell som refereras av andra modeller

För att åtgärda sådana fel bör du antingen:

* uppdatera den beständiga fråga som inte kan hantera ändringar som gjorts i modellen för innehållsfragment
* återställa ändringen av modellen som orsakade problemet

## GraphQL-slutpunkten är inte konfigurerad {#graphql-endpoint-not-configured}

När beständiga frågor returnerar felkoden `404` tillsammans med informationen `No suitable endpoint found` innebär det att ingen GraphQL-slutpunkt har konfigurerats i AEM.

För att korrigera detta följer du stegen för att aktivera och publicera din slutpunkt från [Hantera GraphQL-slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Sökväg saknas i GraphQL beständiga fråge-URL {#missing-path-query-url}

Om beständiga frågor returnerar `400`-felkoden med informationen `Suffix: '/' does not contain a path` anropas GraphQL-servern utan något sökvägssuffix.

Mönstret ska vara `/graphql/execute.json/thePath`.

## Blockerad på grund av IP tillåtelselista {#blocked-due-to-ip-allow-list}

I så fall returnerar frågan felkoden `405`.

Ett sådant fel är inte specifikt för GraphQL. Se KB-artikeln [405 Fel tillåts inte](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824).

## Spärrad av avsändare {#blocked-dispatcher}

Om GraphQL-slutpunkten returnerar felet `404` vid publicering för `POST`-begäranden betyder det att GraphQL-frågor blockeras på dispatchernivå och slutpunkten måste aktiveras manuellt.

Detta bör inte vara fallet som standard, men en anpassad dispatcherkonfiguration kan orsaka problemet. Se mer under [Dispatcher - Slutpunktskonfiguration med AEM Headless](/help/headless/deployment/dispatcher.md).
