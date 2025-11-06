---
title: Projektinställningar
description: Se hur AEM Projects byggs med Maven och vilka standarder du måste följa när du skapar ett eget projekt.
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---

# Projektinställningar {#project-setup}

Se hur AEM Projects byggs med Maven och vilka standarder du måste följa när du skapar ett eget projekt.

## Information om projektinställningar {#project-setup-details}

AEM Projects måste följa följande riktlinjer för att kunna bygga och driftsätta med Cloud Manager:

* Projekt måste skapas med [Apache Maven](https://maven.apache.org).
* Det måste finnas en `pom.xml`-fil i Git-databasens rot. Den här `pom.xml`-filen kan referera till så många undermoduler (som i sin tur kan ha andra undermoduler och så vidare) som det behövs.
* Du kan lägga till referenser till ytterligare Maven-artefaktdatabaser i dina `pom.xml`-filer. Åtkomst till [lösenordsskyddade artefaktdatabaser](#password-protected-maven-repositories) stöds vid konfigurering. Åtkomst till nätverksskyddade artefaktdatabaser stöds dock inte.
* Distribuerbara innehållspaket upptäcks genom att söka efter innehållspaketet `.zip` som finns i en katalog med namnet `target`. Ett valfritt antal undermoduler kan producera innehållspaket.
* Distribuerbara Dispatcher-artefakter upptäcks genom att söka efter `.zip`-filer (som också finns i katalogen `target`) som har katalogerna `conf` och `conf.d`.
* Om det finns mer än ett innehållspaket är det inte säkert att paketdistributioner ordnas. Om en viss ordning behövs kan innehållspaketets beroenden användas för att definiera ordningen.
* Paket kan [hoppas över](#skipping-content-packages) under distributionen.

## Aktivera Maven-profiler i Cloud Manager {#activating-maven-profiles-in-cloud-manager}

I vissa begränsade fall kan du behöva ändra din byggprocess något när du kör i Cloud Manager jämfört med när du kör på arbetsstationer för utvecklare. I dessa fall kan [Maven-profiler](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) användas för att definiera hur bygget ska vara olika i olika miljöer, inklusive Cloud Manager.

Aktivering av en Maven-profil i Cloud Manager-byggmiljön bör göras genom att söka efter `CM_BUILD` [miljövariabeln ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). På samma sätt bör en profil som bara är avsedd att användas utanför Cloud Manager byggmiljö göras genom att man söker efter denna variabel som saknas.

Om du till exempel bara vill visa ett enkelt meddelande när bygget körs i Cloud Manager gör du följande:

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

Om du bara vill få ut ett enkelt meddelande när bygget körs utanför Cloud Manager gör du följande:

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

## Använd en lösenordsskyddad Maven-databas i Cloud Manager {#password-protected-maven-repositories}

>[!NOTE]
>
>Distribuera artefakter från lösenordsskyddade Maven-databaser med försiktighet, eftersom Cloud Manager inte utvärderar koden med sina [regler för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md). Den här metoden bör reserveras för sällsynta situationer och endast tillämpas på kod som inte är relevant för AEM. Adobe rekommenderar att du inkluderar både Java-källorna och hela projektets källkod tillsammans med binärfilen. På så sätt får du bättre transparens och underhållbarhet under hela driftsättningsprocessen.

**Så här använder du en lösenordsskyddad Maven-databas i Cloud Manager:**

1. Ange lösenordet (och eventuellt användarnamnet) som en hemlig [pipeline-variabel](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md).
1. Referera sedan till den hemligheten i en fil med namnet `.cloudmanager/maven/settings.xml` i Git-databasen, som följer schemat för [ Maven Settings File](https://maven.apache.org/settings.html) .

När Cloud Manager byggprocess startar:

* Elementet `<servers>` i den här filen sammanfogas i standardfilen `settings.xml` som tillhandahålls av Cloud Manager.
   * Server-ID:n som börjar med `adobe` och `cloud-manager` betraktas som reserverade. Använd dem inte på anpassade servrar.
   * Cloud Manager speglar endast de server-ID:n som matchar specifika prefix eller standard-ID:t `central`. Alla andra server-ID:n undantas från spegling.
* När den här filen är på plats refereras server-ID:t inifrån ett `<repository>`- och/eller `<pluginRepository>` -element i `pom.xml`-filen.
* I allmänhet ingår dessa `<repository>`- och `<pluginRepository>`-element i en [Cloud Manager-specifik profil](#activating-maven-profiles-in-cloud-manager), även om det inte är absolut nödvändigt att inkludera dem.

Låt oss till exempel säga att databasen är på `https://repository.myco.com/maven2`, att användarnamnet som Cloud Manager ska använda är `cloudmanager` och att lösenordet är `secretword`. Gör så här:

1. Ange lösenordet som en hemlighet i pipeline.

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. Referera den här hemligheten från filen `.cloudmanager/maven/settings.xml` i följande:

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

Konfigurera maven-source-plugin i projektet för att göra det.

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

Det är en god vana att driftsätta hela projektkällan tillsammans med binärfilen i en Maven-databas. På så sätt kan den återskapa den exakta artefakten.

Konfigurera maven-assembly-plugin i ditt projekt på följande sätt:

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

I Cloud Manager kan byggen producera valfritt antal innehållspaket. Det kan av olika skäl vara önskvärt att skapa ett innehållspaket men inte distribuera det. Ett exempel inträffar när innehållspaket byggs enbart i testsyfte eller när ett annat steg i byggprocessen paketerar om dem. Det vill säga ett underpaket till ett annat paket.

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

I många fall distribueras samma kod till flera AEM-miljöer. När det är möjligt undviker Cloud Manager att återskapa kodbasen när det upptäcker att samma Git-implementering används i flera fullständiga pipeline-körningar.

När en körning startas extraheras den aktuella HEAD-implementeringen för grenflödet. Hash för implementeringen visas i användargränssnittet och via API:t. När byggsteget har slutförts lagras de resulterande artefakterna baserat på den implementeringshashen och kan återanvändas i efterföljande pipeline-körningar.

Paket återanvänds i alla rörledningar om de ingår i samma program. När AEM söker efter paket som kan återanvändas ignoreras grenar och artefakter återanvänds i alla grenar.

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

1. När du kör Pipeline 1 skapas paketen normalt.
1. När du sedan kör Pipeline 2 återanvänds de paket som skapats med Pipeline 1.

#### Exempel 2 {#example-2}

Programmet har två grenar:

* Gren `foo`
* Gren `bar`

Båda grenarna har samma implementerings-ID.

1. En utvecklingspipeline skapar och kör `foo`.
1. Därefter byggs och körs `bar` av en produktionspipeline.

I det här fallet återanvänds artefakten från `foo` för produktionsflödet eftersom samma implementeringshash identifierades.

### Avmarkera {#opting-out}

Om du vill kan återanvändningsbeteendet inaktiveras för specifika pipelines genom att pipeline-variabeln `CM_DISABLE_BUILD_REUSE` anges till `true`. Om den här variabeln anges extraheras implementeringshash-koden och de resulterande artefakterna sparas för senare användning, men återanvändning av tidigare lagrade artefakter hoppas över. Tänk på följande scenario om du vill förstå detta:

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
* [Versionshantering för Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) ersätter endast projektversionen i produktionspipelines.
Om samma implementering används för både en utvecklingsdriftsättning och en produktionsprocess, och utvecklingsdistributionen körs först, distribueras versionerna till scenen och produktionen oförändrad. I det här fallet skapas dock fortfarande en tagg.
* Om hämtningen av de lagrade artefakterna inte lyckas körs steget som om inga artefakter lagrades.
* Andra förloppsvariabler än `CM_DISABLE_BUILD_REUSE` beaktas inte när Cloud Manager beslutar att återanvända tidigare skapade byggartefakter.
