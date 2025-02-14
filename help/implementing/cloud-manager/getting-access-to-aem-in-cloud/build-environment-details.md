---
title: Build Environment of Cloud Manager
description: Läs om Cloud Manager byggmiljö och hur den bygger och testar din kod.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e5404de6baae5373aefe5d03894864965b47b049
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---


# Byggmiljö {#build-environment}

Läs om Cloud Manager byggmiljö och hur den bygger och testar din kod.

>[!TIP]
>
>Det här dokumentet innehåller Cloud Manager byggmiljö för utveckling av ditt AEM as a Cloud Service-projekt. Mer information om klientplattformar som stöds av AEM as a Cloud Service för innehållsutveckling finns i dokumentet [Klientplattformar som stöds.](/help/overview/supported-platforms.md)

## Information om byggmiljö {#build-environment-details}

Cloud Manager bygger och testar koden i en specialiserad byggmiljö.

* Byggmiljön är Linux-baserad och kommer från Ubuntu 2.04.
* Apache Maven 3.9.4 är installerad.
   * Adobe rekommenderar att användare [uppdaterar sina Maven-databaser så att de använder HTTPS i stället för HTTP](#https-maven).
<!-- OLD Removed 1/16/25 * The Java versions installed are Oracle JDK 11.0.22 and Oracle JDK 8u401. -->
* De Java-versioner som är installerade är Oracle JDK 11.0.22, Oracle JDK 17.0.10 och Oracle JDK 21.0.4.

<!-- OLD Removed 1/16/25 * **IMPORTANT:** By default, the JAVA_HOME environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. This default should be overridden for AEM Cloud Projects to use JDK 11. See the Setting the Maven JDK Version section for more details. -->
* **VIKTIGT!** Miljövariabeln `JAVA_HOME` är som standard inställd på `/usr/lib/jvm/jdk1.8.0_401` som innehåller Oracle JDK 8u401. ***Den här standardinställningen bör åsidosättas för AEM Cloud-projekt så att JDK 21 (standard), 17 eller 11*** används. Mer information finns i avsnittet [Ange JDK-version för Maven](#alternate-maven-jdk-version).
* Det finns ytterligare systempaket installerade som är nödvändiga.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Andra paket kan installeras vid byggtillfället enligt beskrivningen i avsnittet [Installera ytterligare systempaket](#installing-additional-system-packages).
* Varje bygge körs i en ren miljö där byggbehållaren inte har något läge mellan körningarna.
* Maven körs alltid med följande tre kommandon.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven har konfigurerats på systemnivå med en `settings.xml`-fil, som automatiskt inkluderar den offentliga Adobe-artefaktdatabasen med en profil med namnet `adobe-public`. (Mer information finns i [Adobe Public Maven Repository](https://repo1.maven.org/).)

>[!NOTE]
>
>Även om Cloud Manager inte definierar någon specifik version av `jacoco-maven-plugin` måste den version som används vara minst `0.7.5.201505241946`.

## HTTPS Maven-databaser {#https-maven}

Cloud Manager [release 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) påbörjade en rullande uppdatering av byggmiljön (som i version 2023.12.0) som innehöll en uppdatering till Maven 3.8.8. En betydande förändring som introducerades i Maven 3.8.1 var en säkerhetsförbättring som syftar till att minska potentiella sårbarheter. Maven inaktiverar nu alla osäkra `http://*`-speglar som standard, vilket beskrivs i [versionsinformationen för Maven](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Som ett resultat av den här säkerhetsförbättringen kan vissa användare råka ut för problem under byggfasen, särskilt när artefakter hämtas från Maven-databaser som använder osäkra HTTP-anslutningar.

För att få en smidig upplevelse med den uppdaterade versionen rekommenderar Adobe att användare uppdaterar sina Maven-databaser så att HTTPS används istället för HTTP. Denna justering är anpassad efter branschens växande övergång till säkra kommunikationsprotokoll och hjälper till att upprätthålla en säker och tillförlitlig byggprocess.

<!-- OLD below Removed 1/16/25

### Use a specific Java version

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 11. -->

<!-- OLD below Removed 1/16/25

#### Set the Maven JDK version

Adobe recommends that you set the JDK version for the entire Maven execution to `11` in a `.cloudmanager/java-version file`.

To do so, create a file named `.cloudmanager/java-version` in the git repository branch used by the pipeline. Edit the file so that it contains only the text, `11`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `11` is specified, Oracle 11 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-11.0.22`. -->

### Använd en specifik Java-version {#using-java-support}

Cloud Manager byggprocess använder Oracle 8 JDK för att skapa projekt som standard, men kunder som använder AEM Cloud Service bör ställa in JDK-versionen för Maven-exekvering på 21 (standard), 17 eller 11.

#### Ange version av Maven JDK {#alternate-maven-jdk-version}

Om du vill ställa in Maven-körnings-JDK skapar du en fil med namnet `.cloudmanager/java-version` i Git-databasgrenen som används av pipelinen. Redigera filen så att den bara innehåller texten, `21` eller `17`. Även om Cloud Manager accepterar värdet `8` stöds inte den här versionen längre för AEM Cloud-serviceprojekt. Alla andra värden ignoreras. När `21` eller `17` har angetts används Oracle Java 21 eller Oracle Java 17.


#### Krav för migrering till byggteknik med Java 21 eller Java 17 {#prereq-for-building}

Om du vill gå över till att bygga med Java 21 eller Java 17 måste du först uppgradera till den senaste SonarQube-versionen. Mer information finns i [versionsinformationen för Cloud Manager 2025.1.0](/help/implementing/cloud-manager/release-notes/current.md#what-is-new).

När du migrerar ditt program till en ny Java-version och runtime-version bör du noggrant testa i miljö med dev och stage innan du distribuerar till produktion.

Vi rekommenderar följande distributionsstrategi:

1. Kör ditt lokala SDK med Java 21, som du kan ladda ned från https://experience.adobe.com/#/downloads, distribuera programmet till det och validera dess funktioner. Kontrollera loggarna att det inte finns några fel som tyder på problem med klassinläsning eller byte-kodweaving.
1. Konfigurera en gren i din Cloud Manager-databas för att använda Java 21 som Java-version vid byggtid, konfigurera en DEV-pipeline för att använda den här grenen och köra pipelinen. Kör dina valideringstester.
1. Om det ser bra ut kan du konfigurera din stage/prod-pipeline så att den använder Java 21 som Java-version för byggtid och köra pipelinen.

##### Om vissa översättningsfunktioner {#translation-features}

Följande funktioner kanske inte fungerar som de ska när de körs i Java 21, och Adobe räknar med att kunna åtgärda dem i början av 2025:

* `XLIFF` (XML Localization Interchange File Format) misslyckas när mänsklig översättning används.
* `I18n` (Internationalisering) hanterar inte språk på korrekt sätt hebreiska (`he`), indonesiska (`in`) och jiddistiska (`yi`) på grund av ändringar i språkkonstruktorn i nyare Java-versioner.

#### Körningskrav {#runtime-requirements}

Java 21-miljön används för byggen med Java 21 och Java 17, och den kommer gradvis att tillämpas även på Java 11-byggen (se anmärkningen nedan). En miljö måste finnas i AEM version 17098 eller senare för att Java 21-uppdateringen ska kunna tas emot. För att säkerställa kompatibilitet krävs följande justeringar.

Biblioteksuppdateringar kan användas när som helst eftersom de är kompatibla med äldre Java-versioner.

* **Lägsta version av ASM:**
Uppdatera användningen av Java-paketet `org.objectweb.asm`, som ofta paketeras i `org.ow2.asm.*` artefakter, till version 9.5 eller senare för att säkerställa stöd för nyare JVM-miljöer.

* **Minimiversion av Groovy:**
Uppdatera användningen av Java-paketen `org.apache.groovy` eller `org.codehaus.groovy` till version 4.0.22 eller senare för att säkerställa stöd för nyare JVM-miljöer.

  Det här paketet kan inkluderas indirekt genom att du lägger till tredjepartsberoenden som AEM Groovy Console.

AEM Cloud-tjänsten SDK är kompatibel med Java 21 och kan användas för att validera kompatibiliteten mellan ditt projekt och Java 21 innan du kör en Cloud Manager-pipeline.

* **Redigera en körningsparameter:**
När AEM körs lokalt med Java 21 misslyckas startskripten (`crx-quickstart/bin/start` eller `crx-quickstart/bin/start.bat`) på grund av parametern `MaxPermSize` . Ta bort `-XX:MaxPermSize=256M` från skriptet eller definiera miljövariabeln `CQ_JVM_OPTS` genom att ange den som `-Xmx1024m -Djava.awt.headless=true`.

  Problemet har lösts i AEM Cloud Service SDK version 19149 och senare.

>[!IMPORTANT]
>
>När `.cloudmanager/java-version` är inställt på `21` eller `17` distribueras Java 21-miljön. Java 21-miljön är planerad att gradvis lanseras i alla miljöer (inte bara de miljöer vars kod byggts med Java 11) med början tisdagen den 4 februari 2025. Lanseringen börjar med sandlådor och utvecklingsmiljöer och börjar sedan i april 2025 på alla produktionsmiljöer. Kunder som vill använda Java 21-miljön *tidigare* kan kontakta Adobe på [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).


#### Krav för byggtid {#build-time-reqs}

Följande justeringar krävs för att projektet ska kunna byggas med Java 21 och Java 17. De kan uppdateras även innan du kör Java 21 och Java 17 eftersom de är kompatibla med äldre Java-versioner.

Kunder som har AEM Cloud-tjänster rekommenderas att skapa sina projekt med Java 21 så tidigt som möjligt för att utnyttja de nya språkfunktionerna.

* **Minimiversion av `bnd-maven-plugin`:**
Uppdatera användningen av `bnd-maven-plugin` till version 6.4.0 för att säkerställa stöd för nyare JVM-miljöer.

  Versioner 7 eller senare är inte kompatibla med Java 11 eller tidigare, så en uppgradering till den versionen rekommenderas inte.

* **Minimiversion av `aemanalyser-maven-plugin`:**
Uppdatera användningen av `aemanalyser-maven-plugin` till version 1.6.6 eller senare för att säkerställa stöd för nyare JVM-miljöer.

* **Minimiversion av `maven-bundle-plugin`:**
Uppdatera användningen av `maven-bundle-plugin` till version 5.1.5 eller senare för att säkerställa stöd för nyare JVM-miljöer.

  Versioner 6 eller senare är inte kompatibla med Java 11 eller tidigare, så en uppgradering till den versionen rekommenderas inte.

* **Uppdatera beroenden i `maven-scr-plugin`:**
`maven-scr-plugin` är inte direkt kompatibelt med Java 21 eller Java 17. Beskrivningsfiler kan dock genereras genom att ASM-beroendeversionen uppdateras i plugin-konfigurationen, vilket visas i följande exempel:

```XML
<project>
  ...
  <build>
    ...
    <plugins>
      ...
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-scr-plugin</artifactId>
        <version>1.26.4</version>
        <executions>
          <execution>
            <id>generate-scr-scrdescriptor</id>
            <goals>
              <goal>scr</goal>
            </goals>
          </execution>
        </executions>
        <dependencies>
          <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.7.1</version>
            <scope>compile</scope>
          </dependency>
        </dependencies>
      </plugin>
      ...
    </plugins>
    ...
  </build>
  ...
</project>
```

## Miljövariabler - standard {#environment-variables}

Du kan behöva ändra byggprocessen baserat på information om programmet eller pipeline.

Om JavaScript-miniatyrbilder till exempel inträffar vid byggtillfället med ett verktyg som Glup, kan olika miniatyrnivåer föredras för olika miljöer. En utvecklingsbygge kan använda en mindre miniminivå jämfört med staging och produktion.

Som stöd för detta lägger Cloud Manager till dessa standardmiljövariabler i byggbehållaren för varje körning.

| Variabelnamn | Definition |
|---|---|
| `CM_BUILD` | Alltid inställd på `true` |
| `BRANCH` | Den konfigurerade grenen för körningen |
| `CM_PIPELINE_ID` | Den numeriska pipeline-identifieraren |
| `CM_PIPELINE_NAME` | Pipeline-namnet |
| `CM_PROGRAM_ID` | Den numeriska programidentifieraren |
| `CM_PROGRAM_NAME` | Programnamnet |
| `ARTIFACTS_VERSION` | För ett stadium eller en produktionsprocess, den syntetiska version som genererats av Cloud Manager |
| `CM_AEM_PRODUCT_VERSION` | Versionsversionen |

## Miljövariabler - pipeline {#pipeline-variables}

Din byggprocess kan kräva specifika konfigurationsvariabler som inte ska lagras i Git-databasen. Dessutom kan du behöva justera de här variablerna mellan pipeline-körningar som använder samma gren.

Mer information finns även i [Konfigurera pipeline-variabler](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).

## Installera ytterligare systempaket {#installing-additional-system-packages}

Vissa byggen kräver ytterligare systempaket för att fungera helt. Ett bygge kan till exempel anropa ett Python- eller Ruby-skript och måste ha en lämplig språktolk installerad. Installationsprocessen kan hanteras genom att anropa [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) i `pom.xml` för att anropa APT. Den här exekveringen bör normalt omslutas av en Cloud Manager-specifik Maven-profil. Det här exemplet installerar Python.

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

Samma teknik kan användas för att installera språkspecifika paket, till exempel med `gem` för RubyGems eller `pip` för Python-paket.

>[!NOTE]
>
>Om du installerar ett systempaket på det här sättet installeras det inte i den körningsmiljö som används för att köra Adobe Experience Manager. Kontakta din Adobe-representant om du behöver ett systempaket som är installerat i AEM-miljön.

>[!TIP]
>
>Mer information om frontendens byggmiljö finns i [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
