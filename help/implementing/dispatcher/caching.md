---
title: Cachelagring i AEM as a Cloud Service
description: Lär dig grunderna i cachning på AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 8215686031de1bc37ce37bfdce252b3997646042
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 0%

---

# Introduktion {#intro}

Trafiken passerar genom CDN till ett Apache-webbserverlager som stöder moduler som Dispatcher. För att öka prestandan används Dispatcher främst som ett cacheminne för att begränsa bearbetningen på publiceringsnoderna.
Regler kan tillämpas på Dispatcher-konfigurationen för att ändra standardinställningarna för cacheförfallotid, vilket resulterar i cachelagring vid CDN. Dispatcher respekterar även de resulterande rubrikerna för cacheförfallodatum om `enableTTL` är aktiverat i Dispatcher-konfigurationen, vilket innebär att det uppdaterar specifikt innehåll även utanför det innehåll som publiceras om.

Den här sidan beskriver också hur Dispatcher-cachen ogiltigförklaras och hur cachning fungerar på webbläsarnivå för klientbibliotek.

## Cachning {#caching}

### HTML/text {#html-text}

* som standard, cachelagras av webbläsaren i fem minuter, baserat på `cache-control` sidhuvud som genereras av Apache-lagret. CDN respekterar också detta värde.
* standardinställningen för cachning mellan HTML/text kan inaktiveras genom att definiera `DISABLE_DEFAULT_CACHING` variabel i `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Den här metoden är till exempel användbar när din affärslogik kräver finjustering av sidhuvudet (med ett värde som baseras på kalenderdag) eftersom sidhuvudet som standard är 0. Med det sagt, **var försiktig när du stänger av standardcachelagring.**

* kan åsidosättas för allt HTML/Text-innehåll genom att definiera `EXPIRATION_TIME` variabel i `global.vars` med AEM as a Cloud Service SDK Dispatcher-verktyg.
* kan åsidosättas på en mer detaljerad nivå, inklusive kontroll av CDN och webbläsarcache separat, med följande Apache `mod_headers` direktiv:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >Rubriken Surrogate-Control gäller för CDN som hanteras av Adobe. Om du använder [kundhanterad CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html#point-to-point-CDN), kan det krävas en annan rubrik beroende på din CDN-leverantör.

  Var försiktig när du anger rubriker för global cachekontroll eller liknande cacherubriker som matchar ett brett register så att de inte tillämpas på innehåll som du måste behålla privat. Överväg att använda flera direktiv för att säkerställa att reglerna tillämpas på ett detaljerat sätt. AEM as a Cloud Service tar därför bort cachehuvudet om det upptäcker att det har tillämpats på det som Dispatcher identifierar som otillgängligt, vilket beskrivs i Dispatcher-dokumentationen. Om du vill tvinga AEM att alltid använda cachelagringshuvuden kan du lägga till **`always`** enligt följande:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  Se till att en fil i `src/conf.dispatcher.d/cache` har följande regel (som finns i standardkonfigurationen):

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* För att förhindra att specifikt innehåll cachas **på CDN**, ställer du in rubriken Cache-Control till *private*. Följande förhindrar till exempel HTML-innehåll under en katalog med namnet **säker** från att cachas vid CDN:

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* HTML-innehåll som är inställt på private cachelagras inte vid CDN, men det kan cachas vid Dispatcher om [Behörighetskänslig cachelagring](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html) är konfigurerat så att endast behöriga användare kan hanteras av innehållet.

  >[!NOTE]
  >Andra metoder, inklusive [Dispatcher-ttl AEM ACS Commons-projekt](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), åsidosätter inte värden.

  >[!NOTE]
  >Dispatcher kan fortfarande cachelagra innehåll enligt sin egen [regler för cachelagring](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Om du vill att innehållet ska vara privat kontrollerar du att det inte cachas av Dispatcher.

### Klientbibliotek (js, css) {#client-side-libraries}

* När du använder AEM biblioteksramverk på klientsidan genereras JavaScript- och CSS-kod på ett sådant sätt att webbläsare kan cachelagra den i oändlighet, eftersom alla ändringar manifesteras som nya filer med en unik sökväg. HTML som refererar till klientbiblioteken skapas med andra ord efter behov så att kunderna kan uppleva nytt innehåll när det publiceras. Cachekontrollen är inställd på&quot;oföränderlig&quot; eller 30 dagar för äldre webbläsare som inte respekterar det oföränderliga&quot; värdet.
* se avsnittet [Bibliotek på klientsidan och versionskonsekvens](#content-consistency) om du vill ha mer information.

### Bilder och allt innehåll som är tillräckligt stort för att lagras i blob {#images}

Standardbeteendet för program som skapats efter mitten av maj 2022 (särskilt för program-ID som är högre än 65000) är att cachelagra som standard, samtidigt som autentiseringskontexten för begäran respekteras. Äldre program (program-ID som är lika med eller lägre än 65000) cache-lagrar inte blobbinnehåll som standard.

I båda fallen kan cachelagringshuvuden åsidosättas på en mer detaljerad nivå i lagret Apache/Dispatcher genom att använda Apache `mod_headers` direktiv, till exempel:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Var försiktig så att du inte cachelagrar för mycket när du ändrar cache-huvudena i Dispatcher-lagret. Läs mer i avsnittet HTML/text [ovan](#html-text). Se även till att resurser som ska hållas privata (i stället för cachelagrade) inte ingår i `LocationMatch` -filter.

JCR-resurser (större än 16 kB) som lagras i blobbutiken hanteras vanligtvis som 302 omdirigeringar av AEM. Dessa omdirigeringar fångas upp och följs av CDN och innehållet levereras direkt från blobbbutiken. Endast en begränsad uppsättning rubriker kan anpassas för dessa svar. Anpassa `Content-Disposition` Du bör använda dispatcherdirektiven på följande sätt:

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

Listan med rubriker som kan anpassas för blobbsvar är:

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### Nytt standardbeteende för cachelagring {#new-caching-behavior}

AEM anger cacherubriker beroende på om cachehuvudet redan har angetts och värdet för begärandetypen. Om ingen cache-kontrollrubrik har angetts cachelagras offentligt innehåll och autentiserad trafik anges till privat. Om en cache-kontrollrubrik anges ändras inte cacherubrikerna.

| Cachekontrollhuvud finns? | Typ av begäran | AEM anger cacherubriker till |
|------------------------------|---------------|------------------------------------------------|
| Nej | public | Cache-Control: public, max-age=600, oföränderlig |
| Nej | autentiserad | Cache-Control: private, max-age=600, oföränderlig |
| Ja | alla | oförändrad |

Även om det inte rekommenderas går det att ändra det nya standardbeteendet så att det följer det äldre beteendet (program-ID som är lika med eller lägre än 65000) genom att ställa in miljövariabeln för Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` till false.

