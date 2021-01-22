---
title: Cache i AEM as a Cloud Service
description: 'Cache i AEM as a Cloud Service '
translation-type: tm+mt
source-git-commit: a02e035a842e7c633aaa926d0ab092b2c7aed5cb
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 1%

---


# Introduktion {#intro}

Trafiken passerar genom CDN till ett webbserverlager i Apache, som har stöd för moduler som dispatchern. För att öka prestandan används dispatchern främst som ett cacheminne för att begränsa bearbetningen av publiceringsnoderna.
Regler kan tillämpas på dispatcherns konfiguration för att ändra standardinställningarna för cacheförfallotid, vilket resulterar i cachelagring vid CDN. Observera att dispatchern också respekterar cacheförfallorubrikerna om `enableTTL` är aktiverat i dispatcherns konfiguration, vilket innebär att det uppdaterar specifikt innehåll även utanför det innehåll som publiceras om.

Den här sidan beskriver också hur dispatchercachen ogiltigförklaras, samt hur cachning fungerar på webbläsarnivå med avseende på klientbibliotek.

## Cachelagra {#caching}

### HTML/text {#html-text}

* som standard, cachelagras av webbläsaren i fem minuter, baserat på det `cache-control`-huvud som skickas från apache-lagret. CDN respekterar också detta värde.
* standardinställningen för HTML-/textcache kan inaktiveras genom att definiera variabeln `DISABLE_DEFAULT_CACHING` i `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Detta kan vara användbart när din affärslogik kräver att sidhuvudet justeras (med ett värde som baseras på kalenderdag) eftersom sidhuvudet som standard är 0. **Var dock försiktig när du stänger av standardcachning.**

* kan åsidosättas för allt HTML-/textinnehåll genom att definiera variabeln `EXPIRATION_TIME` i `global.vars` med AEM som SDK Dispatcher-verktyg för Cloud Service.
* kan åsidosättas på en mer detaljerad nivå med följande direktiv för apache mod_headers:

   ```
   <LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Var försiktig när du anger rubriker för global cachekontroll eller rubriker som matchar ett brett område så att de inte tillämpas på innehåll som du kanske tänker behålla privat. Överväg att använda flera direktiv för att säkerställa att reglerna tillämpas på ett detaljerat sätt. AEM som en Cloud Service tar då bort cachehuvudet om det upptäcker att det har tillämpats på det som inte kan nås av dispatchern, vilket beskrivs i dispatcherdokumentationen. Om du vill tvinga AEM att alltid använda cachelagring kan du lägga till alternativet &quot;always&quot; enligt följande:

   ```
   <LocationMatch "\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Du måste se till att en fil under `src/conf.dispatcher.d/cache` har följande regel (som finns i standardkonfigurationen):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Om du vill förhindra att specifikt innehåll cachelagras anger du rubriken Cache-Control till *private*. Följande förhindrar till exempel att HTML-innehåll i en katalog med namnet **myfolder** cachelagras:

   ```
      <LocationMatch "/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >De andra metoderna, inklusive [dispatcher-ttl AEM ACS Commons-projektet](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), kommer inte att åsidosätta värdena.

### Klientbibliotek (js, css) {#client-side-libraries}

