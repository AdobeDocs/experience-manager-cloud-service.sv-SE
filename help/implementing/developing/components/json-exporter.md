---
title: JSON-exporterare för innehållstjänster
description: AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor. De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder.
translation-type: tm+mt
source-git-commit: 02d95b7c45cb4d6d2fbfd9699690ecc1b80e1202
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---


# JSON-exporterare för innehållstjänster {#json-exporter-for-content-services}

AEM Content Services är utformat för att generalisera beskrivningen och leveransen av innehåll i/från AEM utanför webbsidornas fokus.

De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* Enkelsidiga program
* Inbyggda mobilprogram
* Andra kanaler och kontaktpunkter som inte är AEM

Med innehållsfragment som använder strukturerat innehåll kan du tillhandahålla innehållstjänster genom att använda JSON-exporteraren för att leverera innehållet på en (y) AEM sida i JSON-datamodellsformat. Detta kan sedan användas av dina egna program.

## JSON-exporterare med kärnkomponenter för innehållsfragment {#json-exporter-with-content-fragment-core-components}

Med den AEM JSON-exporteraren kan du leverera innehållet på en (y) AEM-sida i JSON-datamodellsformat. Detta kan sedan användas av dina egna program.

Inom AEM levereras med väljaren `model` och `.json` tillägget.

`.model.json`

1. En URL som:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Levererar innehåll som:

   ![JSON-modell för WKND-innehåll](/help/implementing/developing/introduction/assets/json-model-wknd.png)

Du kan också leverera innehållet i ett strukturerat innehållsfragment genom att specifikt rikta in det på det.

Detta görs med hela sökvägen till fragmentet (via `jcr:content`), till exempel med ett suffix som

`.../jcr:content/root/container/container/contentfragment.model.json`

Sidan kan innehålla antingen ett enda innehållsfragment eller flera komponenter av olika typer. Du kan också använda funktioner som listkomponenter för att automatiskt söka efter relevant innehåll.

* En URL som:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* Levererar innehåll som:

   ![JSON-modell för WKND-innehållsfragment](/help/implementing/developing/introduction/assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >Ni kan [anpassa era egna komponenter](enabling-json-exporter.md) för att få tillgång till och använda dessa data.

   >[!NOTE]
   >
   >Även om det inte är en standardimplementering stöds [flera väljare,](enabling-json-exporter.md#multiple-selectors) men `model` måste vara den första.

### Ytterligare information {#further-information}

Se även:

* HTTP API för Assets
   * [HTTP API för Assets](/help/assets/developer-reference-material-apis.md)
* Sling Models:
   * [Sling Models - Associera en modellklass med en resurstyp sedan 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM med JSON:
   * [Aktivera JSON-export för en komponent](enabling-json-exporter.md)

## Related Documentation {#related-documentation}

Mer information finns i:

* [Content Fragments in the Assets user guide](/help/assets/content-fragments/content-fragments.md)
* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och komponenten [Innehållsfragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
