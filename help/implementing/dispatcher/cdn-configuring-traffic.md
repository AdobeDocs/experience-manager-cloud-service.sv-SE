---
title: Konfigurera trafik vid leveransnätverket
description: Lär dig hur du konfigurerar CDN-trafik genom att deklarera regler och filter i en konfigurationsfil och distribuera dem till CDN med hjälp av Cloud Manager Configuration Pipeline.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Konfigurera trafik vid leveransnätverket {#cdn-configuring-cloud}

AEM as a Cloud Service har en samling funktioner som kan konfigureras på [CDN som hanteras av Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) lager som ändrar typen av inkommande eller utgående svar. Följande regler, som beskrivs i detalj på den här sidan, kan deklareras för att uppnå följande beteende:

* [Begär omformningar](#request-transformations) - ändra aspekter av inkommande begäranden, inklusive rubriker, sökvägar och parametrar.
* [Svarsomvandlingar](#response-transformations) - ändra rubriker som är på väg tillbaka till klienten (till exempel en webbläsare).
* [Omdirigeringar på klientsidan](#client-side-redirectors) - utlöser en omdirigering till webbläsaren. Den här funktionen är ännu inte tillgänglig för GA, men för tidiga användare.
* [Väljare för ursprung](#origin-selectors) - proxy till en annan bakgrund.

CDN kan även konfigurera trafikfilterregler (inklusive WAF), som styr vilken trafik som tillåts eller nekas av CDN. Den här funktionen har redan släppts och du kan läsa mer om den i [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) sida.

Om CDN inte kan kontakta sitt ursprung kan du dessutom skriva en regel som refererar till en egen felsida (som sedan återges). Läs mer om detta i [Konfigurera CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md) artikel.

Alla dessa regler, som deklareras i en konfigurationsfil i källkontrollen, distribueras med [Konfigurationspipeline för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Tänk på att den kumulativa storleken på konfigurationsfilen, inklusive trafikfilterregler, inte får överstiga 100 kB.

## Utvärderingsordning {#order-of-evaluation}

De olika funktioner som nämns ovan utvärderas i följande sekvens:

![bild](/help/implementing/dispatcher/assets/order.png)

## Inställningar {#initial-setup}

Innan du kan konfigurera trafik på leveransnätverket måste du göra följande:

* Skapa den här mappen och filstrukturen i den översta mappen i Git-projektet:

```
config/
     cdn.yaml
```

* The `cdn.yaml` konfigurationsfilen ska innehålla både metadata och reglerna som beskrivs i exemplen nedan. The `kind` parametern ska anges till `CDN` och versionen bör anges till schemaversionen, som för närvarande är `1`.

* Skapa en riktad distributionskonfigurationspipeline i Cloud Manager. Se [konfigurera produktionspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) och [konfigurera icke-produktionsrörledningar](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

**Anteckningar**

* De lokala lagringsplatserna stöder för närvarande inte konfigurationsflödet.
* Du kan använda `yq` för att lokalt validera YAML-formateringen i konfigurationsfilen (till exempel `yq cdn.yaml`).

## Syntax {#configuration-syntax}

Regeltyperna i avsnitten nedan har en gemensam syntax.

En regel refereras av ett namn, en villkorlig&quot;when-sats&quot; och åtgärder.

När-satsen avgör om en regel ska utvärderas, baserat på egenskaper som domän, sökväg, frågesträngar, rubriker och cookies. Syntaxen är densamma för alla regeltyper. Mer information finns i [Villkorsstrukturavsnitt](/help/security/traffic-filter-rules-including-waf.md#condition-structure) i artikeln Traffic Filter Rules.

Detaljerna för åtgärdsnoden skiljer sig åt mellan olika regeltyper och beskrivs i de enskilda avsnitten nedan.

## Begär omformningar {#request-transformations}

Regler för omformning av begäranden gör att du kan ändra inkommande begäranden. Reglerna har stöd för att ställa in, ta bort och ändra sökvägar, frågeparametrar och rubriker (inklusive cookies) baserat på olika matchningsvillkor, inklusive reguljära uttryck. Du kan också ange variabler som du senare kan referera till i utvärderingssekvensen.

Användningsexempel varierar och inkluderar URL-omskrivningar för att förenkla programmet eller mappa äldre URL-adresser.

Som vi nämnt tidigare finns det en storleksbegränsning för konfigurationsfilen, så organisationer med större krav bör definiera regler i `apache/dispatcher` lager.

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
```

**Åtgärder**

I tabellen nedan beskrivs de tillgängliga åtgärderna.

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **set** | (reqProperty eller reqHeader eller queryParam eller reqCookie), värde | Anger en angiven begärandeparameter (endast egenskapen path stöds), eller begäranhuvud, frågeparameter eller cookie, till ett givet värde. |
|     | var, värde | Ställer in en angiven request-egenskap på ett givet värde. |
| **unset** | reqProperty | Tar bort en angiven begärandeparameter (endast egenskapen path stöds), eller begäranhuvud, frågeparameter eller cookie, till ett givet värde. |
|         | var | Tar bort en angiven variabel. |
|         | queryParamMatch | Tar bort alla frågeparametrar som matchar ett angivet reguljärt uttryck. |
| **omforma** | op:replace, (reqProperty eller reqHeader eller queryParam eller reqCookie), match, replace | Ersätter en del av parametern request (endast egenskapen path stöds), eller request header, query parameter eller cookie med ett nytt värde. |
|              | op:tolower, (reqProperty eller reqHeader eller queryParam eller reqCookie) | Ställer in parametern request (endast egenskapen path stöds), huvudet request, parametern query eller cookie till dess gemener. |

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

Du kan ange variabler under begärandeomformningen och sedan referera till dem senare i utvärderingssekvensen. Se [utvärderingsordning](#order-of-evaluation) för mer information.

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

## Svarsomvandlingar {#response-transformations}

Med reglerna för svarsomvandling kan du ange och ta bort rubriker för CDN:ens utgående svar. Se även exemplet ovan för att referera till en variabel som tidigare angetts i en omformningsregel för begäran.

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
 
      # Example: Multi-action on response header
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
```

**Åtgärder**

I tabellen nedan beskrivs de tillgängliga åtgärderna.

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **set** | reqHeader, värde | Ställer in en angiven rubrik på ett givet värde i svaret. |
| **unset** | respHeader | Tar bort en angiven rubrik från svaret. |

## Väljare för ursprung {#origin-selectors}

Du kan använda det AEM CDN för att dirigera trafik till olika serverdelar, inklusive program som inte kommer från Adobe (kanske per sökväg eller underdomän).

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
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # useCache: false
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
|     | useCache (valfritt, standardvärdet är true) | Flagga om cachelagring ska användas för begäranden som matchar den här regeln. |

**Original**

Anslutningar till originalen är endast SSL och använder port 443.

| Egenskap | Betydelse |
|------------------|--------------------------------------|
| **name** | Namn som kan refereras av &quot;action.originName&quot;. |
| **domän** | Domännamn som används för att ansluta till den anpassade serverdelen. Det används också för SSL SNI och validering. |
| **ip** (tillval, stöd för iv4 och ipv6) | Om den anges används den för att ansluta till serverdelen i stället för till &quot;domän&quot;. Stilla &quot;domän&quot; används för SSL SNI och validering. |
| **forwardHost** (valfritt, standardvärdet är false) | Om värdet är true skickas &quot;Host&quot;-huvudet från klientbegäran till serverdelen, annars skickas &quot;domain&quot;-värdet i &quot;Host&quot;-huvudet. |
| **forwardCookie** (valfritt, standardvärdet är false) | Om värdet är true skickas&quot;Cookie&quot;-huvudet från klientbegäran till serverdelen, annars tas Cookie-huvudet bort. |
| **forwardAuthorization** (valfritt, standardvärdet är false) | Om värdet är true skickas auktoriseringshuvudet från klientbegäran till serverdelen, annars tas auktoriseringshuvudet bort. |
| **timeout** (valfritt, i sekunder är standardvärdet 60) | Antal sekunder som CDN ska vänta på att en backend-server ska leverera den första byten av en HTTP-svarstext. Det här värdet används också som en tidsgräns mellan byte till serverdelsservern. |

## Omdirigeringar på klientsidan {#client-side-redirectors}

>[!NOTE]
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i programmet för tidig adopter skickar du e-post `aemcs-cdn-config-adopter@adobe.com` och beskriva hur ni använder er.

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
  experimental_redirects:
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
| **omdirigera** | plats | Värde för rubriken Plats. |
|     | status (valfritt, standardvärdet är 301) | HTTP-status som ska användas i omdirigeringsmeddelandet, 301 som standard, är de tillåtna värdena: 301, 302, 303, 307, 308. |
