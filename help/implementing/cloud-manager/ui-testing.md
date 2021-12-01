---
title: UI-testning - Cloud Services
description: UI-testning - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 778fa187df675eada645c73911e6f02e8a112753
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# UI-testning {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI-testning"
>abstract="Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium). Docker-bilden kan skapas med standardverktyg, men måste följa vissa regler när den körs. När du kör Docker-bilden etableras en Selenium-server automatiskt. Med de runtime-konventioner som beskrivs nedan kan din testkod få åtkomst till både Selenium-servern och AEM instanser som testas."

Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium). Docker-bilden kan skapas med standardverktyg, men måste följa vissa regler när den körs. När du kör Docker-bilden etableras en Selenium-server automatiskt. Med de runtime-konventioner som beskrivs nedan kan din testkod få åtkomst till både Selenium-servern och AEM instanser som testas.

>[!NOTE]
> Scen- och produktionsrörledningar som skapats före den 10 februari 2021 måste uppdateras för att de UI-tester som beskrivs på den här sidan ska kunna användas.
> Se [CI-CD-pipeline i Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) för information om pipeline-konfiguration.

## Testning av anpassat användargränssnitt {#custom-ui-testing}

AEM förser sina kunder med en integrerad uppsättning kvalitetsportar för Cloud Manager för att säkerställa smidiga uppdateringar av deras program. I synnerhet tillåter IT-testportar redan kunderna att skapa och automatisera sina egna tester som använder AEM API:er.

