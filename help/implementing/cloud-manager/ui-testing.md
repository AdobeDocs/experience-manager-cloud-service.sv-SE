---
title: UI-testning
description: Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina anpassade program
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 0ea7255f4dfc5c9f2e99cb144ef58152a2565822
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 0%

---


# UI-testning {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI-testning"
>abstract="Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium)."

Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program.

## Översikt {#custom-ui-testing}

AEM innehåller en integrerad svit med [Kvalitetsportar för Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) för smidiga uppdateringar av anpassade program. I synnerhet kommer IT-tester redan igång och automatisering av anpassade tester med AEM API:er.

Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium). Dessutom kan ett UI-testprojekt enkelt genereras med [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Gränssnittstester utförs som en del av en viss kvalitetsgrind för varje Cloud Manager-pipeline med en [dedikerad **Testning av anpassat användargränssnitt** steg.](/help/implementing/cloud-manager/deploy-code.md) Alla gränssnittstester, inklusive regression och nya funktioner, gör att fel kan upptäckas och rapporteras.

Till skillnad från anpassade funktionstester, som är HTTP-tester skrivna i Java, kan gränssnittstester vara en dockningsbild med tester skrivna på vilket språk som helst, förutsatt att de följer konventionerna som definieras i avsnittet [Bygger gränssnittstester.](#building-ui-tests)

>[!TIP]
>
>Adobe rekommenderar att du följer strukturen och språket (JavaScript och WDIO) i [AEM Project Archetype.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

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

## Skapar gränssnittstester {#building-ui-tests}

Ett Maven-projekt genererar ett Docker-byggsammanhang. I denna Docker-byggkontext beskrivs hur du skapar en Docker-bild som innehåller användargränssnittstester, som Cloud Manager-användare använder för att skapa en Docker-bild som innehåller de faktiska användargränssnittstester.

I det här avsnittet beskrivs stegen som krävs för att lägga till ett UI-testprojekt i din databas.

>[!TIP]
>
>The [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) Du kan generera ett UI-testprojekt utan särskilda krav för programmeringsspråket.

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

Sammansättningsbeskrivningen instruerar plugin-programmet att skapa ett arkiv av typen `.tar.gz` och tilldelar `ui-test-docker-context` klassificerare. Dessutom listas de filer som måste ingå i arkivet, inklusive följande:

* A `Dockerfile`, obligatoriskt för att bygga dockningsbilden
* The `wait-for-grid.sh` skript, vars syften beskrivs nedan
* De faktiska gränssnittstesterna, som implementeras av ett Node.js-projekt i `test-module` mapp

Sammansättningsbeskrivningen utesluter också vissa filer som kan genereras när gränssnittstesterna körs lokalt. Detta garanterar ett mindre arkiv och snabbare byggen.

Arkivet som innehåller Docker-byggkontexten hämtas automatiskt av Cloud Manager, som skapar Docker-bilden som innehåller testerna i samband med driftsättningen. Till slut körs Docker-avbildningen i Cloud Manager för att köra gränssnittstester mot ditt program.

Bygget ska antingen producera noll eller ett arkiv. Om inga arkiv skapas godkänns teststeget som standard. Om bygget skapar mer än ett arkiv är det valda arkivet inte deterministiskt.

## Skriver gränssnittstester {#writing-ui-tests}

I det här avsnittet beskrivs de konventioner som Docker-bilden med dina gränssnittstester måste följa. Docker-bilden är inbyggd i Docker-konstruktionssammanhanget som beskrivs i föregående avsnitt.

### Miljövariabler {#environment-variables}

Följande miljövariabler skickas till Docker-bilden vid körning.

| Variabel | Exempel | Beskrivning |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL:en för Selenium-servern |
| `SELENIUM_BROWSER` | `chrome` | Webbläsarimplementeringen som används av Selenium Server |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL:en för AEM författarinstans |
| `AEM_AUTHOR_USERNAME` | `admin` | Användarnamnet som ska loggas in till AEM författarinstans |
| `AEM_AUTHOR_PASSWORD` | `admin` | Lösenordet för inloggning på AEM författarinstans |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL:en för den AEM publiceringsinstansen |
| `AEM_PUBLISH_USERNAME` | `admin` | Användarnamnet som ska loggas in på AEM publiceringsinstans |
| `AEM_PUBLISH_PASSWORD` | `admin` | Lösenordet för att logga in på AEM publiceringsinstans |
| `REPORTS_PATH` | `/usr/src/app/reports` | Sökvägen där XML-rapporten för testresultaten måste sparas |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | Den URL dit filen måste överföras för att göra den tillgänglig för Selenium |

### Väntar på att Selenium ska vara klart {#waiting-for-selenium}

Innan testerna börjar är det dockningsbildens ansvar att säkerställa att Selenium-servern är igång. Att vänta på Selenium-tjänsten är en tvåstegsprocess.

1. Läs URL:en för Selenium-tjänsten på `SELENIUM_BASE_URL` systemvariabel.
1. Avsökning med regelbundna intervall till [statusslutpunkt](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exponeras av Selenium API.

När Seleniums statusendpoint svarar med ett positivt svar kan testerna börja.

### Generera testrapporter {#generate-test-reports}

Docker-bilden måste generera testrapporter i JUnit XML-format och spara dem i den sökväg som anges av systemvariabeln `REPORTS_PATH`. JUnit XML-formatet är ett vanligt format för rapportering av testresultat. Om Docker-bilden använder Java och Maven, standardtestmoduler som [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) och [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/) kan generera sådana rapporter direkt.

Om Docker-bilden implementeras med andra programmeringsspråk eller testkörare bör du kontrollera i dokumentationen vilka verktyg som har valts för att skapa JUnit XML-rapporter.

### Hämta skärmbilder och video {#capture-screenshots}

Docker-bilden kan generera ytterligare testutdata (t.ex. skärmbilder, videor) och spara dem i den sökväg som anges av systemvariabeln `REPORTS_PATH`. Alla filer som finns under `REPORTS_PATH` ingår i testresultatarkivet.

Om ett testresultatarkiv har skapats under en UI-testkörning innehåller testloggfilen i slutet en referens till platsen för testresultatarkivet.

```
[...]

===============================================================
The detailed test results can be downloaded from the URL below.
Note: the link will expire after 60 days

    https://results-host/test-results.zip

===============================================================
```

### Överför filer {#upload-files}

Testerna ibland måste överföra filer till det program som testas. För att driftsättningen av Selenium ska vara flexibel i förhållande till dina tester är det inte möjligt att ladda upp en resurs direkt till Selenium. Om du vill överföra en fil måste du i stället utföra följande steg.

1. Överför filen på den URL som anges av `UPLOAD_URL` systemvariabel.
   * Överföringen måste utföras i en POST med ett multipart-formulär.
   * Multipart-formuläret måste ha ett enda filfält.
   * Detta motsvarar `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Läs dokumentationen och biblioteken för programmeringsspråket som används i Docker-bilden för att få reda på hur en sådan HTTP-begäran ska utföras.
1. Om överföringen lyckas returnerar begäran en `200 OK` typsvar `text/plain`.
   * Svarets innehåll är ett ogenomskinligt filhandtag.
   * Du kan använda det här handtaget i stället för en filsökväg i en `<input>` -element för att testa filöverföringar i programmet.
