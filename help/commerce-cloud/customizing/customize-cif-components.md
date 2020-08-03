---
title: Anpassa CIF-kärnkomponenter
description: Anpassa CIF-kärnkomponenter
translation-type: tm+mt
source-git-commit: dd6973085ae34dd6ea7296c36d0a14f699440269
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---


# Anpassa AEM CIF-kärnkomponenter {#customize-cif-components}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) innehåller en standarduppsättning med Commerce Components som kan användas för att snabba upp ett projekt som integrerar lösningarna Adobe Experience Manager (AEM) och Magento. Dessa komponenter är produktionsklara och kan [enkelt formateras med CSS](style-cif-component.md). Många implementeringar kommer också att vilja utöka dessa komponenter för att uppfylla företagsspecifika krav.

I den här självstudiekursen ska vi granska flera olika tilläggspunkter som AEM CIF Core Components och AEM i allmänhet. Vi gör detta genom att utöka funktionerna i [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) -komponenten för att inkludera möjligheten att återge en&quot;ny&quot; banderoll. Innehållsförfattare kan växla till den här banderollen och bestämma hur länge bannern ska visas. Produktens&quot;ålder&quot; baseras på det datum den skapades i Magento-katalogen. När en produkt är ett visst antal dagar gammal försvinner den nya banderollen automatiskt.