* genom att använda AEM biblioteksramverk på klientsidan, genereras JavaScript- och CSS-kod på ett sådant sätt att webbläsare kan cachelagra den i oändlighet, eftersom alla ändringar manifesteras som nya filer med en unik sökväg.  Med andra ord kommer HTML som refererar till klientbiblioteken att produceras efter behov så att kunderna kan uppleva nytt innehåll när det publiceras. Cachekontrollen är inställd på&quot;oföränderlig&quot; eller 30 dagar för äldre webbläsare som inte respekterar det oföränderliga&quot; värdet.
* Mer information finns i avsnittet [Bibliotek på klientsidan och versionskonsekvens](#content-consistency).

### Bilder och allt innehåll som är tillräckligt stort lagras i bloblagring {#images}

* som standard, inte cachelagrad
* kan ställas in på en finare kornig nivå med följande direktiv för apache `mod_headers`:

   ```
      <LocationMatch "^\.*.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Se diskussionen i avsnittet html/text ovan för att vara försiktig så att du inte cachelagrar för mycket och även hur du tvingar AEM att alltid använda cachning med alternativet &quot;always&quot;.

   Det är nödvändigt att se till att en fil under `src/conf.dispatcher.d/`cache har följande regel (som finns i standardkonfigurationen):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Kontrollera att resurser som ska hållas privata i stället för cachelagrade inte ingår i LocationMatch-direktivets filter.

   >[!NOTE]
   >De andra metoderna, inklusive [dispatcher-ttl AEM ACS Commons-projektet](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), kommer inte att åsidosätta värdena.

### Andra innehållsfiltyper i nodarkivet {#other-content}

* ingen standardcachelagring
* standard kan inte anges med variabeln `EXPIRATION_TIME` som används för HTML-/textfiltyper
* cacheminnets förfallotid kan anges med samma LocationMatch-strategi som beskrivs i avsnittet html/text genom att ange lämplig regex

## Invalidering av Dispatcher-cache {#disp}

I allmänhet behöver du inte göra Dispatcher-cachen ogiltig. Du bör i stället förlita dig på att dispatchern uppdaterar sin cache när innehållet publiceras om och att CDN respekterar förfallorubriker för cache.

### Invalidering av Dispatcher-cache under aktivering/inaktivering {#cache-activation-deactivation}

Precis som i tidigare versioner av AEM rensas innehållet från dispatcherns cache när du publicerar eller avpublicerar sidor. Om ett cachningsproblem misstänks bör kunderna publicera om sidorna i fråga.

När publiceringsinstansen tar emot en ny version av en sida eller resurs från författaren, används justeringsagenten för att göra lämpliga sökvägar ogiltiga i dess dispatcher. Den uppdaterade sökvägen tas bort från dispatcher-cachen, tillsammans med dess överordnade, upp till en nivå (du kan konfigurera den med [statusfilnivå](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Cacheminnet för explicit dispatcher är ogiltigt {#explicit-invalidation}

I allmänhet behöver du inte göra innehåll i dispatchern ogiltigt manuellt, men det är möjligt om det behövs, vilket beskrivs nedan.

Före AEM som Cloud Service fanns det två sätt att ogiltigförklara dispatchercachen.

1. Anropa replikeringsagenten och ange agenten för rensning av publiceringsutgivaren
2. Anropa API:t `invalidate.cache` direkt (till exempel `POST /dispatcher/invalidate.cache`)

Avsändarens `invalidate.cache` API-metod stöds inte längre eftersom den bara adresserar en viss dispatchernod. AEM som en Cloud Service fungerar på tjänstenivå, inte på den enskilda nodnivån, och därför gäller inte invalideringsinstruktionerna i [Ovalidering av cachelagrade sidor från AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html)-sidan längre för AEM som en Cloud Service.
Istället bör agenten för tömning av replikering användas. Detta kan du göra med hjälp av replikerings-API:t. Dokumentationen för replikerings-API finns [här](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) och om du vill se ett exempel på tömning av cachen kan du gå till exempelsidan för [API](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) specifikt `CustomStep`-exemplet som utfärdar en replikeringsåtgärd av typen ACTIVATE till alla tillgängliga agenter. Slutpunkten för rensningsagenten är inte konfigurerbar, men förkonfigurerad att peka mot dispatchern, matchad med publiceringstjänsten som kör rensningsagenten. Flush-agenten kan oftast aktiveras av OSGi-händelser eller arbetsflöden.

Bilden nedan visar detta.

![](assets/cdnd.png "CDNCDN")

Om det finns oro för att dispatchercachen inte rensas kontaktar du [kundsupport](https://helpx.adobe.com/support.ec.html) som kan tömma dispatchercachen om det behövs.

CDN som hanteras av Adobe respekterar TTL:er och behöver därför inte tömmas. Om ett problem misstänks ska du [kontakta kundsupport](https://helpx.adobe.com/support.ec.html) som kan tömma ett CDN-cache som hanteras av Adobe vid behov.

## Klientbibliotek och versionskonsekvens {#content-consistency}

Sidorna består av HTML, JavaScript, CSS och bilder. Kunder uppmuntras att använda [Client-Side Libraries (clientlibs)-ramverket](/help/implementing/developing/introduction/clientlibs.md) för att importera JavaScript- och CSS-resurser till HTML-sidor, med hänsyn tagen till beroenden mellan JS-bibliotek.

Med clientlibs Framework får du automatisk versionshantering, vilket innebär att utvecklare kan checka in ändringar i JS-bibliotek i källkontrollen och att den senaste versionen blir tillgänglig när en kund publicerar sin version. Utan detta skulle utvecklare behöva ändra HTML manuellt med referenser till den nya versionen av biblioteket, vilket är särskilt betungande om många HTML-mallar delar samma bibliotek.

När de nya versionerna av biblioteken släpps i produktion uppdateras de refererande HTML-sidorna med nya länkar till de uppdaterade biblioteksversionerna. När webbläsarens cache har upphört att gälla för en viss HTML-sida finns det ingen oro för att de gamla biblioteken kommer att läsas in från webbläsarens cache eftersom den uppdaterade sidan (från AEM) nu garanterat refererar till de nya versionerna av biblioteken. En uppdaterad HTML-sida kommer med andra ord att innehålla alla de senaste biblioteksversionerna.

Mekanismen för det här är en serialiserad hash-konvertering som läggs till i klientbibliotekslänken, vilket garanterar en unik versionshanterad URL-adress som webbläsaren kan använda för att cachelagra CSS/JS. Den serialiserade hashen uppdateras bara när innehållet i klientbiblioteket ändras. Detta innebär att om det inte sker några ändringar (dvs. inga ändringar av klientbibliotekets underliggande css/js) även med en ny distribution, förblir referensen densamma, vilket säkerställer färre avbrott i webbläsarens cache.

### Aktivera Longcache-versioner av klientbibliotek - AEM som en Cloud Service-SDK QuickStart {#enabling-longcache}

Klientlib som standard finns på en HTML-sida ser ut som i följande exempel:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

När strikt klientlib-versionshantering är aktiverad läggs en långsiktig hash-nyckel till som väljare i klientbiblioteket. Därför ser clientlib-referensen ut så här:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Strikta versioner av klientlib är aktiverat som standard i alla AEM som en Cloud Service-miljö.

Så här aktiverar du strikt versionshantering av klientlib i den lokala SDK-versionen av Quickstart:

1. Navigera till OSGi Configuration Manager `<host>/system/console/configMgr`
1. Hitta OSGi Config för HTML Library Manager för Adobe Granite:
   * Markera kryssrutan för att aktivera Strikta versionshantering
   * I fältet Långsiktig cachenyckel på klientsidan anger du värdet /.*;hash
1. Spara ändringarna. Observera att det inte är nödvändigt att spara den här konfigurationen i källkontrollen eftersom AEM som Cloud Service automatiskt aktiverar den här konfigurationen i utvecklings-, fas- och produktionsmiljöer.
1. När innehållet i klientbiblioteket ändras genereras en ny hash-nyckel och HTML-referensen uppdateras.
