---
title: Exempeltyper för ContextHub-gränssnittsmodul
description: ContextHub innehåller flera exempelmoduler för användargränssnitt som du kan använda i dina lösningar
translation-type: tm+mt
source-git-commit: 2a589ff554a5cced3d7ad45d981697debb73992f
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---


# Exempeltyper för ContextHub-gränssnittsmodul {#sample-contexthub-ui-module-types}

ContextHub innehåller flera exempelmoduler för användargränssnitt som du kan använda i dina lösningar. Följande information tillhandahålls:

* Huvudfunktionerna i gränssnittsmodulen.
* Var du hittar källkoden så att du kan öppna den i utbildningssyfte.
* Konfigurera gränssnittsmodulen.

Mer information om hur du lägger till gränssnittsmoduler i ContextHub finns i [Lägga till en gränssnittsmodul](configuring-contexthub.md#adding-a-ui-module). Mer information om hur du utvecklar gränssnittsmoduler finns i [Skapa gränssnittsmodultyper](extending-contexthub.md#creating-contexthub-ui-module-types)för ContextHub.

## contexthub.base UI-modultyp {#contexthub-base-ui-module-type}

Modultypen context.base är bastypen för alla andra gränssnittsmodultyper. Det innehåller därför generiska funktioner för återgivning av butiksdata.

Följande funktioner är tillgängliga:

* **Titel och ikon:** Ange en rubrik för användargränssnittsmodulen och en ikon. Ikonen kan refereras via en URL eller från ikonbiblioteket för Coral UI.
* **Lagra data:** Identifiera ett eller flera arkiv som data ska hämtas från.
* **Innehåll:** Ange innehållet som visas i gränssnittsmodulen så som det visas i ContextHub-verktygsfältet.
* **Leveransinnehåll:** Ange innehållet som visas i en pekare när användaren klickar eller trycker på gränssnittsmodulen.
* **Helskärmsläge:** Kontrollera om helskärmsläge tillåts.

Källkoden finns på `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.

### Konfiguration {#configuration}

Konfigurera gränssnittsmodulen contexthub.base med hjälp av ett JavaScript-objekt i JSON-format. Inkludera någon av följande egenskaper för att konfigurera gränssnittsmodulens funktioner:

* **bild:** En URL till en bild som ska visas som ikon.
* **ikon:** Namnet på en [Coral UI-ikonklass](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) . Om du anger ett värde för både ikonen och bildegenskaperna används bilden.
* **titel:** En rubrik för gränssnittsmodulen. Titeln visas när pekaren pausas över ikonen för modulen Gränssnitt.
* **helskärm:** Ett booleskt värde som anger om gränssnittsmodulen stöder helskärmsläge. Används `true` för helskärmsläge och `false` för att förhindra helskärmsläge.
* **mall:** En [Handlebars](https://handlebarsjs.com/) -mall som anger innehållet som ska återges i ContextHub-verktygsfältet. Använd högst två `<p>` taggar.
* **storeMapping:** En nyckel/arkivmappning. Använd nyckeln i Handlebar-mallar för att komma åt associerade ContextHub-lagringsdata.
* **lista:** En array med objekt som ska visas som en lista i en portfölj när användaren klickar på gränssnittsmodulen. Om du tar med det här objektet ska du inte ta med poverTemplate. Värdet är en array med objekt med följande tangenter:
   * titel: Den text som ska visas för det här objektet
   * bild: (Valfritt) En URL till en bild som ska visas till vänster
   * ikon: (Valfritt) En CUI-ikonklass som ska visas till vänster. ignoreras om en bild anges
   * markerat: (Valfritt) Ett booleskt värde som anger om det här objektet ska visas som markerat (true=selected). Som standard visas markerade objekt med ett fetstil. Använd en `listType` egenskap för att konfigurera andra utseenden (se nedan).
* **listType:** Det format som ska användas för att överföra listobjekt. Använd något av följande värden:
   * bock
   * kryssruta
   * radio
* **popoverTemplate:** En mall för hanteringsfält som anger innehållet som ska återges i pekaren när användaren klickar på gränssnittsmodulen. Om du tar med det här objektet ska du inte ta med `list` objektet.

### Exempel {#example}

I följande exempel konfigureras en c`ontexthub.base` UI-modul för att visa information från ett [contexthub.emulators](sample-stores.md#granite-emulators-sample-store-candidate) -arkiv. Objektet visar hur du hämtar data från arkivet med hjälp av den nyckel som `template` `storeMapping` objektet upprättar.

```javascript
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![contexthub.base-modul](assets/base-module.png)

## contexthub.browserinfo UI Module Type {#contexthub-browserinfo-ui-module-type}

I modulen `contexthub.browserinfo` Gränssnitt visas information om klientens webbläsare och operativsystem. Information hämtas från surferinfo store, baserat på [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) store-kandidaten.

![contexthub.browserinfo module](assets/browserinfo-module.png)

Källkoden för gränssnittsmodulen finns på `/libs/granite/contexthub/components/modules/browserinfo`. Även om `contexthub.browserinfo` utökar `contexthub.base` gränssnittsmodulen, åsidosätts eller ges inga ytterligare funktioner. Implementeringen innehåller en standardkonfiguration för återgivning av webbläsarinformation.

### Konfiguration {#configuration-1}

Instanser av gränssnittsmodulen contexthub.browserinfo kräver inget värde för Detaljkonfiguration. Följande JSON-text representerar modulens standardkonfiguration.

```javascript
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## kontexthub.datetime, gränssnittsmodultyp {#contexthub-datetime-ui-module-type}

I `contexthub.datetime` gränssnittsmodulen visas datumet och tiden som lagras i en butik med namnet datetime som baseras på [contexthub.datetime](sample-stores.md#contexthub-datetime-sample-store-candidate) -lagringskanalen.

![contexthub.datetime-modul](assets/datetime-module.png)

Modulen innehåller ett leveransformulär där du kan ändra datum och tid i butiken.

Källan till `contexthub.datetime` gränssnittsmodulen finns på `/libs/granite/contexthub/components/modules/datetime`.

### Konfiguration {#configuration-2}

Instanser av gränssnittsmodulen contexthub.datetime kräver inget värde för Detaljkonfiguration. Följande JSON-text representerar modulens standardkonfiguration.

```javascript
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## kontexthub.location, gränssnittsmodultyp {#contexthub-location-ui-module-type}

Användargränssnittsmodulen `contexthub.location` visar klientens longitud och latitud. Modulen innehåller en portfölj som visar en Google-karta som du kan klicka på för att ändra den aktuella platsen. Modulen hämtar information från ett ContextHub-arkiv med namnet geolocation som baseras på [lagringskanalen contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) .

![contexthub.location-modul](assets/location-module.png)

Källan till användargränssnittsmodulen finns på `/etc/cloudsettings/default/contexthub/geolocation`.

### Konfiguration {#configuration-4}

Instanser av gränssnittsmodulen contexthub.location kräver inget värde för detaljkonfigurationen. Följande JSON-text representerar modulens standardkonfiguration.

```javascript
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI Module Type {#contexthub-screen-orientation-ui-module-type}

Användargränssnittsmodulen visar klientens aktuella skärmorientering. `contexthub.screen-orientation` Modulen är inaktiverad som standard, men den innehåller en funktion som gör att du kan välja en orientering. Modulen hämtar information från ett ContextHub-lager med namnet emulators som är baserat på lagringskanalen [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) .

![contexthub.screen-orientation module](assets/screen-orientation-module.png)

Källan till användargränssnittsmodulen finns på `/libs/granite/contexthub/components/modules/screen-orientation`.

### Konfiguration {#configuration-5}

Instanser av `contexthub.screen-orientation` UI-modulen kräver inget värde för Detaljkonfiguration. Följande JSON-text representerar modulens standardkonfiguration. Observera att `clickable` egenskapen är `false` som standard. Om du åsidosätter standardkonfigurationen som du anger `clickable` till `true`visas ett popup-fönster där du kan välja orientering när du klickar på modulen.

```javascript
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## contexthub.tagcloud-modultyp {#contexthub-tagcloud-ui-module-type}

I modulen `contexthub.tagcloud` Gränssnitt visas information om taggar. I verktygsfältet visar gränssnittsmodulen antalet taggar. Popup-fönstret visar ett tagcloud och en textruta för att lägga till nya taggar. Användargränssnittsmodulen hämtar information från ett ContextHub-arkiv med namnet tagcloud som är baserat på [contexthub.tagcloud](sample-stores.md#contexthub-tagcloud-sample-data-store) -butikskandidaten.

![contexthub.tagcloud-modul](assets/tagcloud-module.png)

Källan till användargränssnittsmodulen finns på `/libs/granite/contexthub/components/modules/tagcloud`.

### Konfiguration {#configuration-6}

Instanser av `contexthub.tagcloud` UI-modulen kräver inget värde för Detaljkonfiguration. Följande JSON-text representerar modulens standardkonfiguration.

```javascript
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## granite.profile UI Module Type {#granite-profile-ui-module-type}

Användargränssnittsmodulen `granite.profile` ContextHub visar visningsnamnet för den aktuella användaren. Popup-fönstret visar användarens inloggningsnamn och gör att du kan ändra värdet för visningsnamnet. Användargränssnittsmodulen hämtar information från ett ContextHub-arkiv med namnet profile som baseras på [lagringskanalen granite.profile](sample-stores.md#granite-profile-sample-store-candidate) .

![granite.profile-modul](assets/profile-module.png)

Källan till användargränssnittsmodulen finns i `/libs/granite/contexthub/components/modules/profile`.

### Konfiguration {#configuration-7}

Instanser av `granite.profile` UI-modulen kräver inget värde för Detaljkonfiguration. Följande JSON-text representerar modulens standardkonfiguration.

```javascript
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
