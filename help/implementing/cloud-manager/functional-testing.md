---
title: Funktionstestning
description: Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cd0b40ffa54eac0d7488b23329c4d2666c992da7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---


# Funktionstestning {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Funktionstestning"
>abstract="Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet."

Läs om de tre olika typerna av funktionstestning som ingår i [AEM as a Cloud Service distributionsprocess](/help/implementing/cloud-manager/deploy-code.md) för att säkerställa kvaliteten och tillförlitligheten i koden.

## Översikt {#overview}

Det finns tre olika typer av funktionstestning på AEM as a Cloud Service.

* [Funktionstestning av produkten](#product-functional-testing)
* [Anpassad funktionstestning](#custom-functional-testing)
* [Testning av anpassat användargränssnitt](#custom-ui-testing)

För alla funktionstester kan detaljerade testresultat hämtas som `.zip` genom att använda **Hämta bygglogg** på skärmen som utgör en del av [distributionsprocessen.](/help/implementing/cloud-manager/deploy-code.md)

Loggarna innehåller inte loggarna för den faktiska AEM körningsprocessen. För att få tillgång till loggarna, se dokumentet [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) för mer information.

Både produktfunktionstesterna och de anpassade funktionstesterna baseras på [AEM testar klienter.](https://github.com/adobe/aem-testing-clients)

### Funktionstestning av produkten {#product-functional-testing}

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) av kärnfunktionalitet i AEM som redigerings- och replikeringsuppgifter. Dessa tester underhålls av Adobe och är avsedda att förhindra att ändringar i anpassad programkod driftsätts om kärnfunktionen bryts.

* [Produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): Funktionstester för produkter körs automatiskt när du distribuerar ny kod till Cloud Manager och kan inte hoppas över.
* [Icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): Du kan välja att produktfunktionstester ska köras varje gång du utför en icke-produktionsprocess.

Funktionstester av produkter underhålls som ett öppen källkodsprojekt. Se [funktionsprovningar av produkter](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) i GitHub om du vill ha mer information.

### Anpassad funktionstestning {#custom-functional-testing}

Även om produktfunktionstestning definieras av Adobe kan du skriva egna kvalitetstester för ditt eget program. Detta kommer att utföras som anpassad funktionstestning som en del av [produktionsflöde](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) eller valfritt [rörledning för icke-produktion](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) för att säkerställa programmets kvalitet.

Anpassad funktionstestning utförs både för anpassade koddistributioner och push-uppgraderingar, vilket gör det särskilt viktigt att skriva bra funktionstester som förhindrar att AEM kan knäcka programkoden. Det anpassade funktionsteststeget finns alltid och kan inte hoppas över.

### Testning av anpassat användargränssnitt {#custom-ui-testing}

Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett urval av språk och ramverk som Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium.

Se dokumentet [Testning av anpassat användargränssnitt](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) för mer information.

## Komma igång med funktionstester {#getting-started-functional-tests}

När en ny koddatabas skapas i Cloud Manager kan `it.tests` mappen skapas automatiskt med exempelfall.

>[!NOTE]
>
>Om din databas skapades innan Cloud Manager skapades automatiskt `it.tests` kan du även generera den senaste versionen med [AEM Project Archetype.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

När du har fått innehållet i `it.tests` kan du använda den som bas för dina egna tester och sedan:

1. [Utveckla testfall.](#writing-functional-tests)
1. [Kör testerna lokalt.](#local-test-execution)
1. Implementera koden i molnhanterarens databas och kör en Cloud Manager-pipeline.

## Skriva anpassade funktionstester {#writing-functional-tests}

Samma verktyg som Adobe använder för att skriva produktfunktionstester kan användas för att skriva dina anpassade funktionstester. Använd [funktionsprovningar av produkter](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) i GitHub som ett exempel på hur du skriver dina tester.

Koden för det anpassade funktionstestet är Java-kod som finns i `it.tests` projektmapp. Den ska producera en enda JAR med alla funktionstester. Om bygget skapar mer än en test-JAR är den JAR som är vald icke-deterministisk. Om inga JAR-testversioner skapas godkänns teststeget som standard. [Se AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) för stickprov.

Testerna körs på testinfrastruktur som underhålls i Adobe, inklusive minst två författarinstanser, två publiceringsinstanser och en dispatcherkonfiguration. Det innebär att dina anpassade funktionstester körs mot hela AEM.

### Struktur för funktionstester {#functional-tests-structure}

Anpassade funktionstester måste paketeras som en separat JAR-fil som skapas av samma Maven-bygge som de artefakter som ska distribueras till AEM. I allmänhet är detta en separat Maven-modul. Den resulterande JAR-filen måste innehålla alla nödvändiga beroenden och skulle vanligtvis skapas med `maven-assembly-plugin` med `jar-with-dependencies` beskrivning.

Dessutom måste JAR ha `Cloud-Manager-TestType` manifest header inställd på `integration-test`.

Här följer ett exempel på konfiguration för `maven-assembly-plugin`.

```java
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
```

I den här JAR-filen måste klassnamnen för de faktiska tester som ska köras sluta med `IT`.

En klass med namnet `com.myco.tests.aem.it.ExampleIT` skulle köras, men en klass med namnet `com.myco.tests.aem.it.ExampleTest` skulle inte göra det.

Om du vill utesluta testkoden från disponeringskontrollen för kodskanningen måste testkoden dessutom finnas under ett paket med namnet `it` (filtret för uteslutning av täckning är `**/it/**/*.java`).

Testklasserna måste vara normala JUnit-tester. Testinfrastrukturen är utformad och konfigurerad så att den är kompatibel med konventionerna som används av `aem-testing-clients` testbibliotek. Utvecklare uppmuntras starkt att använda det här biblioteket och följa vedertagna standarder.

Se [`aem-testing-clients` GitHub-repo](https://github.com/adobe/aem-testing-clients) för mer information.

>[!TIP]
>
>[Se videon](https://www.youtube.com/watch?v=yJX6r3xRLHU) om hur du kan använda anpassade funktionstester för att förbättra ditt förtroende för CI/CD-pipelines.

### Lokal testkörning {#local-test-execution}

Innan du aktiverar funktionstester i en pipeline för Cloud Manager rekommenderar vi att du kör funktionstester lokalt med [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) eller en faktisk AEM as a Cloud Service instans.

#### Förutsättningar {#prerequisites}

Testerna i Cloud Manager körs med en teknisk administratörsanvändare.

Om du vill köra funktionstester från den lokala datorn skapar du en användare med administratörsliknande behörigheter för att uppnå samma beteende.

#### Köra i en IDE {#running-in-an-ide}

Eftersom testklasser är JUnit-tester kan de köras från vanliga Java-IDE:er som Eclipse, IntelliJ och NetBeans. Eftersom både produktfunktionstester och anpassade funktionstester baseras på samma teknik, kan båda köras lokalt genom att produkttesterna kopieras till dina anpassade tester.

När du kör dessa tester måste du dock ange ett antal systemegenskaper som förväntas av `aem-testing-clients` (och det underliggande Sling Testing Clients) biblioteket.

Systemegenskaperna är följande.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

#### Köra alla tester med Maven {#using-maven}

1. Öppna ett skal och navigera till `it.tests` i din databas.

1. Kör följande kommando med de parametrar som behövs för att starta testerna med Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