#### Äldre standardbeteende för cachelagring {#old-caching-behavior}

Det AEM lagret cache-lagrar inte blobbinnehåll som standard.

>[!NOTE]
>Ändra det äldre standardbeteendet så att det överensstämmer med det nya beteendet (program-ID som är högre än 65000) genom att ange Cloud Manager-miljövariabeln AEM_BLOB_ENABLE_CACHING_HEADERS till true. Om programmet redan är öppet kontrollerar du att innehållet fungerar som du tänkt dig efter ändringarna.

Nu kan inte bilder i bloblagring som markerats som privata cachelagras hos Dispatcher med [Behörighetskänslig cachelagring](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html). Bilden efterfrågas alltid från AEM ursprung och hanteras om användaren är behörig.

>[!NOTE]
>Andra metoder, inklusive [AEM ACS Commons-projekt](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)åsidosätter inte värdena.

### Andra innehållsfiltyper i nodarkivet {#other-content}

* ingen standardcachelagring
* standard kan inte anges med `EXPIRATION_TIME` variabel som används för filtyperna html/text
* cacheminnets förfallotid kan anges med samma LocationMatch-strategi som beskrivs i avsnittet html/text genom att ange lämplig regex

### Ytterligare optimeringar {#further-optimizations}

* Undvik användning `User-Agent` som en del av `Vary` header. Äldre versioner av standardinställningen Dispatcher (före arkivtypsversion 28) innehöll den och Adobe rekommenderar att du tar bort den genom att följa stegen nedan.
   * Leta reda på värdfilerna i `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Ta bort eller kommentera raden: `Header append Vary User-Agent env=!dont-vary` från alla värdfiler, förutom default.vhost, som är skrivskyddad
* Använd `Surrogate-Control` huvud för att styra CDN-cachning oberoende av webbläsarcachning
* Använd inte [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) och [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) Direktiv som tillåter bakgrundsuppdatering och undviker cachemissar, så att innehållet är snabbt och uppdaterat för användarna.
   * Det finns många sätt att tillämpa dessa direktiv, men att lägga till en 30-minutersperiod `stale-while-revalidate` till alla rubriker för cachekontroll är en bra utgångspunkt.
* Några exempel följer för olika innehållstyper, som kan användas som vägledning när du ställer in egna cachningsregler. Fundera noggrant på och testa dina specifika inställningar och krav:

   * Cachelagra biblioteksresurser för ändringsbara klienter i 12 timmar och bakgrundsuppdatering efter 12 timmar.

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

   * Cachelagra HTML-sidor i fem minuter med bakgrundsuppdatering en timme i webbläsaren och 12 timmar i CDN. Cache-Control-rubriker läggs alltid till så det är viktigt att se till att matchande HTML-sidor under /content/* är avsedda att vara offentliga. Om så inte är fallet bör du överväga att använda en mer specifik regex.

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Cachelagra innehållstjänster/Sling-modellexporterarens json-svar i fem minuter med bakgrundsuppdatering en timme i webbläsaren och 12 timmar i CDN.

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

   * Cachelagra oföränderliga resurser från DAM som bilder och video i 24 timmar och uppdatera bakgrunden efter 12 timmar för att undvika MISS.

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### Analyserar CDN-cacheträffrekvens {#analyze-chr}

Se [självstudiekurs om analys av träffgrad i cache](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/caching/cdn-cache-hit-ratio-analysis.html) om du vill ha information om hur du hämtar CDN-loggar och analyserar webbplatsens cachetipsförhållande med hjälp av en instrumentpanel.

### HEAD beteende vid begäran {#request-behavior}

När en begäran från HEAD tas emot i CDN i Adobe för en resurs som är **not** begäran konverteras och tas emot av Dispatcher- och/eller AEM-instansen som en GET-begäran. Om svaret är tillgängligt kan efterföljande förfrågningar från HEAD besvaras av CDN. Om svaret inte är tillgängligt skickas efterföljande HEAD-begäranden till Dispatcher-instansen, eller AEM-instansen, under en tid som är beroende av `Cache-Control` TTL.

### Parametrar för marknadsföringskampanjer {#marketing-parameters}

Webbplatsadresser innehåller ofta marknadsföringskampanjparametrar som används för att spåra en kampanjs framgång.

För miljöer som skapats i oktober 2023 eller senare kommer CDN att ta bort vanliga marknadsföringsrelaterade frågeparametrar, särskilt de som matchar följande regex-mönster, för att bättre cachelagra begäranden:

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid)$
```

