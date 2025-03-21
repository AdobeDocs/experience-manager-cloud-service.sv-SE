---
title: ASSETS HTTP API
description: Skapa, läsa, uppdatera, ta bort, hantera digitala resurser med HTTP API i  [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---

# Hantera digitala resurser med HTTP-API:t [!DNL Adobe Experience Manager Assets]{#assets-http-api}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

## Kom igång med AEM [!DNL Assets] HTTP API {#overview}

HTTP-API:t för AEM [!DNL Assets] aktiverar CRUD-åtgärder (skapa, läsa, uppdatera och ta bort) för digitala resurser via ett REST-gränssnitt som finns på /`api/assets`. De här åtgärderna gäller metadata för resurser, återgivningar och kommentarer. Den innehåller [stöd för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
> Det finns en moderniserad OpenAPI-implementering av innehållets fragment Management API. Fullständig dokumentation finns i [API för hantering av innehållsfragment](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). Vi rekommenderar att du använder den nya OpenAPI-implementeringen. Den befintliga användningen av Assets HTTP API för innehållsfragment bör migreras till det nya OpenAPI:t för hantering av innehållsfragment.

Så här kommer du åt API:

1. Öppna API-tjänstdokumentet på `https://[hostname]:[port]/api.json`.
1. Följ tjänstlänkens radavstånd för [!DNL Assets] till `https://[hostname]:[server]/api/assets.json`.

API-svaret är en JSON-fil för vissa MIME-typer och en svarskod för alla MIME-typer. JSON-svaret är valfritt och kanske inte är tillgängligt, till exempel för PDF-filer. Använd svarskoden för ytterligare analyser eller åtgärder.

>[!NOTE]
>
>Alla API-anrop som rör överföring eller uppdatering av resurser eller binära filer i allmänhet (som återgivningar) är föråldrade för [!DNL Experience Manager] som en [!DNL Cloud Service]-distribution. Om du vill överföra binära filer använder du [API:er för direkt binär överföring](developer-reference-material-apis.md#asset-upload) i stället.

## Hantera innehållsfragment {#content-fragments}

Ett [innehållsfragment](/help/assets/content-fragments/content-fragments.md) är en strukturerad resurs som lagrar text, siffror och datum. Eftersom det finns flera skillnader mellan `standard`-resurser (t.ex. bilder eller dokument) gäller vissa ytterligare regler för hantering av innehållsfragment.

Mer information finns i [Stöd för innehållsfragment i  [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de koncept som ingår.
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

## Undersök datamodellen {#data-model}

HTTP-API:t [!DNL Assets] visar i första hand två element: mappar och standardresurser. Den innehåller även detaljerade element för anpassade datamodeller som används i innehållsfragment. Mer information finns i Datamodeller för innehållsfragment. Mer information finns i [Datamodeller för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments).

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

### Hantera mappar {#folders}

Mappar är som kataloger som i de traditionella filsystemen. Mappar kan innehålla resurser, undermappar eller både och. Mappar har följande komponenter:

**Entiteter**: Enheterna i en mapp är dess underordnade element, som kan vara mappar och resurser.

**Egenskaper**:

* `name`: Mappens namn (det sista segmentet i URL-sökvägen, utan tillägget).
* `title`: En valfri titel visas i stället för mappnamnet.

>[!NOTE]
>
>Vissa egenskaper för mapp eller resurs är mappade till ett annat prefix. Prefixet `jcr` för `jcr:title`, `jcr:description` och `jcr:language` ersätts med prefixet `dc`. I den returnerade JSON innehåller därför `dc:title` och `dc:description` värdena för `jcr:title` respektive `jcr:description`.

**Länkar**-mappar visar tre länkar:

* `self`: En länk till själva mappen.
* `parent`: En länk till den överordnade mappen.
* `thumbnail` (Valfritt): En länk till en mappminiatyrbild.

### Hantera resurser {#assets}

I [!DNL Experience Manager] innehåller en resurs följande element:

* **Egenskaper och metadata:** Beskrivande information om resursen.
* **Binär fil:** Den ursprungligen överförda filen.
* **Återgivningar:** Flera konfigurerade återgivningar (till exempel bilder i olika storlekar, olika videokodningar eller extraherade sidor från PDF-filer/Adobe InDesign-filer).
* **Kommentarer (valfritt):** Kommentarer från användaren.

Mer information om element i innehållsfragment finns i [Stöd för innehållsfragment i Experience Manager Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

I [!DNL Experience Manager] har en mapp följande komponenter:

* Enheter: De underordnade resurserna är dess återgivningar.
* Egenskaper.
* Länkar.

## Utforska tillgängliga API-åtgärder {#available-features}

HTTP-API:t [!DNL Assets] innehåller följande funktioner:

* [Hämta en mapplista](#retrieve-a-folder-listing).
* [Skapa en mapp](#create-a-folder).
* [Skapa en resurs (inaktuell)](#create-an-asset)
* [Uppdatera resursens binärfil (utgått)](#update-asset-binary).
* [Uppdatera resursmetadata](#update-asset-metadata).
* [Skapa en resursåtergivning](#create-an-asset-rendition).
* [Uppdatera en resursåtergivning](#update-an-asset-rendition).
* [Skapa en objektkommentar](#create-an-asset-comment).
* [Kopiera en mapp eller resurs](#copy-a-folder-or-asset).
* [Flytta en mapp eller resurs](#move-a-folder-or-asset).
* [Ta bort en mapp, resurs eller återgivning](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>För att underlätta läsbarheten utelämnar följande exempel de fullständiga cURL-noteringarna. Anteckningen korrelerar med [Resty](https://github.com/micha/resty) som är en skriptwrapper för cURL.

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

**Svar**: Klassen för entiteten som returneras är en resurs eller en mapp. Egenskaperna för enheter som ingår är en deluppsättning av alla egenskaper för varje enhet. Om du vill få en fullständig representation av entiteten måste klienterna hämta innehållet i den URL som länken pekar på med `rel` av `self`.

## Skapa en mapp {#create-a-folder}

Skapar en `sling`: `OrderedFolder` vid den angivna sökvägen. Om `*` anges i stället för ett nodnamn används parameternamnet som nodnamn. I begäran godkänns något av följande:

* En siren-representation av den nya mappen
* En uppsättning namn/värde-par, kodade som `application/www-form-urlencoded` eller `multipart`/ `form`- `data`. Dessa är användbara när du vill skapa en mapp direkt från ett HTML-formulär.

Mappens egenskaper kan också anges som URL-frågeparametrar.

Ett API-anrop misslyckas med en `500`-svarskod om den överordnade noden för den angivna sökvägen inte finns. Ett anrop returnerar svarskoden `409` om mappen finns.

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

Det går inte att skapa resurser via detta HTTP-API. Använd API:t för [överföring av resurser](developer-reference-material-apis.md) för att skapa resurser.

## Uppdatera en resurbinär {#update-asset-binary}

Mer information om hur du uppdaterar resursbinärfiler finns i [Överför resurser](developer-reference-material-apis.md). Du kan inte uppdatera en resursinbinär fil med HTTP API.

## Uppdatera metadata för en resurs {#update-asset-metadata}

Den här åtgärden uppdaterar resursens metadata. När egenskaper uppdateras i namnutrymmet `dc:` uppdateras motsvarande `jcr:`-egenskap. API:t synkroniserar dock inte egenskaperna under de två namnutrymmena.

**Begäran**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Svarskoder**: Svarskoderna är:

* 200 - OK - Om resursen har uppdaterats utan fel.
* 404 - HITTADES INTE - Om det inte gick att hitta eller få åtkomst till resursen på angiven URI.
* 412 - PRECONDITION MISSLYCKADES - om rotsamlingen inte kan hittas eller nås.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Skapa en resursåtergivning {#create-an-asset-rendition}

Skapa en återgivning för en resurs. Om parameternamnet för begäran inte anges används filnamnet som återgivningsnamn.

**Parametrar**: Parametrarna är:

`name`: för återgivningsnamnet.
`file`: Den binära filen för återgivningen som referens.

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

Kopierar en mapp eller en resurs som är tillgänglig på den angivna sökvägen till ett nytt mål.

**Begäranrubriker**: Parametrarna är:

* `X-Destination` - en ny mål-URI inom API-lösningsscopet som resursen ska kopieras till.
* `X-Depth` - antingen `infinity` eller `0`. Om du använder `0` kopieras bara resursen och dess egenskaper och inte dess underordnade.
* `X-Overwrite` - Använd `F` för att förhindra att en resurs skrivs över på det befintliga målet.

**Begäran**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Svarskoder**: Svarskoderna är:

* 201 - SKAPAD - om mappen/resursen har kopierats till ett icke-befintligt mål.
* 204 - INGET INNEHÅLL - om mappen/resursen har kopierats till ett befintligt mål.
* 412 - PRECONDITION MISSLYCKADES - om ett begärandehuvud saknas.
* 500 - INTERNT SERVERFEL - Om något annat går fel.

## Flytta en mapp eller en resurs {#move-a-folder-or-asset}

Flyttar en mapp eller resurs vid den angivna sökvägen till ett nytt mål.

**Begäranrubriker**: Parametrarna är:

* `X-Destination` - en ny mål-URI inom API-lösningsscopet som resursen ska kopieras till.
* `X-Depth` - antingen `infinity` eller `0`. Om du använder `0` kopieras bara resursen och dess egenskaper och inte dess underordnade.
* `X-Overwrite` - Använd antingen `T` för att framtvinga borttagning av befintliga resurser eller `F` för att förhindra att en befintlig resurs skrivs över.

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

## Följ vedertagna standarder och anteckningsbegränsningar {#tips-limitations}

* Assets och deras återgivningar blir otillgängliga via webbgränssnittet [!DNL Assets] och HTTP API när [!UICONTROL Off Time] nås. API:t returnerar ett 404-fel om [!UICONTROL On Time] finns i framtiden eller om [!UICONTROL Off Time] redan finns.

* Assets HTTP API returnerar bara en delmängd av metadata. Namnutrymmena är hårdkodade och endast dessa namnutrymmen returneras. Fullständiga metadata finns i resurssökvägen `/jcr_content/metadata.json`.

* Vissa egenskaper för mapp eller resurs mappas till ett annat prefix när de uppdateras med API:er. Prefixet `jcr` för `jcr:title`, `jcr:description` och `jcr:language` ersätts med prefixet `dc`. I den returnerade JSON innehåller därför `dc:title` och `dc:description` värdena för `jcr:title` respektive `jcr:description`.

**Utforska relaterade resurser**

* [Översätt Assets](translate-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Referensdokument för utvecklare för  [!DNL Assets]](/help/assets/developer-reference-material-apis.md)
