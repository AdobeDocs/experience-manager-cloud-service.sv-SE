---
title: Använda bibliotek på klientsidan på AEM as a Cloud Service
description: AEM innehåller biblioteksmappar på klientsidan, som gör att du kan lagra klientsidans kod (klientlibs) i databasen, ordna den i kategorier och definiera när och hur varje kodkategori ska skickas till klienten
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2562'
ht-degree: 0%

---


# Använda bibliotek på klientsidan på AEM as a Cloud Service {#using-client-side-libraries}

Digitala upplevelser är till stor del beroende av bearbetning på klientsidan som styrs av komplex JavaScript- och CSS-kod. Med AEM-bibliotek (klientbibliotek) kan du ordna och centralt lagra dessa klientbibliotek i databasen. Kopplad med [front end build process in the AEM Project Archetype,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) det blir enkelt att hantera koden för ditt AEM.

Fördelarna med att använda klienter i AEM är bland annat:

* Kod på klientsidan lagras i databasen precis som all annan programkod och annat innehåll
* Med Clientlibs in AEM kan du samla all CSS och JS i en enda fil
* Visa klienten via en bana som är tillgänglig via [avsändare](/help/implementing/dispatcher/disp-overview.md)
* Tillåter omskrivning av sökvägar för refererade filer eller bilder

Clientlibs är den inbyggda lösningen för att leverera CSS och Javascript från AEM.

