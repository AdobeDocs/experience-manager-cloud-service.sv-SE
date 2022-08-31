---
title: API-referensmaterial
description: AEM har omfattande och kraftfulla API:er som ni kan använda för ert digitala upplevelseprojekt.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 3%

---

# API-referensmaterial {#api-reference-materials}

Adobe Experience Manager (AEM) innehåller många API:er för utveckling av program och utökning av AEM. AEM bygger på ett antal öppen källkod-tekniker som också kan utnyttjas.

## AEM Core API:er {#core-aem-apis}

Följande API:er är viktiga för AEM.

| API | Beskrivning |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Produktabstraktioner som sidor, resurser, arbetsflöden osv. |
| [Granite-gränssnitt](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe&#39;s Open Web stack, med olika viktiga komponenter (Observera att 6.5 Granite-material gäller för AEMaaCS) |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe visuella stil för molngränssnitt som är utformade för att ge en konsekvent användarupplevelse |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## Ytterligare ramar {#additional-apis}

AEM förlitar sig på ett antal andra API:er med öppen källkod.

| API | Beskrivning |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Webbramverk som använder en Java Content Repository (JCR) för att lagra och hantera innehåll |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementera en skalbar och högpresterande hierarkisk Java Content Repository (JCR) som kan användas som grund för moderna webbplatser i världsklass |
| [Java Content Repository](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Specifikation för JCR version 2.0 |
| [Apache Felix](https://felix.apache.org) | Implementering av Open Services Gateway-initiativet (OSGi) och serviceplattformen |

## Riktlinjer för API-inställningar {#guidelines}

AEM bygger på följande fyra primära Java API-uppsättningar i fallande prioritetsordning.

| Prioritet | API | Beskrivning |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Produktabstraktioner som sidor, resurser, arbetsflöden osv. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST och resursbaserade abstraktioner som resurser, värdescheman och HTTP-begäranden. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Data- och innehållsabstraktioner som nod, egenskaper och sessioner. |
| 4 | [Apache Felix](https://felix.apache.org/) | OSSGi-programbehållarabstraktioner som tjänster och OSGi-komponenter. |

Om ett API tillhandahålls av AEM bör du föredra det framför Sling, JCR och OSGi. Om AEM inte har något API bör du välja Sling framför JCR och OSGi.

>[!TIP]
>
>Mer information om dessa riktlinjer finns i dokumentet [Förstå Java API-metodtips.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## AEM Delivery and Content Management Services and APIs {#delivery-apis}

AEM erbjuder anpassningsbara komponenter och alternativ för innehållsleverans.

| Funktion | Beskrivning |
|---|---|
| [Kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | Standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser |
| [JSON-exporterare](/help/implementing/developing/components/json-exporter.md) | Leverera innehåll från alla AEM sidor i JSON-datamodellformat |
| [Aktivera JSON-export för en komponent](/help/implementing/developing/components/enabling-json-exporter.md) | Generera JSON-export av komponentinnehåll baserat på ett modellramverk |
| [Resurs-API](/help/assets/mac-api-assets.md) | Möjliggör åtgärder för att skapa/läsa-uppdatera-ta bort (CRUD) på resurser, inklusive binära filer, metadata, återgivningar och kommentarer. Se AEM Assets HTTP API |
| [HTTP API för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md) | Få åtkomst till innehåll i innehållsfragment direkt via HTTP API via CRUD-åtgärder |
| [Content Fragment GraphQL API](/help/headless/graphql-api/content-fragments.md) | Möjliggör effektiv leverans av innehållsfragment till JavaScript-klienter i headless CMS-implementationer |
| [Content Fragments Assets HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | Exakt format för HTTP-resursbegäranden som stöds |

## SPA-specifika API:er {#spa-apis}

AEM SDK-ramverket (Single-Page Application (SPA) Editor innehåller specifika JavaScript API-referenser.

| API | Beskrivning |
|---|---|
| [Komponentmappning](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Ett sätt för Single Page-programmet att mappa klientkomponenter till Adobe Experience Manager-resurstyper (AEM komponenter) |
| [Sidmodellshanteraren](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | En tolk mellan Adobe Experience Manager Editor och Adobe Experience Manager Single Page Application (SPA) Editor |
| [Reagera på redigerbara komponenter](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Innehåller React-komponenter och integreringslager som hjälper dig att komma igång med Adobe Experience Manager Site Editor |
| [Redigerbara komponenter för angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Innehåller komponenterna i Angularna och integreringslagret som hjälper dig att komma igång med Adobe Experience Manager Site Editor |

>[!TIP]
>
>Kolla in [SPA introduktion och genomgång](/help/implementing/developing/hybrid/introduction.md) för mer information om enkelsidiga program.
