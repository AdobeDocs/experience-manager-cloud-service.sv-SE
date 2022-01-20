---
title: Information om projektinställningar
description: Projektkonfigurationsinformation - Cloud Services
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 4219c8ce30a0f1cd44bbf8e8de46d6be28a1ddf3
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 5%

---

# Konfigurera projektet {#project-setup-details}

## Ändra projektinställningsinformation {#modifying-project-setup-details}

För att kunna byggas och driftsättas med Cloud Manager måste befintliga AEM följa vissa grundläggande regler:

* Projekt måste byggas med Apache Maven.
* Det måste finnas en *pom.xml* -filen i Git-databasens rot. Detta *pom.xml* filen kan referera till så många undermoduler (som i sin tur kan ha andra undermoduler osv.) vid behov.

* Du kan lägga till referenser till ytterligare Maven-artefaktdatabaser i dina *pom.xml* filer. Åtkomst till [lösenordsskyddade artefaktarkiv](#password-protected-maven-repositories) stöds vid konfigurering. Åtkomst till nätverksskyddade artefaktdatabaser stöds dock inte.
* Distribuerbara innehållspaket identifieras genom sökning efter innehållspaket *zip* filer som finns i en katalog med namnet *target*. Ett valfritt antal undermoduler kan producera innehållspaket.

* Distribuerbara Dispatcher-artefakter upptäcks vid sökning efter *zip* filer (igen, i en katalog med namnet *target*) som har kataloger namngivna *conf* och *conf.d*.

* Om det finns mer än ett innehållspaket är det inte säkert att paketdistributioner ordnas. Om en viss ordning behövs kan innehållspaketets beroenden användas för att definiera ordningen. Paket kan vara [överhoppad](#skipping-content-packages) från driftsättning.


## Aktivera Maven-profiler i Cloud Manager {#activating-maven-profiles-in-cloud-manager}

I vissa begränsade fall kan du behöva ändra din byggprocess något när du kör i Cloud Manager i stället för när den körs på arbetsstationer för utvecklare. I dessa fall [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) kan användas för att definiera hur bygget ska vara olika i olika miljöer, inklusive Cloud Manager.

Aktivering av en Maven-profil i Cloud Managers byggmiljö bör göras genom att söka efter miljövariabeln CM_BUILD som beskrivs ovan. Omvänt bör en profil som bara är avsedd att användas utanför Cloud Manager-byggmiljön göras genom att leta efter denna variabel som saknas.

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
>Om du vill testa den här profilen på en arbetsstation för utvecklare kan du antingen aktivera den på kommandoraden (med `-PcmBuild`) eller i din integrerade utvecklingsmiljö.

Om du bara vill få ut ett enkelt meddelande när bygget körs utanför Cloud Manager gör du det här:

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
>Artefakter från en lösenordsskyddad Maven-databas bör endast användas med försiktighet eftersom kod som distribueras via den här mekanismen för närvarande inte kan köras med alla kvalitetsregler som implementerats i Cloud Managers Quality Gates. Därför bör det endast användas i sällsynta fall och för kod som inte är knuten till AEM. Du bör också distribuera Java-källorna samt hela projektets källkod tillsammans med binärfilen.

Om du vill använda en lösenordsskyddad Maven-databas från Cloud Manager anger du lösenordet (och eventuellt användarnamnet) som en hemlig Pipeline-variabel och refererar sedan till hemligheten i en fil med namnet `.cloudmanager/maven/settings.xml` i Git-databasen. Filen följer [Maven Settings-fil](https://maven.apache.org/settings.html) schema. När Cloud Manager-byggprocessen startar `<servers>` -elementet i den här filen kommer att sammanfogas med standardvärdet `settings.xml` som tillhandahålls av Cloud Manager. Server-ID:n som börjar med `adobe` och `cloud-manager` betraktas som reserverade och bör inte användas av anpassade servrar. Server-ID **not** matchar något av dessa prefix eller standard-ID `central` kommer aldrig att speglas av Cloud Manager. När den här filen är på plats refereras server-ID:t inifrån en `<repository>` och/eller `<pluginRepository>` -element inuti `pom.xml` -fil. I allmänhet gäller följande `<repository>` och/eller `<pluginRepository>` -element finns inuti en [Cloud Manager-specifik profil](#activating-maven-profiles-in-cloud-manager)även om det inte är absolut nödvändigt.

Exempel: låt oss säga att databasen finns på https://repository.myco.com/maven2. `cloudmanager` och lösenordet är `secretword`.

Först anger du lösenordet som en hemlighet i pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Referera sedan det här från `.cloudmanager/maven/settings.xml` fil:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

Och referera slutligen till server-ID:t i `pom.xml` fil:

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

Konfigurera maven-source-plugin i ditt projekt:

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

Det är en god vana att driftsätta hela projektkällan tillsammans med binärfilen i en Maven-databas, vilket innebär att den exakta artefakten kan återskapas.

Konfigurera maven-assembly-plugin i ditt projekt:

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

I Cloud Manager kan byggen producera valfritt antal innehållspaket.
Det kan av olika skäl vara önskvärt att skapa ett innehållspaket men inte distribuera det. Detta kan till exempel vara användbart när du skapar innehållspaket som bara används för testning eller som paketeras om med ett annat steg i byggprocessen, det vill säga som ett underpaket till ett annat paket.

För att hantera dessa scenarier söker Cloud Manager efter egenskapen ***cloudManagerTarget*** i egenskaperna för de byggda innehållspaketen. Om den här egenskapen är inställd på ”ingen” hoppas paketet över och driftsätts inte. Mekanismen för hur den här egenskapen anges beror på hur innehållspaketet skapas. Med till exempel filevault-maven-plugin konfigurerar du plugin-programmet så här:

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

Med content-package-maven-plugin är den ungefär så här:

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

I många fall distribueras samma kod till flera AEM miljöer. Om det är möjligt kommer Cloud Manager att undvika att återskapa kodbasen när det upptäcker att samma Git-implementering används i flera fullständiga pipeline-körningar.

När en körning startas extraheras den aktuella HEAD-implementeringen för förgreningsflödet. Hash för implementeringen visas i användargränssnittet och via API:t. När byggsteget har slutförts lagras de resulterande artefakterna baserat på den implementeringshashen och kan återanvändas i efterföljande pipeline-körningar. När en återanvändning sker ersätts stegen för bygg- och kodkvalitet effektivt med resultaten från den ursprungliga körningen. Loggfilen för byggsteget innehåller artefakter och körningsinformation som användes för att skapa dem från början.

Här följer ett exempel på sådana loggutdata.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

Loggen för kodkvalitetssteget innehåller liknande information.

### Avmarkera {#opting-out}

Om du vill kan återanvändningsbeteendet inaktiveras för specifika rörledningar genom att ange rörledningsvariabeln `CM_DISABLE_BUILD_REUSE` till `true`. Om den här variabeln är inställd extraheras fortfarande implementeringshashen och de resulterande artefakterna lagras för senare användning, men eventuella tidigare lagrade artefakter återanvänds inte. Tänk på följande scenario om du vill förstå det här beteendet.

1. En ny pipeline skapas.
1. Pipelinen körs (exekvering nr 1) och den aktuella implementeringen i HEAD är `becdddb`. Körningen är klar och de resulterande artefakterna sparas.
1. The `CM_DISABLE_BUILD_REUSE` variabeln är inställd.
1. Pipelinen körs igen utan att koden ändras. Även om lagrade artefakter är associerade med `becdddb`, används de inte på grund av `CM_DISABLE_BUILD_REUSE` variabel.
1. Koden ändras och pipeline körs. HEAD har bekräftat `f6ac5e6`. Körningen är klar och de resulterande artefakterna sparas.
1. The `CM_DISABLE_BUILD_REUSE` variabeln tas bort.
1. Pipelinen körs igen utan att koden ändras. Eftersom lagrade artefakter är associerade med `f6ac5e6`, återanvänds dessa artefakter.

### Caveats {#caveats}

* [Hantering av versioner av Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) ersätter endast projektversionen i produktionspipelines. Om samma implementering används både för en körning av en utvecklingsdistribution och en körning av en produktionspipeline och utvecklingsdistributionen körs först, distribueras versionerna till fas och produktion utan att ändras. I det här fallet kommer dock en tagg fortfarande att skapas.
* Om hämtningen av de lagrade artefakterna inte lyckas kommer byggsteget att utföras som om inga artefakter hade lagrats.
* Andra rörledningsvariabler än `CM_DISABLE_BUILD_REUSE` tas inte med i beräkningen när Cloud Manager bestämmer sig för att återanvända tidigare skapade byggartefakter.
