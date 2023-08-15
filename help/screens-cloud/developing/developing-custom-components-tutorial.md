---
title: Utveckla en anpassad komponent för skärmar as a Cloud Service
description: I följande självstudiekurs går du igenom stegen för att skapa en anpassad komponent för AEM Screens. AEM Screens återanvänder många befintliga designmönster och tekniker från andra AEM produkter. I självstudiekursen beskrivs skillnader och speciella överväganden när du utvecklar för AEM Screens.
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 0%

---

# Utveckla en anpassad komponent för AEM Screens as a Cloud Service{#developing-a-custom-component-for-aem-screens}

I följande självstudiekurs går du igenom stegen för att skapa en anpassad komponent för AEM Screens. AEM Screens återanvänder många befintliga designmönster och tekniker från andra AEM produkter. I självstudiekursen beskrivs skillnader och speciella överväganden när du utvecklar för AEM Screens.

## Översikt {#overview}

Den här självstudiekursen är avsedd för utvecklare som inte har använt AEM Screens tidigare. I den här självstudiekursen är en enkel Hello World-komponent byggd för en Sequence-kanal i AEM Screens. I en dialogruta kan författare uppdatera den text som visas.


## Förutsättningar {#prerequisites}

Du behöver följande för att kunna slutföra den här självstudiekursen:

1. Senaste skärmfunktionspaket

1. AEM Screens Player

1. Lokal utvecklingsmiljö

Självstudiestegen och skärmbilderna utförs med **CRXDE Lite**. IDE kan också användas för att slutföra självstudiekursen. Mer information om hur du använder en utvecklingsmiljö [AEM finns här.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en)


## Projektinställningar {#project-setup}

