---
title: Java&handel; funktionstester
description: Lär dig skriva Java&handel; funktionstester för AEM as a Cloud Service
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Java™ Functional Testing

Lär dig skriva Java™-funktionstester för AEM as a Cloud Service

## Komma igång med funktionstester {#getting-started-functional-tests}

När en ny koddatabas skapas i Cloud Manager skapas en `it.tests`-mapp automatiskt med exempeltestfall.

>[!NOTE]
>
>Om din databas skapades innan Cloud Manager automatiskt skapade `it.tests`-mappar kan du även generera den senaste versionen med [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests).

När du har innehållet i mappen `it.tests` kan du använda den som grund för dina egna tester och sedan:

1. [Utveckla dina testfall](#writing-functional-tests).
1. [Kör testerna lokalt](#local-test-execution).
1. Implementera koden i Cloud Manager-databasen och kör en Cloud Manager-pipeline.

## Skriva anpassade funktionstester {#writing-functional-tests}

Samma verktyg som Adobe använder för att skriva produktfunktionstester kan användas för att skriva dina anpassade funktionstester. Använd [produktfunktionstesterna](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) i GitHub som exempel på hur du skriver dina tester.

Koden för det anpassade funktionstestet är Java™-kod i mappen `it.tests` i ditt projekt. Den ska producera en enda JAR med alla funktionstester. Om bygget skapar mer än en test-JAR är den JAR som är vald icke-deterministisk. Om inga JAR-testversioner skapas godkänns teststeget som standard. [Se AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) för exempel på tester.

Testerna körs på testinfrastruktur som underhålls av Adobe, inklusive minst två författarinstanser, två publiceringsinstanser och en Dispatcher-konfiguration. Detta innebär att dina anpassade funktionstester körs mot hela AEM.

### Struktur för funktionstester {#functional-tests-structure}

Anpassade funktionstester måste paketeras som en separat JAR-fil som skapas av samma Maven-bygge som de artefakter som ska distribueras till AEM. I allmänhet är detta bygge en separat Maven-modul. Den resulterande JAR-filen måste innehålla alla nödvändiga beroenden och skulle vanligtvis skapas med `maven-assembly-plugin` med hjälp av `jar-with-dependencies`-beskrivningen.

Dessutom måste JAR ha `Cloud-Manager-TestType`-manifesthuvudet inställt på `integration-test`.

Följande är ett exempel på konfiguration för `maven-assembly-plugin`.

```XML
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
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
    </plugins>
</build>
```

I den här JAR-filen måste klassnamnen för de faktiska test som ska köras sluta med `IT`.

En klass med namnet `com.myco.tests.aem.it.ExampleIT` skulle till exempel köras, men inte en klass med namnet `com.myco.tests.aem.it.ExampleTest`.

Om du vill utesluta testkod från disponeringskontrollen för kodskanningen måste testkoden dessutom finnas under ett paket med namnet `it` (disponeringsfiltret är `**/it/**/*.java`).

Testklasserna ska vara normala JUnit-tester. Testinfrastrukturen är utformad och konfigurerad för att vara kompatibel med konventionerna som används av testbiblioteket `aem-testing-clients`. Utvecklare uppmuntras att använda det här biblioteket och följa sina bästa rutiner.

Mer information finns i [`aem-testing-clients` GitHub-repo](https://github.com/adobe/aem-testing-clients).

>[!TIP]
>
>[Titta på den här videon](https://www.youtube.com/watch?v=yJX6r3xRLHU) om hur du kan använda anpassade funktionstester för att förbättra ditt förtroende för CI/CD-pipelines.

### Förutsättningar {#prerequisites}

1. Testerna i Cloud Manager körs med en teknisk administratörsanvändare.

>[!NOTE]
>
>Om du vill köra funktionstester från den lokala datorn skapar du en användare med administratörsliknande behörigheter för att uppnå samma beteende.

1. Den inneslutna infrastruktur som omfattar funktionstestning begränsas av följande gränser:


| Typ | Värde | Beskrivning |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0,5 | Den processortid som reserverats per testkörning |
| Minne | 0,5 Gi | Mängd minne som tilldelats testet, värde i gibibyte |
| Timeout | 30 m | Den varaktighet efter vilken testet avslutas. |
| Rekommenderad varaktighet | 15 m | Adobe rekommenderar att testet inte tar längre tid än så här. |

>[!NOTE]
>
> Om du behöver mer resurser kan du skapa ett kundvårdsärende och beskriva ditt användningsfall. Adobe teamet granskar din begäran och ger lämplig hjälp.

#### Beroenden

* aem-cloud-testing-clients:

Kommande ändringar i den inneslutna infrastruktur som används för att utföra funktionstester kräver att biblioteket [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) som används i ditt anpassade funktionstest uppdateras till minst version **1.2.1**
Kontrollera att beroendet i `it.tests/pom.xml` har uppdaterats.

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>Denna ändring måste utföras före 6 april 2024.
>Om du inte uppdaterar beroendebiblioteket kommer det att uppstå ett pipeline-fel i steget&quot;Custom Functional Testing&quot;.

### Lokal testkörning {#local-test-execution}

Innan du aktiverar funktionstester i en Cloud Manager-pipeline bör du köra funktionstester lokalt med [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) eller en faktisk AEM as a Cloud Service-instans.

#### Köra i en IDE {#running-in-an-ide}

Eftersom testklasser är JUnit-tester kan de köras från vanliga Java™-utvecklingsmiljöer som Eclipse, IntelliJ och NetBeans. Eftersom både produktfunktionstester och anpassade funktionstester baseras på samma teknik, kan båda köras lokalt genom att produkttesterna kopieras till dina anpassade tester.

När du kör dessa tester måste du dock ange olika systemegenskaper som förväntas av biblioteket `aem-testing-clients` (och det underliggande Sling Testing Clients).

Systemegenskaperna är följande.

| Egenskap | Beskrivning | Exempel |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | antal instanser, för att matcha molntjänsten ska anges till `2` | `2` |
| `sling.it.instance.url.1` | ska anges till författarens URL | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | den första instansens körningsläge ska anges till `author` | `author` |
| `sling.it.instance.adminUser.1` | ska anges till författaradministratörsanvändaren. | `admin` |
| `sling.it.instance.adminPassword.1` | ska anges som författarens administratörslösenord. |                         |
| `sling.it.instance.url.2` | ska anges till publicerings-URL:en | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | körningsläge för den andra instansen, ska anges till `publish` | `publish` |
| `sling.it.instance.adminUser.2` | ska ställas in för publiceringsadministratörsanvändaren. | `admin` |
| `sling.it.instance.adminPassword.2` | ska anges till administratörslösenordet för publicering. |                         |



#### Köra alla tester med Maven {#using-maven}

1. Öppna ett skal och navigera till mappen `it.tests` i din databas.

1. Kör följande kommando med de parametrar som krävs för att starta testerna med Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```

