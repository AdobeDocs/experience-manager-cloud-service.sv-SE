---
title: Anpassade regler för kodkvalitet
description: Lär dig mer om Cloud Manager regler för anpassad kodkvalitet, baserade på Adobe Experience Manager bästa praxis för teknikutveckling, för att säkerställa högklassig kod genom grundliga tester.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 629cf9d88531b2e95627917ca139eed1fbddf09d
workflow-type: tm+mt
source-wordcount: '4427'
ht-degree: 0%

---

# Anpassade regler för kodkvalitet {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Anpassade regler för kodkvalitet"
>abstract="Lär dig mer om Cloud Manager regler för anpassad kodkvalitet, baserade på Adobe Experience Manager bästa praxis för teknikutveckling, för att säkerställa högklassig kod genom grundliga tester."

Lär dig mer om Cloud Manager regler för anpassad kodkvalitet, baserade på Adobe Experience Manager bästa praxis för teknikutveckling, för att säkerställa högklassig kod genom grundliga tester. Se även [kodkvalitetstestning](/help/implementing/cloud-manager/code-quality-testing.md).

Fullständiga SonarQube-regler kan inte laddas ned på grund av Adobe egna information. Du kan hämta den fullständiga listan med *aktuella* regler [med den här länken](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx). Fortsätt läsa det här dokumentet för beskrivningar och exempel på reglerna.

>[!IMPORTANT]
>
>Från och med torsdagen den 13 februari 2025 (Cloud Manager 2025.2.0) använder Cloud Manager Code Quality en uppdaterad version av SonarQube 9.9 och en uppdaterad lista över regler som du kan [hämta här](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx).

