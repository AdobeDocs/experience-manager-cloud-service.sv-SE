---
title: Konfigurera trafik vid leveransnätverket
description: Lär dig hur du konfigurerar CDN-trafik genom att deklarera regler och filter i en konfigurationsfil och distribuera dem till CDN med hjälp av Cloud Manager Configuration Pipeline.
feature: Dispatcher
source-git-commit: 0a0c9aa68b192e8e2a612f50a58ba5f9057c862d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---


# Konfigurera trafik vid leveransnätverket {#cdn-configuring-cloud}

>[!NOTE]
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i programmet för tidig adopter skickar du e-post `aemcs-cdn-config-adopter@adobe.com` och beskriva hur ni använder er.

AEM as a Cloud Service har en samling funktioner som kan konfigureras på [CDN som hanteras av Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) lager som ändrar typen av inkommande eller utgående svar. Följande regler, som beskrivs i detalj på den här sidan, kan deklareras för att uppnå följande beteende:

* [Begär omformningar](#request-transformations) - ändra aspekter av inkommande begäranden, inklusive rubriker, sökvägar och parametrar.
* [Svarsomvandlingar](#response-transformations) - ändra rubriker som är på väg tillbaka till klienten (till exempel en webbläsare).
* [Redirectors på klientsidan](#client-side-redirectors) - utlöser en omdirigering till webbläsaren.
* [Väljare för ursprung](#origin-selectors) - proxy till en annan bakgrund.

CDN kan även konfigurera trafikfilterregler (inklusive WAF), som styr vilken trafik som tillåts eller nekas av CDN. Den här funktionen har redan släppts och du kan läsa mer om den i [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) sida.

Om CDN inte kan kontakta sitt ursprung kan du dessutom skriva en regel som refererar till en egen felsida (som sedan återges). Läs mer om detta i [Konfigurera CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md) artikel.

Alla dessa regler, som deklareras i en konfigurationsfil i källkontrollen, distribueras med [Konfigurationspipeline för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Tänk på att den sammanlagda storleken på konfigurationsfilen inte får överstiga 100 kB.

## Utvärderingsordning {#order-of-evaluation}

De olika funktioner som nämns ovan utvärderas i följande sekvens:

![bild](/help/implementing/dispatcher/assets/order.png)

## Inställningar {#initial-setup}

Innan du kan konfigurera trafik på leveransnätverket måste du göra följande:

* Skapa först den här mapp- och filstrukturen i den översta mappen i Git-projektet:

```
config/
     cdn.yaml
```

* För det andra `cdn.yaml` konfigurationsfilen ska innehålla både metadata och reglerna som beskrivs i exemplen nedan.

## Begär omformningar {#request-transformations}

Regler för omformning av begäranden gör att du kan ändra inkommande begäranden. Reglerna har stöd för att ställa in, ta bort och ändra sökvägar, frågeparametrar och rubriker (inklusive cookies) baserat på olika matchningsvillkor, inklusive reguljära uttryck. Du kan också ange variabler som du senare kan referera till i utvärderingssekvensen.

Användningsexempel varierar och inkluderar URL-omskrivningar för att förenkla programmet eller mappa äldre URL-adresser.

Som vi nämnt tidigare finns det en storleksbegränsning för konfigurationsfilen, så organisationer med större krav bör definiera regler i `apache/dispatcher` lager.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:  
  experimental_requestTransformations:
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
 
      - name: set-query-param-rule
        when:
          reqProperty: path
          equals: /set-query-param
        actions:
          - type: set
            queryParam: someParam
            value: someValue
 
      - name: unset-query-param-rule
        when:
          reqProperty: path
          equals: /unset-query-param
        actions:
          - type: unset
            queryParam: someParam
 
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
 
      - name: set-req-cookie-rule
        when:
          reqProperty: path
          equals: /set-req-cookie
        actions:
          - type: set
            reqCookie: someParam
            value: someValue
 
      - name: unset-req-cookie-rule
        when:
          reqProperty: path
          equals: /unset-req-cookie
        actions:
          - type: unset
            reqCookie: someParam
 
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some value
 
      - name: unset-variable-rule
        when:
          reqProperty: path
          equals: /unset-variable
        actions:
          - type: unset
            var: some_var_name
 
      - name: replace-segment
        when:
          reqProperty: path
          like: /replace-segment/*
        actions:
          - type: replace
            reqProperty: path
            match: /replace-segment/
            value: /segment-was-replaced/
 
      - name: replace-extension
        when:
          reqProperty: path
          like: /replace-extension/*.html
        actions:
          - type: replace
            reqProperty: path
            match: \.html
            value: ''
 
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
```

**Åtgärder**

I tabellen nedan beskrivs de tillgängliga åtgärderna.

| Namn | Egenskaper | Betydelse |
|-----------|--------------------------|-------------|
| **set** | reqHeader, värde | Ställer in en angiven rubrik på ett givet värde. |
|     | queryParam, värde | Ställer in en angiven frågeparameter på ett givet värde. |
|     | reqCookie, värde | Anger en angiven cookie till ett angivet värde. |
|     | var, värde | Ställer in en angiven variabel på ett givet värde. |
| **unset** | reqHeader | Tar bort ett angivet huvud. |
|         | queryParam | Tar bort en angiven frågeparameter. |
|         | reqCookie | Tar bort en angiven cookie. |
|         | var | Tar bort en angiven variabel. |
|         | queryParamMatch | Tar bort alla frågeparametrar som matchar ett angivet reguljärt uttryck. |
| **ersätt** | reqProperty, match, value | Ersätter en del av egenskapen request med ett nytt värde. För närvarande stöds bara egenskapen &quot;path&quot;. |

### Variabel {#variables}

Du kan ange variabler under begärandeomformningen och sedan referera till dem senare i utvärderingssekvensen. Se [utvärderingsordning](#order-of-evaluation) för mer information.

Konfigurationsexempel:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:   
  experimental_requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value
 
  experimental_responseTransformations:
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
  experimental_responseTransformations:
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
  experimental_originSelectors:
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

## Redirectors på klientsidan {#client-side-redirectors}

Du kan använda omdirigeringsregler på klientsidan för 301, 302 och liknande omdirigeringar på klientsidan. Om en regel matchar svarar CDN med en statusrad som innehåller statuskoden och meddelandet (till exempel HTTP/1.1 301 Flyttad permanent), samt platshuvuduppsättningen.

Både absoluta och relativa platser med fasta värden tillåts.

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
