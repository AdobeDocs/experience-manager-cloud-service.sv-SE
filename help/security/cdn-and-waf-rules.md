---
title: Konfigurera trafikfilterregler med WAF-regler
description: Använd trafikfilterregler med WAF-regler för att filtrera trafik
source-git-commit: ce7b6922f92208c06f85afe85818574bf2bc8f6d
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 0%

---


# Konfigurera trafikfilterregler med WAF-regler för att filtrera trafik {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i det pågående programmet för tidiga användare skickar du e-post **aemcs-waf-adopter@adobe.com**, inklusive namnet på organisationen och sammanhanget om ditt intresse för funktionen.

Adobe försöker mildra attacker mot kundwebbplatser, men det kan vara användbart att proaktivt filtrera trafik som matchar vissa mönster så att skadlig trafik inte når applikationen. Möjliga strategier är:

* Lagermoduler i Apache som `mod_security`
* Konfigurera trafikfilterregler som distribueras till CDN via Cloud Managers konfigurationsflöde

I den här artikeln beskrivs hur trafikfilterregler används. De flesta av dessa regler blockerar eller tillåter förfrågningar baserat på begäranegenskaper och begäranrubriker, inklusive IP, sökvägar och användaragent. Dessa regler kan konfigureras av alla AEM as a Cloud Service webbplatser och Forms-kunder.

Kunder som licensierar WAF-tillägget (Web Application Firewall) kan också konfigurera ytterligare en kategori med regler som kallas &quot;WAF-trafikfilterregler&quot; (eller WAF-regler för kort). Dessa WAF-regler blockerar förfrågningar som matchar olika mönster som är kända för att vara associerade med skadlig trafik. Kontakta ditt Adobe-kontoteam om du vill ha mer information om hur du kan licensiera den här nya funktionen. Observera att ingen ytterligare licens krävs under det tidiga adopterprogrammet.

Trafikfilterregler kan distribueras till alla typer av molnmiljöer (RDE, dev, stage, prod) i produktionsprogram (icke-sandbox).

## Inställningar {#setup}

1. Skapa först följande mapp- och filstruktur för mappen på den översta nivån i Git:

   ```
   config/
        cdn/
           cdn.yaml
   ```

