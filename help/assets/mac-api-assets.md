---
title: HTTP API för Assets
description: Skapa, läsa, uppdatera, ta bort, hantera digitala resurser med HTTP API i [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API,APIs
role: Developer,Architect,Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager Assets] HTTP-API {#assets-http-api}

## Översikt {#overview}

The [!DNL Assets] HTTP-API:t gör det möjligt att skapa, läsa, uppdatera och ta bort (CRUD) på digitala resurser, inklusive metadata, återgivningar och kommentarer, samt strukturerat innehåll med [!DNL Experience Manager] Innehållsfragment. Den exponeras vid `/api/assets` och implementeras som REST API. Den innehåller [stöd för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md).

Så här kommer du åt API:

1. Öppna API-tjänstdokumentet på `https://[hostname]:[port]/api.json`.
1. Följ [!DNL Assets] tjänstlänk som leder till `https://[hostname]:[server]/api/assets.json`.

API-svaret är en JSON-fil för vissa MIME-typer och en svarskod för alla MIME-typer. JSON-svaret är valfritt och kanske inte är tillgängligt, till exempel för PDF-filer. Använd svarskoden för ytterligare analyser eller åtgärder.

>[!NOTE]
>
>Alla API-anrop som rör överföring eller uppdatering av resurser eller binära filer i allmänhet (som återgivningar) är föråldrade [!DNL Experience Manager] som [!DNL Cloud Service] distribution. Använd för att överföra binära filer [API:er för direkt binär överföring](developer-reference-material-apis.md#asset-upload) i stället.

## Innehållsfragment {#content-fragments}

A [Innehållsfragment](/help/assets/content-fragments/content-fragments.md) är en särskild typ av tillgång. Den kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum. Som det finns flera skillnader mellan `standard` resurser (t.ex. bilder eller dokument), kan vissa ytterligare regler gälla för hantering av innehållsfragment.

Mer information finns i [Stöd för innehållsfragment i [!DNL Experience Manager Assets] HTTP-API](/help/assets/content-fragments/assets-api-content-fragments.md).

## Datamodell {#data-model}

The [!DNL Assets] HTTP API visar två huvudelement, mappar och resurser (för standardresurser). Dessutom visas mer detaljerade element för anpassade datamodeller som beskriver strukturerat innehåll i innehållsfragment. Se [Datamodeller för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) för ytterligare information.

### Mappar {#folders}

Mappar är som kataloger som i de traditionella filsystemen. Mappen kan bara innehålla resurser, bara mappar eller mappar och resurser. Mappar har följande komponenter:

**Enheter**: Enheterna i en mapp är dess underordnade element, som kan vara mappar och resurser.

**Egenskaper**:

* `name` är namnet på mappen. Detta är samma som det sista segmentet i URL-sökvägen utan tillägget.
* `title` är en valfri mapptitel som kan visas i stället för dess namn.

>[!NOTE]
>
>Vissa egenskaper för mapp eller resurs är mappade till ett annat prefix. The `jcr` prefix för `jcr:title`, `jcr:description`och `jcr:language` ersätts med `dc` prefix. I den returnerade JSON-koden `dc:title` och `dc:description` innehåller värdena för `jcr:title` och `jcr:description`, respektive.

**Länkar** I mapparna visas tre länkar:

* `self`: Länka till sig själv.
* `parent`: Länka till den överordnade mappen.
* `thumbnail`: (Valfritt) länka till en mappminiatyrbild.

### Assets {#assets}

I [!DNL Experience Manager] en resurs innehåller följande element:

* Resursens egenskaper och metadata.
* Ursprungligen överförd binär fil för resursen.
* Flera renderingar enligt konfigurationen. Det kan vara bilder med olika storlek, videoklipp med olika kodningar eller extraherade sidor från PDF eller [!DNL Adobe InDesign] filer.
* Valfria kommentarer.

Mer information om element i innehållsfragment finns i [Stöd för innehållsfragment i Experience Manager Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md).

I [!DNL Experience Manager] en mapp har följande komponenter:

* Enheter: Resursernas underordnade är dess återgivningar.
* Egenskaper.
* Länkar.

## Tillgängliga funktioner {#available-features}

The [!DNL Assets] HTTP API innehåller följande funktioner:

* [Hämta en mapplista](#retrieve-a-folder-listing).
* [Skapa en mapp](#create-a-folder).
* [Skapa en resurs (inaktuell)](#create-an-asset)
* [Uppdatera resursens binärfil (borttagen)](#update-asset-binary).
* [Uppdatera metadata för resurs](#update-asset-metadata).
* [Skapa en resursåtergivning](#create-an-asset-rendition).
* [Uppdatera en resursåtergivning](#update-an-asset-rendition).
* [Skapa en resurskommentar](#create-an-asset-comment).
* [Kopiera en mapp eller resurs](#copy-a-folder-or-asset).
* [Flytta en mapp eller resurs](#move-a-folder-or-asset).
* [Ta bort en mapp, resurs eller återgivning](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>För att underlätta läsbarheten utelämnar följande exempel de fullständiga cURL-noteringarna. Kommentaren korrelerar med [Återställ](https://github.com/micha/resty) som är en skriptwrapper för cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Hämta en mapplista {#retrieve-a-folder-listing}

Hämtar en siren-representation av en befintlig mapp och av dess underordnade enheter (undermappar eller resurser).

**Begäran**: `GET /api/assets/myFolder.json`

**Svarskoder**: Svarskoderna är:

* 200 - OK - framgång.
* 404 - HITTADES INTE - mappen finns inte eller är inte tillgänglig.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

**Svar**: Klassen för enheten som returneras är en resurs eller en mapp. Egenskaperna för enheter som ingår är en deluppsättning av alla egenskaper för varje enhet. För att få en fullständig representation av enheten bör kunderna hämta innehållet i den URL som länken pekar på med en `rel` av `self`.

## Skapa en mapp {#create-a-folder}

Skapar en `sling`: `OrderedFolder` vid den angivna sökvägen. If `*` anges i stället för ett nodnamn, används parameternamnet som nodnamn. I begäran godkänns något av följande:

* En siren-representation av den nya mappen
* En uppsättning namn/värde-par, kodade som `application/www-form-urlencoded` eller `multipart`/ `form`- `data`. Dessa är användbara när du vill skapa en mapp direkt från ett HTML-formulär.

Mappens egenskaper kan också anges som URL-frågeparametrar.

Ett API-anrop misslyckas med en `500` svarskod om den överordnade noden för den angivna sökvägen inte finns. Ett anrop returnerar en svarskod `409` om mappen finns.

**Parametrar**: `name` är mappnamnet.

**Begäran**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Svarskoder**: Svarskoderna är:

* 201 - SKAPAD - när den skapades.
* 409 - CONFLICT - om det finns en mapp.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Skapa en resurs {#create-an-asset}

Se [överföring av resurser](developer-reference-material-apis.md) om du vill ha information om hur du skapar en resurs. Du kan inte skapa en resurs med HTTP API.

## Uppdatera en resurbinär {#update-asset-binary}

Se [överföring av resurser](developer-reference-material-apis.md) om du vill ha information om hur du uppdaterar resursbinärfiler. Du kan inte uppdatera en resursinbinär fil med HTTP API.

## Uppdatera metadata för en resurs {#update-asset-metadata}

Uppdaterar egenskaperna för resursmetadata. Om du uppdaterar någon egenskap i `dc:` namnutrymme, uppdaterar API-gränssnittet samma egenskap i `jcr` namnutrymme. API:t synkroniserar inte egenskaperna under de två namnutrymmena.

**Begäran**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Svarskoder**: Svarskoderna är:

* 200 - OK - Om resursen har uppdaterats utan fel.
* 404 - HITTADES INTE - Om det inte gick att hitta eller få åtkomst till resursen på angiven URI.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Skapa en resursåtergivning {#create-an-asset-rendition}

Skapa en återgivning för en resurs. Om parameternamnet för begäran inte anges används filnamnet som återgivningsnamn.

**Parametrar**: Parametrarna är `name` för renderingens namn och `file` som en filreferens.

**Begäran**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Svarskoder**

* 201 - SKAPAD - om återgivningen har skapats.
* 404 - HITTADES INTE - Om det inte gick att hitta eller få åtkomst till resursen på angiven URI.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Uppdatera en resursåtergivning {#update-an-asset-rendition}

Uppdateringarna ersätter en resursåtergivning med nya binära data.

**Begäran**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Svarskoder**: Svarskoderna är:

* 200 - OK - Om återgivningen har uppdaterats.
* 404 - HITTADES INTE - Om det inte gick att hitta eller få åtkomst till resursen på angiven URI.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Lägga till en kommentar till en resurs {#create-an-asset-comment}

**Parametrar**: Parametrarna är `message` för kommentarens meddelandetext och `annotationData` för anteckningsdata i JSON-format.

**Begäran**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Svarskoder**: Svarskoderna är:

* 201 - SKAPAD - om kommentaren har skapats.
* 404 - HITTADES INTE - Om det inte gick att hitta eller få åtkomst till resursen på angiven URI.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Kopiera en mapp eller en resurs {#copy-a-folder-or-asset}

Kopierar en mapp eller resurs som är tillgänglig på den angivna sökvägen till ett nytt mål.

**Begäranrubriker**: Parametrarna är:

* `X-Destination` - en ny mål-URI inom API-lösningens omfång att kopiera resursen till.
* `X-Depth` - antingen `infinity` eller `0`. Använda `0` kopierar bara resursen och dess egenskaper och inte dess underordnade.
* `X-Overwrite` - Användning `F` för att förhindra att en resurs skrivs över på det befintliga målet.

**Begäran**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Svarskoder**: Svarskoderna är:

* 201 - SKAPAD - om mappen/resursen har kopierats till ett icke-befintligt mål.
* 204 - INGET INNEHÅLL - om mappen/resursen har kopierats till ett befintligt mål.
* 412 - PRECONDITION MISSLYCKADES - om ett begärandehuvud saknas.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Flytta en mapp eller en resurs {#move-a-folder-or-asset}

Flyttar en mapp eller resurs vid den angivna sökvägen till ett nytt mål.

**Begäranrubriker**: Parametrarna är:

* `X-Destination` - en ny mål-URI inom API-lösningens omfång att kopiera resursen till.
* `X-Depth` - antingen `infinity` eller `0`. Använda `0` kopierar bara resursen och dess egenskaper och inte dess underordnade.
* `X-Overwrite` - Använd antingen `T` för att tvinga bort befintliga resurser eller `F` för att förhindra att en befintlig resurs skrivs över.

**Begäran**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Svarskoder**: Svarskoderna är:

* 201 - SKAPAD - om mappen/resursen har kopierats till ett icke-befintligt mål.
* 204 - INGET INNEHÅLL - om mappen/resursen har kopierats till ett befintligt mål.
* 412 - PRECONDITION MISSLYCKADES - om ett begärandehuvud saknas.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Ta bort en mapp, en resurs eller en återgivning {#delete-a-folder-asset-or-rendition}

Tar bort en resurs (-tree) vid den angivna sökvägen.

**Begäran**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Svarskoder**: Svarskoderna är:

* 200 - OK - Om mappen har tagits bort.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Tips, metodtips och begränsningar {#tips-limitations}

* Efter [!UICONTROL Off Time], är en resurs och dess återgivningar inte tillgängliga via [!DNL Assets] webbgränssnitt och via HTTP API. API:t returnerar 404-felmeddelande om [!UICONTROL On Time] kommer i framtiden eller [!UICONTROL Off Time] har redan varit.

* Resursens HTTP API returnerar inte alla metadata. Namnutrymmena är hårdkodade och endast dessa namnutrymmen returneras. Fullständiga metadata finns i resurssökvägen `/jcr_content/metadata.json`.

* Vissa egenskaper för mapp eller resurs mappas till ett annat prefix när de uppdateras med API:er. The `jcr` prefix för `jcr:title`, `jcr:description`och `jcr:language` ersätts med `dc` prefix. I den returnerade JSON-koden `dc:title` och `dc:description` innehåller värdena för `jcr:title` och `jcr:description`, respektive.

**Se även**

* [Översätt resurser](translate-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Referensdokument för utvecklare för [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

