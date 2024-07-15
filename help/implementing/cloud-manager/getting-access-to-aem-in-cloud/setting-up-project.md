---
title: Projektinställningar
description: Lär dig hur AEM byggs med Maven och de standarder du måste följa när du skapar ditt eget projekt.
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1399'
ht-degree: 0%

---

# Projektinställningar {#project-setup}

Lär dig hur AEM byggs med Maven och de standarder du måste följa när du skapar ditt eget projekt.

## Information om projektinställningar {#project-setup-details}

För att kunna bygga och driftsätta med Cloud Manager måste AEM följa följande riktlinjer:

* Projekt måste skapas med [Apache Maven.](https://maven.apache.org)
* Det måste finnas en `pom.xml`-fil i Git-databasens rot. Den här `pom.xml`-filen kan referera till så många undermoduler (som i sin tur kan ha andra undermoduler och så vidare) som det behövs.
* Du kan lägga till referenser till ytterligare Maven-artefaktdatabaser i dina `pom.xml`-filer.
   * Åtkomst till [lösenordsskyddade artefaktdatabaser](#password-protected-maven-repositories) stöds vid konfigurering. Åtkomst till nätverksskyddade artefaktdatabaser stöds dock inte.
* Distribuerbara innehållspaket upptäcks genom att söka efter innehållspaketet `.zip` som finns i en katalog med namnet `target`.
   * Ett valfritt antal undermoduler kan producera innehållspaket.
* Distribuerbara dispatcherartefakter upptäcks genom sökning efter `.zip` filer (som också finns i katalogen `target`) med katalogerna `conf` och `conf.d`.
* Om det finns mer än ett innehållspaket är det inte säkert att paketdistributioner ordnas.
   * Om en viss ordning behövs kan innehållspaketets beroenden användas för att definiera ordningen.
* Paket kan [hoppas över](#skipping-content-packages) under distributionen.

## Aktivera Maven-profiler i Cloud Manager {#activating-maven-profiles-in-cloud-manager}

I vissa begränsade fall kan du behöva ändra din byggprocess något när du kör i Cloud Manager jämfört med när du kör på arbetsstationer för utvecklare. I dessa fall kan [Maven-profiler](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) användas för att definiera hur bygget ska vara olika i olika miljöer, inklusive Cloud Manager.

Aktivering av en Maven-profil i Cloud Manager-byggmiljön bör göras genom att söka efter `CM_BUILD` [miljövariabeln ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). På samma sätt bör en profil som bara är avsedd att användas utanför Cloud Manager byggmiljö göras genom att man söker efter denna variabel som saknas.

Om du t.ex. bara vill visa ett enkelt meddelande när bygget körs i Cloud Manager gör du det här.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>Om du vill testa den här profilen på en arbetsstation för utvecklare kan du antingen aktivera den på kommandoraden (med `-PcmBuild`) eller i den integrerade utvecklingsmiljön (IDE).

Och om du bara vill få ut ett enkelt meddelande när bygget körs utanför Cloud Manager gör du det här.

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## Lösenordsskyddat databasstöd för Maven {#password-protected-maven-repositories}

>[!NOTE]
>
>Artefakter från en lösenordsskyddad Maven-databas bör användas med försiktighet eftersom kod som distribueras via den här mekanismen för närvarande inte körs via [regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md) som implementeras i Cloud Manager kvalitetsportar. Därför bör det endast användas i sällsynta fall och för kod som inte är knuten till AEM. Du bör också distribuera Java-källorna och hela projektets källkod tillsammans med binärfilen.

Så här använder du en lösenordsskyddad Maven-databas i Cloud Manager:

1. Ange lösenordet (och eventuellt användarnamnet) som en hemlig [pipeline-variabel](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md).
1. Referera sedan till den hemligheten i en fil med namnet `.cloudmanager/maven/settings.xml` i Git-databasen, som följer schemat för [ Maven Settings File](https://maven.apache.org/settings.html) .

När Cloud Manager byggprocess startar:

* Elementet `<servers>` i den här filen sammanfogas i standardfilen `settings.xml` som tillhandahålls av Cloud Manager.
   * Server-ID:n som börjar med `adobe` och `cloud-manager` betraktas som reserverade. Använd dem inte på anpassade servrar.
   * Server-ID:n som inte matchar något av dessa prefix eller standard-ID:t `central` speglas aldrig av Cloud Manager.
* När den här filen är på plats refereras server-ID:t inifrån ett `<repository>`- och/eller `<pluginRepository>` -element i `pom.xml`-filen.
* I allmänhet finns dessa `<repository>`- och/eller `<pluginRepository>`-element i en [Cloud Manager-specifik profil](#activating-maven-profiles-in-cloud-manager), även om det inte är absolut nödvändigt.

Låt oss till exempel säga att databasen är på `https://repository.myco.com/maven2`, att användarnamnet som Cloud Manager ska använda är `cloudmanager` och att lösenordet är `secretword`. Du gör så här:

1. Ange lösenordet som en hemlighet i pipeline.

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. Referera det här från filen `.cloudmanager/maven/settings.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. Referera slutligen till server-ID:t i filen `pom.xml`:

   ```xml
   <profiles>
       <profile>
           <id>cmBuild</id>
           <activation>
                   <property>
                       <name>env.CM_BUILD</name>
                   </property>
           </activation>
           <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
       </profile>
   </profiles>
   ```

### Distribuera källor {#deploying-sources}

Det är en god vana att driftsätta Java-källorna tillsammans med binärfilen i en Maven-databas.

Det gör du genom att konfigurera maven-source-plugin i projektet.

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-source-plugin</artifactId>
             <executions>
                 <execution>
                     <id>attach-sources</id>
                     <goals>
                         <goal>jar-no-fork</goal>
                     </goals>
                 </execution>
             </executions>
         </plugin>
```

### Distribuera projektkällor {#deploying-project-sources}

Det är en god vana att driftsätta hela projektkällan tillsammans med binärfilen i en Maven-databas. Detta gör att den exakta artefakten kan återskapas.

Det gör du genom att konfigurera maven-assembly-plugin i ditt projekt.

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-assembly-plugin</artifactId>
             <executions>
                 <execution>
                     <id>project-assembly</id>
                     <phase>package</phase>
                     <goals>
                         <goal>single</goal>
                     </goals>
                     <configuration>
                         <descriptorRefs>
                             <descriptorRef>project</descriptorRef>
                         </descriptorRefs>
                     </configuration>
                 </execution>
             </executions>
         </plugin>
```

## Hoppar över innehållspaket {#skipping-content-packages}

I Cloud Manager kan byggen producera valfritt antal innehållspaket. Det kan av olika skäl vara önskvärt att skapa ett innehållspaket men inte distribuera det. Ett exempel kan vara när innehållspaket som bara används för testning skapas eller som paketeras om av ett annat steg i byggprocessen. Det vill säga ett underpaket till ett annat paket.

Cloud Manager letar efter egenskapen `cloudManagerTarget` i egenskaperna för det inbyggda innehållspaketet för att hantera de här scenarierna. Om den här egenskapen är inställd på `none` hoppas paketet över och distribueras inte.

Mekanismen för att ange den här egenskapen beror på hur bygget skapar innehållspaketet. Med till exempel `filevault-maven-plugin` konfigurerar du plugin-programmet enligt följande.

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

`content-package-maven-plugin` har en liknande konfiguration.

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## Bygg återanvändning av felaktigheter {#build-artifact-reuse}

I många fall distribueras samma kod till flera AEM miljöer. När det är möjligt kommer Cloud Manager att undvika att återskapa kodbasen när det upptäcker att samma Git-implementering används i flera fullständiga pipeline-körningar.

När en körning startas extraheras den aktuella HEAD-implementeringen för förgreningsflödet. Hash för implementeringen visas i användargränssnittet och via API:t. När byggsteget har slutförts lagras de resulterande artefakterna baserat på den implementeringshashen och kan återanvändas i efterföljande pipeline-körningar.

Paket återanvänds i alla rörledningar om de ingår i samma program. När du söker efter paket som kan återanvändas ignorerar AEM grenar och återanvänder artefakter över grenar.

När en återanvändning sker ersätts stegen för bygg- och kodkvalitet effektivt med resultaten från den ursprungliga körningen. Loggfilen för byggsteget innehåller artefakter och körningsinformation som användes för att skapa dem från början.

Här följer ett exempel på sådana loggutdata.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

Loggen för kodkvalitetssteget innehåller liknande information.

### Exempel {#example-reuse}

#### Exempel 1 {#example-1}

Tänk på att ditt program har två utvecklingspipelines:

* Pipeline 1 på grenen `foo`
* Pipeline 2 på gren `bar`

Båda grenarna har samma implementerings-ID.

1. Om du kör pipeline 1 först byggs paketen normalt.
1. När du sedan kör Pipeline 2 återanvänds paket som skapats med Pipeline 1.

#### Exempel 2 {#example-2}

Programmet har två grenar:

* Gren `foo`
* Gren `bar`

Båda grenarna har samma implementerings-ID.

1. En utvecklingspipeline skapar och kör `foo`.
1. Därefter byggs och körs `bar` av en produktionspipeline.

I det här fallet återanvänds artefakten från `foo` för produktionsflödet eftersom samma implementeringshash identifierades.

### Avmarkera {#opting-out}

Om du vill kan återanvändningsbeteendet inaktiveras för specifika pipelines genom att pipeline-variabeln `CM_DISABLE_BUILD_REUSE` anges till `true`. Om den här variabeln är inställd extraheras fortfarande implementeringshashen och de resulterande artefakterna lagras för senare användning, men tidigare lagrade artefakter återanvänds inte. Tänk på följande scenario om du vill förstå det här beteendet.

1. En ny pipeline skapas.
1. Pipelinen körs (körning nr 1) och den aktuella HEAD-implementeringen är `becdddb`. Körningen är klar och de resulterande artefakterna sparas.
1. Variabeln `CM_DISABLE_BUILD_REUSE` har angetts.
1. Pipelinen körs igen utan att koden ändras. Även om det finns lagrade artefakter som är associerade med `becdddb`, återanvänds de inte på grund av variabeln `CM_DISABLE_BUILD_REUSE`.
1. Koden ändras och pipeline körs. HEAD implementering är nu `f6ac5e6`. Körningen är klar och de resulterande artefakterna sparas.
1. Variabeln `CM_DISABLE_BUILD_REUSE` har tagits bort.
1. Pipelinen körs igen utan att koden ändras. Eftersom det finns lagrade artefakter associerade med `f6ac5e6`, återanvänds dessa artefakter.

### Caveats {#caveats}

* Skapa artefakter återanvänds inte i olika program, oavsett om implementeringshashen är identisk.
* Artefakter återanvänds i samma program även om grenen och/eller pipeline är annorlunda.
* [Versionshantering för Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) ersätter endast projektversionen i produktionspipelines. Om samma implementering används både för en körning av en utvecklingsdistribution och en körning av en produktionspipeline och utvecklingsdistributionen körs först, distribueras versionerna till fas och produktion utan att ändras. I det här fallet kommer dock en tagg fortfarande att skapas.
* Om hämtningen av de lagrade artefakterna inte lyckas körs byggsteget som om inga artefakter hade lagrats.
* Andra förloppsvariabler än `CM_DISABLE_BUILD_REUSE` beaktas inte när Cloud Manager beslutar att återanvända tidigare skapade byggartefakter.
