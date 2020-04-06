---
title: HTTP API för Assets
description: Lär dig mer om implementering, datamodell och funktioner i Assets HTTP API. Använd Assets HTTP API för att utföra olika åtgärder runt resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# HTTP API för Assets {#assets-http-api}

## Översikt {#overview}

Med Assets HTTP API kan du skapa/läsa/uppdatera/ta bort (CRUD)-åtgärder för resurser, inklusive binära, metadata, återgivningar och kommentarer, tillsammans med strukturerat innehåll med hjälp av AEM Content Fragments. Den exponeras vid `/api/assets` och implementeras som REST API. Det innehåller [stöd för innehållsfragment](content-fragments/content-fragments.md).

Så här kommer du åt API:

1. Öppna API-tjänstdokumentet på `https://[hostname]:[port]/api.json`.
1. Följ länkarna Resurstjänster till `https://[hostname]:[server]/api/assets.json`.

API-svaret är en JSON-fil för vissa MIME-typer och en svarskod för alla MIME-typer. JSON-svaret är valfritt och kanske inte är tillgängligt, till exempel för PDF-filer. Använd svarskoden för ytterligare analyser eller åtgärder.

Efter [!UICONTROL Av-tid]är en resurs och dess återgivningar inte tillgängliga vare sig via webbgränssnittet Resurser eller via HTTP-API:t. API:t returnerar 404-felmeddelande om [!UICONTROL På-tid] är i framtiden eller [!UICONTROL Av-tid] är i det förflutna.

