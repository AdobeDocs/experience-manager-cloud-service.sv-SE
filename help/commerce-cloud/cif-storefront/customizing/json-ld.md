---
title: JSON+LD-metadata
description: Lär dig hur du aktiverar och verifierar JSON+LD-funktionen i AEM CIF.
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# JSON+LD-metadata {#json-ld}

Den här guiden förklarar hur du aktiverar och verifierar JSON+LD-funktionen i AEM CIF.

>[!NOTE]
>
> Den här funktionen är experimentell.

## Aktivera JSON+LD i CIF-konfiguration {#enabling}

Som standard är kryssrutan **Aktivera JSON+LD** inte synlig i CIF-konfigurationen. Om du vill aktivera den här funktionen måste projektet innehålla den nödvändiga OSGi-konfigurationen, som gör att kryssrutan kan visas. Den här konfigurationen gör att användare kan växla stöd för JSON+LD-skript på produktsidor.

Om du vill göra kryssrutan **Aktivera JSON+LD** tillgänglig i CIF-konfigurationen lägger du till följande OSGi-konfiguration i ditt projekt:

`com.adobe.cq.cif.components.models.JsonLdFeatureEnable`.

Mer information om hur du lägger till den här konfigurationen finns i [Lägger till konfiguration för Json-Ld](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json) i databasen för offentliga aem-cif-guides-venia.

När den här konfigurationen har lagts till och distribuerats visas kryssrutan i CIF konfigurationsinställningar och här är de steg som krävs för att aktivera **JSON+LD**:

1. Navigera till CIF-konfigurationen i AEM.
1. Avbryt arv.
1. Markera kryssrutan **Aktivera JSON+LD**.
1. Spara konfigurationen.

## Verifiera JSON+LD på en produktinformationssida (PDP) {#verify}

För att illustrera stegen för att verifiera JSON+LD används Venia-projektet som exempel, där den nödvändiga JSON+LD-konfigurationen redan har lagts till för att aktivera funktionen. Så här gör du:

1. Navigera till din lokala AEM-instans och öppna produktinformationssidan (PDP): `http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html`
1. Skriv en produkt på produktinformationssidan (PDP).
1. Växla till **Visa som publiceringsläge**.
1. Öppna **Visa sidan Source** i webbläsaren.
1. Sök efter JSON+LD i sidans källa.

Om det är korrekt konfigurerat hittar du JSON+LD-skriptet som är associerat med produkten som injicerats på sidan.

## Exempel på JSON+LD-struktur för en produkt {#sample}

Nedan visas ett exempel på en **JSON+LD**-struktur för Agatha Skirt, som skapats på PDP-sidan i Venia-projektet:

```html
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## Mappa JSON+LD-attribut till GraphQL {#mapping}

JSON+LD-attribut kan mappas till GraphQL-frågor i AEM CIF så att strukturerade data dynamiskt återspeglar produktinformation som hämtats via GraphQL.

### Exempel på produktmappning {#example}

| JSON+LD-attribut | Magento GraphQL Attribute | Obligatoriskt (J/N) |
|---------------------------------|-------------------|---|
| sku | sku | N |
| offers.url | Anpassad logik | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | sku | N |
| offers.priceSpecification.priceCurrency | valuta | Y |
| offers.priceSpecification.price | normal_price | N |
| offers.priceCurrency | valuta | Y |
| offers.price | special_price | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| name | name | Y |
| image | media_gallery.url | Y |
| description | description | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | rating_summary | N |
| @id | id | N |

Denna mappning säkerställer att JSON+LD-skriptet fylls i dynamiskt baserat på produktdata som hämtats via GraphQL-frågor.

Om du vill testa JSON+LD-strukturen kan du använda [Rich Results Test - Google Search Console.](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw) Det här verktyget ger detaljerad feedback, inklusive om de attribut som krävs finns eller saknas, och hjälper till att säkerställa att strukturerade data implementeras korrekt.
