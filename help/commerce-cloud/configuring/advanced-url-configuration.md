---
title: Avancerade URL-konfigurationer
description: Lär dig hur du anpassar URL:er för produkt- och kategorisidor. Detta gör att implementeringar kan optimera URL:er för sökmotorer och främja identifiering.
sub-product: Handel
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 490a93cfcfdac5ba209e52b1de3e1f823e80d26f
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 2%

---

# Avancerade URL-konfigurationer {#url}

[AEM CIF Core ](https://github.com/adobe/aem-core-cif-components) Components innehåller avancerade konfigurationer för att anpassa URL:er för produkt- och kategorisidor. Många implementeringar anpassar dessa URL:er för sökmotoroptimering (SEO).  Följande video visar hur du konfigurerar tjänsten `UrlProvider` och funktionerna i [Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att anpassa URL:er för produkt- och kategorisidor.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Konfiguration {#configuration}

Om du vill konfigurera tjänsten `UrlProvider` enligt SEO-kraven och behöver ett projekt måste det tillhandahålla en OSGI-konfiguration för konfigurationen för CIF URL-providern.

>[!NOTE]
>
> Sedan version 2.0.0 av AEM CIF Core Components finns det bara fördefinierade url-format i URL-providerkonfigurationen, i stället för det kostnadsfria format som kan konfigureras från 1.x-versioner. Dessutom har användningen av väljare för att skicka data i URL-adresser ersatts med suffix.

### Produktsidans URL-format {#product}

Detta konfigurerar URL:erna för produktsidorna och stöder följande alternativ:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (standard)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

där, i fallet [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)

* `{{page}}` ersätts med  `/content/venia/us/en/products/product-page`
* `{{sku}}` ersätts med produktens sku, t.ex.  `VP09`
* `{{url_key}}` ersätts med produktens  `url_key` egendom, t.ex.  `lenora-crochet-shorts`
* `{{url_path}}` ersätts med produktens  `url_path`, t.ex.  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` ersätts med den aktuella varianten, t.ex.  `VP09-KH-S`

Med exempeldata ovan kommer en produktvariant-URL som är formaterad med standard-URL-formatet att se ut som `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### URL-format för kategorisida {#product-list}

Detta konfigurerar URL:erna för kategori- eller produktlistsidorna och stöder följande alternativ:

* `{{page}}.html/{{url_path}}.html` (standard)
* `{{page}}.html/{{url_key}}.html`

där, i fallet [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)

* `{{page}}` ersätts med  `/content/venia/us/en/products/category-page`
* `{{url_key}}` ersätts av kategorins  `url_key` egenskap
* `{{url_path}}` ersätts av kategoriens  `url_path`

Med exempeldata ovan kommer en kategorisidas URL-adress som är formaterad med standardformatet för URL att se ut som `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> `url_path` är en sammanfogning av `url_keys` för en produkts eller kategorins överordnade och produktens eller kategorins `url_key` avgränsade med `/`-snedstreck.

## Anpassade URL-format {#custom-url-format}

Om ett projekt ska tillhandahålla ett anpassat URL-format kan det implementera gränssnittet [`UrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html) och registrera implementeringen som en OSGI-tjänst, med det antingen som kategorisida eller som URL-format för produktsida. Egenskapen `UrlFormat#PROP_USE_AS` för tjänsten anger vilket av de fördefinierade formaten som ska ersättas:

* `useAs=productPageUrlFormat`, ersätter det konfigurerade URL-formatet för produktsidan
* `useAs=categoryPageUrlFormat`, ersätter det konfigurerade URL-formatet för kategorisidan

Om det finns flera implementeringar av `UrlFormat` som är registrerade som OSGI-tjänster ersätter den med den högre rangordningen den med den lägre rangordningen.

`UrlFormat` måste implementera ett par metoder för att skapa en URL från en given parameterkarta och tolka en URL för att returnera samma parameterkarta. Parametrarna är desamma som beskrivs ovan, endast för kategorier anges ytterligare en `{{uid}}`-parameter till `UrlFormat`.

## Kombinera med delningskartor {#sling-mapping}

Förutom `UrlProvider` är det även möjligt att konfigurera [delningskartor](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att skriva om och bearbeta URL:er. Det AEM Archetype-projektet innehåller också [en exempelkonfiguration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) för att konfigurera vissa Sling Mappings för port 4503 (publicera) och 80 (dispatcher).

## Kombinera med AEM Dispatcher {#dispatcher}

URL-omskrivningar kan också utföras med AEM Dispatcher HTTP-server med modulen `mod_rewrite`. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) innehåller en referens AEM Dispatcher-konfiguration som redan innehåller grundläggande [omskrivningsregler](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) för den genererade storleken.

## Exempel

I [Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia)-projektet finns exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor. På så sätt kan varje projekt konfigurera individuella URL-mönster för produkt- och kategorisidor efter sina SEO-behov. En kombination av CIF `UrlProvider` och Sling Mappings enligt beskrivningen ovan används.

>[!NOTE]
>
>Den här konfigurationen måste justeras med den externa domän som används av projektet. Samlingsmappningarna fungerar baserat på värdnamnet och domänen. Den här konfigurationen är därför inaktiverad som standard och måste aktiveras före distributionen. Om du vill göra det byter du namn på mappen Sling Mapping `hostname.adobeaemcloud.com` i `ui.content/src/main/content/jcr_root/etc/map.publish/https` enligt det domännamn som används och aktiverar den här konfigurationen genom att lägga till `resource.resolver.map.location="/etc/map.publish"` i `JcrResourceResolver`-konfigurationen för projektet.

## Ytterligare resurser

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
