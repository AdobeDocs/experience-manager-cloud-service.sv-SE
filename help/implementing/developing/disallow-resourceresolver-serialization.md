---
title: Tillåt inte serialisering av ResourceResolvers via Sling Model Exporter
description: Tillåt inte serialisering av ResourceResolvers via Sling Model Exporter
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Tillåt inte serialisering av ResourceResolvers via Sling Model Exporter {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Med exportfunktionen för segmenteringsmodell kan du serialisera Sling Model-objekt till JSON-format. Den här funktionen används ofta eftersom den gör det möjligt för SPA (program med en sida) att enkelt komma åt data från AEM. På implementeringssidan används Jackson Database-biblioteket för att serialisera dessa objekt.

Serialiseringen är en rekursiv åtgärd. Med början från ett&quot;rotobjekt&quot; itererar det rekursivt igenom alla giltiga objekt och serialiserar dem och deras underordnade objekt. Du kan hitta en beskrivning av vilka fält som är serialiserade i artikeln [Jackson - Bestäm vilka fält som ska bli serialiserade/deserialiserade](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Den här metoden serialiserar alla typer av objekt till JSON. Det kan naturligtvis också serialisera ett Sling `ResourceResolver`-objekt, om det omfattas av serialiseringsreglerna. Detta är problematiskt eftersom tjänsten `ResourceResolver` (och därför även det serviceobjekt som representerar den) innehåller potentiellt känslig information, som inte bör avslöjas. Till exempel:

* Användar-ID
* Sökvägarna som du vill lösa relativa sökvägar
* `propertyMap`

Särskilt känslig är `propertyMap` (se API-dokumentationen för [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)) eftersom det är en intern datastruktur, som kan användas för många syften, till exempel cachelagra objekt som har samma livscykel som `ResourceResolver`. Serialisering av dessa kan läcka implementeringsdetaljer och kan ha en inverkan på säkerheten, eftersom data exponeras som inte ska vara läsbara och tillgängliga för slutanvändaren. Därför ska `ResourceResolvers` inte serialiseras till JSON.

Adobe planerar att inaktivera serialiseringen av `ResourceResolvers` i två steg:

1. Från och med AEM as a Cloud Service version 14697 loggar AEM ett varningsmeddelande när `ResourceResolver` är serialiserat. Alla kunder uppmanas att söka i sina programloggar efter dessa loggsatser och anpassa sin kodbas därefter.
1. Vid ett senare tillfälle inaktiverar Adobe serialiseringen av `ResourceResolver` som JSON.

## Implementering {#implementation}

WARN-meddelandet loggas både i AEM as a Cloud Service och lokala AEM SDK-instanser och ser ut så här:

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Det här loggmeddelandet innebär att `/content/…/page` redan är serialiserat under serialiseringen av JSON. `ResourceResolver` Genom att begära `/content/../page.model.json` kan du kontrollera exakt var fälten i `ResourceResolver` visas och använda den för att identifiera klassen Sling Model som faktiskt aktiverar det här beteendet.


>[!NOTE]
>
>[AEM kärnkomponenter](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/introduction) har verifierats att inte påverkas av det här problemet.

## Begärd åtgärd {#requested-action}

Adobe begär att alla kunder ska kontrollera sina programloggar och kodbaser för att se om de påverkas av problemet och ändra det anpassade programmet där det behövs, så att det här varningsmeddelandet inte längre visas i loggarna.

I de flesta fall antas dessa ändringar vara raka framifrån. Objekten `ResourceResolver` är inte obligatoriska i JSON-utdata alls eftersom informationen som finns där normalt inte krävs av klientprogram, vilket i de flesta fall innebär att det bör räcka att utesluta objektet `ResourceResolver` från att beaktas av Jackson (se [reglerna](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

Om en Sling Model påverkas av det här problemet, men inte ändras, kommer den explicita inaktiveringen av serialiseringen av `ResourceResolver`-objektet (som utförs av Adobe som det andra steget) att framtvinga en ändring i JSON-utdata.
