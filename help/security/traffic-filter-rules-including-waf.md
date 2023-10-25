---
title: Trafikfilterregler inklusive WAF-regler
description: Konfigurera trafikfilterregler inklusive Brandväggsregler för webbprogram (WAF)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 221f6df73fe660c6f8dbf79affdccdd081ad3906
workflow-type: tm+mt
source-wordcount: '4210'
ht-degree: 0%

---


# Trafikfilterregler inklusive WAF-regler {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i det pågående programmet för tidiga användare skickar du e-post **aemcs-waf-adopter@adobe.com**, inklusive namnet på organisationen och sammanhanget om ditt intresse för funktionen.

Trafikfilterregler kan användas för att blockera eller tillåta förfrågningar i CDN-lagret, vilket kan vara användbart i scenarier som:

* Begränsa åtkomsten till specifika domäner till intern företagstrafik innan en ny webbplats publiceras
* Fastställande av hastighetsgränser så att de blir mindre mottagliga för volymetriska DDoS-attacker
* Förhindra att IP-adresser som du vet är skadliga riktas mot dina sidor

Vissa av dessa trafikfilterregler är tillgängliga för alla AEM as a Cloud Service webbplatser och Forms-kunder. De arbetar huvudsakligen med egenskaper för begäran och begäranrubriker, inklusive IP, värdnamn, sökväg och användaragent.

