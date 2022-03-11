---
title: Aktivera JSON-export för en komponent
description: Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Aktivera JSON-export för en komponent {#enabling-json-export-for-a-component}

Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.

## Översikt {#overview}

JSON-exporten baseras på [Sling Models](https://sling.apache.org/documentation/bundles/models.html)och på [Export av försäljningsmodell](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) som i sig förlitar sig på [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Det innebär att komponenten måste ha en Sling-modell om den behöver exportera JSON. Därför måste du följa dessa två steg för att aktivera JSON-export för alla komponenter.

* [Definiera en segmentmodell för komponenten](#define-a-sling-model-for-the-component)
* [Anteckna gränssnittet för segmenteringsmodellen](#annotate-the-sling-model-interface)

## Definiera en delningsmodell för komponenten {#define-a-sling-model-for-the-component}

Först måste en segmentmodell definieras för komponenten.

>[!NOTE]
>
>Ett exempel på hur du använder modeller finns i artikeln [Utveckla export av försäljningsmodeller i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Implementeringsklassen för Sling-modellen måste kommenteras med följande:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Detta garanterar att komponenten kan exporteras fristående med `.model` väljaren och `.json` tillägg.

Dessutom anger detta att klassen Sling Model kan anpassas till `ComponentExporter` gränssnitt.

>[!NOTE]
>
>Jackson-anteckningar anges vanligtvis inte på klassnivå för Sling Model, utan på gränssnittsnivå för Model. Detta för att säkerställa att JSON-exporten betraktas som en del av komponent-API:t.

>[!NOTE]
>
>The `ExporterConstants` och `ComponentExporter` klasserna kommer från `com.adobe.cq.export.json` paket.

### Använda flera väljare {#multiple-selectors}

Även om det inte är ett standardanvändningsfall är det möjligt att konfigurera flera väljare förutom `model` väljare.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

I sådana fall gäller dock att `model` väljaren måste vara den första väljaren och tillägget måste vara `.json`.

## Anteckna gränssnittet för segmenteringsmodellen {#annotate-the-sling-model-interface}

Modellgränssnittet bör implementera `ComponentExporter` gränssnitt (eller `ContainerExporter`, om det är en behållarkomponent).

Motsvarande Sling Model-gränssnitt (`MyComponent`) kommenteras sedan med [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) för att definiera hur den ska exporteras (serialiseras).

Modellgränssnittet måste kommenteras ordentligt för att definiera vilka metoder som ska serialiseras. Som standard kommer alla metoder som respekterar den vanliga namnkonventionen för get-ters att serialiseras och härleder sina JSON-egenskapsnamn naturligt från get-namnen. Detta kan förhindras eller åsidosättas med `@JsonIgnore` eller `@JsonProperty` för att byta namn på JSON-egenskapen.

## Exempel {#example}

[Kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) stöder JSON-export och kan användas som referens.

Ett exempel finns i Sling Model-implementeringen av Image Core-komponenten och dess kommenterade gränssnitt.

## Relaterad dokumentation {#related-documentation}

Mer information finns i:

* [Content Fragments in the Assets user guide](/help/assets/content-fragments/content-fragments.md)
* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och [Innehållsfragmentkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