>[!NOTE]
>
>De kodexempel som anges här är endast avsedda som illustrationer. Mer information om SonarQube-koncept och kvalitetsregler finns i SonarQube [Concepts-dokumentationen](https://docs.sonarsource.com/sonarqube/latest/).

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

Om du använder en formatsträng från en extern källa (till exempel en begärandeparameter eller användargenererat innehåll) kan programmet utsättas för denial of service-attacker. Det finns tillfällen då en formatsträng kan styras externt, men bara tillåts från betrodda källor.

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

När du gör HTTP-begäranden i ett Experience Manager-program är det viktigt att konfigurera lämpliga tidsgränser för att förhindra onödig trådförbrukning.
Både Java™ HTTP Client (java.net.HttpUrlConnection) och den vanliga Apache HTTP Components-klienten har som standard inga tidsgränser, så de måste konfigureras manuellt. Som en god praxis bör timeout anges till 60 sekunder eller mindre.

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
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

ResourceResolver-objekt som hämtats från `ResourceResolverFactory` förbrukar systemresurser. Även om det finns åtgärder för att återta dessa resurser när `ResourceResolver` inte längre används, är det mer effektivt att stänga öppna `ResourceResolver`-objekt explicit genom att anropa metoden `close()`.

En vanlig missuppfattning är att `ResourceResolver` objekt som skapats med en befintlig JCR-session inte får stängas explicit, eller att stängning av dem påverkar JCR-sessionen. Informationen är felaktig. En `ResourceResolver` ska alltid stängas när den inte längre behövs. Eftersom `ResourceResolver` implementerar gränssnittet `Closeable` kan du även använda syntaxen `try-with-resources` i stället för att anropa `close()` direkt.

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
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2018.4.0

Så som beskrivs i [`Sling`-dokumentationen &#x200B;](https://sling.apache.org/documentation/the-sling-engine/servlets.html) rekommenderas inte bindningar av sökvägar. Sökvägsbundna servrar kan inte använda vanliga JCR-åtkomstkontroller och därför krävs ytterligare säkerhetsproblem. I stället för att använda sökvägsbundna servrar rekommenderar vi att du skapar noder i databasen och registrerar servlets efter resurstyp.

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

* **Nyckel**: CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

I allmänhet bör ett undantag loggas exakt en gång. Loggningsundantag flera gånger kan orsaka missförstånd. Orsaken är att det är oklart hur många gånger ett undantag inträffade. Det vanligaste mönstret som leder till den här effekten är loggning och generering av ett fångat undantag.

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

* **Nyckel**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Typ**: `Code Smell`
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

### Undvik att logga in på INFO när du hanterar förfrågningar från GET eller HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Nyckel**: CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre

I allmänhet bör INFO-loggnivån användas för att avgränsa viktiga åtgärder och som standard är Experience Manager konfigurerat för att logga på INFO-nivå eller högre. GET- och HEAD-metoder bör aldrig vara skrivskyddade och därför inte utgöra några viktiga åtgärder. Loggning på INFO-nivå som svar på GET- eller HEAD-förfrågningar skapar troligen avsevärt loggbrus, vilket gör det svårare att identifiera användbar information i loggfiler. När du hanterar förfrågningar från GET eller HEAD loggar du på WARN- eller ERROR-nivå om något har gått fel. Använd nivån DEBUG eller TRACE om detaljerad felsökningsinformation behövs.

>[!NOTE]
>
>Gäller inte loggning av typen `access.log` för varje begäran.

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

* **Nyckel**: CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som en god praxis bör loggmeddelanden innehålla sammanhangsberoende information om var i programmet ett undantag har inträffat. Kontexten kan också bestämmas med stackspår, men i allmänhet blir loggmeddelandet lättare att läsa och förstå. När du loggar ett undantag är det därför en dålig vana att använda undantagets meddelande som loggmeddelande. Undantagsmeddelandet förklarar vad som gick fel, medan loggmeddelandet bör informera läsaren om vad programmet gjorde när undantaget inträffade. Undantagsmeddelandet är fortfarande loggat. Genom att ange ett eget meddelande blir loggarna lättare att förstå.

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

* **Nyckel**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som namnet antyder bör Java™-undantag alltid användas i undantagsfall. Därför är det viktigt att loggmeddelanden loggas på lämplig nivå när ett undantag fångas upp, antingen WARN eller ERROR. Den här processen ser till att meddelandena visas korrekt i loggarna.

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

* **Nyckel**: CQRules:CQBP-44---ExceptionPrintStackTrace
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Som vi nämnt är sammanhang viktigt när du ska förstå loggmeddelanden. Om `Exception.printStackTrace()` används kommer endast stackspårningen att skickas till standardfelströmmen, vilket innebär att all kontext förloras. Om flera undantag skrivs ut med den här metoden parallellt i ett program med flera trådar, som Experience Manager, kan stackspårningarna överlappa varandra, vilket kan skapa stor förvirring. Undantag bör endast loggas via loggningsramverket.

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

* **Nyckel**: CQRules:CQBP-44 - LogLevelConsolePrinters
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Loggning i Experience Manager ska alltid göras via loggningsramverket (SLF4J). Om du matar ut direkt till standardutdata eller standardfelströmmar förlorar du den strukturella och kontextuella information som tillhandahålls av loggningsramverket. Ibland kan det orsaka prestandaproblem.

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

### Undvik hårdkodade appar och libs paths {#avoid-hardcoded-apps-and-libs-paths}

* **Nyckel**: CQRules:CQBP-71
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2018.4.0

Banor som börjar med `/libs` och `/apps` bör vanligtvis inte hårdkodas. Dessa sökvägar lagras vanligtvis i förhållande till söksökvägen `Sling`, som har standardvärdet `/libs,/apps`. Om du använder den absoluta sökvägen kan det orsaka subtila defekter som bara skulle visas senare i projektets livscykel.

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
* **Typ**: `Code Smell`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Använd inte schemaläggaren `Sling` för aktiviteter som kräver en garanterad körning. Sling Scheduled Jobs garanterar körning och passar bättre för både klustrade och icke-klustrade miljöer.

Mer information om hur du hanterar jobb i klustrade miljöer finns i [`Apache Sling` Händelse och jobbhantering](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html).

### Använd inte inaktuella API:er från Experience Manager {#sonarqube-aem-api-deprecated}

* **Nyckel**: java:S1874
* **Typ**: `Vulnerability` eller `Bug`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Info, delversion eller större
* **Sedan**: Version 2026.1.0

Experience Manager API-ytan är under ständig revision för att identifiera API:er för vilka användningen måste stoppas. Denna API är inaktuell och markerad med ett borttagningsdatum.

Ju närmare borttagningsdatumet infaller, desto allvarligare bryter regeln mot. Användning av sådan API måste ersättas med ett säkert alternativ.

### Använd inte inaktuella API:er från Experience Manager {#sonarqube-aem-deprecated}

* **Nyckel**: AMSCORE-553
* **Typ**: `Code Smell`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Experience Manager API-yta är under ständig revision för att identifiera API:er som inte används och därför betraktas som inaktuella.

Dessa API:er är ofta föråldrade med Java™ `@Deprecated`-standardanteckningen och, som sådan, som identifieras av `squid:CallToDeprecatedMethod`.

Det finns dock fall där en API är inaktuell i Experience Manager-sammanhang men inte kan bli inaktuell i andra sammanhang. Den här regeln identifierar den andra klassen.

### Använd inte @Inject-anteckning med @Optional i Sling-modeller {#sonarqube-slingmodels-inject-optional}

* **Nyckel**: InjectAnnotationWithOptionalInjectionCheck
* **Typ**: Programkvalitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.11

Projektet `Apache Sling` uppmuntrar inte användning av anteckningen `@Inject` i kontexten för delningsmodeller, eftersom den kan leda till sämre prestanda när den kombineras med `DefaultInjectionStrategy.OPTIONAL` (antingen på fält- eller klassnivå). I stället bör mer specifika injektioner (som `@ValueMapValue` eller `@OsgiInjector` anteckningar) användas.

Läs [`Apache Sling`-dokumentationen &#x200B;](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1) om du vill ha mer information om de rekommenderade anteckningarna och varför den här rekommendationen gjordes från början.


### Återanvänd instanser av en HTTPClient {#sonarqube-reuse-httpclient}

* **Nyckel**: AEMSRE-870
* **Typ**: Programkvalitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.11

AEM-program når ofta ut till andra program med HTTP-protokollet, och Apache HttpClient är ett bibliotek som ofta används för att uppnå detta. Men när du skapar ett sådant HttpClient-objekt får du en del overhead, så dessa objekt bör återanvändas så mycket som möjligt.

Den här regeln kontrollerar att ett sådant HttpClient-objekt inte är privat inom en metod, utan globalt på en klassnivå, så att det kan återanvändas. I det här fallet ska fältet HttpClient anges i konstruktorn för klassen eller metoden `activate()` (om den här klassen är en OSGi-komponent/tjänst).

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
>OakPAL är ett ramverk som validerar innehållspaket med en fristående Oak-databas. En Experience Manager-partner som vann utmärkelsen Experience Manager Rockstar North America 2019 utvecklade den.

### Kunder bör inte implementera eller utöka produkt-API:er som kommenteras med @ProviderType{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Nyckel**: CQBP-84
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2018.7.0

Experience Manager-API:t innehåller Java™-gränssnitt och -klasser, som endast är avsedda att användas - men inte implementeras - av anpassad kod. Till exempel bör bara Experience Manager implementera gränssnittet `com.day.cq.wcm.api.Page`.

När nya metoder läggs till i dessa gränssnitt påverkar dessa ytterligare metoder inte befintlig kod som använder dessa gränssnitt. Det betyder att tillägg av nya metoder i dessa gränssnitt anses vara bakåtkompatibelt. Men om anpassad kod implementerar ett av dessa gränssnitt har den anpassade koden introducerat en bakåtkompatibilitetsrisk för kunden.

Gränssnitt och klasser - som implementerats av Experience Manager - antecknas med `org.osgi.annotation.versioning.ProviderType` eller ibland en liknande äldre anteckning `aQute.bnd.annotation.ProviderType`. Den här regeln identifierar fall där anpassad kod implementerar ett sådant gränssnitt eller utökar en klass.

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

Flera körklara Experience Manager Oak-index innehåller en Tika-konfiguration och en Tika-konfiguration måste finnas för att dessa index ska kunna anpassas. Den här regeln söker efter anpassningar av indexen `damAssetLucene`, `lucene` och `graphqlConfig` och aktiverar ett problem om `tika`  noden saknas eller om `tika` -noden saknar en underordnad nod med namnet `config.xml`.

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

Oak-index av typen `lucene` måste alltid indexeras asynkront. Om du inte gör det kan systemet bli instabilt. Mer information om strukturen för Lucene-index finns i [Oak-dokumentationen](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition).

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

### Oak-index för anpassade DAM-tillgångar är korrekt strukturerade {#oakpal-damAssetLucene-sanity-check}

* **Nyckel**: IndexDamAssetLucene
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: 2021.6.0

För att resurssökning ska fungera korrekt i Experience Manager Assets måste anpassningar av Oak-indexet `damAssetLucene` följa en uppsättning riktlinjer som är specifika för det här indexet. Den här regeln kontrollerar att indexdefinitionen måste ha en flervärdesegenskap med namnet `tags`, som innehåller värdet `visualSimilaritySearch`.

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

### Kundpaket bör inte skapa eller ändra noder under libs {#oakpal-customer-package}

* **Nyckel**: BannedPath
* **Typ**: Fel
* **Allvarlighetsgrad**: Kritisk
* **Sedan**: Version 2019.6.0

Det har varit en god vana att innehållsträdet `/libs` i Experience Manager-innehållsarkivet alltid ska betraktas som skrivskyddat av kunder. Att ändra noder och egenskaper under `/libs` innebär en betydande risk för större och mindre uppdateringar. Använd Adobe via officiella kanaler för att göra ändringar i `/libs`.

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
>I allmänhet gäller att den här situationen inte följer [riktlinjerna för innehållspaketets struktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md). I det här exemplet saknar paketet `com.myco:com.myco.ui.apps` egenskapen `<cloudManagerTarget>none</cloudManagerTarget>`.

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

Av säkerhetsskäl kan sökvägar som innehåller `/config/` och `/install/` bara läsas av administrationsanvändare i Experience Manager och bör endast användas för OSGi-konfigurationer och OSGi-paket. Om du placerar andra typer av innehåll under banor som innehåller dessa segment, skiljer sig programbeteendet åt mellan administrativa och icke-administrativa användare oavsiktligt.

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

Ungefär som [Paket får inte innehålla regeln för duplicerade OSGi-konfigurationer](#oakpal-package-osgi), är den här situationen ett vanligt problem i komplexa projekt där samma nodsökväg skrivs av flera separata innehållspaket. Även om beroenden för innehållspaket kan användas för att säkerställa ett konsekvent resultat är det bättre att undvika överlappningar helt och hållet.

### Standardredigeringsläget får inte vara ett klassiskt användargränssnitt {#oakpal-default-authoring}

* **Nyckel**: ClassicUIAuthoringMode
* **Typ**: `Code Smell`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

OSGi-konfigurationen `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definierar standardredigeringsläget i Experience Manager. Eftersom det klassiska användargränssnittet har tagits bort sedan Experience Manager 6.4 uppstår nu ett problem när standardredigeringsläget är konfigurerat till Classic UI.

### Komponenter med dialogrutor måste ha dialogrutor för Touch UI {#oakpal-components-dialogs}

* **Nyckel**: ComponentWithOnlyClassicUIDialog
* **Typ**: `Code Smell`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Experience Manager-komponenter som har en klassisk användargränssnittsdialogruta bör alltid ha en motsvarande dialogruta för användargränssnittet. Båda ger en optimal redigeringsupplevelse som är kompatibel med Cloud Service distributionsmodell, där det inte längre finns stöd för Classic UI. Den här regeln verifierar följande scenarier:

* En komponent med en klassisk gränssnittsdialogruta (d.v.s. en underordnad `dialog`-nod) måste ha en motsvarande Touch UI-dialogruta (d.v.s. en underordnad `cq:dialog`-nod).
* En komponent med en klassisk dialogruta för användargränssnittsdesign (d.v.s. en `design_dialog`-nod) måste ha en motsvarande designdialogruta för användargränssnittet (d.v.s. en underordnad `cq:design_dialog`-nod).
* En komponent med både en klassisk användargränssnittsdialogruta och en klassisk dialogruta för användargränssnittsdesign måste ha både en motsvarande dialogruta för användargränssnittet för touchredigering och en motsvarande designdialogruta för användargränssnittet för touchgränssnitt.

Dokumentationen för Experience Manager Moderniseringsverktyg innehåller dokumentation och verktyg för hur du konverterar komponenter från det klassiska gränssnittet till Touch-gränssnittet. Mer information finns i [dokumentationen för Experience Manager Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### Paket får inte innehålla både muterbara och oföränderliga {#oakpal-packages-immutable}

* **Nyckel**: ImmutableMutableMixedPackage
* **Typ**: `Code Smell`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

För att vara kompatibel med Cloud Service distributionsmodell måste enskilda innehållspaket innehålla antingen innehåll för de oföränderliga områdena i databasen (`/apps` och `/libs`) eller det ändringsbara området (allt inte i `/apps` eller `/libs`), men inte båda. Ett paket som innehåller både `/apps/myco/components/text` och `/etc/clientlibs/myco` är till exempel inte kompatibelt med Cloud Service och orsakar att ett problem rapporteras.

>[!NOTE]
>
>Regeln [Kundpaket får inte skapa eller ändra noder under libs](#oakpal-customer-package) gäller alltid.

Mer information finns i [Projektstruktur för Experience Manager](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

### Använd inte agenter för omvänd replikering {#oakpal-reverse-replication}

* **Nyckel**: ReverseReplication
* **Typ**: `Code Smell`/Cloud Service-kompatibilitet
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2020.5.0

Stöd för omvänd replikering är inte tillgängligt i Cloud Service-distributioner, vilket beskrivs i [versionsinformationen för Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md#replication-agents).

Kunder som använder omvänd replikering bör kontakta Adobe för alternativa lösningar.

### Resurser i proxyaktiverade klientbibliotek bör finnas i en mapp med namnet resources {#oakpal-resources-proxy}

* **Nyckel**: ClientlibProxyResource
* **Typ**: Fel
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager klientbibliotek kan innehålla statiska resurser som bilder och teckensnitt. Så som beskrivs i dokumentet [Använda preprocessorer](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) måste dessa statiska resurser finnas i en underordnad mapp med namnet `resources` för att effektivt kunna refereras till på publiceringsinstanserna när du använder proxiderade klientbibliotek.

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

### Användning av Cloud Service inkompatibla arbetsflöden {#oakpal-usage-cloud-service}

* **Nyckel**: CloudServiceIncompatibleWorkflowProcess
* **Typ**: Fel
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 2021.2.0

I och med övergången till tillgångsmikrotjänster för tillgångsbearbetning i Adobe Experience Manager as a Cloud Service stöds nu inte flera arbetsflödesprocesser som används lokalt och i AMS-versioner. Många av dessa arbetsflöden har också blivit onödiga.

Migreringsverktyget i [Experience Manager as a Cloud Service Assets GitHub-databasen](https://github.com/adobe/aem-cloud-migration) kan användas för att uppdatera arbetsflödesmodeller under migrering till Experience Manager as a Cloud Service.

### Användning av statiska mallar rekommenderas inte för redigerbara mallar {#oakpal-static-template}

* **Nyckel**: StaticTemplateUsage
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det är historiskt sett vanligt att använda statiska mallar i Experience Manager-projekt, men Adobe rekommenderar redigerbara mallar eftersom de ger den flexibilitet och stöder ytterligare funktioner som inte finns i statiska mallar. Mer information finns i dokumentet [Sidmallar](/help/implementing/developing/components/templates.md).

Migrering från statiska till redigerbara mallar kan till stor del automatiseras med [Experience Manager Moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/).

### Användning av äldre baskomponenter rekommenderas inte {#oakpal-usage-legacy}

* **Nyckel**: LegacyFoundationComponentUsage
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

De äldre Foundation-komponenterna (d.v.s. komponenterna under `/libs/foundation`) har ersatts för flera Experience Manager-versioner till förmån för Core-komponenterna. Användning av Foundation Components som grund för anpassade komponenter (oavsett om de är övertäckningar eller arv) rekommenderas inte och bör konverteras till motsvarande Core Components.

[Experience Manager moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/) kan underlätta den här konverteringen.

### Använd endast namn och ordning för körningsläge som stöds {#oakpal-supported-runmodes}

* **Nyckel**: SupportedRunmode
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service tillämpar en strikt namngivningsprincip för körlägesnamn och en strikt ordning för dessa körningslägen. Listan över körningslägen som stöds baseras i dokumentet [Distribuera till Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) och alla avvikelser från listan identifieras som ett problem.

### Definitionsnoder för anpassade sökindex måste vara direkt underordnade `/oak:index` {#oakpal-custom-search}

* **Nyckel**: OakIndexLocation
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) är direkta underordnade noder till `/oak:index`. Index på andra platser måste flyttas för att vara kompatibla med Experience Manager as a Cloud Service. Mer information om sökindex finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md).

### Definitionsnoder för anpassade sökindex måste ha en compatVersion av 2 {#oakpal-custom-search-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (till exempel noder av typen `oak:QueryIndexDefinition`) måste ha egenskapen `compatVersion` inställd på `2`. Adobe Experience Manager as a Cloud Service stöder inte något annat värde. Mer information om sökindex finns i [Innehållssökning och indexering](/help/operations/indexing.md).

### Underordnade noder för anpassade sökindexdefinitionsnoder måste vara av typen `nt:unstructured `{#oakpal-descendent-nodes}

* **Nyckel**: IndexDescendantNodeType
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Det är svårt att felsöka problem när en anpassad sökindexdefinitionsnod har oordnade underordnade noder. För att undvika detta rekommenderar vi att alla underordnade noder för en `oak:QueryIndexDefinition`-nod är av typen `nt:unstructured`.

### Definitionsnoder för anpassade sökindex måste innehålla en underordnad nod med namnet indexRules som har underordnade noder {#oakpal-custom-search-index}

* **Nyckel**: IndexRulesNode
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

En korrekt definierad definitionsnod för anpassat sökindex måste innehålla en underordnad nod med namnet `indexRules`, som i sin tur måste ha minst en underordnad nod. Mer information finns i [Oak-dokumentationen](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Definitionsnoder för anpassade sökindex måste följa namnkonventioner {#oakpal-custom-search-definitions}

* **Nyckel**: IndexName
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) ska namnges efter ett specifikt mönster som beskrivs i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md).

### Definitionsnoder för anpassade sökindex måste använda indextypen Lucene {#oakpal-index-type-lucene}

* **Nyckel**: IndexType
* **Typ**: Fel
* **Allvarlighetsgrad**: Blockerare
* **Sedan**: Version 2021.2.0 (ändrad typ och allvarlighetsgrad 2021.8.0)

Experience Manager as a Cloud Service kräver att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) har en `type` -egenskap med värdet `lucene`. Indexering med äldre indextyper måste uppdateras innan migrering till Experience Manager as a Cloud Service. Mer information finns i [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use).

### Definitionsnoder för anpassade sökindex får inte innehålla en egenskap med namnet seed {#oakpal-property-name-seed}

* **Nyckel**: IndexSeedProperty
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskapen `seed`. Indexering med den här egenskapen måste uppdateras innan migrering till Experience Manager as a Cloud Service. Mer information finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use).

### Definitionsnoder för anpassade sökindex får inte innehålla egenskapen reindex {#oakpal-reindex-property}

* **Nyckel**: IndexReindexProperty
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2021.2.0

Experience Manager as a Cloud Service tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskapen `reindex`. Indexering med den här egenskapen måste uppdateras innan migrering till Experience Manager som
Cloud Service. Mer information finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md#how-to-use).

### Anpassade DAM-resursklassnoder får inte ange `queryPaths` {#oakpal-damAssetLucene-queryPaths}

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

### Om den anpassade sökindexsdefinitionen innehåller `compatVersion` måste den anges till 2 {#oakpal-compatVersion}

* **Nyckel**: IndexCompatVersion
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Större
* **Sedan**: Version 202.1.0


### Indexnoden som anger `includedPaths` ska även ange `queryPaths` med samma värden {#oakpal-included-paths-without-query-paths}

* **Nyckel**: IndexIncludedPathsWithoutQueryPaths
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

Konfigurera `includedPaths` och `queryPaths` med identiska värden för anpassade index. Om en anges måste den andra matcha den. Det finns emellertid ett specialfall för index för `damAssetLucene`, inklusive anpassade versioner. Ange bara `includedPaths` för dessa fall.

### Indexnoden som anger `nodeScopeIndex` för den generiska nodtypen ska också ange `includedPaths` och `queryPaths` {#oakpal-full-text-on-generic-node-type}

* **Nyckel**: IndexFulltextOnGenericType
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

När du anger egenskapen `nodeScopeIndex` för en &quot;generisk&quot; nodtyp som `nt:unstructured` eller `nt:base` måste du även ange egenskaperna `includedPaths` och `queryPaths`.
Nodtypen `nt:base` kan betraktas som generisk eftersom alla nodtyper ärver från den. Om du ställer in `nodeScopeIndex` på `nt:base` indexeras alla noder i databasen. På samma sätt betraktas `nt:unstructured` som&quot;allmän&quot; eftersom det finns många noder i databaser av den här typen.

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
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

Om du åsidosätter standardvärdet kan sidläsningen bli långsam, särskilt när mer innehåll läggs till.

### Flera aktiva versioner av samma index {#oakpal-multiple-active-versions}

* **Nyckel**: IndexDetectMultipleActiveVersionsOfSameIndex
* **Typ**: `Code Smell`
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
* **Typ**: `Code Smell`
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

Om den analyserade egenskapen inte anges explicit är standardvärdet false.

### Tagg, egenskap {#tags-property}

* **Nyckel**: IndexHasValidTagsProperty
* **Typ**: `Code Smell`
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2023.1.0

För specifika index måste du behålla taggegenskapen och dess aktuella värden. Det går att lägga till nya värden i taggegenskapen, men om du tar bort befintliga värden (eller egenskapen helt) kan det leda till oväntade resultat.

### Indexdefinitionsnoder får inte distribueras i UI-innehållspaket {#oakpal-ui-content-package}

* **Nyckel**: IndexNotUnderUIContent
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten tillåter inte att anpassade sökindexdefinitioner (noder av typen `oak:QueryIndexDefinition`) distribueras i UI-innehållspaketet.

>[!WARNING]
>
>Du bör lösa det här problemet så snart som möjligt, eftersom det kan orsaka pipeline-fel som börjar med [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Anpassad heltextindexdefinition av typen damAssetLucene måste ha korrekt prefix med damAssetLucene {#oakpal-dam-asset-lucene}

* **Nyckel**: CustomFulltextIndexesOfTheDamAssetCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten förhindrar att anpassade fulltextindexdefinitioner av typen `damAssetLucene` prefix med något annat än `damAssetLucene`.

>[!WARNING]
>
>Lös det här problemet så snart som möjligt, eftersom det kan orsaka pipeline-fel som börjar med [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Indexdefinitionsnoder får inte innehålla egenskaper med samma namn {#oakpal-index-property-name}

* **Nyckel**: DuplicateNameProperty
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten tillåter inte att anpassade sökindexdefinitioner (d.v.s. noder av typen `oak:QueryIndexDefinition`) innehåller egenskaper med samma namn

>[!WARNING]
>
>Lös det här problemet så snart som möjligt, eftersom det kan orsaka pipeline-fel som börjar med [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Det är inte tillåtet att anpassa vissa färdiga indexdefinitioner {#oakpal-customizing-ootb-index}

* **Nyckel**: RestrictIndexCustomization
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

AEM Cloud-tjänsten tillåter inte obehöriga ändringar av följande OOTB-index:

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>Lös det här problemet så snart som möjligt, eftersom det kan orsaka pipeline-fel som börjar med [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Konfiguration av tokeniserare i analysatorer ska skapas med namnet tokenizer {#oakpal-tokenizer}

* **Nyckel**: AnalyzerTokenizerConfigCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.6.0

Tjänsten AEM Cloud tillåter inte att tokeniserare med felaktiga namn skapas i analysatorer. Tokenizers ska alltid definieras som `tokenizer`.

>[!WARNING]
>
>Lös det här problemet så snart som möjligt, eftersom det kan orsaka pipeline-fel som börjar med [Cloud Manager August 2024-utgåvan](/help/implementing/cloud-manager/release-notes/current.md).

### Konfiguration av indexeringsdefinitioner får inte innehålla blanksteg {#oakpal-indexing-definitions-spaces}

* **Nyckel**: PathSpacesCheck
* **Typ**: Förbättring
* **Allvarlighetsgrad**: Mindre
* **Sedan**: Version 2024.7.0

AEM Cloud-tjänsten tillåter inte skapande av indexeringsdefinitioner som innehåller egenskaper med mellanslag.
