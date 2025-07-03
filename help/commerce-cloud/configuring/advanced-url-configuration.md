---
title: Avancerade URL-konfigurationer
description: Lär dig hur du anpassar URL:er för produkt- och kategorisidor. Genom att anpassa kan implementeringar optimera URL:er för sökmotorer och främja identifiering.
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 0%

---

# Avancerade URL-konfigurationer {#url}

>[!NOTE]
>
> Sökmotoroptimering (SEO) har blivit en viktig fråga för många marknadsförare. Därför måste SEO-frågor behandlas i många projekt på Adobe Experience Manager (AEM) as a Cloud Service. Mer information finns i [Bästa metoder för SEO- och URL-hantering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/seo-and-url-management.html).

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) innehåller avancerade konfigurationer för att anpassa URL:er för produkt- och kategorisidor. Många implementeringar anpassar dessa URL:er för sökmotoroptimering (SEO). Följande video visar hur du konfigurerar tjänsten `UrlProvider` och funktionerna i [Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att anpassa URL:er för produkt- och kategorisidor.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Konfiguration {#configuration}

Om du vill konfigurera tjänsten `UrlProvider` enligt SEO-kraven och -behoven måste ett projekt tillhandahålla en OSGI-konfiguration för _CIF URL Provider-konfigurationen_.

>[!NOTE]
>
> Sedan version 2.0.0 av AEM CIF Core Components tillhandahåller URL-providerkonfigurationen endast fördefinierade URL-format, i stället för det kostnadsfria format som kan konfigureras i 1.x-versioner. Dessutom har användningen av väljare för att skicka data i URL-adresser ersatts med suffix.

### URL-format för produktsida {#product}

Konfigurerar URL:erna för produktsidorna och stöder följande alternativ:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (standard)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

Om det finns [Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/product-page`
* `{{sku}}` ersätts med produktens SKU, till exempel `VP09`
* `{{url_key}}` ersätts med produktens `url_key`-egenskap, till exempel `lenora-crochet-shorts`
* `{{url_path}}` ersätts med produktens `url_path`, till exempel `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` ersätts med den valda varianten, till exempel `VP09-KH-S`

Eftersom `url_path` har tagits bort använder de fördefinierade produkt-URL-formaten en produkts `url_rewrites` och väljer den med de flesta sökvägssegmenten som alternativ om `url_path` inte är tillgänglig.

Med exempeldata ovan ser en produktvariant-URL som formaterats med standardformatet för URL ut som `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### URL-format för kategorisida {#product-list}

Konfigurerar URL:erna för kategorierna eller produktlistsidorna och stöder följande alternativ:

* `{{page}}.html/{{url_path}}.html` (standard)
* `{{page}}.html/{{url_key}}.html`

Om det finns [Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/category-page`
* `{{url_key}}` ersätts av kategorins `url_key`-egenskap
* `{{url_path}}` ersätts av kategorins `url_path`

Med exempeldata ovan ser en kategorisidas URL som är formaterad med standardformatet för URL ut som `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> `url_path` är en sammanfogning av `url_keys` för en produkts eller kategorins överordnade och produktens eller kategorins `url_key` avgränsade med `/` snedstreck. Varje `url_key` betraktas som unik i en angiven butik.

### Butiksspecifik konfiguration {#store-specific-urlformats}

Du kan ändra formaten för systemomfattande kategori- och produktsidans URL-adress som anges av _CIF URL Provider-konfigurationen_ för varje butik.

I CIF Configuration kan en redigerare välja ett alternativ produkt- eller kategorisidans URL-format. Om inget har valts där återgår implementeringen till den systemomfattande konfigurationen.

Om du ändrar URL-formatet för en aktiv webbplats kan det påverka webbplatsens organiska trafik negativt. Se [Bästa praxis](#best-practices) nedan och planera noggrant ändringen av URL-formatet i förväg.

![URL-format i CIF Configuration](assets/store-specific-url-formats.png)

>[!NOTE]
>
> Den butiksspecifika konfigurationen av URL-formaten kräver [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) och den senaste versionen av Adobe Experience Manager Content och Commerce Add-on.

## Kategorimedvetna produktsid-URL:er {#context-aware-pdps}

Eftersom det är möjligt att koda kategoriinformation i en produkt-URL kan produkter som finns i flera kategorier även adresseras med flera produkt-URL:er.

I standardformatet för URL väljs ett av de möjliga alternativen med följande schema:

* om `url_path` definieras av e-handelsbackend använder det (borttaget)
* från `url_rewrites` använder de URL:er som slutar med produktens `url_key` som alternativ
* de här alternativen använder det som har flest bansegment
* om det finns flera, ta den första i den ordning som e-handelsbackend ger den

Det här schemat väljer `url_path` med de mest överordnade, baserat på antagandet att en underordnad kategori är mer specifik än dess överordnade kategori. Den valda `url_path` betraktas som _kanoniskt_ och används alltid som en kanonisk länk på produktsidor eller i produktwebbplatskartan.

Men när en kund går från en kategorisida till en produktsida, eller från en produktsida till en annan relaterad produktsida i samma kategori, är det värt att behålla den aktuella kategorikontexten. I det här fallet bör markeringen `url_path` föredra alternativ som finns i den aktuella kategorikontexten framför den _kanoniska_ markering som beskrivs ovan.

Den här funktionen måste vara aktiverad i _CIF URL Provider-konfigurationen_. Om det här alternativet är aktiverat får markeringen fler alternativ när

* de matchar delar av en angiven kategoris `url_path` från början (otydlig prefixmatchning)
* eller så matchar de `url_key` för en viss kategori var som helst (exakt partiell matchning)

Ta till exempel svaret på en [produktfråga](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) nedan. Med följande:

* användaren finns på kategorisidan&quot;New Products / New in Sommaren 2022&quot;
* butiken använder standardsidans URL-format

Alternativet new-products/new-in-summer-2022/gold-cirque-earrings.html matchar två av kontextens bansegment från början. Det vill säga&quot;nya produkter&quot; och&quot;nya-sommaren-2022&quot;. Om butiken använder ett URL-format för kategorisidor som bara innehåller kategorin `url_key`, skulle samma alternativ fortfarande vara markerat eftersom det matchar kontextens `url_key` var som helst. I båda fallen skapas produktsidans URL för&quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> Kategorimedvetna produkt-URL:er kräver [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) eller senare.

## Specifika kategori- och produktsidor {#specific-pages}

Det går bara att skapa [flera kategorier och produktsidor](../authoring/multi-template-usage.md) för en viss delmängd av kategorier eller produkter i en katalog.

### Urvalskriterier {#specific-pages-selection}

Markeringen av en viss kategorisida är rak framåt, baserat på kategorins `url_path` eller `url_key`. Matchande underkategorier stöds bara för URL-format som innehåller den fullständiga kategorin `url_path`. I annat fall går det bara att exakt matcha `url_key`.

Specifika produktsidor väljs antingen enligt produktens SKU eller kategori. Den senare kräver att viss kategoriinformation kodas i produkt-URL:en. Den här funktionen är bara tillgänglig för vissa av standardformaten för URL-adresser. I följande tabell finns en jämförelse som visar vilket URL-format som stöder specifikt sidval per SKU eller kategori.


| URL-format | efter SKU | per kategori |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | no | no |
| `{{page}}.html/{{category}}/{{url_key}}.html` | no | endast exakt matchning |
| `{{page}}.html/{{url_path}}.html` | no | ja |
| `{{page}}.html/{{sku}}.html` | ja | no |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | ja | no |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | ja | endast exakt matchning |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | ja | ja |

{style="table-layout:auto"}

>[!NOTE]
>
> Om du vill välja specifika produktsidor per kategori måste du ha [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) eller senare.

### Djuplänkning {#specific-pages-deep-linking}

`UrlProvider` är förkonfigurerad för att generera djuplänkar till specifika kategorier och produktsidor på instanser på författarnivå. Den här funktionen är användbar för redigerare som bläddrar på en webbplats i förhandsgranskningsläge, navigerar till en viss produkt- eller kategorisida och växlar tillbaka till redigeringsläget för att redigera sidan.

Vid publiceringsskiktsinstanser bör katalogsidans URL-adresser hållas stabila så att de inte förlorar vinster på t.ex. sökmotorrankningar. På grund av den publiceringsnivån återges inte djuplänkar till specifika katalogsidor som standard. Om du vill ändra det här beteendet kan du konfigurera _CIF URL Provider Specific Page Strategy_ så att den alltid genererar särskilda sidadresser.

### Flera katalogsidor {#multiple-product-pages}

När redaktörer vill ha fullständig kontroll över navigeringen på den översta nivån på en webbplats kanske det inte är önskvärt att använda en enda katalogsida för att återge kategorierna på den översta nivån i en katalog. I stället kan redigerare skapa flera katalogsidor, en för varje kategori i katalogen som de vill inkludera i navigeringen på den översta nivån.

I det fallet kan varje katalogsida ha en referens till en produkt- och kategorisida som är specifik för den kategori som har konfigurerats för katalogsidan. `UrlProvider` använder dessa anslutningar för att skapa länkar för sidorna och kategorierna i den konfigurerade kategorin. Av prestandaskäl beaktas dock endast de underordnade katalogsidorna för en webbplats navigeringsrot/landningssida.

Vi rekommenderar att produkt- och kategorisidorna för en katalogsida är underordnade den katalogsidan, annars kanske inte komponenter som Navigation eller Breadcrumb fungerar som de ska.

>[!NOTE]
>
> Fullt stöd för flera katalogsidor kräver [CIF Core Components 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) eller senare.

## Anpassningar {#customization}

### Anpassade URL-format {#custom-url-format}

Om du vill ange ett anpassat URL-format kan ett projekt implementera tjänstgränssnittet [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) eller [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) och registrera implementeringen som en OSGI-tjänst. Dessa implementeringar, om de är tillgängliga, ersätter det konfigurerade fördefinierade formatet. Om det finns flera registrerade implementeringar ersätter den med den högre rangordningen dem med den lägre rangordningen.

Implementeringarna av det anpassade URL-formatet måste implementera ett par metoder för att skapa en URL från angivna parametrar och för att tolka en URL för att returnera samma parametrar.

### Kombinera med delningskartor {#sling-mapping}

Förutom `UrlProvider` går det också att konfigurera [Kopplingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) så att URL:er skrivs om och bearbetas. AEM Archetype-projektet innehåller även [en exempelkonfiguration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) som konfigurerar vissa Sling Mappings för port 4503 (publicera) och 80 (Dispatcher).

### Kombinera med AEM Dispatcher {#dispatcher}

URL-omskrivningar kan också göras med hjälp av AEM Dispatcher HTTP-server med modulen `mod_rewrite`. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) innehåller en referenskonfiguration för AEM Dispatcher som redan innehåller grundläggande [omskrivningsregler](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) för den genererade storleken.

## Bästa praxis {#best-practices}

### Välj det bästa URL-formatet {#choose-url-format}

Som vi nämnt innan du väljer ett av de tillgängliga standardformaten, eller till och med implementerar ett anpassat format, beror i hög grad på butikens behov och krav. Följande förslag kan hjälpa dig att fatta ett väl underbyggt beslut.

_**Använd ett URL-format för en produktsida som innehåller SKU:n.**_

CIF Core Components använder SKU:n som primär identifierare i alla komponenter. Om produktsidans URL-format inte innehåller SKU:n måste du ha en GraphQL-fråga för att kunna lösa det. Den här upplösningen kan påverka tiden till första byten. Det kan också vara önskvärt att kunderna kan hitta produkter genom SKU med sökmotorer.

_**Använd ett URL-format för en produktsida som innehåller kategorikontexten.**_

Vissa funktioner i CIF URL Provider är bara tillgängliga när du använder produkts-URL-format, som kodar kategorikontexten, till exempel kategorin `url_key` eller kategorin `url_path`. Även om dessa funktioner kanske inte behövs för en ny butik kan du minska migreringsansträngningarna i framtiden genom att använda något av de här URL-formaten i början.

_**Balans mellan URL-längd och kodad information.**_

Beroende på katalogstorleken, särskilt kategoriträdets storlek och djup, är det inte säkert att det går att koda hela `url_path` kategorier till URL:en. I så fall kan URL-längden minskas genom att endast kategorins `url_key` inkluderas i stället. Den här metoden stöder de flesta av de funktioner som är tillgängliga när du använder kategorin `url_path`.

Använd också [Samlingsmappningar](#sling-mapping) för att kombinera SKU:n med produkten `url_key`. I de flesta e-handelssystem följer SKU:n ett visst format och det bör vara enkelt att separera SKU:n från `url_key` för inkommande begäranden. Med detta i åtanke bör det vara möjligt att skriva om en produktsidas URL till `/p/{{category}}/{{sku}}-{{url_key}}.html` och en kategori-URL till `/c/{{url_key}}.html`. Prefixen `/p` och `/c` behövs fortfarande för att skilja produkt- och kategorisidor från andra innehållssidor.

### Migrera till ett nytt URL-format {#migrate-url-formats}

Många av de förvalda URL-formaten är på något sätt kompatibla med varandra, vilket innebär att URL:er som är formaterade av en kan tolkas av en annan. Det gör det lättare att migrera mellan olika URL-format.

Å andra sidan behöver sökmotorer tid för att rita om alla katalogsidor med det nya URL-formatet. För att stödja den här processen och även för att förbättra användarupplevelsen rekommenderar vi att du tillhandahåller omdirigeringar som vidarebefordrar användaren från de gamla URL:erna till de nya.

Ett sätt att göra detta kan vara att ansluta en scenmiljö till e-handelsservern för produktion och konfigurera den så att den använder det nya URL-formatet. Hämta sedan produktwebbplatskartan [som genererats av CIF-produktwebbplatskartor](../../overview/seo-and-url-management.md) för både scenen och produktionsmiljön och använd dem för att skapa en [Apache httpd-omskrivningskarta](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Denna omskrivningskarta kan sedan distribueras till Dispatcher tillsammans med utrullningen av det nya URL-formatet.

## Exempel {#example}

Projektet [Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia) innehåller exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor. Med den här konfigurationen kan varje projekt ställa in enskilda URL-mönster för produkt- och kategorisidor efter sina SEO-behov. En kombination av CIF `UrlProvider` och Sling Mappings används enligt beskrivningen ovan.

>[!NOTE]
>
>Den här konfigurationen måste justeras med den externa domän som används av projektet. Samlingsmappningarna fungerar baserat på värdnamnet och domänen. Den här konfigurationen är därför inaktiverad som standard och måste aktiveras före distributionen. Om du vill göra det byter du namn på mappen för kopplingsmappning `hostname.adobeaemcloud.com` i `ui.content/src/main/content/jcr_root/etc/map.publish/https` enligt det domännamn som används och aktiverar den här konfigurationen genom att lägga till `resource.resolver.map.location="/etc/map.publish"` i projektkonfigurationen `JcrResourceResolver`.

## Ytterligare resurser {#additional}

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [AEM-resursmappning](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Kopplingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
