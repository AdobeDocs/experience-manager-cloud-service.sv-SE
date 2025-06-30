---
title: Integrera resursväljaren med API:t för Dynamic Media-öppning
description: Integrera resursväljare med olika program från Adobe, andra företag än Adobe och tredje part.
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# Integrering av Dynamic Media med OpenAPI-funktioner {#integrate-asset-selector-dynamic-media-open-apis}

Med resursväljaren kan du integrera med olika Adobe-program så att de kan fungera tillsammans sömlöst.

## Förutsättningar {#prereqs-polaris}

Använd följande krav om du integrerar resursväljare med dynamiska media med OpenAPI-funktioner:

* [Kommunikationsmetoder](/help/assets/overview-asset-selector.md#prereqs)
* För att få tillgång till Dynamic Media med OpenAPI-funktioner måste du ha licenser för:
   * Assets-arkiv (till exempel Experience Manager Assets as a Cloud Service).
   * AEM Dynamic Media.
* Endast [godkända resurser](/help/assets/approve-assets.md) är tillgängliga för användning för att säkerställa varumärkets enhetlighet.

## Integrering av Dynamic Media med OpenAPI-funktioner {#adobe-app-integration-polaris}

Integrering av resursväljare med Dynamic Media OpenAPI-process omfattar olika steg som skapar en anpassad dynamisk medie-URL eller är klar att välja dynamisk medie-URL, osv.

### Integrera resursväljare för dynamiska media med OpenAPI-funktioner {#integrate-dynamic-media}

Egenskaperna `rootPath` och `path` ska inte ingå i Dynamic Media med OpenAPI-funktioner. I stället kan du konfigurera egenskapen `aemTierType`. Här följer syntaxen för konfiguration:

```
aemTierType:[1: "delivery"]
```

Med den här konfigurationen kan du visa alla godkända resurser utan mappar eller som en platt struktur. Mer information får du om du går till egenskapen `aemTierType` under [Resursväljarens egenskaper](/help/assets/asset-selector-properties.md).


### Skapa en dynamisk leverans-URL från godkända resurser {#create-dynamic-media-url}

När du har konfigurerat resursväljaren används ett objektschema för att skapa en dynamisk leverans-URL från de valda resurserna.
Ett schema med ett objekt från en array med objekt som tas emot när en resurs väljs:

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

Alla markerade resurser bärs av funktionen `handleSelection` som fungerar som ett JSON-objekt. Exempel: `JsonObj`. Den dynamiska leverans-URL:en skapas genom att följande bärare kombineras:

| Objekt | JSON |
|---|---|
| Värd | `assetJsonObj["repo:repositoryId"]` |
| API-rot | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| format | `.jpg` |

#### Godkänd specifikation för tillgångsleverans-API {#approved-assets-delivery-api-specification}

URL:
`https://<delivery-api-host>/adobe/assets/<asset-id>/as/<seo-name>.<format>?<image-modification-query-parameters>`

Var,

* Värddatorn är `https://delivery-pxxxxx-exxxxxx.adobe.com`
* API-roten är `"/adobe/assets"`
* `<asset-id>` är tillgångsidentifierare
* `as` är den konstanta delen av en öppen API-specifikation som anger vad resursen ska kallas
* `<seo-name>` är namnet på en resurs
* `<format>` är utdataformatet
* `<image modification query parameters>` stöds av den godkända resursens leverans-API-specifikation

#### Godkänt material Ursprungligt återgivnings-API {#approved-assets-delivery-api}

Den dynamiska leverans-URL:en har följande syntax:
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`, där,

* Värddatorn är `https://delivery-pxxxxx-exxxxxx.adobe.com`
* API-roten för ursprunglig återgivningsleverans är `"/adobe/assets"`
* `<asset-id>` är tillgångsidentifierare
* `/original/as` är den konstanta delen av en öppen API-specifikation som anger vilken ursprunglig återgivning som ska kallas
* `<seo-name>` är namnet på resursen som kan ha ett tillägg eller inte

### Redo att välja dynamisk leverans-URL {#ready-to-pick-dynamic-delivery-url}

Alla markerade resurser bärs av funktionen `handleSelection` som fungerar som ett JSON-objekt. Exempel: `JsonObj`. Den dynamiska leverans-URL:en skapas genom att följande bärare kombineras:

| Objekt | JSON |
|---|---|
| Värd | `assetJsonObj["repo:repositoryId"]` |
| API-rot | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

Nedan visas två sätt att gå igenom JSON-objektet:

![Dynamisk leverans-URL](assets/dynamic-delivery-url.png)

* **Miniatyrbild:** Miniatyrbilder kan vara bilder och resurser som PDF, video, bilder och så vidare. Även om du kan använda attributen height och width för en resurs miniatyrbild som dynamisk leveransåtergivning.
Följande uppsättning återgivningar kan användas för PDF-typresurser:
När du har valt en PDF-fil i en sidospark visas nedanstående information i urvalssammanhanget. Här nedan beskrivs hur du går igenom JSON-objektet:

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  Du kan referera till `selection[0].....selection[4]` för arrayen med återgivningslänk från skärmbilden ovan. Nyckelegenskaperna för en av miniatyrbildsrenderingarna är till exempel:

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

På skärmbilden ovan måste leveransadressen för den ursprungliga PDF-återgivningen införlivas i målversionen om PDF krävs och inte i dess miniatyrbild. Exempel: `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **Video:** Du kan använda videospelarens URL för videomaterialet som använder en inbäddad iFrame. Du kan använda följande arrayåtergivningar i målupplevelsen:
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/DragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  Du kan referera till `selection[0].....selection[4]` för arrayen med återgivningslänk från skärmbilden ovan. Nyckelegenskaperna för en av miniatyrbildsrenderingarna är till exempel:

  Kodfragmentet i skärmbilden ovan är ett exempel på en videoresurs. Den innehåller en array med återgivningslänkar. `selection[5]` i utdraget är ett exempel på en miniatyrbild som kan användas som platshållare för videominiatyrbilden i målupplevelsen. `selection[5]` i återgivningens array är för videospelaren. Detta fungerar som en HTML och kan anges som `src` för iframe. Den stöder strömning med adaptiv bithastighet, som är webboptimerad leverans av videon.

  I exemplet ovan är videospelarens URL `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

### Konfigurera anpassade filter {#configure-custom-filters-dynamic-media-open-api}

Med resursväljaren för Dynamic Media med OpenAPI-funktioner kan du konfigurera anpassade egenskaper och de filter som baseras på dem. Egenskapen `filterSchema` används för att konfigurera sådana egenskaper. Anpassningen kan visas som `metadata.<metadata bucket>.<property name>.` som filtren kan konfigureras mot, där,

* `metadata` är information om en resurs
* `embedded` är den statiska parametern som används för konfiguration, och
* `<propertyname>` är det filternamn som du konfigurerar

Egenskaper som definieras på `jcr:content/metadata/`-nivå visas som `metadata.<metadata bucket>.<property name>.` för de filter som du vill konfigurera för konfigurationen.

I Resursväljaren för dynamiska media med OpenAPI-funktioner konverteras till exempel en egenskap på `asset jcr:content/metadata/client_name:market` till `metadata.embedded.client_name:market` för filterkonfiguration.

En engångsaktivitet måste göras för att hämta namnet. Gör ett söknings-API-anrop för resursen och hämta egenskapsnamnet (i stort sett).

### Användargränssnitt för resursväljare för Dynamic Media med OpenAPI-funktioner {#interface-dynamic-media-open-api}

Efter integrering med Adobe Micro-Frontend Asset Selector kan du bara se resursstrukturen för alla godkända resurser som är tillgängliga i Experience Manager resurskatalog.

![Dynamiska media med OpenAPI-funktioner, användargränssnitt](assets/polaris-ui.png)

* **A**: Visa/Göm panel
* **B**: Assets
* **C**: Sortering
* **D**: Filter
* **E**: Sökfältet
* **F**: Sortera i stigande eller fallande ordning
* **G**: Avbryt markering
* **H**: Markera en eller flera resurser

>[!NOTE]
>
>Mappar stöds bara vid anslutning till en författardatabas, inte dynamiska medier med OpenAPI-databas.

>[!MORELIKETHIS]
>
>* [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
>* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
>* [Anpassningar av resursväljare](/help/assets/asset-selector-customization.md)
