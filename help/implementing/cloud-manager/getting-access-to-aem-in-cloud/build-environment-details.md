---
title: Bygg miljö
description: Lär dig mer om Cloud Managers byggmiljö och hur den bygger och testar din kod.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 3bf8764500d2b0068b808a42ecfd1400f78b1d13
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 0%

---

# Bygg miljö {#build-environment}

Lär dig mer om Cloud Managers byggmiljö och hur den bygger och testar din kod.

## Information om byggmiljö {#build-environment-details}

Cloud Manager bygger och testar koden med en specialiserad byggmiljö.

* Byggmiljön är Linux-baserad och kommer från Ubuntu 18.04.
* Apache Maven 3.6.0 är installerad.
* De Java-versioner som är installerade är Oraclena JDK 8u202, Azul Zulu 8u292, Oracle JDK 11.0.2 och Azul Zulu 11.0.11.
* Som standard är `JAVA_HOME` Miljövariabeln är inställd på `/usr/lib/jvm/jdk1.8.0_202`  som innehåller Oraclet JDK 8u202. Se [Alternate Maven Execution JDK Version](#alternate-maven-jdk-version) för mer information.
* Det finns ytterligare systempaket installerade som är nödvändiga.

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* Andra paket kan installeras vid byggtillfället enligt beskrivningen i avsnittet [Installerar ytterligare systempaket.](#installing-additional-system-packages)
* Varje bygge görs i en riktig miljö. byggbehållaren behåller inte något läge mellan körningar.
* Maven körs alltid med följande tre kommandon.

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven konfigureras på systemnivå med en `settings.xml` -fil, som automatiskt inkluderar den offentliga Adobe-artefaktdatabasen med en profil med namnet `adobe-public`. (Se [Adobe Public Maven Repository](https://repo1.maven.org/) för mer information).

>[!NOTE]
>
>Även om Cloud Manager inte definierar en specifik version av `jacoco-maven-plugin`måste den använda versionen vara minst `0.7.5.201505241946`.

### Använda en specifik Java-version {#using-java-support}

Som standard byggs projekt av Cloud Managers byggprocess med Oracle 8 JDK. Kunder som vill använda en alternativ JDK har två alternativ.

* [Använd Maven Toolchains.](#maven-toolchains)
* [Välj en alternativ JDK-version för hela körningsprocessen för Maven.](#alternate-maven-jdk-version)

#### Maven Toolchains {#maven-toolchains}

The [Maven Toolchains Plugin](https://maven.apache.org/plugins/maven-toolchains-plugin/) gör det möjligt för projekt att välja en viss JDK (eller verktygskedja) som ska användas i samband med verktygsfältsmedvetna Maven-plugin-program. Detta görs i projektets `pom.xml` genom att ange en leverantör och ett versionsvärde.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

Detta gör att alla verktygskedjedåliga Maven-plugin-program använder Oraclet JDK, version 11.

När du använder den här metoden körs Maven fortfarande med JDK-standardinställningen (Oracle 8) och `JAVA_HOME`  miljövariabeln har inte ändrats. Kontroll eller genomförande av Java-versionen via plugin-program som Apache Maven Enforcer Plugin fungerar därför inte och sådana plugin-program får inte användas.

De aktuella kombinationerna av leverantör/version är:

| Leverantör | Version |
|---|---|
| `oracle` | `1.8` |
| `oracle` | `1.11` |
| `oracle` | `11` |
| `sun` | `1.8` |
| `sun` | `1.11` |
| `sun` | `11` |
| `azul` | `1.8` |
| `azul` | `1.11` |
| `azul` | `8` |

#### Alternate Maven Execution JDK Version {#alternate-maven-jdk-version}

Det går också att välja Azul 8 eller Azul 11 som JDK för hela Maven-exekveringen. Till skillnad från alternativen för verktygskedjor ändras det JDK som används för alla plugin-program, såvida inte konfigurationen för verktygskedjor också anges. I så fall tillämpas fortfarande konfigurationen för verktygskedjor för Maven-plugin-program som är medvetna om verktygskedjor. Resultatet blir att du kontrollerar och använder Java-versionen med [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) kommer att fungera.

Det gör du genom att skapa en fil med namnet `.cloudmanager/java-version` i Git-databasgrenen som används av pipeline. Den här filen kan ha antingen innehållet 11 eller 8. Alla andra värden ignoreras. Om 11 anges används Azul 11 och `JAVA_HOME` Miljövariabeln är inställd på `/usr/lib/jvm/jdk-11.0.11`. Om 8 anges används Azul 8 och `JAVA_HOME` Miljövariabeln är inställd på `/usr/lib/jvm/jdk-8.0.292`.

## Miljövariabler {#environment-variables}

### Standardmiljövariabler {#standard-environ-variables}

Du kan behöva ändra byggprocessen baserat på information om programmet eller pipeline.

Om JavaScript-miniatyrbilder vid bygge görs med ett verktyg som Glup, kan det finnas en önskan om att använda en annan miniminivå när du skapar för en utvecklingsmiljö i stället för att bygga för staging och produktion.

Som stöd för detta lägger Cloud Manager till dessa standardmiljövariabler i byggbehållaren för varje körning.

| Variabelnamn | Definition |
|---|---|
| `CM_BUILD` | Alltid inställt på `true` |
| `BRANCH` | Den konfigurerade grenen för körningen |
| `CM_PIPELINE_ID` | Den numeriska pipeline-identifieraren |
| `CM_PIPELINE_NAME` | Pipeline-namnet |
| `CM_PROGRAM_ID` | Den numeriska programidentifieraren |
| `CM_PROGRAM_NAME` | Programnamnet |
| `ARTIFACTS_VERSION` | Den syntetiska versionen som genererats av Cloud Manager för en fas eller produktionsprocess |
| `CM_AEM_PRODUCT_VERSION` | Versionsversionen |

### Rörledningsvariabler {#pipeline-variables}

Din byggprocess kan vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen, eller så måste du variera dem mellan pipeline-körningar som använder samma gren.

Med Cloud Manager kan dessa variabler konfigureras via Cloud Manager API eller Cloud Manager CLI per pipeline. Variabler kan lagras som antingen ren text eller krypteras i vila. I båda fallen görs variablerna tillgängliga i byggmiljön som en miljövariabel som sedan kan refereras inifrån `pom.xml` eller andra byggskript.

Det här CLI-kommandot anger en variabel.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Det här kommandot listar variabler.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Variabelnamn måste följa följande konventioner.

* Variabler får endast innehålla alfanumeriska tecken och understreck (`_`).
* Namnen ska vara versaler.
* Det finns en gräns på 200 variabler per pipeline.
* Varje namn får innehålla högst 100 tecken.
* Varje `string` variabelvärdet måste vara mindre än 2 048 tecken.
* Varje `secretString` variabelvärdet type måste vara mindre än 500 tecken.

Vid användning i en Maven `pom.xml` är det praktiskt att mappa dessa variabler till Maven-egenskaper med en syntax som liknar den här.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## Installera ytterligare systempaket {#installing-additional-system-packages}

Vissa byggen kräver att ytterligare systempaket installeras för att fungera helt. Ett bygge kan till exempel anropa ett Python- eller Ruby-skript och måste ha en lämplig språktolk installerad. Detta kan du göra genom att anropa [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) i `pom.xml` för att anropa APT. Den här exekveringen bör normalt omslutas av en molnhanterarspecifik Maven-profil. Det här exemplet installerar Python.

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

Samma teknik kan användas för att installera språkspecifika paket, t.ex. med `gem` för RubyGems eller `pip` för Python Packages.

>[!NOTE]
>
>Om du installerar ett systempaket på det här sättet installeras det inte i den körningsmiljö som används för att köra Adobe Experience Manager. Om du behöver ett systempaket som är installerat i AEM ska du kontakta Adobe.
