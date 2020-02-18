---
title: Förstå testresultaten - molntjänster
description: Förstå testresultat - molntjänster
translation-type: tm+mt
source-git-commit: c34137ba6f49785304ab21355eaad75798f26267

---


# Förstå testresultaten {#understand-test-results}

Körningar av pipeline för Cloud Manager för molntjänster stöder körning av tester som körs mot scenmiljön. Detta är i motsats till tester som körs under steget Build och Unit Testing, som körs offline, utan åtkomst till någon AEM-miljö som körs.
Det finns två typer av tester som körs i det här sammanhanget:
* Kundskrivna tester
* Adobe-skriftliga tester

Båda testtyperna körs i en innesluten infrastruktur som är utformad för att köra dessa typer av tester.


## Testning av kodkvalitet {#code-quality-testing}

Som en del av pipeline skannas källkoden för att säkerställa att distributionerna uppfyller vissa kvalitetskriterier. För närvarande implementeras detta genom en kombination av SonarQube och granskning på innehållspaketnivå med hjälp av OakPAL. Det finns över 100 regler som kombinerar allmänna Java-regler och AEM-specifika regler. I följande tabell sammanfattas klassificeringen för testkriterier:

| Namn | Definition | Kategori | Feltröskel |
|--- |--- |--- |--- |
| Säkerhetsklassificering | A = 0 Sårbarhet <br/>B = minst 1 Mindre sårbarhet<br/> C = minst 1 Större sårbarhet <br/>D = minst 1 Kritisk sårbarhet <br/>E = minst 1 Blockerare Sårbarhet |  Kritisk | &lt; B |
| Tillförlitlighetsklassificering | A = 0 Fel <br/>B = minst 1 mindre fel <br/>C = minst 1 större fel <br/>D = minst 1 allvarligt fel E = minst 1 blockeringsfel | Viktigt | &lt; C |
| Underhållbarhetsklassificering | Oöverträffade reparationskostnader för illaluktande kod är: <br/><ul><li>&lt;=5 % av tiden som redan har gått in i programmet är klassificeringen A </li><li>Betyg 6-10 % är B </li><li>Betyg mellan 11 och 20 % är ett C </li><li>Betyg mellan 21 och 50 % är ett D</li><li>över 50 % är ett E</li></ul> | Viktigt | &lt; A |
| Täckning | En blandning av radens disponering och villkorstäckning med denna formel: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>där CT = villkor som har utvärderats till &#39;true&#39; minst en gång under enhetstester <br/>CF = villkor som har utvärderats till &#39;false&#39; minst en gång under enhetstester <br/>LC = täckta linjer = lines_to_cover - uncover_lines <br/><br/> B = totalt antal villkor <br/>EL = totalt antal körbara rader (lines_to_cover) | Viktigt | &lt; 50% |
| Överhoppade enhetstester | Antal överhoppade enhetstester. | Information | > 1 |
| Öppna ärenden | Generella problemtyper - sårbarheter, fel och kodmellanslag | Information | > 1 |
| Duplicerade rader | Antal rader som ingår i duplicerade block. <br/>För att ett kodblock ska betraktas som duplicerat: <br/><ul><li>**Projekt som inte är Java:**</li><li>Det ska finnas minst 100 efterföljande och duplicerade tokens.</li><li>Dessa tokens bör spridas åtminstone på: </li><li>30 kodrader för COBOL </li><li>20 kodrader för ABAP </li><li>10 kodrader för andra språk</li><li>**Java-projekt:**</li><li> Det ska finnas minst 10 efterföljande och duplicerade satser oavsett antalet tokens och rader.</li></ul> <br/>Skillnader i indrag och i stränglitteraler ignoreras när dubbletter identifieras. | Information | > 1% |


>[!NOTE]
>
>Mer detaljerade definitioner finns i [Måttdefinitioner](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) .

Du kan hämta listan med regler här [code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-Rules-new-one.xlsx)

>[!NOTE]
>
>Mer information om de anpassade regler för kodkvalitet som körs av [!UICONTROL Cloud Manager]finns i [Anpassade regler](/help/implementing/cloud-manager/custom-code-quality-rules.md)för kodkvalitet.

### Hantera med falskt positiva {#dealing-with-false-positives}

Kvalitetsskanningsprocessen är inte perfekt och kan ibland felaktigt identifiera problem som inte är problematiska. Detta kallas &quot;falskt positivt&quot;.

I dessa fall kan källkoden kommenteras med Java- `@SuppressWarnings` standardanteckningen som anger regel-ID som anteckningsattribut. Ett vanligt problem är att regeln SonarQube för att identifiera hårdkodade lösenord kan vara aggressiv om hur ett hårdkodat lösenord identifieras.

Om du vill titta på ett specifikt exempel är koden ganska vanlig i ett AEM-projekt som har kod för att ansluta till en extern tjänst:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube kommer då att öka en blockerbarhets - sårbarhet. När du har granskat koden identifierar du att detta inte är en sårbarhet och kan kommentera detta med rätt regel-ID.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Om koden i själva verket var så här:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Den rätta lösningen är sedan att ta bort det hårdkodade lösenordet.

>[!NOTE]
>
>Även om det är en god vana att göra anteckningen så specifik som möjligt, dvs. bara anteckna den specifika programsats eller det block som orsakar problemet, är det möjligt att anteckna på klassnivå. `@SuppressWarnings`

## Skriva funktionstester {#writing-functional-tests}

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

En klass med namnet `com.myco.tests.aem.ExampleIT` skulle till exempel köras, men inte en klass med namnet `com.myco.tests.aem.ExampleTest` .

Testklasserna måste vara normala JUnit-tester. Testinfrastrukturen är utformad och konfigurerad för att vara kompatibel med de konventioner som används av testbiblioteket för aem-testing-clients. Utvecklare uppmuntras starkt att använda det här biblioteket och följa vedertagna standarder. Mer information finns i [Git-länken](https://github.com/adobe/aem-testing-clients) .

## Anpassad funktionstestning {#custom-functional-test}

Det anpassade funktionsteststeget i pipeline finns alltid och kan inte hoppas över.

Om JAR-test inte skapas av bygget godkänns testet som standard. Det här steget utförs nu direkt efter scendistributionen.

> Obs!
>Knappen **Hämtningslogg** ger åtkomst till en ZIP-fil som innehåller loggarna för det detaljerade formuläret för testkörning. Loggarna innehåller inte loggarna för den faktiska AEM-körningsprocessen, som du kommer åt med de vanliga funktionerna för hämtning och spårningsloggar. Mer information finns i [Åtkomst och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) .

## Lokal testkörning {#local-test-execution}

Eftersom testklasserna är JUnit-tester kan de köras från vanliga Java-IDE:er som Eclipse, IntelliJ, NetBeans och så vidare.

När du kör dessa tester med nödvändighet måste du dock ange ett antal systemegenskaper som förväntas av aem-testing-clients (och de underliggande Sling Testing Clients).

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