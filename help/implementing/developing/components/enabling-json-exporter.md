---
title: Aktivera JSON-export för en komponent
description: Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 07327f80b23e1e6fdbb3fb49d861221877724d39
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Aktivera JSON-export för en komponent {#enabling-json-export-for-a-component}

Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.

## Ökning {#overview}

JSON-exporten baseras på [Sling Models](https://sling.apache.org/documentation/bundles/models.html) och ramverket [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (som i sin tur är beroende av [Jackson-anteckningar](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Det innebär att komponenten måste ha en Sling-modell om den måste exportera JSON. Följ därför de här två stegen för att aktivera JSON-export för alla komponenter.

* [Definiera en segmentmodell för komponenten](#define-a-sling-model-for-the-component)
* [Anteckna gränssnittet för segmenteringsmodellen](#annotate-the-sling-model-interface)

## Definiera en delningsmodell för komponenten {#define-a-sling-model-for-the-component}

Först måste en segmentmodell definieras för komponenten.

>[!NOTE]
>
>Ett exempel på hur du använder segmentmodeller finns i artikeln [Developing Sling Model Exporters in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Implementeringsklassen för Sling-modellen måste kommenteras med följande:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Detta garanterar att din komponent kan exporteras fristående med väljaren `.model` och tillägget `.json`.

Detta anger dessutom att klassen Sling Model kan anpassas till gränssnittet `ComponentExporter`.

>[!NOTE]
>
>Jackson-anteckningar anges vanligtvis inte på klassnivå för Sling Model, utan på gränssnittsnivå för Model. Detta för att säkerställa att JSON-exporten betraktas som en del av komponent-API:t.

>[!NOTE]
>
>Klasserna `ExporterConstants` och `ComponentExporter` kommer från paketet `com.adobe.cq.export.json`.

### Använda flera väljare {#multiple-selectors}

Även om det inte är ett standardanvändningsfall går det att konfigurera flera väljare förutom väljaren `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

I så fall måste väljaren `model` vara den första väljaren och tillägget måste vara `.json`.

## Anteckna gränssnittet för segmenteringsmodellen {#annotate-the-sling-model-interface}

Modellgränssnittet bör implementera gränssnittet `ComponentExporter` (eller `ContainerExporter` om det är en behållarkomponent) för att JSON-exportramverket ska kunna användas.

Motsvarande Sling Model-gränssnitt (`MyComponent`) kommenteras sedan med [Jackson-anteckningar](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) för att definiera hur det ska exporteras (serialiseras).

Modellgränssnittet måste vara korrekt kommenterat för att definiera vilka metoder som ska serialiseras. Som standard serialiseras alla metoder som respekterar den vanliga namnkonventionen för get-ters och härleder deras JSON-egenskapsnamn naturligt från get-namnen. Detta kan förhindras eller åsidosättas med `@JsonIgnore` eller `@JsonProperty` för att byta namn på JSON-egenskapen.

## Exempel {#example}

[Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) stöder JSON-export och kan användas som referens.

Ett exempel finns i Sling Model-implementeringen av Image Core-komponenten och dess kommenterade gränssnitt.

## Relaterad dokumentation {#related-documentation}

* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Skapa med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och komponenten [Innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
