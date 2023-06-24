---
title: Avancerade URL-konfigurationer
description: Lär dig hur du anpassar URL:er för produkt- och kategorisidor. Genom att anpassa kan implementeringar optimera URL:er för sökmotorer och främja identifiering.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '2172'
ht-degree: 1%

---

# Avancerade URL-konfigurationer {#url}

>[!NOTE]
>
> Sökmotoroptimering (SEO) har blivit en viktig fråga för många marknadsförare. Därför måste SEO-frågor behandlas i många projekt på Adobe Experience Manager-as a Cloud Service (AEM). Se [Bästa praxis för hantering av SEO och URL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/seo-and-url-management.html) för ytterligare information.

[AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) innehåller avancerade konfigurationer för att anpassa URL:er för produkt- och kategorisidor. Många implementeringar anpassar dessa URL:er för sökmotoroptimering (SEO). Följande video visar hur du konfigurerar `UrlProvider` Service och funktioner i [Samlingsmappning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att anpassa URL:er för produkt- och kategorisidor.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Konfiguration {#configuration}

Så här konfigurerar du `UrlProvider` i enlighet med SEO:s krav och behov måste ett projekt tillhandahålla en OSGI-konfiguration för _CIF URL-providerkonfiguration_.

>[!NOTE]
>
> Sedan version 2.0.0 av AEM CIF Core Components finns det bara fördefinierade URL-format i URL-providerkonfigurationen, i stället för de format som är tillgängliga i 1.x-versioner. Dessutom har användningen av väljare för att skicka data i URL-adresser ersatts med suffix.

### URL-format för produktsida {#product}

Konfigurerar webbadresserna för produktsidorna och stöder följande alternativ:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (standard)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

Om det finns [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/product-page`
* `{{sku}}` ersätts med exempelvis produktens SKU, `VP09`
* `{{url_key}}` ersätts med produktens `url_key` egenskap, till exempel `lenora-crochet-shorts`
* `{{url_path}}` ersätts med produktens `url_path`, till exempel `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` ersätts med den markerade varianten, till exempel `VP09-KH-S`

Sedan `url_path` eftersom de fördefinierade produkt-URL-formaten är inaktuella används en produkts `url_rewrites` och välja det med de flesta bansegmenten som alternativ om `url_path` är inte tillgängligt.

Med exempeldata ser en produktvariant-URL som är formaterad med standardformatet för URL ut som `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### URL-format för kategorisida {#product-list}

Konfigurerar URL:erna för kategorierna eller produktlistsidorna och stöder följande alternativ:

* `{{page}}.html/{{url_path}}.html` (standard)
* `{{page}}.html/{{url_key}}.html`

Om det finns [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/category-page`
* `{{url_key}}` ersätts av kategoriens `url_key` property
* `{{url_path}}` ersätts av kategoriens `url_path`

Med exempeldata ovan ser en kategorisidas URL-adress formaterad med standardformatet för URL-adresser ut som `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> The `url_path` är en sammanfogning av `url_keys` för en produkts eller kategoris överordnade och produkten eller kategorin `url_key` avgränsad med `/` snedstreck. Varje `url_key` betraktas som unik i en viss butik.

### Butiksspecifik konfiguration {#store-specific-urlformats}

De systemomfattande kategori- och produktsidans URL-format som anges av _CIF URL-providerkonfiguration_ kan ändras för varje butik.

I CIF-konfigurationen kan en redigerare välja ett alternativt sidformat för produkt eller kategori. Om inget har valts där återgår implementeringen till den systemomfattande konfigurationen.

Om du ändrar URL-formatet för en aktiv webbplats kan det påverka webbplatsens organiska trafik negativt. Se [Bästa praxis](#best-practices) nedan och planera noggrant ändringen av URL-formatet i förväg.

![URL-format i CIF-konfiguration](assets/store-specific-url-formats.png)

>[!NOTE]
>
> Den butiksspecifika konfigurationen av URL-formaten kräver [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) och den senaste versionen av tillägget Adobe Experience Manager Content and Commerce.

## Kategorimedvetna produktsid-URL:er {#context-aware-pdps}

Eftersom det är möjligt att koda kategoriinformation i en produkt-URL kan produkter som finns i flera kategorier även adresseras med flera produkt-URL:er.

I standardformatet för URL väljs ett av de möjliga alternativen med följande schema:

* om `url_path` definieras av e-handelns serverdel som använder den (borttagen)
* från `url_rewrites` använda de URL:er som slutar med produktens `url_key` som alternativ
* de här alternativen använder det som har flest bansegment
* om det finns flera, ta den första i den ordning som e-handelsbackend ger den

Det här schemat väljer `url_path` med de flesta överordnade, baserat på antagandet att en underordnad kategori är mer specifik än den överordnade kategorin. Den markerade `url_path` beaktas _kanoniskt_ och används alltid som en kanonisk länk på produktsidor eller i produktwebbplatskartan.

Men när en kund går från en kategorisida till en produktsida, eller från en produktsida till en annan relaterad produktsida i samma kategori, är det värt att behålla den aktuella kategorikontexten. I det här fallet `url_path` markeringen bör föredra alternativ som finns inom den aktuella kategorikontexten framför _kanoniskt_ markeringen som beskrivs ovan.

Den här funktionen måste aktiveras i _CIF URL-providerkonfiguration_. Om det här alternativet är aktiverat får markeringen fler alternativ när

* de matchar delar av en viss kategori `url_path` från början (luddig prefixmatchning)
* eller de matchar en viss kategori `url_key` var som helst (exakt partiell matchning)

Ta till exempel svaret på en [produktfråga](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) nedan. Med följande:

* användaren finns på kategorisidan&quot;New Products / New in Sommaren 2022&quot;
* butiken använder standardsidans URL-format

Alternativet new-products/new-in-summer-2022/gold-cirque-earrings.html matchar två av kontextens bansegment från början. Det vill säga&quot;nya produkter&quot; och&quot;nya-sommaren-2022&quot;. Om butiken använder ett URL-format för kategorisida som bara innehåller kategorin `url_key`, skulle samma alternativ fortfarande vara markerat eftersom det matchar kontextens `url_key` var som helst. I båda fallen skapas produktsidans URL för&quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

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
> Kategorimedvetna produkt-URL:er kräver [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) eller nyare.

## Specifika kategori- och produktsidor {#specific-pages}

Det går att skapa [sidor med flera kategorier och produkter](../authoring/multi-template-usage.md) för endast en viss delmängd av kategorier eller produkter i en katalog.

### Urvalskriterier {#specific-pages-selection}

Urvalet av en viss kategorisida är rakt framåt, baserat på kategorins `url_path` eller `url_key`. Matchande underkategorier stöds bara för URL-format som innehåller hela kategorin `url_path`. Annars är det bara en exakt matchning av `url_key` är möjligt.

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
> Välja specifika produktsidor per kategori kräver [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) eller nyare.

### Djuplänkning {#specific-pages-deep-linking}

The `UrlProvider` är förkonfigurerat för att generera djupa länkar till specifika kategorier och produktsidor på instanser på författarnivå. Den här funktionen är användbar för redigerare som bläddrar på en webbplats i förhandsgranskningsläge, navigerar till en viss produkt- eller kategorisida och växlar tillbaka till redigeringsläget för att redigera sidan.

Vid publiceringsskiktsinstanser bör katalogsidans URL-adresser hållas stabila så att de inte förlorar vinster på t.ex. sökmotorrankningar. På grund av den publiceringsnivån återges inte djuplänkar till specifika katalogsidor som standard. Om du vill ändra det här beteendet _CIF URL Provider Specific Page Strategy_ kan konfigureras för att alltid generera särskilda sidadresser.

### Flera katalogsidor {#multiple-product-pages}

När redaktörer vill ha fullständig kontroll över navigeringen på den översta nivån på en webbplats kanske det inte är önskvärt att använda en enda katalogsida för att återge kategorierna på den översta nivån i en katalog. I stället kan redigerare skapa flera katalogsidor, en för varje kategori i katalogen som de vill inkludera i navigeringen på den översta nivån.

I det fallet kan varje katalogsida ha en referens till en produkt- och kategorisida som är specifik för den kategori som har konfigurerats för katalogsidan. The `UrlProvider` använder de här anslutningarna för att skapa länkar för sidorna och kategorierna i den konfigurerade kategorin. Av prestandaskäl beaktas dock endast de underordnade katalogsidorna för en webbplats navigeringsrot/landningssida.

Vi rekommenderar att produkt- och kategorisidorna för en katalogsida är underordnade den katalogsidan, annars kanske inte komponenter som Navigation eller Breadcrumb fungerar som de ska.

>[!NOTE]
>
> Fullt stöd för flera katalogsidor kräver [CIF Core Components 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) eller nyare.

## Anpassningar {#customization}

### Anpassade URL-format {#custom-url-format}

Ett projekt kan implementera antingen [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) eller [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) och registrera implementeringen som en tjänst av allmänt ekonomiskt intresse. Dessa implementeringar, om de är tillgängliga, ersätter det konfigurerade fördefinierade formatet. Om det finns flera registrerade implementeringar ersätter den med den högre rangordningen dem med den lägre rangordningen.

Implementeringarna av det anpassade URL-formatet måste implementera ett par metoder för att skapa en URL från angivna parametrar och för att tolka en URL för att returnera samma parametrar.

### Kombinera med delningskartor {#sling-mapping}

Förutom `UrlProvider`går det också att konfigurera [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att skriva om och bearbeta URL:er. Det AEM Archetype-projektet innehåller även [en exempelkonfiguration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) om du vill konfigurera vissa kopplingsmappningar för port 4503 (publicera) och 80 (Dispatcher).

### Kombinera med AEM Dispatcher {#dispatcher}

URL-omskrivningar kan också göras med AEM Dispatcher HTTP-server med `mod_rewrite` -modul. The [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) innehåller en referens AEM Dispatcher-konfiguration som redan innehåller grundläggande [skriv om regler](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) för den genererade storleken.

## Bästa praxis {#best-practices}

### Välj det bästa URL-formatet {#choose-url-format}

Som vi nämnt innan du väljer ett av de tillgängliga standardformaten, eller till och med implementerar ett anpassat format, beror i hög grad på butikens behov och krav. Följande förslag kan hjälpa dig att fatta ett väl underbyggt beslut.

_**Använd ett URL-format för produktsidan som innehåller SKU:n.**_

CIF Core Components använder SKU:n som primär identifierare i alla komponenter. Om produktsidans URL-format inte innehåller SKU:n måste du ha en GraphQL-fråga för att kunna lösa det. Den här upplösningen kan påverka tiden till första byten. Det kan också vara önskvärt att kunderna kan hitta produkter genom SKU med sökmotorer.

_**Använd ett URL-format för produktsidan som innehåller kategorisammanhanget.**_

Vissa funktioner i CIF URL-providern är bara tillgängliga när du använder produkts-URL-format, som kodar kategorisammanhanget, som kategorin `url_key` eller kategorin `url_path`. Även om dessa funktioner kanske inte behövs för en ny butik kan du minska migreringsansträngningarna i framtiden genom att använda något av dessa URL-format i början.

_**Balansera URL-längden och kodad information.**_

Beroende på katalogstorleken, särskilt storleken och djupet på kategoriträdet, är det kanske inte rimligt att koda hela `url_path` av kategorier i URL:en. I så fall kan URL-längden minskas genom att endast kategorins `url_key` i stället. Den här metoden har stöd för de flesta funktioner som är tillgängliga när du använder kategorin `url_path`.

Använd också [Samlingsmappningar](#sling-mapping) för att kombinera SKU:n med produkten `url_key`. I de flesta e-handelssystem följer SKU:n ett visst format och skiljer SKU:n från `url_key` för inkommande förfrågningar bör enkelt vara möjligt. Med detta i åtanke bör det vara möjligt att skriva om en produktsidas URL till `/p/{{category}}/{{sku}}-{{url_key}}.html`och en kategori-URL till `/c/{{url_key}}.html` respektive. The `/p` och `/c` -prefix är fortfarande nödvändigt för att skilja produkt- och kategorisidor från andra innehållssidor.

### Migrera till ett nytt URL-format {#migrate-url-formats}

Många av de förvalda URL-formaten är på något sätt kompatibla med varandra, vilket innebär att URL:er som är formaterade av en kan tolkas av en annan. Det gör det lättare att migrera mellan olika URL-format.

Å andra sidan behöver sökmotorer tid för att rita om alla katalogsidor med det nya URL-formatet. För att stödja den här processen och även för att förbättra användarupplevelsen rekommenderar vi att du tillhandahåller omdirigeringar som vidarebefordrar användaren från de gamla URL:erna till de nya.

Ett sätt att göra detta kan vara att ansluta en scenmiljö till e-handelsservern för produktion och konfigurera den så att den använder det nya URL-formatet. Efteråt får du [produktwebbplatskarta som genererats av CIF-produkter för webbplatskartor](../../overview/seo-and-url-management.md) för både scenen och produktionsmiljön, och använda dem för att skapa en [Omskrivningskarta för Apache httpd](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Denna omskrivningskarta kan sedan distribueras till Dispatcher tillsammans med utrullningen av det nya URL-formatet.

## Exempel {#example}

The [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia) projektet innehåller exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor. Med den här konfigurationen kan varje projekt ställa in enskilda URL-mönster för produkt- och kategorisidor efter sina SEO-behov. En kombination av CIF `UrlProvider` och Samlingsmappningar enligt ovan används.

>[!NOTE]
>
>Den här konfigurationen måste justeras med den externa domän som används av projektet. Samlingsmappningarna fungerar baserat på värdnamnet och domänen. Den här konfigurationen är därför inaktiverad som standard och måste aktiveras före distributionen. Om du vill göra det byter du namn på kopplingsmappningen `hostname.adobeaemcloud.com` mapp i `ui.content/src/main/content/jcr_root/etc/map.publish/https` enligt det använda domännamnet och aktivera den här konfigurationen genom att lägga till `resource.resolver.map.location="/etc/map.publish"` till `JcrResourceResolver` projektets konfiguration.

## Ytterligare resurser {#additional}

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
