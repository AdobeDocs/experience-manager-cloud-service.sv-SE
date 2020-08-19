---
title: Förstå testresultaten - Cloud Services
description: Förstå testresultat - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 3%

---


# Förstå testresultat {#understand-test-results}

Körningar av pipeline för Cloud Manager för Cloud Services stöder körning av tester som körs mot mellanlagringsmiljön. Detta är i motsats till tester som körs under steget Skapa och Enhetstestning som körs offline, utan åtkomst till någon AEM miljö som körs.

Det finns tre olika testkategorier som stöds av Cloud Manager för Cloud Services i pipeline:

1. [Testning av kodkvalitet](#code-quality-testing)
1. [Funktionstestning](#functional-testing)
1. [Testning av innehållsgranskning](#content-audit-testing)

Dessa tester kan vara:

* Kundskriven
* Adobe-skriven
* Verktyg med öppen källkod (från Google)

   >[!NOTE]
   > Både kundskrivna tester och Adobe-skrivna tester körs i en containerinfrastruktur som är utformad för att köra dessa typer av tester.


## Testning av kodkvalitet {#code-quality-testing}

I det här steget utvärderas kvaliteten på programkoden. Det är huvudmålet för en rörledning med enbart kodkvalitet och genomförs omedelbart efter byggsteget i alla rörledningar för icke-produktion och produktion.

Mer information om olika typer av pipelines finns i [Konfigurera CI-CD-pipeline](/help/implementing/cloud-manager/configure-pipeline.md) .

### Förstå regler för anpassad kodkvalitet {#understanding-code-quality-rules}

I Kodkvalitetstestning skannas källkoden så att den uppfyller vissa kvalitetskriterier. För närvarande implementeras detta genom en kombination av SonarQube och granskning på innehållspaketnivå med hjälp av OakPAL. Det finns över 100 regler som kombinerar allmänna Java-regler och AEM-specifika regler. Vissa av de AEM specifika reglerna skapas baserat på bästa praxis från AEM och kallas [anpassade regler](/help/implementing/cloud-manager/custom-code-quality-rules.md)för kodkvalitet.

Du kan hämta listan med regler [här](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx).

Resultatet av det här steget visas som *klassificering*. I följande tabell sammanfattas klassificeringen för testkriterier:

| Namn | Definition | Kategori | Feltröskel |
|--- |--- |--- |--- |
| Säkerhetsklassificering | A = 0 Sårbarhet <br/>B = minst 1 Mindre sårbarhet<br/> C = minst 1 Större sårbarhet <br/>D = minst 1 Kritisk sårbarhet <br/>E = minst 1 Blockerare Sårbarhet | Kritisk | &lt; B |
| Tillförlitlighetsklassificering | A = 0 Fel <br/>B = minst 1 mindre fel <br/>C = minst 1 större fel <br/>D = minst 1 allvarligt fel E = minst 1 blockeringsfel | Viktigt | &lt; C |
| Underhållbarhetsklassificering | Oöverträffade reparationskostnader för illaluktande kod är: <br/><ul><li>&lt;=5 % av tiden som redan har gått in i programmet är klassificeringen A </li><li>Betyg 6-10 % är B </li><li>Betyg mellan 11 och 20 % är ett C </li><li>Betyg mellan 21 och 50 % är ett D</li><li>över 50 % är ett E</li></ul> | Viktigt | &lt; A |
| Täckning | En blandning av radens disponering och villkorstäckning med denna formel: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>där: CT = villkor som har utvärderats till &#39;true&#39; minst en gång under enhetstester <br/>CF = villkor som har utvärderats till &#39;false&#39; minst en gång under enhetstester <br/>LC = täckta linjer = lines_to_cover - uncover_lines <br/><br/> B = totalt antal villkor <br/>EL = totalt antal körbara rader (lines_to_cover) | Viktigt | &lt; 50% |
| Överhoppade enhetstester | Antal överhoppade enhetstester. | Information | > 1 |
| Öppna ärenden | Generella problemtyper - sårbarheter, fel och kodmellanslag | Information | > 0 |
| Duplicerade rader | Antal rader som ingår i duplicerade block. <br/>För att ett kodblock ska betraktas som duplicerat: <br/><ul><li>**Projekt som inte är Java:**</li><li>Det ska finnas minst 100 efterföljande och duplicerade tokens.</li><li>Dessa tokens bör spridas åtminstone på: </li><li>30 kodrader för COBOL </li><li>20 kodrader för ABAP </li><li>10 kodrader för andra språk</li><li>**Java-projekt:**</li><li> Det ska finnas minst 10 efterföljande och duplicerade satser oavsett antalet tokens och rader.</li></ul> <br/>Skillnader i indrag och i stränglitteraler ignoreras när dubbletter identifieras. | Information | > 1% |
| Cloud Service-kompatibilitet | Antal identifierade kompatibilitetsproblem för Cloud Service. | Information | > 0 |

>[!NOTE]
>
>Mer detaljerade definitioner finns i [Måttdefinitioner](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) .


>[!NOTE]
>
>Mer information om de anpassade regler för kodkvalitet som körs av [!UICONTROL Cloud Manager]finns i [Anpassade regler](/help/implementing/cloud-manager/custom-code-quality-rules.md)för kodkvalitet.

### Hantera med falskt positiva {#dealing-with-false-positives}

Kvalitetsskanningsprocessen är inte perfekt och kan ibland felaktigt identifiera problem som inte är problematiska. Detta kallas &quot;falskt positivt&quot;.

I dessa fall kan källkoden kommenteras med Java- `@SuppressWarnings` standardanteckningen som anger regel-ID som anteckningsattribut. Ett vanligt problem är att regeln SonarQube för att identifiera hårdkodade lösenord kan vara aggressiv om hur ett hårdkodat lösenord identifieras.

Om du vill titta på ett specifikt exempel är koden ganska vanlig i ett AEM projekt som har kod att ansluta till en extern tjänst:

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

>[!NOTE]
>Även om det inte finns något explicit steg för säkerhetstestning finns det fortfarande säkerhetsrelaterade regler för kodkvalitet som utvärderas under steget för kodkvalitet. Se [säkerhetsöversikt för AEM som Cloud Service](/help/security/cloud-service-security-overview.md) om du vill veta mer om Cloud Service.

## Funktionstestning {#functional-testing}

Funktionstestning indelas i två typer:

* Funktionstestning av produkten
* Anpassad funktionstestning

### Funktionstestning av produkten {#product-functional-testing}

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) runt kärnfunktioner i AEM (till exempel redigering och replikering) som förhindrar att kundändringar i programkoden distribueras om kärnfunktionen bryts.

Funktionstester för produkter körs automatiskt när en kund distribuerar ny kod till Cloud Manager och kan inte hoppas över.

Se [Produktfunktionstester](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) för exempeltester.

### Anpassad funktionstestning {#custom-functional-testing}

Det anpassade funktionsteststeget i pipeline finns alltid och kan inte hoppas över.

Om JAR-test inte skapas av bygget godkänns testet som standard.

>[!NOTE]
>Använd knappen **Ladda ned logg** för att hämta en ZIP-fil med loggarna för det detaljerade formuläret för testkörning. Loggarna innehåller inte loggarna för den faktiska AEM körningsprocessen, som du kommer åt med de vanliga funktionerna för hämtning och spårningsloggar. Mer information finns i [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) .


#### Skriva funktionstester {#writing-functional-tests}

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

#### Lokal testkörning {#local-test-execution}

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


## Testning av innehållsgranskning {#content-audit-testing}

Content Audit är en funktion som finns i Cloud Manager Sites Production pipelines som drivs av Lighthuse, ett verktyg med öppen källkod från Google. Den här funktionen är aktiverad i alla produktionspipelinjer för Cloud Manager.

Den validerar distributionsprocessen och säkerställer att ändringar som distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inkludera inte regressioner i dessa dimensioner.

Content Audit i Cloud Manager säkerställer att slutanvändarnas digitala upplevelse på webbplatsen kan underhållas enligt högsta standard. Resultaten är informativa och gör att användaren kan se poängen och ändringen mellan den aktuella och den tidigare poängen. Den här insikten är värdefull för att avgöra om det finns en regression som kommer att introduceras i den aktuella distributionen.

### Om granskningsresultat för innehåll {#understanding-content-audit-results}

Content Audit ger aggregerade och detaljerade testresultat på sidnivå via körningssidan för Production Pipeline.

* Mätvärden för aggregerad nivå mäter medelpoängen för de sidor som granskades.
* Enskilda sidnivåpoäng kan också göras via fördjupning.
* Det finns uppgifter om poängen för att se vilka resultat de enskilda testerna ger, tillsammans med vägledning om hur man åtgärdar eventuella problem som upptäcktes under innehållsgranskningen.
* En historik över testresultaten sparas i Cloud Manager så att kunderna kan se om de ändringar som införs i pipeline-körningen innehåller några regressioner från föregående körning.

#### Sammanställd bakgrundsmusik {#aggregate-scores}

Det finns ett aggregerat nivåpoäng för varje testtyp (prestanda, hjälpmedel, SEO, bästa praxis och PWA).

Poängen för sammanställd nivå tar medelpoängen för de sidor som ingår i körningen. Ändringen på aggregeringsnivå representerar medelpoängen för sidorna i den aktuella körningen jämfört med medelvärdet för poängen från föregående körning, även om den sidsamling som konfigurerats att inkluderas har ändrats mellan körningar.

Värdet för Change-måttet kan vara något av följande:

* **Positivt värde** - sidan/sidorna har förbättrats på det valda testet sedan den senaste produktionskanalen kördes

* **Negativt värde** - sidan/sidorna har gått om på det valda testet sedan den senaste körningen av produktionsflödet

* **Ingen ändring** - sidan/sidorna har fått samma resultat sedan den senaste produktionspipeline-körningen

* **Ej tillämpligt** - det fanns ingen tidigare poäng att jämföra med

   ![](assets/content-audit-test1.png)

#### Poäng på sidnivå {#page-level-scores}

Genom att gå in i något av testerna kan man se en mer detaljerad sidnivåbedömning. Användaren kommer att kunna se hur de enskilda sidorna sparades för det specifika testet tillsammans med ändringen från den föregående gången testet kördes.

Om du klickar på detaljerna för en enskild sida visas information om de element på sidan som har utvärderats och vägledning för att åtgärda problem om möjligheter till förbättring upptäcks. Detaljer om testerna och tillhörande vägledning tillhandahålls av Google Lighthuse.

![](assets/page-level-scores.png)

