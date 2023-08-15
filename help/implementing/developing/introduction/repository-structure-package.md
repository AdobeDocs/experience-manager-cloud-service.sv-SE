---
title: Strukturpaket för AEM-projektdatabas
description: Maven-projekt på Adobe Experience Manager as a Cloud Service kräver en definition av underpaketet Databasstruktur vars enda syfte är att definiera de JCR-databasrötter som projektets Code-underpaket distribueras till.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 2%

---

# Strukturpaket för AEM-projektdatabas

Maven-projekt för Adobe Experience Manager as a Cloud Service kräver en underpaketsdefinition för databasstruktur vars enda syfte är att definiera de JCR-databasrötter som projektets kodunderpaket distribueras till. Den här metoden ser till att installationen av paket på Experience Manager as a Cloud Service automatiskt beställs av JCR-resursberoenden. Saknade beroenden kan leda till scenarier där delstrukturer installeras före de överordnade strukturerna och därför tas bort oväntat, vilket bryter distributionen.

Om kodpaketet distribueras till en plats **inte täckt** av kodpaketet måste alla överordnade resurser (JCR-resurser närmare JCR-roten) räknas upp i databasstrukturpaketet. Denna process är nödvändig för att fastställa dessa beroenden.

![Databasstrukturpaket](./assets/repository-structure-packages.png)

Databasstrukturpaketet definierar det förväntade, gemensamma tillståndet för `/apps` som paketvalideraren använder för att fastställa områden som är&quot;säkra från potentiella konflikter&quot; eftersom de är standardrottar.

De vanligaste sökvägarna som ska inkluderas i databasstrukturpaketet är:

+ `/apps` som är en systemansluten nod
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`och `/apps/sling/...` som innehåller gemensamma övertäckningar för `/libs`.
+ `/apps/settings` som är den delade kontextmedvetna konfigurationsrotsökvägen

Det här underpaketet **har inte** allt innehåll och endast består av `pom.xml` definiera filterrötterna.

## Skapa databasstrukturpaketet

Om du vill skapa ett databasstrukturpaket för ditt Maven-projekt skapar du ett tomt Maven-delprojekt med följande `pom.xml`, uppdaterar projektmetadata enligt det överordnade Maven-projektet.

Uppdatera `<filters>` för att inkludera alla sökvägar till JCR-databasen som dina kodpaket distribueras till.

Se till att lägga till det nya Maven-delprojektet i de överordnade projekten `<modules>` lista.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlay structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Referera till databasstrukturpaketet

Om du vill använda databasstrukturpaketet refererar du det via alla kodpaket (de delpaket som distribueras till `/apps`) Maven projects via FileVault content package Maven plug-ins `<repositoryStructurePackage>` konfiguration.

I `ui.apps/pom.xml`och alla andra kodpaket `pom.xml`s lägger du till en referens till projektets konfiguration av databasstrukturpaket (#database-structure-package) i plugin-programmet för FileVault-paketet Maven.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## Användningsfall för paket med flera koder

Ett mindre vanligt och mer komplicerat användningsfall är stöd för driftsättning av flera kodpaket som installeras i samma områden i JCR-databasen.

Till exempel:

+ Kodpaket A distribuerar till `/apps/a`
+ Kodpaket B distribueras till `/apps/a/b`

Om ett beroende på paketnivå inte har etablerats från kodpaket B i kodpaket A, kan kodpaket B distribueras först i `/apps/a`. Därefter följer kodpaketet B, som distribueras till `/apps/a`. Resultatet blir att den tidigare installerade filen tas bort `/apps/a/b`.

I detta fall:

+ Kodpaket A bör definiera en `<repositoryStructurePackage>` i projektets databasstrukturpaket (som ska ha ett filter för `/apps`).
+ Kodpaket B bör definiera en `<repositoryStructurePackage>` i kodpaket A, eftersom kodpaket B distribueras i utrymme som delas av kodpaket A.

## Fel och felsökning

Om databasstrukturpaketen inte är korrekt konfigurerade rapporteras ett fel vid konstruktionen av Maven:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Det här felet indikerar att det inte finns någon `<repositoryStructurePackage>` som listor `/apps/some/path` i filterlistan.

## Ytterligare resurser

+ [Plugin-programmet FileVault Content Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