Testfunktionen för anpassat användargränssnitt är en [valfri funktion](#customer-opt-in) som gör det möjligt för våra kunder att skapa och automatiskt köra gränssnittstester för sina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium). Du kan läsa mer om hur du skapar gränssnittstester och skriver gränssnittstester härifrån. Dessutom kan ett UI-testprojekt enkelt genereras med den AEM projekttypen.

Kunderna kan skapa (via GIT) anpassade tester och testsvit för användargränssnittet. Gränssnittstestet kommer att utföras som en del av en särskild kvalitetsport för varje Cloud Manager-pipeline med deras specifika steg och feedbackinformation. Alla gränssnittstester, inklusive regression och nya funktioner, gör att fel kan upptäckas och rapporteras i kundsammanhang.

Kundens gränssnittstester körs automatiskt på produktionsflödet under steget&quot;Anpassad gränssnittstestning&quot;.

Till skillnad från Custom Functional Testing, som är HTTP-tester skrivna i java, kan UI-testerna vara en dockningsbild med tester skrivna på vilket språk som helst, förutsatt att de följer konventionerna som definieras i [Skapar gränssnittstester](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>Vi rekommenderar att du följer strukturen och språket *(js and wdio)* finns i [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) som startpunkt.

### Kundens deltagande {#customer-opt-in}

För att få sina gränssnittstester skapade och körda måste kunderna&quot;anmäla sig&quot; genom att lägga till en fil i sin koddatabas, under huvudundermodulen för UI-tester (bredvid filen pom.xml i undermodulen för användargränssnittstester) och se till att den här filen finns i roten för de inbyggda `tar.gz` -fil.

*Filnamn*: `testing.properties`

*Innehåll*: `ui-tests.version=1`

Om detta inte finns i `tar.gz` fil, UI-testerna byggs och körningar hoppas över

Lägg till `testing.properties` i den inbyggda artefakten lägger du till en `include` programsats in `assembly-ui-test-docker-context.xml` -fil (i undermodulen UI-tester):

    &quot;
    [...]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- testmodul för deltagande i Cloud Manager —>
    &lt;/includes>
    [...]
    &quot;

>[!NOTE]
>Produktionspipelinor som skapats före den 10 februari 2021 måste uppdateras för att de UI-tester som beskrivs i detta avsnitt ska kunna användas. Detta innebär att användaren måste redigera produktionsflödet och klicka på **Spara** från användargränssnittet även om inga ändringar gjorts.
>Se [Konfigurera CI-CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) om du vill veta mer om pipelinekonfigurationen.

## Skapar gränssnittstester {#building-ui-tests}

UI-tester är byggda utifrån Docker-byggkontext som genereras av ett Maven-projekt. Cloud Manager använder Docker-byggkontexten för att generera en Docker-bild som innehåller de faktiska gränssnittstesterna. Sammanfattningsvis genererar ett Maven-projekt en Docker-byggkontext och Docker-byggkontexten beskriver hur du skapar en Docker-bild som innehåller UI-testerna.

I det här avsnittet beskrivs stegen som krävs för att lägga till ett UI-testprojekt i din databas. Om du har bråttom eller inte har några särskilda krav för programmeringsspråket [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) kan generera ett UI-testprojekt åt dig.

### Generera kontext för Docker-bygge {#generate-docker-build-context}

För att skapa en Docker-byggkontext behöver du en Maven-modul som:

- Skapar ett arkiv som innehåller en `Dockerfile` och alla andra filer som behövs för att bygga Docker-bilden med testerna.
- Taggar arkivet med `ui-test-docker-context` klassificerare.

Det enklaste sättet att uppnå detta är att konfigurera [Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/) för att skapa kontextarkivet för Docker-bygget och tilldela rätt klassificerare till det.

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

Den här exekveringen instruerar Maven Assembly Plugin att skapa ett arkiv baserat på instruktionerna i `assembly-ui-test-docker-context.xml`, anropade en sammansättningsbeskrivning i plugin-programmets jargon. Sammansättningsbeskrivningen visar alla filer som måste ingå i arkivet.

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

Sammansättningsbeskrivningen instruerar plugin-programmet att skapa ett arkiv av typen `.tar.gz` och tilldelar `ui-test-docker-context` klassificerare. Dessutom listas de filer som måste ingå i arkivet:

- A `Dockerfile`, obligatoriskt för att bygga Docker-bilden.
- The `wait-for-grid.sh` skript, vars syften beskrivs nedan.
- De faktiska gränssnittstesterna, som implementeras av ett Node.js-projekt i `test-module` mapp.

Sammansättningsbeskrivningen utesluter också vissa filer som kan genereras när gränssnittstesterna körs lokalt. Detta garanterar ett mindre arkiv och snabbare byggen.

Arkivet som innehåller Docker-byggkontexten hämtas automatiskt av Cloud Manager, som skapar Docker-bilden som innehåller testerna under driftsättningsfasen. Till slut körs Docker-avbildningen i Cloud Manager för att köra gränssnittstester mot ditt program.

Bygget ska antingen producera noll eller ett arkiv. Om det skapar ett nollarkiv godkänns teststeget som standard. Om bygget skapar mer än ett arkiv är det valda arkivet inte deterministiskt.

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

1. Läs URL:en för Selenium-tjänsten på `SELENIUM_BASE_URL` miljövariabel.
2. Avsökning med regelbundna intervall till [statusslutpunkt](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) exponeras av Selenium API.

När Seleniums statusendpoint svarar med ett positivt svar kan testerna slutligen börja.

### Generera testrapporter {#generate-test-reports}

Docker-bilden måste generera testrapporter i JUnit XML-format och spara dem i den sökväg som anges av systemvariabeln `REPORTS_PATH`. JUnit XML-formatet är ett utbrett format för rapportering av testresultat. Om Docker-bilden använder Java och Maven är båda [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) och [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/). Om Docker-bilden implementeras med andra programmeringsspråk eller testkörare bör du kontrollera dokumentationen för de valda verktygen för att se hur du genererar JUnit XML-rapporter.

### Överför filer {#upload-files}

Testerna ibland måste överföra filer till det program som testas. För att behålla distributionen av Selenium i förhållande till dina tester är det inte möjligt att överföra en resurs direkt till Selenium. I stället överförs en fil genom några steg:

1. Överför filen på den URL som anges av `UPLOAD_URL` miljövariabel. Överföringen måste utföras i en POST med ett multipart-formulär. Multipart-formuläret måste ha ett enda filfält. Detta motsvarar `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Läs dokumentationen och biblioteken för programmeringsspråket som används i Docker-bilden för att få reda på hur en sådan HTTP-begäran ska utföras.
2. Om överföringen lyckas returnerar begäran en `200 OK` typsvar `text/plain`. Svarets innehåll är ett ogenomskinligt filhandtag. Du kan använda det här handtaget i stället för en filsökväg i en `<input>` -element för att testa filöverföringar i programmet.
