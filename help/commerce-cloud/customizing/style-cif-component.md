---
title: Stil AEM CIF-kärnkomponenter
description: Stil AEM CIF-kärnkomponenter
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 0%

---


# Stil AEM CIF-kärnkomponenter {#style-aem-cif-core-components}

CIF-projektets [projekttyp](https://github.com/adobe/aem-cif-project-archetype) skapar ett minimalt CIF-projekt i Adobe Experience Manager (AEM) som utgångspunkt för kundprojekt med [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components). En standardstil, som kallas Venia-varumärket, används till att börja med på webbplatsen. I den här självstudiekursen kommer du att inspektera ett nytt AEM CIF-projekt, som genereras av arkitypen och förstå hur CSS och JavaScript som används av AEM CIF Core-komponenter är organiserade. Du skapar också ett nytt format med CSS som ersätter standardformatet för Product Teaser-komponenten.

![Vad du ska bygga](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> En ny stil kommer att implementeras för Product Teaser-komponenten som liknar ett kort.

## Förutsättningar {#prerequisites}

Följande verktyg och tekniker krävs:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) eller [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (endast AEM 6.5+)
* [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
* Adobe Experience Manager (lokal instans)
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/sp-release-notes.html)
* Magento som kör en [version som är kompatibel med arketypen](https://github.com/adobe/aem-cif-project-archetype#requirements)

## Generera ett projekt {#generate-project}

Vi genererar ett nytt AEM CIF-projekt med [CIF-projekttypen](https://github.com/adobe/aem-cif-project-archetype) och åsidosätter sedan standardstilarna.

**Du kan använda ett befintligt projekt** (baserat på CIF-projekttypen) och hoppa över det här avsnittet.

1. Ta reda på den senaste versionen av CIF-projektarkitekturen genom att visa [den senaste versionen på GitHub](https://github.com/adobe/aem-cif-project-archetype/releases/latest). I nästa steg ersätter du `x.y.z` med den senaste versionen.

1. Kör följande Maven-kommando för att generera ett nytt projekt i [gruppläge](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html).

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. Bygg och distribuera projektet till en lokal instans av AEM:

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Lägg till nödvändiga OSGi-konfigurationer för att ansluta AEM till en Magento-instans eller lägga till konfigurationerna i det nyskapade projektet.

1. Nu bör du ha en fungerande version av en storefront som är ansluten till en Magento-instans. Navigera till `US` > `Home` sida: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Du ser att butiken för närvarande använder temat Venia. När du expanderar huvudmenyn för butiken bör du se olika kategorier som anger att anslutningen Magento fungerar.

   ![Storefront konfigurerat med Venedig-tema](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## Introduktion till klientbibliotek {#introduction-to-client-libraries}

Den CSS och JavaScript som ansvarar för att återge temat/formaten för butiken hanteras i AEM av ett [klientbibliotek](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html) eller klientlibs för kort. Klientbibliotek erbjuder en mekanism för att ordna CSS och Javascript i ett projekts kod och sedan leverera på sidan.

Det sätt vi kan använda varumärkesspecifika format på AEM CIF Core Components är genom att lägga till och åsidosätta CSS som hanteras av dessa klientbibliotek. Det är viktigt att förstå hur klientbibliotek är strukturerade och inkluderas på sidan.

### Project Client Libraries {#project-client-libraries}

Därefter undersöker vi klientbiblioteken som genereras automatiskt av typen archive. Använd den utvecklingsmiljö du väljer för att [importera projektet som skapades i föregående övning](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment).

1. Navigera och expandera modulen **ui.apps** och expandera mapphierarkin till: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps clientlibs](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   Det finns två mappar under, **clientlib-base** och **tema**.

1. **clientlib-base** - Det här är ett tomt klientbibliotek som helt enkelt bäddar in nödvändiga beroenden från [AEM Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html).

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   Nedan finns XML-definitionen för **clientlib-base** ( `.content.xml` filen):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` är kategorin för det här klientbiblioteket. Tänk på en kategori som en tagg. Detta används för att inkludera eller bädda in biblioteket på sidan.

   Observera egenskapen `embed` och arrayen för andra clientlib-kategorier. Var och en av dessa kategorier representerar ett klientbibliotek. Exempel: `core.wcm.components.accordion.v1` innehåller det javascript som behövs för att [dragspelskomponenten](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) ska fungera.

   Genom att använda egenskaperna `embed` och `categories` kan du hantera och inkludera klientbibliotek från olika projekt.

   `allowProxy=true` ser till att klientbibliotekets CSS och JavaScript hanteras från en sökväg som har följande prefix: `/etc.clientlibs`. Detta garanterar att programkod under `/apps` skyddas från slutanvändare, men CSS och JavaScript som krävs för att webbplatsen ska fungera kan hanteras anonymt. Mer information om egenskapen [allowProxy finns här](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **tema** - Det här är klientbiblioteket som innehåller starttemat och CSS för CIF-projektet. Det här klientbiblioteket är utformat för att anpassas vid varje implementering och det är praktiskt att börja med några befintliga format så att komponenterna kan börja med.

   ![temaklientbibliotek](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   Nedan finns XML-definitionen för **temat**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` är kategorin för det här klientbiblioteket och så här inkluderas klientbiblioteket på sidan.

1. Under **temats** klientbibliotek ska du se en fil med namnet **css.txt** som finns på: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   Css. **txt** (och **js.txt**) fungerar som manifest som styr i vilken ordning enskilda filer inkluderas i den slutliga CSS-filen. Ordningen är viktig för både CSS och JavaScript, och det är bra att kunna skapa flera filer för att hantera koden bättre. När du tittar igenom **css.txt** -filen ser du att filerna är ordnade efter de komponenter som formaten tillämpas på.

1. Inspect CSS-filerna under **temat/komponenterna** för att få en uppfattning om objektkomponentformaten. Vi uppdaterar några av de här filerna senare i självstudiekursen.

### Inkludering av klientbibliotek med bassidkomponent

Därefter undersöker vi hur klientbibliotek inkluderas på en sida med hjälp av [HTML](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) och komponenten Page.

1. I modulen **ui.apps** navigerar du till `page` komponentdefinitionen under: `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. Den här **sidkomponenten** , som genereras av arkitypen, är startpunkten som används för att återge alla sidor i projektet.

1. Om du inspekterar **sidkomponentens** definition (`page/.content.xml`) kommer du att märka en egenskap `sling:resourceSuperType` som pekar på `core/cif/components/structure/page/v1/page`. Det innebär att **sidkomponenten** i projektet (Acme) ärver alla funktioner i [CIF Core Page](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) -komponenten och gör att vi kan hantera mindre kod.

1. Under **sidkomponenten** finns två filer: **customheaderlibs.html** och **customfooterlibs.html**.

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** är ett HTML-skript som återges i sidhuvudet. Det är ett vanligt skript som åsidosätter och lägger till projektspecifik logik. I det här fallet använder vi den för att inkludera klientbiblioteket med en kategori av `acme.wcm.base`. Efter bästa praxis för webbutveckling tar vi bara med CSS i sidhuvudet.

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** är ett HTML-skript som återges längst ned på sidan, precis före den avslutande `</body>` taggen. Återigen används kategorin för `acme.wcm.base` , men den här gången läses bara JavaScript för klientbiblioteket in.

När du ändrar HTML-skript för **sidkomponenten** är det så som `acme.wcm.base` inkluderas på alla sidor. Men hur är det `acme.theme`? I nästa övning ska vi titta på ett annat alternativ för att inkludera klientbibliotek.

### Inkludering av klientbibliotek med sidmallar {#client-library-inclusion-pagetemplates}

Det finns flera alternativ för hur du inkluderar ett klientbibliotek. Därefter undersöker vi hur det genererade projektet innehåller temats klientbibliotek via [Sidmallar](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html).

Öppna en ny webbläsare och logga in i den AEM där du distribuerade projektet i början av kursen.

1. Gå till **Verktyg** > **Allmänt** > **Mallar** på AEM startskärmen.

   ![Mallnavigering](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Navigera till **Acme Store-konfigurationsmappen** . Öppna **kategorisidmallen** genom att välja *pennikonen* .

   ![mallkort för kategorisida](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. I det övre vänstra hörnet markerar du ikonen **Sidinformation** och klickar på **Sidprofil**.

   ![Menyalternativ för sidpolicy](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. Då öppnas sidprincipen för katalogsidmallen:

   ![Sidprofil - katalogsida](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   Till höger ser du en lista över **kategorier** för klientbibliotek som ska inkluderas på alla sidor som använder den här mallen.

   * **wcm.foundation.components.page.responsive** - Tillhandahåller den CSS som behövs för att författare ska kunna aktivera [responsiva layoutkontroller](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/siteandpage/responsive-layout.html) .
   * **acme.theme** - Det här är starttemat som arketypen genererar automatiskt. Som standard är den här stilen som Venia-demobutiken. Men som du kan se av namnet är det tänkt att anpassas efter projektimplementeringen. *Det här är vad vi kommer att ändra i nästa avsnitt!*
   * **core.CIF.components.response** - Detta är ett kompilerat klientbibliotek med flera React-komponenter som används för dynamiska funktioner som Kundvagnen. Mer [information finns här](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   Observera att andra mallar använder samma princip, **Innehållssida**, **Landningssida** osv. Genom att återanvända samma policy kan vi se till att samma klientbibliotek inkluderas på alla sidor.

   Fördelen med att använda mallar och sidprofiler för att hantera inkludering av klientbibliotek är att du kan ändra principen per mall. Du kanske hanterar två olika varumärken inom samma AEM. Varje varumärke har sin egen stil eller *tema* , men basbiblioteken och koden är desamma. Om du har ett större klientbibliotek som du bara vill visa på vissa sidor kan du skapa en unik sidprofil för just den mallen. Den andra fördelen

### Verifiera klientbibliotek på sidan {#verify-client-libraries}

Nu har vi granskat hur du inkluderar klientbibliotek med HTML med **customheaderlibs.html** och **customfoterlibs.html** -skript och hur mallens sidpolicy kan användas för att inkludera ytterligare klientbibliotek. Därefter kontrollerar vi om klientbiblioteken finns med på webbplatsen.

1. På AEM startsida går du till **Sites** > **Acme Store** > **United States** > **English** och öppnar sidan för redigering: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Välj menyn **Sidinformation** och klicka på **Visa som publicerad**:

   ![Visa som publicerad](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   Sidan öppnas utan att någon av författarens javascript-skript AEM, som det skulle se ut på den publicerade webbplatsen. Observera att frågeparametern är `?wcmmode=disabled` tillagd på URL:en. När du utvecklar CSS och Javascript är det en god vana att använda den här parametern för att förenkla sidan utan att skriva ut något från AEM författare.

1. Visa sidkällan så bör du kunna identifiera följande klientbibliotek: **acme.wcm.base**, **wcm.foundation.components.page.responsive**, **acme.theme**, **core.cif.components.rea**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## Stila Product Teaser {#style-product-teaser}

Nu när vi förstår klientbiblioteksstrukturen som genereras av typen archipe kan vi börja anpassa AEM CIF Core Components. Vi ska ändra stilarna på Product Teaser-komponenten så att den ser mer ut som ett&quot;kort&quot;.

### Skapa Product Teaser {#author-product-teaser}

Som ett första steg ska vi lägga till en ny instans av Product Teaser-komponenten på hemsidan på vår webbplats med hjälp av de AEM utvecklingsverktygen.

1. Öppna en ny flik i webbläsaren och gå till webbplatsens **hemsida** : [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Infoga en ny **Product Teaser** Component i sidans huvudlayoutbehållare.

   ![Insert Product Teaser](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. Expandera sidopanelen (om den inte redan är aktiverad) och växla till listrutan **Produkter**. Här visas en lista över tillgängliga produkter från en ansluten Magento-instans. Välj en produkt och **dra och släpp** den i **Product Teaser** -komponenten på sidan.

   ![Dra och släpp Product Teaser](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > Observera att du även kan konfigurera den visade produkten genom att konfigurera komponenten med hjälp av dialogrutan (klicka på *skiftnyckelsikonen* ).

1. Du bör nu se en produkt som visas av Product Teaser. Produktens namn och produktens pris är standardattribut som visas.

   ![Product Teaser - standardstil](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Uppdatera CSS för Product Teaser {#update-css-product-teaser}

Därefter ska vi ändra CSS i **temats** klientbibliotek för att implementera en kortliknande stil för Product Teaser.

Återgå till utvecklingsmiljön och det genererade projektet.

1. I modulen **ui.apps** navigerar du till mappen: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. Här definieras alla stilar för Product Teaser.

1. Öppna filen **teaser.css** och uppdatera motsvarande CSS-regler (eller ladda ned [lösningen teaser.css file](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) and replace).

   Lägg till en skugga och ta med rundade hörn i Product Teaser.

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   Ändra bildens kantlinje i Product Teaser.

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
    }
   ```

   Uppdatera produktens namn så att det visas längst ned på teaser och ändra textfärgen.

   ```css
   .productteaser .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

   Uppdatera produktens pris så att det också visas längst ned på teaser och ändra textfärgen.

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   Uppdatera mediefrågan längst ned för att stapla namnet och priset på skärmar som är mindre än 992 px.

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   Spara ändringarna i **teaser.css**. Du kan hämta [filen teaser.css här](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css).

1. Distribuera uppdateringarna i modulen **ui.apps** för att AEM med hjälp av dina Maven-kunskaper från en kommandoradsterminal:

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >Det finns ytterligare [IDE-inställningar och -verktyg](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) som kan synkronisera projektfiler direkt till en lokal AEM utan att behöva utföra en fullständig Maven-konstruktion.

### Visa uppdaterad Product Teaser {#view-updated-product-teaser}

När koden för projektet har distribuerats till AEM bör vi nu kunna se ändringarna i Product Teaser.

1. Gå tillbaka till webbläsaren och uppdatera hemsidan: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). Du bör se hur de uppdaterade produktmallarna används.

   ![Uppdaterad Product Teaser-stil](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. Experimentera genom att lägga till ytterligare produktutbildningar. Använd layoutläget om du vill ändra komponenternas bredd och förskjutning för att visa flera scener på en rad.

   ![Flera produkttekniker](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >Varje produktteaser innehåller samma stil.

### Felsökning {#troubleshooting}

I [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) kan du kontrollera att den uppdaterade CSS-filen har distribuerats: [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

När du distribuerar nya CSS- och/eller JavaScript-filer är det också viktigt att kontrollera att webbläsaren inte hanterar inaktuella filer. Du kan ta bort detta genom att rensa webbläsarens cache eller starta en ny webbläsarsession.

AEM försöker också cachelagra klientbibliotek för att få prestandan. Efter en koddistribution skickas de äldre filerna ibland. Du kan göra AEM klientbibliotekscachen ogiltig manuellt med verktyget [](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)Återskapa klientbibliotek. *Ogiltiga cacheminnen är att föredra om du misstänker att AEM har cachelagrat en gammal version av ett klientbibliotek. Det är ineffektivt och tidskrävande att återskapa bibliotek.*

### Grattis {#congratulations}

Du har just formaterat din första AEM CIF Core Component!

### Bonus Challenge {#bonus-challenge}

Använd [AEM Style System](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) för att skapa två format som kan aktiveras/inaktiveras av en innehållsförfattare. [Utveckla med Style System](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) innehåller detaljerade steg och information om hur du uppnår detta.

![Bonus Challenge - system av olika slag](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## Ytterligare resurser {#additional-resources}

* [AEM CIF-arkityp](https://github.com/adobe/aem-cif-project-archetype)

* [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components)

* [Konfigurera en lokal AEM utvecklingsmiljö](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [Klientbibliotek](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html)
* [Komma igång med AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [Utveckla med Style System](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
