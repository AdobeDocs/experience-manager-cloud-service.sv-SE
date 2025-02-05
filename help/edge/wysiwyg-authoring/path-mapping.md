---
title: Banmappning för Edge Delivery Services
description: Lär dig hur du mappar sidsökvägar som används i AEM till offentliga sidsökvägar som används på webbplatsen och styr vilket innehåll som publiceras till Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Banmappning för Edge Delivery Services {#path-mapping}

Lär dig hur du mappar sidsökvägar som används i AEM till offentliga sidsökvägar som används på webbplatsen och styr vilket innehåll som publiceras till Edge Delivery Services.

## Ökning {#overview}

Om du vill kunna skapa WYSIWYG-innehåll med AEM och publicera det till Edge Delivery Services måste du konfigurera projektets sökvägsmappning. Mappningen har två syften.

* Den mappar och skapar en relation mellan de sidsökvägar som används i AEM och de offentliga sidsökvägar som används på webbplatsen.
* Det styr vilket innehåll (sidor, ark, resurser osv.) som publiceras till Edge Delivery Services.

Sökvägsmappningen måste konfigureras individuellt för varje projekt och enligt projektets innehåll och URL-struktur. Den används av AEM vid innehållspublicering och vid redigering av innehåll i [Universal Editor](/help/sites-cloud/authoring/universal-editor/navigation.md).

## Konfigurationsformat {#configuration-format}

Formatet för sökvägsmappningskonfigurationen innehåller två avsnitt (`mappings` och `includes`) som i följande exempel.

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### mappningar {#mappings}

Konfigurationen `mappings` innehåller en matris med interna sökvägar (i AEM redigeringsinstans) och externa URL-sökvägar (på den offentliga webbplatsen).

Formatet är `<internal paths>:<external path>`. Det består vanligtvis av minst två poster.

1. Den första posten från exemplet är sökvägsmappningen för webbplatssidorna.
1. Den andra posten styr mappningen av `.helix/config.json` till motsvarande kalkylbladssida i AEM.

I det här exemplet är alla sidor som lagras under `/content/aem-boilerplate/...` tillgängliga för allmänheten på webbplatsen Edge Delivery Services direkt under `https://main--my-site--org.aem.live/....`.

>[!TIP]
>
>Alla tabelldata som hanteras som kalkylblad (t.ex. metadata, omdirigeringar och taxonomi) publiceras vanligtvis som `.json` API-URL:er på Edge Delivery Services. Om du vill göra det måste de listas individuellt i mappningskonfigurationen.
>
>Mer information finns i dokumentet [Använda kalkylblad för att hantera tabelldata](/help/edge/wysiwyg-authoring/tabular-data.md).

### inkluderar {#includes}

Konfigurationen `includes` kontrollerar vilka innehållssökvägar som faktiskt replikeras till Edge Delivery Services. Den kan innehålla alla typer av sökvägar och innehåller vanligtvis platsernas rotsida på den översta nivån.

Assets som används på Edge Delivery Services publiceras vanligtvis tillsammans med webbsidan. De exporteras automatiskt från AEM till Edge Delivery Services.

>[!TIP]
>
>Om du har ett användningsfall där du vill att resurser ska publiceras direkt till Edge Delivery Services (du vill t.ex. att bilder eller PDF ska vara direkt tillgängliga via deras URL:er utanför en sidkontext), måste du även lägga till DAM-sökvägarna i `includes`-avsnittet i konfigurationen.
>
>Om till exempel en resursens rotmapp, som `/content/dam/my-site/documents`, som innehåller en uppsättning PDF ska vara tillgänglig för allmänheten via `/assets/...`, måste en post läggas till i avsnittet `includes` i konfigurationen.

## Konfigurera {#how-to-configure}

Sökvägsmappningar kan konfigureras på ett av två sätt beroende på hur projektet är konfigurerat.

1. Om projektet har konfigurerats för `aem.live` och använder [konfigurationstjänsten](https://www.aem.live/docs/config-service-setup) för centraliserade konfigurationer, konfigureras sökvägsmappningen för varje plats via den här konfigurationstjänsten.

   * Här är ett exempel på en cURL-begäran för att konfigurera sökvägsmappningar.

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. Om projektet inte använder konfigurationstjänsten konfigureras sökvägsmappningen via en `paths.json`-fil i GitHub-databasen för dina projekt.

   * Se [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) för ett exempel.

I båda fallen kan du kontrollera konfigurationen via den offentliga konfigurations-URL:en `https://<branch>--<site>--<org>.aem.page/config.json` när du har konfigurerat dina sökvägsmappningar.