1. `cdn.yaml` ska innehålla metadata samt en lista över trafikfilterregler och WAF-regler.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
         ...
   ```

Parametern &quot;kind&quot; ska ställas in på &quot;CDN&quot; och versionen ska ställas in på schemaversionen, som för närvarande är &quot;1&quot;. Se exemplen längre fram.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. För att konfigurera WAF-regler måste WAF vara aktiverat i Cloud Manager, vilket beskrivs nedan för både nya och befintliga programscenarier. Observera att en separat licens måste köpas för WAF.

   1. Om du vill konfigurera WAF för ett nytt program ska du kontrollera **WAF-DDOS-skydd** kryssrutan i **Säkerhet** enligt nedan. Fortsätt genom att följa stegen som beskrivs i [Lägg till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) för att skapa ditt program

   1. Om du vill konfigurera WAF för ett befintligt program väljer du **Redigera program** genom att följa stegen som beskrivs i [Redigeringsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) dokumentation. Sedan i **Säkerhet** kan du när som helst avmarkera eller kontrollera alternativet WAF-DDOS

1. För andra miljötyper än RDE kör du Cloud Managers konfigurationsflöde, som kan konfigureras enligt beskrivningen nedan.

   1. På ditt pipeline-kort på startsidan för Cloud Manager väljer du **Lägg till produktionspipeline** eller **Lägg till icke-produktionsförlopp** för att starta guiden Lägg till pipeline
   1. Välj **Distributionsförlopp** på konfigurationsfliken

      ![Välj alternativet Distributionsförlopp](/help/security/assets/deployment.png)

   1. Ge pipelinen ett namn och välj distributionsutlösare och välj sedan **Fortsätt**
   1. I **Källkod** flik, välja **Målinriktad distribution** väljer **Konfig**

      ![Välj målinriktad distribution](/help/security/assets/target-deployment.png)

   1. Välj databas och gren efter behov. Om det finns en konfigurationspipeline för den valda miljön är det här valet inaktiverat.

      ![Översikt över en konfigurationspipeline](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > Användarna måste vara inloggade som Deployment Manager för att kunna konfigurera eller köra dessa pipelines.
      > Dessutom kan du bara konfigurera och köra en Config-pipeline per miljö.

   1. Välj **Spara**. Din nya pipeline kommer att visas i pipeline-kortet och kan köras när du är klar.
   1. Kommandoraden kommer att användas för RDE, men RDE stöds inte för närvarande.

## Syntax för trafikfilterregler {#rules-syntax}

Du kan konfigurera `traffic filter rules` för att matcha på mönster som IP, användaragent, begäranrubriker, värdnamn, geo och url.

Kunder som licensierar WAF-erbjudandet kan också konfigurera en särskild kategori trafikfilterregler som kallas för `WAF traffic filter rules` (eller WAF-regler för kort) som refererar till en eller flera WAF-flaggor, som listas i sitt eget avsnitt nedan.

Här är ett exempel på en uppsättning trafikfilterregler, som även innehåller en WAF-regel.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

Formatet på trafikfilterreglerna i filen cdn.yaml beskrivs nedan. Se några exempel i ett senare avsnitt.


| **Egenskap** | **De flesta trafikfilterreglerna** | **WAF-trafikfilterregler** | **Typ** | **Standardvärde** | **Beskrivning** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Regelnamn (64 tecken långt, får bara innehålla alfanumeriska tecken och - ) |
| när | X | X | `Condition` | - | Den grundläggande strukturen är:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Se Syntaxen för villkorsstruktur nedan, som beskriver get-ters, prediates och hur du kombinerar flera villkor. |
| åtgärd | X | X | `Action` | logg | log, allow, block, log eller action object Standardvärdet är log |
| rateLimit | X |   | `RateLimit` | inte definierad | Konfiguration för hastighetsbegränsning. Hastighetsbegränsning är inaktiverad om den inte är definierad.<br><br>Det finns ett separat avsnitt nedan som beskriver rateLimit-syntaxen, tillsammans med exempel. |

### Villkorsstruktur {#condition-structure}

Ett villkor kan vara antingen ett enkelt villkor eller en grupp villkor.

**Enkelt villkor**

Ett enkelt villkor består av en get-metod och ett predikat.

```
{ <getter>: <value>, <predicate>: <value> }
```

**Gruppvillkor**

En grupp villkor består av flera enkla och/eller gruppvillkor.

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **Egenskap** | **Typ** | **Betydelse** |
|---|---|---|
| **allOf** | `array[Condition]` | **och** operation. true om alla angivna villkor returnerar true |
| **anyOf** | `array[Condition]` | **eller** operation. true om något av villkoren i listan returnerar true |

**Getter**

| **Egenskap** | **Typ** | **Beskrivning** |
|---|---|---|
| reqProperty | `string` | Request-egenskap.<br><br>En av: `path` , `queryString`, `method`, `tier`, `domain`, `clientIp`, `clientCountry`<br><br>Egenskapen domain är en gemener transformering av begärans värdhuvud. Det är användbart för strängjämförelser så att matchningar inte missas på grund av skiftlägeskänslighet.<br><br>The `clientCountry` använder två bokstavskoder som visas på [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | Returnerar begärandehuvud med angivet namn |
| queryParam | `string` | Returnerar frågeparameter med angivet namn |
| cookie | `string` | Returnerar cookie med angivet namn |

**Förutse**

| **Egenskap** | **Typ** | **Betydelse** |
|---|---|---|
| **är lika med** | `string` | true om get-resultatet är lika med det angivna värdet |
| **doesNotEqual** | `string` | true om get-resultatet inte är lika med det angivna värdet |
| **gilla** | `string` | true om get-resultatet matchar angivet mönster |
| **notLike** | `string` | true om get-resultatet inte matchar det angivna mönstret |
| **matchar** | `string` | true om get-resultatet matchar angivet regex |
| **doesNotMatch** | `string` | true om get-resultatet inte matchar angivet regex |
| **in** | `array[string]` | true om den angivna listan innehåller get-resultat |
| **notIn** | `array[string]` | true om den angivna listan inte innehåller get-resultat |

### Åtgärdsstruktur {#action-structure}

Anges av `action` fält som kan vara en sträng som anger åtgärdstyp (allow, block, log) och antar standardvärden för alla andra alternativ, eller ett objekt där regeltypen definieras via `type` obligatoriskt fält tillsammans med andra alternativ som gäller för den typen.

**Åtgärdstyper**

Åtgärderna prioriteras utifrån deras typer i följande tabell, som ordnas för att återspegla den ordning som åtgärderna utförs:

| **Namn** | **Tillåtna egenskaper** | **Betydelse** |
|---|---|---|
| **tillåt** | `wafFlags` (valfritt) | om wafFlags inte finns avbryter ytterligare regelbearbetning och fortsätter att ge svar. Om det finns wafFlags inaktiverar den angivna WAF-skyddet och fortsätter till ytterligare regelbearbetning. |
| **block** | `status, wafFlags` (valfritt och ömsesidigt uteslutande) | Om wafFlags inte finns returnerar HTTP-fel utan att alla andra egenskaper skickas, definieras felkoden av statusegenskapen eller så är standardvärdet 406. Om det finns wafFlags aktiverar det angivna WAF-skyddet och fortsätter till ytterligare regelbearbetning. |
| **logg** | `wafFlags` (valfritt) | loggar det faktum att regeln utlöstes, annars påverkas inte bearbetningen. wafFlags har ingen effekt |

### WAF-flagglista {#waf-flags-list}

The `wafFlag` kan innehålla följande:

| **Flagga-ID** | **Flaggnamn** | **Beskrivning** |
|---|---|---|
| SQLI | SQL-inmatning | SQL Injection är ett försök att få åtkomst till ett program eller få privilegierad information genom att köra godtyckliga databasfrågor. |
| BAKDOOR | Bakdörr | En bakdörrssignal är en begäran som försöker avgöra om det finns en gemensam bakdörrsfil i systemet. |
| CMDEXE | Kommandokörning | Kommandokörning är ett försök att få kontroll över eller skada ett målsystem genom godtyckliga systemkommandon med hjälp av användarindata. |
| XSS | Skript för flera webbplatser | Korsskriptning mellan webbplatser är ett försök att kapa en användares konto eller webbläsarsession via skadlig JavaScript-kod. |
| TRAVERSAL | Kataloggenomgång | Directory Traversal är ett försök att navigera i behöriga mappar i ett system för att kunna hämta känslig information. |
| USERAGENT | Attackverktyg | Attack Tooling är användning av automatiserad programvara för att identifiera säkerhetsproblem eller för att försöka utnyttja en upptäckt säkerhetslucka. |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI-attacker försöker utnyttja [Log4Shell-sårbarhet](https://en.wikipedia.org/wiki/Log4Shell) finns i Log4J-versioner tidigare än 2.16.0 |
| AWS SSRF | AWS-SSRF | SSRF (Server Side Request Forgery) är en begäran som försöker skicka begäranden från webbprogrammet till interna målsystem. AWS SSRF-attacker använder SSRF för att få Amazon Web Services-nycklar (AWS) och få tillgång till S3-bucket och deras data. |
| BHH | Felaktiga Hop-huvuden | Felaktiga Hop-huvuden anger ett försök till HTTP-smuggling via en felformaterad Transfer-Encoding (TE) eller Content-Length (CL)-rubrik, eller en korrekt formaterad TE- och CL-rubrik |
| ABNORMALPATH | Onormal bana | Onormal bana anger att den ursprungliga banan skiljer sig från den normaliserade banan (till exempel `/foo/./bar` normaliseras till `/foo/bar`) |
| KOMPRIMERAD | Komprimering upptäcktes | POSTENS begärandetext är komprimerad och kan inte inspekteras. Om t.ex. begärandehuvudet &quot;Content-Encoding: gzip&quot; anges och POSTENS brödtext inte är oformaterad text. |
| DUBBELKODNING | Dubbel kodning | Dubbel kodning används för att kontrollera om HTML-tecken med dubbel kodning kan användas |
| FORCEFULBROWSING | Tvingad bläddring | Tvingad bläddring är det misslyckade försöket att komma åt administratörssidor |
| NOTUTF8 | Ogiltig kodning | Ogiltig kodning kan göra att servern översätter skadliga tecken från en begäran till ett svar, vilket kan orsaka denial of service eller XSS |
| JSON-ERROR | JSON-kodningsfel | En begärandetext för POST, PUT eller PATCH som har angetts som innehåller JSON i begärandehuvudet för Content-Type men som innehåller JSON-tolkningsfel. Detta beror ofta på ett programmeringsfel eller en automatiserad eller skadlig begäran. |
| MALFORMED-DATA | Felformaterade data i begärandetexten | En begärandetext för POST, PUT eller PATCH som har fel format enligt begärandehuvudet Content-Type. Om en begäranderubrik av typen&quot;Content-Type: application/x-www-form-urlencoded&quot; anges och innehåller en POST som är json. Detta är ofta ett programmeringsfel, en automatiserad eller skadlig begäran. Kräver agent 3.2 eller högre. |
| SANS | Skadlig IP-trafik | [SANS Internet Storm Center](https://isc.sans.edu/) lista över IP-adresser som har rapporterats ha varit inblandade i skadlig aktivitet |
| SIGSCI-IP | Nätverkseffekt | IP flaggad av SignalSciences: När ett IP-värde flaggas på grund av en skadlig signal från beslutsmotorn sprids detta IP-värde till alla kunder. Efterföljande förfrågningar från de IP-adresser som innehåller ytterligare signaler under flaggan loggas sedan |
| INNEHÅLLSTYP | Begäranhuvudet Content-Type saknas | En POST-, PUT- eller PATCH-begäran som inte har någon Content-Type-begäranderubrik. Som standard ska programservrar anta&quot;Content-Type: text/plain; charset=us-ascii&quot; i det här fallet. Många automatiska och skadliga förfrågningar kanske saknar&quot;Innehållstyp&quot;. |
| NOUA | Ingen användaragent | Många automatiserade och skadliga förfrågningar använder falska eller saknade användaragenter för att göra det svårt att identifiera vilken typ av enhet som framställningarna görs på. |
| TORNODE | Tor Traffic | Tor är programvara som döljer en användares identitet. En spik i Tor-trafiken kan indikera en angripare som försöker maskera sin plats. |
| DATACENTER | Datacentertrafik | Datacentralstrafik är icke-organisk trafik som härrör från identifierade värdtjänstleverantörer. Den här typen av trafik är vanligtvis inte kopplad till en riktig slutanvändare. |
| NULLBYTE | Null byte | Null-byte visas normalt inte i en begäran och anger att begäran är felformaterad och potentiellt skadlig. |
| IMPOSTOR | SearchBot Impostor | Sökrobotimporteraren är någon som låtsas vara en sökrobot från Google eller Bing, men som inte är berättigad. Observera att är inte beroende av ett svar för sig självt, utan måste lösas i molnet först, så det bör inte användas i en förregel. |
| PRIVATEFILE | Privata filer | Privata filer är vanligtvis konfidentiella, till exempel Apache `.htaccess` eller en konfigurationsfil som kan läcka känslig information |
| SKANNER | Skanner | Identifierar vanliga skanningstjänster och verktyg |
| RESPONSESPLIST | HTTP-svarsdelning | Identifierar när CRLF-tecken skickas som indata till programmet för att mata in rubriker i HTTP-svaret |
| XML-FEL | XML-kodningsfel | En begärandetext för POST, PUT eller PATCH som har angetts som innehållande XML i begärandehuvudet för Content-Type men som innehåller XML-tolkningsfel. Detta beror ofta på ett programmeringsfel eller en automatiserad eller skadlig begäran. |

## Överväganden {#considerations}

* När två motstridiga regler skapas har alltid reglerna Tillåt företräde framför blockreglerna. Om du till exempel skapar en regel som blockerar en viss sökväg och en regel som tillåter en viss IP-adress, tillåts förfrågningar från den IP-adressen på den blockerade sökvägen.

* Om en regel matchas och blockeras svarar CDN med en `406` returkod.

* Konfigurationsfilerna bör inte innehålla hemligheter eftersom de skulle kunna läsas av alla som har åtkomst till Git-databasen.

## Exempel på regler {#examples}

Vissa regelexempel följer. Se [rabattgränssektion](#rules-with-rate-limits) ytterligare ned för exempel på hastighetsbegränsning.

**Exempel 1**

Den här regeln blockerar begäranden från IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**Exempel 2**

Den här regeln blockerar begäranden på sökvägen `/helloworld` vid publicering med en användaragent som innehåller Chrome:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
           allOf:
            - { reqProperty: path, equals: /helloworld }
            - { reqProperty: tier, equals: publish }
            - { reqHeader: user-agent, matches: '.*Chrome.*'  }
           action:
             type: block
```

