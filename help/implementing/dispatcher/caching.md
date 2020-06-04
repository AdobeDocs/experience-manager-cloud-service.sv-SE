---
title: Cachelagra i AEM som en molntjänst
description: 'Cachelagra i AEM som en molntjänst '
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# Introduktion {#intro}

Cachelagring vid CDN kan konfigureras med hjälp av dispatcherregler. Observera att dispatchern också respekterar de resulterande rubrikerna för cacheförfallodatum om `enableTTL` är aktiverade i dispatcherns konfiguration, vilket innebär att det uppdaterar specifikt innehåll även utanför det innehåll som publiceras om.

## Cachelagring {#caching}

### HTML/text {#html-text}

* som standard, cachelagras av webbläsaren i fem minuter, baserat på det cachekontrollhuvud som skickas av apache-lagret. CDN respekterar också detta värde.
* kan åsidosättas för allt HTML-/textinnehåll genom att definiera variabeln i `EXPIRATION_TIME` `global.vars` med hjälp av AEM som ett SDK Dispatcher-verktyg för molntjänster.
* kan åsidosättas på en mer detaljerad nivå med följande direktiv för apache mod_headers:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

Du måste se till att en fil under `src/conf.dispatcher.d/cache` har följande regel (som finns i standardkonfigurationen):

```
/0000
{ /glob "*" /type "allow" }
```

* Observera att andra metoder, inklusive [dispatcher-ttl AEM ACS Commons-projektet](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), inte kan åsidosätta värden.

### Klientbibliotek (js, css) {#client-side-libraries}

