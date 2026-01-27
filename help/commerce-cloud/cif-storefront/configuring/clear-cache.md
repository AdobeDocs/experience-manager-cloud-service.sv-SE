---
title: Cachelagring för komponenter och GraphQL
description: Lär dig hur du aktiverar och verifierar funktionen för rensning av cache i AEM CIF.
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
index: false
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Cachelagring för komponenter och GraphQL {#clear-cache}

Det här dokumentet innehåller en omfattande guide om hur du aktiverar och verifierar funktionen för rensning av cache i AEM CIF.

>[!NOTE]
>
> Den här funktionen är experimentell.

## Aktivera funktionen Rensa cache i CIF-konfigurationen {#enable-clear-cache}

Som standard är funktionen för rensning av cache inaktiverad i CIF-konfigurationen. Om du vill aktivera det måste du lägga till följande i dina motsvarande projekt:

* Aktivera servern `/bin/cif/invalidate-cache` som hjälper dig att utlösa API:t för rensning av cache med deras motsvarande begäranden genom att lägga till konfigurationen `com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json` i ditt projekt enligt [här.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json)

  >[!NOTE]
  >
  > Konfiguration behöver bara aktiveras för författarinstanserna.

* Gör det möjligt för avlyssnaren att rensa cacheminnet från varje instans av AEM (publicera och författare) genom att lägga till konfigurationen `com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json` i ditt projekt så som visas [här.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)
   * Konfiguration ska vara aktiverat för både författare och publiceringsinstanser.
   * Aktivera Dispatcher-cachen (valfritt): du kan aktivera inställningen för rensningscache för dispatcher genom att ange egenskapen `enableDispatcherCacheInvalidation` till true i ovanstående konfiguration. Detta innehåller funktioner för att rensa cacheminnet från dispatchern.

     >[!NOTE]
     >
     > Detta fungerar bara med publiceringsinstanser.

   * Se även till att du anger motsvarande mönster som passar din produkt, kategori och CMS-sida måste läggas till i ovanstående konfigurationsfil för att den ska kunna tas bort från dispatchercachen.

* Om du vill förbättra prestanda för SQL-frågor för att hitta motsvarande sida som är relaterad till produkten och kategorin lägger du till motsvarande index i projektet (rekommenderas). Mer information finns i [cifCacheInvalidationSupport.](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml)

## Verifierar funktionen Rensa cache {#verify-clear-cache}

Så här kontrollerar du att allt är korrekt konfigurerat:

* Trigga motsvarande server till Author Instance AEM, till exempel [http://localhost:4502/bin/CIF/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache), och du bör få ett 200 HTTP-svar.
* Kontrollera att en nod har skapats under följande sökväg i författarinstanser: `/var/cif/cacheinvalidation`. Nodnamnet följer mönstret: `cmd_{{timestamp}}`.
* Kontrollera att samma nod har skapats i varje publiceringsinstans.

För att kontrollera om cacheminnen rensas ordentligt:

1. Navigera till motsvarande PLP- och PDP-sidor.
2. Uppdatera ett produkt- eller kategorinamn i e-handelsmotorn. Ändringarna återspeglas inte direkt i AEM baserat på cachekonfigurationer.
3. Trigga serverletens API så här:

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ******' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

Om allt blir bra återspeglas de nya ändringarna i alla instanser. Om ändringarna inte visas i publiceringsinstansen kan du försöka komma åt relevanta PLP- och PDP-sidor i ett privat/inkognito-webbläsarfönster.

>[!NOTE]
>
> Publiceringsinstanser kan ha flera nivåer av cachelager. Funktionen ansvarar bara för rensning av cache från AEM interna minne och dispatcher.

## Rensa cache-invalidering-API {#clear-cache-api}

Det här är det API som du måste utlösa när du vill rensa cacheminnet för handelsrelaterade data från AEM.

Typ av begäran: `POST`

### Sidhuvuden {#headers}

| Parameter | Värde | Obligatoriskt/obligatoriskt | Kommentar |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | Obligatoriskt |  |
| `Authorization` | Motsvarande autentiseringsuppgifter för författare (autentiseringstyp: grundläggande autentisering) | Obligatoriskt | Lägg till motsvarande användarnamn och lösenord. |


### Nyttolast {#payload}

I följande tabell visas befintliga attribut som funktionen har. Dessa `InvalidateType`-egenskaper måste anges i kombination med obligatoriskt attribut (till exempel `storePath`).

| `invalidateType` | Värde | Typ (Array/String/Boolean) | Rensa dispatchercachen? | Kommentar |
|------------------------------|-------------------|---|---|---|
| `productSkus` | Produktens sku - som måste ogiltigförklaras från cachen. | Array | Ja | Rensa cacheminnet från det interna minnet med följande mönster:<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>Rensa PDP-sidcachen för motsvarande SKU</li><li>Rensa cacheminnet för motsvarande kategorisida där de finns (baserat på grafiskt svar från e-handel)</li><li>Rensa cacheminne baserat på följande fråga:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | Kategorins uid - som måste ogiltigförklaras från cachen. | Array | Ja | Rensa cacheminnet från det interna minnet med följande mönster:<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>Rensa cacheminnet för kategorisidor för motsvarande data (inklusive dess underordnade kategorisida)</li><li>Rensa alla PDP-sidor som har motsvarande kategorier</li><li>Rensa cacheminne baserat på följande fråga:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | Om du behöver rensa GraphQL svarsdata baserat på regex-mönster ska du använda detta. | Array | Nej | |
| `cacheNames` | De här värdena definieras under motsvarande konfigurationskonfiguration för CIF GraphQL-klienten >> Motsvarande konfiguration för StorePath GraphQL >> cachekonfigurationer för GraphQL | Array | Nej | |
| `invalidateAll` | True eller false | Boolean | Ja | |

I den här tabellen visas den obligatoriska egenskapen som måste skickas i alla API-anrop:

| Egenskap | Värde | Typ (Array/String/Boolean) | Rensa dispatchercachen? | Kommentar |
|------------------------------|-------------------|---|---|---|
| `storePath` | Motsvarande värde för webbplatssökvägen där cachen måste tas bort (Exempel: `/content/venia/us/en` som referens med veniaprojekt). | Sträng | Ja | Detta måste anges med kombinationen av `invalidateType.` |

### Exempel på API-begäran {#sample-request}

```text
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ******' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## Utbyggbarhet {#clear-cache-extensibility}

Den här funktionen har inte bara basfunktioner utan också utbyggbarhet, vilket gör att utvecklare kan bygga vidare på och anpassa den ytterligare efter behov.

### Utöka befintligt attribut {#existing-attribute}

Om cacheminnet behöver rensas och inte täcks av den befintliga attributbaserade funktionen (till exempel `categoryUids`), kan du referera till [ den här referensfilen ](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java) för att lägga till nya mönster och definiera ytterligare `invalidatePaths` som ska rensas från cacheminnet utöver vad den aktuella implementeringen hanterar.

### Lägger till nytt anpassat attribut {#new-custom-attribute}

Om du till exempel inte vill använda det befintliga attributet för att rensa cachen, kan du skapa ett eget attribut och definiera dess motsvarande funktioner.

* Om du bara behöver rensa cacheminnet från AEM (graphql-svaret) måste du följa [den här referensen.](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java)
* Om du behöver rensa cache från det interna minnet och dispatchercachen måste du följa [den här referensen.](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java)

  >[!NOTE]
  >
  > Du kan ignorera den interna rensningscachen genom att returnera `null` för metoden `getPatterns()`.
