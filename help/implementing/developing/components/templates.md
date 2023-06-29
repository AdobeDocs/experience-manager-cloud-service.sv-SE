---
title: Sidmallar
description: Sidmallar används när du skapar en sida som används som bas för den nya sidan
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 0%

---

# Sidmallar {#page-templates}

När du skapar en sida måste du välja en mall. Sidmallen används som bas för den nya sidan. Mallen definierar strukturen för den resulterande sidan, allt ursprungligt innehåll och de komponenter som kan användas (designegenskaper). Detta har flera fördelar:

* Med sidmallar kan skribenter [skapa och redigera mallar](/help/sites-cloud/authoring/features/templates.md).
   * Sådana specialister kallas **mallskapare**
   * Mallförfattare måste vara medlemmar i `template-authors` grupp.
* Sidmallar behåller en dynamisk anslutning till alla sidor som skapas från dem. Detta säkerställer att alla ändringar i mallen återspeglas på själva sidorna.
* Sidmallar gör sidkomponenten mer generisk så att huvudsidkomponenten kan användas utan anpassning.

Med Sidmallar isoleras de delar som utgör en sida i komponenterna. Du kan konfigurera nödvändiga kombinationer av komponenter i ett användargränssnitt, vilket eliminerar behovet av att utveckla en ny sidkomponent för varje sidvariant.

Det här dokumentet:

* Ger en översikt över hur du skapar en sidmall
* Beskriver de admin-/utvecklaråtgärder som krävs för att skapa redigerbara mallar
* Beskriver de tekniska grunderna för redigerbara mallar
* Beskriver hur AEM utvärderar en malls tillgänglighet

>[!NOTE]
>
>Det här dokumentet förutsätter att du redan är bekant med att skapa och redigera mallar. Se redigeringsdokumentet [Skapa sidmallar](/help/sites-cloud/authoring/features/templates.md), som beskriver funktionerna i redigerbara mallar så som de visas för mallskaparen.

>[!TIP]
>
>[WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md) fördjupar sig i hur du använder sidmallar genom att implementera ett exempel och är mycket användbart för att förstå hur du konfigurerar en mall i ett nytt projekt

## Skapa en ny mall {#creating-a-new-template}

Skapa sidmallar görs i första hand med [mallkonsol och mallredigerare](/help/sites-cloud/authoring/features/templates.md) av en mallskapare. I det här avsnittet ges en översikt över processen och en beskrivning av vad som händer på teknisk nivå.

När du skapar en ny redigerbar mall:

