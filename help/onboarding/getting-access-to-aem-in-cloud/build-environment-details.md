---
title: Information om byggmiljö
description: Information om byggmiljö - Cloud Services
translation-type: tm+mt
source-git-commit: 81f2d4f4f956edbf88135a703df0162afd92bc43
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Förstå byggmiljön {#understanding-build-environment}

## Information om byggmiljö {#build-environment-details}

Cloud Manager bygger och testar koden med en specialiserad byggmiljö. Den här miljön har följande attribut:

* Byggmiljön är Linux-baserad och kommer från Ubuntu 18.04.
* Apache Maven 3.6.0 är installerad.
* De installerade Java-versionerna är Oracle JDK 8u202 och 11.0.2.
* Det finns ytterligare systempaket installerade som är nödvändiga:

   * bzip2
   * uppzip
   * libpng
   * imagemagick
   * grafikSnabb

* Andra paket kan installeras vid byggtillfället enligt beskrivningen [nedan](#installing-additional-system-packages).
* Varje bygge görs i en riktig miljö. byggbehållaren behåller inte något läge mellan körningar.
* Maven körs alltid med följande tre kommandon:

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven är konfigurerad på systemnivå med filen settings.xml som automatiskt inkluderar databasen för Adobe **Artifact** . (Mer information finns i [Adobe Public Maven Repository](https://repo.adobe.com/) .)

>[!NOTE]
>Även om Cloud Manager inte definierar en specifik version av `jacoco-maven-plugin`filen måste den version som används vara minst `0.7.5.201505241946`.

### Använda Java 11-stöd {#using-java-support}

Cloud Manager har nu stöd för att bygga kundprojekt med både Java 8 och Java 11. Som standard byggs projekt med Java 8.

Kunder som vill använda Java 11 i sina projekt kan göra det med [Apache Maven Toolchains Plugin](https://maven.apache.org/plugins/maven-toolchains-plugin/).

Det gör du genom att lägga till en post som ser ut så här i filen pom.xml: `<plugin>`

```
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

>[!NOTE]
>Leverantörsvärden som stöds är `oracle` och `sun`.
>
>Versionsvärden som stöds är `1.8`, `1.11`och `11`.

## Miljövariabler {#environment-variables}

### Standardmiljövariabler {#standard-environ-variables}

I vissa fall tycker kunderna att det är nödvändigt att variera byggprocessen baserat på information om programmet eller pipeline.

Om JavaScript-miniatyrbilder för byggtid utförs, till exempel med hjälp av ett verktyg som Glup, kan det finnas en önskan om att använda en annan miniminivå när du skapar för en utvecklingsmiljö i stället för att bygga för scenen och produktionen.

Som stöd för detta lägger Cloud Manager till dessa standardmiljövariabler i byggbehållaren för varje körning.

| **Variabelnamn** | **Definition** |
|---|---|
| CM_BUILD | Alltid inställd på &quot;true&quot; |
| BRANSCHER | Den konfigurerade grenen för körningen |
| CM_PIPELINE_ID | Den numeriska pipeline-identifieraren |
| CM_PIPELINE_NAME | Pipeline-namnet |
| CM_PROGRAM_ID | Den numeriska programidentifieraren |
| CM_PROGRAM_NAME | Programnamnet |
| ARTIFACTS_VERSION | Den syntetiska versionen som genererats av Cloud Manager för en fas eller produktionsprocess |
| CM_AEM_PRODUCT_VERSION | Versionsnamnet |

### Rörledningsvariabler {#pipeline-variables}

I vissa fall kan en kunds byggprocess vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen eller som behöver variera mellan olika pipeline-körningar som använder samma gren.

Med Cloud Manager kan dessa variabler konfigureras via Cloud Manager API eller Cloud Manager CLI per pipeline. Variabler kan lagras som antingen ren text eller krypteras i vila. I båda fallen görs variabler tillgängliga i byggmiljön som en miljövariabel som sedan kan refereras inifrån `pom.xml` filen eller andra byggskript.

Om du vill ange en variabel med hjälp av CLI kör du ett kommando som:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

Aktuella variabler kan listas:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

Variabelnamn får endast innehålla alfanumeriska tecken och understreck (_). Namnen ska vara versaler. Det finns en gräns på 200 variabler per pipeline. Varje namn måste innehålla färre än 100 tecken och varje värde måste innehålla färre än 2 048 tecken.

När de används i en `Maven pom.xml` fil är det praktiskt att mappa dessa variabler till Maven-egenskaper med en syntax som liknar den här:

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

Vissa byggen kräver att ytterligare systempaket installeras för att fungera helt. Ett bygge kan till exempel anropa ett Python- eller ruby-skript och därför måste ha en lämplig språktolk installerad. Detta kan du göra genom att anropa [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) för att anropa APT. Den här exekveringen bör normalt omslutas av en molnhanterarspecifik Maven-profil. Så här installerar du python:

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

Samma teknik kan användas för att installera språkspecifika paket, dvs. med `gem` för RubyGems eller `pip` för Python-paket.

>[!NOTE]
>
>Om du installerar ett systempaket på det här sättet installeras det **inte** i den körningsmiljö som används för att köra Adobe Experience Manager. Om du behöver ett systempaket som är installerat i AEM ska du kontakta Adobe.