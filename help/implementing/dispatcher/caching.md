---
title: Cache i AEM as a Cloud Service
description: 'Cache i AEM as a Cloud Service '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: b490d581532576bc526f9bd166003df7f2489495
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 1%

---

# Introduktion {#intro}

Trafiken passerar genom CDN till ett webbserverlager i Apache, som har stöd för moduler som dispatchern. För att öka prestandan används dispatchern främst som ett cacheminne för att begränsa bearbetningen av publiceringsnoderna.
Regler kan tillämpas på dispatcherns konfiguration för att ändra standardinställningarna för cacheförfallotid, vilket resulterar i cachelagring vid CDN. Observera att dispatchern också respekterar de resulterande rubrikerna för cacheförfallodatum om `enableTTL` är aktiverat i dispatcherns konfiguration, vilket innebär att det kommer att uppdatera specifikt innehåll även utanför det innehåll som publiceras om.

Den här sidan beskriver också hur dispatchercachen ogiltigförklaras, samt hur cachning fungerar på webbläsarnivå med avseende på klientbibliotek.

## Cachelagring {#caching}

### HTML/text {#html-text}

* som standard, cachelagras av webbläsaren i fem minuter, baserat på `cache-control` sidhuvud som genereras av apache-lagret. CDN respekterar också detta värde.
* standardinställningen för cachning mellan HTML/text kan inaktiveras genom att definiera `DISABLE_DEFAULT_CACHING` variabel i `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Detta kan vara användbart när din affärslogik kräver att sidhuvudet justeras (med ett värde som baseras på kalenderdag) eftersom sidhuvudet som standard är 0. Med det sagt, **var försiktig när du stänger av standardcachning.**

* kan åsidosättas för allt HTML/Text-innehåll genom att definiera `EXPIRATION_TIME` variabel i `global.vars` med AEM as a Cloud Service SDK Dispatcher-verktyg.
* kan åsidosättas på en mer detaljerad nivå med följande direktiv för apache mod_headers:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Var försiktig när du anger rubriker för global cachekontroll eller rubriker som matchar ett brett område så att de inte tillämpas på innehåll som du kanske tänker behålla privat. Överväg att använda flera direktiv för att säkerställa att reglerna tillämpas på ett detaljerat sätt. AEM as a Cloud Service tar då bort cachehuvudet om det upptäcker att det har tillämpats på det som identifierats som otillgängligt av dispatchern, vilket beskrivs i dispatcherdokumentationen. Om du vill tvinga AEM att alltid använda cachelagringshuvuden kan du lägga till **alltid** enligt följande:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Du måste se till att en fil under `src/conf.dispatcher.d/cache` har följande regel (som finns i standardkonfigurationen):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* För att förhindra att specifikt innehåll cachas **på CDN**, ställer du in rubriken Cache-Control till *private*. Följande förhindrar till exempel HTML-innehåll under en katalog med namnet **säker** från att cachas vid CDN:

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >Andra metoder, inklusive [AEM ACS Commons-projekt](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), kommer inte att åsidosätta värdena.

   >[!NOTE]
   >Observera att dispatchern fortfarande kan cachelagra innehåll enligt sina egna [regler för cachelagring](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Om du vill göra innehållet helt privat bör du se till att det inte cachas av dispatchern.

### Klientbibliotek (js, css) {#client-side-libraries}

* genom att använda AEM biblioteksramverk på klientsidan, genereras JavaScript- och CSS-kod på ett sådant sätt att webbläsare kan cachelagra den i oändlighet, eftersom alla ändringar manifesteras som nya filer med en unik sökväg.  HTML som refererar till klientbiblioteken kommer med andra ord att produceras efter behov så att kunderna kan uppleva nytt innehåll när det publiceras. Cachekontrollen är inställd på&quot;oföränderlig&quot; eller 30 dagar för äldre webbläsare som inte respekterar det oföränderliga&quot; värdet.
* se avsnittet [Bibliotek på klientsidan och versionskonsekvens](#content-consistency) om du vill ha mer information.

### Bilder och allt innehåll som är tillräckligt stort för att lagras i blobben {#images}

* som standard, inte cachelagrad
* kan ställas in på en finare kornig nivå med följande apache `mod_headers` direktiv:

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Se diskussionen i avsnittet html/text ovan för att vara försiktig så att du inte cachelagrar för mycket och även hur du tvingar AEM att alltid använda cachning med alternativet &quot;always&quot;.

   Det är nödvändigt att säkerställa att en fil i `src/conf.dispatcher.d/`cache har följande regel (som finns i standardkonfigurationen):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Kontrollera att resurser som ska hållas privata i stället för cachelagrade inte ingår i LocationMatch-direktivets filter.

   >[!NOTE]
   >Andra metoder, inklusive [AEM ACS Commons-projekt](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), kommer inte att åsidosätta värdena.

### Andra innehållsfiltyper i nodarkivet {#other-content}

* ingen standardcachelagring
* standard kan inte anges med `EXPIRATION_TIME` variabel som används för filtyperna html/text
* cacheminnets förfallotid kan anges med samma LocationMatch-strategi som beskrivs i avsnittet html/text genom att ange lämplig regex

## Invalidering av Dispatcher-cache {#disp}

I allmänhet behöver du inte göra Dispatcher-cachen ogiltig. Du bör i stället förlita dig på att dispatchern uppdaterar sin cache när innehållet publiceras om och att CDN respekterar förfallorubriker för cache.

### Invalidering av Dispatcher-cache under aktivering/inaktivering {#cache-activation-deactivation}

Precis som i tidigare versioner av AEM rensas innehållet från dispatcherns cache när du publicerar eller avpublicerar sidor. Om ett problem med cachelagring misstänks bör kunderna publicera om sidorna i fråga och se till att det finns en virtuell värd som matchar den lokala värden för ServerAlias, vilket krävs för att inaktivera dispatchercachen.


När publiceringsinstansen tar emot en ny version av en sida eller resurs från författaren, används justeringsagenten för att göra lämpliga sökvägar ogiltiga i dess dispatcher. Den uppdaterade sökvägen tas bort från dispatchercachen, tillsammans med dess överordnade, upp till en nivå (du kan konfigurera den med [statusfilernivå](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Cacheogiltigförklaring av explicit dispatcher {#explicit-invalidation}

I allmänhet behöver du inte göra innehåll i dispatchern ogiltigt manuellt, men det är möjligt om det behövs.

>[!NOTE]
>Före AEM as a Cloud Service fanns det två sätt att göra Dispatcher-cachen ogiltig.
>
>1. Anropa replikeringsagenten och ange agenten för rensning av publiceringsutgivaren
>2. Anropa `invalidate.cache` API (till exempel `POST /dispatcher/invalidate.cache`)

>
>Avsändaren `invalidate.cache` API-metoden stöds inte längre eftersom den bara riktar sig till en viss dispatchernod. AEM as a Cloud Service arbetar på tjänstenivå, inte på den enskilda nodnivån, och därmed görs ogiltighetsinstruktionerna i [Invaliderar cachelagrade sidor från AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) sidan är inte längre giltig för AEM as a Cloud Service.

Replikeringsrensningsagenten ska användas. Detta kan du göra med [Replikerings-API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). Slutpunkten för rensningsagenten är inte konfigurerbar, men förkonfigurerad att peka mot dispatchern, matchad med publiceringstjänsten som kör rensningsagenten. Flush-agenten kan oftast aktiveras av OSGi-händelser eller arbetsflöden.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 
-->

Bilden nedan visar detta.

![CDN](assets/cdnd.png "CDN")

Om det finns oro för att dispatchercachen inte rensas kontaktar du [kundsupport](https://helpx.adobe.com/support.ec.html) som vid behov kan tömma dispatchercachen.

CDN som hanteras av Adobe respekterar TTL:er och behöver därför inte tömmas. Om ett problem misstänks, [kontakta kundsupport](https://helpx.adobe.com/support.ec.html) som kan tömma ett CDN-cache som hanteras av Adobe efter behov.

## Bibliotek på klientsidan och versionskonsekvens {#content-consistency}

Sidorna består av HTML, Javascript, CSS och bilder. Kunderna uppmuntras att utnyttja [Klientbibliotek (clientlibs) - ramverk](/help/implementing/developing/introduction/clientlibs.md) importera JavaScript- och CSS-resurser till HTML-sidor, med hänsyn tagen till beroenden mellan JS-bibliotek.

Med clientlibs Framework får du automatisk versionshantering, vilket innebär att utvecklare kan checka in ändringar i JS-bibliotek i källkontrollen och att den senaste versionen blir tillgänglig när en kund publicerar sin version. Utan detta skulle utvecklare behöva ändra HTML manuellt med referenser till den nya versionen av biblioteket, vilket är särskilt betungande om många HTML-mallar delar samma bibliotek.

När de nya versionerna av biblioteken släpps i produktion uppdateras de refererande HTML-sidorna med nya länkar till de uppdaterade biblioteksversionerna. När webbläsarens cache har gått ut för en viss HTML-sida finns det ingen oro för att de gamla biblioteken kommer att läsas in från webbläsarens cache eftersom den uppdaterade sidan (från AEM) nu garanterat refererar till de nya versionerna av biblioteken. En uppdaterad HTML-sida kommer med andra ord att innehålla alla de senaste biblioteksversionerna.

Mekanismen för det här är en serialiserad hash-konvertering som läggs till i klientbibliotekslänken, vilket garanterar en unik versionshanterad URL-adress som webbläsaren kan använda för att cachelagra CSS/JS. Den serialiserade hashen uppdateras bara när innehållet i klientbiblioteket ändras. Detta innebär att om det inte sker några ändringar (dvs. inga ändringar av klientbibliotekets underliggande css/js) även med en ny distribution, förblir referensen densamma, vilket säkerställer färre avbrott i webbläsarens cache.

### Aktivera Longcache-versioner av klientbibliotek - AEM as a Cloud Service SDK QuickStart {#enabling-longcache}

Standardversionen av Clientlib som finns på en HTML-sida ser ut som i följande exempel:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

När strikt klientlib-versionshantering är aktiverad läggs en långsiktig hash-nyckel till som väljare i klientbiblioteket. Därför ser clientlib-referensen ut så här:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Strikta versioner av klientlib är aktiverat som standard i alla AEM as a Cloud Service miljöer.

Så här aktiverar du strikt versionshantering av klientlib i den lokala SDK-versionen av Quickstart:

1. Navigera till OSGi Configuration Manager `<host>/system/console/configMgr`
1. Hitta OSGi Config för Adobe Granite HTML Library Manager:
   * Markera kryssrutan för att aktivera Strikta versionshantering
   * I fältet Långsiktig cachenyckel på klientsidan anger du värdet /.*;hash
1. Spara ändringarna. Observera att det inte är nödvändigt att spara den här konfigurationen i källkontrollen eftersom AEM as a Cloud Service automatiskt aktiverar den här konfigurationen i utvecklings-, fas- och produktionsmiljöer.
1. Varje gång innehållet i klientbiblioteket ändras genereras en ny hash-nyckel och HTML-referensen uppdateras.