**Exempel 3**

Den här regeln blockerar begäranden som innehåller frågeparametern `foo`, men tillåter alla förfrågningar från IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Exempel 4**

Den här regeln blockerar begäranden till path /block-me och blockerar alla begäranden som matchar ett SQLI- eller XSS-mönster:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**Exempel 4**

Den här regeln blockerar åtkomst till OFAC-länder:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - { reqProperty: tier, equals: publish }
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## Regler med hastighetsbegränsningar {#rules-with-rate-limits}

Ibland är det önskvärt att blockera trafikmatchning för en regel endast om matchningen överskrider en viss hastighet över tiden. Ange ett värde för `rateLimit` Egenskapen begränsar hastigheten för de begäranden som matchar regelvillkoret.

### rateLimit-struktur {#ratelimit-structure}

| **Egenskap** | **Typ** | **Standard** | **MENING** |
|---|---|---|---|
| limit | heltal mellan 10 och 10000 | obligatoriskt | Begärandefrekvens i begäranden per sekund som regeln aktiveras för. |
| window | heltal: 1, 10 eller 60 | 10 | Provningsfönstret i sekunder för vilket begärandehastigheten beräknas. |
| påföljd | heltal mellan 60 och 3600 | 300 (5 minuter) | En period i sekunder för vilken matchande begäranden blockeras (avrundat till närmaste minut). |
| groupBy | array[Getter] | ingen | Räknaren för hastighetsbegränsning sammanställs av en uppsättning egenskaper för begäran (till exempel clientIp). |

