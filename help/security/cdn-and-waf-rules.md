---
title: Konfigurera CDN- och WAF-regler för att filtrera trafik
description: Använd reglerna för brandvägg för CDN och webbaserade program för att filtrera skadlig trafik
source-git-commit: a9b8b4d6029d0975428b9cff04dbbec993d56172
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 0%

---


# Konfigurera CDN- och WAF-regler för att filtrera trafik {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i det pågående programmet för tidiga användare skickar du e-post **aemcs-waf-adopter@adobe.com**, inklusive namnet på organisationen och sammanhanget om ditt intresse för funktionen.

Adobe försöker mildra attacker mot kundwebbplatser, men det kan vara praktiskt att proaktivt filtrera förfrågningar som matchar vissa mönster så att skadlig trafik inte når applikationen. Möjliga strategier är:

* Lagermoduler i Apache som `mod_security`
* Konfigurera regler som distribueras till CDN via Cloud Managers konfigurationsflöde.

I den här artikeln beskrivs den senare metoden, som innehåller två kategorier av regler:

1. **CDN-regler**: blockera eller tillåt förfrågningar baserat på begäranegenskaper och begäranrubriker, inklusive IP, sökvägar och användaragent. Dessa regler kan konfigureras av alla AEM as a Cloud Service kunder
1. **WAF** (Brandvägg för webbaserade program): blockbegäranden som matchar olika mönster som man vet är associerade med skadlig trafik. Dessa regler kan konfigureras av kunder som licensierar WAF-tillägget. Kontakta Adobe-kontoteamet för mer information. Observera att ingen ytterligare licens krävs under det tidiga adopterprogrammet.

Dessa regler kan distribueras till dev-, stage- och prod-molnmiljötyper, för produktionsprogram (inte sandbox). Stöd för RDE-miljöer kommer att finnas tillgängligt i framtiden.

## Inställningar {#setup}

1. Skapa först följande mapp- och filstruktur för mappen på den översta nivån i Git:

   ```
   config/
        cdn/
           cdn.yaml
           _config.yaml
   ```

1. `_config.yaml` beskriver vissa metadata om konfigurationen. Parametern &quot;kind&quot; ska ställas in på &quot;CDN&quot; och versionen ska ställas in på schemaversionen, som för närvarande är &quot;1&quot;. Se utdraget nedan:

   ```
   kind: "CDN"
   version: "1"
   ```

   <!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. `cdn.yaml` ska innehålla en lista över CDN-regler och WAF-regler, som beskrivs i avsnitten nedan
1. För att matcha WAF-regler måste WAF vara aktiverat i Cloud Manager, vilket beskrivs nedan för både nya och befintliga programscenarier. Observera att en separat licens måste köpas för WAF.

   1. Om du vill konfigurera WAF för ett nytt program ska du kontrollera **WAF-DDOS-skydd** kryssrutan i **Säkerhet** enligt nedan. Fortsätt genom att följa stegen som beskrivs i [Lägg till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) för att skapa ditt program

   1. Om du vill konfigurera WAF för ett befintligt program väljer du **Redigera program** genom att följa stegen som beskrivs i [Redigeringsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) dokumentation. Sedan i **Säkerhet** kan du när som helst avmarkera eller kontrollera alternativet WAF-DDOS

