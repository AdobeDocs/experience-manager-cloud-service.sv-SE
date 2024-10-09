---
title: Anpassade regler för kodkvalitet
description: På den här sidan beskrivs de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av testningen av kodkvalitet. De bygger på god praxis från Adobe Experience Manager Engineering.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '4513'
ht-degree: 0%

---

# Anpassade regler för kodkvalitet {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Anpassade regler för kodkvalitet"
>abstract="På den här sidan beskrivs de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av testningen av kodkvalitet. De bygger på god praxis från Adobe Experience Manager Engineering."

Den här sidan beskriver de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av [kodkvalitetstestningen](/help/implementing/cloud-manager/code-quality-testing.md). De bygger på god praxis från Experience Manager Engineering.

>[!NOTE]
>
>Fullständiga SonarQube-regler kan inte laddas ned på grund av Adobe egna information. Du kan hämta den fullständiga listan med regler [med den här länken](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx). Fortsätt läsa det här dokumentet för beskrivningar och exempel på reglerna.

>[!NOTE]
>
>De kodexempel som anges här är endast avsedda som illustrationer. Mer information om SonarQube-koncept och kvalitetsregler finns i SonarQube [Concepts-dokumentationen](https://docs.sonarqube.org/latest/).

## SonarQube-regler {#sonarqube-rules}

Följande avsnitt innehåller information om SonarQube-regler som körs av Cloud Manager.

### Använd inte potentiellt farliga funktioner {#do-not-use-potentially-dangerous-functions}

* **Nyckel**: CQRules:CWE-676
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Metoderna `Thread.stop()` och `Thread.interrupt()` kan skapa problem som är svåra att återge och ibland säkerhetsproblem. Deras användning bör övervakas noggrant och valideras. I allmänhet är meddelandeöverföring ett säkrare sätt att uppnå samma sak.

#### Kod som inte uppfyller kraven {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### Kompatibel kod {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### Använd inte formatsträngar som kan vara externt kontrollerade {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Nyckel**: CQRules:CWE-134
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Om du använder en formatsträng från en extern källa (t.ex. en begärandeparameter eller ett användargenererat innehåll) kan programmet utsättas för denial of service-attacker. Det finns tillfällen då en formatsträng kan styras externt, men bara tillåts från betrodda källor.

#### Kod som inte uppfyller kraven {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP-begäranden ska alltid ha socket- och anslutningstimeout {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Nyckel**: CQRules:ConnectionTimeoutMechanism
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.6.0

När HTTP-begäranden körs inifrån ett Experience Manager-program är det viktigt att se till att rätt tidsgränser är konfigurerade för att undvika onödig trådförbrukning. Tyvärr är standardbeteendet för både Java™ standardklient för HTTP (`java.net.HttpUrlConnection`) och den vanligaste Apache HTTP Components-klienten aldrig timeout, så timeout måste anges explicit. Dessutom bör dessa timeout inte vara längre än 60 sekunder.

#### Kod som inte uppfyller kraven {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### Kompatibel kod {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis () {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### Stäng alltid ResursResolver-objekt {#resourceresolver-objects-should-always-be-closed}

* **Nyckel**: CQRules:CQBP-72
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

`ResourceResolver` objekt som hämtats från `ResourceResolverFactory` förbrukar systemresurser. Även om det finns åtgärder för att återta dessa resurser när `ResourceResolver` inte längre används, är det mer effektivt att uttryckligen stänga alla öppna `ResourceResolver`-objekt genom att anropa metoden `close()`.

En relativt vanlig missuppfattning är att `ResourceResolver` objekt som skapats med en befintlig JCR-session inte får stängas explicit eller att det gör det stänger den underliggande JCR-sessionen. Detta är inte fallet. Oavsett hur en `ResourceResolver` öppnas bör den stängas när den inte längre används. Eftersom `ResourceResolver` implementerar gränssnittet `Closeable` går det också att använda syntaxen `try-with-resources` i stället för att anropa `close()` explicit.

#### Kod som inte uppfyller kraven {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Kompatibel kod {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### Använd inte SSLING-serversökvägar för att registrera servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Nyckel**: CQRules:CQBP-75
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Så som beskrivs i [Sling-dokumentationen](https://sling.apache.org/documentation/the-sling-engine/servlets.html) rekommenderas inte bindningar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

#### Kod som inte uppfyller kraven {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Undantag som fångas upp ska loggas eller kastas, inte båda {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Nyckel**: CQRules:CQBP-44—CatchAndeitherLogOrThrow
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

I allmänhet bör ett undantag loggas exakt en gång. Om du loggar undantag flera gånger kan det leda till missförstånd eftersom det är oklart hur många gånger ett undantag inträffade. Det vanligaste mönstret som leder till detta är loggning och generering av ett fångat undantag.

#### Kod som inte uppfyller kraven {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### Kompatibel kod {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### Undvik loggsatser som omedelbart följs av en throw-sats {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Nyckel**: CQRules:CQBP-44 - ConsecutiousLogAndThrow
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Ett annat vanligt sätt att undvika är att logga ett meddelande och sedan omedelbart generera ett undantag. Den här proceduren innebär vanligtvis att undantagsmeddelandet kommer att dupliceras i loggfiler.

#### Kod som inte uppfyller kraven {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Kompatibel kod {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Undvik att logga på INFO när du hanterar GET- eller HEAD-förfrågningar {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Nyckel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och Experience Manager är som standard konfigurerad för att logga på INFO-nivå eller högre. Metoderna GET och HEAD bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. Loggning vid hantering av GET- eller HEAD-begäranden bör finnas antingen på WARN- eller FEL-nivå när något har gått fel eller på DEBUG- eller TRACE-nivå om mer detaljerad felsökningsinformation skulle vara till hjälp.

>[!NOTE]
>
>Detta gäller inte loggning av typen `access.log` för varje begäran.

#### Kod som inte uppfyller kraven {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Kompatibel kod {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Använd inte Exception.getMessage() som första parameter i en loggningssats {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Nyckel**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som en god praxis bör loggmeddelanden innehålla sammanhangsberoende information om var i programmet ett undantag har inträffat. Kontexten kan också bestämmas med stackspår, men i allmänhet blir loggmeddelandet lättare att läsa och förstå. När du loggar ett undantag är det därför en dålig vana att använda undantagets meddelande som loggmeddelande. Undantagsmeddelandet innehåller det som gick fel medan loggmeddelandet bör användas för att tala om för en loggläsare vad programmet gjorde när undantaget inträffade. Undantagsmeddelandet är fortfarande loggat. Genom att ange ett eget meddelande blir loggarna lättare att förstå.

#### Kod som inte uppfyller kraven {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Kompatibel kod {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Inloggning av catch-block ska ske på WARN- eller ERROR-nivå {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Nyckel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som namnet antyder bör Java™-undantag alltid användas i undantagsfall. Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp, antingen WARN eller ERROR. Detta garanterar att meddelandena visas korrekt i loggarna.

#### Kod som inte uppfyller kraven {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Kompatibel kod {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Skriv inte ut stackspår till konsolen {#do-not-print-stack-traces-to-the-console}

* **Nyckel**: CQRules:CQBP-44—ExceptionPrintStackTrace
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som vi nämnt är sammanhang viktigt när du ska förstå loggmeddelanden. Om `Exception.printStackTrace()` används kommer endast stackspårningen att skickas till standardfelströmmen, vilket innebär att all kontext förloras. Om flera undantag skrivs ut med den här metoden parallellt i ett program med flera trådar, som Experience Manager, kan stackspårningarna överlappa, vilket kan skapa stor förvirring. Undantag bör endast loggas via loggningsramverket.

#### Kod som inte uppfyller kraven {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Kompatibel kod {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Exportera inte till standardutdata eller standardfel {#do-not-output-to-standard-output-or-standard-error}

* **Nyckel**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Loggning i Experience Manager ska alltid ske via loggningsramverket (SLF4J). Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket. Ibland kan det orsaka prestandaproblem.

#### Kod som inte uppfyller kraven {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Kompatibel kod {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Undvik hårdkodade sökvägar för /appar och /libs {#avoid-hardcoded-apps-and-libs-paths}

* **Nyckel**: CQRules:CQBP-71
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Vanligtvis ska sökvägar som börjar med `/libs` och `/apps` inte vara hårdkodade eftersom de sökvägar de refererar till oftast lagras som sökvägar i förhållande till sökvägen för Sling, som är inställd på `/libs,/apps` som standard. Om du använder den absoluta sökvägen kan det orsaka subtila defekter som bara skulle visas senare i projektets livscykel.

#### Kod som inte uppfyller kraven {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Kompatibel kod {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Använd inte Sling-schemaläggare {#sonarqube-sling-scheduler}

* **Nyckel**: CQRules:AMSCORE-554
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Använd inte Sling Scheduler för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Läs [Apache Sling-händelser och jobbhantering](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) om du vill veta mer om hur Sling-jobb hanteras i klustrade miljöer.

### Använd inte inaktuella API:er från Experience Manager {#sonarqube-aem-deprecated}

* **Nyckel**: AMSCORE-553
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

API-ytan i Experience Manager är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

Dessa API:er är ofta föråldrade med Java™ `@Deprecated`-standardanteckningen och, som sådan, som identifieras av `squid:CallToDeprecatedMethod`.

Det finns dock fall där en API är inaktuell i Experience Manager men inte kan användas i andra sammanhang. Den här regeln identifierar den andra klassen.

### Använd inte @Inject-anteckning med @Optional i Sling-modeller {#sonarqube-slingmodels-inject-optional}

* **Nyckel**: InjectAnnotationWithOptionalInjectionCheck
* **Typ**: Programkvalitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.11

Apache Sling-projektet avråder från att använda `@Inject`-anteckningen i kontexten för Sling-modeller, eftersom det kan leda till sämre prestanda när det kombineras med `DefaultInjectionStrategy.OPTIONAL` (antingen på fält- eller klassnivå). I stället bör mer specifika injektioner (som `@ValueMapValue` eller `@OsgiInjector` anteckningar) användas.

Läs [dokumentationen för Apache Sling](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1) om du vill ha mer information om de rekommenderade anteckningarna och varför den här rekommendationen gjordes från början.


### Återanvänd instanser av en HTTPClient {#sonarqube-reuse-httpclient}

* **Nyckel**: AEMSRE-870
* **Typ**: Programkvalitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.11

AEM når ofta ut till andra program med HTTP-protokollet, och Apache HttpClient är ett bibliotek som ofta används för att uppnå detta. Men när du skapar ett sådant HttpClient-objekt får du en del overhead, så dessa objekt bör återanvändas så mycket som möjligt.

Den här regeln kontrollerar att ett sådant HttpClient-objekt inte är privat inom en metod, utan globalt på en klassnivå, så att det kan återanvändas. I det här fallet ska httpClient-fältet anges i konstruktorn för klassen eller metoden `activate()` (om den här klassen är en OSGi-komponent/tjänst).

Läs [Optimeringsguiden](https://hc.apache.org/httpclient-legacy/performance.html) för HttpClient om du vill veta mer om hur du använder HttpClient.

#### Kod som inte uppfyller kraven {#non-compliant-code-14}

```java
public void doHttpCall() {
  HttpClient httpclient = HttpClients.createDefault();
  // do something with the httpclient
}
```

#### Kompatibel kod {#compliant-code-11}

```java
public class myClass {

  HttpClient httpclient;

  public void doHttpCall() {
    // do something with the httpclient
  }

}
```

## OakPAL-innehållsregler {#oakpal-rules}

I följande avsnitt beskrivs de OakPAL-kontroller som utförs av Cloud Manager.

>[!NOTE]
>
>OakPAL är ett ramverk som validerar innehållspaket med en fristående Oak-databas. Den utvecklades av en Experience Manager-partner och vinnare av utmärkelsen Experience Manager Rockstar North America 2019.

### Produkt-API:er som annoterats med @ProviderType ska inte implementeras eller utökas av kunder {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Nyckel**: CQBP-84
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.7.0

API:t för Experience Manager innehåller Java™-gränssnitt och -klasser som endast är avsedda att användas - men inte implementeras - av anpassad kod. Gränssnittet `com.day.cq.wcm.api.Page` ska till exempel endast implementeras av Experience Manager.

När nya metoder läggs till i dessa gränssnitt påverkar dessa ytterligare metoder inte befintlig kod som använder dessa gränssnitt. Det betyder att tillägg av nya metoder i dessa gränssnitt anses vara bakåtkompatibelt. Men om anpassad kod implementerar ett av dessa gränssnitt har den anpassade koden introducerat en bakåtkompatibilitetsrisk för kunden.

Gränssnitt och klasser - som implementerats av Experience Manager - antecknas med `org.osgi.annotation.versioning.ProviderType` eller ibland en liknande äldre anteckning `aQute.bnd.annotation.ProviderType`. Den här regeln identifierar de fall där ett sådant gränssnitt implementeras eller en klass utökas av anpassad kod.

#### Kod som inte uppfyller kraven {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Anpassade Lucene Oak-index måste ha en Tika-konfiguration {#oakpal-indextikanode}

* **Nyckel**: IndexTikaNode
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: 2021.8.0

Flera färdiga Experience Manager Oak-index innehåller en Tika-konfiguration och anpassningar av dessa index måste innehålla en Tika-konfiguration. Den här regeln söker efter anpassningar av indexen `damAssetLucene`, `lucene` och `graphqlConfig` och aktiverar ett problem om `tika`  noden saknas eller om `tika` -noden saknar en underordnad nod med namnet `config.xml`.

Mer information om hur du anpassar indexdefinitioner finns i [indexeringsdokumentation](/help/operations/indexing.md#preparing-the-new-index-definition).

#### Kod som inte uppfyller kraven {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### Kompatibel kod {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Oak-index för anpassade Lucene får inte vara synkrona {#oakpal-indexasync}

* **Nyckel**: IndexAsyncProperty
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: 2021.8.0

Oak-index av typen `lucene` måste alltid indexeras asynkront. Om du inte gör detta kan det leda till att systemet blir instabilt. Mer information om strukturen för Lucene-index finns i [Oak-dokumentationen](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition).

#### Kod som inte uppfyller kraven {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      - tags: [visualSimilaritySearch]
      + tika
        + config.xml
```

#### Kompatibel kod {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Oak-index för anpassade DAM-tillgångar är korrekt strukturerade  {#oakpal-damAssetLucene-sanity-check}

* **Nyckel**: IndexDamAssetLucene
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: 2021.6.0

För att resurssökning ska fungera korrekt i Experience Manager Assets måste anpassningar av Oak-indexet `damAssetLucene` följa en uppsättning riktlinjer som är specifika för det här indexet. Den här regeln kontrollerar att indexdefinitionen måste ha en flervärdesegenskap med namnet `tags` som innehåller värdet `visualSimilaritySearch`.

#### Kod som inte uppfyller kraven {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      + tika
        + config.xml
```

#### Kompatibel kod {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Kundpaket får inte skapa eller ändra noder under /libs {#oakpal-customer-package}

* **Nyckel**: BannedPath
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2019.6.0

Det har varit en god vana att innehållsträdet `/libs` i Experience Manager-innehållsdatabasen alltid ska betraktas som skrivskyddat av kunder. Att ändra noder och egenskaper under `/libs` innebär en betydande risk för större och mindre uppdateringar. Ändringar av `/libs` måste göras av Adobe via officiella kanaler.

### Paket får inte innehålla dubbla OSGi-konfigurationer {#oakpal-package-osgi}

* **Nyckel**: DuplicateOsgiConfigurations
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Ett vanligt problem som inträffar i komplexa projekt är när samma OSGi-komponent konfigureras flera gånger. Detta skapar en tvetydighet om vilken konfiguration som är tillämplig. Den här regeln är&quot;körningsmedveten&quot; eftersom den bara identifierar problem där samma komponent har konfigurerats flera gånger i samma körningsläge eller en kombination av körningslägen.

>[!NOTE]
>
>Den här regeln ger problem där samma konfiguration, med samma sökväg, definieras i flera paket, inklusive fall där samma paket dupliceras i den övergripande listan med inbyggda paket.
>
>Om bygget till exempel skapar paket med namnet `com.myco:com.myco.ui.apps` och `com.myco:com.myco.all` där `com.myco:com.myco.all` bäddar in `com.myco:com.myco.ui.apps`, rapporteras alla konfigurationer i `com.myco:com.myco.ui.apps` som dubbletter.
>
>Detta är vanligtvis ett fall där [riktlinjerna för innehållspaketets struktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md) inte följs. I det här specifika exemplet saknar paketet `com.myco:com.myco.ui.apps` egenskapen `<cloudManagerTarget>none</cloudManagerTarget>`.

#### Kod som inte uppfyller kraven {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Kompatibel kod {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Konfigurations- och installationsmappar får endast innehålla OSGi-noder {#oakpal-config-install}

* **Nyckel**: ConfigAndInstallShouldOnlyContainOsgiNodes
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Av säkerhetsskäl kan sökvägar som innehåller `/config/` och `/install/` bara läsas av administrationsanvändare i Experience Manager och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller dessa segment, kommer programbeteendet att variera oavsiktligt mellan administrativa och icke-administrativa användare.

Ett vanligt problem är att använda noder med namnet `config` i komponentdialogrutor eller när du anger RTF-redigerarkonfigurationen för intern redigering. För att lösa det här problemet bör namnet på den felande noden ändras till ett kompatibelt namn. Använd egenskapen `configPath` på noden `cq:inplaceEditing` för att ange den nya platsen för RTF-redigerarkonfigurationen.

#### Kod som inte uppfyller kraven {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Kompatibel kod {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Paket får inte överlappa {#oakpal-no-overlap}

* **Nyckel**: PackageOverlaps
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2019.6.0

Ungefär som [Paket får inte innehålla regeln för duplicerade OSGi-konfigurationer](#oakpal-package-osgi) är detta ett vanligt problem i komplexa projekt där samma nodsökväg skrivs till av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara ett klassiskt användargränssnitt {#oakpal-default-authoring}

* **Nyckel**: ClassicUIAuthoringMode
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i Experience Manager. Eftersom det klassiska användargränssnittet har tagits bort sedan Experience Manager 6.4, uppstår nu ett problem när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor bör ha dialogrutor med pekskärmsgränssnitt {#oakpal-components-dialogs}

* **Nyckel**: ComponentWithOnlyClassicUIDialog
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Experience Manager-komponenter som har en klassisk användargränssnittsdialogruta bör alltid ha en motsvarande dialogruta för användargränssnittet. Båda ger en optimal redigeringsupplevelse och är kompatibla med Cloud Servicens distributionsmodell, där det klassiska användargränssnittet inte stöds. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk gränssnittsdialogruta (d.v.s. en underordnad `dialog`-nod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en underordnad `cq:dialog`-nod).
* En komponent med en klassisk dialogruta för användargränssnittsdesign (d.v.s. en `design_dialog`-nod) måste ha en motsvarande designdialogruta för användargränssnittet (d.v.s. en underordnad `cq:design_dialog`-nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för Experience Manager Moderniseringsverktyg innehåller dokumentation och verktyg för hur du konverterar komponenter från det klassiska användargränssnittet till Touch-användargränssnittet. Mer information finns i [dokumentationen för Experience Manager Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/).

### Paket får inte innehålla både muterbara och oföränderliga {#oakpal-packages-immutable}

* **Nyckel**: ImmutableMutableMixedPackage
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

För att vara kompatibel med databasens distributionsmodell måste enskilda innehållspaket innehålla antingen innehåll för de oföränderliga områdena i databasen (`/apps` och `/libs`) eller det ändringsbara området (allt inte i `/apps` eller `/libs`), men inte båda. Ett paket som innehåller både `/apps/myco/components/text` och `/etc/clientlibs/myco` är till exempel inte kompatibelt med Cloud Service och orsakar att ett problem rapporteras.

>[!NOTE]
>
>Regeln [Kundpaket får inte skapa eller ändra noder under /libs](#oakpal-customer-package) gäller alltid.

Mer information finns i [Projektstruktur för Experience Manager](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

### Använd inte agenter för omvänd replikering {#oakpal-reverse-replication}

* **Nyckel**: ReverseReplication
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i distributioner av Cloud Service, vilket beskrivs i [versionsinformationen för Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md#replication-agents).

Kunder som använder omvänd replikering bör kontakta Adobe för att få alternativa lösningar.

### Resurser i proxyaktiverade klientbibliotek bör finnas i en mapp med namnet resources {#oakpal-resources-proxy}

* **Nyckel**: ClientlibProxyResource
* **Typ**: Fel
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Klientbibliotek i Experience Manager kan innehålla statiska resurser som bilder och teckensnitt. Så som beskrivs i dokumentet [Använda preprocessorer](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) måste dessa statiska resurser finnas i en underordnad mapp med namnet `resources` för att effektivt kunna refereras till på publiceringsinstanserna när du använder proxiderade klientbibliotek.

#### Kod som inte uppfyller kraven {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Kompatibel kod {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Användning av arbetsflödesprocesser som inte är kompatibla med Cloud Service {#oakpal-usage-cloud-service}

* **Nyckel**: CloudServiceIncompatibleWorkflowProcess
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2021.2.0

I och med övergången till tillgångsmikrotjänster för tillgångsbearbetning på Experience Manager as a Cloud Service har flera arbetsflödesprocesser som användes på plats och i AMS-versioner av Experience Manager blivit antingen ostödda eller onödiga.

Migreringsverktyget i [Experience Manager as a Cloud Service Assets GitHub-databasen](https://github.com/adobe/aem-cloud-migration) kan användas för att uppdatera arbetsflödesmodeller under migrering till Experience Manager as a Cloud Service.

### Användning av statiska mallar rekommenderas inte för redigerbara mallar {#oakpal-static-template}

* **Nyckel**: StaticTemplateUsage
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Även om det historiskt sett är vanligt att använda statiska mallar i Experience Manager-projekt rekommenderar Adobe redigerbara mallar eftersom de ger den flexibilitet och stöder ytterligare funktioner som inte finns i statiska mallar. Mer information finns i dokumentet [Sidmallar](/help/implementing/developing/components/templates.md).

Migrering från statiska till redigerbara mallar kan till stor del automatiseras med [Experience Manager Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### Användning av äldre baskomponenter rekommenderas inte {#oakpal-usage-legacy}

* **Nyckel**: LegacyFoundationComponentUsage
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

De äldre Foundation-komponenterna (d.v.s. komponenterna under `/libs/foundation`) har tagits bort för flera Experience Manager-versioner till förmån för Core-komponenterna. Användning av Foundation Components som grund för anpassade komponenter (oavsett om de är övertäckningar eller arv) rekommenderas inte och bör konverteras till motsvarande Core Components.

Den här konverteringen kan underlättas med [Experience Manager Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/).

### Använd endast namn och ordning för körningsläge som stöds {#oakpal-supported-runmodes}

* **Nyckel**: SupportedRunmode
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service har en strikt namngivningsprincip för körningslägesnamn och en strikt ordning för dessa körningslägen. En lista över körningslägen som stöds finns i dokumentet [Distribuera till Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) och alla avvikelser från detta identifieras som ett problem.

### Definitionsnoder för anpassade sökindex måste vara direkt underordnade /oak:index {#oakpal-custom-search}

* **Nyckel**: OakIndexLocation
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) ska vara direkt underordnade noder till `/oak:index`. Index på andra platser måste flyttas för att vara kompatibla med Experience Manager as a Cloud Service. Mer information om sökindex finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md).

### Definitionsnoder för anpassade sökindex måste ha en compatVersion av 2 {#oakpal-custom-search-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (till exempel noder av typen `oak:QueryIndexDefinition`) måste ha egenskapen `compatVersion` inställd på `2`. Alla andra värden stöds inte av Experience Manager as a Cloud Service. Mer information om sökindex finns i [Innehållssökning och indexering](/help/operations/indexing.md).

### Underordnade noder för anpassade sökindexdefinitionsnoder måste vara av typen nt:undefined {#oakpal-descendent-nodes}

* **Nyckel**: IndexDescendantNodeType
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det är svårt att felsöka problem när en anpassad sökindexdefinitionsnod har oordnade underordnade noder. För att undvika detta rekommenderar vi att alla underordnade noder för en `oak:QueryIndexDefinition`-nod är av typen `nt:unstructured`.

### Definitionsnoder för anpassade sökindex måste innehålla en underordnad nod med namnet indexRules som har underordnade noder {#oakpal-custom-search-index}

* **Nyckel**: IndexRulesNode
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

En korrekt definierad definitionsnod för anpassat sökindex måste innehålla en underordnad nod med namnet `indexRules` som i sin tur måste ha minst en underordnad nod. Mer information finns i [Oak-dokumentationen](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Definitionsnoder för anpassade sökindex måste följa namnkonventioner {#oakpal-custom-search-definitions}

* **Nyckel**: IndexName
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) ska namnges efter ett specifikt mönster som beskrivs i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md).

### Definitionsnoder för anpassade sökindex måste använda indextypen Lucene  {#oakpal-index-type-lucene}

* **Nyckel**: IndexType
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 2021.2.0 (ändrad typ och allvarlighetsgrad 2021.8.0)

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) har en `type` -egenskap med värdet `lucene`. Indexering med äldre indextyper måste uppdateras innan migrering till Experience Manager as a Cloud Service görs. Mer information finns i [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use).

### Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet seed {#oakpal-property-name-seed}

* **Nyckel**: IndexSeedProperty
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskapen `seed`. Indexering med den här egenskapen måste uppdateras innan migrering till Experience Manager as a Cloud Service. Mer information finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use).

### Definitionsnoder för anpassade sökindex får inte innehålla egenskapen reindex {#oakpal-reindex-property}

* **Nyckel**: IndexReindexProperty
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskapen `reindex`. Indexering med den här egenskapen måste uppdateras före migrering till Experience Manager som en
Cloud Service. Mer information finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use).

### Anpassade DAM-resursklassnoder får inte ange queryPaths {#oakpal-damAssetLucene-queryPaths}

* **Nyckel**: IndexDamAssetLucene
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 202.1.0

#### Kod som inte uppfyller kraven {#non-compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-1
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - queryPaths: [/content/dam]
      - type: lucene
      + tika
        + config.xml
```

#### Kompatibel kod {#compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Om indexdefinitionen för anpassad sökning innehåller compatVersion måste den anges till 2 {#oakpal-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 202.1.0


### Indexnoden som anger includedPaths ska även ange queryPaths med samma värden {#oakpal-included-paths-without-query-paths}

* **Nyckel**: IndexIncludedPathsWithoutQueryPaths
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

För anpassade index bör både `includedPaths` och `queryPaths` konfigureras med identiska värden. Om en anges måste den andra matcha den. Det finns emellertid ett specialfall för index för `damAssetLucene`, inklusive anpassade versioner. För dessa bör du bara ange `includedPaths`.

### Indexnod som anger nodeScopeIndex för allmän nodtyp ska även ange includedPaths och queryPaths {#oakpal-full-text-on-generic-node-type}

* **Nyckel**: IndexFulltextOnGenericType
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

När du anger egenskapen `nodeScopeIndex` för en &quot;generisk&quot; nodtyp som `nt:unstructured` eller `nt:base` måste du även ange egenskaperna `includedPaths` och `queryPaths`.
`nt:base` kan betraktas som&quot;allmän&quot; eftersom alla nodtyper ärver från den. Om du ställer in `nodeScopeIndex` på `nt:base` indexeras det alla noder i databasen. På samma sätt betraktas `nt:unstructured` som&quot;allmän&quot; eftersom det finns många noder i databaser av den här typen.

#### Kod som inte uppfyller kraven {#non-compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

#### Kompatibel kod {#compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
  - includedPaths: ["/content/dam/"] 
  - queryPaths: ["/content/dam/"]
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

### Egenskapen queryLimitReads för frågemotorn ska inte åsidosättas {#oakpal-query-limit-reads}

* **Nyckel**: OverrideOfQueryLimitReads
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

Om du åsidosätter standardvärdet kan det leda till mycket långsam sidläsning, särskilt när mer innehåll läggs till.

### Flera aktiva versioner av samma index {#oakpal-multiple-active-versions}

* **Nyckel**: IndexDetectMultipleActiveVersionsOfSameIndex
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

#### Kod som inte uppfyller kraven {#non-compliant-code-multiple-active-versions}

```text
+ oak:index
  + damAssetLucene-1-custom-1
    ...
  + damAssetLucene-1-custom-2
    ...
  + damAssetLucene-1-custom-3
    ...
```

#### Kompatibel kod {#compliant-code-multiple-active-versions}

```text
+ damAssetLucene-1-custom-3
    ...
```


### Namnet på helt anpassade indexdefinitioner bör överensstämma med de officiella riktlinjerna {#oakpal-fully-custom-index-name}

* **Nyckel**: IndexValidFullyCustomName
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

Det förväntade mönstret för fullständigt anpassade indexnamn är: `[prefix].[indexName]-custom-[version]`. Mer information finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md).

### Samma egenskap med olika analyserade värden i samma indexdefinition {#oakpal-same-property-different-analyzed-values}

#### Kod som inte uppfyller kraven {#non-compliant-code-same-property-different-analyzed-values}

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
```

#### Kompatibel kod {#compliant-code-same-property-different-analyzed-values}

Exempel:

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

Exempel:

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

Om den analyserade egenskapen inte uttryckligen har angetts, kommer standardvärdet att vara false.

### Tagg, egenskap {#tags-property}

* **Nyckel**: IndexHasValidTagsProperty
* **Typ**: kodmeddelande
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

För specifika index måste du behålla taggegenskapen och dess aktuella värden. Det går att lägga till nya värden i taggegenskapen, men om du tar bort befintliga värden (eller egenskapen helt) kan det leda till oväntade resultat.

### Indexdefinitionsnoder får inte distribueras i UI-innehållspaket {#oakpal-ui-content-package}

* **Nyckel**: IndexNotUnderUIContent
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte att anpassade sökindexdefinitioner (noder av typen `oak:QueryIndexDefinition`) distribueras i UI-innehållspaketet.

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Anpassad heltextindexdefinition av typen damAssetLucene måste ha rätt prefix med damAssetLucene {#oakpal-dam-asset-lucene}

* **Nyckel**: CustomFulltextIndexesOfTheDamAssetCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte att anpassade fulltextindexdefinitioner av typen `damAssetLucene` får prefix med något annat än `damAssetLucene`.

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Indexdefinitionsnoder får inte innehålla egenskaper med samma namn {#oakpal-index-property-name}

* **Nyckel**: DuplicateNameProperty
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskaper med samma namn

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Det är förbjudet att anpassa vissa OOTB-indexdefinitioner {#oakpal-customizing-ootb-index}

* **Nyckel**: RestrictIndexCustomization
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte obehöriga ändringar av följande OOTB-index:

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Konfigurationen av tokenisererna i analysatorerna ska skapas med namnet tokenizer {#oakpal-tokenizer}

* **Nyckel**: AnalyzerTokenizerConfigCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud Service tillåter inte att tokeniserare med felaktiga namn skapas i analysatorer. Tokenizers ska alltid definieras som `tokenizer`.

>[!WARNING]
>
>Du uppmanas att åtgärda detta så snart som möjligt eftersom det kommer att leda till att pipelines misslyckas med början i [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Konfiguration av indexeringsdefinitioner får inte innehålla blanksteg {#oakpal-indexing-definitions-spaces}

* **Nyckel**: PathSpacesCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.7.0

AEM Cloud Service tillåter inte att indexdefinitioner som innehåller egenskaper med blanksteg skapas.
