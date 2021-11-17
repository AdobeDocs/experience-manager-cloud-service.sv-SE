---
title: Funktionstestning - Cloud Services
description: Funktionstestning - Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 2bb72c591d736dd1fe709abfacf77b02fa195e4c
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 2%

---

# Funktionstestning {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Funktionstestning"
>abstract="Funktionstestning indelas i tre typer: Funktionstestning av produkter, anpassad funktionstestning och anpassad gränssnittstestning"

Funktionstestning indelas i tre typer:


* Funktionstestning av produkten
* Anpassad funktionstestning
* Testning av anpassat användargränssnitt

## Funktionstestning av produkten {#product-functional-testing}

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) runt kärnfunktioner i AEM (till exempel redigering och replikering) som förhindrar att kundändringar i programkoden distribueras om kärnfunktionen bryts.

Funktionstester för produkter körs automatiskt när en kund distribuerar ny kod till Cloud Manager och kan inte hoppas över.

Se [Funktionstester för produkten](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) för stickprov.

## Anpassad funktionstestning {#custom-functional-testing}

Det anpassade funktionsteststeget i pipeline finns alltid och kan inte hoppas över.

Byggnaden bör producera antingen noll eller en test-JAR. Om inga JAR-testversioner skapas godkänns teststeget som standard. Om bygget skapar fler än en test-JAR är den JAR som är vald icke-deterministisk.

>[!NOTE]
>Använd knappen **Ladda ned logg** för att hämta en ZIP-fil med loggarna för det detaljerade formuläret för testkörning. Loggarna innehåller inte loggarna för den faktiska AEM körningsprocessen, som du kommer åt med de vanliga funktionerna för hämtning och spårningsloggar. Se [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) för mer information.

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

### Skriva funktionstester {#writing-functional-tests}

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

I den här JAR-filen måste klassnamnen för de faktiska tester som ska köras sluta med `IT`.

En klass med namnet `com.myco.tests.aem.it.ExampleIT` skulle köras, men en klass med namnet `com.myco.tests.aem.it.ExampleTest` skulle inte göra det.

Om du vill utesluta testkoden från disponeringskontrollen för kodskanningen måste testkoden dessutom finnas under ett paket med namnet `it` (filtret för uteslutning av täckning är `**/it/**/*.java`).

Testklasserna måste vara normala JUnit-tester. Testinfrastrukturen är utformad och konfigurerad för att vara kompatibel med de konventioner som används av testbiblioteket för aem-testing-clients. Utvecklare uppmuntras starkt att använda det här biblioteket och följa vedertagna standarder. Se [Git-länk](https://github.com/adobe/aem-testing-clients) för mer information.

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
