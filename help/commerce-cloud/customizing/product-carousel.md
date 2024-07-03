---
title: Anpassade attribut till CIF produktCarousel
description: Lär dig hur du utökar AEM produktCarousel-komponenten genom att uppdatera Sling-modellen och anpassa koden.
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 594f0e6ec88851c86134be8d5d7f1719f74ddf4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Anpassade attribut till CIF produktCarousel {#product-carousel}

## Introduktion {#intro}

Produktkarusellkomponenten utökas genom hela kursen. Som ett första steg lägger du till en instans av Product Carousel på startsidan för att förstå baslinjefunktionerna:

1. Navigera till webbplatsens hemsida, till exempel [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. Infoga en ny Product Carousel-komponent i huvudlayoutbehållaren på sidan.
   ![Produkt-Carousel-komponent](/help/commerce-cloud/assets/product-carousel-component.png)
1. Expandera sidopanelen (om den inte redan är aktiverad) och växla till listrutan för resurssökning. **Produkter**.
     ![Carousel Products](/help/commerce-cloud/assets/carousel-products.png)    
1. Här visas en lista över tillgängliga produkter från en ansluten Adobe Commerce-instans.
   ![Ansluten instans](/help/commerce-cloud/assets/connected-instance.png)
1. Produkter visas enligt nedan med standardegenskaper:
   ![Produkt som visas med egenskaper](/help/commerce-cloud/assets/discount.png)

## Uppdatera försäljningsmodellen {#update-sling-model}

Du kan utöka affärslogiken i Product Carousel genom att implementera en Sling-modell:

1. I din utvecklingsmiljö navigerar du under kärnmodulen till `core/src/main/java/com/venia/core/models/commerce` och skapa ett CustomCarousel-gränssnitt som utökar CIF ProductCarousel-gränssnitt:

   ```
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```
1. Skapa sedan en implementeringsklass `CustomCarouselImpl.java` på `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`.
Delegeringsmönstret för delningsmodeller tillåter `CustomCarouselImpl` till referens `ProductCarousel` modell via `sling:resourceSuperType` egenskap:

   ```
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. Anteckningen @PostConstruct säkerställer att den här metoden anropas när Sling-modellen initieras. Produktens GraphQL-fråga har redan utökats med metoden extendProductQueryWith för att hämta attribut. Uppdatera GraphQL-frågan så att attributet inkluderas i den partiella frågan:

   ```
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   I ovanstående kod visas `addCustomSimpleField` används för att hämta `accessory_gemstone_addon` -attribut.

## Anpassa markeringen {#customize-markup}

Så här anpassar du markeringen ytterligare:

1. Skapa en kopia av `productcard.html` från `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` (huvudkomponentens crxde-sökväg) till modulen ui.apps `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`.

1. Redigera `productcard.html` anropa attributet custom, som nämns i implementeringsklassen:

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. Spara ändringarna och distribuera uppdateringarna till AEM med ditt Maven-kommando från en kommandoradsterminal. Du kan se det anpassade attributet `accessory_gemstone_addon` värdet för de valda produkterna på sidan.
