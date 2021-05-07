---
title: UI-testning - Cloud Services
description: UI-testning - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Gränssnittstestning {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI-testning"
>abstract="Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium). Docker-bilden kan skapas med standardverktyg, men måste följa vissa regler när den körs. När du kör Docker-bilden etableras en Selenium-server automatiskt. Med de runtime-konventioner som beskrivs nedan kan din testkod få åtkomst till både Selenium-servern och AEM instanser som testas."

Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium). Docker-bilden kan skapas med standardverktyg, men måste följa vissa regler när den körs. När du kör Docker-bilden etableras en Selenium-server automatiskt. Med de runtime-konventioner som beskrivs nedan kan din testkod få åtkomst till både Selenium-servern och AEM instanser som testas.

>[!NOTE]
> Scen- och produktionsrörledningar som skapats före den 10 februari 2021 måste uppdateras för att de UI-tester som beskrivs på den här sidan ska kunna användas.
> Se [Konfigurera CI-CD-pipeline](/help/implementing/cloud-manager/configure-pipeline.md) för information om pipeline-konfigurationen.

## Skapar gränssnittstester {#building-ui-tests}

UI-tester är byggda utifrån Docker-byggkontext som genereras av ett Maven-projekt. Cloud Manager använder Docker-byggkontexten för att generera en Docker-bild som innehåller de faktiska gränssnittstesterna. Sammanfattningsvis genererar ett Maven-projekt en Docker-byggkontext och Docker-byggkontexten beskriver hur du skapar en Docker-bild som innehåller UI-testerna.

I det här avsnittet beskrivs stegen som krävs för att lägga till ett UI-testprojekt i din databas. Om du har bråttom eller inte har några särskilda krav för programmeringsspråket, kan [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) generera ett UI Tests-projekt åt dig.

### Skapa en Docker-byggkontext {#generate-docker-build-context}

För att skapa en Docker-byggkontext behöver du en Maven-modul som:

- Skapar ett arkiv som innehåller en `Dockerfile` och alla andra filer som behövs för att skapa Docker-bilden med dina tester.
- Taggar arkivet med `ui-test-docker-context`-klassificeraren.

Det enklaste sättet att uppnå detta är att konfigurera plugin-programmet [Maven Assembly](http://maven.apache.org/plugins/maven-assembly-plugin/) för att skapa kontextarkivet för Docker-bygget och tilldela rätt klassificerare till det.

Du kan skapa gränssnittstester med olika tekniker och ramverk, men i det här avsnittet förutsätts att ditt projekt är utformat på ett sätt som liknar följande.

```
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

Den här körningen instruerar Maven Assembly Plugin att skapa ett arkiv baserat på instruktionerna i `assembly-ui-test-docker-context.xml`, som kallas sammansättningsbeskrivare i plugin-programmets jargon. Sammansättningsbeskrivningen visar alla filer som måste ingå i arkivet.

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

Sammansättningsbeskrivningen instruerar plugin-programmet att skapa ett arkiv av typen `.tar.gz` och tilldelar klassificeraren `ui-test-docker-context` till det. Dessutom listas de filer som måste ingå i arkivet:

- A `Dockerfile`, mandatory for building the Docker image.
- `wait-for-grid.sh`-skriptet, vars syften beskrivs nedan.
- De faktiska gränssnittstesterna, som implementeras av ett Node.js-projekt i mappen `test-module`.

Sammansättningsbeskrivningen utesluter också vissa filer som kan genereras när gränssnittstesterna körs lokalt. Detta garanterar ett mindre arkiv och snabbare byggen.

Arkivet som innehåller Docker-byggkontexten hämtas automatiskt av Cloud Manager, som skapar Docker-bilden som innehåller testerna under driftsättningsfasen. Till slut körs Docker-avbildningen i Cloud Manager för att köra gränssnittstester mot ditt program.

## Skriver gränssnittstester {#writing-ui-tests}

I det här avsnittet beskrivs de konventioner som Docker-bilden med dina gränssnittstester måste följa. Docker-bilden är inbyggd i Docker-konstruktionssammanhanget som beskrivs i föregående avsnitt.

### Miljövariabler {#environment-variables}

Följande miljövariabler skickas till Docker-bilden vid körning.

| Variabel | Exempel | Beskrivning |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL:en för Selenium-servern |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Webbläsarimplementeringen som används av Selenium Server |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL:en för AEM författarinstans |
| `AEM_AUTHOR_USERNAME` | `admin` | Användarnamnet som ska loggas in till AEM författarinstans |
| `AEM_AUTHOR_PASSWORD` | `admin` | Lösenordet för inloggning på AEM författarinstans |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL:en för den AEM publiceringsinstansen |
| `AEM_PUBLISH_USERNAME` | `admin` | Användarnamnet som ska loggas in till AEM publiceringsinstans |
| `AEM_PUBLISH_PASSWORD` | `admin` | Lösenordet för att logga in på AEM publiceringsinstans |
| `REPORTS_PATH` | `/usr/src/app/reports` | Sökvägen där XML-rapporten för testresultaten måste sparas |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | Den URL dit filen måste överföras för att göra den tillgänglig för Selenium |

### Väntar på att Selenium ska vara klart {#waiting-for-selenium}

Innan testerna börjar är det dockningsbildens ansvar att säkerställa att Selenium-servern är igång. Att vänta på Selenium-tjänsten är en tvåstegsprocess:

1. Läs URL:en för Selenium-tjänsten från miljövariabeln `SELENIUM_BASE_URL`.
2. Avsök med regelbundna mellanrum mot [statusslutpunkten](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) som exponeras av Selenium API.

När Seleniums statusendpoint svarar med ett positivt svar kan testerna slutligen börja.

### Generera testrapporter {#generate-test-reports}

Docker-bilden måste generera testrapporter i JUnit XML-format och spara dem i den sökväg som anges av miljövariabeln `REPORTS_PATH`. JUnit XML-formatet är ett utbrett format för rapportering av testresultat. Om Docker-bilden använder Java och Maven, kan du använda både [Plugin-programmet Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) och plugin-programmet [Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/). Om Docker-bilden implementeras med andra programmeringsspråk eller testkörare bör du kontrollera dokumentationen för de valda verktygen för att se hur du genererar JUnit XML-rapporter.

### Överför filer (#upload-files)

Testerna ibland måste överföra filer till det program som testas. För att behålla distributionen av Selenium i förhållande till dina tester är det inte möjligt att överföra en resurs direkt till Selenium. I stället överförs en fil genom några steg:

1. Överför filen på den URL som anges av miljövariabeln `UPLOAD_URL`. Överföringen måste utföras i en POST med ett multipart-formulär. Multipart-formuläret måste ha ett enda filfält. Detta motsvarar `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Läs dokumentationen och biblioteken för programmeringsspråket som används i Docker-bilden för att få reda på hur en sådan HTTP-begäran ska utföras.
2. Om överföringen lyckas returnerar begäran ett `200 OK`-svar av typen `text/plain`. Svarets innehåll är ett ogenomskinligt filhandtag. Du kan använda det här handtaget i stället för en filsökväg i ett `<input>`-element för att testa filöverföringar i programmet.
