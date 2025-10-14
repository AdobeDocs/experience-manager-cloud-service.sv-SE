---
title: Konfigurera layoutbehållaren och layoutläget
description: Lär dig hur du konfigurerar layoutbehållare och layoutläge för att aktivera responsiva layouter för innehållsförfattare.
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 70a35cfeb163967b0f627d3ac6495f112d922974
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---


# Konfigurera layoutbehållaren och layoutläget {#configuring-layout-container-and-layout-mode}

Lär dig hur du konfigurerar layoutbehållare och layoutläge för att aktivera responsiva layouter för innehållsförfattare.

>[!TIP]
>
>I det här dokumentet beskrivs hur en webbplatsadministratör kan konfigurera layoutbehållaren så att den stöder responsiv webbdesign. Ytterligare resurser finns:
>
>* Information om hur du använder responsiva designfunktioner på en innehållssida finns i dokumentet [Responsiv layout.](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
>* För utvecklare beskrivs information om layoutbehållaren och det responsiva stödrastret i [Det responsiva designdokumentet &#x200B;](/help/implementing/developing/introduction/responsive-design.md) som innehåller tips och tips om hur du använder layoutbehållare och responsiva stödraster när du designar din plats.

## Ökning {#overview}

Responsiv layout är en mekanism för att förverkliga [responsiv webbdesign](https://en.wikipedia.org/wiki/Responsive_web_design). Detta gör att innehållsförfattaren kan skapa webbsidor som har en layout och dimensioner som är beroende av vilka enheter som användarna använder.

AEM implementerar en responsiv layout för dina sidor med en kombination av mekanismer:

* **[Layoutbehållare](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)** - Den här komponenten innehåller ett rutnätsstyckesystem där du kan lägga till och placera komponenter i ett responsivt rutnät.
   * Den kan användas som standardparsyta för sidan och/eller göras tillgänglig för författare i komponentwebbläsaren.
   * Standardkomponenten för **Layoutbehållare** definieras under `/libs/wcm/foundation/components/responsivegrid`.
   * Du kan definiera layoutbehållare:
      * Som en komponent som användaren kan lägga till på en sida.
      * Som standardparsys för sidan.
      * Som både en komponent och standardparsys.
         * Du kan ha layoutbehållaren som standard för sidan, samtidigt som användaren kan lägga till fler layoutbehållare i den, till exempel för att uppnå kolumnkontroll.
* **[Layoutläge](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)** - När layoutbehållaren har placerats på sidan kan du använda läget **Layout** för att placera innehåll i det responsiva rutnätet.
* **[Emulator](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)** - Det gör att du kan skapa och redigera responsiva webbplatser som ändrar layout efter enhetens/fönstrets storlek genom att ändra storlek på komponenterna interaktivt. Användaren kan sedan se hur innehållet återges med emulatorn.

Med dessa responsiva rutnätsmekanismer kan du:

* Använd brytpunkter (som indikerar enhetsgruppering) för att definiera olika innehållsbeteenden baserat på enhetslayout.
* Dölj komponenter baserat på enhetsgrupp (definiera på vilken brytpunkt en komponent ska döljas).
* Använd vågrät fäst mot rutnät (placera komponenter i rutnätet, ändra storlek efter behov, definiera när de ska komprimeras/omformas så att de ligger sida vid sida eller ovanför/nedanför).
* Uppnå kolumnkontroll.

>[!NOTE]
>
>När du skapar en webbplats från [Project Archetype](#addlink) eller från [standardwebbplatsmallen](#addlink) konfigureras den responsiva layouten i allmänhet. Annars måste du [aktivera layoutbehållarkomponenten](#enable-the-layout-container-component-for-page) för dina sidor.

## Aktivera emulatorn {#enabling-emulator}

[Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE) och [Standard Site Template](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template) har redan aktiverats för att använda emulatorn. Om du har utvecklat ditt eget innehåll som inte är baserat på kärnkomponenterna eller arkitekturen kan du läsa dokumentet [Responsiv design](/help/implementing/developing/introduction/responsive-design.md) för mer information om hur du utvecklar dina komponenter samtidigt som du utnyttjar dessa funktioner.

## Aktivera layoutläge för webbplatsen {#activate-layout-mode-for-your-site}

**Layout** gör att du kan använda emulatorn för att justera layouten för ditt innehåll för olika enheter. WKND-exempelwebbplatsen har redan aktiverats för **Layout**-läget. Följ de här stegen för att aktivera din egen webbplats.

### Konfigurera brytpunkter {#configure-breakpoints}

Brytpunkter är viktiga för responsiv design och definierar hur och när innehåll justeras till målenheten. Var dock försiktig eftersom varje brytpunkt du lägger in genererar ytterligare arbete åt författarna så att de får plats med innehållet. Många gånger kan det räcka med två brytpunkter, inklusive den standardbrytpunkt som alltid finns där. Adobe rekommenderar att du inte skapar fler än tre brytpunkter, inklusive standardvärdet, dvs. inte fler än två noder under `cq:responsive/breakpoint`.

* Brytpunkter har en rubrik och en bredd:
   * Titeln beskriver den generiska enhetsgrupperingen, med orientering om det behövs.
      * Till exempel `phone`, `tablet`
   * Bredden definierar den maximala bredden i pixlar för den allmänna enhetsgrupperingen.
      * Om till exempel brytpunktstelefonen har en bredd på 768 är det den maximala bredden för den layout som används för en telefonenhet.
* Brytpunkter kan definieras:
   * På sidmallen, från vilken inställningarna kopieras till alla sidor som skapas med den mallen.
   * På sidnoden, varifrån inställningarna ärvs av underordnade sidor.
* Brytpunkter visas som markörer högst upp i sidredigeraren när du använder emulatorn.
* Brytpunkter ärvs från den överordnade nodhierarkin och kan åsidosättas när så önskas.
* Det finns en standardbrytpunkt som täcker allt ovanför den senast konfigurerade brytpunkten.
* Brytpunkter kan definieras med CRXDE Lite eller XML.

Brytpunkter bör beaktas både för nya och befintliga projekt.

* Om du skapar ett nytt projekt bör du lägga till brytpunkter i mallarna.
* Om du migrerar ett befintligt projekt (med befintligt innehåll) måste du:
   * Lägg till brytpunkter i mallarna.
   * Lägg till samma brytpunkter på de befintliga sidorna.

På grund av arv behöver du bara göra detta för innehållets rotsida.

#### Konfigurera brytpunkter med CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Använd CRXDE Lite för att navigera till:

   * Din malldefinition.
   * Sidans `jcr:content`-nod.

1. Skapa noden under `jcr:content`:

   * Namn: `cq:responsive`
   * Typ: `nt:unstructured`

1. Skapa noden här:

   * Namn: `breakpoints`
   * Typ: `nt:unstructured`

1. Under brytpunktsnoden kan du skapa valfritt antal brytpunkter. Varje definition är en enda nod med följande egenskaper:

   * Namn: `<descriptive name>`
   * Typ: `nt:unstructured`
   * Titel: `String <descriptive title seen in Emulator>`
   * Bredd: `Decimal <value of breakpoint>`

#### Konfigurera brytpunkter med XML {#configuring-breakpoints-using-xml}

Brytpunkter finns i avsnittet `<jcr:content>` i `.context.html` under lämplig mallmapp (eller innehållsmapp).

En exempeldefinition:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## Aktivera komponentstorleksändring för sidan {#enable-component-resizing-for-the-page}

Att ändra storlek på komponenter i **Layout** -läge är en viktig del av responsiv design, som kan användas i WKND-exempelwebbplatsen. Följ de här stegen för att aktivera din egen webbplats.

### Ange layoutbehållare som huvudparsys {#set-layout-container-as-main-parsys}

Om du vill ange att huvudparsytan på sidan ska vara en layoutbehållare definierar du parsytorna som:

`wcm/foundation/components/responsivegrid`

I antingen

* Sidkomponent
* Sidmall (för framtida bruk)

I följande två exempel illustreras definitionen:

* **HTML:**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### Inkludera responsiv CSS {#include-the-responsive-css}

#### CSS för brytpunkter med LESS {#css-for-breakpoints-using-less}

AEM använder LESS för att generera delar av den CSS som behövs, och dessa måste ingå i dina projekt.

Du måste skapa ett [klientbibliotek](/help/implementing/developing/introduction/clientlibs.md) för att kunna tillhandahålla ytterligare konfigurations- och funktionsanrop. Följande LESS-extrakt är ett exempel på det minsta som du måste lägga till i projektet:

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

Basrutnätsdefinitionen finns under:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Fundera på formatering {#styling-considerations}

Storleken på komponenter som finns i en responsiv behållare ändras (tillsammans med deras respektive HTML DOM-element) beroende på stödrastrets responsiva storlek. Därför bör du under dessa omständigheter undvika (eller uppdatera) definitioner av DOM-element med fast bredd (som finns).

Till exempel:

* Före:

   * `width=100px`

* Efter:

   * `max-width=100px`

#### Storleksändring och adaptiv bildkompatibilitet {#resizing-and-adaptive-image-compliance}

Om du ändrar storlek på en komponent i rutnätet utlöses följande avlyssnare om det är lämpligt:

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

Om du vill ändra storlek på och uppdatera innehållet i en adaptiv bild som ingår i ett responsivt stödraster måste du lägga till en `afterEdit`-uppsättning till `REFRESH_PAGE`-avlyssnare i `EditConfig`-filen för alla ingående komponenter.

Till exempel:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Den adaptiva bildmekanismen görs tillgänglig via ett skript som styr valet av rätt bild för fönstrets aktuella storlek. Den aktiveras när DOM är redo eller när en dedikerad händelse tas emot. För närvarande måste sidan uppdateras för att korrekt återspegla resultatet av användarens åtgärd.

>[!CAUTION]
>
>Klientlibs för anpassade formatmallar måste läsas in som en del av sidhuvudet för att de ska fungera korrekt både när de skapas och publiceras.

## Aktivera layoutbehållarkomponenten för sidan {#enable-the-layout-container-component-for-page}

För effektiv responsiv layout måste innehållsförfattaren kunna dra instanser av komponenten Layoutbehållare till sidan. Detta är redan aktiverat för WKND-exempelwebbplatsen. Följ de här stegen för att aktivera din egen webbplats.

### Aktivera layoutbehållarkomponenten för sidredigering {#enable-the-layout-container-component-for-page-editing}

Om du vill att författare ska kunna lägga till fler responsiva rutnät på innehållssidorna måste du aktivera layoutbehållarkomponenten för sidan. Du kan göra detta med:

* **Via redigeringsmiljön** - [Redigera sidmallar](/help/sites-cloud/authoring/page-editor/templates.md) för att aktivera layoutbehållaren för en sida.
* **Komponentdefinition** - Använd `allowedComponent` eller en statisk inkludering när du definierar komponenten.

### Konfigurera stödrastret för layoutbehållaren {#configure-the-grid-of-the-layout-container}

Du kan konfigurera antalet kolumner som är tillgängliga för varje instans av layoutbehållaren [genom att redigera sidmallarna](/help/sites-cloud/authoring/page-editor/templates.md).

### Kapslade responsiva stödraster {#nested-responsive-grids}

Adobe rekommenderade metod är att hålla strukturen så platt som möjligt.

Om du inte kan undvika att använda kapslade responsiva rutnät läser du i utvecklardokumentet [Responsiv design.](/help/implementing/developing/introduction/responsive-design.md#nested-responsive-grids)
