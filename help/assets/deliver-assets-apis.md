---
title: Leverans-API:er
description: Lär dig hur du använder leverans-API:erna.
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Leverans-API:er {#delivery-apis}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media med funktionsguiden OpenAPI finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Dynamic Media med OpenAPI-funktionshandboken PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Alla [godkända resurser](approve-assets.md) som är tillgängliga i resurskatalogen för Experience Manager kan [genomsökas](search-assets-api.md) och sedan levereras till integrerade program längre fram i kedjan med en leverans-URL.

Ändringar som görs i godkända resurser i DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i leverans-URL:erna. Med ett kort TTL-värde (Time-to-Live) på 10 minuter konfigurerat för mediedistribution via CDN blir uppdateringarna synliga i alla redigerings- och publiceringsgränssnitt på mindre än 10 minuter.

Följande bild visar tillgängliga URL:er för leverans:

![Leverans-API:er](assets/delivery-url.png)

I följande tabell visas hur de olika tillgängliga leverans-API:erna används:

| Leverans-API | Beskrivning |
|---|---|
| [Webboptimerad binär representation av resursen i begärt utdataformat](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | Returnerar den webboptimerade binära återgivningen av resursen i det begärda utdataformatet baserat på det resurs-ID som skickades i begäran. Dessutom kan du definiera olika bildmodifierare som bredd, höjd, rotering, vändning, kvalitet, beskärning, format och [smart beskärning](/help/assets/dynamic-media/image-profiles.md). Se [API-informationen](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) för de format och bildmodifierare som stöds.<br>Adobe rekommenderar att du använder detta API för alla bildformattyper. |
| [Webboptimerad binär representation av resursen](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | Bekvämt API som tillämpar standardvärden för webboptimerad binär representation av resursen som returneras i svaret. Standardvärdena är JPEG/WEBP, quality => 65 och width => 1024. |
| [Ursprungligt överfört binärt värde för resursen](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | Returnerar resursens ursprungligen överförda binärfiler. Adobe rekommenderar att du använder detta API för dokumentformat och SVG-bilder. |
| [Förgenererad återgivning av resursen som är tillgänglig i AEM Assets-redigeringsmiljö](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | Returnerar resursåtergivningens bitström som är tillgänglig i AEM Assets redigeringsmiljö baserat på det resurs-ID och återgivningsnamn som skickats i begäran. |
| [Resursmetadata](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | Returnerar egenskaperna som är kopplade till en resurs, till exempel titel, beskrivning, CreateDate, ModifyDate och så vidare. |
| [Spelarbehållare för videoresursen](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | Returnerar videoresursens spelarbehållare. Du kan bädda in spelaren i i ett iframe HTML-element och spela upp videon. |
| [Uppspelningsmanifest i det valda utdataformatet](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | Returnerar uppspelningsmanifestfilen för den angivna videoresursen i det valda utdataformatet. Du måste skapa en anpassad spelare som kan hantera adaptiv strömning via HLS- eller DASH-protokoll för att kunna hämta uppspelningsmanifestfilen och spela upp videon. |

## Slutpunkter för leverans-API:er {#delivery-apis-endpoint}

API-slutpunkterna varierar för varje leverans-API. API-slutpunkten för `Web-optimized binary representation of the asset in the requested output format` API är till exempel:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

Leveransdomänen har liknande struktur som Experience Manager författarmiljöns domän. Den enda skillnaden är att termen `author` ersätts med `delivery`.

`pXXXX` refererar till program-ID

`eYYYY` refererar till miljö-ID

Mer information finns i [API-information](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets).

## Begärandemetod för leverans-API:er {#delivery-api-request-method}

GET

## Rubrik för leverans-API {#deliver-assets-api-header}

Du måste ange följande information när du definierar en rubrik i huvudet för leverans-API:er:

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

Om du vill anropa leverans-API:erna krävs en IMS-token i `Authorization`-informationen för att leverera en begränsad resurs. IMS-token hämtas från ett tekniskt konto. Se [Hämta AEM as a Cloud Service-autentiseringsuppgifter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) för att skapa ett nytt tekniskt konto. Se [Generera åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) för att generera IMS-token och använda den korrekt i huvud för förfrågan-API:er för leverans.


Om du vill visa exempel på förfrågningar, svarsexempel och svarskoder läser du [Leverans-API:er](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat).
