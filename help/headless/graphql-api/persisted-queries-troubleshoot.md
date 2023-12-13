---
title: Felsöka beständiga GraphQL-frågor
description: Lär dig felsöka problem med beständiga GraphQL-frågor i Adobe Experience Manager as a Cloud Service.
feature: Content Fragments,GraphQL API
source-git-commit: c8ea9846600d1773e6f269973635f5338f31906f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Felsöka beständiga GraphQL-frågor {#troubleshoot-persisted-graphql-queries}

The [Actions Center](/help/operations/actions-center.md) innehåller **GraphQL beständiga frågefel** varning. Det innebär att du får information när någon av dina GraphQL beständiga frågor genererar ett fel.

För att hjälpa dig att felsöka och lösa sådana problem förklarar vi *mest vanligt* orsaker till fel och steg för hur du åtgärdar dem.

## Ändringar i modellen för innehållsfragment {#changes-to-content-fragment-model}

En GraphQL-beständig fråga kan misslyckas när den baseras på GraphQL-typer som är föråldrade, ofta på grund av en ändring i de underliggande modellerna för innehållsfragment.

Det här kan hända av flera olika anledningar. När en innehållsmodellförfattare till exempel:

* tar bort eller byter namn på ett fält
* uppdaterar tillåtna modeller som definierats för en fragmentreferens
* återger en modell som refereras av andra modeller
* andra åtgärder och orsaker

För att åtgärda detta:

* den beständiga frågan som misslyckas bör uppdateras för att passa ändringen av modellen för innehållsfragment
* eller så bör ändringen av den modell som orsakade problemet återställas

## GraphQL-slutpunkten är inte konfigurerad {#graphql-endpoint-not-configured}

Vid beständiga frågor returnerar du `400` eller `500` felkod, tillsammans med informationen `No suitable endpoint found`innebär det att ingen GraphQL-slutpunkt har konfigurerats i AEM.

För att korrigera detta följer du stegen för att aktivera och publicera slutpunkten från [Hantera GraphQL-slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Sökväg saknas i GraphQL beständiga fråge-URL {#missing-path-query-url}

Om beständiga frågor returneras `400` eller `500` felkod med informationen `Suffix: '/' does not contain a path`, anropas GraphQL-servern utan ett sökvägssuffix.

Mönstret ska vara `/graphql/execute.json/thePath`.

## Blockerad på grund av IP tillåtelselista {#blocked-due-to-ip-allow-list}

I så fall returnerar frågan `405` felkod.

Detta är inte specifikt för GraphQL. Se KB-artikeln [405 Fel tillåts inte](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## Spärrad av avsändare {#blocked-dispatcher}

Om GraphQL-slutpunkten returnerar `404` fel vid publicering för `POST` -begäranden, det betyder att GraphQL-frågor blockeras på dispatchernivå och att slutpunkten måste aktiveras manuellt.

Detta bör inte vara fallet som standard, men en anpassad dispatcherkonfiguration kan orsaka problemet. Se mer under [Dispatcher - slutpunktskonfiguration med AEM Headless](/help/headless/deployment/dispatcher.md).
