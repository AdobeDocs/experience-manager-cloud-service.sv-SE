---
title: Trafikfilterregler inklusive WAF-regler
description: Konfigurerar trafikfilterregler inklusive WAF-regler (Web Application Firewall).
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: f2616fb8f27d4f966243c3a43abedcc46ceff477
workflow-type: tm+mt
source-wordcount: '4053'
ht-degree: 0%

---


# Trafikfilterregler inklusive WAF-regler {#traffic-filter-rules-including-waf-rules}

Trafikfilterregler kan användas för att blockera eller tillåta förfrågningar i CDN-lagret, vilket kan vara användbart i scenarier som:

* Begränsa åtkomsten till specifika domäner till intern företagstrafik innan en ny webbplats publiceras
* Fastställande av hastighetsgränser som är mindre mottagliga för volymetriska DoS-attacker
* Förhindra att IP-adresser som du vet är skadliga riktas mot dina sidor

De flesta av dessa trafikfilterregler är tillgängliga för alla AEM as a Cloud Service Sites- och Forms-kunder. De arbetar huvudsakligen med egenskaper för begäran och begäranrubriker, inklusive IP, värdnamn, sökväg och användaragent.

En underkategori av trafikfilterregler kräver antingen en förbättrad säkerhetslicens eller en WAF-DDoS-skyddslicens. Dessa kraftfulla regler kallas trafikfilterregler för WAF (Web Application Firewall) (eller WAF-regler för kort) och har tillgång till de [WAF-flaggor](#waf-flags-list) som beskrivs senare i den här artikeln.

Trafikfilterregler kan distribueras via Cloud Manager konfigurationspipelines för att utveckla, fasa och producera miljötyper i produktionsprogram (icke-sandlådeprogram). Konfigurationsfilen kan distribueras till Rapid Development Environment (RDE) med kommandoradsverktyg.

[Följ igenom en självstudiekurs](#tutorial) för att snabbt bygga upp konkreta expertkunskaper om den här funktionen.

>[!NOTE]
>Mer information om hur du konfigurerar trafik på CDN, inklusive redigering av begäran/svar, deklarering av omdirigeringar och proxering till ett icke-AEM ursprung, finns i artikeln [Konfigurera trafik på CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md) .


## Hur den här artikeln ordnas {#how-organized}

Den här artikeln är indelad i följande avsnitt:

* **Trafikskydd - översikt:** Lär dig hur du skyddas från skadlig trafik.
* **Föreslagen process för konfigurering av regler:** Läs om en högnivåmetod för skydd av din webbplats.
* **Installation:** Upptäck hur du konfigurerar, konfigurerar och distribuerar trafikfilterregler, inklusive de avancerade WAF-reglerna.
* **Regelsyntax:** Läs om hur du deklarerar trafikfilterregler i konfigurationsfilen `cdn.yaml`. Detta omfattar både trafikfilterreglerna som är tillgängliga för alla Sites- och Forms-kunder och underkategorin WAF-regler för dem som licensierar den funktionen.
* **Regelexempel:** Se exempel på deklarerade regler för att du ska komma igång.
* **Regler för hastighetsbegränsning:** Lär dig hur du använder regler för hastighetsbegränsning för att skydda din webbplats från attacker med stora volymer.
* **Varningar om trafikfilterregler** Konfigurera varningar som ska meddelas när reglerna aktiveras.
* **Standardtrafikspik vid ursprungsvarning** Få meddelande när det finns en trafiktoppning vid det ursprung som tyder på en DDoS-attack.
* **CDN-loggar:** Se vad som deklarerats och WAF Flags matchar trafiken.
* **Kontrollpanelsverktyg:** Analysera CDN-loggarna för att hitta nya trafikfilterregler.
* **Rekommenderade startregler:** En uppsättning regler att komma igång med.
* **Självstudiekurs:** Praktiska kunskaper om funktionen, inklusive hur du använder instrumentpanelsverktyg för att deklarera rätt regler.

Adobe bjuder in dig att ge feedback eller ställa frågor om trafikfilterregler genom att skicka ett e-postmeddelande till **aemcs-waf-adopter@adobe.com**.

## Trafikskydd - översikt {#traffic-protection-overview}

I det digitala landskapet är skadlig trafik ett hot som aldrig tidigare förekommit. Adobe inser hur allvarlig risken är och erbjuder flera strategier för att skydda kundtillämpningar och mildra attacker när de inträffar.

Vid kanten absorberar det hanterade CDN-nätverket DoS-attacker i nätverkslagret (lager 3 och 4), inklusive översvämnings- och reflektions-/amplifieringsattacker.

Som standard vidtar Adobe åtgärder för att förhindra prestandaförsämringar på grund av oväntat höga trafikökningar över ett visst tröskelvärde. Om det inträffar en DoS-attack som påverkar webbplatsens tillgänglighet larmas Adobe ledningsgrupper och vidtar åtgärder för att minska risken.

Kunderna kan vidta förebyggande åtgärder för att mildra attacker i programlager (lager 7) genom att konfigurera regler i olika lager i innehållsleveransflödet.

På exempelvis Apache-lagret kan kunderna konfigurera antingen [Dispatcher-modulen](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter) eller [ModSecurity](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) för att begränsa åtkomsten till visst innehåll.

Som beskrivs i den här artikeln kan trafikfilterregler distribueras till det hanterade CDN-nätverket i Adobe med Cloud Manager [config pipelines.](/help/operations/config-pipeline.md) Utöver trafikfilterregler som baseras på egenskaper som IP-adress, sökväg och rubriker, eller regler som baseras på att hastighetsgränser anges, kan kunder även licensiera en kraftfull underkategori av trafikfilterregler som kallas WAF-regler.

## Föreslagen process {#suggested-process}

Nedan följer en högnivårekommenderad process från början till slut för att komma fram till rätt trafikfilterregler:

1. Konfigurera pipelines för icke-produktion och produktionskonfiguration enligt beskrivningen i avsnittet [Inställningar](#setup).
1. Kunder som har licensierat underkategorin till WAF trafikfilterregler bör aktivera dem i Cloud Manager.
1. Läs igenom och prova självstudiekursen för att få en större förståelse för hur man använder trafikfilterregler, inklusive WAF-regler om de har licensierats. I självstudiekursen får du hjälp med att distribuera regler till en utvecklingsmiljö, simulera skadlig trafik, hämta [CDN-loggarna](#cdn-logs) och analysera dem i [instrumentpanelsverktyget](#dashboard-tooling).
1. Kopiera de rekommenderade startreglerna till `cdn.yaml` och distribuera konfigurationen till produktionsmiljön i loggläge.
1. När du har samlat in trafik analyserar du resultatet med [instrumentpanelsverktyget](#dashboard-tooling) för att se om det finns några matchningar. Leta upp felaktiga positiva inställningar och gör eventuella nödvändiga justeringar för att aktivera startreglerna i blockläge.
1. Lägg till anpassade regler baserat på analys av CDN-loggarna, först testning med simulerad trafik i utvecklingsmiljöer innan driftsättning i scen- och produktionsmiljöer i loggläge, sedan blockläge.
1. Övervaka trafiken kontinuerligt och ändra reglerna allteftersom hotbilden utvecklas.

## Inställningar {#setup}

1. Skapa en fil `cdn.yaml` med en uppsättning trafikfilterregler, inklusive WAF-regler.

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

   Se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#common-syntax) för en beskrivning av egenskaperna ovanför noden `data`. Egenskapsvärdet `kind` ska anges till *CDN* och versionen ska anges till `1`.


1. Om WAF-regler är licensierade bör du aktivera funktionen i Cloud Manager enligt beskrivningen nedan för både nya och befintliga programscenarier.

   1. Om du vill konfigurera WAF för ett nytt program markerar du kryssrutan **WAF-DDOS Protection** på fliken **Säkerhet** när du [lägger till ett produktionsprogram.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Om du vill konfigurera WAF för ett befintligt program [redigerar du programmet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) och avmarkerar eller markerar alternativet **WAF-DDOS** när som helst på fliken **Säkerhet** .

1. Skapa en config pipeline i Cloud Manager, enligt beskrivningen i [Konfigurera pipelineartikeln.](/help/operations/config-pipeline.md#managing-in-cloud-manager) Pipelinen kommer att referera till en `config`-mapp på den översta nivån där filen `cdn.yaml` placeras någonstans under, se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#folder-structure).

## Syntax för trafikfilterregler {#rules-syntax}

Du kan konfigurera *trafikfilterregler* så att de matchar på mönster som IP, användaragent, begäranrubriker, värdnamn, geo och url.

Kunder som licensierar erbjudandet Förbättrat skydd eller WAF-DDoS-skydd kan även konfigurera en särskild kategori av trafikfilterregler som kallas *WAF trafikfilterregler* (eller WAF-regler för kort) som refererar till en eller flera [WAF-flaggor](#waf-flags-list).

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
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

Formatet på trafikfilterreglerna i filen `cdn.yaml` beskrivs nedan. Se några [andra exempel](#examples) i ett senare avsnitt och ett separat avsnitt om [Regler för hastighetsbegränsning](#rate-limit-rules).


| **Egenskap** | **De flesta trafikfilterreglerna** | **WAF trafikfilterregler** | **Typ** | **Standardvärde** | **Beskrivning** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Regelnamn (64 tecken långt, får bara innehålla alfanumeriska tecken och - ) |
| när | X | X | `Condition` | - | Den grundläggande strukturen är:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Se syntaxen för villkorsstruktur](#condition-structure) nedan, som beskriver get-metoder, predikatmetoder och hur du kombinerar flera villkor. |
| åtgärd | X | X | `Action` | logg | log-, allow-, block- eller Action-objekt. Standard är logg |
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
| **allOf** | `array[Condition]` | Åtgärden **och**. true om alla angivna villkor returnerar true |
| **anyOf** | `array[Condition]` | **eller**-åtgärd. true om något av villkoren i listan returnerar true |

**Getter**

| **Egenskap** | **Typ** | **Beskrivning** |
|---|---|---|
| reqProperty | `string` | Request-egenskap.<br><br>En av:<br><ul><li>`path`: Returnerar den fullständiga sökvägen för en URL utan frågeparametrarna. (använd `pathRaw` för varianten unescape)</li><li>`url`: Returnerar den fullständiga URL:en inklusive frågeparametrarna. (använd `urlRaw` för varianten unescape)</li><li>`queryString`: Returnerar frågedelen av en URL</li><li>`method`: Returnerar HTTP-metoden som används i begäran.</li><li>`tier`: Returnerar ett av `author`, `preview` eller `publish`.</li><li>`domain`: Returnerar egenskapen domain (enligt definition i rubriken `Host`) i gemener</li><li>`clientIp`: Returnerar klient-IP.</li><li>`forwardedDomain`: Returnerar den första domänen som definieras i huvudet `X-Forwarded-Host` i gemener</li><li>`forwardedIp`: Returnerar den första IP-adressen i huvudet `X-Forwarded-For`.</li><li>`clientCountry`: Returnerar en kod med två bokstäver ([Regional indikatorsymbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol)) som identifierar i vilket land klienten finns.</li></ul> |
| reqHeader | `string` | Returnerar begärandehuvud med angivet namn |
| queryParam | `string` | Returnerar frågeparameter med angivet namn |
| reqCookie | `string` | Returnerar cookie med angivet namn |
| postParam | `string` | Returnerar Post-parametern med det angivna namnet från begärandetexten. Fungerar bara när innehållet är av innehållstypen `application/x-www-form-urlencoded` |

**Förutse**

| **Egenskap** | **Typ** | **Betydelse** |
|---|---|---|
| **är lika med** | `string` | true om get-resultatet är lika med det angivna värdet |
| **doesNotEqual** | `string` | true om get-resultatet inte är lika med det angivna värdet |
| **gillar** | `string` | true om get-resultatet matchar angivet mönster |
| **notLike** | `string` | true om get-resultatet inte matchar det angivna mönstret |
| **träffar** | `string` | true om get-resultatet matchar angivet regex |
| **doesNotMatch** | `string` | true om get-resultatet inte matchar angivet regex |
| **in** | `array[string]` | true om den angivna listan innehåller get-resultat |
| **notIn** | `array[string]` | true om den angivna listan inte innehåller get-resultat |
| **finns** | `boolean` | true om värdet är true och egenskapen finns eller om värdet är false och egenskapen inte finns |

**Anteckningar**

* Egenskapen `clientIp` för begäran kan bara användas med följande predikat: `equals`, `doesNotEqual`, `in`, `notIn`. `clientIp` kan också jämföras med IP-intervall när predikaten `in` och `notIn` används. I följande exempel implementeras ett villkor för att utvärdera om en klient-IP ligger i IP-intervallet 192.168.0.0/24 (från 192.168.0.0 till 192.168.0.255):

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Adobe rekommenderar att du använder [regex101](https://regex101.com/) och [Snabbt sidindelning](https://fiddle.fastly.dev/) när du arbetar med regex. Du kan också lära dig mer om hur Snabbt hanterar regex från [snabb dokumentation - Reguljära uttryck i Fastly VCL](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes).


### Åtgärdsstruktur {#action-structure}

En `action` kan antingen vara en sträng som anger åtgärden (allow, block eller log), eller ett objekt som består av både åtgärdstypen (allow, block eller log) och alternativ som wafFlags och/eller status.

**Åtgärdstyper**

Åtgärderna prioriteras utifrån deras typer i följande tabell, som ordnas för att återspegla den ordning som åtgärderna utförs:

| **Namn** | **Tillåtna egenskaper** | **Betydelse** |
|---|---|---|
| **tillåt** | `wafFlags` (valfritt), `alert` (valfritt) | om wafFlags inte finns avbryter ytterligare regelbearbetning och fortsätter att ge svar. Om det finns wafFlags inaktiveras angivna WAF-skydd och ytterligare regelbearbetning fortsätter. <br>Om en varning anges skickas ett meddelande från Åtgärdscenter om regeln aktiveras 10 gånger i ett 5 minuter långt fönster. När en varning aktiveras för en viss regel utlöses den inte igen förrän nästa dag (UTC). |
| **block** | `status, wafFlags` (valfritt och exklusivt), `alert` (valfritt) | Om wafFlags inte finns returnerar HTTP-fel utan att alla andra egenskaper skickas, definieras felkoden av statusegenskapen eller så är standardvärdet 406. Om det finns wafFlags aktiverar det angivna WAF-skydd och fortsätter till ytterligare regelbearbetning. <br>Om en varning anges skickas ett meddelande från Åtgärdscenter om regeln aktiveras 10 gånger i ett 5 minuter långt fönster. När en varning aktiveras för en viss regel utlöses den inte igen förrän nästa dag (UTC). |
| **log** | `wafFlags` (valfritt), `alert` (valfritt) | loggar det faktum att regeln utlöstes, annars påverkas inte bearbetningen. wafFlags har ingen effekt. <br>Om en varning anges skickas ett meddelande från Åtgärdscenter om regeln aktiveras 10 gånger i ett 5 minuter långt fönster. När en varning aktiveras för en viss regel utlöses den inte igen förrän nästa dag (UTC). |

### WAF Flags List {#waf-flags-list}

Egenskapen `wafFlags`, som kan användas i de licensbara WAF-trafikfilterreglerna, kan referera till följande:

| **Flagga-ID** | **Flaggnamn** | **Beskrivning** |
|---|---|---|
| SQLI | SQL-inmatning | SQL Injection är ett försök att få åtkomst till ett program eller få privilegierad information genom att köra godtyckliga databasfrågor. |
| BAKDOOR | Bakdörr | En bakdörrssignal är en begäran som försöker avgöra om det finns en gemensam bakdörrsfil i systemet. |
| CMDEXE | Kommandokörning | Kommandokörning är ett försök att få kontroll över eller skada ett målsystem genom godtyckliga systemkommandon med hjälp av användarindata. |
| CMDEXE-NO-BIN | Kommandokörning förutom på `/bin/` | Ange samma skyddsnivå som `CMDEXE` när falskt positivt på `/bin` inaktiveras på grund av AEM arkitektur. |
| XSS | Skript för flera webbplatser | Korsskriptning mellan webbplatser är ett försök att kapa en användares konto eller webbläsarsession via skadlig JavaScript-kod. |
| TRAVERSAL | Kataloggenomgång | Directory Traversal är ett försök att navigera i behöriga mappar i ett system för att kunna hämta känslig information. |
| USERAGENT | Attackverktyg | Attack Tooling är användning av automatiserad programvara för att identifiera säkerhetsproblem eller för att försöka utnyttja en upptäckt säkerhetslucka. |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI-attacker försöker utnyttja [Log4Shell-sårbarheten](https://en.wikipedia.org/wiki/Log4Shell) som fanns i Log4J-versioner tidigare än 2.16.0 |
| BHH | Felaktiga Hop-huvuden | Felaktiga Hop-huvuden anger ett försök till HTTP-smuggling via en felformaterad Transfer-Encoding (TE) eller Content-Length (CL)-rubrik, eller en korrekt formaterad TE- och CL-rubrik |
| KODEINJEKTION | Kodinmatning | Kodinjektion är ett försök att få kontroll över eller skada ett målsystem genom godtyckliga programkodkommandon som användaren anger. |
| ABNORMALPATH | Onormal bana | Onormal sökväg anger att den ursprungliga sökvägen skiljer sig från den normaliserade sökvägen (till exempel normaliseras `/foo/./bar` till `/foo/bar`) |
| DUBBELKODNING | Dubbel kodning | Dubbel kodning används för att kontrollera om HTML-tecken med dubbel kodning kan användas |
| NOTUTF8 | Ogiltig kodning | Ogiltig kodning kan göra att servern översätter skadliga tecken från en begäran till ett svar, vilket kan orsaka denial of service eller XSS |
| JSON-ERROR | JSON-kodningsfel | En begärandetext för POST, PUT eller PATCH som har angetts som innehåller JSON i begärandehuvudet för Content-Type men som innehåller JSON-tolkningsfel. Detta beror ofta på ett programmeringsfel eller en automatiserad eller skadlig begäran. |
| MALFORMED-DATA | Felformaterade data i begärandetexten | En begärandetext för POST, PUT eller PATCH som har fel format enligt begärandehuvudet Content-Type. Om en begäranderubrik av typen&quot;Content-Type: application/x-www-form-urlencoded&quot; anges och innehåller en POST som är json. Detta är ofta ett programmeringsfel, en automatiserad eller skadlig begäran. Kräver agent 3.2 eller högre. |
| SANS | Skadlig IP-trafik | [SANS Internet Storm Center](https://isc.sans.edu/) - lista över rapporterade IP-adresser som har varit inblandade i skadlig aktivitet. |
| INNEHÅLLSTYP | Begäranhuvudet Content-Type saknas | En POST-, PUT- eller PATCH-begäran som inte har någon Content-Type-begäranderubrik. Som standard ska programservrar anta&quot;Content-Type: text/plain; charset=us-ascii&quot; i det här fallet. Många automatiska och skadliga förfrågningar kanske saknar&quot;Innehållstyp&quot;. |
| NOUA | Ingen användaragent | Anger att en begäran inte innehöll någon &quot;User-Agent&quot;-rubrik eller att rubrikvärdet inte har angetts. |
| TORNODE | Tor Traffic | Tor är programvara som döljer en användares identitet. En spik i Tor-trafiken kan indikera en angripare som försöker maskera sin plats. |
| NULLBYTE | Null byte | Null-byte visas normalt inte i en begäran och anger att begäran är felformaterad och potentiellt skadlig. |
| PRIVATEFILE | Privata filer | Privata filer är konfidentiella, till exempel en Apache `.htaccess`-fil eller en konfigurationsfil som kan läcka känslig information |
| SKANNER | Skanner | Identifierar vanliga skanningstjänster och verktyg |
| RESPONSESPLIST | HTTP-svarsdelning | Identifierar när CRLF-tecken skickas som indata till programmet för att mata in rubriker i HTTP-svaret |
| XML-FEL | XML-kodningsfel | En begärandetext för POST, PUT eller PATCH som har angetts som innehållande XML i begärandehuvudet för Content-Type men som innehåller XML-tolkningsfel. Detta beror ofta på ett programmeringsfel eller en automatiserad eller skadlig begäran. |
| DATACENTER | Datacenter | Identifierar att begäran kommer från en känd värdtjänstleverantör. Den här typen av trafik är vanligtvis inte kopplad till en riktig slutanvändare. |


## Överväganden {#considerations}

* När två konfliktskapande regler skapas har alltid de tillåtna reglerna företräde framför blockreglerna. Om du till exempel skapar en regel som blockerar en viss sökväg och en regel som tillåter en viss IP-adress, tillåts förfrågningar från den IP-adressen på den blockerade sökvägen.

* Om en regel matchas och blockeras svarar CDN med returkoden `406`.

* Konfigurationsfilerna bör inte innehålla hemligheter eftersom de skulle kunna läsas av alla som har åtkomst till Git-databasen.

* IP-tillåtelselista som definieras i Cloud Manager har högre prioritet än trafikfilterregler.

* WAF-regelmatchningar visas endast i CDN-loggar för CDN-missar och -pass, inte träffar.

## Exempel på regler {#examples}

Vissa regelexempel följer. Se avsnittet [tariffgräns](#rate-limit-rules) längre ned för exempel på regler för hastighetsbegränsning.

**Exempel 1**

Den här regeln blockerar begäranden från **IP 192.168.1.1**:

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

Den här regeln blockerar begäran på sökvägen `/helloworld` vid publicering med en användaragent som innehåller Chrome:

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

Den här regeln blockerar begäranden vid publicering som innehåller frågeparametern `foo`, men tillåter alla begäranden som kommer från IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Exempel 4**

Den här regeln blockerar begäranden till sökvägen `/block-me` vid publicering och blockerar alla begäranden som matchar ett `SQLI` - eller `XSS` -mönster. Det här exemplet innehåller en WAF-trafikfilterregel som refererar till `SQLI` och `XSS` [WAF Flags](#waf-flags-list) och därför kräver en separat licens.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
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

## Regler för hastighetsbegränsning

Ibland är det önskvärt att blockera trafik om den överskrider en viss frekvens av inkommande begäranden, baserat på ett visst villkor. Om du anger ett värde för egenskapen `rateLimit` begränsas hastigheten för de begäranden som matchar regelvillkoret.

Regler för hastighetsbegränsning kan inte referera till WAF-flaggor. De är tillgängliga för alla Sites- och Forms-kunder.

Kursen beräknas per CDN POP. Anta till exempel att POP i Montreal, Miami och Dublin har en trafikfrekvens på 80, 90 respektive 120 förfrågningar per sekund. Regeln för hastighetsbegränsning är satt till en gräns på 100. I så fall skulle endast trafiken till Dublin begränsas.

Hastighetsgränserna utvärderas baserat på antingen trafik som faller i kanten, trafik som faller i origo eller antalet fel.

### rateLimit-struktur {#ratelimit-structure}

| **Egenskap** | **Typ** | **Standard** | **MENAR** |
|---|---|---|---|
| limit | heltal mellan 10 och 10000 | obligatoriskt | Begärandefrekvens (per CDN POP) i begäranden per sekund som regeln aktiveras för. |
| window | heltal: 1, 10 eller 60 | 10 | Provningsfönstret i sekunder för vilket begärandehastigheten beräknas. Räknarnas noggrannhet beror på fönstrets storlek (större fönsternoggrannhet). Du kan till exempel förvänta dig 50 % noggrannhet för det sekundära fönstret och 90 % noggrannhet för det 60-sekundersfönstret. |
| påföljd | heltal mellan 60 och 3600 | 300 (5 minuter) | En period i sekunder för vilken matchande begäranden blockeras (avrundat till närmaste minut). |
| antal | alla, hämtningar, fel | alla | utvärderas baserat på edge-trafik (all), ursprungstrafik (hämtningar) eller antalet fel (fel). |
| groupBy | array[Getter] | ingen | Räknaren för hastighetsbegränsning sammanställs av en uppsättning egenskaper för begäran (till exempel clientIp). |

### Exempel {#ratelimiting-examples}

**Exempel 1**

Den här regeln blockerar en klient i 5 millisekunder när den överskrider ett genomsnitt på 60 req/sek (per CDN-POP) under de senaste 10 sektionerna:

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
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Exempel 2**

Blockera begäranden på sökvägen/critical/resource i 60 sekunder när det överskrider ett genomsnitt på 100 begäranden till ursprungsläget per sekund (per CDN POP) i ett tidsfönster på tio sekunder:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

## CVE-regler {#cve-rules}

Om WAF har licens tillämpar Adobe automatiskt blockeringsregler för att skydda mot många kända CVE-nummer (Common Vulnerabilities and Exposure), och nya CVE-nummer kan läggas till snart de har upptäckts. Kunder bör inte och behöver inte konfigurera själva CVE-reglerna.

Om en trafikbegäran matchar en CVE-fil visas den i motsvarande CDN-loggpost.

Kontakta Adobe support om det finns frågor om en viss CVE eller om det finns en viss CVE-regel som din organisation vill inaktivera.

## Varningar om trafikfilterregler {#traffic-filter-rules-alerts}

En regel kan konfigureras att skicka ett meddelande från Åtgärdscenter om det aktiveras tio gånger inom ett 5 minuter långt fönster. En sådan regel varnar dig när vissa trafikmönster förekommer så att du kan vidta nödvändiga åtgärder. När en varning aktiveras för en viss regel utlöses den inte igen förrän nästa dag (UTC).

Läs mer om [Åtgärdscenter](/help/operations/actions-center.md), inklusive hur du konfigurerar de meddelandeprofiler som krävs för att ta emot e-postmeddelanden.

![Åtgärdscentermeddelande](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


Varningsegenskapen kan användas för åtgärdsnoden för alla åtgärdstyper (allow, block, log).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## Standardtrafikspik vid ursprungsvarning {#traffic-spike-at-origin-alert}

Ett e-postmeddelande från [Åtgärdscenter](/help/operations/actions-center.md) skickas när en stor mängd trafik skickas till ursprungsläget, där ett högt tröskelvärde för begäranden kommer från samma IP-adress, vilket tyder på en DDoS-attack.

Om detta undantag uppfylls blockerar Adobe trafiken från den IP-adressen, men vi rekommenderar att du vidtar ytterligare åtgärder för att skydda ditt ursprung, inklusive att konfigurera trafikfilterregler för hastighetsbegränsning så att trafiktoppar vid lägre tröskelvärden blockeras. Se självstudiekursen [Blockera DoS- och DDoS-attacker med trafikregler](#tutorial-blocking-DDoS-with-rules) för en guidad genomgång.

Den här varningen är aktiverad som standard, men kan inaktiveras med egenskapen *defaultTrafficAlerts* inställd på false. När varningen har utlösts kommer den inte att utlösas igen förrän nästa dag (UTC).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## CDN-loggar {#cdn-logs}

AEM as a Cloud Service ger åtkomst till CDN-loggar, som är användbara för fall som till exempel optimering av träffar i cache och konfigurering av trafikfilterregler. CDN-loggar visas i dialogrutan **Hämta loggar** i Cloud Manager när du väljer tjänsten Författare eller Publish.

CDN-loggar kan fördröjas upp till fem minuter.

Egenskapen `rules` beskriver vilka trafikfilterregler som matchas och har följande mönster:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Till exempel:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Reglerna fungerar på följande sätt:

* Alla matchande regelnamn som har deklarerats av kunden listas i attributet `match`.
* Attributet `action` avgör om regelblocket, tillåt eller loggen ska användas.
* Om WAF är licensierat och aktiverat visar attributet `waf` alla WAF-flaggor (till exempel SQLI) som har identifierats. Detta gäller oavsett om WAF-flaggorna har listats i några regler eller inte. Detta är för att ge insikter i eventuella nya regler att deklarera.
* Egenskapen `rules` är tom om inga kunddeklarerade regler matchar och inga SWF-regler matchar.

Som tidigare nämnts visas matchningar av WAF-regler endast i CDN-loggar för CDN-missar och -pass, inte träffar.

I exemplet nedan visas ett exempel på `cdn.yaml` och två CDN-loggposter:


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
| *cli_country* | [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2-landskod med två bokstäver för klientlandet. |
| *rid* | Värdet på begärandehuvudet som används för att unikt identifiera begäran. |
| *req_ua* | Användaragenten som ansvarar för att göra en given HTTP-begäran. |
| *värd* | Den myndighet som begäran avser. |
| *url* | Den fullständiga sökvägen, inklusive frågeparametrar. |
| *metod* | HTTP-metod som skickas av klienten, till exempel &quot;GET&quot; eller &quot;POST&quot;. |
| *res_type* | Den innehållstyp som används för att ange resursens ursprungliga medietyp. |
| *cache* | Status för cachen. Möjliga värden är HIT, MISS eller PASS |
| *status* | HTTP-statuskoden som ett heltalsvärde. |
| *res_age* | Den tid (i sekunder) som ett svar har cachelagrats (i alla noder). |
| *pop* | Datacenter för CDN-cacheservern. |
| *regler* | Namnet på matchande regler.<br><br>Anger också om matchningen resulterade i ett block. <br><br>Exempel: `match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`<br><br>Tom om inga regler matchar. |

## Verktyg för instrumentpanel {#dashboard-tooling}

Adobe tillhandahåller en mekanism för att hämta instrumentpanelsverktyg till din dator för att importera CDN-loggar som hämtats via Cloud Manager. Med den här verktygen kan du analysera trafiken för att hitta rätt trafikfilterregler som ska deklareras, inklusive WAF-regler.

Instrumentpanelsverktygen kan klonas direkt från GitHub-databasen [AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling).

[Tutorials](#tutorial) finns för konkreta instruktioner om hur du använder instrumentpanelsverktygen.

## Rekommenderade startregler {#recommended-starter-rules}

Du kan kopiera de rekommenderade reglerna nedan till din `cdn.yaml` för att komma igång. Starta i loggläge, analysera trafiken och när du är nöjd ändras den till blockläge. Du kanske vill ändra reglerna baserat på de unika egenskaperna för webbplatsens livstrafik.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
    - name: block-ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```

## Självstudiekurser {#tutorial}

Det finns två självstudiekurser.

### Skydda webbplatser med trafikfilterregler (inklusive WAF regler) {#tutorial-protecting-websites}

[Arbeta igenom en självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview) för att få allmän, praktisk kunskap och erfarenhet om trafikfilterregler, inklusive WAF regler.

Självstudiekursen leder dig igenom:

* Ställa in Cloud Manager konfigurationsflöde
* Använda verktyg för att simulera skadlig trafik
* Deklarera trafikfilterregler, inklusive WAF-regler
* Analysera resultat med kontrollpanelsverktyg
* God praxis

### Blockera DoS- och DDoS-attacker med trafikfilterregler {#tutorial-blocking-DDoS-with-rules}

[Detaljerad information om hur du blockerar ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/blocking-dos-attack-using-traffic-filter-rules) DoS-attacker (Denial of Service) och DDoS-attacker (Distributed Denial of Service) med trafikfilterregler för hastighetsbegränsning och andra strategier.

Självstudiekursen leder dig igenom:

* skydd
* få meddelanden när hastighetsgränserna överskrids
* analysera trafikmönster med kontrollpanelsverktyg för att konfigurera tröskelvärden för trafikfilterregler för hastighetsbegränsning