![Ny banderoll utökad](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Förutsättningar {#prerequisites}

Följande verktyg och tekniker krävs:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
* [AEM Cloud SKD med CIF-tillägg](../develop.md)
* Magento-kompatibel med CIF Core Components

Vi rekommenderar att du granskar följande innehåll innan du fortsätter med den här självstudiekursen:

* [Introducing Commerce Integration Framework on AEM as a Cloud Service](/help/commerce-cloud/overview.md)
* [Style AEM CIF Core Components - självstudiekurs](style-cif-component.md)

## Startprojekt

Vi har tagit fram ett startprojekt som ska användas med den här självstudiekursen. Projektet genererades med [v0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) av CIF-projekttypen. Det anses vara en god vana att alltid använda den [senaste versionen](https://github.com/adobe/aem-cif-project-archetype/releases/latest) av typen när du startar ett nytt projekt.

1. Ladda ned startprojektet [**acme-store.zip **](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip)till skrivbordet.

1. Zippa upp **acme-store.zip** så ser du följande mappstruktur:

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. Öppna ett nytt terminalfönster och bygg och driftsätt projektet i en lokal instans av AEM.

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Lägg till nödvändiga OSGi-konfigurationer för att ansluta AEM till en Magento-instans eller lägga till konfigurationerna i det nyskapade projektet.

1. Nu bör du ha en fungerande version av en storefront som är ansluten till en Magento-instans. Navigera till `US` > `Home` sida: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Du ser att butiken för närvarande använder temat Venia. När du expanderar huvudmenyn för butiken bör du se olika kategorier som anger att anslutningen Magento fungerar.

   ![Storefront konfigurerat med Venedig-tema](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Skapa Product Teaser {#author-product-teaser}

Vi kommer att utöka Product Teaser Component genom hela kursen. Som ett första steg ska vi lägga till en ny instans av Product Teaser på hemsidan för att förstå baslinjefunktionerna.

1. Navigera till webbplatsens **hemsida** : [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Infoga en ny **Product Teaser** Component i sidans huvudlayoutbehållare.

   ![Insert Product Teaser](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Expandera sidopanelen (om den inte redan är aktiverad) och växla till listrutan **Produkter**. Här visas en lista över tillgängliga produkter från en ansluten Magento-instans. Välj en produkt och **dra och släpp** den i **Product Teaser** -komponenten på sidan.

   ![Dra och släpp Product Teaser](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Observera att du även kan konfigurera den visade produkten genom att konfigurera komponenten med hjälp av dialogrutan (klicka på *skiftnyckelsikonen* ).

1. Du bör nu se en produkt som visas av Product Teaser. Produktens namn och produktens pris är standardattribut som visas.

   ![Product Teaser - standardstil](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Anpassa koden för Product Teaser {#customize-markup-product-teaser}

Ett vanligt tillägg för AEM är att ändra den kod som genereras av komponenten. Detta görs genom att åsidosätta det [HTML-skript](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) som komponenten använder för att återge sin kod. HTML-mallspråk (HTL) är ett lättviktsmallspråk som används AEM komponenter för att dynamiskt återge kod baserat på redigerat innehåll, vilket gör att komponenterna kan återanvändas. Product Teaser kan till exempel återanvändas om och om igen för att visa olika produkter.

I det här fallet vill vi återge en banderoll ovanpå teaser för att ange att produkten är&quot;Ny&quot; och nyligen har lagts till i katalogen. Designmönstret för att [anpassa markeringen](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) för en komponent är i själva verket standard för alla AEM komponenter, inte bara för de AEM CIF Core-komponenterna.

Använd den utvecklingsmiljö du väljer för att [öppna startprojektet som laddas ned](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) i början av självstudiekursen.

1. Navigera och expandera modulen **ui.apps** och expandera mapphierarkin till: `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` och inspektera `.content.xml` filen.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Ovanför finns komponentdefinitionen för Product Teaser Component i vårt projekt. Lägg märke till egenskapen `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Det här är ett exempel på hur du skapar en [Proxy-komponent](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components). I stället för att kopiera och klistra in alla Product Teaser HTML-skript från AEM CIF Core Components kan vi använda `sling:resourceSuperType` för att ärva alla funktioner.

1. Öppna en ny webbläsare och navigera till [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) i AEM. Expandera trädet för att visa `productteaser` komponenten under: `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![CRXDE Lite Product Teaser](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Det här är den fullständiga komponentdefinitionen för Product Teaser-komponenten.

1. Växla tillbaka till din utvecklingsmiljö och Acme Store-projektet. Skapa en ny fil med namnet `productteaser.html` under `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Kopiera innehållet i `productteaser.html` från [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) och klistra in det i Acme-Store-projektet i den nya `productteaser.html` filen.

   ![Product Teaser html-överskrivning](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. I Acme-Store-projektet ändrar du `productteaser.html` filen och infogar en ny div som representerar ett märke ovanför produktbildkoden:

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. Distribuera den uppdaterade koden till den lokala instansen av AEM med hjälp av dina maven-kunskaper eller [av funktionerna i din IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. I webbläsaren går du tillbaka till [startsidan för butikssidan](http://localhost:4502/editor.html/content/acme/us/en.html) i AEM. Uppdatera så ser du att en&quot;ny&quot; banderoll visas i komponentens övre högra hörn.

   ![Ny banderoll utökad](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   För närvarande finns det ingen logik bakom när banderollen visas. Under de kommande övningarna kommer vi att rätta till det.

   > Observera att CSS för att återge banderollen ingick i startprojektet och finns på: `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Mer information finns i självstudiekursen [Styling CIF Core Components](style-cif-component.md).

## Anpassa dialogrutan för Product Teaser {#customize-dialog-product-teaser}

Därefter anpassar vi dialogrutan för Product Teaser-komponenten så att en författare kan bestämma vilket datumintervall en produkt ska anses vara&quot;ny&quot; och om banderollen ska visas. Vi gör detta genom att [anpassa dialogrutan](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) för Product Teaser som en del av Acme Store-projektet.

1. Öppna Acme Store-projektet i den utvecklingsmiljö du vill använda och navigera till `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Under `productteaser` mappen lägger du till en ny mapp med namnet `_cq_dialog`. Lägg till en ny fil i `_cq_dialog` mappen `.content.xml`. Du bör nu ha följande filstruktur:

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. Uppdatera `_cq_dialog/.content.xml` med följande XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   Ovanför har ytterligare två fält lagts till som en del av en ny flik och ett enda dolt fält.

   1. Kryssruta för att visa märket&quot;Nytt&quot;
   2. Nummerfält som definierar maximal produktålder
   3. Dolt fält för att säkerställa att den maximala produktåldern sparas som lång (mer information finns i [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) )

   Dialogrutor som definieras som en del av en proxykomponent ärver alla befintliga dialogrutefält med en funktion som kallas [Dela resurssammanslagning](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html). Därför behöver vi inte definiera om de befintliga fälten som ingår i Product Teaser.

1. Uppdatera `productteaser.html` och lägg till en `data-sly-test` till `<div>` för märket. Detta är ett enkelt test som avgör om märket ska återges om användaren har markerat &quot;true&quot;.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Distribuera den uppdaterade koden till den lokala instansen av AEM med hjälp av funktioner i den utvecklingsmiljö du använder eller genom att använda dina maven-kunskaper:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Gå tillbaka till Product Teaser och klicka på *skiftnyckelsikonen* för att öppna dialogrutan. Nu visas en flik för **Badge** med ytterligare två fält. Om du uppdaterar de här fälten behålls värdena som AEM. Du bör kunna aktivera/inaktivera märket med kryssrutan:

   ![Växla märke](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Detta ger författaren kontroll över när märket visas. Men det skulle vara idealiskt att märket försvinner automatiskt när produkten har nått en viss ålder på dagen baserat på posten för **Max produktålder**. Därför måste vi implementera viss backend-logik.

## Uppdatera produktunderlagets försäljningsmodell {#updating-sling-model-product-teaser}

Därefter ska vi utöka produktTeaser affärslogik genom att implementera en Sling Model. [Sling Models](https://sling.apache.org/documentation/bundles/models.html)är anteckningsdrivna &quot;POJOs&quot; (Plain Old Java Objects) som implementerar någon av de affärslogik som komponenten behöver. Sling-modeller används tillsammans med HTML-skript som en del av komponenten. Vi kommer att följa [delegeringsmönstret för Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) så att vi bara kan utöka delar av den befintliga Product Teaser-modellen.

Sling Models implementeras som Java och finns i **kärnmodulen** i det genererade projektet.

1. Öppna Acme Store-projektet i den utvecklingsmiljö du vill och navigera i **kärnmodulen** till: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** är ett Java-gränssnitt som vi har skapat tidigare och som utökar CIF **ProductTeaser** -gränssnittet.

1. Öppna sedan filen **MyProductTeaserImpl.java** som finns på: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` är implementeringsklassen för gränssnittet `MyProductTeaser`.

   Med hjälp av [delegeringsmönstret för segmenteringsmodeller](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) kan vi referera till `ProductTeaser` klassen via `sling:resourceSuperType` egenskapen:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   För alla metoder som vi inte vill åsidosätta eller ändra kan vi helt enkelt returnera värdet som `ProductTeaser` returneras:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. En av de extra tilläggspunkterna AEM CIF Core Components är den `AbstractProductRetriever` som gör att vi kan få tillgång till specifika produktattribut. Lägg till följande metod för att initiera `AbstractProductRetriever` i `init()` metoden:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
       }
   ...
   ```

1. Gör att du kan testa dessa ändringar genom att ändra det formaterade priset och åsidosätta logiken i `getFormattedPrice()`. Gör följande uppdateringar så att vi uttryckligen formaterar priset baserat på den tyska språkinställningen. (eller välj ett annat land!)

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   Observera hur objektet `productRetriever` ger oss åtkomst till `ProductInterface` objektet via `fetchProduct()` metoden. Du kan se alla [tillgängliga metoder här](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Obs!* Att ändra språkområdet till tyska är bara ett roligt exempel på hur man åsidosätter språket. I själva verket använder ProductTeaser [sidans språkområde för att fastställa formatet](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. Därefter måste vi uppdatera **productteaser.html** i modulen **ui.apps** så att den hänvisar till vår nya Sling Model på: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
       ...
   ```

   Spara ändringarna i `productteaser.html`.

1. Distribuera kodbasen till den lokala instansen av AEM. Eftersom ändringar gjorts i både **ui.apps** och **core** -modulerna kan du skapa och distribuera projektet från roten:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Öppna en webbläsare och navigera till: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Den här konsolen visar alla Sling Models som är registrerade i systemet. Dubbelkontrollera att MyTeaserModelImpl har distribuerats och mappats korrekt. Du ska kunna se något som:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Till sist går du till den plats där du skapade Product Teaser-komponenten och bör nu se priset med det tyska valutaformatet:

   ![Prisformatet har uppdaterats](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementera logiken isShowBadge {#implement-isshowbadge}

Nu när vi har haft en chans att experimentera med att åsidosätta Sling Model-metoder, kan vi implementera logiken för när vi ska visa det nya märket.

1. Gå tillbaka till din utvecklingsmiljö och öppna filen **MyProductTeaser.java** på: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. Lägg till en ny metod `isShowBadge()` i gränssnittet:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   Det här är en ny metod som vi kommer att införa för att kapsla in logiken för att visa märket eller inte.

1. Öppna sedan **MyProductTeaserImpl.java** igen `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`.

1. Logiken för hur lång tid det&quot;nya&quot; märket kommer att visas baseras på produktens `created_at` attribut. För att få tillgång till det attributet måste vi utöka **GraphQL** -frågan som utförs av ProductTeaser. Vi kan göra detta genom att uppdatera `init()` metoden i **MyProductTeaserImpl.java**:

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   Att utöka metoden är ett kraftfullt sätt att se till att fler produktattribut finns tillgängliga för resten av modellen. `extendProductQueryWith` Det minimerar även antalet frågor som körs.

   >[!NOTE]
   >I ovanstående kod använder vi`addCustomSimpleField` för att hämta `created_at` egenskapen. Detta visar hur du kan söka efter anpassade attribut som ingår i Magento-schemat.
   >
   > Egenskapen har dock faktiskt `created_at` implementerats som en del av [produktgränssnittet](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) och en bättre metod är att återanvända metoden så här: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. De flesta av de vanligaste schemaattributen har implementerats, så använd bara `addCustomSimpleField` för verkligt anpassade attribut.

1. Därefter ska vi implementera `isShowBadge()` metoden:

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   I ovanstående metod kontrollerar vi först om författaren har aktiverat märkordsfunktionen med kryssrutan. Sedan läser vi in värdet för egenskapen `age` som är inställd som en del av dialogrutan och som representerar det maximala antal dagar en produkt ska vara tills banderollen försvinner. Slutligen beräknar vi hur gammal produkten är baserat på `created_at` datumet. Om vi efter att ha jämfört de två värdena återgår vi `true` till att visa märket, `false` i alla andra fall.

1. Slutligen måste ytterligare ett tillägg göras till skriptet för att `productteaser.html` anropa `isShowBadge()` metoden. Öppna filen i `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Gör följande uppdatering:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Distribuera kodbasen till den lokala instansen av AEM. Eftersom ändringar gjorts i både **ui.apps** och **core** -modulerna kan du skapa och distribuera projektet från roten:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Återgå till AEM och ProductTeaser och experimentera med olika nummer för att visa produktens maximala ålder. Beroende på hur gammal produkten är kan du behöva ange ett mycket stort antal för att visa märket.

   ![Maximal produktålder 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Sök slutligen i AEM loggar för att se loggsatsen som anges i steg 5 ovan. Detta bör skriva ut värdet för den `created_at` egenskap som kommer från Magento. Du kan visa loggarna för AEM genom att öppna `error.log` filen. Den här filen finns under `crx-quickstart/logs/error.log` den plats där AEM har installerats. Du kan förvänta dig följande radalternativ:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Nu kan du verifiera att logiken vi implementerade är korrekt!

### Grattis {#congratulations}

Du har just skräddarsytt din första AEM CIF-komponent! Ladda ned det [färdiga lösningspaketet här](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Ytterligare resurser {#additional-resources}

* [AEM](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components)
* [Anpassa AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Anpassa kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