Skicka en supportanmälan om du vill att det här beteendet ska inaktiveras.

För miljöer som skapats före oktober 2023 bör du konfigurera Dispatcher-konfigurationens `ignoreUrlParams` egenskap som [dokumenteras här](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters).

Det finns två möjligheter att ignorera marknadsföringsparametrar. (Där den första är att föredra att ignorera cachebusting via frågeparametrar):

1. Ignorera alla parametrar och tillåt selektivt parametrar som används.
Endast i följande exempel `page` och `product` parametrar ignoreras inte och förfrågningarna vidarebefordras till utgivaren.

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "allow" }
   /0002 { /glob "page" /type "deny" }
   /0003 { /glob "product" /type "deny" }
}
```

1. Tillåt alla parametrar utom marknadsföringsparametrarna. Filen [marketing_query_parameters.any](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.dispatcher.d/cache/marketing_query_parameters.any) definierar en lista med vanliga marknadsföringsparametrar som kommer att ignoreras. Adobe kommer inte att uppdatera den här filen. Den kan utökas av användare beroende på vilka marknadsföringsleverantörer de har.

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   $include "../cache/marketing_query_parameters.any"
}
```


## Invalidering av Dispatcher-cache {#disp}

I allmänhet behöver du inte göra Dispatcher-cachen ogiltig. Du bör i stället förlita dig på att Dispatcher uppdaterar sin cache när innehåll publiceras om och att CDN respekterar förfallorubriker för cache.