En underkategori av trafikfilterregler kräver antingen en förbättrad säkerhetslicens eller en licens för skydd av WAF-DDoS. Dessa kraftfulla regler kallas för trafikfilterregler för WAF (Web Application Firewall) (eller för korta WAF-regler) och har tillgång till [WAF-flaggor](#waf-flags-list) beskrivs senare i den här artikeln. Webbplatser och Forms-kunder kan kontakta sitt Adobe-kontoteam för att få information om hur man licensierar den här avancerade funktionen.

Trafikfilterregler kan distribueras via Cloud Managers konfigurationspipelines för att dev, stage och produktionsmiljötyper i produktionsprogram (icke-sandlådeprogram). Stöd för de regionala utvecklingsföretagen kommer i framtiden.

## Hur den här artikeln ordnas {#how-organized}

Den här artikeln är indelad i följande avsnitt:

* **Trafikskydd - översikt:** Lär dig hur du skyddas mot skadlig trafik.
* **Föreslagen process för att konfigurera regler:** Läs om en högnivåmetod för att skydda er webbplats.
* **Inställningar:** Upptäck hur du konfigurerar, konfigurerar och distribuerar trafikfilterregler, inklusive avancerade WAF-regler.
* **Regelsyntax:** Läs om hur du deklarerar trafikfilterregler i `cdn.yaml` konfigurationsfil. Detta omfattar både trafikfilterreglerna som är tillgängliga för alla Sites- och Forms-kunder samt underkategorin med WAF-regler för dem som licensierar den funktionen.
* **Exempel på regler:** Se exempel på deklarerade regler som hjälper dig att komma igång.
* **Regler för hastighetsbegränsning:** Lär dig hur du använder hastighetsbegränsande regler för att skydda din webbplats från attacker med stora volymer.
* **CDN-loggar:** Se vilka regler och WAF-flaggor som matchar er trafik.
* **Kontrollpanelsverktyg:** Analysera dina CDN-loggar och hitta nya trafikfilterregler.
* **Självstudiekurs:** Praktisk kunskap om funktionen, inklusive hur du använder kontrollpanelsverktyg för att deklarera rätt regler.
<!-- About the tutorial: sets the context for a linked tutorial, which gives you practical knowledge about the feature, including how to use dashboard tooling to declare the right rules. -->

## Trafikskydd - översikt {#traffic-protection-overview}

I det digitala landskapet är skadlig trafik ett hot som aldrig tidigare förekommit. Vi inser hur allvarlig risken är och erbjuder flera strategier för att skydda kundens tillämpningar och mildra attacker när de inträffar.

Vid kanten absorberar det hanterade CDN-nätverket i Adobe DDoS-attacker i nätverkslagret (lager 3 och 4), inklusive översvämnings- och speglings-/amplifieringsattacker.

Som standard vidtar Adobe åtgärder för att förhindra prestandaförsämringar på grund av oväntat höga trafikökningar över ett visst tröskelvärde. I händelse av en DDoS-attack som påverkar webbplatsens tillgänglighet, varnas Adobe ledningsgrupper och vidtar åtgärder för att minska risken.

Kunderna kan vidta förebyggande åtgärder för att mildra attacker i programlager (lager 7) genom att konfigurera regler i olika lager i innehållsleveransflödet.

På exempelvis lagret Apache kan man konfigurera antingen [avsändarmodul](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) eller [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) för att begränsa åtkomsten till visst innehåll.

Som beskrivs i den här artikeln kan trafikfilterregler distribueras till CDN med hjälp av Cloud Managers konfigurationsflöde. Utöver trafikförfrågningsbaserade trafikfilterregler som baseras på egenskaper som IP-adress, sökväg och rubriker kan kunderna även licensiera en kraftfull underkategori av trafikfilterregler som kallas för WAF-regler.

## Föreslagen process {#suggested-process}

Nedan följer en högnivårekommenderad process från början till slut för att komma fram till rätt trafikfilterregler:

1. Konfigurera en icke-produktions- och produktionskonfigurationspipeline, enligt beskrivningen i [Inställningar](#setup) -avsnitt.
1. Kunder som har licensierat underkategorin för reglerna för WAF-trafikfilter bör aktivera dem i Cloud Manager.
1. Läs igenom och prova självstudiekursen för att få en större förståelse för hur du använder trafikfilterregler, inklusive WAF-regler om de har licensierats. Självstudiekursen leder dig genom att distribuera regler till en utvecklingsmiljö, simulera skadlig trafik, ladda ned [CDN-loggar](#cdn-logs)och analysera dem i [kontrollpanelsverktyg](#dashboard-tooling).
1. Kopiera de rekommenderade initialreglerna till `cdn.yaml` och distribuera konfigurationen till produktionen i loggläge.
1. Analysera resultatet efter att ha samlat in viss trafik med [kontrollpanelsverktyg](#dashboard-tooling) för att se om det fanns några träffar. Leta efter falska positiva inställningar och gör nödvändiga justeringar för att aktivera standardreglerna i blockläge.
1. Lägg till anpassade regler baserat på analys av CDN-loggarna, först testning med simulerad trafik i utvecklingsmiljöer, innan distributionen till scenen och produktionen i loggläge görs, sedan blockläge.
1. Övervaka trafiken kontinuerligt och ändra reglerna allt eftersom hotelandskapet utvecklas.

## Inställningar {#setup}

1. Skapa först följande mapp- och filstruktur för mappen på den översta nivån i projektet i Git:

   ```
   config/
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
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

The `kind` parametern ska anges till `CDN` och versionen bör anges till schemaversionen, som för närvarande är `1`. Se exemplen längre fram.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. För att konfigurera WAF-regler måste WAF vara aktiverat i Cloud Manager, vilket beskrivs nedan för både nya och befintliga programscenarier. Observera att en separat licens måste köpas för WAF.

   1. Om du vill konfigurera WAF för ett nytt program ska du kontrollera **WAF-DDOS-skydd** kryssruta på **Säkerhet** när du [lägga till ett produktionsprogram.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Så här konfigurerar du WAF för ett befintligt program: [redigera ditt program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) och **Säkerhet** avmarkera eller kontrollera **WAF-DDOS** när som helst.

1. För andra miljötyper än RDE skapar du en riktad distributionskonfiguration i Cloud Manager.

   * [Se det här dokumentet för produktion av rörledningar.](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Se det här dokumentet för icke-produktionsrörledningar.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

Kommandoraden kommer att användas för RDE, men RDE stöds inte för närvarande.

## Syntax för trafikfilterregler {#rules-syntax}

Du kan konfigurera `traffic filter rules` för att matcha på mönster som IP, användaragent, begäranrubriker, värdnamn, geo och url.

Kunder som licensierar erbjudandet Förbättrat skydd eller skydd via WAF-DDoS kan också konfigurera en särskild kategori trafikfilterregler som kallas för `WAF traffic filter rules` (eller WAF-regler för korta) som hänvisar till en eller flera [WAF-flaggor](#waf-flags-list).

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

Formatet på trafikfilterreglerna i `cdn.yaml` filen beskrivs nedan. Se några [andra exempel](#examples) i ett senare avsnitt, samt i ett separat avsnitt om [Regler för hastighetsbegränsning](#rate-limit-rules).


| **Egenskap** | **De flesta trafikfilterreglerna** | **WAF-trafikfilterregler** | **Typ** | **Standardvärde** | **Beskrivning** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Regelnamn (64 tecken långt, får bara innehålla alfanumeriska tecken och - ) |
| när | X | X | `Condition` | - | Den grundläggande strukturen är:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Se Syntax för villkorsstruktur](#condition-structure) nedan, som beskriver get-metoderna, predikaten och hur du kombinerar flera villkor. |
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
| reqCookie | `string` | Returnerar cookie med angivet namn |
| postParam | `string` | Returnerar parametern med det angivna namnet från brödtexten. Fungerar bara när brödtexten är av innehållstyp `application/x-www-form-urlencoded` |

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
| **exists** | `boolean` | true om värdet är true och egenskapen finns eller om värdet är false och egenskapen inte finns |

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

The `wafFlags` egenskapen, som kan användas i de licensbara reglerna för WAF-trafikfilter, kan referera till följande:

| **Flagga-ID** | **Flaggnamn** | **Beskrivning** |
|---|---|---|
| SQLI | SQL-inmatning | SQL Injection är ett försök att få åtkomst till ett program eller få privilegierad information genom att köra godtyckliga databasfrågor. |
| BAKDOOR | Bakdörr | En bakdörrssignal är en begäran som försöker avgöra om det finns en gemensam bakdörrsfil i systemet. |
| CMDEXE | Kommandokörning | Kommandokörning är ett försök att få kontroll över eller skada ett målsystem genom godtyckliga systemkommandon med hjälp av användarindata. |
| XSS | Skript för flera webbplatser | Korsskriptning mellan webbplatser är ett försök att kapa en användares konto eller webbläsarsession via skadlig JavaScript-kod. |
| TRAVERSAL | Kataloggenomgång | Directory Traversal är ett försök att navigera i behöriga mappar i ett system för att kunna hämta känslig information. |
| USERAGENT | Attackverktyg | Attack Tooling är användning av automatiserad programvara för att identifiera säkerhetsproblem eller för att försöka utnyttja en upptäckt säkerhetslucka. |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI-attacker försöker utnyttja [Log4Shell-sårbarhet](https://en.wikipedia.org/wiki/Log4Shell) finns i Log4J-versioner tidigare än 2.16.0 |
| BHH | Felaktiga Hop-huvuden | Felaktiga Hop-huvuden anger ett försök till HTTP-smuggling via en felformaterad Transfer-Encoding (TE) eller Content-Length (CL)-rubrik, eller en korrekt formaterad TE- och CL-rubrik |
| ABNORMALPATH | Onormal bana | Onormal bana anger att den ursprungliga banan skiljer sig från den normaliserade banan (till exempel `/foo/./bar` normaliseras till `/foo/bar`) |
| DUBBELKODNING | Dubbel kodning | Dubbel kodning används för att kontrollera om HTML-tecken med dubbel kodning kan användas |
| NOTUTF8 | Ogiltig kodning | Ogiltig kodning kan göra att servern översätter skadliga tecken från en begäran till ett svar, vilket kan orsaka denial of service eller XSS |
| JSON-ERROR | JSON-kodningsfel | En begärandetext för POST, PUT eller PATCH som har angetts som innehåller JSON i begärandehuvudet för Content-Type men som innehåller JSON-tolkningsfel. Detta beror ofta på ett programmeringsfel eller en automatiserad eller skadlig begäran. |
| MALFORMED-DATA | Felformaterade data i begärandetexten | En begärandetext för POST, PUT eller PATCH som har fel format enligt begärandehuvudet Content-Type. Om en begäranderubrik av typen&quot;Content-Type: application/x-www-form-urlencoded&quot; anges och innehåller en POST som är json. Detta är ofta ett programmeringsfel, en automatiserad eller skadlig begäran. Kräver agent 3.2 eller högre. |
| SANS | Skadlig IP-trafik | [SANS Internet Storm Center](https://isc.sans.edu/) lista över IP-adresser som har rapporterats ha varit inblandade i skadlig aktivitet |
| SIGSCI-IP | Nätverkseffekt | IP flaggad av SignalSciences: När ett IP-värde flaggas på grund av en skadlig signal från beslutsmotorn sprids detta IP-värde till alla kunder. Efterföljande förfrågningar från de IP-adresser som innehåller ytterligare signaler under flaggan loggas sedan |
| INNEHÅLLSTYP | Begäranhuvudet Content-Type saknas | En POST-, PUT- eller PATCH-begäran som inte har någon Content-Type-begäranderubrik. Som standard ska programservrar anta&quot;Content-Type: text/plain; charset=us-ascii&quot; i det här fallet. Många automatiska och skadliga förfrågningar kanske saknar&quot;Innehållstyp&quot;. |
| NOUA | Ingen användaragent | Många automatiserade och skadliga förfrågningar använder falska eller saknade användaragenter för att göra det svårt att identifiera vilken typ av enhet som framställningarna görs på. |
| TORNODE | Tor Traffic | Tor är programvara som döljer en användares identitet. En spik i Tor-trafiken kan indikera en angripare som försöker maskera sin plats. |
| NULLBYTE | Null byte | Null-byte visas normalt inte i en begäran och anger att begäran är felformaterad och potentiellt skadlig. |
| PRIVATEFILE | Privata filer | Privata filer är vanligtvis konfidentiella, till exempel Apache `.htaccess` eller en konfigurationsfil som kan läcka känslig information |
| SKANNER | Skanner | Identifierar vanliga skanningstjänster och verktyg |
| RESPONSESPLIST | HTTP-svarsdelning | Identifierar när CRLF-tecken skickas som indata till programmet för att mata in rubriker i HTTP-svaret |
| XML-FEL | XML-kodningsfel | En begärandetext för POST, PUT eller PATCH som har angetts som innehållande XML i begärandehuvudet för Content-Type men som innehåller XML-tolkningsfel. Detta beror ofta på ett programmeringsfel eller en automatiserad eller skadlig begäran. |

## Överväganden {#considerations}

* När två motstridiga regler skapas har alltid reglerna Tillåt företräde framför blockreglerna. Om du till exempel skapar en regel som blockerar en viss sökväg och en regel som tillåter en viss IP-adress, tillåts förfrågningar från den IP-adressen på den blockerade sökvägen.

* Om en regel matchas och blockeras svarar CDN med en `406` returkod.

* Konfigurationsfilerna bör inte innehålla hemligheter eftersom de skulle kunna läsas av alla som har åtkomst till Git-databasen.

## Exempel på regler {#examples}

Vissa regelexempel följer. Se [rabattgränssektion](#rules-with-rate-limits) närmare anges om det finns exempel på regler för avgiftsgränser.

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
        when:
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

Den här regeln blockerar begäranden till sökväg `/block-me`och blockerar alla förfrågningar som matchar `SQLI` eller `XSS` mönster. I det här exemplet finns det en regel för WAF-trafikfilter som refererar till `SQLI` och `XSS` [WAF-flaggor](#waf-flags-list)som kräver en separat licens.

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

**Exempel 5**

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
            - reqProperty: tier
              matches: "author|publish"
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

## Regler för hastighetsbegränsning {#rate-limits-rules}

Ibland är det önskvärt att blockera trafikmatchning för en regel endast om matchningen överskrider en viss hastighet över tiden. Ange ett värde för `rateLimit` Egenskapen begränsar hastigheten för de begäranden som matchar regelvillkoret.

Regler för hastighetsbegränsning kan inte referera till WAF-flaggor. De är tillgängliga för alla Sites- och Forms-kunder.

### rateLimit-struktur {#ratelimit-structure}

| **Egenskap** | **Typ** | **Standard** | **MENING** |
|---|---|---|---|
| limit | heltal mellan 10 och 10000 | obligatoriskt | Begärandefrekvens (per CDN POP) i begäranden per sekund som regeln aktiveras för. |
| window | heltal: 1, 10 eller 60 | 10 | Provningsfönstret i sekunder för vilket begärandehastigheten beräknas. |
| påföljd | heltal mellan 60 och 3600 | 300 (5 minuter) | En period i sekunder för vilken matchande begäranden blockeras (avrundat till närmaste minut). |
| groupBy | array[Getter] | ingen | Räknaren för hastighetsbegränsning sammanställs av en uppsättning egenskaper för begäran (till exempel clientIp). |

### Exempel {#ratelimiting-examples}

**Exempel 1**

Den här regeln blockerar en klient i 5 m när den överskrider 100 req/sek (per CDN POP) under de senaste 60 sektionerna:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Exempel 2**

Blockera förfrågningar för 60-tal på sökvägen/kritisk/resurs när den överskrider 100 req/sek (per CDN POP) under de senaste 60 sektionerna:

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

Observera att CDN-loggar kan fördröjas upp till 5 minuter.

The `rules` egenskapen beskriver vilka trafikfilterregler som matchas och har följande mönster:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Till exempel:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Reglerna fungerar på följande sätt:

* Det kunddeklarerade regelnamnet för matchande regler visas i attributet match.
* Åtgärdsattributet anger om reglerna har en effekt av blockering, tillåtelse eller loggning.
* Om WAF är licensierat och aktiverat listas alla SWF-regler (t.ex. SQLI; observera att detta är oberoende av det kunddeklarerade namnet) som har identifierats, oavsett om SWF-reglerna har listats i konfigurationen.
* Om inga kunddeklarerade regler matchar och inga SWF-regler matchar, kommer egenskapen för regelattribut att vara tom.

I allmänhet visas matchande regler i loggposten för alla förfrågningar till CDN, oavsett om det är en CDN-träff, ett pass eller en miss. Däremot visas WAF-regler i loggposten endast för begäranden till CDN som betraktas som CDN-missar eller -pass, men inte CDN-träffar.

Exemplet nedan visar ett exempel `cdn.yaml` och två CDN-loggposter:


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

## Verktyg för instrumentpanel {#dashboard-tooling}

Adobe tillhandahåller en mekanism för att hämta instrumentpanelsverktyg till din dator för att importera CDN-loggar som hämtats via Cloud Manager. Med den här verktygen kan du analysera trafiken för att hitta rätt trafikfilterregler som ska deklareras, inklusive WAF-regler.

Kontrollpanelsverktygen kan klonas direkt från [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Github-arkiv.

[Se självstudiekursen](#tutorial) om du vill ha konkreta anvisningar om hur du använder kontrollpanelsverktygen.

## Självstudiekurs {#tutorial}

Adobe tillhandahåller en mekanism för att hämta instrumentpanelsverktyg till din dator för att importera CDN-loggar som hämtats via Cloud Manager. Med den här verktygen kan du analysera trafiken för att hitta rätt trafikfilterregler som ska deklareras, inklusive WAF-regler. Det här avsnittet innehåller först några instruktioner för att bli bekant med kontrollpanelsverktygen i en utvecklingsmiljö, följt av vägledning om hur du använder dessa kunskaper för att skapa regler i en produktmiljö.

Kontrollpanelsverktygen kan klonas direkt från [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) GitHub-databas.


### Bekanta dig med kontrollpanelsverktygen {#dashboard-getting-familiar}

1. Skapa en icke-produktionskonfigurationspipeline för Cloud Manager som är kopplad till en utvecklingsmiljö. Markera först **Distributionsförlopp** alternativ. Välj sedan **Målinriktad distribution**, Config, din databas, Git-grenen och ange kodplatsen till /config.

   ![Lägg till utvalda distributioner av icke-produktionspipeline](/help/security/assets/waf-select-pipeline1.png)

   ![Lägg till produktionsflöde som valts som mål](/help/security/assets/waf-select-pipeline2.png)

[I det här dokumentet finns mer information om hur du ställer in icke-produktionsrörledningar.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. Skapa en mappkonfiguration på rotnivå på arbetsytan och lägg till en fil med namnet `cdn.yaml`, där du deklarerar en enkel regel och anger den i loggläge i stället för i blockeringsläge.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. Verkställ och push-implementera ändringarna och distribuera konfigurationen med hjälp av konfigurationsflödet.

   ![Kör konfigurationsförlopp](/help/security/assets/waf-run-pipeline.png)

1. När konfigurationen har distribuerats kan du försöka komma åt den `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` med webbläsaren eller med kommandot Rulla nedan. Du bör få en felsida 404 eftersom den sidan inte finns.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Hämta CDN-loggarna från Cloud Manager och validera att reglerna matchar varandra som förväntat, med en regelegenskap som matchar regelnamnet:

   ```
   "rules": "match=log-rule-example"
   ```

   ![Välj hämtningsloggar](/help/security/assets/waf-download-logs1.png)

   ![Hämtningsloggar](/help/security/assets/waf-download-logs2.png)

1. Läs in Docker-bilden med kontrollpanelsverktygen och följ README för att importera CDN-loggarna. Välj rätt tidsperiod, rätt miljö och rätt filter enligt följande skärmbilder.

   ![Välj tid från kontrollpanelen](/help/security/assets/dashboard-select-time.png)

   ![Välj miljö från kontrollpanelen](/help/security/assets/dashboard-select-env.png)

1. När rätt filter har tillämpats bör du kunna se en kontrollpanel som har lästs in med förväntade data. På skärmbilden nedan har regelloggen-rule-example utlösts tre gånger under de senaste två timmarna av samma IP-adress som finns i Irland, med en webbläsare och bläddring.

   ![Visa DV-instrumentpanelsdata](/help/security/assets/dashboard-see-data-logmode.png)
   ![Visa widgetar för instrumentpanelsdata](/help/security/assets/dashboard-see-data-logmode2.png)

1. Ändra nu cdn.yaml så att regeln försätts i blockläge för att säkerställa att sidorna blockeras som förväntat. Utför sedan, push och utlöser konfigurationsflödet som tidigare.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. När konfigurationen har distribuerats kan du försöka komma åt den `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` med webbläsaren eller med kommandot Rulla nedan. Du bör få en felsida på 406 som anger att begäran blockerades.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Återigen hämtar du CDN-loggar i Cloud Manager (Obs! Det kan ta upp till 5 minuter innan nya begäranden visas i CDN-loggarna) och importerar dem till instrumentpanelsverktygen som vi gjorde tidigare. Uppdatera instrumentpanelen när du är klar. Som du kan se i skärmbilden nedan, begär `/log/me` är blockerade av vår regel.

   ![Visa produktkontrollpanelsdata](/help/security/assets/dashboard-see-data-blockmode.png)
   ![Visa produktkontrollpanelsdata](/help/security/assets/dashboard-see-data-blockmode2.png)

1. Om du har aktiverat WAF-trafikfilter (detta kräver ytterligare licens när funktionen är GA) upprepar du med en regel för WAF-trafikfilter, i loggläge och distribuerar reglerna.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
        when:
          reqProperty: tier
          matches: "author|publish"
        action:
          type: log
          wafFlags:
              - SANS
              - SIGSCI-IP
              - TORNODE
              - NOUA
              - SCANNER
              - USERAGENT
              - PRIVATEFILE
              - ABNORMALPATH
              - TRAVERSAL
              - NULLBYTE
              - BACKDOOR
              - LOG4J-JNDI
              - SQLI
              - XSS
              - CODEINJECTION
              - CMDEXE
              - NO-CONTENT-TYPE
              - UTF8
```

1. Använd ett verktyg som [nikto](https://github.com/sullo/nikto/tree/master) för att generera matchande begäranden. Kommandot nedan skickar runt 550 skadliga förfrågningar på mindre än en minut.

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. Hämta CDN-loggarna från Cloud Manager (kom ihåg att det kan ta upp till 5 minuter att visa dem) och validera att både de matchande deklarerade reglerna och WAF-flaggorna visas.

   Som ni ser flaggas flera av de förfrågningar som gjorts av Nikto av WAF som skadliga. Vi ser att Nikto försökte utnyttja säkerhetsluckorna CMDEXE, SQLI och NULLBYTE. Om du nu ändrar åtgärden från logg till block och återutlöser en skanning med Nikto blockeras alla tidigare flaggade begäranden den här gången.

   ![Visa WAF-data](/help/security/assets/dashboard-see-data-waf.png)


   Observera att när en begäran matchar någon av WAF-flaggorna, kommer dessa WAF-flaggor att visas, även om de inte är en del av den deklarerade regeln. Detta är så att du alltid är medveten om potentiellt ny skadlig trafik, som du ännu inte har deklarerat matchningsregler för. Exempel:

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. Upprepa med en regel som använder hastighetsbegränsning i loggläge. Som alltid, implementera, push och utlösa konfigurationsflödet för att tillämpa konfigurationen.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: limit-requests-client-ip
        when:
          reqProperty: tier
          matches: "author|publish"
        rateLimit:
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. Använd ett verktyg som [Vegeta](https://github.com/tsenart/vegeta) för att generera trafik.

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. När du har kört verktyget kan du hämta CDN-loggar och importera dem på kontrollpanelen för att verifiera att hastighetsbegränsningsregeln har utlösts

   ![Visa WAF-data](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![Visa WAF-data](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   Som du kan se vår regel **limit-requests-client-ip** har utlösts.

   Nu när du är bekant med hur trafikfilterregler fungerar kan du gå över till produktionsmiljön.

### Distribuera regler till produktionsmiljön {#dashboard-prod-env}

Se till att först deklarera regler i loggläge för att validera att det inte finns några falska positiva inställningar, vilket betyder legitim trafik som skulle blockeras felaktigt.

1. Skapa en produktionskonfigurationspipeline som är kopplad till produktionsmiljön.

1. Kopiera de rekommenderade reglerna nedan till cdn.yaml. Du kanske vill ändra reglerna baserat på de unika egenskaperna i webbplatsens livstrafik. Bekräfta, push och utlösa konfigurationsflödet. Kontrollera att reglerna är i loggläge.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
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
      action: log
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - SIGSCI-IP
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: log
        wafFlags:
          - CMDEXE
```

1. Lägg till eventuella ytterligare regler för att blockera skadlig trafik som du kanske känner till. Exempel: vissa IP-adresser som har attackerat din webbplats.

1. Efter några minuter, timmar eller dagar, beroende på webbplatsens trafikvolym, hämtar du CDN-loggar från Cloud Manager och analyserar dem med kontrollpanelen.

1. Här är några överväganden:
   1. Trafikmatchningsdeklarerade regler visas i diagram och begärandeloggar så att du enkelt kan kontrollera om dina deklarerade regler aktiveras.
   1. WAF-flaggor som matchar trafik visas i diagram och begärandeloggar, även om du inte loggade in dem i en regel. Detta för att ni alltid är medvetna om potentiellt ny skadlig trafik och kan skapa nya regler efter behov. Titta på WAF-flaggor som inte återspeglas i de deklarerade reglerna och överväg att deklarera dem.
   1. Om du vill hitta matchande regler kontrollerar du om det finns falskt positiva inställningar i förfrågningsloggarna och om du kan filtrera bort dem från reglerna. De kanske bara är falska positiva för vissa banor.

1. Ställ in lämpliga regler på blockläge och överväg även att lägga till ytterligare regler. Vissa av reglerna kanske ska vara i loggläge när du analyserar mer trafik.

1. Distribuera om konfigurationen.

1. Iterera och analysera instrumentpanelerna ofta.

