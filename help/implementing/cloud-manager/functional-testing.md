---
title: Funktionstestning
description: Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 15de47e28e804fd84434d5e8e5d2fe8fe6797241
workflow-type: tm+mt
source-wordcount: '632'
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

För alla funktionstester kan detaljerade testresultat hämtas som `.zip` genom att använda **Hämta bygglogg** på skärmen som utgör en del av [distributionsprocessen.](/help/implementing/cloud-manager/deploy-code.md) Loggarna innehåller inte loggarna för den faktiska AEM körningsprocessen. För att få tillgång till loggarna, se dokumentet [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) för mer information.

## Funktionstestning av produkten {#product-functional-testing}

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) av kärnfunktionalitet i AEM som redigerings- och replikeringsuppgifter. Dessa tester förhindrar att kundändringar i anpassad programkod distribueras om de bryter grundfunktionerna.

Funktionstester för produkter körs automatiskt när du distribuerar ny kod till Cloud Manager och kan inte hoppas över.

Se [funktionsprovningar av produkter](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) i GitHub för provtester.

## Anpassad funktionstestning {#custom-functional-testing}

Anpassat funktionstestningssteg i pipeline finns alltid och kan inte hoppas över.

Byggnaden bör producera antingen noll eller en test-JAR. Om inga JAR-testversioner skapas godkänns teststeget som standard. Om bygget skapar fler än en test-JAR är den JAR som är vald icke-deterministisk.

### Skriva funktionstester {#writing-functional-tests}

Anpassade funktionstester måste paketeras som en separat JAR-fil som skapas av samma Maven-bygge som de artefakter som ska distribueras till AEM. I allmänhet är detta en separat Maven-modul. Den resulterande JAR-filen måste innehålla alla nödvändiga beroenden och skulle vanligtvis skapas med `maven-assembly-plugin` med `jar-with-dependencies` beskrivning.

Dessutom måste JAR ha `Cloud-Manager-TestType` manifest header inställd på `integration-test`. I framtiden förväntas ytterligare rubrikvärden stödjas.

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

## Testning av anpassat användargränssnitt {#custom-ui-testing}

Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för att möjliggöra ett brett val av språk och ramverk (t.ex. Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium).

Se dokumentet [Testning av anpassat användargränssnitt](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) för mer information.

## Lokal testkörning {#local-test-execution}

Eftersom testklasser är JUnit-tester kan de köras från vanliga Java-IDE:er som Eclipse, IntelliJ, NetBeans och så vidare.

När du kör dessa tester måste du dock ange ett antal systemegenskaper som förväntas av `aem-testing-clients` (och det underliggande Sling Testing Clients) biblioteket.

Systemegenskaperna är följande.

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