>[!NOTE]
>
>Alla API-anrop som rör överföring eller uppdatering av resurser eller binära filer i allmänhet (som återgivningar) dedikeras för AEM som en distribution av molntjänster. Om du vill överföra binära filer ska du använda API:er för [direkt binär överföring](developer-reference-material-apis.md#asset-upload-technical) i stället.

## Innehållsfragment {#content-fragments}

Ett [innehållsfragment](content-fragments/content-fragments.md) är en särskild typ av resurs. Den kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum. Eftersom det finns flera skillnader mellan `standard` resurser (t.ex. bilder eller dokument) gäller vissa ytterligare regler för hantering av innehållsfragment.

Mer information finns i Stöd för [innehållsfragment i AEM Assets HTTP API](content-fragments/content-fragments.md).

## Datamodell {#data-model}

Resursens HTTP-API visar två huvudelement, mappar och resurser (för standardresurser).

Dessutom visas mer detaljerade element för anpassade datamodeller som beskriver strukturerat innehåll i innehållsfragment. Mer information finns i [Datamodeller](content-fragments/content-fragments.md) för innehållsfragment.

### Mappar {#folders}

Mappar är som kataloger i traditionella filsystem. De är behållare för andra mappar eller kontroller. Mappar har följande komponenter:

**Enheter**: Enheterna i en mapp är dess underordnade element, som kan vara mappar och resurser.

**Egenskaper**:
* `name`  — Namnet på mappen. Detta är samma som det sista segmentet i URL-sökvägen utan tillägget
* `title` — Valfri rubrik för mappen som kan visas i stället för dess namn

>[!NOTE]
>
>Vissa egenskaper för mapp eller resurs är mappade till ett annat prefix. Prefixet `jcr` , `jcr:title`och `jcr:description`ersätts med `jcr:language` `dc` prefix. I det returnerade JSON-objektet `dc:title` och `dc:description` innehåller därför värdena för `jcr:title` respektive `jcr:description`.

**Länkmappar** visar tre länkar:
* `self`: Länka till sig själv
* `parent`: Länka till överordnad mapp
* `thumbnail`: (Valfritt) länk till en mappminiatyrbild

### Assets {#assets}

I AEM innehåller en resurs följande element:

* Resursens egenskaper och metadata
* Flera återgivningar, till exempel den ursprungliga återgivningen (som är den ursprungliga överförda resursen), en miniatyrbild och olika andra återgivningar. Ytterligare återgivningar kan vara bilder av olika storlek, olika videokodningar eller extraherade sidor från PDF eller InDesign.
* Valfria kommentarer

Mer information om element i innehållsfragment finns i Stöd för [innehållsfragment i AEM Assets HTTP API](content-fragments/content-fragments.md).

I AEM har en mapp följande komponenter:

* Enheter: Resursens underordnade är dess renderingar.
* Egenskaper
* Länkar

Resursens HTTP-API innehåller följande funktioner:

* Hämta en mapplista
* Skapa en mapp
* Skapa en resurs (inaktuell)
* Uppdatera resursens binärfil (borttagen)
* Uppdatera metadata för resurs
* Skapa en resursåtergivning
* Uppdatera en resursåtergivning
* Skapa en resurskommentar
* Kopiera en mapp eller resurs
* Flytta en mapp eller resurs
* Ta bort en mapp, resurs eller återgivning

>[!NOTE]
>
>För att underlätta läsbarheten utelämnar följande exempel den fullständiga cURL-notationen. Faktum är att anteckningen korrelerar med [Resty](https://github.com/micha/resty) , som är en skriptwrapper för cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Hämta en mapplista {#retrieve-a-folder-listing}

Hämtar en siren-representation av en befintlig mapp och av dess underordnade enheter (undermappar eller resurser).

**Begäran**

```
GET /api/assets/myFolder.json
```

**Svarskoder**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**Svar**

Klassen för enheten som returneras är resurser/mapp.

Egenskaper för enheter som ingår är en deluppsättning av alla egenskaper för varje enhet. För att få en fullständig representation av enheten bör kunderna hämta innehållet i den URL som länken pekar på med en `rel` av `self`.

## Skapa en mapp {#create-a-folder}

Skapar en ny `sling`: `OrderedFolder` vid den angivna sökvägen. Om * anges i stället för ett nodnamn kommer serverleten att använda parameternamnet som nodnamn. Data accepteras som begäran antingen som en Siren-representation av den nya mappen eller som en uppsättning namn/värde-par, kodade som `application/www-form-urlencoded` eller `multipart`/ `form`- `data`, vilket är användbart när du skapar en mapp direkt från ett HTML-formulär. Dessutom kan mappens egenskaper anges som URL-frågeparametrar.

Åtgärden misslyckas med en `500` svarskod om den överordnade noden för den angivna sökvägen inte finns. Om mappen redan finns returneras en `409` svarskod.

**Parametrar**

* `name` - Mappnamn

**Begäran**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

eller

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**Svarskoder**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Skapa en resurs {#create-an-asset}

Mer information om hur du skapar en resurs med API:er finns i [Överför](developer-reference-material-apis.md) resurser. Det går inte att skapa en resurs med HTTP API.

## Uppdatera en resurbinär {#update-asset-binary}

Mer information om hur du uppdaterar resursbinärfiler med API:er finns i [Överför](developer-reference-material-apis.md) resurser. Uppdateringen av en resursinbinär fil med HTTP API är föråldrad.

## Uppdatera metadata för en resurs {#update-asset-metadata}

Uppdaterar egenskaperna för resursmetadata.

**Begäran**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**Svarskoder**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Skapa en resursåtergivning {#create-an-asset-rendition}

Skapar en ny resursåtergivning för en resurs. Om parameternamnet för begäran inte anges används filnamnet som återgivningsnamn.

**Parametrar**

* `name` - Återgivningsnamn
* `file` - Filreferens

**Begäran**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

eller

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**Svarskoder**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Uppdatera en resursåtergivning {#update-an-asset-rendition}

Uppdateringar ersätter en resursåtergivning med nya binära data.

**Begäran**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**Svarskoder**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Skapa en resurskommentar {#create-an-asset-comment}

Skapar en ny resurskommentar.

**Parametrar**

* `message` - Meddelande
* `annotationData` - Anteckningsdata (JSON)

**Begäran**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**Svarskoder**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Kopiera en mapp eller en resurs {#copy-a-folder-or-asset}

Kopierar en mapp eller resurs vid den angivna sökvägen till ett nytt mål.

**Begäranrubriker**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**Begäran**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**Svarskoder**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Flytta en mapp eller en resurs {#move-a-folder-or-asset}

Flyttar en mapp eller resurs vid den angivna sökvägen till ett nytt mål.

**Begäranrubriker**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**Begäran**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**Svarskoder**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Ta bort en mapp, en resurs eller en återgivning {#delete-a-folder-asset-or-rendition}

Tar bort en resurs (-tree) vid den angivna sökvägen.

**Begäran**

```
DELETE /api/assets/myFolder
```

eller

```
DELETE /api/assets/myFolder/myAsset.png
```

eller

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**Svarskoder**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