1. För andra miljötyper än RDE kör du Cloud Managers konfigurationsflöde, som kan konfigureras enligt beskrivningen nedan.

   1. På ditt pipeline-kort på startsidan för Cloud Manager väljer du **Lägg till produktionspipeline** eller **Lägg till icke-produktionsförlopp** för att starta guiden Lägg till pipeline
   1. Välj **Distributionsförlopp** på konfigurationsfliken

      ![Välj alternativet Distributionsförlopp](/help/security/assets/deployment.png)

   1. Ge pipelinen ett namn och välj distributionsutlösare och välj sedan **Fortsätt**
   1. I **Källkod** flik, välja **Målinriktad distribution** väljer **Konfig**

      ![Välj riktad distribution](/help/security/assets/target-deployment.png)

   1. Välj databas och gren efter behov. Om det finns en konfigurationspipeline för den valda miljön är det här valet inaktiverat.

      ![Översikt över en konfigurationspipeline](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      >Du kan bara konfigurera och köra en Config-pipeline per miljö.

   1. Välj **Spara**. Din nya pipeline kommer att visas i pipeline-kortet och kan köras när du är klar.
   1. För RDE används kommandoraden, men RDE stöds inte just nu.

## Regelsyntax {#rules-syntax}

Regelformatet beskrivs nedan, följt av några exempel i ett senare avsnitt.

| **Egenskap** | **CDN-regler** | **WAF-regler** | **Typ** | **Standardvärde** | **Beskrivning** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Regelnamn (64 tecken långt, får bara innehålla alfanumeriska tecken och - ) |
| när | X | X | `Condition` | - | Den grundläggande strukturen är:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Se Syntaxen för villkorsstruktur nedan, som beskriver get-ters, prediates och hur du kombinerar flera villkor. |
| åtgärd | X | X | `Enum` | log (CDN-regler) | För CDN-regler: allow, block, log. Standardvärdet är log.<br><br>För WAF-regler: `enableWafRules`, `disableWafRules`, log. Ingen standard. |
| rateLimit | X |   | `RateLimit` | inte definierad | Konfiguration för hastighetsbegränsning. Hastighetsbegränsning är inaktiverad om den inte är definierad.<br><br>Det finns ett separat avsnitt nedan som beskriver rateLimit-syntaxen, tillsammans med exempel. |
| wafRules |   | X | `array[Enum]` | - | Lista över WAF-regler som ska aktiveras eller inaktiveras.<br><br>Exempel är SQLI och XSS. En fullständig lista finns i listan över wf-regler nedan. |

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

| **Egenskap** | **Typ** | **Beskrivning** |
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

| **Egenskap** | **Typ** | **Beskrivning** |
|---|---|---|
| **är lika med** | `string` | true om get-resultatet är lika med det angivna värdet |
| **doesNotEqual** | `string` | true om get-resultatet inte är lika med det angivna värdet |
| **gilla** | `string` | true om get-resultatet matchar angivet mönster |
| **notLike** | `string` | true om get-resultatet inte matchar det angivna mönstret |
| **matchar** | `string` | true om get-resultatet matchar angivet regex |
| **doesNotMatch** | `string` | true om get-resultatet inte matchar angivet regex |
| **in** | `array[string]` | true om den angivna listan innehåller get-resultat |
| **notIn** | `array[string]` | true om den angivna listan inte innehåller get-resultat |

**wafRules List**

The `wafRules` -egenskapen kan innehålla följande regler:

| **Regel-ID** | **Regelnamn** | **Beskrivning** |
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

## Exempel {#examples}

Vissa regelexempel följer. Se [rabattgränssektion](#rules-with-rate-limits) ytterligare ned för exempel på hastighetsbegränsning.

**Exempel 1**

Den här regeln blockerar begäranden från IP 192.168.1.1:

```
data:
  rules:
    - name: "block-request-from-ip"
      when: { reqProperty: clientIp, equals: "192.168.1.1" }
      action: block
```

**Exempel 2**

Den här regeln blockerar begäranden på sökvägen `/helloworld` vid publicering med en användaragent som innehåller Chrome:

```
data:
  rules:
    - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
      when:
        allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
      action: block
```

**Exempel 3**

Den här regeln blockerar begäranden som innehåller frågeparametern `foo`, men tillåter alla förfrågningar från IP 192.168.1.1:

```
data:
  rules:
    - name: "block-request-that-contains-query-parameter-foo"
      when: { queryParam: url-param, equals: foo }
      action: block
    - name: "allow-all-requests-from-ip"
      when: { reqProperty: clientIp, equals: 192.168.1.1 }
      action: allow
```

**Exempel 4**

Den här regeln blockerar begäranden till path /block-me och blockerar alla begäranden som matchar ett SQLI- eller XSS-mönster:

```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

## Regler med hastighetsbegränsningar {#rules-with-rate-limits}

Ibland är det önskvärt att blockera trafikmatchning för en regel endast om matchningen överskrider en viss hastighet över tiden. Ange ett värde för `rateLimit` Egenskapen begränsar hastigheten för de begäranden som matchar regelvillkoret.

### rateLimit-struktur {#ratelimit-structure}

| **Egenskap** | **Typ** | **Standardvärde** | **Beskrivning** |
|---|---|---|---|
| limit | heltal mellan 10 och 10000 | obligatoriskt | Begärandefrekvens i begäranden per sekund som regeln aktiveras för |
| window | heltal: 1, 10 eller 60 | 10 | Provtagningsfönster i sekunder för vilket begärandehastigheten beräknas |
| påföljd | heltal mellan 60 och 3600 | 300 (5 minuter) | En period i sekunder för vilken matchande begäranden blockeras (avrundat till närmaste minut) |

### Exempel {#ratelimiting-examples}

Exempel 1: Om begärandehastigheten överstiger 100 begäranden per sekund under de senaste 60 sekunderna blockerar du `/critical/resource` i 60 sekunder

```
- name: rate-limit-example
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit: { limit: 100, window: 60, penalty: 60 }
```

Exempel 2: När begärandehastigheten överstiger 10 begäranden per sekund på 10 sekunder blockerar du resursen i 300 sekunder:

```
- name: rate-limit-using-defaults
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit:
    limit: 10
```

## CDN-loggar {#cdn-logs}

AEM as a Cloud Service ger åtkomst till CDN-loggar, som är användbara för fall som till exempel optimering av träffkvoten och konfigurering av CDN- och WAF-regler. CDN-loggar visas i Cloud Manager **Hämta loggar** när du väljer Författare eller Publiceringstjänst.

Namnet på regeln visas i egenskapen rules om begäran matchar regeln, även om åtgärden är&quot;allow&quot; och därför inte blockeras trafiken.

Matchande CDN-regler visas i loggposten för alla förfrågningar till CDN, oavsett om det är en CDN-träff, ett pass eller en miss. Däremot visas WAF-regler i loggposten endast för begäranden till CDN som betraktas som CDN-missar eller -pass, men inte CDN-träffar.

Exemplet nedan visar ett exempel `cdn.yaml` och två CDN-loggposter, med icke-tomma värden i egenskapen rules på grund av blockerade begäranden som matchar CDN-regeln respektive WAF-regeln.


```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=path-rule;waf=;action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"req_mthd": "GET",
"res_type": "image/png",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=;waf=SQLI;action=blocked"
}
```

### Loggformat {#cdn-log-format}

Nedan finns en lista med de fältnamn som används i CDN-loggar, tillsammans med en kort beskrivning.

| **Fältnamn** | **Beskrivning** |
|---|---|
| *tidsstämpel* | Den tidpunkt då begäran startades, efter TLS-avslutning |
| *ttfb* | Förkortning för *Tid till första byte*. Tidsintervallet mellan begäran startades fram till punkten innan svarstexten började direktuppspelas. |
| *cip* | Klientens IP-adress. |
| *rutnät* | Värdet på begärandehuvudet som används för att unikt identifiera begäran. |
| *ua* | Användaragenten som ansvarar för att göra en given HTTP-begäran. |
| *värd* | Den myndighet som begäran avser. |
| *url* | Den fullständiga sökvägen, inklusive frågeparametrar. |
| *req_mthd* | HTTP-metod som skickas av klienten, till exempel &quot;GET&quot; eller &quot;POST&quot;. |
| *res_type* | Den innehållstyp som används för att ange resursens ursprungliga medietyp |
| *cache* | Status för cachen. Möjliga värden är HIT, MISS eller PASS |
| *res_status* | HTTP-statuskoden som ett heltalsvärde. |
| *res_bsize* | Brödtextbyte som skickas till klienten i svaret. |
| *server* | Datacenter för CDN-cacheservern. |
| *regler* | Namnet på matchande regler, för både CDN-regler och SWF-regler.<br><br>Matchande CDN-regler visas i loggposten för alla förfrågningar till CDN, oavsett om det är en CDN-träff, ett pass eller en miss.<br><br>Anger också om matchningen resulterade i ett block. <br><br>Till exempel &quot;`cdn=;waf=SQLI;action=blocked`&quot;<br><br>Tom om inga regler matchade. |
