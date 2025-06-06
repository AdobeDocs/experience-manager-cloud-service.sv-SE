---
title: Konfigurera trafik vid leveransnätverket
description: Lär dig hur du konfigurerar CDN-trafik genom att deklarera regler och filter i en konfigurationsfil och distribuera dem till CDN med hjälp av en Cloud Manager-konfigurationspipeline.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: ab855192e4b60b25284b19cc0e3a8e9da5a7409c
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 0%

---


# Konfigurera trafik vid leveransnätverket {#cdn-configuring-cloud}

AEM as a Cloud Service erbjuder en samling funktioner som kan konfigureras på lagret [Adobe-hanterad CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) som ändrar typen av inkommande eller utgående svar. Följande regler, som beskrivs i detalj på den här sidan, kan deklareras för att uppnå följande beteende:

* [Begär omformningar](#request-transformations) - ändra aspekter av inkommande begäranden, inklusive huvuden, sökvägar och parametrar.
* [Svarsomvandlingar](#response-transformations) - ändra huvuden som är på väg tillbaka till klienten (till exempel en webbläsare).
* [Omdirigering på serversidan](#server-side-redirectors) - utlöser en omdirigering av webbläsaren.
* [Ursprungsväljare](#origin-selectors) - proxy till en annan ursprunglig serverdel.

CDN kan även konfigurera trafikfilterregler (inklusive WAF), som styr vilken trafik som tillåts eller nekas av CDN. Den här funktionen har redan släppts och du kan läsa mer om den på sidan [Trafikfilterregler, inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md).

Om CDN inte kan kontakta sitt ursprung kan du dessutom skriva en regel som refererar till en egen felsida (som sedan återges). Läs mer om detta i artikeln [Konfigurera CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md).

Alla dessa regler, som deklareras i en konfigurationsfil i källkontrollen, distribueras med Cloud Manager [config-pipeline](/help/operations/config-pipeline.md). Tänk på att den kumulativa storleken på konfigurationsfilen, inklusive trafikfilterregler, inte får överstiga 100 kB.

## Utvärderingsordning {#order-of-evaluation}

De olika funktioner som nämns ovan utvärderas i följande sekvens:

![Utvärderingsordning](/help/implementing/dispatcher/assets/order.png)

## Inställningar {#initial-setup}

Innan du kan konfigurera trafik på leveransnätverket måste du göra följande:

1. Skapa en fil med namnet `cdn.yaml` eller liknande, och referera till de olika konfigurationsfragmenten i avsnitten nedan.

   Alla fragment har dessa gemensamma egenskaper, som beskrivs under [Konfigurera pipeline](/help/operations/config-pipeline.md#common-syntax). Egenskapsvärdet `kind` ska vara *CDN* och egenskapen `version` ska vara *1*.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   ```

1. Placera filen någonstans under en mapp på den översta nivån med namnet *config* eller liknande, enligt beskrivningen under [Konfigurera pipeline](/help/operations/config-pipeline.md#folder-structure).

1. Skapa en konfigurationspipeline i Cloud Manager, enligt beskrivningen under [Konfigurera pipeline](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Distribuera konfigurationen.

## Regelsyntax {#configuration-syntax}

Regeltyperna i avsnitten nedan har en gemensam syntax.

En regel refereras av ett namn, en villkorlig&quot;when-sats&quot; och åtgärder.

När-satsen avgör om en regel ska utvärderas utifrån egenskaper som domän, sökväg, frågesträngar, rubriker och cookies. Syntaxen är densamma för alla regeltyper. Mer information finns i avsnittet [Villkorsstruktur](/help/security/traffic-filter-rules-including-waf.md#condition-structure) i artikeln Regler för trafikfilter.

Detaljerna för åtgärdsnoden skiljer sig åt mellan olika regeltyper och beskrivs i de enskilda avsnitten nedan.

I konfigurationsreglerna kan du referera till hemligheter som definierats som miljövariabler (se [Konfigurationshemligheter](/help/implementing/dispatcher/cdn-credentials-authentication.md)).

## Begär omformningar {#request-transformations}

Regler för omformning av begäranden gör att du kan ändra inkommande begäranden. Reglerna har stöd för att ställa in, ta bort och ändra sökvägar, frågeparametrar och rubriker (inklusive cookies) baserat på olika matchningsvillkor, inklusive reguljära uttryck. Du kan också ange variabler som du senare kan referera till i utvärderingssekvensen.

Användningsexempel varierar och inkluderar URL-omskrivningar för att förenkla programmet eller mappa äldre URL-adresser.

Som vi nämnt tidigare finns det en storleksgräns för konfigurationsfilen, så organisationer med större krav bör definiera regler i lagret `apache/dispatcher`.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$
      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$
      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'
      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: \.html$
            replacement: ""
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: forwarded_host
            value:
              reqHeader: x-forwarded-host
```

**Åtgärder**

I tabellen nedan beskrivs de tillgängliga åtgärderna.

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **uppsättning** | reqProperty, värde | Anger en angiven begärandeparameter (endast egenskapen &quot;path&quot; stöds) |
|     | reqHeader, värde | Anger ett angivet begärandehuvud till ett angivet värde. |
|     | queryParam, värde | Ställer in en angiven frågeparameter på ett givet värde. |
|     | reqCookie, värde | Anger en angiven begärandecookie till ett angivet värde. |
|     | logProperty, värde | Ställer in en angiven CDN-loggegenskap på ett givet värde. |
|     | var, värde | Ställer in en angiven variabel på ett givet värde. |
| **unset** | reqProperty | Tar bort en angiven begärandeparameter (endast egenskapen &quot;path&quot; stöds) |
|     | reqHeader, värde | Tar bort ett angivet begärandehuvud. |
|     | queryParam, värde | Tar bort en angiven frågeparameter. |
|     | reqCookie, värde | Tar bort en angiven cookie. |
|     | logProperty, värde | Tar bort en angiven CDN-loggegenskap. |
|     | var | Tar bort en angiven variabel. |
|     | queryParamMatch | Tar bort alla frågeparametrar som matchar ett angivet reguljärt uttryck. |
|     | queryParamDoesNotMatch | Tar bort alla frågeparametrar som inte matchar ett angivet reguljärt uttryck. |
| **omforma** | op:replace, (reqProperty eller reqHeader eller queryParam eller reqCookie eller var), match, replace | Ersätter en del av parametern request (endast egenskapen path stöds), huvudet request, parametern query, cookie, eller variabeln med ett nytt värde. |
|              | op:tolower, (reqProperty eller reqHeader eller queryParam eller reqCookie eller var) | Ställer in parametern request (endast egenskapen path stöds), huvudet request, parametern query, cookie, eller variabeln till dess gemener. |

Ersätt funktionsmakron har stöd för hämtningsgrupper, vilket visas nedan:

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

Åtgärder kan knytas ihop. Till exempel:

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### Variabel {#variables}

Du kan ange variabler under begärandeomformningen och sedan referera till dem senare i utvärderingssekvensen. Se [utvärderingsordningen](#order-of-evaluation) för mer information.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value

  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

### Egenskapen Log {#logproperty}

Du kan lägga till egna loggegenskaper i CDN-loggarna med hjälp av omvandlingar av begäranden och svar.

Konfigurationsexempel:

```
requestTransformations:
  rules:
    - name: log-on-request
      when: "*"
      actions:
        - type: set
          logProperty: forwarded_host
          value:
            reqHeader: x-forwarded-host
responseTransformations:
  rules:
    - name: log-on-response
      when: '*'
      actions:
        - type: set
          logProperty: cache_control
          value:
            respHeader: cache-control
```

Exempel på logg:

```
{
"timestamp": "2025-03-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "",
"forwarded_host": "example.com",
"cache_control": "max-age=300"
}
```

## Svarsomvandlingar {#response-transformations}

Med reglerna för svarsomvandling kan du ange och ta bort rubriker, cookies och status för CDN:ens utgående svar. Se även exemplet ovan för att referera till en variabel som tidigare angetts i en omformningsregel för begäran.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header
      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'
      - name: set-response-cookie-with-attributes-as-object
        when: '*'
        actions:
          - type: set
            respCookie: first-name
            value: first-value
            attributes:
              expires: '2025-08-29T10:00:00'
              domain: example.com
              path: /some-path
              secure: true
              httpOnly: true
              extension: ANYTHING
      - name: unset-response-cookie
        when: '*'
        actions:
          - type: unset
            respCookie: third-name
```

**Åtgärder**

I tabellen nedan beskrivs de tillgängliga åtgärderna.

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **uppsättning** | respProperty, värde | Anger en svarsegenskap. Stöder bara egenskapen &quot;status&quot; för att ange statuskoden. |
|     | respHeader, värde | Anger ett angivet svarshuvud till ett angivet värde. |
|     | respCookie, attribut (förfaller, domän, sökväg, säker, httpOnly, tillägg), värde | Ställer in en angiven begärandecookie med specifika attribut för ett givet värde. |
|     | logProperty, värde | Ställer in en angiven CDN-loggegenskap på ett givet värde. |
|     | var, värde | Ställer in en angiven variabel på ett givet värde. |
| **unset** | respHeader | Tar bort en angiven rubrik från svaret. |
|     | respCookie, värde | Tar bort en angiven cookie. |
|     | logProperty, värde | Tar bort en angiven CDN-loggegenskap. |
|     | var | Tar bort en angiven variabel. |

## Väljare för ursprung {#origin-selectors}

Du kan använda AEM CDN för att dirigera trafik till olika serverdelar, inklusive program som inte kommer från Adobe (kanske per sökväg eller underdomän).

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true
        # forwardAuthorization: true
        # timeout: 20
```

**Åtgärder**

Tabellen nedan förklarar den tillgängliga åtgärden.

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **selectOrigin** | originName | Namnet på ett av de definierade originalen. |
|     | skipCache (valfritt, standardvärdet är false) | Flagga om cachelagring ska användas för begäranden som matchar den här regeln. Som standard cachelagras svar enligt svarscachningshuvudet (t.ex. Cache-Control eller Expires) |

**Original**

Anslutningar till originalen är endast SSL och använder port 443.

| Egenskap | Betydelse |
|------------------|--------------------------------------|
| **namn** | Namn som kan refereras av &quot;action.originName&quot;. |
| **domän** | Domännamn som används för att ansluta till den anpassade serverdelen. Det används också för SSL SNI och validering. |
| **ip** (valfritt, stöd för iv4 och ipv6) | Om den anges används den för att ansluta till serverdelen i stället för till &quot;domän&quot;. Stilla &quot;domän&quot; används för SSL SNI och validering. |
| **forwardHost** (valfritt, standardvärdet är false) | Om värdet är true skickas &quot;Host&quot;-huvudet från klientbegäran till serverdelen, annars skickas &quot;domain&quot;-värdet i &quot;Host&quot;-huvudet. |
| **forwardCookie** (valfritt, standardvärdet är false) | Om värdet är true skickas&quot;Cookie&quot;-huvudet från klientbegäran till serverdelen, annars tas Cookie-huvudet bort. |
| **forwardAuthorization** (valfritt, standardvärdet är false) | Om värdet är true skickas auktoriseringshuvudet från klientbegäran till serverdelen, annars tas auktoriseringshuvudet bort. |
| **timeout** (valfritt, i sekunder är standardvärdet 60) | Antal sekunder som CDN ska vänta på att en backend-server ska leverera den första byten av en HTTP-svarstext. Det här värdet används också som en tidsgräns mellan byte till serverdelsservern. |

### Proxyserver till Edge Delivery Services {#proxying-to-edge-delivery}

Det finns scenarier där ursprungsväljare ska användas för att dirigera trafik via AEM Publish till AEM Edge Delivery Services:

* Visst innehåll levereras av en domän som hanteras av AEM Publish, medan annat innehåll från samma domän levereras av Edge Delivery Services
* Innehåll som levereras av Edge Delivery Services kan utnyttja regler som distribueras via konfigurationsflödet, inklusive trafikfilterregler eller begäran-/svarsomvandlingar

Här är ett exempel på en väljarregel för origo som kan åstadkomma detta:

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
> Eftersom det hanterade CDN-nätverket för Adobe används, måste du konfigurera push-ogiltigförklaring i **hanterat** läge genom att följa Edge Delivery Services [Setup invalidation documentation](https://www.aem.live/docs/byo-dns#setup-push-invalidation).


## Serveromdirigeringar {#server-side-redirectors}

Du kan använda omdirigeringsregler på klientsidan för 301, 302 och liknande omdirigeringar på klientsidan. Om en regel matchar svarar CDN med en statusrad som innehåller statuskoden och meddelandet (till exempel HTTP/1.1 301 Flyttad permanent), samt platshuvuduppsättningen.

Både absoluta och relativa platser med fasta värden tillåts.

Tänk på att den kumulativa storleken på konfigurationsfilen, inklusive trafikfilterregler, inte får överstiga 100 kB.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **omdirigering** | plats | Värde för rubriken Plats. |
|     | status (valfritt, standardvärdet är 301) | HTTP-status som ska användas i omdirigeringsmeddelandet, 301 som standard, är de tillåtna värdena: 301, 302, 303, 307, 308. |

Platserna för en omdirigering kan antingen vara stränglitteraler (t.ex. https://www.example.com/page) eller resultatet av en egenskap (t.ex. path) som kan omformas, med följande syntax:

```
redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: url
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
