---
title: Leverans-API:er
description: Lär dig hur du använder leverans-API:erna.
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 9f7164e99abb6fce3b1bbc6401234996bcd43889
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Leverans-API:er {#delivery-apis}

Alla [godkända resurser](approve-assets.md) som är tillgängliga i Experience Manager-resurskatalogen kan [genomsökas](search-assets-api.md) och sedan levereras till integrerade underordnade program med en leverans-URL.

Ändringar som görs i godkända resurser i DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i leverans-URL:erna. Med ett kort TTL-värde (Time-to-Live) på 10 minuter konfigurerat för mediedistribution via CDN blir uppdateringarna synliga i alla redigerings- och publiceringsgränssnitt på mindre än 10 minuter.

Följande bild visar tillgängliga URL:er för leverans:

![Leverans-API:er](assets/delivery-url.png)

I följande tabell visas hur de olika tillgängliga leverans-API:erna används:

| Leverans-API | Beskrivning |
|---|---|
| [Webboptimerad binär representation av resursen i begärt utdataformat](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat) | Returnerar den webboptimerade binära återgivningen av resursen i det begärda utdataformatet baserat på det resurs-ID som skickades i begäran. Dessutom kan du definiera olika bildmodifierare, till exempel bredd, höjd, rotering, vändning, kvalitet, beskärning, format och [smart beskärning](/help/assets/dynamic-media/image-profiles.md). Se [API-informationen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat) för de format och bildmodifierare som stöds.<br>Adobe rekommenderar att du använder detta API för alla bildformattyper. |
| [Webboptimerad binär representation av resursen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAsset) | Bekvämt API som tillämpar standardvärden för en webboptimerad binär representation av resursen som returneras i svaret. Standardvärdena är JPEG/WEBP, quality => 65 och width => 1024. |
| [Ursprungligt överfört binärt värde för resursen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetOriginal) | Returnerar resursens ursprungligen överförda binärfiler. Adobe rekommenderar att du använder detta API för dokumentformat och SVG-bilder. |
| [Förgenererad återgivning av resursen som är tillgänglig i AEM Assets-redigeringsmiljö](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetRendition) | Returnerar resursåtergivningens bitström som är tillgänglig i AEM Assets redigeringsmiljö baserat på det resurs-ID och återgivningsnamn som skickats i begäran. |
| [Resursmetadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetMetadata) | Returnerar egenskaperna som är associerade med en resurs, till exempel titel, beskrivning, CreateDate, ModifyDate och så vidare. |
| [Spelarbehållare för videoresursen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/videoPlayerDelivery) | Returnerar videoresursens spelarbehållare. Du kan bädda in spelaren i i ett iframe HTML-element och spela upp videon. |
| [Uppspelningsmanifest i det valda utdataformatet](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/videoManifestDelivery) | Returnerar uppspelningsmanifestfilen för den angivna videoresursen i det valda utdataformatet. Du måste skapa en anpassad spelare som kan hantera adaptiv strömning via HLS- eller DASH-protokoll för att kunna hämta uppspelningsmanifestfilen och spela upp videon. |

>[!IMPORTANT]
>
>Du kan testa valfri modifierare, som vanligtvis inte är tillgänglig via experimentella API:er. Exempel: `</adobe/experimental/advancemodifiers-expires-YYYYMMDD/assets>`
>&#x200B;>Klicka här om du vill veta mer om hur du använder [experimentella API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/#experimental-apis) och den [fullständiga listan med modifierare](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

Dynamic Media med OpenAPI-funktioner har också stöd för videor med lång form. Videorna har stöd för upp till 50 GB och 2 timmar.

Information om tillgängliga Dynamic Media-erbjudanden och deras funktioner finns i [Dynamic Media Prime och Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

>[!NOTE]
>
>DM Prime-kunder kan använda grundläggande bildmodifierare som rotation, beskärning, vändning, höjd, bredd och kvalitet. Smart Imaging stöder inte AVIF för DM Prime-kunder.

## Slutpunkter för leverans-API:er {#delivery-apis-endpoint}

API-slutpunkterna varierar för varje leverans-API. API-slutpunkten för `Web-optimized binary representation of the asset in the requested output format` API är till exempel:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

Leveransdomänen har liknande struktur som Experience Manager författarmiljöns domän. Den enda skillnaden är att termen `author` ersätts med `delivery`.

`pXXXX` refererar till program-ID

`eYYYY` refererar till miljö-ID

Mer information finns i [API-information](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#tag/Assets).

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

Om du vill anropa leverans-API:erna krävs en IMS-token i `Authorization`-informationen för att leverera en begränsad resurs. IMS-token hämtas från ett tekniskt konto. Se [Hämta AEM as a Cloud Service-autentiseringsuppgifter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis) för att skapa ett nytt tekniskt konto. Se [Generera åtkomsttoken](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis) för att generera IMS-token och använda den korrekt i huvud för förfrågan-API:er för leverans.


Om du vill visa exempel på förfrågningar, svarsexempel och svarskoder läser du [Leverans-API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat).
