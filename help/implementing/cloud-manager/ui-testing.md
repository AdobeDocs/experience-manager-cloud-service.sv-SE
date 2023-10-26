---
title: UI-testning
description: Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina anpassade program
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2389'
ht-degree: 0%

---


# UI-testning {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI-testning"
>abstract="Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium)."

Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program.

## Översikt {#custom-ui-testing}

AEM innehåller en integrerad svit med [Kvalitetsportar för Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) för smidiga uppdateringar av anpassade program. I synnerhet har IT-testportar redan stöd för att skapa och automatisera anpassade tester med AEM API:er.

Användargränssnittstester är paketerade i en Docker-bild för att ge ett brett val i språk och miljöer (som Cypress, Selenium, Java och Maven samt JavaScript). Dessutom kan ett UI-testprojekt enkelt genereras med [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Adobe uppmuntrar användningen av Cypress eftersom det ger realtidsladdning och automatisk väntetid, vilket sparar tid och förbättrar produktiviteten under testningen. Cypress har också en enkel och intuitiv syntax som gör det enkelt att lära sig och använda, även för dem som inte har testat tidigare.

Gränssnittstester utförs som en del av en viss kvalitetsgrind för varje Cloud Manager-pipeline med en [**Anpassade gränssnittstestningar** steg](/help/implementing/cloud-manager/deploy-code.md) in [produktionsrörledningar](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) eller valfritt [rörledningar för icke-produktion](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Alla gränssnittstester, inklusive regression och nya funktioner, gör att fel kan upptäckas och rapporteras.

Till skillnad från anpassade funktionstester, som är HTTP-tester skrivna i Java, kan gränssnittstester vara en dockningsbild med tester skrivna på vilket språk som helst, förutsatt att de följer konventionerna som definieras i avsnittet [Skapar gränssnittstester](#building-ui-tests).

>[!TIP]
>
>Adobe rekommenderar att du använder Cypress för UI-testning enligt koden i [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).
> 
>Adobe innehåller även exempel på gränssnittstestmoduler baserade på JavaScript med WebdriverIO (se [AEM Project Archettype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) och Java med WebDriver (se [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)).

## Kom igång med gränssnittstester {#get-started-ui-tests}

I det här avsnittet beskrivs stegen som krävs för att konfigurera gränssnittstester för körning i Cloud Manager.

1. Bestäm vilket programmeringsspråk du vill använda.

   * För Cypress använder du exempelkoden från [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).

   * För JavaScript och WDIO använder du exempelkoden som automatiskt genereras i `ui.tests` i din Cloud Manager-databas.

     >[!NOTE]
     >
     >Om din databas skapades innan Cloud Manager skapades automatiskt `ui.tests` kan du även generera den senaste versionen med [AEM Project Archettype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests).

   * För Java och WebDriver använder du exempelkoden i [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver).

   * För andra programmeringsspråk, se avsnittet [Skapar gränssnittstester](#building-ui-tests) i det här dokumentet för att konfigurera testprojektet.

1. Se till att gränssnittstestning är aktiverat enligt avsnittet [Kundens deltagande](#customer-opt-in) i det här dokumentet.

1. Utveckla testfall och [köra testerna lokalt](#run-ui-tests-locally).

1. Implementera koden i molnhanterarens databas och kör en Cloud Manager-pipeline.

## Skapar gränssnittstester {#building-ui-tests}

Ett Maven-projekt genererar ett Docker-byggsammanhang. I denna Docker build-kontext beskrivs hur du skapar en Docker-bild som innehåller gränssnittstester, som används i Cloud Manager för att generera en Docker-bild som innehåller de faktiska gränssnittstester.

I det här avsnittet beskrivs stegen som krävs för att lägga till ett UI-testprojekt i din databas.

>[!TIP]
>
>The [AEM Project Archettype](https://github.com/adobe/aem-project-archetype) Du kan generera ett UI-testprojekt åt dig, som uppfyller följande beskrivning, om du inte har några särskilda krav för programmeringsspråket.

### Skapa en kontext för Docker Build {#generate-docker-build-context}

För att skapa en Docker-byggkontext behöver du en Maven-modul som:

* Skapar ett arkiv som innehåller en `Dockerfile` och alla andra filer som behövs för att bygga Docker-bilden med testerna.
* Taggar arkivet med `ui-test-docker-context` klassificerare.

Det enklaste sättet att göra detta är att konfigurera [Maven Assembly Plugin](https://maven.apache.org/plugins/maven-assembly-plugin/) för att skapa kontextarkivet för Docker-bygget och tilldela rätt klassificerare till det.

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

The `pom.xml` filen tar hand om Maven-bygget. Lägg till en exekvering av Maven Assembly Plugin som liknar följande.

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

Den här exekveringen instruerar Maven Assembly Plugin att skapa ett arkiv baserat på instruktionerna i `assembly-ui-test-docker-context.xml`, som kallas **sammansättningsbeskrivning** i pluginens jargon. Sammansättningsbeskrivningen visar alla filer som måste ingå i arkivet.

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

Sammansättningsbeskrivningen instruerar plugin-programmet att skapa ett arkiv av typen `.tar.gz` och tilldelar `ui-test-docker-context` -klassificerare. Dessutom listas de filer som måste ingå i arkivet, inklusive följande:

* A `Dockerfile`, obligatoriskt för att bygga dockningsbilden
* The `wait-for-grid.sh` skript, vars syften beskrivs nedan
* De faktiska gränssnittstesterna, som implementeras av ett Node.js-projekt i `test-module` mapp

Sammansättningsbeskrivningen utesluter också vissa filer som kan genereras när användargränssnittstesterna körs lokalt. Detta garanterar ett mindre arkiv och snabbare byggen.

Arkivet som innehåller Docker-byggkontexten hämtas automatiskt av Cloud Manager, som skapar Docker-bilden som innehåller testerna i samband med driftsättningen. Till slut körs Docker-avbildningen i Cloud Manager för att köra UI-testerna mot ditt program.

Bygget ska antingen producera noll eller ett arkiv. Om inga arkiv skapas godkänns teststeget som standard. Om bygget skapar mer än ett arkiv är det valda arkivet inte deterministiskt.

### Kundens deltagande {#customer-opt-in}

För att Cloud Manager ska kunna bygga och köra dina gränssnittstester måste du välja den här funktionen genom att lägga till en fil i databasen.

* Filnamnet måste vara `testing.properties`.
* Filinnehållet måste vara `ui-tests.version=1`.
* Filen måste finnas under maven-undermodulen för gränssnittstester intill `pom.xml` fil för undermodulen för gränssnittstester.
* Filen måste finnas i roten för den inbyggda `tar.gz` -fil.

UI-testerna byggs och körningarna hoppas över om filen inte finns.

Ta med en `testing.properties` fil i build-artefakten, lägga till en `include` programsats i `assembly-ui-test-docker-context.xml` -fil.

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
>Om projektet inte innehåller den här raden måste du redigera filen för att kunna välja gränssnittstestning.
>
>Filen kan innehålla en rad som anger att den inte ska redigeras. Detta beror på att det introducerades i ditt projekt innan gränssnittstestning för deltagande introducerades och att klienterna inte var avsedda att redigera filen. Detta kan ignoreras.

Om du använder exemplen från Adobe:

* För JavaScript-baserade `ui.tests` mapp som genererats baserat på [AEM Project Archettype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)kan du köra nedanstående kommando för att lägga till den konfiguration som krävs.

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
|---|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL för Selenium-servern | Endast selen |
| `SELENIUM_BROWSER` | `chrome` | Webbläsarimplementeringen som används av Selenium Server | Endast selen |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL:en för AEM författarinstans | Alla |
| `AEM_AUTHOR_USERNAME` | `admin` | Användarnamnet som ska loggas in i AEM författarinstans | Alla |
| `AEM_AUTHOR_PASSWORD` | `admin` | Lösenordet för att logga in på AEM författarinstans | Alla |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL:en för AEM publiceringsinstans | Alla |
| `AEM_PUBLISH_USERNAME` | `admin` | Användarnamnet som ska loggas in på AEM publiceringsinstans | Alla |
| `AEM_PUBLISH_PASSWORD` | `admin` | Lösenordet för att logga in på AEM publiceringsinstans | Alla |
| `REPORTS_PATH` | `/usr/src/app/reports` | Sökvägen där XML-rapporten för testresultaten måste sparas | Alla |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | Den URL till vilken filen måste överföras för att göra den tillgänglig för testramverket | Alla |

Provexemplen från Adobe ger hjälpfunktioner för att komma åt konfigurationsparametrarna:

* Cypress: använd standardfunktionen `Cypress.env('VARIABLE_NAME')`
* JavaScript: Se [lib/config.js](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/config.js) modul
* Java: Se [Konfig](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) class

### Generera testrapporter {#generate-test-reports}

Docker-bilden måste generera testrapporter i JUnit XML-format och spara dem i den sökväg som anges av systemvariabeln `REPORTS_PATH`. JUnit XML-formatet är ett format som ofta används för att rapportera testresultat. Om Docker-bilden använder Java och Maven, standardtestmoduler som [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) och [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/) kan generera sådana rapporter direkt.

Om Docker-bilden implementeras med andra programmeringsspråk eller testkörare bör du kontrollera i dokumentationen vilka verktyg som har valts för att skapa JUnit XML-rapporter.

>[!NOTE]
>
>Resultatet av UI-teststeget utvärderas endast baserat på testrapporter. Se till att du genererar rapporten i enlighet med din testkörning.
>
>Använd kontroller i stället för att bara logga ett fel till STDERR eller returnera en avslutningskod som inte är noll, annars kan distributionsflödet fortsätta normalt.

### Förutsättningar {#prerequisites}

* Testerna i Cloud Manager körs med en teknisk administratörsanvändare.

>[!NOTE]
>
>Om du vill köra funktionstester från den lokala datorn skapar du en användare med administratörsliknande behörigheter för att uppnå samma beteende.

* Den inneslutna infrastruktur som omfattar funktionstestning begränsas av följande gränser:

| Typ | Värde | Beskrivning |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | Den processortid som reserverats per testkörning |
| Minne | 1Gi | Mängd minne som tilldelats testet, värde i gibibyte |
| Timeout | 30m | Den varaktighet efter vilken provningen avslutas. |
| Rekommenderad varaktighet | 15m | Adobe rekommenderar att testet inte tar längre tid än så här. |

>[!NOTE]
>
> Om du behöver mer resurser kan du skapa ett kundvårdsärende och beskriva ditt användningsfall. Adobe granskar din begäran och ger dig lämplig hjälp.

## Selenumspecifik information

>[!NOTE]
>
>Detta avsnitt gäller endast när Selenium är den valda testinfrastrukturen.

### Väntar på att Selenium ska vara klart {#waiting-for-selenium}

Innan testerna börjar är det dockningsbildens ansvar att säkerställa att Selenium-servern är igång. Att vänta på Selenium-tjänsten är en tvåstegsprocess.

1. Läs URL:en för Selenium-tjänsten på `SELENIUM_BASE_URL` miljövariabel.
1. Avsökning med regelbundna mellanrum till [statusslutpunkt](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exponeras av Selenium API.

När Seleniums statusendpoint svarar med ett positivt svar kan testerna börja.

Adobe UI-testexemplen hanterar detta med skriptet `wait-for-grid.sh`, som körs när Docker startar och startar den faktiska testkörningen först när rutnätet är klart.

### Hämta skärmbilder och video {#capture-screenshots}

Docker-bilden kan generera ytterligare testutdata (till exempel skärmbilder eller videoklipp) och spara dem i den sökväg som anges av systemvariabeln `REPORTS_PATH`. Alla filer som finns under `REPORTS_PATH` ingår i testresultatarkivet.

Testexemplen från Adobe skapar som standard skärmbilder för misslyckade tester.

Du kan använda hjälpfunktionerna för att skapa skärmbilder genom testerna.

* JavaScript: [kommandot takeScreenshot](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Kommandon](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

Om ett testresultatarkiv skapas under en UI-testkörning kan du hämta det från Cloud Manager med `Download Details` knappen under [**Anpassade gränssnittstestningar** steg](/help/implementing/cloud-manager/deploy-code.md).

### Överför filer {#upload-files}

Testerna ibland måste överföra filer till det program som testas. För att driftsättningen av Selenium ska vara flexibel i förhållande till dina tester går det inte att överföra en resurs direkt till Selenium. Om du vill överföra en fil måste du i stället utföra följande steg.

1. Överför filen på den URL som anges av `UPLOAD_URL` miljövariabel.
   * Överföringen måste utföras i en POST med ett multipart-formulär.
   * Multipart-formuläret måste ha ett enda filfält.
   * Detta motsvarar `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Läs dokumentationen och biblioteken för programmeringsspråket som används i Docker-bilden för att få reda på hur en sådan HTTP-begäran ska utföras.
   * Testexemplen från Adobe innehåller hjälpfunktioner för att överföra filer:
      * JavaScript: Se [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) -kommando.
      * Java: Se [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) klassen.
1. Om överföringen lyckas returnerar begäran en `200 OK` typsvar `text/plain`.
   * Svarets innehåll är ett ogenomskinligt filhandtag.
   * Du kan använda det här handtaget i stället för en filsökväg i en `<input>` -element för att testa filöverföringar i programmet.

## Köra gränssnittstester lokalt {#run-ui-tests-locally}

Innan gränssnittstester aktiveras i en Cloud Manager-pipeline bör gränssnittstester köras lokalt mot [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) eller mot en faktisk AEM as a Cloud Service instans.

### Cypress-testexempel {#cypress-sample}

1. Öppna ett skal och navigera till `ui.tests/test-module` mapp i din databas

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
>Loggfilerna lagras i `target/` -mapp i din databas.
>
>Mer information finns i [AEM Test Samples](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md).

### JavaScript WebdriverIO-testexempel {#javascript-sample}

1. Öppna ett skal och navigera till `ui.tests` mapp i din databas

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
>* Loggfilerna lagras i `target/reports` mapp i din databas
>* Du måste se till att datorn kör den senaste Chrome-versionen när testet hämtar den senaste versionen av ChromeDriver automatiskt för testning.
>
>Mer information finns i [AEM Project Archetype-databas](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md).

### Java Selenium WebDriver Test Sample {#java-sample}

1. Öppna ett skal och navigera till `ui.tests/test-module` mapp i din databas

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
>Loggfilerna lagras i `target/reports` -mapp i din databas.
>
>Mer information finns i [AEM Test Samples](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