* genom att använda AEM:s biblioteksramverk på klientsidan, genereras JavaScript- och CSS-kod på ett sådant sätt att webbläsare kan cachelagra den i oändlighet, eftersom alla ändringar manifesteras som nya filer med en unik sökväg.  Med andra ord kommer HTML som refererar till klientbiblioteken att produceras efter behov så att kunderna kan uppleva nytt innehåll när det publiceras. Cachekontrollen är inställd på&quot;oföränderlig&quot; eller 30 dagar för äldre webbläsare som inte respekterar det oföränderliga&quot; värdet.
* Mer information finns i avsnittet Bibliotek på [klientsidan och versionskonsekvens](#content-consistency) .

### Bilder och allt innehåll som är tillräckligt stort för att lagras i blobben {#images}

* som standard, inte cachelagrad
* kan ställas in på en finare kornig nivå genom följande `mod_headers` direktiv:

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

Det är nödvändigt att se till att en fil under src/conf.dispatcher.d/cache har följande regel (som finns i standardkonfigurationen):

```
/0000
{ /glob "*" /type "allow" }
```

Kontrollera att resurser som ska hållas privata i stället för cachelagrade inte ingår i LocationMatch-direktivets filter.

* Observera att andra metoder, inklusive [dispatcher-ttl AEM ACS Commons-projektet](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), inte kan åsidosätta värden.

### Andra innehållsfiltyper i nodarkivet {#other-content}

* ingen standardcachelagring
* standard kan inte anges med den `EXPIRATION_TIME` variabel som används för HTML-/textfiltyper
* cacheminnets förfallotid kan anges med samma LocationMatch-strategi som beskrivs i avsnittet html/text genom att ange lämplig regex

## Dispatcher {#disp}

Trafiken går igenom en webbserver med apache som har stöd för moduler som dispatchern. Avsändaren används främst som cache för att begränsa bearbetningen av publiceringsnoderna för att öka prestandan.

Så som beskrivs i CDN:s cachelagringsavsnittet kan regler tillämpas på dispatcherkonfigurationen för att ändra standardinställningarna för cacheförfallotid.

I resten av det här avsnittet beskrivs överväganden som rör invalidering av dispatchercache. För de flesta kunder bör det inte vara nödvändigt att ogiltigförklara dispatchercachen, i stället förlita sig på att dispatchern uppdaterar cachen när innehållet publiceras om, och CDN respekterar förfallorubriker för cachen.

### Invalidering av Dispatcher-cache under aktivering/inaktivering {#cache-activation-deactivation}

Precis som i tidigare versioner av AEM rensas innehållet från dispatchercachen när du publicerar eller avpublicerar sidor. Om ett problem med cachning misstänks bör kunderna publicera om sidorna i fråga.

När publiceringsinstansen tar emot en ny version av en sida eller resurs från författaren, används justeringsagenten för att göra lämpliga sökvägar ogiltiga i dess dispatcher. Den uppdaterade sökvägen tas bort från dispatchercachen, tillsammans med dess överordnade, upp till en nivå (du kan konfigurera den med [statusfilnivån](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

### Cacheogiltigförklaring av explicit dispatcher {#explicit-invalidation}

I allmänhet behöver du inte göra innehåll i dispatchern ogiltigt manuellt, men det är möjligt om det behövs, vilket beskrivs nedan.

Före AEM som molntjänst fanns det två sätt att ogiltigförklara dispatchercachen.

1. Anropa replikeringsagenten och ange agenten för rensning av publiceringsutgivaren
2. Anropa `invalidate.cache` API:t direkt (till exempel `POST /dispatcher/invalidate.cache`)

Avsändarens `invalidate.cache` API-metod stöds inte längre eftersom den bara adresserar en viss dispatchernod. AEM som en molntjänst arbetar på tjänstenivå, inte på nodnivå. Instruktionerna för ogiltigförklaring på sidan [Invalidera cachelagrade sidor från AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) är därför inte längre giltiga för AEM som en molntjänst.
Istället bör agenten för tömning av replikering användas. Detta kan du göra med hjälp av replikerings-API:t. Dokumentationen för replikerings-API finns [här](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) . Ett exempel på hur du tömmer cachen finns på exempelsidan [för](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API. Exemplet `CustomStep` innehållerexempel på hur du skickar en replikeringsåtgärd av typen ACTIVATE till alla tillgängliga agenter. Slutpunkten för rensningsagenten är inte konfigurerbar, men förkonfigurerad att peka mot dispatchern, matchad med publiceringstjänsten som kör rensningsagenten. Flush-agenten kan oftast aktiveras av OSGi-händelser eller arbetsflöden.

Bilden nedan visar detta.

![](assets/cdnd.png "CDNCDN")

Om det finns oro för att dispatchercachen inte rensas kontaktar du [kundsupport](https://helpx.adobe.com/support.ec.html) som kan tömma dispatchercachen om det behövs.

CDN som hanteras av Adobe respekterar TTL:er och behöver därför inte tömmas. Om du misstänker ett problem [kontaktar du kundsupporten](https://helpx.adobe.com/support.ec.html) som kan tömma ett Adobe-hanterat CDN-cacheminne efter behov.

## Bibliotek på klientsidan och versionskonsekvens {#content-consistency}

Sidorna består av HTML, JavaScript, CSS och bilder. Kunder uppmuntras att använda ramverket för klientbibliotek (clientlibs) för att importera JavaScript- och CSS-resurser till HTML-sidor, med hänsyn tagen till beroenden mellan JS-bibliotek.

Med clientlibs Framework får du automatisk versionshantering, vilket innebär att utvecklare kan checka in ändringar i JS-bibliotek i källkontrollen och att den senaste versionen blir tillgänglig när en kund publicerar sin version. Utan detta skulle utvecklare behöva ändra HTML manuellt med referenser till den nya versionen av biblioteket, vilket är särskilt betungande om många HTML-mallar delar samma bibliotek.

När de nya versionerna av biblioteken släpps i produktion uppdateras de refererande HTML-sidorna med nya länkar till de uppdaterade biblioteksversionerna. När webbläsarens cache har gått ut för en viss HTML-sida finns det ingen oro för att de gamla biblioteken kommer att läsas in från webbläsarens cache eftersom den uppdaterade sidan (från AEM) nu garanterat refererar till de nya versionerna av biblioteken. En uppdaterad HTML-sida kommer med andra ord att innehålla alla de senaste biblioteksversionerna.

Mekanismen för det här är en serialiserad hash-konvertering som läggs till i klientbibliotekslänken, vilket garanterar en unik versionshanterad URL-adress som webbläsaren kan använda för att cachelagra CSS/JS. Den serialiserade hashen uppdateras bara när innehållet i klientbiblioteket ändras. Detta innebär att om det inte sker några ändringar (dvs. inga ändringar av klientbibliotekets underliggande css/js) även med en ny distribution, förblir referensen densamma, vilket säkerställer färre avbrott i webbläsarens cache.

### Aktivera Longcache-versioner av klientbibliotek - AEM som molntjänst SDK Snabbstart {#enabling-longcache}

Klientlib som standard finns på en HTML-sida ser ut som i följande exempel:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

När strikt klientlib-versionshantering är aktiverad läggs en långsiktig hash-nyckel till som väljare i klientbiblioteket. Därför ser clientlib-referensen ut så här:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Strikta versioner av klientlib är aktiverat som standard i alla AEM-miljöer som molntjänster.

Så här aktiverar du strikt versionshantering av klientlib i den lokala SDK-versionen av Quickstart:

1. Navigera till OSGi Configuration Manager `<host>/system/console/configMgr`
1. Hitta OSGi Config för Adobe Granite HTML Library Manager:
   * Markera kryssrutan för att aktivera Strikta versionshantering
   * I fältet Långsiktig cachenyckel på klientsidan anger du värdet /.*;hash
1. Spara ändringarna. Observera att det inte är nödvändigt att spara den här konfigurationen i källkontrollen eftersom AEM som en molntjänst automatiskt aktiverar den här konfigurationen i utvecklings-, fas- och produktionsmiljöer.
1. När innehållet i klientbiblioteket ändras genereras en ny hash-nyckel och HTML-referensen uppdateras.
