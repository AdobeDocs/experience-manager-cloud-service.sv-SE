---
title: Anpassade regler för kodkvalitet
description: Den här sidan beskriver de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av [kodkvalitetstestning. De bygger på god praxis från AEM Engineering.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: ee45ba3a03f9ab5461a09188888694ca22a11b20
workflow-type: tm+mt
source-wordcount: '3495'
ht-degree: 3%

---

# Anpassade regler för kodkvalitet {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Anpassade regler för kodkvalitet"
>abstract="Den här sidan beskriver de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av testningen av kodkvalitet. De bygger på god praxis från AEM Engineering."

Den här sidan beskriver de anpassade regler för kodkvalitet som körs av Cloud Manager som en del av [kodkvalitetstestning.](/help/implementing/cloud-manager/code-quality-testing.md) De bygger på god praxis från AEM Engineering.

>[!NOTE]
>
>De kodexempel som anges här är endast avsedda som illustrationer. Se SonarQube [Konceptdokumentation](https://docs.sonarqube.org/7.4/user-guide/concepts/) om du vill veta mer om SonarQube-koncept och kvalitetsregler.

## SonarQube-regler {#sonarqube-rules}

Följande avsnitt innehåller information om SonarQube-regler som körs av Cloud Manager.

### Använd inte potentiellt farliga funktioner {#do-not-use-potentially-dangerous-functions}

* **Nyckel**: CQRules:CWE-676
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2018.4.0

Metoderna `Thread.stop()` och `Thread.interrupt()` kan ge upphov till problem som är svåra att reproducera och, i vissa fall, säkerhetsluckor. Deras användning bör övervakas noggrant och valideras. I allmänhet är meddelandeöverföring ett säkrare sätt att uppnå samma sak.

#### Icke-kompatibel kod {#non-compliant-code}

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

### Använd inte formatsträngar som kan vara externt styrda {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Nyckel**: CQRules:CWE-134
* **Typ**: Sårbarhet
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2018.4.0

Om du använder en formatsträng från en extern källa (t.ex. en begärandeparameter eller ett användargenererat innehåll) kan programmet utsättas för denial of service-attacker. Det finns tillfällen då en formatsträng kan styras externt, men bara tillåts från betrodda källor.

#### Icke-kompatibel kod {#non-compliant-code-1}

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

När du kör HTTP-begäranden inifrån ett AEM-program är det viktigt att se till att rätt tidsgränser är konfigurerade för att undvika onödig trådförbrukning. Tyvärr är standardbeteendet för båda Java:s standard-HTTP-klient (`java.net.HttpUrlConnection`) och den vanligaste Apache HTTP Components-klienten är att aldrig timeout, så timeout måste anges explicit. Dessutom bör dessa timeout inte vara längre än 60 sekunder.

#### Icke-kompatibel kod {#non-compliant-code-2}

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

public void orDoThis() {
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

### ResourceResolver-objekt ska alltid stängas {#resourceresolver-objects-should-always-be-closed}

* **Nyckel**: CQRules:CQBP-72
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2018.4.0

`ResourceResolver` objekt som hämtats från `ResourceResolverFactory` förbruka systemresurser. Även om det finns åtgärder för att återkräva dessa resurser när en `ResourceResolver` används inte längre, det är mer effektivt att uttryckligen stänga alla öppna `ResourceResolver` objekt genom att anropa `close()` -metod.

En relativt vanlig missuppfattning är att `ResourceResolver` objekt som skapats med en befintlig JCR-session ska inte stängas explicit, eller så stängs den underliggande JCR-sessionen. Detta är inte fallet. Oavsett hur `ResourceResolver` öppnas, ska den stängas när den inte längre används. Sedan `ResourceResolver` implementerar `Closeable` -gränssnittet kan du också använda `try-with-resources` syntax i stället för explicit anrop `close()`.

#### Icke-kompatibel kod {#non-compliant-code-4}

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

### Använd inte SSL-serversökvägar för att registrera servrar {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Nyckel**: CQRules:CQBP-75
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2018.4.0

Enligt beskrivningen i [Sling-dokumentation](http://sling.apache.org/documentation/the-sling-engine/servlets.html), rekommenderas inte bindningsservrar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

#### Icke-kompatibel kod {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Infångade undantag ska loggas eller kastas, inte båda {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Nyckel**: CQRules:CQBP-44—CatchAndeitherLogOrThrow
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

I allmänhet bör ett undantag loggas exakt en gång. Om du loggar undantag flera gånger kan det leda till missförstånd eftersom det är oklart hur många gånger ett undantag inträffade. Det vanligaste mönstret som leder till detta är loggning och generering av ett fångat undantag.

#### Icke-kompatibel kod {#non-compliant-code-6}

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

### Undvik loggsatser som följs av en utdragsbeskrivning {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Nyckel**: CQRules:CQBP-44 - ConsecutiousLogAndThrow
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Ett annat vanligt sätt att undvika är att logga ett meddelande och sedan omedelbart generera ett undantag. Detta innebär vanligtvis att undantagsmeddelandet kommer att dupliceras i loggfiler.

#### Icke-kompatibel kod {#non-compliant-code-7}

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

### Undvik inloggning vid INFO vid hantering av GET- eller HEAD-förfrågningar {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Nyckel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och AEM är som standard konfigurerad för att logga på INFO-nivå eller högre. Metoderna GET och HEAD bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. Loggning vid hantering av GET- eller HEAD-begäranden bör finnas antingen på WARN- eller FEL-nivå när något har gått fel eller på DEBUG- eller TRACE-nivå om mer detaljerad felsökningsinformation skulle vara till hjälp.

>[!NOTE]
>
>Detta gäller inte för `access.log`loggning av -typ för varje begäran.

#### Icke-kompatibel kod {#non-compliant-code-8}

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
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som en god praxis bör loggmeddelanden innehålla sammanhangsberoende information om var i programmet ett undantag har inträffat. Även om kontexten kan avgöras genom att stackspårningar används, kommer loggmeddelandet i allmänhet att vara lättare att läsa och förstå. När du loggar ett undantag är det därför en dålig vana att använda undantagets meddelande som loggmeddelande. Undantagsmeddelandet innehåller det som gick fel, medan loggmeddelandet bör användas för att tala om för en loggläsare vad programmet gjorde när undantaget inträffade. Undantagsmeddelandet kommer fortfarande att loggas. Genom att ange ett eget meddelande blir loggarna enklare att förstå.

#### Icke-kompatibel kod {#non-compliant-code-9}

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

### Loggning in Catch Blocks Should at the WARN or ERROR Level {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Nyckel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som namnet antyder bör Java-undantag alltid användas i undantagsfall. Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp, antingen WARN eller ERROR. Detta garanterar att meddelandena visas korrekt i loggarna.

#### Icke-kompatibel kod {#non-compliant-code-10}

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
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som vi nämnt är sammanhang viktigt när du ska förstå loggmeddelanden. Använda `Exception.printStackTrace()` gör att endast stackspårningen matas ut till standardfelströmmen och därmed förlorar all kontext. Om flera undantag skrivs ut med den här metoden parallellt i ett program med flera trådar, som AEM, kan stackspårningarna överlappa varandra, vilket kan skapa stor förvirring. Undantag bör endast loggas via loggningsramverket.

#### Icke-kompatibel kod {#non-compliant-code-11}

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

### Utdata inte till standardutdata eller standardfel {#do-not-output-to-standard-output-or-standard-error}

* **Nyckel**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Loggning AEM alltid ske via loggningsramverket (SLF4J). Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket och kan i vissa fall orsaka prestandaproblem.

#### Icke-kompatibel kod {#non-compliant-code-12}

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

### Undvik hårdkodade/program- och /libs-sökvägar {#avoid-hardcoded-apps-and-libs-paths}

* **Nyckel**: CQRules:CQBP-71
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Vanligtvis banor som börjar med `/libs` och `/apps` ska inte hårdkodas eftersom sökvägarna som de refererar till vanligtvis lagras som sökvägar i förhållande till sökbanan för Sling, som är inställd på `/libs,/apps` som standard. Om du använder den absoluta sökvägen kan det orsaka subtila defekter som bara skulle visas senare i projektets livscykel.

#### Icke-kompatibel kod {#non-compliant-code-13}

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

### Sling Scheduler ska inte användas {#sonarqube-sling-scheduler}

* **Nyckel**: CQRules:AMSCORE-554
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Sling Scheduler får inte användas för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Se [Apache Sling Eventing och Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) om du vill veta mer om hur Sling Jobs hanteras i klustrade miljöer.

### AEM inaktuella API:er ska inte användas {#sonarqube-aem-deprecated}

* **Nyckel**: AMSCORE-553
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

AEM API-yta är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

I många fall är dessa API:er föråldrade med standard-Java `@Deprecated` anteckning och, som sådan, identifierad av `squid:CallToDeprecatedMethod`.

Det finns dock fall där ett API är inaktuellt i AEM men inte i andra sammanhang. Den här regeln identifierar den andra klassen.


## OakPAL-innehållsregler {#oakpal-rules}

Följande avsnitt innehåller information om de OakPAL-kontroller som körs av Cloud Manager.

>[!NOTE]
>
>OakPAL är ett ramverk som validerar innehållspaket med en fristående Oak-databas. Den utvecklades av en AEM partner och vinnare av 2019 AEM Rockstar North America-priset.

### Produkt-API:er som antecknas med @ProviderType ska inte implementeras eller utökas av kunder {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Nyckel**: CQBP-84
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.7.0

API:t för AEM innehåller Java-gränssnitt och -klasser som bara är avsedda att användas, inte implementeras, av anpassad kod. Gränssnittet `com.day.cq.wcm.api.Page` är till exempel utformat att implementeras av enbart AEM.

När nya metoder läggs till i dessa gränssnitt påverkar inte dessa ytterligare metoder befintlig kod som använder dessa gränssnitt, och därför anses tillägg av nya metoder i dessa gränssnitt vara bakåtkompatibelt. Men om anpassad kod implementerar ett av dessa gränssnitt har den anpassade koden skapat en risk vad gäller bakåtkompatibilitet för kunden.

Gränssnitt och klasser, som endast är avsedda att implementeras av AEM, kommenteras med `org.osgi.annotation.versioning.ProviderType` eller i vissa fall en liknande äldre anteckning `aQute.bnd.annotation.ProviderType`. Den här regeln identifierar de fall där ett sådant gränssnitt implementeras eller en klass utökas av anpassad kod.

#### Icke-kompatibel kod {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Anpassade Luceneak-index måste ha en Tika-konfiguration {#oakpal-indextikanode}

* **Nyckel**: IndexTikaNode
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockera
* **Sedan**: 2021.8.0

Flera körklara AEM Oak-index innehåller en kodkonfiguration och anpassningar av dessa index måste innehålla en kodkonfiguration. Den här regeln söker efter anpassningar av `damAssetLucene`, `lucene`och `graphqlConfig` index och ger upphov till ett problem om `tika`  noden saknas eller om `tika` noden saknar en underordnad nod med namnet `config.xml`.

Se [indexeringsdokumentation](/help/operations/indexing.md#preparing-the-new-index-definition) om du vill ha mer information om hur du anpassar indexdefinitioner.

#### Icke-kompatibel kod {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
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
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Egna Lucene-ekindex får inte vara synkrona {#oakpal-indexasync}

* **Nyckel**: IndexAsyncProperty
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockera
* **Sedan**: 2021.8.0

Oak-index av typen `lucene` måste alltid indexeras asynkront. Om du inte gör detta kan det leda till att systemet blir instabilt. Mer information om strukturen för lucene-index finns i [Oak-dokumentation.](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### Icke-kompatibel kod {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
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
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### De anpassade DAM-resursindexen Luceneak är korrekt strukturerade  {#oakpal-damAssetLucene-sanity-check}

* **Nyckel**: IndexDamAssetLucene
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockera
* **Sedan**: 2021.6.0

För att resurssökningen ska fungera korrekt i AEM Assets måste du anpassa `damAssetLucene` Oak-indexet måste följa en uppsättning riktlinjer som är specifika för detta index. Den här regeln kontrollerar att indexdefinitionen måste ha en egenskap med flera värden som heter `tags` som innehåller värdet `visualSimilaritySearch`.

#### Icke-kompatibel kod {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
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
      - reindex: false
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

Det har länge varit en god praxis att `/libs` innehållsträdet i AEM innehållsarkiv ska betraktas som skrivskyddat av kunderna. Ändra noder och egenskaper under `/libs` innebär en betydande risk för större och mindre uppdateringar. Ändringar av `/libs` bör endast göras av Adobe via officiella kanaler.

### Paket får inte innehålla dubbletter av OSGi-konfigurationer {#oakpal-package-osgi}

* **Nyckel**: DuplicateOsgiConfigurations
* **Typ**: Fel
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2019.6.0

Ett vanligt problem som inträffar i komplexa projekt är när samma OSGi-komponent konfigureras flera gånger. Detta skapar en tvetydighet om vilken konfiguration som ska användas. Den här regeln är&quot;körningsmedveten&quot; eftersom den bara identifierar problem där samma komponent har konfigurerats flera gånger i samma körningsläge eller en kombination av körningslägen.

>[!NOTE]
>
>Den här regeln ger problem där samma konfiguration, med samma sökväg, definieras i flera paket, inklusive fall där samma paket dupliceras i den övergripande listan över inbyggda paket.
>
>Om till exempel bygget skapar paket med namnet `com.myco:com.myco.ui.apps` och `com.myco:com.myco.all` där `com.myco:com.myco.all` inbäddade `com.myco:com.myco.ui.apps`, sedan alla konfigurationer i `com.myco:com.myco.ui.apps` rapporteras som dubbletter.
>
>Detta är vanligtvis ett fall där man inte följer [Riktlinjer för innehållspaketets struktur.](/help/implementing/developing/introduction/aem-project-content-package-structure.md). I det här specifika exemplet `com.myco:com.myco.ui.apps` saknar `<cloudManagerTarget>none</cloudManagerTarget>` -egenskap.

#### Icke-kompatibel kod {#non-compliant-code-osgi}

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
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2019.6.0

Av säkerhetsskäl innehåller sökvägar `/config/` och `/install/` kan endast läsas av administrativa användare i AEM och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller dessa segment, kommer programbeteendet att variera oavsiktligt mellan administrativa och icke-administrativa användare.

Ett vanligt problem är att använda namngivna noder `config` i komponentdialogrutor eller när du anger RTF-redigeringskonfigurationen för infogad redigering. För att lösa detta bör den felande noden byta namn till ett kompatibelt namn. För textredigerarkonfigurationen använder du `configPath` på `cq:inplaceEditing` för att ange den nya platsen.

#### Icke-kompatibel kod {#non-compliant-code-config-install}

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
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2019.6.0

Liknar [Paket får inte innehålla en dubblettregel för OSGi-konfigurationer,](#oakpal-package-osgi) detta är ett vanligt problem i komplexa projekt där samma nodsökväg skrivs av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara ett klassiskt användargränssnitt {#oakpal-default-authoring}

* **Nyckel**: KlassisktUIAuthoringMode
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i AEM. För [det klassiska användargränssnittet har tagits bort sedan AEM 6.4,](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) Ett problem kommer nu att uppstå när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor bör ha gränssnittsdialogrutor med pekskärmar {#oakpal-components-dialogs}

* **Nyckel**: ComponentWithOnlyClassicUIDialog
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

AEM som har en Classic UI-dialogruta ska alltid ha en motsvarande Touch-dialogruta, både för att ge en optimal redigeringsupplevelse och för att vara kompatibel med Cloud Servicens distributionsmodell, där Classic UI inte stöds. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk användargränssnittsdialogruta (d.v.s. en `dialog` underordnad nod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en `cq:dialog` underordnad nod).
* En komponent med en klassisk dialogruta för användargränssnittsdesign (dvs. en `design_dialog` nod) måste ha en motsvarande dialogruta för Touch UI-design (d.v.s. en `cq:design_dialog` underordnad nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för AEM Moderniseringsverktyg innehåller dokumentation och verktyg för hur du konverterar komponenter från det klassiska gränssnittet till Touch-gränssnittet. Se [dokumentationen för AEM Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) för mer information.

### Paketen får inte innehålla blandbart och oföränderligt innehåll {#oakpal-packages-immutable}

* **Nyckel**: ImmutableMutableMixedPackage
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

För att vara kompatibel med databasens distributionsmodell måste enskilda innehållspaket innehålla antingen innehåll för databasens oföränderliga områden (dvs. `/apps` och `/libs`) eller det muterbara området (det vill säga allt som inte finns i `/apps` eller `/libs`), men inte båda. Ett paket som innehåller både `/apps/myco/components/text and /etc/clientlibs/myco` är inte kompatibelt med Cloud Service och kommer att orsaka ett problem som rapporteras.

>[!NOTE]
>
>Regeln [Kundpaket får inte skapa eller ändra noder under /libs](#oakpal-customer-package) gäller alltid.

Se [AEM projektstruktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md) för mer information.

### Omvända replikeringsagenter ska inte användas {#oakpal-reverse-replication}

* **Nyckel**: ReverseReplication
* **Typ**: Kompatibilitet med kodmeddelanden/Cloud Service
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i distributioner av Cloud Service, vilket beskrivs som en del av AEM as a Cloud Service [versionsinformation.](/help/release-notes/aem-cloud-changes.md#replication-agents)

Kunder som använder omvänd replikering bör kontakta Adobe för att få alternativa lösningar.

### Resurser i proxyaktiverade klientbibliotek bör finnas i en mapp med namngivna resurser {#oakpal-resources-proxy}

* **Nyckel**: ClientlibProxyResource
* **Typ**: Fel
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM klientbibliotek kan innehålla statiska resurser som bilder och teckensnitt. Enligt beskrivningen i dokumentet [Använda preprocessorer,](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) när du använder proxyanslutna klientbibliotek måste dessa statiska resurser finnas i en underordnad mapp med namnet `resources` för att effektivt kunna referera till publiceringsinstanserna.

#### Icke-kompatibel kod {#non-compliant-proxy-enabled}

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

### Användning av Cloud Service som inte är kompatibla arbetsflödesprocesser {#oakpal-usage-cloud-service}

* **Nyckel**: CloudServiceIncompatibleWorkflowProcess
* **Typ**: Fel
* **Allvarlighetsgrad**: Viktigt
* **Sedan**: Version 2021.2.0

I och med övergången till tillgångsmikrotjänster för tillgångsbearbetning på AEM as a Cloud Service har flera arbetsflödesprocesser som användes på plats och i AMS-versioner av AEM blivit antingen ostödda eller onödiga.

Migreringsverktyget i [AEM Assets as a Cloud Service GitHub-databas](https://github.com/adobe/aem-cloud-migration) kan användas för att uppdatera arbetsflödesmodeller under migrering till AEM as a Cloud Service.

### Användning av statiska mallar rekommenderas inte för redigerbara mallar {#oakpal-static-template}

* **Nyckel**: StaticTemplateUsage
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det har tidigare varit mycket vanligt att använda statiska mallar i AEM projekt, men redigerbara mallar rekommenderas eftersom de ger den flexibilitet och stöder ytterligare funktioner som inte finns i statiska mallar. Mer information finns i dokumentet [Sidmallar.](/help/implementing/developing/components/templates.md)

Migrering från statiska till redigerbara mallar kan till stor del automatiseras med [AEM moderniseringsverktyg.](https://opensource.adobe.com/aem-modernize-tools/)

### Användning av äldre grundkomponenter rekommenderas inte {#oakpal-usage-legacy}

* **Nyckel**: LegacyFoundationComponentUsage
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

De äldre Foundation Components (dvs. komponenter under `/libs/foundation`) har [har tagits bort för flera AEM versioner](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) till förmån för kärnkomponenterna. Användning av Foundation Components som grund för anpassade komponenter (oavsett om de är övertäckningar eller arv) rekommenderas inte och bör konverteras till motsvarande Core Components.

Den här konverteringen kan underlättas av [AEM moderniseringsverktyg.](https://opensource.adobe.com/aem-modernize-tools/)

### Endast körlägesnamn och -ordning som stöds ska användas {#oakpal-supported-runmodes}

* **Nyckel**: SupportedRunmode
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM as a Cloud Service använder en strikt namngivningsprincip för körningslägesnamn och en strikt ordning för dessa körningslägen. En lista över körningslägen som stöds finns i dokumentet [Distribuera till AEM as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) och eventuella avvikelser från detta identifieras som en fråga.

### Definitionsnoder för anpassade sökindex måste vara direkt underordnade /oak:index {#oakpal-custom-search}

* **Nyckel**: OakIndexLocation
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM as a Cloud Service kräver anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) be direct child nodes of `/oak:index`. Index på andra platser måste flyttas för att vara kompatibla med AEM as a Cloud Service. Mer information om sökindex finns i dokumentet [Innehållssökning och indexering.](/help/operations/indexing.md)

### Definitionsnoder för anpassade sökindex måste ha en compatVersion av 2 {#oakpal-custom-search-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM as a Cloud Service kräver anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) måste ha `compatVersion` egenskap inställd på `2`. Andra värden stöds inte av AEM as a Cloud Service. Mer information om sökindex finns på [Innehållssökning och indexering.](/help/operations/indexing.md)

### Underordnade noder i definitionsnoder för anpassade sökindex måste vara av typen nt:ostrukturerad {#oakpal-descendent-nodes}

* **Nyckel**: IndexDescendantNodeType
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det är svårt att felsöka problem när en anpassad sökindexdefinitionsnod har oordnade underordnade noder. Om du vill undvika den här situationen rekommenderar vi att alla underordnade noder för en `oak:QueryIndexDefinition` noden är av typen `nt:unstructured`.

### Definitionsnoder för anpassade sökindex måste innehålla en underordnad nod med namnet indexRules som har underordnade noder {#oakpal-custom-search-index}

* **Nyckel**: IndexRulesNode
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

En korrekt definierad definitionsnod för anpassade sökindex måste innehålla en underordnad nod med namnet `indexRules` som i sin tur måste ha minst ett barn. Mer information finns i [Oak-dokumentation.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### Definitionsnoder för anpassade sökindex måste följa namngivningskonventioner {#oakpal-custom-search-definitions}

* **Nyckel**: IndexName
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM as a Cloud Service kräver anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) måste namnges efter ett specifikt mönster som beskrivs i dokumentet [Innehållssökning och indexering.](/help/operations/indexing.md)

### Indexdefinitionsnoder för anpassade sökningar måste använda indextypsklugin  {#oakpal-index-type-lucene}

* **Nyckel**: IndexType
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockera
* **Sedan**: Version 2021.2.0 (ändrad typ och allvarlighetsgrad 2021.8.0)

AEM as a Cloud Service kräver anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) har en `type` egenskap med värdet inställt på `lucene`. Indexering med äldre indextyper måste uppdateras innan migrering till AEM as a Cloud Service. Se dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use) för mer information.

### Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet seed {#oakpal-property-name-seed}

* **Nyckel**: IndexSeedProperty
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM as a Cloud Service tillåter inte anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) som innehåller en egenskap med namnet `seed`. Indexering med den här egenskapen måste uppdateras innan migrering till AEM as a Cloud Service. Se dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use) för mer information.

### Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet reindex {#oakpal-reindex-property}

* **Nyckel**: IndexReindexProperty
* **Typ**: Code Smell
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

AEM as a Cloud Service tillåter inte anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) som innehåller en egenskap med namnet `reindex`. Indexering med den här egenskapen måste uppdateras innan migrering till AEM as a Cloud Service. Se dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use) för mer information.