### Invalidering av Dispatcher-cache under aktivering/inaktivering {#cache-activation-deactivation}

Precis som i tidigare versioner av AEM rensas innehållet från Dispatcher-cachen när du publicerar eller avpublicerar sidor. Om ett problem med cachelagring misstänks bör du publicera om sidorna och se till att det finns ett virtuellt värdsystem som matchar `ServerAlias` localhost, vilket krävs för invalidering av Dispatcher-cache.

>[!NOTE]
>För att Dispatcher ska bli ogiltig måste du se till att begäranden från&quot;127.0.0.1&quot;,&quot;localhost&quot;, &quot;\*.local&quot;, &quot;\*.adobeaemcloud.com&quot; och &quot;\*.adobeaemcloud.net&quot; matchas och hanteras av en värdkonfiguration så att begäran kan hanteras. Du kan göra detta genom att globalt matcha &quot;*&quot; i en konfiguration som fångar upp alla värden enligt mönstret i referensen [AEM](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost). Du kan också se till att den tidigare nämnda listan fångas av någon av värdarna.

När publiceringsinstansen tar emot en ny version av en sida eller resurs från författaren, används justeringsagenten för att göra lämpliga sökvägar ogiltiga i dess Dispatcher. Den uppdaterade sökvägen tas bort från Dispatcher-cachen, tillsammans med överordnade sökvägar, upp till en nivå (du kan konfigurera den här nivån med [statusfilernivå](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Explicit ogiltigförklaring av Dispatcher-cachen {#explicit-invalidation}

Adobe rekommenderar att du använder standardcache-huvuden för att styra innehållets leveranslivscykel. Om det behövs kan du emellertid göra innehållet ogiltigt direkt i Dispatcher.

Följande lista innehåller scenarier där du kanske vill göra cachen ogiltig (men avlyssna när ogiltigförklaringen har slutförts):

* Efter publicering av innehåll som upplevelsefragment eller innehållsfragment blir publicerat och cachelagrat innehåll som refererar till dessa element ogiltigt.
* Meddela ett externt system när refererade sidor har ogiltigförklarats.

Det finns två sätt att göra cacheminnet explicit ogiltigt:

* Det bästa sättet är att använda Sling Content Distribution (SCD) från författaren.
* Den andra metoden är att använda replikerings-API:t för att anropa replikeringsagenten för rensning av publiceringsutskickare.

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
       <li><p><strong>Från författarnivå</strong> - Tar bort innehåll och gör cachen ogiltig (om den aktiveras från AEM författarnivå i publiceringsagenten).</p>
           <p><strong>Från publiceringsnivå</strong> - Gör bara cachen oskadad (om den aktiveras från AEM publiceringsnivå på agenten för tömning eller tömning enbart på resurs).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

De två åtgärder som är direkt relaterade till cacheogiltigförklaring är API-inaktivering för Sling Content Distribution (SCD) och replikerings-API.

I tabellen kan du även se följande:

* SCD API behövs när varje händelse måste garanteras, till exempel synkronisering med ett externt system som kräver korrekt kunskap. Om det finns en publiceringsnivåuppskalningshändelse vid tidpunkten för ogiltigförklaringsanropet, utlöses en extra händelse när varje ny publiceringsnivå bearbetar ogiltigförklaringen.

* Det är inte vanligt att använda replikerings-API:t, men det kan användas om utlösaren för att göra cachen ogiltig kommer från publiceringsskiktet och inte från författarskiktet. Den här metoden kan vara användbar om Dispatcher TTL har konfigurerats.

Sammanfattningsvis, om du vill göra Dispatcher-cachen ogiltig, rekommenderar vi att du använder SCD API-åtgärden Ovalidate från Författare. Du kan också lyssna efter händelsen så att du sedan kan utlösa ytterligare åtgärder längre fram.

### Sling Content Distribution (SCD) {#sling-distribution}

>[!NOTE]
>När du använder instruktionerna nedan testar du den anpassade koden i en AEM Cloud Service Dev-miljö och inte lokalt.

När du använder SCD-åtgärden från författaren ser implementeringsmönstret ut så här:

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

* (Valfritt) Lyssna efter en händelse som reflekterar resursen som ogiltigförklaras för alla Dispatcher-instanser:


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
>CDN i Adobe rensas inte när Dispatcher ogiltigförklaras. CDN som hanteras av Adobe respekterar TTL:er och behöver därför inte tömmas.

### Replikerings-API {#replication-api}

Nedan visas implementeringsmönstret när åtgärden för inaktivering av replikerings-API används:

1. Anropa replikerings-API:t på publiceringsnivån för att utlösa replikeringsagenten för rensning av publiceringsdispatcher.

Slutpunkten för rensningsagenten kan inte konfigureras utan är i stället förkonfigurerad så att den pekar på Dispatcher, matchad med publiceringstjänsten som körs tillsammans med tömningsagenten.

Flush-agenten kan oftast aktiveras av anpassad kod som baseras på OSGi-händelser eller arbetsflöden.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
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

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## Bibliotek på klientsidan och versionskonsekvens {#content-consistency}

Sidorna består av HTML, JavaScript, CSS och bilder. Vi rekommenderar [Klientbibliotek (clientlibs) ramverk](/help/implementing/developing/introduction/clientlibs.md) om du vill importera JavaScript- och CSS-resurser till HTML-sidor, med hänsyn till beroenden mellan JS-bibliotek.

Med clientlibs Framework får du automatisk versionshantering. Det innebär att utvecklare kan checka in ändringar i JS-bibliotek i källkontrollen och att den senaste versionen blir tillgänglig när kunden publicerar sin release. Utan det här arbetsflödet måste utvecklare ändra HTML manuellt med referenser till den nya versionen av biblioteket, vilket är särskilt betungande om samma bibliotek delar många HTML-mallar.

När de nya versionerna av biblioteken släpps i produktion uppdateras de refererande HTML-sidorna med nya länkar till de uppdaterade biblioteksversionerna. När webbläsarcachen har upphört att gälla för en viss HTML-sida behöver du inte bekymra dig om att de gamla biblioteken läses in från webbläsarens cacheminne. Orsaken är att den uppdaterade sidan (från AEM) nu garanterat refererar till de nya versionerna av biblioteken. Det vill säga att en uppdaterad HTML-sida innehåller alla de senaste biblioteksversionerna.

Mekanismen bakom den här funktionen är en serialiserad hash som läggs till i klientbibliotekslänken. Den ser till att webbläsaren har en unik versionsadress för att cachelagra CSS/JS. Den serialiserade hashen uppdateras bara när innehållet i klientbiblioteket ändras. Det innebär att om det inte sker några ändringar (det vill säga om klientbibliotekets underliggande css/js ändras) även om det finns en ny distribution, förblir referensen densamma. Det säkerställer i sin tur färre avbrott i webbläsarens cache.

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

Så här aktiverar du strikt versionshantering av klientlib i den lokala SDK QuickStart:

1. Navigera till OSGi Configuration Manager `<host>/system/console/configMgr`
1. Hitta OSGi Config för Adobe Granite HTML Library Manager:
   * Markera kryssrutan så att Strikta versionshantering aktiveras
   * I fältet **Cachenyckel på lång klientsida**, anger värdet för /.*;hash
1. Spara ändringarna. Det är inte nödvändigt att spara den här konfigurationen i källkontrollen eftersom AEM as a Cloud Service automatiskt aktiverar den här konfigurationen i miljö med dev, stage och production.
1. När innehållet i klientbiblioteket ändras skapas en ny hash-nyckel och HTML-referensen uppdateras.
