---
title: Avancerade URL-konfigurationer
description: Lär dig hur du anpassar URL:er för produkt- och kategorisidor. Detta gör att implementeringar kan optimera URL:er för sökmotorer och främja identifiering.
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 3ea19210049e49401da892021f098005759542a3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 6%

---

# Avancerade URL-konfigurationer {#url}

>[!NOTE]
>
> Sökmotoroptimering (SEO) har blivit en viktig fråga för många marknadsförare. Därför måste SEO-frågor hanteras i många Adobe Experience Manager (AEM) as a Cloud Service-projekt. Läs [Bästa praxis för hantering av SEO och URL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) för ytterligare information.

[AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) innehåller avancerade konfigurationer för att anpassa URL:er för produkt- och kategorisidor. Många implementeringar anpassar dessa URL:er för sökmotoroptimering (SEO). Följande video visar hur du konfigurerar `UrlProvider` Service och funktioner i [Samlingsmappning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att anpassa URL:er för produkt- och kategorisidor.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Konfiguration {#configuration}

Så här konfigurerar du `UrlProvider` i enlighet med SEO-kraven och ett projekt måste tillhandahålla en OSGI-konfiguration för CIF URL Provider-konfigurationen.

>[!NOTE]
>
> Sedan version 2.0.0 av de AEM CIF Core-komponenterna finns det bara fördefinierade url-format i URL-providerkonfigurationen, i stället för de format som kan konfigureras fritt från 1.x-versioner. Dessutom har användningen av väljare för att skicka data i URL-adresser ersatts med suffix.

### URL-format för produktsida {#product}

Detta konfigurerar URL:erna för produktsidorna och stöder följande alternativ:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (standard)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

När det gäller [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/product-page`
* `{{sku}}` ersätts med produktens sku, t.ex. `VP09`
* `{{url_key}}` ersätts av produktens `url_key` egenskap, t.ex. `lenora-crochet-shorts`
* `{{url_path}}` ersätts av produktens `url_path`, t.ex. `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` ersätts med den aktuella varianten, t.ex. `VP09-KH-S`

Med exempeldata ovan ser en produktvariant-URL som är formaterad med standardformatet för URL ut som `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### URL-format för kategorisida {#product-list}

Detta konfigurerar URL:erna för kategori- eller produktlistsidorna och stöder följande alternativ:

* `{{page}}.html/{{url_path}}.html` (standard)
* `{{page}}.html/{{url_key}}.html`

När det gäller [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/category-page`
* `{{url_key}}` ersätts av kategoriens `url_key` property
* `{{url_path}}` ersätts av kategoriens `url_path`

Med exempeldata ovan ser en kategorisidas URL-adress formaterad med standardformatet för URL-adresser ut som `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> The `url_path` är en sammanfogning av `url_keys` för en produkts eller kategoris överordnade och produkten eller kategorin `url_key` avgränsad med `/` snedstreck.

## Anpassade URL-format {#custom-url-format}

Ett projekt kan implementera det anpassade URL-formatet [`UrlFormat` gränssnitt](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html) och registrera implementeringen som en tjänst av allmänt ekonomiskt intresse, med den som kategorisida eller som webbsidesformat för produktsidor. The `UrlFormat#PROP_USE_AS` egenskapen service anger vilket av de fördefinierade formaten som ska ersättas:

* `useAs=productPageUrlFormat`, ersätter det konfigurerade URL-formatet för produktsidan
* `useAs=categoryPageUrlFormat`, ersätter det konfigurerade URL-formatet för kategorisidan

Om det finns flera implementeringar av `UrlFormat` som är registrerade som OSGI-tjänster ersätter den med den högre rankningen den med den lägre rankningen.

The `UrlFormat` måste implementera ett par metoder för att skapa en URL från en given parameterkarta och tolka en URL för att returnera samma parameterkarta. Parametrarna är desamma som beskrivs ovan, endast för kategorier och ytterligare `{{uid}}` parametern anges för `UrlFormat`.

## Kombinera med delningskartor {#sling-mapping}

Förutom `UrlProvider`går det också att konfigurera [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att skriva om och bearbeta URL:er. Det AEM Archetype-projektet innehåller även [en exempelkonfiguration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) om du vill konfigurera vissa kopplingsmappningar för port 4503 (publicera) och 80 (dispatcher).

## Kombinera med AEM Dispatcher {#dispatcher}

URL-omskrivningar kan också göras med AEM Dispatcher HTTP-server med `mod_rewrite` -modul. The [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) innehåller en referens AEM Dispatcher-konfiguration som redan innehåller grundläggande [skriv om regler](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) för den genererade storleken.

## Exempel {#example}

The [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia) projektet innehåller exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor. På så sätt kan varje projekt skapa individuella URL-mönster för produkt- och kategorisidor efter sina SEO-behov. En kombination av CIF `UrlProvider` och Samlingsmappningar enligt ovan används.

>[!NOTE]
>
>Den här konfigurationen måste justeras med den externa domän som används av projektet. Samlingsmappningarna fungerar baserat på värdnamnet och domänen. Den här konfigurationen är därför inaktiverad som standard och måste aktiveras före distributionen. Om du vill göra det byter du namn på kopplingsmappningen `hostname.adobeaemcloud.com` mapp i `ui.content/src/main/content/jcr_root/etc/map.publish/https` enligt det använda domännamnet och aktivera den här konfigurationen genom att lägga till `resource.resolver.map.location="/etc/map.publish"` till `JcrResourceResolver` projektets konfiguration.

## Ytterligare resurser {#additional}

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