### Exempel {#ratelimiting-examples}

**Exempel 1**

Den här regeln blockerar en klient i 5 m när den överskrider 100 req/sek under de senaste 60 sektionerna:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Exempel 2**

Blockera förfrågningar för 60-tal på sökvägen /critical/resource när den överskrider 100 req/sek under de senaste 60 sektionerna:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## CDN-loggar {#cdn-logs}

AEM as a Cloud Service ger åtkomst till CDN-loggar, som är användbara för fall som till exempel optimering av träffkvoten och konfigurering av CDN- och WAF-regler. CDN-loggar visas i Cloud Manager **Hämta loggar** när du väljer Författare eller Publiceringstjänst.

Egenskapen&quot;rules&quot; beskriver vilka trafikfilterregler som matchas och har följande mönster:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Till exempel:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Reglerna fungerar på följande sätt:

* Alla matchande regelnamn som har deklarerats av kunden visas i attributet match.
* åtgärdsattributet innehåller information om huruvida reglerna har lett till blockering, tillstånd eller loggning.
* om WAF är licensierat och aktiverat listas alla SWF-regler (t.ex. SQLI; observera att detta är oberoende av det kunddeklarerade namnet) som upptäcktes, oavsett om SWF-reglerna listades i konfigurationen.
* om inga kunddeklarerade regler matchar och inga waf-regler matchar, kommer egenskapen för regelattribut att vara tom.

