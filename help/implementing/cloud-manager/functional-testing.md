---
title: Funktionstestning - Cloud Services
description: Funktionstestning - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---


# Funktionstestning {#functional-testing}

Funktionstestning indelas i två typer:

* Funktionstestning av produkten
* Anpassad funktionstestning

## Funktionstestning av produkten {#product-functional-testing}

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) runt kärnfunktioner i AEM (till exempel redigering och replikering) som förhindrar att kundändringar i programkoden distribueras om kärnfunktionen bryts.

Funktionstester för produkter körs automatiskt när en kund distribuerar ny kod till Cloud Manager och kan inte hoppas över.

Se [Produktfunktionstester](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) för exempeltester.

## Anpassad funktionstestning {#custom-functional-testing}

Det anpassade funktionsteststeget i pipeline finns alltid och kan inte hoppas över.

Om JAR-test inte skapas av bygget godkänns testet som standard.

>[!NOTE]
>Använd knappen **Ladda ned logg** för att hämta en ZIP-fil med loggarna för det detaljerade formuläret för testkörning. Loggarna innehåller inte loggarna för den faktiska AEM körningsprocessen, som du kommer åt med de vanliga funktionerna för hämtning och spårningsloggar. Mer information finns i [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md).


### Skriver funktionstester {#writing-functional-tests}

Funktionstester som skrivs av kunden måste paketeras som en separat JAR-fil som skapas av samma Maven-bygge som de artefakter som ska distribueras till AEM. I allmänhet är detta en separat Maven-modul. Den resulterande JAR-filen måste innehålla alla nödvändiga beroenden och skapas vanligtvis med maven-assembly-plugin med hjälp av jar-with-berodencies-beskrivningen.

Dessutom måste JAR ha manifesthuvudet Cloud-Manager-TestType inställt på integrationstest. I framtiden förväntas ytterligare rubrikvärden stödjas. Ett exempel på konfigurationen för maven-assembly-plugin är:

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

I den här JAR-filen måste klassnamnen för de faktiska tester som ska köras sluta i IT.

En klass med namnet `com.myco.tests.aem.ExampleIT` skulle till exempel köras, men en klass med namnet `com.myco.tests.aem.ExampleTest` skulle inte göra det.

Testklasserna måste vara normala JUnit-tester. Testinfrastrukturen är utformad och konfigurerad för att vara kompatibel med de konventioner som används av testbiblioteket för aem-testing-clients. Utvecklare uppmuntras starkt att använda det här biblioteket och följa vedertagna standarder. Mer information finns i [Git Link](https://github.com/adobe/aem-testing-clients).

### Lokal testkörning {#local-test-execution}

Eftersom testklasserna är JUnit-tester kan de köras från vanliga Java-IDE:er som Eclipse, IntelliJ, NetBeans och så vidare.

När du kör dessa tester måste du dock ange ett antal systemegenskaper som förväntas av aem-testing-clients (och de underliggande Sling Testing Clients).

Systemegenskaperna är följande:

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

