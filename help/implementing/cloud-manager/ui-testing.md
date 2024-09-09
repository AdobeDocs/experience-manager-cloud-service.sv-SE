---
title: UI-testning
description: Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina anpassade program
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 0%

---


# UI-testning {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI-testning"
>abstract="Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium)."

Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program.

## Ökning {#custom-ui-testing}

AEM tillhandahåller en integrerad svit med [Cloud Manager-kvalitetsportar](/help/implementing/cloud-manager/custom-code-quality-rules.md) för att säkerställa smidiga uppdateringar av anpassade program. I synnerhet har IT-testportar redan stöd för att skapa och automatisera anpassade tester med AEM API:er.

Användargränssnittstester är paketerade i en Docker-bild för att ge ett brett urval på språk och i miljöer (t.ex. Cypress, Selenium, Java och Maven och JavaScript). Ett UI-testprojekt kan också enkelt genereras med [den AEM projekttypen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html).

Adobe uppmuntrar användningen av Cypress eftersom det ger realtidsladdning och automatisk väntetid, vilket sparar tid och förbättrar produktiviteten under testningen. Cypress har också en enkel och intuitiv syntax som gör det enkelt att lära sig och använda, även för dem som inte har testat tidigare.

Gränssnittstester körs som en del av en viss kvalitetsport för varje Cloud Manager-pipeline med ett [**anpassat gränssnittstestningssteg** ](/help/implementing/cloud-manager/deploy-code.md) i [produktionspipelinjer](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) eller eventuellt [icke-produktionspipelinjer](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) . Alla gränssnittstester, inklusive regression och nya funktioner, gör att fel kan upptäckas och rapporteras.