I allmänhet visas matchande regler i loggposten för alla förfrågningar till CDN, oavsett om det är en CDN-träff, ett pass eller en miss. Däremot visas WAF-regler i loggposten endast för begäranden till CDN som betraktas som CDN-missar eller -pass, men inte CDN-träffar.

I exemplet nedan visas ett exempel på cdn.yaml och två CDN-loggposter:


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### Loggformat {#cdn-log-format}

Nedan finns en lista med de fältnamn som används i CDN-loggar, tillsammans med en kort beskrivning.

| **Fältnamn** | **Beskrivning** |
|---|---|
| *tidsstämpel* | Den tidpunkt då begäran startades, efter TLS-avslutning. |
| *ttfb* | Förkortning för *Tid till första byte*. Tidsintervallet mellan begäran startades fram till punkten innan svarstexten började direktuppspelas. |
| *cli_ip* | Klientens IP-adress. |
| *cli_country* | Två bokstäver [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2-landskod för klientlandet. |
| *rutnät* | Värdet på begärandehuvudet som används för att unikt identifiera begäran. |
| *req_ua* | Användaragenten som ansvarar för att göra en given HTTP-begäran. |
| *värd* | Den myndighet som begäran avser. |
| *url* | Den fullständiga sökvägen, inklusive frågeparametrar. |
| *method* | HTTP-metod som skickas av klienten, till exempel &quot;GET&quot; eller &quot;POST&quot;. |
| *res_type* | Den innehållstyp som används för att ange resursens ursprungliga medietyp. |
| *cache* | Status för cachen. Möjliga värden är HIT, MISS eller PASS |
| *status* | HTTP-statuskoden som ett heltalsvärde. |
| *_Bläddra* | Den tid (i sekunder) som ett svar har cachelagrats (i alla noder). |
| *pop* | Datacenter för CDN-cacheservern. |
| *regler* | Namnet på matchande regler.<br><br>Anger också om matchningen resulterade i ett block. <br><br>Till exempel &quot;`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>Tom om inga regler matchade. |
