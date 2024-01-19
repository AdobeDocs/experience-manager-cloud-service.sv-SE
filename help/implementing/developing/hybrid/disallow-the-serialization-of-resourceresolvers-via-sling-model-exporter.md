---
title: Tillåt inte serialisering av ResourceResolvers via Sling Model Exporter
description: Tillåt inte serialisering av ResourceResolvers via Sling Model Exporter
source-git-commit: 4543a4646719f8433df7589b21344433c43ab432
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Tillåt inte serialisering av ResourceResolvers via Sling Model Exporter {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Med exportfunktionen för segmenteringsmodeller kan du serialisera objekt för delningsmodeller till ett JSON-format. Den här funktionen används ofta eftersom den gör det möjligt för SPA (program med en sida) att enkelt komma åt data från AEM. På implementeringssidan används Jacson-databasbiblioteket för att serialisera dessa objekt.

Serialiseringen är en rekursiv åtgärd. Med början från ett&quot;rotobjekt&quot; itererar programmet rekursivt igenom alla giltiga objekt och serialiserar dem och deras underordnade objekt. Du kan hitta en beskrivning av vilka fält som är serialiserade i [den här artikeln](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Den här metoden serialiserar alla typer av objekt till JSON, och naturligt nog kan den också serialisera en Sling `ResourceResolver` -objektet, om det omfattas av serialiseringsreglerna. Detta är problematiskt eftersom `ResourceResolver` Tjänsten (och därför även det serviceobjekt som representerar den) innehåller potentiellt känslig information, som inte bör offentliggöras. Till exempel:

* Användar-ID
* Sökvägarna som du vill lösa relativa sökvägar
* The `propertyMap`.

Specialkänslig är `propertyMap` (se API-dokumentationen för [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), eftersom det är en intern datastruktur, som kan användas för många syften - till exempel cachelagra objekt som har samma livscykel som `ResourceResolver`. Serialisering av dessa kan läcka implementeringsdetaljer och kan ha en inverkan på säkerheten, eftersom data exponeras som inte ska vara läsbara och tillgängliga för slutanvändaren. Av den anledningen `ResourceResolvers` ska inte serialiseras till JSON.

Adobe planerar att inaktivera serialiseringen av `ResourceResolvers` i två steg:

1. Från och med AEM as a Cloud Service version 14697, när en `ResourceResolver` är serialiserat AEM loggar ett varningsmeddelande. Alla kunder uppmanas att söka i sina programloggar efter dessa loggsatser och anpassa sin kodbas därefter.
1. Vid ett senare tillfälle inaktiverar Adobe serialiseringen av ResourceResolvers som JSON.

## Implementering {#implementation}

WARN-meddelandet loggas både i AEM as a Cloud Service och lokala AEM SDK-instanser och ser ut så här:

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Det här loggmeddelandet innebär att under serialiseringen av `/content/…/page` till JSON a `ResourceResolver` har redan serialiserats. Genom att begära `/content/../page.model.json` du kan kontrollera exakt var fälten i `ResourceResolver` visas och använder det för att identifiera klassen Sling Model som faktiskt aktiverar det här beteendet.


>[!NOTE]
>
>AEM kärnkomponenter har verifierats så att de inte påverkas av det här problemet.

## Begärd åtgärd {#requested-action}

Adobe ber alla sina kunder att kontrollera sina programloggar och kodbaser för att se om de påverkas av problemet och ändra det anpassade programmet där det behövs, så att detta WARN-meddelande inte visas längre.

I de flesta fall antas dessa ändringar vara raka framifrån, eftersom `ResourceResolver` -objekt är inte obligatoriska i JSON-utdata alls, eftersom informationen som finns där vanligtvis inte krävs av klientprogram. Det innebär att det i de flesta fall bör räcka att utesluta `ResourceResolver` -objektet inte beaktas av Jackson (se [regler](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

Om en Sling-modell påverkas av det här problemet men inte ändras, inaktiveras serialiseringen av `ResourceResolver` -objektet (som det körs av Adobe som det andra steget) framtvingar en ändring i JSON-utdata.



