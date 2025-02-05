---
title: Redigerbara mallar
description: Lär dig hur redigerbara mallar används när du skapar en sida, definierar dess ursprungliga innehåll, strukturerat innehåll, redigeringsprinciper och layout.
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 0%

---

# Redigerbara mallar {#editable-templates}

Lär dig hur redigerbara mallar används när du skapar en sida, definierar dess ursprungliga innehåll, strukturerat innehåll, redigeringsprinciper och layout.

## Ökning {#overview}

När du skapar en sida måste du välja en mall. Sidmallen används som bas för den nya sidan. Mallen kan definiera strukturen för den resulterande sidan, allt ursprungligt innehåll och de komponenter som kan användas (designegenskaper).

* Redigerbara mallar gör att författare kan skapa och använda mallar.
* Redigerbara mallar kan användas för att skapa sidor som är redigerbara med båda
   * [Sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md) och
   * [Universal Editor](/help/sites-cloud/authoring/universal-editor/templates.md)

Sidmallar som används för att skapa sidor som kan redigeras med den universella redigeraren använder en begränsad delmängd av de redigerbara mallfunktionerna. Därför är resten av det här dokumentet fokuserat på redigerbara mallar som används för att skapa sidor som är redigerbara med sidredigeraren.

## Redigerbara mallar och sidor som har redigerats med sidredigeraren {#page-editor}

När du skapar mallar för att skapa sidor som är redigerbara med sidredigeraren identifieras vanligtvis specialiserade författare.

* Sådana specialiserade författare kallas **mallskapare**
* Mallförfattare måste vara medlemmar i gruppen `template-authors`.
* Redigerbara mallar behåller en dynamisk anslutning till alla sidor som skapas från dem. Detta säkerställer att alla ändringar i mallen återspeglas på själva sidorna.
* Redigerbara mallar gör sidkomponenten mer generisk så att kärnsideskomponenten kan användas utan anpassning.

Med redigerbara mallar isoleras de delar som utgör en sida inuti komponenterna. Du kan konfigurera nödvändiga kombinationer av komponenter i ett användargränssnitt, vilket eliminerar behovet av att utveckla en ny sidkomponent för varje sidvariant.

Det här dokumentet:

* Ger en översikt över hur du skapar en redigerbar mall
* Beskriver de admin-/utvecklaråtgärder som krävs för att skapa redigerbara mallar
* Beskriver de tekniska grunderna för redigerbara mallar
* Beskriver hur AEM utvärderar en malls tillgänglighet

>[!NOTE]
>
>Det här dokumentet förutsätter att du redan är bekant med att skapa och redigera mallar. Se redigeringsdokumentet [Mallar för att skapa sidor som är redigerbara med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md), som innehåller information om funktionerna i redigerbara mallar så som de visas för mallskaparen.

>[!TIP]
>
>[WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md) handlar om hur du använder redigerbara mallar genom att implementera ett exempel och är mycket användbar för att förstå hur du konfigurerar en mall i ett nytt projekt

## Skapa en ny redigerbar mall {#creating-a-new-template}

Skapandet av redigerbara mallar görs huvudsakligen med [mallkonsolen och mallredigeraren](/help/sites-cloud/authoring/page-editor/templates.md) av en mallskapare. I det här avsnittet ges en översikt över processen och en beskrivning av vad som händer på teknisk nivå.

När du skapar en redigerbar mall:

