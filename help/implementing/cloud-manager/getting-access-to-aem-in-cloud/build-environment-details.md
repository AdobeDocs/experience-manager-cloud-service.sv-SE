---
title: Build Environment of Cloud Manager
description: Läs om Cloud Manager byggmiljö och hur den bygger och testar din kod.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3bc9ec12de604818f6be1c0717566a5f16c6a7b9
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---


# Byggmiljö {#build-environment}

Läs om Cloud Manager byggmiljö och hur den bygger och testar din kod.

## Information om byggmiljö {#build-environment-details}

Cloud Manager bygger och testar koden i en specialiserad byggmiljö.

* Byggmiljön är Linux-baserad och kommer från Ubuntu 2.04.
* Apache Maven 3.9.4 är installerad.
   * Adobe rekommenderar att användare [uppdaterar sina Maven-databaser så att HTTPS används i stället för HTTP](#https-maven).
* <!-- OLD --> De Java-versioner som är installerade är Oracle JDK 11.0.22 och Oracle JDK 8u401.
<!-- NEW but needed to be removed 12/5/24 * The Java versions installed are Oracle JDK 11.0.22, Oracle JDK 17.0.10, and Oracle JDK 21.0.4. -->
<!-- OLD --> * **VIKTIGT!** Miljövariabeln JAVA_HOME är som standard inställd på `/usr/lib/jvm/jdk1.8.0_401` som innehåller Oraclet JDK 8u401. Den här standardinställningen bör åsidosättas för AEM Cloud Projects som ska använda JDK 11. Mer information finns i avsnittet Setting the Maven JDK Version (Ställ in JDK-versionen).
<!-- NEW but needed to be removed 12/5/24 * **IMPORTANT:** By default, the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. ***This default should be overridden for AEM Cloud Projects to use JDK 21 (preferred), 17, or 11***. See the [Setting the Maven JDK Version](#alternate-maven-jdk-version) section for more details. -->
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

För att få en smidig upplevelse med den uppdaterade versionen rekommenderar Adobe att användare uppdaterar sina Maven-databaser till att använda HTTPS i stället för HTTP. Denna justering är anpassad efter branschens växande övergång till säkra kommunikationsprotokoll och hjälper till att upprätthålla en säker och tillförlitlig byggprocess.

<!-- OLD below -->

### Använd en specifik Java-version

Cloud Manager byggprocess använder Oracle 8 JDK för att skapa projekt som standard, men AEM Cloud Service-kunder bör ange JDK-versionen för Maven execution som 11.

<!-- OLD below -->

#### Ange version av Maven JDK

Adobe rekommenderar att du ställer in JDK-versionen för hela Maven-körningen till `11` i en `.cloudmanager/java-version file`.

Det gör du genom att skapa en fil med namnet `.cloudmanager/java-version` i Git-databasgrenen som används av pipeline. Redigera filen så att den bara innehåller texten, `11`. Även om Cloud Manager accepterar värdet `8` stöds inte den här versionen längre för AEM Cloud Service-projekt. Alla andra värden ignoreras. När `11` anges används Oracle 11 och miljövariabeln `JAVA_HOME` ställs in på `/usr/lib/jvm/jdk-11.0.22`.

<!-- NEW but needed to be removed 12/5/24 ### Use a specific Java version {#using-java-support}

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 21 (preferred), 17, or 11.

#### Set the Maven JDK version {#alternate-maven-jdk-version}

Adobe recommends setting the Maven execution JDK version to `21` or `17` in a `.cloudmanager/java-version` file.

To do so, create a file named `.cloudmanager/java-version` in the Git repository branch used by the pipeline. Edit the file so that it contains only the text, `21` or `17`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `21` or `17` is specified, Oracle Java 21 or Oracle Java 17 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-21` or `/usr/lib/jvm/jdk-17`.

#### Prerequisites for migrating to building with Java 21 or Java 17 {#prereq-for-building}

>[!NOTE]
>
>*When migrating your application to a new Java build version and runtime version, thoroughly test in dev and stage environments before deploying to production.
>Of special note, the following features have not yet been formally validated with Java 21 runtime: [Forms](/help/forms/home.md), [Workflows](/help/sites-cloud/authoring/workflows/overview.md), [Inbox](/help/sites-cloud/authoring/inbox.md), and [Projects](/help/sites-cloud/authoring/projects/overview.md). If your application relies on these features, ensure comprehensive testing to verify functionality.*

##### About some translation features {#translation-features}

The following features might not function correctly when building with Java 21 or Java 17, and Adobe expects to resolve them by early 2025:

* `XLIFF` (XML Localization Interchange File Format) fails when using Human Translation.  
* `I18n` (Internationalization) does not properly handle language locales Hebrew (`he`), Indonesian (`in`), and Yiddish (`yi`) due to changes in the Locale constructor in newer Java versions.

#### Runtime requirements {#runtime-requirements}

The Java 21 runtime is used for builds on Java 21, Java 17, and Java 11 starting in February 2025. To ensure compatibility, the following adjustments are necessary. 

Library updates can be applied anytime, as they remain compatible with older Java versions.

* **Minimum version of `org.objectweb.asm`:**
Update the usage of `org.objectweb.asm` to version 9.5 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `org.apache.groovy`:**
Update the usage of `org.apache.groovy` to version 4.0.22 or higher to ensure support for newer JVM runtimes.

  This bundle can be indirectly included by adding third party dependencies such as the AEM Groovy Console.

* **Edit a runtime parameter:**
When running AEM locally with Java 21, the start scripts (`crx-quickstart/bin/start` or `crx-quickstart/bin/start.bat`) fail due to the `MaxPermSize` parameter. As a remedy, either remove `-XX:MaxPermSize=256M` from the script or define the environment variable `CQ_JVM_OPTS`, setting it to `-Xmx1024m -Djava.awt.headless=true`.

  Adobe plans to resolve this issue in a future release.

>[!NOTE]
>
>When `.cloudmanager/java-version` is set to `21` or `17`, the Java 21 runtime is deployed. In February or March 2025, the Java 21 runtime is planned for deployment to all customers, even if Java 11 is used to build your code. 

#### Build time requirements

The following adjustments are required to allow building the project with Java 21 and Java 17. They can be updated at any time as they are compatible with older versions of Java.

* **Minimum version of `bnd-maven-plugin`:**
Update the usage of `bnd-maven-plugin` to version 6.4.0 to ensure support for newer JVM runtimes. 

  Versions 7 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Minimum version of `aemanalyser-maven-plugin`:**
Update the usage of `aemanalyser-maven-plugin` to version 1.6.6 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `maven-bundle-plugin`:**
Update the usage of `maven-bundle-plugin` to version 5.1.5 or higher to ensure support for newer JVM runtimes. 

  Versions 6 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Update dependencies in `maven-scr-plugin`:**
The `maven-scr-plugin` is not directly compatible with Java 21 or Java 17. However, descriptor files can be generated by updating the ASM dependency version in the plugin configuration, as shown in the following example:

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
-->


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
>Om du installerar ett systempaket på det här sättet installeras det inte i den körningsmiljö som används för att köra Adobe Experience Manager. Om du behöver ett systempaket som är installerat i AEM ska du kontakta Adobe.

>[!TIP]
>
>Mer information om frontendens byggmiljö finns i [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