>[!TIP]
>
>Utvecklare som skapar CSS och Javascript för AEM bör också bekanta sig med [AEM Project Archetype och dess automatiserade front-end-byggprocess.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## Vad är bibliotek på klientsidan? {#what-are-clientlibs}

Webbplatser kräver JavaScript och CSS samt statiska resurser som ikoner och webbteckensnitt för att kunna bearbetas på klientsidan. En klientlib är AEM som refererar (efter kategori om det behövs) och betjänar sådana resurser.

AEM samlar in webbplatsens CSS och Javascript till en enda fil, på en central plats, för att säkerställa att endast en kopia av en resurs inkluderas i utdata från HTML. Detta maximerar effektiviteten vid leverans och gör att sådana resurser kan underhållas centralt i databasen via proxy, vilket skyddar åtkomsten.

## Front-End Development för AEM as a Cloud Service {#fed-for-aemaacs}

Alla JavaScript-, CSS- och andra front end-resurser ska bevaras i [ui.front-modulen i AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) Tack vare den flexibla arkitekturen kan du använda dina moderna webbverktyg för att skapa och hantera dessa resurser.

Arketypen kan sedan kompilera resurserna till en enda CSS- och JS-fil och bädda in dem automatiskt i en `cq:clientLibraryFolder` i databasen.

## Mappstruktur för klientbibliotek {#clientlib-folders}

En biblioteksmapp på klientsidan är en databasnod av typen `cq:ClientLibraryFolder`. Dess definition i [CND-notation](https://jackrabbit.apache.org/node-type-notation.html) är

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` kan placeras var som helst i `/apps` underträd till databasen.
* Använd `categories` för noden för att identifiera de bibliotekskategorier som den tillhör.

Varje `cq:ClientLibraryFolder` innehåller en uppsättning JS- och/eller CSS-filer, tillsammans med några stödfiler (se nedan). Viktiga egenskaper för `cq:ClientLibraryFolder` är konfigurerade enligt följande:

* `allowProxy`: Eftersom alla klientlibs måste lagras under `apps`, tillåter den här egenskapen åtkomst till klientbibliotek via proxyservrar. Se avsnittet [Hitta en klientbiblioteksmapp och använda servern för proxyklientbibliotek](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) nedan.
* `categories`: Identifierar de kategorier i vilka uppsättningen JS- och/eller CSS-filer i den här `cq:ClientLibraryFolder` höst. The `categories` eftersom en biblioteksmapp är flervärdesdel kan den ingå i mer än en kategori (se nedan hur detta kan vara användbart).

Om klientbiblioteksmappen innehåller en eller flera källfiler som sammanfogas till en enda JS- och/eller CSS-fil vid körning. Den genererade filens namn är nodnamnet med antingen `.js` eller `.css` filnamnstillägg. Biblioteksnoden med namnet `cq.jquery` resultat i den genererade filen med namnet `cq.jquery.js` eller `cq.jquery.css`.

Klientbiblioteksmappar innehåller följande objekt:

* JS- och/eller CSS-källfiler
* Statiska resurser som stöder CSS-format, t.ex. ikoner, webbteckensnitt osv.
* Ett `js.txt` fil och/eller en `css.txt` som identifierar de källfiler som ska sammanfogas i de genererade JS- och/eller CSS-filerna

![Clientlib-arkitektur](assets/clientlib-architecture.drawio.png)

## Skapa biblioteksmappar på klientsidan {#creating-clientlib-folders}

Klientbibliotek måste finnas under `/apps`. Den här regeln är nödvändig för att kunna isolera kod från innehåll och konfiguration på ett bättre sätt.

I ordning för klientbiblioteken under `/apps` För att vara tillgänglig används en proxyserver. Åtkomstkontrollistorna används fortfarande i klientbiblioteksmappen, men med den kan innehållet läsas via `/etc.clientlibs/` om `allowProxy` egenskapen är inställd på `true`.

1. Öppna CRXDE Lite i en webbläsare (`https://<host>:<port>/crx/de`).
1. Välj `/apps` mapp och klicka på **Skapa > Skapa nod**.
1. Ange ett namn för biblioteksmappen och i dialogrutan **Typ** välj lista `cq:ClientLibraryFolder`. Klicka **OK** och sedan klicka **Spara alla**.
1. Om du vill ange den eller de kategorier som biblioteket tillhör väljer du `cq:ClientLibraryFolder` lägg till följande egenskap och klicka sedan på **Spara alla**:
   * Namn: `categories`
   * Typ: Sträng
   * Värde: Kategorinamnet
   * Flera: Markerad
1. För att klientbiblioteken ska vara tillgängliga via proxy under `/etc.clientlibs`väljer du `cq:ClientLibraryFolder` lägg till följande egenskap och klicka sedan på **Spara alla**:
   * Namn: `allowProxy`
   * Typ: Boolean
   * Värde: `true`
1. Om du behöver hantera statiska resurser skapar du en undermapp med namnet `resources` nedanför klientbiblioteksmappen.
   * Om du lagrar statiska resurser var som helst utom under mappen `resources`kan de inte refereras till i en publiceringsinstans.
1. Lägg till källfiler i biblioteksmappen.
   * Detta görs vanligtvis i den inledande byggprocessen för [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Du kan ordna källfiler i undermappar om du vill.
1. Markera klientbiblioteksmappen och klicka på **Skapa > Skapa fil**.
1. Skriv något av följande filnamn i rutan Filnamn och klicka på OK:
   * **`js.txt`:** Använd det här filnamnet för att generera en JavaScript-fil.
   * **`css.txt`:** Använd det här filnamnet för att generera en CSS (Cascading Style Sheet).
1. Öppna filen och skriv följande text för att identifiera källfilernas rot:
   * `#base=*[root]*`
   * Ersätt `[root]` med sökvägen till den mapp som innehåller källfilerna i förhållande till TXT-filen. Använd till exempel följande text när källfilerna finns i samma mapp som TXT-filen:
      * `#base=.`
   * Följande kod anger roten som mappen mobile under `cq:ClientLibraryFolder` nod:
      * `#base=mobile`
1. På raderna nedan `#base=[root]`anger du sökvägarna för källfilerna i förhållande till roten. Placera varje filnamn på en separat rad.
1. Klicka **Spara alla**.

## Serverar bibliotek på klientsidan {#serving-clientlibs}

När klientbiblioteksmappen är [konfigurerad efter behov,](#creating-clientlib-folders) dina klienter kan beställas via proxy. Exempel:

* Du har en klientlib i `/apps/myproject/clientlibs/foo`
* Du har en statisk bild i `/apps/myprojects/clientlibs/foo/resources/icon.png`

The `allowProxy` kan du begära:

* Klientlib via `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Den statiska bilden via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Läser in klientbibliotek via HTML {#loading-via-htl}

När dina klienter har lagrats och hanterats i klientbiblioteksmappen kan de nås via HTML.

Klientbibliotek läses in via en hjälpmall från AEM, som du kommer åt via `data-sly-use`. Hjälpmallar är tillgängliga i den här filen, som kan anropas via `data-sly-call`.

Varje hjälpmall förväntar sig en `categories` för att referera till önskade klientbibliotek. Det alternativet kan antingen vara en array med strängvärden eller en sträng som innehåller en kommaseparerad värdelista.

[Se dokumentationen för HTML](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) om du vill ha mer information om hur du läser in klientlibs via HTML.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Klientbibliotek på författare jämfört med Publicera {#clientlibs-author-publish}

De flesta klientlibs krävs i den AEM publiceringsinstansen. Det vill säga, de flesta kundens syften är att skapa en användarupplevelse av innehållet. För clientlibs on publish instances, [verktyg för framtagning](#fed-for-aemaacs) kan användas och distribueras via [klientbiblioteksmappar enligt beskrivningen ovan.](#creating-clientlib-folders)

Det finns dock tillfällen då klientbibliotek kan behövas för att anpassa redigeringsupplevelsen. Om du till exempel anpassar en dialogruta kan det krävas att du distribuerar små bitar av CSS eller JS till AEM.

### Hantera klientbibliotek på författare {#clientlibs-on-author}

Om du behöver använda klientbibliotek när du är författare kan du skapa dina klientbibliotek under `/apps` använda samma metoder som för publicering, men skriva direkt under `/apps/.../clientlibs/foo` i stället för att skapa ett helt projekt för att hantera det.

Du kan sedan&quot;koppla&quot; till JS:t för redigering genom att lägga till dina klientbibliotek i en körklar klientbibliotekskategori.

## Felsökningsverktyg {#debugging-tools}

AEM innehåller flera verktyg för felsökning och testning av klientbiblioteksmappar.

### Identifiera klientbibliotek {#discover-client-libraries}

The `/libs/cq/granite/components/dumplibs/dumplibs` genererar en sida med information om alla klientbiblioteksmappar i systemet. The `/libs/granite/ui/content/dumplibs` -noden har komponenten som en resurstyp. Om du vill öppna sidan använder du följande URL (ändra värd och port efter behov):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Informationen omfattar bibliotekets sökväg och typ (CSS eller JS) samt värdena för biblioteksattributen, t.ex. kategorier och beroenden. Efterföljande tabeller på sidan visar biblioteken i varje kategori och kanal.

### Se genererade utdata {#see-generated-output}

The `dumplibs` -komponenten innehåller en testväljare som visar den källkod som genereras för `ui:includeClientLib` -taggar. Sidan innehåller kod för olika kombinationer av js-, css- och temaattribut.

1. Använd någon av följande metoder för att öppna sidan Testa utdata:
   * Från `dumplibs.html` klickar du på länken på sidan **Klicka här för utdatatestning** text.
   * Öppna följande URL i webbläsaren (använd en annan värd och port efter behov):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * Standardsidan visar utdata för taggar utan värde för attributet categories.
1. Om du vill visa utdata för en kategori anger du värdet för klientbibliotekets `categories` egenskap och klicka på **Skicka fråga**.

## Ytterligare funktioner i klientbiblioteksmappen {#additional-features}

Det finns ett antal andra funktioner som stöds av klientbiblioteksmappar i AEM. Dessa är dock inte nödvändiga på AEM as a Cloud Service och därför bör de inte användas. De listas här för fullständighetens skull.

>[!WARNING]
>
>Dessa extrafunktioner i klientbiblioteksmappar behövs inte på AEM as a Cloud Service och därför bör de inte användas. De listas här för fullständighetens skull.

### Bibliotekshanteraren Adobe Granite HTML {#html-library-manager}

Ytterligare inställningar för klientbibliotek kan styras via **Bibliotekshanteraren Adobe Granite HTML** panelen System Console på `https://<host>:<port>/system/console/configMgr`).

### Ytterligare mappegenskaper {#additional-folder-properties}

Ytterligare mappegenskaper kan styra beroenden och inbäddningar, men behövs vanligtvis inte längre och användningen bör därför inte användas:

* `dependencies`: Det här är en lista över andra klientbibliotekskategorier som den här biblioteksmappen är beroende av. Anges till exempel två `cq:ClientLibraryFolder` noder `F` och `G`, om det finns en fil i `F` kräver en annan fil i `G` för att fungera som den ska `categories` av `G` ska vara bland `dependencies` av `F`.
* `embed`: Används för att bädda in kod från andra bibliotek. Om nod `F` bäddar in noder `G` och `H`blir HTML en sammanfogning av innehåll från noder `G` och `H`.

### Länka till beroenden {#linking-to-dependencies}

När koden i klientbiblioteksmappen refererar till andra bibliotek identifierar du de andra biblioteken som beroenden. The `ui:includeClientLib` -taggen som refererar till din klientbiblioteksmapp gör att HTML-koden innehåller en länk till den biblioteksfil som genereras samt beroenden.

Beroenden måste vara ett annat `cq:ClientLibraryFolder`. Om du vill identifiera beroenden lägger du till en egenskap i `cq:ClientLibraryFolder` nod med följande attribut:

* **Namn:** beroenden
* **Typ:** Sträng[]
* **Värden:** Värdet på egenskapen categories för den cq:ClientLibraryFolder-nod som den aktuella biblioteksmappen är beroende av.

Till exempel `/etc/clientlibs/myclientlibs/publicmain` är beroende av `cq.jquery` bibliotek. Sidan som refererar till huvudklientbiblioteket genererar HTML som innehåller följande kod:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Bädda in kod från andra bibliotek {#embedding-code-from-other-libraries}

Du kan bädda in kod från ett klientbibliotek i ett annat klientbibliotek. Vid körning innehåller de genererade JS- och CSS-filerna för inbäddningsbiblioteket koden för det inbäddade biblioteket.

Inbäddning av kod är användbart för att ge åtkomst till bibliotek som lagras i skyddade områden i databasen.

#### Appspecifika klientbiblioteksmappar {#app-specific-client-library-folders}

Det är en god vana att behålla alla programrelaterade filer i programmappen nedan `/apps`. Det är också en god vana att neka åtkomst för webbplatsbesökare till `/apps` mapp. Skapa en klientbiblioteksmapp under `/etc` mapp som bäddar in klientbiblioteket som finns under `/apps`.

Använd egenskapen categories för att identifiera klientbiblioteksmappen som ska bäddas in. Om du vill bädda in biblioteket lägger du till en egenskap i inbäddningen `cq:ClientLibraryFolder` nod, med följande egenskapsattribut:

* **Namn:** embed
* **Typ:** Sträng[]
* **Värde:** Värdet för egenskapen categories i `cq:ClientLibraryFolder` nod att bädda in.

#### Använda inbäddning för att minimera begäranden {#using-embedding-to-minimize-requests}

I vissa fall kan det finnas ett relativt stort antal HTML som har skapats för en vanlig sida av publiceringsinstansen `<script>` -element.

I sådana fall kan det vara användbart att kombinera all nödvändig klientbibliotekskod till en enda fil så att antalet fram- och tillbaka-begäranden vid sidinläsning minskar. För att göra detta kan du `embed` de nödvändiga biblioteken i ditt programspecifika klientbibliotek med hjälp av egenskapen embed i `cq:ClientLibraryFolder` nod.

#### Sökvägar i CSS-filer {#paths-in-css-files}

När du bäddar in CSS-filer använder den genererade CSS-koden sökvägar till resurser som är relativa till inbäddningsbiblioteket. Till exempel det bibliotek som är tillgängligt för allmänheten `/etc/client/libraries/myclientlibs/publicmain` bäddar in `/apps/myapp/clientlib` klientbibliotek:

The `main.css` filen innehåller följande format:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS-filen som `publicmain` noden genererar följande format med den ursprungliga bildens URL:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Se Inbäddade filer i utdata från HTML {#see-embedded-files}

Om du vill spåra ursprunget för inbäddad kod eller se till att inbäddade klientbibliotek ger det förväntade resultatet, kan du se namnen på de filer som bäddas in under körning. Om du vill se filnamnen lägger du till `debugClientLibs=true` parametern till webbsidans URL. Biblioteket som skapas innehåller `@import` -programsatser i stället för den inbäddade koden.

I exemplet i föregående [Bädda in kod från andra bibliotek](#embedding-code-from-other-libraries) -avsnittet, `/etc/client/libraries/myclientlibs/publicmain` klientbiblioteksmappen bäddar in `/apps/myapp/clientlib` biblioteksmapp för klient. Om du lägger till parametern på webbsidan skapas följande länk i webbsidans källkod:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Öppna `publicmain.css` filen visar följande kod:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Lägg till följande text i URL:en för HTML i webbläsarens adressruta:
   * `?debugClientLibs=true`
1. Visa sidans källa när sidan läses in.
1. Klicka på länken som anges som href för länkelementet för att öppna filen och visa källkoden.

### Använda preprocessorer {#using-preprocessors}

AEM gör det möjligt att ansluta till förprocessorer och levereras med stöd för [YUI-kompressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) för CSS och JavaScript och [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) för JavaScript med YUI inställt som AEM standardpreprocessor.

De anslutningsbara preprocessorerna möjliggör flexibel användning, inklusive:

* Definiera ScriptProcessors som kan bearbeta skriptkällor
* Processorer kan konfigureras med alternativ
* Processorer kan användas för miniatyrbilder, men även för icke-miniatyrärenden
* clientlib kan definiera vilken processor som ska användas

>[!NOTE]
>
>Som standard använder AEM YUI-kompressor. Se [YUI Compressor GitHub-dokumentation](https://github.com/yui/yuicompressor/issues) om du vill se en lista över kända fel. Om du växlar till GCC-komprimerare för vissa klienter kan vissa problem som uppstår när du använder YUI lösas.

>[!CAUTION]
>
>Placera inte ett miniatyrbibliotek i ett klientbibliotek. Ange i stället Raw-biblioteket och om miniatyrbilder krävs använder du alternativen för preprocessorerna.

#### Användning {#usage}

Du kan välja att konfigurera preprocessorer-konfigurationen per klientbibliotek eller system i hela systemet.

* Lägg till flervärdesegenskaper `cssProcessor` och `jsProcessor` på klientbiblioteksnoden
* Eller definiera systemets standardkonfiguration via **HTML Library Manager** OSGi-konfiguration

En preprocessorkonfiguration på klientlib-noden har företräde framför OSGI-konfigurationen.

#### Format och exempel {#format-and-examples}

##### Format {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### YUI-kompressor för CSS Minification och GCC för JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Typescript to Preprocess and then GCC to Minify and Obfuscate {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### Fler GCC-alternativ {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Mer information om GCC-alternativ finns i [GCC-dokumentation](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Ange systemstandardminiatyr {#set-system-default-minifier}

YUI anges som standardminifierare i AEM. Följ de här stegen för att ändra detta till GCC.

1. Gå till Apache Felix Config Manager på (`http://<host>:<portY/system/console/configMgr`)
1. Sök och redigera **Bibliotekshanteraren Adobe Granite HTML**.
1. Aktivera **Minify** (om det inte redan är aktiverat).
1. Ange värdet **Standardkonfigurationer för JS-processor** till `min:gcc`.
   * Alternativ kan skickas om de avgränsas med ett semikolon, till exempel `min:gcc;obfuscate=true`.
1. Klicka **Spara** för att spara ändringarna.
