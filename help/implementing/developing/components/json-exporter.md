---
title: JSON-exporterare för innehållstjänster
description: AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor. De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder.
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: 89f23a590338561b4cfeb10b54a260a135ec2f08
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

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

Inom AEM levereras med väljaren `model` och `.json` tillägg.

`.model.json`

1. En URL som:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Levererar innehåll som:

   ![JSON-modell för WKND-innehåll](assets/json-model-wknd.png)

Du kan också leverera innehållet i ett strukturerat innehållsfragment genom att specifikt rikta in det på det.

Detta görs med hela sökvägen till fragmentet (via `jcr:content`), till exempel med ett suffix som

`.../jcr:content/root/container/container/contentfragment.model.json`

Sidan kan innehålla antingen ett enda innehållsfragment eller flera komponenter av olika typer. Du kan också använda funktioner som listkomponenter för att automatiskt söka efter relevant innehåll.

* En URL som:

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* Levererar innehåll som:

  ![JSON-modell för WKND-innehållsfragment](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >Du kan [anpassa era egna komponenter](enabling-json-exporter.md) för att få tillgång till och använda dessa data.

  >[!NOTE]
  >
  >Även om det inte är en standardimplementering [flera väljare stöds,](enabling-json-exporter.md#multiple-selectors) men `model` måste vara den första.

### Ytterligare information {#further-information}

* Resurser för HTTP API
   * [Resurser för HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling Models:
   * [Sling Models - Associera en modellklass med en resurstyp sedan 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM med JSON:
   * [Aktivera JSON-export för en komponent](enabling-json-exporter.md)

## Relaterad dokumentation {#related-documentation}

* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [Skapa med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och [Innehållsfragmentkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