1. Skapa en [mapp för mallarna](#template-folders). Detta är inte obligatoriskt, men vi rekommenderar bästa praxis.
1. Välj en [malltyp](#template-type). Detta kopieras för att skapa [malldefinitionen](#template-definitions).

   >[!NOTE]
   >
   >Du kan välja mellan olika malltyper direkt. Du kan även [skapa egna webbplatsspecifika malltyper](#creating-template-types) om det behövs.

1. Konfigurera den nya mallens struktur, innehållsprinciper, ursprungliga innehåll och layout.

   **Struktur**

   * Strukturen gör att du kan definiera komponenter och innehåll för mallen.
   * Komponenter som definieras i mallstrukturen kan inte flyttas till en resultatsida eller tas bort från eventuella resultatsidor.
   * Om du vill att sidförfattare ska kunna lägga till och ta bort komponenter lägger du till ett styckesystem i mallen.
   * Komponenter kan låsas upp och låsas igen så att du kan definiera ursprungligt innehåll.

   Mer information om hur en mallskapare definierar strukturen finns i [Mallar för att skapa sidor som är redigerbara med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author).

   Mer teknisk information om strukturen finns i [Struktur](#structure) i det här dokumentet.

   **Profiler**

   * Innehållsprinciperna definierar designegenskaperna för en komponent.

      * Till exempel de tillgängliga komponenterna eller minimi-/maximidimensionerna.

   * Dessa gäller för mallen (och sidor som skapas med mallen).

   Mer information om hur en mallskapare definierar profiler finns i [Mallar för att skapa sidor som är redigerbara med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author).

   Teknisk information om profiler finns i [Innehållsprinciper](#content-policies) i det här dokumentet.

   **Inledande innehåll**

   * Ursprungligt innehåll definierar innehåll som visas när en sida skapas baserat på mallen.
   * Det initiala innehållet kan sedan redigeras av sidförfattare.

   Mer information om hur en mallskapare definierar strukturen finns i [Mallar för att skapa sidor som är redigerbara med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-initial-content-author).

   Teknisk information om ursprungligt innehåll finns i [Inledande innehåll](#initial-content) i det här dokumentet.

   **Layout**

   * Du kan definiera mallayouten för ett antal olika enheter.
   * Responsiv layout för mallar fungerar på samma sätt som för sidredigering.

   Mer information om hur en mallskapare definierar mallayouten finns i [Mallar för att skapa sidor som kan redigeras med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-layout-template-author).

   Mer teknisk information om mallayout finns i [Layout](#layout) i det här dokumentet.

1. Aktivera mallen och tillåt den sedan för specifika innehållsträd.

   * En mall kan aktiveras eller inaktiveras för att göra den tillgänglig eller inte tillgänglig för sidförfattare.
   * En mall kan göras tillgänglig eller otillgänglig för vissa sidgrenar.

   Mer information om hur en mallskapare aktiverar en mall finns i [Mallar för att skapa sidor som kan redigeras med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author).

   Mer teknisk information om hur du aktiverar en mall finns i [Aktivera och tillåta en mall för användare](#enabling-and-allowing-a-template-for-use)e i det här dokumentet

1. Använd det för att skapa innehållssidor.

   * När du använder en mall för att skapa en sida finns det ingen synlig skillnad och ingen indikation mellan statiska och redigerbara mallar.
   * För sidförfattaren är processen genomskinlig.

   Mer information om hur en sidförfattare använder mallar för att skapa en sida finns i [Skapa och ordna sidor](/help/sites-cloud/authoring/sites-console/organizing-pages.md#templates).

   Mer teknisk information om hur du skapar sidor med redigerbara mallar finns i [Gällande innehållssidor](#resultant-content-pages) i det här dokumentet.

>[!TIP]
>
>Ange aldrig någon information som måste internationaliseras i en mall. För internalisering rekommenderas [lokaliseringsfunktionerna för kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html).

>[!NOTE]
>
>Mallar är kraftfulla verktyg som effektiviserar arbetsflödet för att skapa sidor. Alltför många mallar kan överbelasta författarna och göra det förvirrande att skapa sidor. En bra tumregel är att hålla antalet mallar under 100.
>
>Adobe rekommenderar inte att ha fler än 1 000 mallar på grund av potentiella prestandaeffekter.

>[!NOTE]
>
>Redigeringsklientbiblioteket förutsätter att namnområdet `cq.shared` finns på innehållssidorna och om det saknas kommer JavaScript-felet `Uncaught TypeError: Cannot read property 'shared' of undefined` att uppstå.
>
>Alla exempelinnehållssidor innehåller `cq.shared`, så allt innehåll som baseras på dem inkluderar automatiskt `cq.shared`. Om du vill skapa egna innehållssidor från grunden utan att basera dem på exempelinnehåll måste du se till att inkludera namnutrymmet `cq.shared`.
>
>Mer information finns i [Använda bibliotek på klientsidan](/help/implementing/developing/introduction/clientlibs.md).

## Mallmappar {#template-folders}

Du kan använda följande mappar för att ordna dina mallar:

* `global`
* Webbplatsspecifik

>[!NOTE]
>
>Även om du kan kapsla dina mappar visas de som en platt struktur när användaren visar dem i konsolen **Mallar**.

I en AEM finns mappen `global` redan i mallkonsolen. Detta innehåller standardmallar och fungerar som reserv om inga principer och/eller malltyper hittas i den aktuella mappen. Du kan lägga till dina standardmallar i den här mappen eller skapa en mapp (rekommenderas).

>[!NOTE]
>
>Det är en god vana att skapa en mapp för dina anpassade mallar och inte använda mappen `global`.

>[!CAUTION]
>
>Mappar måste skapas av en användare med `admin` rättigheter.

Malltyper och profiler ärvs i alla mappar enligt följande prioritetsordning:

1. Aktuell mapp
1. Överordnad(e) till aktuell mapp
1. `/conf/global`
1. `/apps`
1. `/libs`

En lista över alla tillåtna poster skapas. Om några konfigurationer överlappar ( `path`/ `label`) visas endast den instans som ligger närmast den aktuella mappen för användaren.

Om du vill skapa en mapp kan du göra det här:

* Programmerat eller med CRXDE Lite
* Använda [Configuration Browser](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

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
   * Värde: Den rubrik (för mappen) som du vill ska visas i konsolen **Mallar**.

1. Förutom de vanliga redigeringsbehörigheterna och behörigheterna (till exempel `content-authors`) måste du nu tilldela grupper och definiera de åtkomstbehörigheter som krävs för att författarna ska kunna skapa mallar i den nya mappen.

   Gruppen `template-authors` är standardgruppen som måste tilldelas. Mer information finns i avsnittet [ACL:er och grupper](#acls-and-groups).

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Använda Konfigurationsläsaren {#using-the-configuration-browser}

1. Gå till **Global navigering** > **Verktyg** > [**Konfigurationsläsaren**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   De befintliga mapparna visas till vänster inklusive mappen `global`.

1. Klicka på **Skapa**.
1. I dialogrutan **Skapa konfiguration** måste följande fält konfigureras:

   * **Titel**: Ange en rubrik för konfigurationsmappen
   * **Redigerbara mallar**: Markera för att tillåta redigerbara mallar i den här mappen

1. Klicka på **Skapa**

>[!NOTE]
>
>I [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) kan du redigera den globala mappen och aktivera alternativet **Redigerbara mallar** om du vill skapa mallar i den här mappen, men detta är inte den bästa metoden.

### Behörighetslistor och grupper {#acls-and-groups}

När mallmapparna har skapats (antingen via CRXDE eller med Configuration Browser) måste åtkomstkontrollistor definieras för rätt grupper för mallmapparna för att säkerställa rätt säkerhet.

Mallmapparna för [WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md) kan användas som exempel.

#### Mallförfattargruppen {#the-template-authors-group}

Gruppen `template-authors` är den grupp som används för att hantera åtkomst till mallar och levereras som standard med AEM, men är tom. Användare måste läggas till i gruppen för projektet/webbplatsen.

>[!CAUTION]
>
>Gruppen `template-authors` är bara avsedd för användare som måste kunna skapa nya mallar.
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
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i det platsspecifika <code>/conf</code>-området</td>
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
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i det platsspecifika <code>/conf</code>-området</td>
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

Den här standardgruppen `template-authors` täcker bara projektinställningarna, där alla `template-authors`-medlemmar har åtkomst till och kan redigera alla mallar. För mer komplexa konfigurationer, där flera mallförfattargrupper behövs för att separera åtkomsten till mallar, måste fler anpassade mallskapargrupper skapas. Behörigheterna för mallförfattargrupperna är dock fortfarande desamma.

## Malltyp {#template-type}

När du skapar en mall måste du ange en malltyp:

* Malltyper tillhandahåller effektivt mallar för en mall. När du skapar en mall används strukturen och det ursprungliga innehållet för den valda malltypen för att skapa till den nya mallen.

   * Malltypen kopieras för att skapa mallen.
   * När kopian är klar är den enda kopplingen mellan mallen och malltypen en statisk referens i informationssyfte.

* Med malltyper kan du definiera:

   * Sidkomponentens resurstyp.
   * Rotnodens princip, som definierar vilka komponenter som tillåts i mallredigeraren.
   * Vi rekommenderar att du definierar brytpunkter för responsiva rutnät och inställningar för mobilemulatorn på malltypen.

* AEM innehåller ett litet urval av färdiga malltyper som HTML5 Page och Adaptive Form Page.

   * Ytterligare exempel finns som en del av [WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* Malltyper definieras vanligtvis av utvecklare.

Malltyperna som inte finns lagrade under:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Du får inte ändra något i sökvägen `/libs`. Detta beror på att innehållet i `/libs` kan skrivas över när som helst genom en uppdatering till AEM.

Platsspecifika malltyper bör lagras på samma plats som:

* `/apps/settings/wcm/template-types`

Definitioner för dina anpassade malltyper ska lagras i användardefinierade mappar (rekommenderas) eller i `global`. Till exempel:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Malltyperna måste respektera rätt mappstruktur (d.v.s. `/settings/wcm/...`), annars hittas inte malltyperna.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating an editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

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

1. Skapa en mall precis som vilken sidmall som helst. Se [Mallar för att skapa sidor som kan redigeras med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md#creating-a-new-template-template-author). Detta fungerar som bas för malltypen.
1. Kopiera med CRXDE Lite den skapade mallen från noden `templates` till noden `template-types` under [mallmappen](#template-folders).
1. Ta bort mallen från noden `templates` under [mallmappen](#template-folders).
1. I kopian av mallen som finns under noden `template-types` tar du bort alla `cq:template` - och `cq:templateType` -egenskaper från alla `jcr:content` -noder.

Du kan också utveckla en egen malltyp med en exempelredigerbar mall som bas, som finns på GitHub.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-sites-example-custom-template-type-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Malldefinitioner {#template-definitions}

Definitioner för redigerbara mallar lagras i [användardefinierade mappar](#template-folders) (rekommenderas) eller i `global`. Till exempel:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Rotnoden för mallen är av typen `cq:Template` med en skelettstruktur på:

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

* Sammanfogas med det ursprungliga innehållet ( `/initial`) när en sida skapas.
* Ändringar som görs i strukturen återspeglas i alla sidor som skapas med mallen.
* Noden `root` ( `structure/jcr:content/root`) definierar listan över komponenter som är tillgängliga på den resulterande sidan.
   * Komponenter som definieras i mallstrukturen kan inte flyttas eller tas bort från resultatsidor.
   * När en komponent har låsts upp är egenskapen `editable` inställd på `true`.
   * När en komponent som redan innehåller innehåll har låsts upp, flyttas det här innehållet till grenen `initial`.

* Noden `cq:responsive` innehåller definitioner för den responsiva layouten.

### Ursprungligt innehåll {#initial-content}

Definierar det ursprungliga innehåll som en ny sida kommer att ha när den skapas:

* Innehåller en `jcr:content`-nod som kopieras till nya sidor.
* Sammanfogas med strukturen ( `/structure`) när du skapar en sida.
* Befintliga sidor uppdateras inte om det ursprungliga innehållet ändras efter att de har skapats.
* Noden `root` innehåller en lista med komponenter som definierar vad som är tillgängligt på den resulterande sidan.
* Om innehåll läggs till i en komponent i strukturläge och komponenten sedan låses upp (eller omvänt), används det här innehållet som ursprungligt innehåll.

### Layout {#layout}

När du [redigerar en mall kan du definiera layouten](/help/sites-cloud/authoring/page-editor/templates.md), använder detta [den responsiva standardlayouten](/help/sites-cloud/administering/responsive-layout.md) som kan [konfigureras på sidan av innehållsförfattaren](/help/sites-cloud/authoring/page-editor/responsive-layout.md).

### Innehållsprinciper {#content-policies}

Innehållsprinciperna definierar designegenskaperna för en komponent. Till exempel de tillgängliga komponenterna eller minimi-/maximidimensionerna. Dessa gäller för mallen (och sidor som skapas med mallen). Du kan skapa och välja innehållsprinciper i mallredigeraren.

* Egenskapen `cq:policy` på noden `root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Ger en relativ referens till innehållsprincipen för sidans styckesystem.

* Egenskapen `cq:policy`, på de komponentspecifika noderna under `root`, innehåller länkar till principerna för de enskilda komponenterna.

* De faktiska principdefinitionerna lagras under:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Sökvägarna för principdefinitioner beror på komponentens sökväg. `cq:policy` innehåller en relativ referens till själva konfigurationen.

### Sidprofiler {#page-policies}

Med sidprofiler kan du definiera sidans [innehållsprincip](#content-policies) (huvudparsys), antingen i mallen eller på de resulterande sidorna.

### Aktivera och tillåta en mall för användning {#enabling-and-allowing-a-template-for-use}

1. **Aktivera mallen**

   Innan en mall kan användas måste den aktiveras av något av följande:

   * [Aktivera mallen](/help/sites-cloud/authoring/page-editor/templates.md) från konsolen **Mallar**.

   * Anger egenskapen status för noden `jcr:content`.

      * På:
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definiera egenskapen:

         * Namn: status
         * Typ: String
         * Värde: `enabled`

1. **Tillåtna mallar**

   * [Definiera tillåtna mallsökvägar på **Sidegenskaper**](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) för rätt sida eller rotsida i en underavdelning.
   * Ange egenskapen:
     `cq:allowedTemplates`
På noden `jcr:content` för den begärda grenen.

   Med värdet:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Gällande innehållssidor {#resultant-content-pages}

Sidor skapade från redigerbara mallar:

* Skapas med ett underträd som sammanfogas från `structure` och `initial` i mallen

* Har referenser till information som finns i mallen och malltypen. Detta uppnås med en `jcr:content`-nod med egenskaperna:

   * `cq:template` - Tillhandahåller den dynamiska referensen till den faktiska mallen; aktiverar ändringar i mallen som ska återspeglas på de faktiska sidorna.

   * `cq:templateType` - Tillhandahåller en referens till malltypen.

![Hur mallar, innehåll och komponenter relaterar ](assets/templates-content-components.png)

Diagrammet ovan visar hur mallar, innehåll och komponenter samverkar:

* Styrenhet - `/content/<my-site>/<my-page>` - Den resulterande sidan som refererar till mallen. Innehållet styr hela processen. Enligt definitionerna har den åtkomst till rätt mall och komponenter.
* Konfiguration - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [mallen och relaterade innehållsprinciper](#template-definitions) definierar sidkonfigurationen.
* Modell - OSGi-paket - [OSGI-paket](/help/implementing/deploying/configuring-osgi.md) implementerar funktionen.
* Visa - `/apps/<my-site>/components` - I både författar- och publiceringsmiljöer återges innehållet av komponenter.

När en sida återges:

* **Mallar**:

   * Egenskapen `cq:template` för noden `jcr:content` refereras till för att komma åt mallen som motsvarar den sidan.

* **Komponenter**:

   * Sidkomponenten sammanfogar mallens `structure/jcr:content`-träd med sidans `jcr:content`-träd.
      * Sidkomponenten tillåter bara författaren att redigera noderna i mallstrukturen som har flaggats som redigerbara (och eventuella underordnade noder).
      * När du återger en komponent på en sida hämtas komponentens relativa sökväg från noden `jcr:content`. Samma sökväg under noden `policies/jcr:content` i mallen söks sedan igenom.
         * Egenskapen `cq:policy` för den här noden pekar på den faktiska innehållsprincipen (d.v.s. den innehåller designkonfigurationen för den komponenten).
            * På så sätt kan du ha flera mallar som återanvänder samma innehållsprincipkonfigurationer.

### Malltillgänglighet {#template-availability}

När du skapar en sida i webbplatsens administratörsgränssnitt beror listan med tillgängliga mallar på platsen för den nya sidan och de placeringsbegränsningar som anges i varje mall.

Följande egenskaper avgör om mallen `T` får användas för en ny sida som ska placeras som underordnad till sidan `P`. Var och en av dessa egenskaper är en sträng med flera värden som innehåller noll eller flera reguljära uttryck som används för matchning med sökvägar:

* Egenskapen `cq:allowedTemplates` för `jcr:content`-undernoden till `P` eller en överordnad till `P`.

* Egenskapen `allowedPaths` för `T`.

* Egenskapen `allowedParents` för `T`.

* Egenskapen `allowedChildren` för mallen för `P`.

Utvärderingen fungerar enligt följande:

* Den första icke-tomma `cq:allowedTemplates`-egenskapen som påträffades när sidhierarkin som börjar med `P` överskreds matchas mot sökvägen för `T`. Om inget av värdena matchar avvisas `T`.

* Om `T` har en `allowedPaths`-egenskap som inte är tom, men inget av värdena matchar sökvägen för `P`, avvisas `T`.

* Om båda ovanstående egenskaper är tomma eller inte finns, avvisas `T` om den inte tillhör samma program som `P`. `T` tillhör samma program som `P` om och bara om namnet på den andra nivån i sökvägen `T` är detsamma som namnet på den andra nivån i sökvägen `P`. Mallen `/apps/wknd/templates/foo` tillhör till exempel samma program som sidan `/content/wknd`.

* Om `T` har en `allowedParents`-egenskap som inte är tom, men inget av värdena matchar sökvägen för `P`, avvisas `T`.

* Om mallen för `P` har en `allowedChildren`-egenskap som inte är tom, men inget av värdena matchar sökvägen för `T`, avvisas `T`.

* I alla andra fall tillåts `T`.

I följande diagram visas mallutvärderingsprocessen:

![Mallutvärderingsprocess](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM erbjuder flera egenskaper för att styra mallarna som tillåts under **Platser**. En kombination av dem kan dock leda till mycket komplexa regler som är svåra att spåra och hantera.
>
>Därför rekommenderar Adobe att du börjar enkelt genom att definiera:
>
>* endast egenskapen `cq:allowedTemplates`
>
>* endast i platsroten
>
>Se till exempel [WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md): `/content/wknd/jcr:content`
>
>Egenskaperna `allowedPaths`, `allowedParents` och `allowedChildren` kan också placeras i mallarna för att definiera mer avancerade regler. Om det är möjligt är det *mycket* enklare att definiera ytterligare `cq:allowedTemplates` egenskaper för underavsnitt på webbplatsen om det finns behov av att begränsa de tillåtna mallarna ytterligare.
>
>En ytterligare fördel är att `cq:allowedTemplates`-egenskaperna kan uppdateras av en författare på fliken **Avancerat** i **Sidegenskaper**. De andra mallegenskaperna kan inte uppdateras med (standard) användargränssnittet, så behöver en utvecklare för att behålla reglerna och en koddistribution för varje ändring.

#### Begränsa mallar som används på underordnade sidor {#limiting-templates-used-in-child-pages}

Om du vill begränsa vilka mallar som kan användas för att skapa underordnade sidor under en viss sida använder du egenskapen `cq:allowedTemplates` för noden `jcr:content` för att ange listan med mallar som ska tillåtas som underordnade sidor. Varje värde i listan måste vara en absolut sökväg till en mall för en tillåten underordnad sida, till exempel `/apps/wknd/templates/page-content`.

Du kan använda egenskapen `cq:allowedTemplates` på mallens `jcr:content`-nod om du vill att den här konfigurationen ska tillämpas på alla skapade sidor som använder mallen.

Om du vill lägga till fler begränsningar, till exempel för mallhierarkin, kan du använda egenskaperna `allowedParents/allowedChildren` i mallen. Du kan sedan uttryckligen ange att sidor som skapats från en mall T måste vara överordnade/underordnade sidor till sidor som skapats från en mall T.