1. Skapa en [mapp för mallarna](#template-folders). Detta är inte obligatoriskt, men vi rekommenderar bästa praxis.
1. Välj en [malltyp](#template-type). Detta kopieras för att skapa [malldefinition](#template-definitions).

   >[!NOTE]
   >
   >Ett urval av malltyper finns färdiga. Du kan också [skapa egna webbplatsspecifika malltyper](#creating-template-types) vid behov.

1. Konfigurera den nya mallens struktur, innehållsprinciper, ursprungliga innehåll och layout.

   **Struktur**

   * Strukturen gör att du kan definiera komponenter och innehåll för mallen.
   * Komponenter som definieras i mallstrukturen kan inte flyttas till en resultatsida eller tas bort från eventuella resultatsidor.
   * Om du vill att sidförfattare ska kunna lägga till och ta bort komponenter lägger du till ett styckesystem i mallen.
   * Komponenter kan låsas upp och låsas igen så att du kan definiera ursprungligt innehåll.

   Mer information om hur en mallskapare definierar strukturen finns i [Skapa sidmallar](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   För teknisk information om strukturen, se [Struktur](#structure) i det här dokumentet.

   **Profiler**

   * Innehållsprinciperna definierar designegenskaperna för en komponent.

      * Till exempel de tillgängliga komponenterna eller minimi-/maximidimensionerna.

   * Dessa gäller för mallen (och sidor som skapas med mallen).

   Mer information om hur en mallskapare definierar principer finns i [Skapa sidmallar](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Teknisk information om profiler finns i [Innehållsprofiler](#content-policies) i det här dokumentet.

   **Ursprungligt innehåll**

   * Ursprungligt innehåll definierar innehåll som visas när en sida skapas baserat på mallen.
   * Startinnehållet kan sedan redigeras av sidförfattare.

   Mer information om hur en mallskapare definierar strukturen finns i [Skapa sidmallar](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   Teknisk information om ursprungligt innehåll finns på [Ursprungligt innehåll](#initial-content) i det här dokumentet.

   **Layout**

   * Du kan definiera mallayouten för ett antal olika enheter.
   * Responsiv layout för mallar fungerar på samma sätt som för sidredigering.

   Mer information om hur en mallskapare definierar mallayouten finns i [Skapa sidmallar](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   Mer teknisk information om mallayout finns i [Layout](#layout) i det här dokumentet.

1. Aktivera mallen och tillåt den sedan för specifika innehållsträd.

   * En mall kan aktiveras eller inaktiveras för att göra den tillgänglig eller inte tillgänglig för sidförfattare.
   * En mall kan göras tillgänglig eller otillgänglig för vissa sidgrenar.

   Mer information om hur en mallskapare aktiverar en mall finns i [Skapa sidmallar](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Teknisk information om hur du aktiverar en mall finns i [Aktivera och tillåta en mall för oss](#enabling-and-allowing-a-template-for-use)e i det här dokumentet

1. Använd det för att skapa innehållssidor.

   * När du använder en mall för att skapa en ny sida finns det ingen synlig skillnad och ingen indikation mellan statiska och redigerbara mallar.
   * För sidförfattaren är processen genomskinlig.

   Mer information om hur en sidförfattare använder mallar för att skapa en sida finns i [Skapa och ordna sidor](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Teknisk information om hur du skapar sidor med redigerbara mallar finns i [Gällande innehållssidor](#resultant-content-pages) i det här dokumentet.

>[!TIP]
>
>Ange aldrig någon information som behöver internationaliseras i en mall. För internalisering [lokaliseringsfunktioner för kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) rekommenderas.

>[!NOTE]
>
>Mallar är kraftfulla verktyg som effektiviserar arbetsflödet för att skapa sidor. Alltför många mallar kan överbelasta författarna och göra det förvirrande att skapa sidor. En bra tumregel är att hålla antalet mallar under 100.
>
>Adobe rekommenderar inte att ha fler än 1 000 mallar på grund av potentiella prestandaeffekter.

>[!NOTE]
>
>Redigerarens klientbibliotek förutsätter att det finns `cq.shared` namnutrymme på innehållssidor och om det inte finns något JavaScript-fel `Uncaught TypeError: Cannot read property 'shared' of undefined` blir resultatet.
>
>Alla exempelinnehållssidor innehåller `cq.shared`så allt innehåll som baseras på dem automatiskt innehåller `cq.shared`. Om du däremot bestämmer dig för att skapa egna innehållssidor från grunden utan att basera dem på exempelinnehåll måste du se till att inkludera `cq.shared` namnutrymme.
>
>Se [Använda bibliotek på klientsidan](/help/implementing/developing/introduction/clientlibs.md) för ytterligare information.



## Mallmappar {#template-folders}

Du kan använda följande mappar för att ordna dina mallar:

* `global`
* Webbplatsspecifik

>[!NOTE]
>
>Även om du kan kapsla dina mappar när de visas i **Mallar** konsolen som visas som en platt struktur.

I en AEM `global` mappen finns redan i mallkonsolen. Detta innehåller standardmallar och fungerar som reserv om inga principer och/eller malltyper hittas i den aktuella mappen. Du kan lägga till dina standardmallar i den här mappen eller skapa en ny mapp (rekommenderas).

>[!NOTE]
>
>Det är bäst att skapa en ny mapp för dina anpassade mallar och inte använda `global` mapp.

>[!CAUTION]
>
>Mappar måste skapas av en användare med `admin` rättigheter.

Malltyper och profiler ärvs i alla mappar enligt följande prioritetsordning:

1. Aktuell mapp
1. Överordnad(e) till aktuell mapp
1. `/conf/global`
1. `/apps`
1. `/libs`

En lista över alla tillåtna poster skapas. Om några konfigurationer överlappar ( `path`/ `label`) visas bara den instans som ligger närmast den aktuella mappen för användaren.

Om du vill skapa en ny mapp kan du göra det här:

* Programmerat eller med CRXDE Lite
* Använda [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## Använda CRXDE Lite {#using-crxde-lite}

1. En ny mapp (under /conf) kan skapas för din instans antingen programmatiskt eller med CRXDE Lite.

   Följande struktur måste användas:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Du kan sedan definiera följande egenskaper på mappens rotnod:

   `<your-folder-name> [sling:Folder]`

   * Namn: `jcr:title`
   * Typ: `String`
   * Värde: Den rubrik (för mappen) som du vill ska visas i **Mallar** konsol.

1. Förutom de vanliga redigeringsbehörigheterna och -behörigheterna (till exempel `content-authors`) måste du nu tilldela grupper och definiera de åtkomstbehörigheter som krävs för att författarna ska kunna skapa mallar i den nya mappen.

   The `template-authors` grupp är standardgruppen som måste tilldelas. Se avsnittet [Behörighetslistor och grupper](#acls-and-groups) för mer information.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Använda Konfigurationsläsaren {#using-the-configuration-browser}

1. Gå till **Global navigering** -> **verktyg** > [**Konfigurationsläsaren**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   De befintliga mapparna visas till vänster, inklusive `global` mapp.

1. Klicka **Skapa**.
1. I **Skapa konfiguration** måste följande fält konfigureras:

   * **Titel**: Ange en rubrik för konfigurationsmappen
   * **Redigerbara mallar**: Markera för att tillåta redigerbara mallar i den här mappen

1. Klicka **Skapa**

>[!NOTE]
>
>I [Configuration Browser,](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) kan du redigera den globala mappen och aktivera **Redigerbara mallar** om du vill skapa mallar i den här mappen, men detta är inte den bästa metoden.

### Behörighetslistor och grupper {#acls-and-groups}

När mallmapparna har skapats (antingen via CRXDE eller med Configuration Browser) måste åtkomstkontrollistor definieras för rätt grupper för mallmapparna för att säkerställa rätt säkerhet.

Mallmappar för [WKND, genomgång](/help/implementing/developing/introduction/develop-wknd-tutorial.md) kan användas som exempel.

#### Mallförfattargruppen {#the-template-authors-group}

The `template-authors` grupp är den grupp som används för att hantera åtkomst till mallar och levereras som standard med AEM, men är tom. Användare måste läggas till i gruppen för projektet/webbplatsen.

>[!CAUTION]
>
>The `template-authors` grupp är bara avsedd för användare som måste kunna skapa nya mallar.
>
>Att redigera mallar är mycket kraftfullt och om det inte görs på rätt sätt kan befintliga mallar brytas. Därför bör denna roll fokuseras och endast omfatta kvalificerade användare.

Följande tabell visar vilka behörigheter som krävs för mallredigering.

<table>
 <tbody>
  <tr>
   <th>Bana</th>
   <th>Roll/grupp</th>
   <th>Behörigheter<br /> </th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Mallförfattare<br /> </td>
   <td>läsa, skriva, replikera</td>
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i platsspecifika <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>read</td>
   <td>En anonym webbanvändare måste läsa mallar när en sida återges</td>
  </tr>
  <tr>
   <td>Innehållsförfattare</td>
   <td>replikera</td>
   <td>replikateInnehållsförfattare måste aktivera sidans mallar när en sida aktiveras</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>läsa, skriva, replikera</td>
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i platsspecifika <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>read</td>
   <td>En anonym webbanvändare måste läsa principer när en sida återges</td>
  </tr>
  <tr>
   <td>Innehållsförfattare</td>
   <td>replikera</td>
   <td>Innehållsförfattare måste aktivera profilerna för en sidmall när de aktiverar en sida</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Mallförfattare</td>
   <td>read</td>
   <td>Mallförfattare skapar en ny mall baserad på en av de fördefinierade malltyperna.</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>ingen</td>
   <td>En anonym webbanvändare får inte komma åt malltyperna</td>
  </tr>
 </tbody>
</table>

Den här standardinställningen `template-authors` gruppen täcker endast projektinställningarna, där alla `template-authors` -medlemmar har åtkomst till och kan redigera alla mallar. För mer komplexa konfigurationer, där flera mallförfattargrupper behövs för att separera åtkomsten till mallar, måste fler anpassade mallskapargrupper skapas. Behörigheterna för mallförfattargrupperna är dock fortfarande desamma.

## Malltyp {#template-type}

När du skapar en ny mall måste du ange en malltyp:

* Malltyper tillhandahåller effektivt mallar för en mall. När du skapar en ny mall används strukturen och det ursprungliga innehållet för den valda malltypen för att skapa till den nya mallen.

   * Malltypen kopieras för att skapa mallen.
   * När kopian är klar är den enda kopplingen mellan mallen och malltypen en statisk referens i informationssyfte.

* Med malltyper kan du definiera:

   * Sidkomponentens resurstyp.
   * Rotnodens princip, som definierar vilka komponenter som tillåts i mallredigeraren.
   * Vi rekommenderar att du definierar brytpunkter för responsiva rutnät och inställningar för mobilemulatorn på malltypen.

* AEM innehåller ett litet urval av färdiga malltyper som HTML5 Page och Adaptive Form Page.

   * Ytterligare exempel finns som en del av [WKND, genomgång](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* Malltyper definieras vanligtvis av utvecklare.

Malltyperna som inte finns lagrade under:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Du får inte ändra något i `/libs` bana. Detta beror på innehållet i `/libs` kan skrivas över när som helst genom en uppdatering till AEM.

Platsspecifika malltyper bör lagras på samma plats som:

* `/apps/settings/wcm/template-types`

Definitioner för dina anpassade malltyper bör lagras i användardefinierade mappar (rekommenderas) eller alternativt i `global`. Till exempel:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Malltyperna måste ta hänsyn till rätt mappstruktur (d.v.s. `/settings/wcm/...`), annars går det inte att hitta malltyperna.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### Skapa malltyper {#creating-template-types}

Om du har skapat en mall som kan användas som bas för andra mallar kan du kopiera den här mallen som en malltyp.

1. Skapa en mall på samma sätt som vilken sidmall som helst [dokumenteras här](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), som kommer att fungera som bas för din malltyp.
1. Kopiera den nya mallen från CRXDE Lite `templates` nod till `template-types` noden under [mallmapp](#template-folders).
1. Ta bort mallen från `templates` noden under [mallmapp](#template-folders).
1. I kopian av mallen som finns under `template-types` nod, ta bort alla `cq:template` och `cq:templateType` egenskaper från alla `jcr:content` noder.

Du kan också utveckla en egen malltyp med en exempelredigerbar mall som bas, som finns på GitHub.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-sites-example-custom-template-type-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Malldefinitioner {#template-definitions}

Definitioner för redigerbara mallar sparas [användardefinierade mappar](#template-folders) (rekommenderas) eller `global`. Till exempel:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Mallens rotnod är av typen `cq:Template` med en skelettstruktur på

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Huvudelementen är:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:innehåll {#jcr-content}

Den här noden innehåller egenskaper för mallen:

* **Namn**: `jcr:title`
* **Namn**: `status`
   * &quot;**Typ**: `String`
   * **Värde**: `draft`, `enabled` eller `disabled`

### Struktur {#structure}

Definierar strukturen för den resulterande sidan:

* Sammanfogas med det ursprungliga innehållet ( `/initial`) när du skapar en ny sida.
* Ändringar som görs i strukturen återspeglas i alla sidor som skapas med mallen.
* The `root` ( `structure/jcr:content/root`)-noden definierar listan med komponenter som är tillgängliga på den resulterande sidan.
   * Komponenter som definieras i mallstrukturen kan inte flyttas eller tas bort från resultatsidor.
   * När en komponent har låsts upp `editable` egenskapen är inställd på `true`.
   * När en komponent som redan innehåller innehåll har låsts upp, flyttas det här innehållet till `initial` förgrening.

* The `cq:responsive` noden innehåller definitioner för den responsiva layouten.

### Ursprungligt innehåll {#initial-content}

Definierar det ursprungliga innehåll som en ny sida kommer att ha när den skapas:

* Innehåller en `jcr:content` nod som kopieras till nya sidor.
* Sammanfogas med strukturen ( `/structure`) när du skapar en ny sida.
* Befintliga sidor uppdateras inte om det ursprungliga innehållet ändras efter att de har skapats.
* The `root` noden innehåller en lista med komponenter som definierar vad som är tillgängligt på den resulterande sidan.
* Om innehåll läggs till i en komponent i strukturläge och den komponenten sedan låses upp (eller vice versa), används det här innehållet som ursprungligt innehåll.

### Layout {#layout}

När [redigera en mall kan du definiera layouten](/help/sites-cloud/authoring/features/templates.md)används [responsiv standardlayout](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Innehållsprofiler {#content-policies}

Innehållsprinciperna definierar designegenskaperna för en komponent. Till exempel de tillgängliga komponenterna eller minimi-/maximidimensionerna. Dessa gäller för mallen (och sidor som skapas med mallen). Du kan skapa och välja innehållsprinciper i mallredigeraren.

* Egenskapen `cq:policy`, på `root` nod
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Ger en relativ referens till innehållsprincipen för sidans styckesystem.

* Egenskapen `cq:policy`, på de komponentspecifika noderna under `root`, innehåller länkar till profilerna för de enskilda komponenterna.

* De faktiska principdefinitionerna lagras under:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Sökvägarna för principdefinitioner beror på komponentens sökväg. `cq:policy` innehåller en relativ referens till själva konfigurationen.

### Sidprofiler {#page-policies}

Med sidprofiler kan du definiera [innehållsprincip](#content-policies) för sidan (huvudparametrar), antingen i mallen eller på de resulterande sidorna.

### Aktivera och tillåta en mall för användning {#enabling-and-allowing-a-template-for-use}

1. **Aktivera mallen**

   Innan en mall kan användas måste den aktiveras av något av följande:

   * [Aktivera mallen](/help/sites-cloud/authoring/features/templates.md) från **Mallar** konsol.

   * Ställa in egenskapen status på `jcr:content` nod.

      * På:
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definiera egenskapen:

         * Namn: status
         * Typ: Sträng
         * Värde: `enabled`

1. **Tillåtna mallar**

   * [Definiera tillåtna mallsökvägar på **Sidegenskaper**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) av rätt sida eller rotsida i en underavdelning.
   * Ange egenskapen:
     `cq:allowedTemplates`
På `jcr:content` noden för den begärda grenen.

   Med till exempel värdet:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Gällande innehållssidor {#resultant-content-pages}

Sidor skapade från redigerbara mallar:

* Skapas med ett underträd som sammanfogas från `structure` och `initial` i mallen

* Har referenser till information som finns i mallen och malltypen. Detta uppnås med en `jcr:content` nod med egenskaperna:

   * `cq:template` - innehåller en dynamisk referens till den faktiska mallen, gör att ändringar i mallen kan återspeglas på de faktiska sidorna.

   * `cq:templateType` - Tillhandahåller en referens till malltypen.

![Hur mallar, innehåll och komponenter samverkar](assets/templates-content-components.png)

Diagrammet ovan visar hur mallar, innehåll och komponenter samverkar:

* Styrenhet - `/content/<my-site>/<my-page>` - Den resulterande sidan som refererar till mallen. Innehållet styr hela processen. Enligt definitionerna har den åtkomst till rätt mall och komponenter.
* Konfiguration - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [mallar och relaterade innehållsprinciper](#template-definitions) definiera sidkonfigurationen.
* Model - OSGi bundles - The [OSGI-paket](/help/implementing/deploying/configuring-osgi.md) implementera funktionen.
* Visa - `/apps/<my-site>/components` - I både författar- och publiceringsmiljöer återges innehållet av komponenter.

Vid återgivning av en sida:

* **Mallar**:

   * The `cq:template` egenskap för dess `jcr:content` noden refereras till för att komma åt mallen som motsvarar den sidan.

* **Komponenter**:

   * Sidkomponenten kommer att sammanfoga `structure/jcr:content` mallens träd med `jcr:content` sidans träd.
      * Sidkomponenten tillåter bara författaren att redigera noderna i mallstrukturen som har flaggats som redigerbara (och eventuella underordnade noder).
      * När en komponent återges på en sida hämtas den relativa sökvägen från `jcr:content` nod; samma bana under `policies/jcr:content` -noden i mallen söks sedan igenom.
         * The `cq:policy` den här nodens egenskap pekar på den faktiska innehållsprincipen (d.v.s. den innehåller komponentens designkonfiguration).
            * På så sätt kan du ha flera mallar som återanvänder samma innehållsprincipkonfigurationer.

### Malltillgänglighet {#template-availability}

När du skapar en ny sida i webbplatsens administratörsgränssnitt beror listan med tillgängliga mallar på platsen för den nya sidan och de placeringsbegränsningar som anges i varje mall.

Följande egenskaper avgör om en mall `T` får användas för en ny sida som ska placeras som underordnad till sidan `P`. Var och en av dessa egenskaper är en sträng med flera värden som innehåller noll eller flera reguljära uttryck som används för matchning med sökvägar:

* The `cq:allowedTemplates` egenskapen för `jcr:content` undernod till `P` eller en överordnad till `P`.

* The `allowedPaths` egenskap för `T`.

* The `allowedParents` egenskap för `T`.

* The `allowedChildren` egenskap för mallen för `P`.

Utvärderingen fungerar enligt följande:

* Den första som inte är tom `cq:allowedTemplates` egenskap påträffades när sidhierarkin skulle ökas från `P` matchas mot sökvägen för `T`. Om inget av värdena matchar, `T` avvisas.

* If `T` har ett värde som inte är tomt `allowedPaths` -egenskapen, men inget av värdena matchar sökvägen för `P`, `T` avvisas.

* Om båda ovanstående egenskaper är tomma eller inte finns, `T` avvisas om det inte tillhör samma program som `P`. `T` tillhör samma program som `P` om och bara om namnet på den andra nivån i sökvägen för `T` är samma som namnet på den andra nivån i sökvägen för `P`. Mallen `/apps/wknd/templates/foo` tillhör samma program som sidan `/content/wknd`.

* If `T` har ett värde som inte är tomt `allowedParents` -egenskapen, men inget av värdena matchar sökvägen för `P`, `T` avvisas.

* Om mallen för `P` har ett värde som inte är tomt `allowedChildren` -egenskapen, men inget av värdena matchar sökvägen för `T`, `T` avvisas.

* I alla andra fall `T` är tillåtet.

I följande diagram visas mallutvärderingsprocessen:

![Mallutvärderingsprocess](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM har flera egenskaper som styr mallarna under **Webbplatser**. En kombination av dem kan dock leda till mycket komplexa regler som är svåra att spåra och hantera.
>
>Därför rekommenderar Adobe att du börjar enkelt genom att definiera:
>
>* endast `cq:allowedTemplates` property
>
>* endast i platsroten
>
>Se till exempel [WKND, genomgång](/help/implementing/developing/introduction/develop-wknd-tutorial.md) innehåll: `/content/wknd/jcr:content`
>
>Egenskaperna `allowedPaths`, `allowedParents`och `allowedChildren` kan också placeras i mallar för att definiera mer avancerade regler. Men när det är möjligt är det *mycket* enklare att definiera `cq:allowedTemplates` egenskaper för underavsnitt av webbplatsen om det finns behov av att ytterligare begränsa de tillåtna mallarna.
>
>Ytterligare en fördel är att `cq:allowedTemplates` kan uppdateras av en författare i **Avancerat** -fliken i **Sidegenskaper**. De andra mallegenskaperna kan inte uppdateras med (standard) användargränssnittet, så behöver en utvecklare för att behålla reglerna och en koddistribution för varje ändring.

#### Begränsa mallar som används på underordnade sidor {#limiting-templates-used-in-child-pages}

Om du vill begränsa vilka mallar som kan användas för att skapa underordnade sidor under en viss sida använder du `cq:allowedTemplates` egenskap för `jcr:content` nod på sidan för att ange listan med mallar som ska tillåtas som underordnade sidor. Varje värde i listan måste vara en absolut sökväg till en mall för en tillåten underordnad sida, till exempel `/apps/wknd/templates/page-content`.

Du kan använda `cq:allowedTemplates` -egenskap i mallens  `jcr:content` nod som den här konfigurationen ska tillämpas på alla nyskapade sidor som använder den här mallen.

Om du vill lägga till fler begränsningar, till exempel för mallhierarkin, kan du använda `allowedParents/allowedChildren` -egenskaper i mallen. Du kan sedan uttryckligen ange att sidor som skapats från en mall T måste vara överordnade/underordnade sidor till sidor som skapats från en mall T.
