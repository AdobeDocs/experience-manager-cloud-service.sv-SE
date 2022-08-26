---
title: Cache i AEM as a Cloud Service
description: 'Cache i AEM as a Cloud Service '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: a624b4f1999238adae2f6a03c2169cb30de9f730
workflow-type: tm+mt
source-wordcount: '2591'
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
* kan åsidosättas på en mer detaljerad nivå, inklusive kontroll av CDN och webbläsarcache separat, med följande direktiv för apache mod_headers:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >Rubriken Surrogate-Control gäller för CDN som hanteras av Adobe. Om du använder en [kundhanterad CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), kan det krävas en annan rubrik beroende på din CDN-leverantör.

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

### Bilder och allt innehåll som är tillräckligt stort för att lagras i blob {#images}

Standardbeteendet för program som skapats efter mitten av maj 2022 (särskilt för program-ID som är högre än 65000) är att cachelagra som standard, samtidigt som autentiseringskontexten för begäran respekteras. Äldre program (program-ID som är lika med eller lägre än 65000) cache-lagrar inte blobbinnehåll som standard.

I båda fallen kan cachelagringshuvuden åsidosättas på en mer detaljerad nivå i lagret apache/dispatcher med hjälp av apache `mod_headers` direktiv, till exempel:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Var försiktig så att du inte cachelagrar för mycket när du ändrar cachelagringshuvuden i dispatcherlagret. Mer information finns i avsnittet HTML/text. [ovan](#html-text). Se även till att resurser som ska hållas privata (i stället för cachelagrade) inte ingår i `LocationMatch` -filter.

#### Nytt standardbeteende för cachelagring {#new-caching-behavior}

AEM kommer att ange cacherubriker beroende på om cachehuvudet redan har angetts och värdet för begärandetypen. Observera att om ingen cache-kontrollrubrik har angetts cachelagras offentligt innehåll och autentiserad trafik anges till privat. Om en cache-kontrollrubrik har angetts ändras inte cacherubrikerna.

| Cachekontrollhuvud finns? | Typ av begäran | AEM anger cacherubriker till |
|------------------------------|---------------|------------------------------------------------|
| Nej | public | Cache-Control: public, max-age=600, oföränderlig |
| Nej | autentiserad | Cache-Control: private, max-age=600, oföränderlig |
| Ja | alla | oförändrad |

Även om det inte rekommenderas går det att ändra det nya standardbeteendet så att det följer det äldre beteendet (program-ID som är lika med eller lägre än 65000) genom att ställa in miljövariabeln för Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` till false.

#### Äldre standardbeteende för cachelagring {#old-caching-behavior}

Som standard cachelagras inte blobbinnehåll i AEM.

>[!NOTE]
>Vi rekommenderar att du ändrar det äldre standardbeteendet så att det överensstämmer med det nya beteendet (program-ID som är högre än 65000) genom att ange Cloud Managers miljövariabel AEM_BLOB_ENABLE_CACHING_HEADERS till true. Om programmet redan är öppet kontrollerar du att innehållet fungerar som du tänkt dig efter ändringarna.

>[!NOTE]
>Andra metoder, inklusive [AEM ACS Commons-projekt](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), kommer inte att åsidosätta värdena.

### Andra innehållsfiltyper i nodarkivet {#other-content}

* ingen standardcachelagring
* standard kan inte anges med `EXPIRATION_TIME` variabel som används för filtyperna html/text
* cacheminnets förfallotid kan anges med samma LocationMatch-strategi som beskrivs i avsnittet html/text genom att ange lämplig regex

### Ytterligare optimeringar {#further-optimizations}

* Undvik att använda `User-Agent` som en del av `Vary` header. Äldre versioner av standardinställningen för dispatcher (före arkivtypsversion 28) innehöll detta och vi rekommenderar att du tar bort det genom att följa stegen nedan.
   * Hitta värdfilerna i `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Ta bort eller kommentera raden: `Header append Vary User-Agent env=!dont-vary` från alla värdfiler, med undantag för default.vhost, som är skrivskyddad
* Använd `Surrogate-Control` huvud för att styra CDN-cachning oberoende av webbläsarcachning
* Överväg att tillämpa [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) och [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) Direktiv som tillåter bakgrundsuppdatering och undviker cachemissar, så att innehållet är snabbt och uppdaterat för användarna.
   * Det finns många sätt att tillämpa dessa direktiv, men att lägga till en 30-minutersperiod `stale-while-revalidate` till alla rubriker för cachekontroll är en bra utgångspunkt.
* Några exempel följer för olika innehållstyper, som kan användas som vägledning när du ställer in egna cachningsregler. Fundera noga över och testa dina specifika inställningar och krav:

   * Cachelagra ändringsbara klientbiblioteksresurser för 12 timmar och bakgrundsuppdatering efter 12 timmar.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Cachelagra oföränderliga biblioteksresurser på lång sikt (30 dagar) med bakgrundsuppdatering för att undvika MISS.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Cachelagra HTML-sidor för 5 min med bakgrundsuppdatering 1 timme i webbläsaren och 12 timmar i CDN. Cache-Control-rubriker läggs alltid till så det är viktigt att se till att matchande HTML-sidor under /content/* är avsedda att vara offentliga. Om så inte är fallet bör du överväga att använda en mer specifik regex.

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Cachelagra innehållstjänster/Sling-modellexporterarens json-svar för 5 minuter med bakgrundsuppdatering 1 timme i webbläsaren och 12 timmar i CDN.

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Cachelagra oföränderliga URL:er från huvudbildkomponenten på lång sikt (30 dagar) med bakgrundsuppdatering för att undvika MISS.

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Cachelagra ändringsbara resurser från DAM som bilder och video i 24 timmar och bakgrundsuppdatering efter 12 timmar för att undvika MISS

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEAD beteende {#request-behavior}

När en begäran från HEAD tas emot i CDN i Adobe för en resurs som är **not** cachelagras, begäran omformas och tas emot av dispatchern och/eller AEM som en GET-begäran. Om svaret är nåbart kommer efterföljande förfrågningar från HEAD att besvaras av CDN. Om svaret inte är tillgängligt kommer efterföljande HEAD-begäranden att skickas till dispatchern och/eller AEM-instansen under en tidsperiod som beror på `Cache-Control` TTL.

<!---### Marketing campaign parameters {#marketing-parameters}

Marketing campaign parameters are added to a website to track different marketing campaigns but rarely have impact on how the website should look like. That's why in the dispatcher they can mostly be ignored for dispatcher caching decisions. This can be achieved by setting the [ignoreUrlParams](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters) parameter.
Adobe maintains a list of commonly used marketing query parameters in the file `conf.dispatcher.d/cache/marketing_query_parameters.any`. Uncomment the lines that are used by the websites marketing campaigns and uncomment the `/ignoreUrlParams` section in the enabled farm.

```
/ignoreUrlParams {
 	/0001 { /glob "*" /type "deny" }
 	$include "../cache/marketing_query_parameters.any"
}
```
-->

## Invalidering av Dispatcher-cache {#disp}

I allmänhet behöver du inte göra Dispatcher-cachen ogiltig. Du bör i stället förlita dig på att dispatchern uppdaterar sin cache när innehållet publiceras om och att CDN respekterar förfallorubriker för cache.

### Invalidering av Dispatcher-cache under aktivering/inaktivering {#cache-activation-deactivation}

Precis som i tidigare versioner av AEM rensas innehållet från dispatcherns cache när du publicerar eller avpublicerar sidor. Om ett problem med cachelagring misstänks bör kunderna publicera om sidorna i fråga och se till att det finns en virtuell värd som matchar den lokala värden för ServerAlias, vilket krävs för att inaktivera dispatchercachen.

När publiceringsinstansen tar emot en ny version av en sida eller resurs från författaren, används justeringsagenten för att göra lämpliga sökvägar ogiltiga i dess dispatcher. Den uppdaterade sökvägen tas bort från dispatchercachen, tillsammans med dess överordnade, upp till en nivå (du kan konfigurera den med [statusfilernivå](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Explicit ogiltigförklaring av dispatchercachen {#explicit-invalidation}

Adobe rekommenderar att du förlitar dig på standardcache-huvuden för att styra innehållets leveranslivscykel. Om det behövs kan du emellertid göra innehållet ogiltigt direkt i dispatchern.

Följande lista innehåller scenarier där du kanske vill göra cachen ogiltig (men avlyssna när ogiltigförklaringen har slutförts):

* Efter publicering av innehåll som upplevelsefragment eller innehållsfragment blir publicerat och cachelagrat innehåll som refererar till dessa element ogiltigt.
* Meddela ett externt system när refererade sidor har ogiltigförklarats.

Det finns två sätt att göra cacheminnet explicit ogiltigt:

* Det bästa sättet är att använda Sling Content Distribution (SCD) från författaren.
* Genom att använda replikerings-API:t för att anropa agenten för tömning av publiceringsdispatcher.

Metoderna skiljer sig åt när det gäller tillgång till nivån, möjlighet att deduplicera händelser och händelsebearbetningsgaranti. Tabellen nedan sammanfattar dessa alternativ:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Ej tillämpligt</th>
    <th>Tillgång till nivån</th>
    <th>Deduplicering </th>
    <th>Garanti </th>
    <th>Åtgärd </th>
    <th>Effekt </th>
    <th>Beskrivning </th>
  </tr>  
  <tr>
    <td>Sling Content Distribution (SCD) API</td>
    <td>Författare</td>
    <td>Möjligt med antingen Discovery API eller genom att aktivera <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">dedupliceringsläge</a>.</td>
    <td>Minst en gång.</td>
    <td>
     <ol>
       <li>LÄGG TILL</li>
       <li>DELETE</li>
       <li>OGILTIG</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Hierarkisk/stationär nivå</li>
       <li>Hierarkisk/stationär nivå</li>
       <li>Endast nivå-resurs</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publicerar innehåll och gör cachen ogiltig.</li>
       <li>Tar bort innehåll och gör cachen ogiltig.</li>
       <li>Gör innehållet ogiltigt utan att publicera det.</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>Replikerings-API</td>
    <td>Publicera</td>
    <td>Inte möjligt, händelse som aktiveras för varje publiceringsinstans.</td>
    <td>Bästa försök.</td>
    <td>
     <ol>
       <li>AKTIVERA</li>
       <li>INAKTIVERA</li>
       <li>DELETE</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Hierarkisk/stationär nivå</li>
       <li>Hierarkisk/stationär nivå</li>
       <li>Hierarkisk/stationär nivå</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publicerar innehåll och gör cachen ogiltig.</li>
       <li>Från författar-/publiceringsnivå - Tar bort innehåll och gör cachen ogiltig.</li>
       <li><p><strong>Från författarnivå</strong> - Tar bort innehåll och gör cachen ogiltig (om den aktiveras från AEM Author-nivån i Publish Agent).</p>
           <p><strong>Från publiceringsnivå</strong> - Gör endast cacheminnet (om det aktiveras från AEM-publiceringsnivån på agenten för tömning eller tömning endast av resurser) ogiltigt.</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Observera att de två åtgärder som är direkt relaterade till cacheogiltigförklaring är Sling Content Distribution (SCD) API Invalidate och Replication API Deactivate.

Vi kan också se följande från tabellen:

* SCD API behövs när varje händelse måste garanteras, till exempel synkronisering med ett externt system som kräver korrekt kunskap. Observera, att om det finns en händelse för publiceringsnivåuppskalning vid tidpunkten för ogiltigförklaringsanropet, kommer en extra händelse att utlösas när varje ny publiceringsprocess bearbetar ogiltigförklaringen.

* Att använda replikerings-API är inte vanligt, men bör användas i fall där utlösaren för att göra cachen ogiltig kommer från publiceringsnivån och inte från författarnivån. Det här kan vara användbart om TTL för dispatcher har konfigurerats.

Sammanfattningsvis, om du vill göra dispatchercachen ogiltig, rekommenderar vi att du använder SCD API-åtgärden Ovalidate från författare. Dessutom kan du lyssna efter händelsen så att du kan utlösa fler efterföljande åtgärder.

### Sling Content Distribution (SCD) {#sling-distribution}

>[!NOTE]
>När du använder instruktionerna nedan bör du vara medveten om att du bör testa den anpassade koden i en AEM Cloud Service Dev-miljö och inte lokalt.

När du använder SCD-åtgärden från författaren är implementeringsmönstret följande:

1. Skriv egen kod från författaren för att anropa distributionen av försäljningsinnehåll [API](https://sling.apache.org/documentation/bundles/content-distribution.html), skickar åtgärden invalidate med en lista över sökvägar:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Valfritt) Lyssna efter en händelse som återger den resurs som ogiltigförklaras för alla dispatcherinstanser:


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* (Valfritt) Kör affärslogik i `invalidated(String[] paths, String packageId)` ovanstående metod.

>[!NOTE]
>
>CDN i Adobe rensas inte när avsändaren ogiltigförklaras. CDN som hanteras av Adobe respekterar TTL:er och behöver därför inte tömmas.

### Replikerings-API {#replication-api}

Nedan visas implementeringsmönstret när åtgärden för inaktivering av replikerings-API används:

1. Anropa replikerings-API:t på publiceringsnivån för att utlösa replikeringsagenten för tömning av publiceringsdispatcher.

Slutpunkten för rensningsagenten kan inte konfigureras utan är i stället förkonfigurerad så att den pekar på dispatcher, matchad med publiceringstjänsten som körs tillsammans med tömningsagenten.

Flush-agenten kan oftast aktiveras av anpassad kod som baseras på OSGi-händelser eller arbetsflöden.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals(“flush”);
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

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
