---
title: Aktivera JSON-export för en komponent
description: Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 4%

---


# Aktivera JSON-export för en komponent {#enabling-json-export-for-a-component}

Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.

## Översikt {#overview}

JSON-exporten baseras på [Sling Models](https://sling.apache.org/documentation/bundles/models.html)och på [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (som i sin tur bygger på [Jackson-anteckningar](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Det innebär att komponenten måste ha en Sling-modell om den behöver exportera JSON. Därför måste du följa dessa två steg för att aktivera JSON-export för alla komponenter.

* [Definiera en segmentmodell för komponenten](#define-a-sling-model-for-the-component)
* [Anteckna gränssnittet för segmenteringsmodellen](#annotate-the-sling-model-interface)

## Definiera en delningsmodell för komponenten {#define-a-sling-model-for-the-component}

Först måste en segmentmodell definieras för komponenten.

>[!NOTE]
>
>Ett exempel på hur du använder delningsmodeller finns i artikeln [Developing Sling Model Exporters in AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Implementeringsklassen för Sling-modellen måste kommenteras med följande:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Detta garanterar att komponenten kan exporteras fristående med hjälp av väljaren och `.model` `.json` tillägget.

Dessutom anger detta att klassen Sling Model kan anpassas till `ComponentExporter` gränssnittet.

>[!NOTE]
>
>Jackson-anteckningar anges vanligtvis inte på klassnivå för Sling Model, utan på gränssnittsnivå för Model. Detta för att säkerställa att JSON-exporten betraktas som en del av komponent-API:t.

>[!NOTE]
>
>Klasserna `ExporterConstants` och `ComponentExporter` kommer från `com.adobe.cq.export.json` paketet.

### Använda flera väljare {#multiple-selectors}

Även om det inte är ett standardanvändningsfall är det möjligt att konfigurera flera väljare förutom `model` väljaren.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

I så fall måste dock väljaren vara den första väljaren och tillägget måste vara `model` `.json`.

## Anteckna gränssnittet för segmenteringsmodellen {#annotate-the-sling-model-interface}

Modellgränssnittet bör implementera gränssnittet (eller, `ComponentExporter` `ContainerExporter`om det är en behållarkomponent) för att det ska kunna beaktas av JSON-exportramverket.

Motsvarande Sling Model-gränssnitt (`MyComponent`) kommenteras sedan med [Jackson-anteckningar](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) för att definiera hur det ska exporteras (serialiseras).

Modellgränssnittet måste kommenteras ordentligt för att definiera vilka metoder som ska serialiseras. Som standard kommer alla metoder som respekterar den vanliga namnkonventionen för get-ters att serialiseras och härleder sina JSON-egenskapsnamn naturligt från get-namnen. Detta kan förhindras eller åsidosättas med `@JsonIgnore` eller `@JsonProperty` för att byta namn på JSON-egenskapen.

## Exempel {#example}

[Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) stöder JSON-export och kan användas som referens.

Ett exempel finns i Sling Model-implementeringen av Image Core-komponenten och dess kommenterade gränssnitt.

## Related Documentation {#related-documentation}

Mer information finns i:

* [Content Fragments in the Assets user guide](/help/assets/content-fragments/content-fragments.md)
* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och komponenten [Innehållsfragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