Källkoden för ett skärmsprojekt hanteras vanligtvis som ett Maven-projekt med flera moduler. För att underlätta självstudiekursen har ett projekt förskapats med [AEM Project Archetype 13](https://github.com/adobe/aem-project-archetype). Mer information om [skapa ett projekt med Maven AEM Project Archetype finns här](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en).

1. Hämta och installera följande paket med [CRX Package Manager](http://localhost:4502/crx/packmgr/index.jsp):

[Hämta fil](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [Hämta fil](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **Valfritt** om du arbetar med Eclipse eller någon annan utvecklingsmiljö hämtar källpaketet nedan. Distribuera projektet till en lokal AEM med kommandot Maven:

   **`mvn -PautoInstallPackage clean install`**

   Start HelloWorld SRC Screens We.Retail Run Project

[Hämta fil](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. I [CRX Package Manager](http://localhost:4502/crx/packmgr/index.jsp)kontrollerar du att följande två paket är installerade:

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Skärmar, Web.Retail Kör Ui.Apps och Ui.Innehållspaket som installeras via CRX Package Manager](assets/crx-packages.png)

   Skärmar, Web.Retail Kör Ui.Apps och Ui.Innehållspaket som installeras via CRX Package Manager

1. The **screens-weretail-run.ui.apps** paketet installerar kod under `/apps/weretail-run`.

   Det här paketet innehåller koden som ansvarar för att återge anpassade komponenter för projektet. Det här paketet innehåller komponentkod och eventuell JavaScript eller CSS som behövs. Det här paketet bäddar även in **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** som innehåller all Java™-kod som krävs för projektet.

   >[!NOTE]
   >
   >I den här självstudiekursen skrivs ingen Java™-kod. Om mer komplex affärslogik behövs kan back-end Java™ skapas och driftsättas med Core Java™-paketet.

   ![Representation av ui.apps-koden i CRXDE Lite](/help/screens-cloud/developing/assets/uipps-contents.png)

   Representation av ui.apps-koden i CRXDE Lite

   The **`helloworld`** är bara en platshållare. Under kursen har funktioner lagts till som gör att en författare kan uppdatera det meddelande som visas av komponenten.

1. The **screens-weretail-run.ui.content** paketet installerar kod under:

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   Det här paketet innehåller det startinnehåll och den konfigurationsstruktur som krävs för projektet. **`/conf/we-retail-run`** innehåller alla konfigurationer för Web.Retail Run-projektet. **`/content/dam/we-retail-run`** innehåller start av digitala resurser för projektet. **`/content/screens/we-retail-run`** innehåller innehållsstrukturen för skärmar. Innehållet under alla dessa sökvägar uppdateras huvudsakligen i AEM. För att främja enhetlighet mellan miljöer (lokal, utvecklare, scen, produktion) sparas ofta en grundinnehållsstruktur i källkontrollen.

1. **Gå till AEM Screens > We.Retail Run-projektet:**

   Från AEM Start-meny > Klicka på Skärmar-ikonen. Verifiera att det går att se Kör projekt för webb.butik.

   ![we-retaiul-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## Skapa Hello World-komponenten {#hello-world-cmp}

Komponenten Hello World är en enkel komponent som gör att en användare kan ange ett meddelande som ska visas på skärmen. Komponenten är baserad på [AEM Screens Component Template: https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template).

AEM Screens har intressanta begränsningar som inte nödvändigtvis är sanna för traditionella WCM-webbplatskomponenter.

* De flesta skärmar-komponenter måste köras i helskärmsläge på de digitala signeringsenheterna
* De flesta skärmkomponenter måste vara inbäddade i sekvenskanalerna för att bildspel ska kunna genereras
* Redigering bör göra det möjligt att redigera enskilda komponenter i en sekvenskanal, så att återgivning av dem i helskärmsläge inte påverkas

1. I **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` (eller valfri IDE), navigera till `/apps/weretail-run/components/content/helloworld.`

   Lägg till följande egenskaper i `helloworld` komponent:

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![Egenskaper för /apps/weretail-run/components/content/helpWorld](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   Egenskaper för /apps/weretail-run/components/content/helpWorld

   The **`helloworld`** -komponenten utökar **grund/komponenter/parbase** så att den kan användas i en sekvenskanal.

1. Skapa en fil under `/apps/weretail-run/components/content/helloworld` namngiven `helloworld.html.`

   Fyll filen med följande:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (that is, on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, that is, edit, design, scaffolding, etc. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   Skärmkomponenter kräver två olika återgivningar beroende på vilken [redigeringsläge](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/authoring/author-environment-tools.html?lang=en#page-modes) används:

   1. **Produktion**: Förhandsgranska eller publicera (wcmmode=disabled)
   1. **Redigera**: används för alla andra redigeringslägen, t.ex. redigering, design, ställningar, utvecklare...

   `helloworld.html`fungerar som en växel, kontrollerar vilket redigeringsläge som är aktivt och dirigerar om till ett annat HTML-skript. En vanlig konvention som används för skärmkomponenter är att ha en `edit.html` skript för redigeringsläge och `production.html` skript för produktionsläge.

1. Skapa en fil under `/apps/weretail-run/components/content/helloworld` namngiven `production.html.`

   Fyll filen med följande:

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   Produktionskoden ovan gäller Hello World-komponenten. A `data-duration` -attributet inkluderas eftersom komponenten används på en sekvenskanal. The `data-duration` -attributet används av sekvenskanalen för att veta hur länge ett sekvensobjekt ska visas.

   Komponenten återger en `div` och `h1` med text. `${properties.message}` är en del av HTML-skriptet som matar ut innehållet i en JCR-egenskap med namnet `message`. En dialogruta skapas senare där användaren kan ange ett värde för `message` egenskapstext.

   Observera också att BEM-notation (Block Element Modifier) används med komponenten. BEM är en CSS-kodkonvention som gör det enklare att skapa återanvändbara komponenter. BEM är den beteckning som används av [AEM kärnkomponenter](https://github.com/adobe/aem-core-wcm-components/wiki/CSS-coding-conventions). <!-- WEBSITE WAS NOT ACCESSIBLE AS OF SEPTEMBER 1, 2022 More info can be found at: [https://getbem.com/](https://getbem.com/) -->

1. Skapa en fil under `/apps/weretail-run/components/content/helloworld` namngiven `edit.html.`

   Fyll filen med följande:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/edit.html
   
   */-->
   
   <!--/* if message populated */-->
   <div
    data-sly-test.message="${properties.message}"
    class="aem-Screens-editWrapper cmp-hello-world">
    <p class="cmp-hello-world__message">${message}</p>
   </div>
   
   <!--/* empty place holder */-->
   <div data-sly-test="${!message}"
        class="aem-Screens-editWrapper cq-placeholder cmp-hello-world"
        data-emptytext="${'Hello World' @ i18n, locale=request.locale}">
   </div>
   ```

   Redigeringsmarkeringen ovan gäller Hello World-komponenten. Det första blocket visar en redigeringsversion av komponenten om dialogmeddelandet har fyllts i.

   Det andra blocket återges om inget dialogrutemeddelande har angetts. The `cq-placeholder` och `data-emptytext` återge etiketten ***Hello World*** som platshållare i det fallet. Strängen för etiketten kan internationaliseras med i18n som stöd för redigering på flera språk.

1. **Copy Sscreens Image Dialog to be used for the Hello World component.**

   Det är enklast att börja från en befintlig dialogruta och sedan göra ändringar.

   1. Kopiera dialogrutan från: `/libs/screens/core/components/content/image/cq:dialog`
   1. Klistra in dialogrutan under `/apps/weretail-run/components/content/helloworld`

   ![copy-image-dialog](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **Uppdatera dialogrutan Hello World så att den innehåller en flik för meddelandet.**

   Uppdatera dialogrutan så att den matchar följande. JCR-nodstrukturen i den slutliga dialogrutan visas nedan i XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       jcr:title="Hello World"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content
           jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/coral/foundation/tabs"
           size="L">
           <items jcr:primaryType="nt:unstructured">
               <message
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Message"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <message
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                   fieldDescription="Message for component to display"
                                   fieldLabel="Message"
                                   name="./message"/>
                           </items>
                       </column>
                   </items>
               </message>
               <sequence
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Sequence"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <duration
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
                                   defaultValue=""
                                   fieldDescription="Amount of time the image is shown in the sequence, in milliseconds"
                                   fieldLabel="Duration (ms)"
                                   min="0"
                                   name="./duration"/>
                           </items>
                       </column>
                   </items>
               </sequence>
           </items>
       </content>
   </jcr:root>
   ```

   The `textfield` för meddelandet sparas i en egenskap med namnet `message` och `numberfield` för Varaktighet sparas i en egenskap med namnet `duration`. Båda dessa två egenskaper refereras i `/apps/weretail-run/components/content/helloworld/production.html` av HTML som `${properties.message}` och `${properties.duration}`.

   ![Hello World - slutförd dialogruta](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Hello World - slutförd dialogruta

## Skapa bibliotek på klientsidan {#clientlibs}

Med bibliotek på klientsidan kan du ordna och hantera CSS- och JavaScript-filer som behövs för en AEM implementering.

AEM Screens-komponenter återges annorlunda i redigeringsläge jämfört med förhandsgransknings-/produktionsläge. Två klientbibliotek skapas: ett för redigeringsläget och ett för Förhandsgranska/Produktion.

1. Skapa en mapp för klientbibliotek för Hello World-komponenten.

   Under `/apps/weretail-run/components/content/helloworld`, skapa en mapp med namnet `clientlibs`.

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. Under `clientlibs` mapp, skapa en nod med namnet `shared` av typen `cq:ClientLibraryFolder.`

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. Lägg till följande egenskaper i det delade klientbiblioteket:

   * `allowProxy` | Boolean | `true`

   * `categories`| Sträng[] | `cq.screens.components`

   ![Egenskaper för /apps/weretail-run/components/content/helpWorld/clientlibs/shared](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   Egenskaper för /apps/weretail-run/components/content/helpWorld/clientlibs/shared

   Egenskapen categories är en sträng som identifierar klientbiblioteket. Kategorin cq.screens.component används i både redigeringsläget och läget Förhandsgranska/produktion. Därför läses alla CSS/JS som definierats i SharedClientlib in i alla lägen.

   Det är en god vana att aldrig visa några sökvägar direkt för /apps i en produktionsmiljö. Egenskapen allowProxy ser till att klientbibliotekets CSS och JS refereras via ett prefix of/etc.clientlibs.

1. Skapa en fil med namnet `css.txt` under den delade mappen.

   Fyll filen med följande:

   ```
   #base=css
   
   styles.less
   ```

1. Skapa en mapp med namnet `css` under `shared` mapp. Lägga till en fil med namnet `style.less` under `css` mapp. Klientbibliotekens struktur bör nu se ut så här:

   ![2018-04-30_at_3_11pm](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   I stället för att skriva CSS direkt använder den här självstudien LESS. [LESS](https://lesscss.org/) är en populär CSS-förkompilator som stöder CSS-variabler, mixiner och funktioner. AEM klientbibliotek stöder LESS-kompilering. Sass eller andra förkompilatorer kan användas men måste kompileras utanför AEM.

1. Fylla `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` med följande:

   ```css
   /**
       Shared Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less
   
   **/
   
   .cmp-hello-world {
       background-color: #fff;
   
    &__message {
     color: #000;
     font-family: Helvetica;
     text-align:center;
    }
   }
   ```

1. Kopiera och klistra in `shared` klientbiblioteksmapp för att skapa ett klientbibliotek med namnet `production`.

   ![Kopiera det delade klientbiblioteket för att skapa ett nytt produktionsklientbibliotek](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   Kopiera det delade klientbiblioteket för att skapa ett produktionsklientbibliotek.

1. Uppdatera `categories` egenskapen för det produktionsklientbibliotek som ska `cq.screens.components.production.`

   Om du gör det ser du till att formaten bara läses in i förhandsvisnings-/produktionsläge.

   ![Egenskaper för /apps/weretail-run/components/content/help/world/clientlibs/production](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   Egenskaper för /apps/weretail-run/components/content/help/world/clientlibs/production

1. Fylla `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` med följande:

   ```css
   /**
       Production Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less
   
   **/
   .cmp-hello-world {
   
       height: 100%;
       width: 100%;
       position: fixed;
   
    &__message {
   
     position: relative;
     font-size: 5rem;
     top:25%;
    }
   }
   ```

   Ovanstående format visar meddelandet centrerat mitt på skärmen, men endast i produktionsläge.

En tredje klientbibliotekskategori: `cq.screens.components.edit` kan användas för att lägga till redigeringsspecifika format i komponenten.

| Kategorin Clientlib | Användning |
|---|---|
| `cq.screens.components` | Format och skript som delas mellan redigerings- och produktionslägen |
| `cq.screens.components.edit` | Format och skript som endast används i redigeringsläge |
| `cq.screens.components.production` | Format och skript som endast används i produktionsläge |

## Skapa en designsida {#design-page}

AEM Screens använder [statiska sidmallar](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-static.html?lang=en) och [Designkonfigurationer](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/siteandpage/default-components-designmode.html?lang=en) för globala ändringar. Designkonfigurationer används ofta för att konfigurera tillåtna komponenter för parsys i en kanal. Ett tips är att lagra dessa konfigurationer på ett appspecifikt sätt.

En sida för att köra webb.butik skapas nedan som lagrar alla konfigurationer som är specifika för Web.Retail Run-projektet.

1. I **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs`, navigera till `/apps/settings/wcm/designs`
1. Skapa en nod under designmappen med namnet `we-retail-run` med en typ av `cq:Page`.
1. Under `we-retail-run` sida, lägg till en annan nod med namnet `jcr:content` av typen `nt:unstructured`. Lägg till följande egenskaper i `jcr:content` nod:

   | Namn | Typ | Värde |
   |---|---|---|
   | jcr:title | Sträng | Vi.Retail Run |
   | sling:resourceType | Sträng | wcm/core/components/designer |
   | cq:doctype | Sträng | html_5 |

   ![Designsida på /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   Designsida på /apps/settings/wcm/designs/we-retail-run

## Skapa en sekvenskanal {#create-sequence-channel}

Hello World-komponenten är avsedd att användas på en sekvenskanal. Om du vill testa komponenten skapas en ny sekvenskanal.

1. Navigera AEM Start-menyn till **Skärmar** > **Vi.Retail Ru** n > och markera **Kanaler**.

1. Klicka på **Skapa** knapp

   1. Välj **Skapa entitet**

   ![2018-04-30_at_5_18pm](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. I guiden Skapa:

1. Mallsteg - välj **Sekvenskanal**

   1. Egenskapssteg

   * Fliken Grundläggande > Titel = **Inaktiv kanal**
   * Kanalflik > kontrollera **Gör kanalen online**

   ![inaktiv kanal](/help/screens-cloud/developing/assets/idle-channel.gif)

1. Öppna sidegenskaperna för inaktivitetskanalen. Uppdatera designfältet så att det pekar på `/apps/settings/wcm/designs/we-retail-run,`den designsida som skapades i föregående avsnitt.

   ![Designkonfiguration /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   Designkonfiguration som pekar på /apps/settings/wcm/designs/we-retail-run

1. Redigera den nyligen skapade inaktivitetskanalen så att du kan öppna den.

1. Växla sidläge till **Design** Läge.

   1. Klicka på **wrench** Ikon i Parsys så att du kan konfigurera tillåtna komponenter.

   1. Välj **Skärmar** gruppen och **Vi.Retail Run - Innehåll** grupp.

   ![2018-04-30_at_5_43pm](assets/2018-04-30_at_5_43pm.png)

1. Växla sidläge till **Redigera**. Komponenten Hello World kan nu läggas till på sidan och kombineras med andra sekvenskanalkomponenter.

   ![2018-04-30_at_5_53pm](assets/2018-04-30_at_5_53pm.png)

1. I **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par`, navigera till `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`. Lägg märke till `components` egenskapen inkluderar nu `group:Screens`, `group:We.Retail Run - Content`.

   ![Designkonfiguration under /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   Designkonfiguration under /apps/settings/wcm/designs/we-retail-run

## Mall för anpassade hanterare {#custom-handlers}

Om din anpassade komponent använder externa resurser, t.ex. resurser (bilder, videoklipp, teckensnitt och ikoner), särskilda återgivningar av resurser eller klientbibliotek (css och js), läggs dessa resurser inte automatiskt till i offlinekonfigurationen. Orsaken är att Adobe bara paketerar HTML-koden som standard.

För att du ska kunna anpassa och optimera de exakta resurserna som hämtas till spelaren har Adobe en tilläggsfunktion för anpassade komponenter som visar deras beroenden för offline-cachningslogiken i skärmar.

I avsnittet nedan visas mallen för anpassade offline-resurshanterare och minimikraven i `pom.xml` för det specifika projektet.

```java
package …;

import javax.annotation.Nonnull;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceUtil;
import org.apache.sling.api.resource.ValueMap;

import com.adobe.cq.screens.visitor.OfflineResourceHandler;

@Service(value = OfflineResourceHandler.class)
@Component(immediate = true)
public class MyCustomHandler extends AbstractResourceHandler {

 @Reference
 private …; // OSGi services injection

 /**
  * The resource types that are handled by the handler.
  * @return the handled resource types
  */
 @Nonnull
 @Override
 public String[] getSupportedResourceTypes() {
     return new String[] { … };
 }

 /**
  * Accept the provided resource, visit and traverse it as needed.
  * @param resource The resource to accept
  */
 @Override
 public void accept(@Nonnull Resource resource) {
     ValueMap properties = ResourceUtil.getValueMap(resource);
     
     /* You can directly add explicit paths for offline caching using the `visit`
        method of the visitor. */
     
     // retrieve a custom property from the component
     String myCustomRenditionUrl = properties.get("myCustomRenditionUrl", String.class);
     // adding that exact asset/rendition/path to the offline manifest
     this.visitor.visit(myCustomRenditionUrl);
     
     
     /* You can delegate handling for dependent resources so they are also added to
        the offline cache using the `accept` method of the visitor. */
     
     // retrieve a referenced dependent resource
     String referencedResourcePath = properties.get("myOtherResource", String.class);
     ResourceResolver resolver = resource.getResourceResolver();
     Resource referencedResource = resolver.getResource(referencedResourcePath);
     // let the handler for that resource handle it
     if (referencedResource != null) {
         this.visitor.accept(referencedResource);
     }
   }
}
```

Följande kod innehåller minimikraven i `pom.xml` för det specifika projektet:

```css
   <dependencies>
        …
        <!-- Felix annotations -->
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.9.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Screens core bundle with OfflineResourceHandler/AbstractResourceHandler -->
        <dependency>
            <groupId>com.adobe.cq.screens</groupId>
            <artifactId>com.adobe.cq.screens</artifactId>
            <version>1.5.90</version>
            <scope>provided</scope>
        </dependency>
        …
      </dependencies>
```

## Sammanställ allt {#putting-it-all-together}

I videon nedan visas den färdiga komponenten och hur den kan läggas till i en sekvenskanal. Kanalen läggs sedan till i en platsvisning och tilldelas till en skärmspelare.

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## Kod klar {#finished-code}

Nedan visas den färdiga koden från självstudiekursen. The **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** och **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip** är de kompilerade AEM. **SRC-screens-weretail-run-0.0.1.zip **är den okompilerade källkoden som kan distribueras med Maven.

[Hämta fil](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[Hämta fil](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[Hämta fil](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
