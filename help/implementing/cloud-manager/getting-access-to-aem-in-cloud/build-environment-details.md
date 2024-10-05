---
title: Bygg miljö
description: Läs om Cloud Manager byggmiljö och hur den bygger och testar din kod.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---


# Bygg miljö {#build-environment}

Läs om Cloud Manager byggmiljö och hur den bygger och testar din kod.

## Information om byggmiljö {#build-environment-details}

Cloud Manager bygger och testar koden i en specialiserad byggmiljö.

* Byggmiljön är Linux-baserad och kommer från Ubuntu 2.04.
* Apache Maven 3.9.4 är installerad.
   * Adobe rekommenderar att användare [uppdaterar sina Maven-databaser så att HTTPS används i stället för HTTP](#https-maven).
* De Java-versioner som är installerade är Oracle JDK 11.0.22 och Oracle JDK 8u401.
* **VIKTIGT**: Som standard är miljövariabeln `JAVA_HOME` inställd på `/usr/lib/jvm/jdk1.8.0_401` som innehåller Oraclet JDK 8u401. *_Den här standardinställningen bör åsidosättas för AEM Cloud Projects som ska använda JDK 11_*. Mer information finns i avsnittet [Ange JDK-version för Maven](#alternate-maven-jdk-version).
* Det finns ytterligare systempaket installerade som är nödvändiga.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Andra paket kan installeras vid byggtillfället enligt beskrivningen i avsnittet [Installera ytterligare systempaket](#installing-additional-system-packages).
* Varje bygge görs i en absolut miljö. Byggbehållaren behåller inte något läge mellan körningarna.
* Maven körs alltid med följande tre kommandon.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven har konfigurerats på systemnivå med en `settings.xml`-fil, som automatiskt inkluderar den offentliga Adobe-artefaktdatabasen med en profil med namnet `adobe-public`. (Mer information finns i [Adobe Public Maven Repository](https://repo1.maven.org/).)

>[!NOTE]
>
>Även om Cloud Manager inte definierar någon specifik version av `jacoco-maven-plugin` måste den version som används vara minst `0.7.5.201505241946`.

## HTTPS Maven-databaser {#https-maven}

Cloud Manager [release 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) påbörjade en rullande uppdatering av byggmiljön (som i version 2023.12.0) som innehöll en uppdatering till Maven 3.8.8. En betydande förändring som introducerades i Maven 3.8.1 var en säkerhetsförbättring som syftar till att minska potentiella sårbarheter. Maven inaktiverar nu alla osäkra `http://*`-speglar som standard, vilket beskrivs i [versionsinformationen för Maven](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Som ett resultat av den här säkerhetsförbättringen kan vissa användare råka ut för problem under byggfasen, särskilt när artefakter hämtas från Maven-databaser som använder osäkra HTTP-anslutningar.

För att få en smidig upplevelse med den uppdaterade versionen rekommenderar Adobe att användare uppdaterar sina Maven-databaser till att använda HTTPS i stället för HTTP. Denna justering är anpassad efter branschens växande övergång till säkra kommunikationsprotokoll och hjälper till att upprätthålla en säker och tillförlitlig byggprocess.

### Använda en specifik Java-version {#using-java-support}

Som standard skapas projekt av Cloud Manager byggprocess med Oracle 8 JDK, men AEM Cloud Service-kunder rekommenderas att ställa in JDK-versionen som användes för att köra Maven på `11`.

#### Setting the Maven JDK Version {#alternate-maven-jdk-version}

Vi rekommenderar att du ställer in JDK-versionen för hela Maven-körningen till `11` i en `.cloudmanager/java-version`-fil.

Det gör du genom att skapa en fil med namnet `.cloudmanager/java-version` i Git-databasgrenen som används av pipeline. Redigera filen så att den bara innehåller texten, `11`. Även om Cloud Manager accepterar värdet `8` stöds inte den här versionen längre för AEM Cloud Service-projekt. Alla andra värden ignoreras. När `11` anges används Oracle 11 och miljövariabeln `JAVA_HOME` ställs in på `/usr/lib/jvm/jdk-11.0.22`.

## Miljövariabler {#environment-variables}

### Standardmiljövariabler {#standard-environ-variables}

Du kan behöva ändra byggprocessen baserat på information om programmet eller pipeline.

Om t.ex. JavaScript-miniatyrbilder under byggfasen utförs med ett verktyg som Glup, kan det finnas en önskan om att använda en annan miniminivå när du skapar för en utvecklingsmiljö i stället för att bygga för staging och produktion.

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

### Rörledningsvariabler {#pipeline-variables}

Din byggprocess kan vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen, eller så måste du variera dem mellan pipeline-körningar som använder samma gren.

Se även [Konfigurera pipeline-variabler](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) för mer information

## Installera ytterligare systempaket {#installing-additional-system-packages}

Vissa byggen kräver att ytterligare systempaket installeras för att fungera helt. Ett bygge kan till exempel anropa ett Python- eller Ruby-skript och måste ha en lämplig språktolk installerad. Detta kan du göra genom att anropa [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) i `pom.xml` för att anropa APT. Den här exekveringen bör normalt omslutas av en Cloud Manager-specifik Maven-profil. Det här exemplet installerar Python.

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
>Om du installerar ett systempaket på det här sättet installeras det inte i den körningsmiljö som används för att köra Adobe Experience Manager. Om du behöver ett systempaket som är installerat i AEM ska du kontakta Adobe.

>[!TIP]
>
>Mer information om frontendens byggmiljö finns i [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