Till skillnad från anpassade funktionstester, som är HTTP-tester skrivna i Java, kan gränssnittstester vara en dockningsbild med tester skrivna på vilket språk som helst, förutsatt att de följer konventionerna som definieras i avsnittet [Byggnadens gränssnittstester](#building-ui-tests).

>[!TIP]
>
>Adobe rekommenderar att du använder Cypress för UI-testning, enligt koden i [AEM testexempeldatabasen](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).
> 
>Adobe innehåller även exempel på gränssnittstestmoduler baserade på JavaScript med WebdriverIO (se [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) och Java med WebDriver (se [AEM Test Samples database](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)).

## Kom igång med gränssnittstester {#get-started-ui-tests}

I det här avsnittet beskrivs de steg som krävs för att konfigurera gränssnittstester för körning i Cloud Manager.

1. Bestäm vilket programmeringsspråk du vill använda.

   * För Cypress använder du exempelkoden från databasen [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).

   * För JavaScript och WDIO använder du den exempelkod som genereras automatiskt i mappen `ui.tests` i din Cloud Manager-databas.

     >[!NOTE]
     >
     >Om din databas skapades innan Cloud Manager automatiskt skapade `ui.tests`-mappar kan du även generera den senaste versionen med [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests).

   * För Java och WebDriver använder du exempelkoden från databasen [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver).

   * För andra programmeringsspråk, se avsnittet [Skapa gränssnittstester](#building-ui-tests) i det här dokumentet för att konfigurera testprojektet.

1. Kontrollera att gränssnittstestning är aktiverat enligt avsnittet [Kundens anmälan](#customer-opt-in) i det här dokumentet.

1. Utveckla dina testfall och [kör testerna lokalt](#run-ui-tests-locally).

1. Arkivera koden i Cloud Manager-databasen och kör en Cloud Manager-pipeline.

## Bygga UI-tester {#building-ui-tests}

Ett Maven-projekt genererar en Docker-byggkontext. Den här Docker-byggkontexten beskriver hur du skapar en Docker-avbildning som innehåller gränssnittstesterna, som Cloud Manager använder för att generera en Docker-bild som innehåller de faktiska gränssnittstesterna.

I det här avsnittet beskrivs de steg som krävs för att lägga till ett UI-testprojekt på lagringsplatsen.

>[!TIP]
>
>[AEM Project Archetype](https://github.com/adobe/aem-project-archetype) kan generera ett UI-testprojekt åt dig, vilket är kompatibelt med följande beskrivning, om du inte har några särskilda krav för programmeringsspråket.

### Skapa en kontext för Docker Build {#generate-docker-build-context}

För att skapa en Docker-byggkontext behöver du en Maven-modul som:

* Skapar ett arkiv som innehåller en `Dockerfile` och alla andra filer som behövs för att skapa Docker-bilden med dina tester.
* Taggar arkivet med klassificeraren `ui-test-docker-context`.

Det enklaste sättet att göra detta är att konfigurera plugin-programmet [Maven Assembly](https://maven.apache.org/plugins/maven-assembly-plugin/) för att skapa kontextarkivet för Docker-bygget och tilldela rätt klassificerare till det.

Du kan skapa gränssnittstester med olika tekniker och ramverk, men i det här avsnittet förutsätts att ditt projekt är utformat på ett sätt som liknar följande.

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

Filen `pom.xml` tar hand om Maven-bygget. Lägg till en exekvering av Maven Assembly Plugin som liknar följande.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Den här körningen instruerar Maven Assembly Plugin att skapa ett arkiv baserat på instruktionerna i `assembly-ui-test-docker-context.xml`, som kallas **sammansättningsbeskrivare** i plugin-programmets jargon. Sammansättningsbeskrivningen visar alla filer som måste ingå i arkivet.

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

Sammansättningsbeskrivningen instruerar plugin-programmet att skapa ett arkiv av typen `.tar.gz` och tilldelar klassificeraren `ui-test-docker-context` till det. Dessutom listas de filer som måste ingå i arkivet, inklusive följande:

* A `Dockerfile`, obligatoriskt för att skapa dockningsbilden
* Skriptet `wait-for-grid.sh` vars syften beskrivs nedan
* De faktiska UI-testerna, som implementeras av ett Node.js-projekt i mappen `test-module`

Sammansättningsbeskrivningen utesluter också vissa filer som kan genereras när användargränssnittstesterna körs lokalt. Detta garanterar ett mindre arkiv och snabbare byggen.

Arkivet som innehåller Docker-byggkontexten hämtas automatiskt av Cloud Manager, som kommer att skapa en Docker-bild som innehåller testerna i samband med driftsättningen. Så småningom kommer Cloud Manager att köra Docker-bilden för att köra UI-testerna mot ditt program.

Bygget ska antingen producera noll eller ett arkiv. Om inga arkiv skapas godkänns teststeget som standard. Om bygget skapar mer än ett arkiv är det valda arkivet inte deterministiskt.

### Kundens deltagande {#customer-opt-in}

För att Cloud Manager ska kunna bygga och köra dina gränssnittstester måste du välja den här funktionen genom att lägga till en fil i databasen.

* Filnamnet måste vara `testing.properties`.
* Filinnehållet måste vara `ui-tests.version=1`.
* Filen måste finnas under maven-undermodulen för gränssnittstester bredvid filen `pom.xml` i undermodulen för gränssnittstester.
* Filen måste finnas i roten för den inbyggda `tar.gz`-filen.

UI-testerna byggs och körningarna hoppas över om filen inte finns.

Om du vill inkludera en `testing.properties`-fil i build-artefakten lägger du till en `include` -sats i filen `assembly-ui-test-docker-context.xml`.

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>Om projektet inte innehåller den här raden redigerar du filen för att välja gränssnittstestning.
>
>Filen kan innehålla en rad som anger att den inte ska redigeras. Detta beror på att det introducerades i ditt projekt innan gränssnittstestning för deltagande introducerades och att klienterna inte var avsedda att redigera filen. Detta kan ignoreras.

Om du använder exemplen från Adobe:

* För den JavaScript-baserade `ui.tests`-mappen som genereras baserat på [AEM Project Archettype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) kan du köra nedanstående kommando för att lägga till den konfiguration som krävs.

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Testexemplen av Cypress och Java Selenium som tillhandahålls av Adobe har redan flaggan opt-in.

## Skriver gränssnittstester {#writing-ui-tests}

I det här avsnittet beskrivs de konventioner som Docker-bilden som innehåller dina gränssnittstester måste följa. Docker-bilden är inbyggd i Docker-konstruktionssammanhanget som beskrivs i föregående avsnitt.

### Miljövariabler {#environment-variables}

Följande miljövariabler skickas till din Docker-bild vid körning, beroende på ditt ramverk.

| Variabel | Exempel | Beskrivning | Testramverk |
|----------------------------|----------------------------------|---------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL för Selenium-servern | Endast selen |
| `SELENIUM_BROWSER` | `chrome` | Webbläsarimplementeringen som används av Selenium Server | Endast selen |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL:en för AEM författarinstans | Alla |
| `AEM_AUTHOR_USERNAME` | `admin` | Användarnamnet som ska loggas in i AEM författarinstans | Alla |
| `AEM_AUTHOR_PASSWORD` | `admin` | Lösenordet för att logga in på AEM författarinstans | Alla |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL:en för AEM publiceringsinstans | Alla |
| `AEM_PUBLISH_USERNAME` | `admin` | Användarnamnet som ska loggas in på AEM publiceringsinstans | Alla |
| `AEM_PUBLISH_PASSWORD` | `admin` | Lösenordet för att logga in på AEM publiceringsinstans | Alla |
| `REPORTS_PATH` | `/usr/src/app/reports` | Sökvägen där XML-rapporten för testresultaten måste sparas | Alla |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | URL:en som filen måste laddas upp till för att göra dem tillgängliga för testramverket | Alla |
| `PROXY_HOST` | `proxy-host` | Värdnamnet för den interna HTTP-proxy som ska användas av testramverket | Alla utom selen |
| `PROXY_HTTPS_PORT` | `8071` | Proxyserverns lyssnarport för HTTPS-anslutningar (kan vara tom) | Alla utom selen |
| `PROXY_HTTP_PORT` | `8070` | Proxyserverns lyssnarport för HTTP-anslutningar (kan vara tom) | Alla utom selen |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | Sökvägen till certifikatutfärdarcertifikatet som ska användas av testramverket | Alla utom selen |
| `PROXY_OBSERVABILITY_PORT` | `8081` | HTTP-hälsokontrollporten för proxyservern | Alla utom selen |
| `PROXY_RETRY_ATTEMPTS` | `12` | Föreslaget antal nya försök i väntan på att proxyservern ska vara klar | Alla utom selen |
| `PROXY_RETRY_DELAY` | `5` | Föreslagen fördröjning mellan nya försök i väntan på proxyserverberedskap | Alla utom selen |

Provexemplen från Adobe ger hjälpfunktioner för att komma åt konfigurationsparametrarna:

* Cypress: använd standardfunktionen `Cypress.env('VARIABLE_NAME')`
* JavaScript: Se modulen [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js)
* Java: Se klassen [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java)

### Generera testrapporter {#generate-test-reports}

Docker-avbildningen måste generera testrapporter i JUnit XML-format och spara dem i den sökväg som anges av miljövariabeln `REPORTS_PATH`. JUnit XML-formatet är ett format som ofta används för att rapportera testresultat. Om Docker-bilden använder Java och Maven kan standardtestmoduler som [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) och [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/) generera sådana rapporter direkt från paketet.

Om Docker-bilden implementeras med andra programmeringsspråk eller testkörare bör du kontrollera i dokumentationen vilka verktyg som har valts för att skapa JUnit XML-rapporter.

>[!NOTE]
>
>Resultatet av UI-teststeget utvärderas endast baserat på testrapporter. Se till att du genererar rapporten i enlighet med din testkörning.
>
>Använd kontroller i stället för att bara logga ett fel till STDERR eller returnera en avslutningskod som inte är noll, annars kan distributionsflödet fortsätta normalt.
>
>Om en HTTP-proxy användes under testkörningen kommer resultatet att innehålla en `request.log`-fil.

### Förutsättningar {#prerequisites}

* Testerna i Cloud Manager körs med en teknisk administratörsanvändare.

>[!NOTE]
>
>Om du vill köra funktionstester från den lokala datorn skapar du en användare med administratörsliknande behörigheter för att uppnå samma beteende.

* Den inneslutna infrastruktur som omfattar funktionstestning begränsas av följande gränser:

| Typ | Värde | Beskrivning |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2,0 | Den processortid som reserverats per testkörning |
| Minne | 1 Gi | Mängd minne som tilldelats testet, värde i gibibyte |
| Timeout | 30 m | Den varaktighet efter vilken provningen avslutas. |
| Rekommenderad varaktighet | 15 m | Adobe rekommenderar att testet inte tar längre tid än så här. |

>[!NOTE]
>
> Om du behöver mer resurser kan du skapa ett kundvårdsärende och beskriva ditt användningsfall. Adobe granskar din begäran och ger dig lämplig hjälp.

## Selenumspecifik information

>[!NOTE]
>
>Detta avsnitt gäller endast när Selenium är den valda testinfrastrukturen.

### Väntar på att Selenium ska vara klart {#waiting-for-selenium}

Innan testerna börjar är det dockningsbildens ansvar att säkerställa att Selenium-servern är igång. Att vänta på Selenium-tjänsten är en tvåstegsprocess.

1. Läs URL:en för Selenium-tjänsten från miljövariabeln `SELENIUM_BASE_URL`.
1. Avsök med regelbundna mellanrum mot [statusslutpunkten](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) som exponeras av Selenium API.

När Seleniums statusendpoint svarar med ett positivt svar kan testerna börja.

Adobe UI-testexemplen hanterar detta med skriptet `wait-for-grid.sh`, som körs när Docker startas och startar den faktiska testkörningen först när rutnätet är klart.

### Hämta skärmbilder och video {#capture-screenshots}

Docker-avbildningen kan generera ytterligare testutdata (till exempel skärmbilder eller videor) och spara dem i den sökväg som anges av miljövariabeln `REPORTS_PATH`. Alla filer som `REPORTS_PATH` finns nedan ingår i arkivet för testresultat.

De testexempel som tillhandahålls av Adobe skapar som standard skärmbilder för alla misslyckade tester.

Du kan använda hjälpfunktionerna för att skapa skärmdumpar genom dina tester.

* JavaScript: [kommandot takeScreenshot](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Kommandon](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

Om ett testresultatarkiv skapas under en testkörning av ett användargränssnitt kan du hämta det från Cloud Manager med knappen `Download Details` under steget [**Anpassad användargränssnittstestning**](/help/implementing/cloud-manager/deploy-code.md).

### Överför filer {#upload-files}

Testerna ibland måste överföra filer till det program som testas. För att driftsättningen av Selenium ska vara flexibel i förhållande till dina tester går det inte att överföra en resurs direkt till Selenium. Om du vill överföra en fil måste du i stället utföra följande steg.

1. Överför filen på den URL som anges av miljövariabeln `UPLOAD_URL`.
   * Överföringen måste utföras i en POST med ett multipart-formulär.
   * Multipart-formuläret måste ha ett enda filfält.
   * Detta motsvarar `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Läs dokumentationen och biblioteken för programmeringsspråket som används i Docker-bilden för att få reda på hur en sådan HTTP-begäran ska utföras.
   * Testexemplen från Adobe innehåller hjälpfunktioner för att överföra filer:
      * JavaScript: Se kommandot [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js).
      * Java: Se klassen [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java).
1. Om överföringen lyckas returnerar begäran ett `200 OK`-svar av typen `text/plain`.
   * Svarets innehåll är ett ogenomskinligt filhandtag.
   * Du kan använda den här referensen i stället för en filsökväg i ett `<input>`-element för att testa filöverföringar i programmet.

## Cypressspecifik information

>[!NOTE]
>
>Detta avsnitt gäller endast när Cypress är den valda testinfrastrukturen.

### Konfigurera HTTP-proxy

Docker-behållarens ingångspunkt måste kontrollera värdet för miljövariabeln `PROXY_HOST`.

Om det här värdet är tomt behövs inga ytterligare steg och testerna ska köras utan HTTP-proxy.

Om det inte är tomt måste entrypoint-skriptet:

1. Konfigurera en HTTP-proxyanslutning för att köra UI-tester. Detta kan uppnås genom att exportera miljövariabeln `HTTP_PROXY` som har skapats med följande värden:
   * Proxyvärd, som tillhandahålls av variabeln `PROXY_HOST`
   * Proxyport, som tillhandahålls av variabeln `PROXY_HTTPS_PORT` eller `PROXY_HTTP_PORT` (variabeln med ett värde som inte är tomt används)
2. Ange det certifikatutfärdarcertifikat som ska användas vid anslutning till HTTP-proxyn. Dess plats anges av variabeln `PROXY_CA_PATH`.
   * Detta kan uppnås genom att exportera miljövariabeln `NODE_EXTRA_CA_CERTS`.
3. Vänta tills HTTP-proxyn är klar.
   * För att kontrollera beredskapen används miljövariablerna `PROXY_HOST`, `PROXY_OBSERVABILITY_PORT`, `PROXY_RETRY_ATTEMPTS` och `PROXY_RETRY_DELAY` kan användas.
   * Du kan kontrollera med hjälp av en cURL-begäran och se till att installera cURL i din `Dockerfile`.

Ett exempel på implementering finns i Cypress Sample Test Module&#39;s Entrypoint på [GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh).

## Uppspelningsspecifik information

>[!NOTE]
>
> Det här avsnittet gäller bara när Playwright är den valda testinfrastrukturen.

### Konfigurera HTTP-proxy

>[!NOTE]
>
> I presenterade exempel antar vi att Chrome används som projektwebbläsare.

På liknande sätt som för Cypress måste testerna använda HTTP-proxyn om en `PROXY_HOST`-miljövariabel som inte är tom anges.

För att göra detta måste följande ändringar göras.

#### Dockerfile

Installera cURL och `libnss3-tools`, som tillhandahåller `certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### Skript för ingångspunkt

Inkludera ett basskript som, om miljövariabeln `PROXY_HOST` anges, gör följande:

1. Exportera proxyrelaterade variabler som `HTTP_PROXY` och `NODE_EXTRA_CA_CERTS`
2. Använd `certutil` för att installera proxy-CA-certifikat för krom
3. Vänta tills HTTP-proxyn är klar (eller avsluta vid fel).

Exempel på implementering:

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### Playright configuration

Ändra konfigurationen för uppspelningsrättigheten (till exempel i `playwright.config.js`) så att en proxy används om miljövariabeln `HTTP_PROXY` anges.

Exempel på implementering:

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

## Köra gränssnittstester lokalt {#run-ui-tests-locally}

Innan gränssnittstester aktiveras i en Cloud Manager-pipeline bör gränssnittstester köras lokalt mot [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) eller mot en faktisk AEM as a Cloud Service-instans.

### Cypress-testexempel {#cypress-sample}

1. Öppna ett skal och navigera till mappen `ui.tests/test-module` i din databas

1. Installera Cypress och andra krav

   ```shell
   npm install
   ```

1. Ange de systemvariabler som krävs för testkörning

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. Köra tester med något av följande kommandon

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>Loggfilerna lagras i mappen i databasen `target/` .
>
>Mer information finns i [Databas för](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md) AEM testprover.

### Exempel på JavaScript WebdriverIO-test {#javascript-sample}

1. Öppna ett skal och navigera till `ui.tests` mappen i ditt repository

1. Kör nedanstående kommando för att starta testerna med Maven

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* Detta startar en fristående seleninstans och kör testerna mot den.
>* Loggfilerna lagras i mappen `target/reports` i databasen
>* Du måste se till att datorn kör den senaste Chrome-versionen när testet automatiskt hämtar den senaste versionen av ChromeDriver för testning.
>
>Mer information finns i [AEM Project Archetype-databas](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md).

### Java Selenium WebDriver Test Sample {#java-sample}

1. Öppna ett skal och navigera till mappen `ui.tests/test-module` i din databas

1. Kör nedanstående kommandon för att starta testerna med Maven

   ```shell
   # Start selenium docker image (for x64 CPUs)
   docker run --platform linux/amd64 -d -p 4444:4444 selenium/standalone-chrome-debug:latest
   
   # Start selenium docker image (for ARM CPUs)
   docker run -d -p 4444:4444 seleniarm/standalone-chromium
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>Loggfilerna lagras i mappen `target/reports` i databasen.
>
>Mer information finns i [AEM Test Samples-databasen](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
