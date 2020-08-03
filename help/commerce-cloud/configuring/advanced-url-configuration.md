---
title: Avancerade URL-konfigurationer
description: Avancerade URL-konfigurationer
translation-type: tm+mt
source-git-commit: 3a235e3d8e2d97e413f445df1f0bfe52e97024b3
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Avancerade URL-konfigurationer {#url}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) innehåller avancerade konfigurationer för att anpassa URL:er för produkt- och kategorisidor. Många implementeringar anpassar dessa URL:er för sökmotoroptimering (SEO).  Följande video visar hur du konfigurerar `UrlProvider` tjänsten och funktionerna för [Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att anpassa URL:er för produkt- och kategorisidor.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Konfiguration {#configuration}

För att konfigurera `UrlProvider` tjänsten enligt SEO-kraven och kraven måste ett projekt tillhandahålla en OSGI-konfiguration för konfigurationen CIF URL Provider och konfigurera tjänsten enligt beskrivningen nedan.

>[!NOTE]
>
> I [projektet för Venia Reference store](https://github.com/adobe/aem-cif-guides-venia) (se nedan) finns exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor.

### URL-mall för produktsida {#product}

Detta konfigurerar URL:erna för produktsidorna med följande egenskaper:

* **Produkt-URL-mall**: definierar formatet för URL:er med en uppsättning platshållare. Standardvärdet är `{{page}}.{{url_key}}.html#{{variant_sku}}`, vilket resulterar i att URL:er genereras, till exempel `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange` där
   * `{{page}}` ersattes med `/content/venia/us/en/products/product-page`
   * `{{url_key}}` har ersatts av produktens Magento `url_key` -egenskap, här `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` har ersatts med den valda varianten här `MH01-M-Orange`
* **Produktidentifierarplats**: definierar platsen för den identifierare som ska användas för att hämta produktdata. Standardvärdet är `SELECTOR`, det andra möjliga värdet är `SUFFIX`. I föregående exempel-URL betyder det att identifieraren `chaz-kangeroo-hoodie` kommer att användas för att hämta produktdata.
* **Produktidentifierartyp**: definierar vilken typ av identifierare som ska användas när produktdata hämtas. Standardvärdet är `URL_KEY`, det andra möjliga värdet är `SKU`. Med den tidigare exempel-URL:en innebär det att produktdata kommer att hämtas med ett Magento GraphQL-filter som `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### URL-mall för produktlistsida {#product-list}

Detta konfigurerar URL:erna för kategori- eller produktlistsidorna med följande egenskaper:

* **Kategori-URL-mall**: definierar formatet för URL:er med en uppsättning platshållare. Standardvärdet är `{{page}}.{{id}}.html`, vilket resulterar i att URL:er genereras, till exempel `/content/venia/us/en/products/category-page.3.html` där
   * `{{page}}` ersattes med `/content/venia/us/en/products/category-page`
   * `{{id}}` har ersatts av egenskapen Magento `id` i kategorin här `3`
* **Kategoriidentifierarplats**: definierar platsen för den identifierare som ska användas för att hämta produktdata. Standardvärdet är `SELECTOR`, det andra möjliga värdet är `SUFFIX`. I föregående exempel-URL betyder det att identifieraren `3` kommer att användas för att hämta produktdata.
* **Kategoriidentifierartyp**: definierar vilken typ av identifierare som ska användas när produktdata hämtas. Standardvärdet och det värde som för närvarande bara stöds är `ID`. Med den tidigare exempel-URL:en innebär det att kategoridata kommer att hämtas med ett Magento GraphQL-filter som `category(id:3)`.

Det går att lägga till anpassade egenskaper för varje mall, förutsatt att motsvarande data ställs in av komponenterna med hjälp av `UrlProvider`. Kontrollera till exempel koden för `ProductListItemImpl` klassen för att ta reda på hur den implementeras.

Det går också att ersätta `UrlProvider` tjänsten med en helt anpassad OSGi-tjänst. I så fall måste du implementera gränssnittet och registrera det med en högre rankning för att kunna ersätta standardimplementeringen. `UrlProvider`

## Kombinera med delningskartor {#sling-mapping}

Förutom `UrlProvider`är det även möjligt att konfigurera [delningskartor](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att skriva om och bearbeta URL:er. Det AEM Archetype-projektet innehåller även [en exempelkonfiguration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) för att konfigurera vissa Sling Mappings för port 4503 (publicera) och 80 (dispatcher).

## Kombinera med AEM Dispatcher {#dispatcher}

URL-omskrivningar kan också göras med AEM Dispatcher HTTP-server med `mod_rewrite` modul. Den [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) innehåller en referens AEM Dispatcher config som redan innehåller grundläggande [skrivregler](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) för den genererade storleken.

## Exempel

I projektet [för Venedig Reference Store](https://github.com/adobe/aem-cif-guides-venia) ingår exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor. På så sätt kan varje projekt konfigurera individuella URL-mönster för produkt- och kategorisidor efter sina SEO-behov. En kombination av CIF `UrlProvider` och Sling Mappings används enligt beskrivningen ovan.

>[!NOTE]
>
>Den här konfigurationen måste justeras med den externa domän som används av projektet. Samlingsmappningarna fungerar baserat på värdnamnet och domänen. Den här konfigurationen är därför inaktiverad som standard och måste aktiveras före distributionen. Om du vill göra det byter du namn på `hostname.adobeaemcloud.com` mappen för kopplingsmappning i `ui.content/src/main/content/jcr_root/etc/map.publish/https` enlighet med det domännamn som används och aktiverar den här konfigurationen genom `resource.resolver.map.location="/etc/map.publish"` att lägga till i `JcrResourceResolver` projektets konfiguration.

## Ytterligare resurser

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [AEM](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
