---
title: Anpassa CIF-kärnkomponenter
description: Lär dig hur du anpassar AEM CIF Core Components. Självstudiekursen handlar om hur du på ett säkert sätt kan utöka en CIF Core-komponent för att uppfylla företagsspecifika krav. Lär dig hur du utökar en GraphQL-fråga för att returnera ett anpassat attribut och visa det nya attributet i en CIF Core-komponent.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 4933fc37-5890-47f5-aa09-425c999f0c91
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2594'
ht-degree: 0%

---

# Anpassa AEM CIF-kärnkomponenter {#customize-cif-components}

The [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) är en referenskodbas för att använda [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components). I den här självstudiekursen kommer du att utöka [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) om du vill visa ett anpassat attribut från Adobe Commerce. Du får också lära dig mer om GraphQL integrering mellan AEM och Adobe Commerce och de förlängningskopplingar som CIF Core Components tillhandahåller.

>[!TIP]
>
> Använd [AEM](https://github.com/adobe/aem-project-archetype) när du startar en egen implementering av e-handeln.

## Vad du ska bygga

Varumärket Venia började nyligen tillverka vissa produkter med hjälp av hållbara material och företaget skulle vilja visa en **Miljövänlig** som en del av Product Teaser. Ett nytt anpassat attribut skapas i Adobe Commerce för att ange om en produkt använder **Miljövänlig** material. Det anpassade attributet läggs sedan till som en del av GraphQL-frågan och visas i Product Teaser för angivna produkter.

![Slutlig implementering av miljöanpassade märken](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Förutsättningar {#prerequisites}

Det krävs en lokal utvecklingsmiljö för att slutföra den här självstudiekursen. Detta inkluderar en instans av AEM som körs och som är konfigurerad och ansluten till en Adobe Commerce-instans. Granska kraven och stegen för [konfigurera en lokal utveckling med AEM as a Cloud Service SDK](../develop.md). Om du vill följa självstudiekursen fullständigt måste du ha behörighet att lägga till [Attribut till en produkt](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) i Adobe Commerce.

Du behöver också GraphQL IDE som [GraphiQL](https://github.com/graphql/graphiql) eller ett webbläsartillägg för att köra kodexempel och självstudiekurser. Om du installerar ett webbläsartillägg måste du se till att det går att ange begäranrubriker. På Google Chrome [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) är ett tillägg som kan utföra jobbet.

## Klona Veniaprojektet {#clone-venia-project}

Vi klonar [Venedig-projektet](https://github.com/adobe/aem-cif-guides-venia) och åsidosätt sedan standardformaten.

>[!NOTE]
>
> **Du kan använda ett befintligt projekt** (baserat på AEM Project Archetype med CIF inkluderat) och hoppa över det här avsnittet.

1. Kör följande Git-kommando för att klona projektet:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Bygg och distribuera projektet till en lokal instans av AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Lägg till nödvändiga OSGi-konfigurationer för att ansluta AEM till en Adobe Commerce-instans eller lägga till konfigurationerna i det nyskapade projektet.

1. Nu bör du ha en fungerande version av en storefront som är ansluten till en Adobe Commerce-instans. Navigera till `US` > `Home` sida vid: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Du ser att butiken för närvarande använder temat Venia. När du expanderar huvudmenyn för butiken bör du se olika kategorier som anger att anslutningen till Adobe Commerce fungerar.

   ![Storefront konfigurerat med Venia-tema](../assets/customize-cif-components/venia-store-configured.png)

## Skapa Product Teaser {#author-product-teaser}

Product Teaser Component utökas genom hela kursen. Som ett första steg lägger du till en ny instans av Product Teaser på startsidan för att förstå baslinjefunktionerna.

1. Navigera till **Hemsida** för platsen: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Infoga en ny **Product Teaser** Komponent i sidans huvudlayoutbehållare.

   ![Insert Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expandera sidopanelen (om den inte redan är aktiverad) och växla till listrutan för resurssökning **Produkter**. Här visas en lista över tillgängliga produkter från en ansluten Adobe Commerce-instans. Välj en produkt och **dra och släpp** på **Product Teaser** på sidan.

   ![Dra och släpp Product Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Observera att du även kan konfigurera den visade produkten genom att konfigurera komponenten med hjälp av dialogrutan (klicka på _wrench_ ikon).

4. Du bör nu se en produkt som visas av Product Teaser. Produktens namn och produktens pris är standardattribut som visas.

   ![Product Teaser - standardstil](../assets/customize-cif-components/product-teaser-default-style.png)

## Lägg till ett anpassat attribut i Adobe Commerce {#add-custom-attribute}

De produkter och produktdata som visas i AEM lagras i Adobe Commerce. Lägg sedan till ett nytt attribut för **Miljövänlig** som en del av produktattributet som anges med Adobe Commerce användargränssnitt.

>[!TIP]
>
> Har redan en anpassad **Ja/Nej** som en del av din produktattributuppsättning? Du kan använda den och hoppa över det här avsnittet.

1. Logga in på din Adobe Commerce-instans.
1. Navigera till **Katalog** > **Produkter**.
1. Uppdatera sökfiltret för att hitta **Konfigurerbar produkt** används när de läggs till Teaser-komponenten i föregående övning. Öppna produkten i redigeringsläge.

   ![Sök efter Valeria-produkt](../assets/customize-cif-components/search-valeria-product.png)

1. I produktvyn klickar du på **Lägg till attribut** > **Skapa nytt attribut**.
1. Fyll i **Nytt attribut** formulär med följande värden (lämna standardinställningarna för andra värden)

   | Fältuppsättning | Fältetikett | Värde |
   | ----------------------------- | ------------------ | ---------------- |
   | Attributegenskaper | Attributetikett | **Miljövänlig** |
   | Attributegenskaper | Indatatyp för katalog | **Ja/Nej** |
   | Avancerade attributegenskaper | Attributkod | **miljövänlig** |

   ![Nytt attributformulär](../assets/customize-cif-components/attribute-new-form.png)

   Klicka **Spara attribut** när du är klar.

1. Rulla längst ned i produkten och expandera **Attribut** rubrik. Du borde se det nya **Miljövänlig** fält. Växla till **Ja**.

   ![Växla till ja](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Spara** ändringar av produkten.

   >[!TIP]
   >
   > Mer information om hantering [Produktattribut finns i användarhandboken för Adobe Commerce](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Navigera till **System** > **verktyg** > **Cachehantering**. Eftersom en uppdatering har gjorts av dataschemat måste vissa cachetyper i Adobe Commerce göras ogiltiga.
1. Markera rutan bredvid **Konfiguration** och skicka cachetypen för **Uppdatera**

   ![Uppdatera cachetyp för konfiguration](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Mer information om [Cachehantering finns i användarhandboken för Adobe Commerce](https://docs.magento.com/user-guide/system/cache-management.html).

## Använd en GraphQL-utvecklingsmiljö för att verifiera attribut {#use-graphql-ide}

Innan du börjar använda AEM kod är det praktiskt att utforska [GraphQL - översikt](https://devdocs.magento.com/guides/v2.4/graphql/) med en GraphQL IDE. Adobe Commerce integrering med AEM görs huvudsakligen via en serie GraphQL-frågor. Att förstå och ändra GraphQL-frågor är ett av de viktigaste sätten att utöka CIF Core-komponenterna.

Använd sedan en GraphQL-utvecklingsmiljö för att verifiera att `eco_friendly` har lagts till i produktattributuppsättningen. Skärmbilder i den här självstudiekursen använder [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Öppna GraphQL IDE och ange URL:en `http://<commerce-server>/graphql` i URL-fältet för den utvecklingsmiljö eller det tillägg du använder.
2. Lägg till följande [produktfråga](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) där `YOUR_SKU` är **SKU** av den produkt som använts i föregående undersökning:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Kör frågan så får du ett svar som följande:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Exempel på GraphQL-svar](../assets/customize-cif-components/sample-graphql-query.png)

   Observera att värdet för **Ja** är ett heltal av **1**. Detta är användbart när vi skriver GraphQL-frågan i Java.

   >[!TIP]
   >
   > Mer detaljerad dokumentation om [Adobe Commerce GraphQL finns här](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Uppdatera produktundervisningsmodellen {#updating-sling-model-product-teaser}

Därefter ska vi utöka produktTeaser affärslogik genom att implementera en Sling Model. [Sling Models](https://sling.apache.org/documentation/bundles/models.html), är anteckningsdrivna &quot;POJOs&quot; (Plain Old Java Objects) som implementerar någon av de affärslogik som behövs för komponenten. Sling-modeller används tillsammans med HTML-skript som en del av komponenten. Vi kommer att följa [Delegeringsmönster för delningsmodeller](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) så att vi bara kan utöka delar av den befintliga Product Teaser-modellen.

Sling Models implementeras som Java och finns i **kärna** för det genererade projektet.

Använd [den utvecklingsmiljö du vill](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) för att importera Venia-projektet. Skärmbilder som används finns i [Visual Studio Code IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. I din utvecklingsmiljö navigerar du under **kärna** till: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE för huvudplats](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` är ett Java-gränssnitt som utökar CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) gränssnitt.

   En ny metod har redan lagts till med namnet `isShowBadge()` för att visa ett märke om produkten anses vara&quot;Nytt&quot;.

1. Lägg till en ny metod, `isEcoFriendly()` till gränssnittet:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Det här är en ny metod som vi kommer att införa för att kapsla in logiken som anger om produkten har `eco_friendly` attribut inställt på **Ja** eller **Nej**.

1. Kontrollera sedan `MyProductTeaserImpl.java` på `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   The [Delegeringsmönster för delningsmodeller](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) tillåter `MyProductTeaserImpl` till referens `ProductTeaser` modell via `sling:resourceSuperType` egenskap:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   För alla metoder som vi inte vill åsidosätta eller ändra kan vi helt enkelt returnera värdet som `ProductTeaser` returneras. Till exempel:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Detta minimerar mängden Java-kod som en implementering behöver skriva.

1. En av de extra tilläggspunkterna AEM CIF Core Components är `AbstractProductRetriever` som ger tillgång till specifika produktattribut. Inspect `initModel()` metod:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to initialize the productRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   The `@PostConstruct` annoteringsfunktionen ser till att den här metoden anropas så snart som Sling-modellen initieras.

   Observera att GraphQL-frågan redan har utökats med `extendProductQueryWith` metod för att hämta ytterligare `created_at` -attribut. Det här attributet används senare som en del av `isShowBadge()` -metod.

1. Uppdatera GraphQL-frågan så att den innehåller `eco_friendly` attribut i den partiella frågan:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Lägga till i `extendProductQueryWith` är ett kraftfullt sätt att säkerställa att ytterligare produktattribut är tillgängliga för resten av modellen. Det minimerar även antalet frågor som körs.

   I ovanstående kod`addCustomSimpleField` används för att hämta `eco_friendly` -attribut. Detta visar hur du kan söka efter anpassade attribut som ingår i Adobe Commerce-schemat.

   >[!NOTE]
   >
   > The `createdAt()` metoden har faktiskt implementerats som en del av [Produktgränssnitt](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). De flesta av de vanligaste schemaattributen har implementerats, så använd bara `addCustomSimpleField` för verkligt anpassade attribut.

1. Lägg till en loggare som kan hjälpa dig att felsöka Java-koden:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Implementera sedan `isEcoFriendly()` metod:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   I ovanstående metod `productRetriever` används för att hämta produkten och `getAsInteger()` -metoden används för att hämta värdet för `eco_friendly` -attribut. Baserat på de GraphQL-frågor vi körde tidigare vet vi att det förväntade värdet när `eco_friendly` attribute is set to &quot;**Ja**&quot; är i själva verket ett heltal av **1**.

   Nu när delningsmodellen har uppdaterats måste komponentkoden uppdateras för att visa en indikator på **Miljövänlig** baserat på Sling-modellen.

## Anpassa koden för Product Teaser {#customize-markup-product-teaser}

Ett vanligt tillägg för AEM är att ändra den kod som genereras av komponenten. Detta görs genom att åsidosätta [HTL-skript](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html) som komponenten använder för att återge sin kod. HTML (HTML Template Language) är ett lättviktsmallspråk som används AEM komponenter för att dynamiskt återge kod baserat på det innehåll som skapats, vilket gör att komponenterna kan återanvändas. Product Teaser kan till exempel återanvändas om och om igen för att visa olika produkter.

I det här fallet vill vi återge en banderoll ovanpå teaser för att ange att produkten är&quot;miljövänlig&quot; baserat på ett anpassat attribut. Designmönstret för [anpassa markeringen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) för en komponent är faktiskt standard för alla AEM, inte bara för AEM CIF Core Components.

>[!NOTE]
>
> Om du anpassar en komponent med CIF-produkt- och kategoriväljare som denna Product Teaser eller CIF-sidkomponenten måste du inkludera den `cif.shell.picker` clientlib för komponentdialogrutorna. Se [Användning av CIF-produkt- och kategoriväljare](use-cif-pickers.md) för mer information.

1. Navigera i och expandera dialogrutan `ui.apps` och expandera mapphierarkin till: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` och inspektera `.content.xml` -fil.

   ![Product Teaser Ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Ovanför finns komponentdefinitionen för Product Teaser Component i vårt projekt. Observera egenskapen `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Det här är ett exempel på hur du skapar en [Proxy-komponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). I stället för att kopiera och klistra in alla Product Teaser HTML-skript från AEM CIF Core Components kan vi använda `sling:resourceSuperType` för att ärva alla funktioner.

1. Öppna filen `productteaser.html`. Det här är en kopia av `productteaser.html` från [CIF Product Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Observera att Sling Model för `MyProductTeaser` används och tilldelas `product` variabel.

1. Ändra `productteaser.html` för att ringa `isEcoFriendly` metod som har använts i föregående övning:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   När en Sling Model-metod anropas i HTML-koden `get` och `is` del av metoden tas bort och den första bokstaven minskas. Så `isShowBadge()` blir `.showBadge` och `isEcoFriendly` blir `.ecoFriendly`. Baserat på det booleska värdet som returneras från `.isEcoFriendly()` avgör om `<span>Eco Friendly</span>` visas.

   Mer information om `data-sly-test` och andra [HTML-blockprogramsatser finns här](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/block-statements.html#test).

1. Spara ändringarna och distribuera uppdateringarna till AEM med dina Maven-kunskaper från en kommandoradsterminal:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Öppna ett nytt webbläsarfönster och navigera till AEM och **OSGi-konsol** > **Status** > **Sling Models**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Sök efter `MyProductTeaserImpl` och du ska se en rad som följande:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Detta indikerar att Sling-modellen har distribuerats korrekt och mappats till rätt komponent.

1. Uppdatera till **Venia - startsida** på [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) där Product Teaser har lagts till.

   ![Miljövänligt meddelande visas](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Om produkten har `eco_friendly` attribut inställt på **Ja** ska du se texten&quot;Eco-Friendly&quot; på sidan. Försök att byta till olika produkter för att se hur beteendet förändras.

1. Öppna AEM `error.log` för att se de loggsatser vi lagt till. The `error.log` finns på `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Sök i AEM loggar för att se de loggsatser som lagts till i Sling-modellen:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > Du kan också se vissa stackspår om den produkt som används i teaser inte har `eco_friendly` som en del av dess attributuppsättning.

## Lägg till stilar för etiketten Eco Friendly {#add-styles}

I det här läget är logiken för när **Miljövänlig** emblemet fungerar, men den oformaterade texten kan använda vissa format. Lägg sedan till en ikon och format i `ui.frontend` för att slutföra implementeringen.

1. Ladda ned [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) -fil. Detta används som **Miljövänlig** emblem.
1. Återgå till utvecklingsmiljön och navigera till `ui.frontend` mapp.
1. Lägg till `eco_friendly.svg` till `ui.frontend/src/main/resources/images` mapp:

   ![Miljövänlig SVG har lagts till](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Öppna filen `productteaser.scss` på `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Lägg till följande Sass-regler i `.productteaser` klass:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > Checka ut [Utforma CIF-kärnkomponenter](./style-cif-component.md) för mer information om arbetsflöden.

1. Spara ändringarna och distribuera uppdateringarna till AEM med dina Maven-kunskaper från en kommandoradsterminal:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Uppdatera till **Venia - startsida** på [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) där Product Teaser har lagts till.

   ![Slutlig implementering av miljöanpassade märken](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Grattis {#congratulations}

Du har just skräddarsytt din första AEM CIF-komponent! Ladda ned [färdiga lösningsfiler här](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Bonus Challenge {#bonus-challenge}

Granska funktionaliteten i **Nytt** emblem som redan har implementerats i Product Teaser. Försök lägga till ytterligare en kryssruta där författarna kan styra när **Miljövänlig** emblem ska visas. Du måste uppdatera komponentdialogrutan på `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Utmaning vid implementering av nya märken](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Ytterligare resurser {#additional-resources}

- [AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components)
- [Anpassa AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [Anpassa kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [Komma igång med AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
- [Användning av CIF-produkt- och kategoriväljare](use-cif-pickers.md)
