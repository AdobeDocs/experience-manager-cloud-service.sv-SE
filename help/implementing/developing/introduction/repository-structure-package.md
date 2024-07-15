---
title: AEM projektdatabasstrukturpaket
description: Maven-projekt på Adobe Experience Manager as a Cloud Service kräver en definition av underpaketet Databasstruktur vars enda syfte är att definiera de JCR-databasrötter som projektets Code-underpaket distribueras till.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 520ab0229b4f00a1de981209bf26059b0d00c3da
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# AEM projektdatabasstrukturpaket

Maven-projekt för Adobe Experience Manager as a Cloud Service kräver en underpaketsdefinition för databasstruktur vars enda syfte är att definiera de JCR-databasrötter som projektets kodunderpaket distribueras till. Den här metoden ser till att installationen av paket i Experience Manager as a Cloud Service automatiskt beställs av JCR-resursberoenden. Saknade beroenden kan leda till scenarier där delstrukturer installeras före de överordnade strukturerna och därför tas bort oväntat, vilket bryter distributionen.

Om kodpaketet distribueras till en plats **som inte täcks** av kodpaketet, måste alla överordnade resurser (JCR-resurser som ligger närmare JCR-roten) räknas upp i databasstrukturpaketet. Denna process är nödvändig för att fastställa dessa beroenden.

![Databasstrukturpaket](./assets/repository-structure-packages.png)

Databasstrukturpaketet definierar det förväntade, gemensamma tillståndet för `/apps` som paketvalideraren använder för att fastställa områden som är säkra från potentiella konflikter när de är standardrottar.

De vanligaste sökvägarna som ska inkluderas i databasstrukturpaketet är:

+ `/apps` som är en systemansluten nod
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...` och `/apps/sling/...` som tillhandahåller vanliga övertäckningar för `/libs`.
+ `/apps/settings`, som är den delade kontextredigerade konfigurationsrotsökvägen

Det här underpaketet **har inte** något innehåll och består endast av en `pom.xml` som definierar filterrötterna.

## Skapa databasstrukturpaketet

Om du vill skapa ett databasstrukturpaket för ditt Maven-projekt skapar du ett tomt Maven-underprojekt med följande `pom.xml`, och uppdaterar projektets metadata så att de överensstämmer med ditt överordnade Maven-projekt.

Uppdatera `<filters>` så att den omfattar alla sökvägar till JCR-databasen som dina kodpaket distribueras till.

Se till att du lägger till det här nya Maven-underprojektet i listan över överordnade projekt `<modules>`.

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

Om du vill använda databasstrukturpaketet refererar du till det via alla kodpaket (delpaket som distribueras till `/apps`) Maven-projekt via konfigurationen för FileVault-innehållspaketet Maven plug-ins `<repositoryStructurePackage>` .

I `ui.apps/pom.xml`, och i alla andra kodpaket `pom.xml`, lägger du till en referens till projektets konfiguration för databasstrukturpaket (#database-structure-package) i plugin-programmet för FileVault-paketet Maven.

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

+ Kodpaket A distribueras till `/apps/a`
+ Kodpaket B distribueras till `/apps/a/b`

Om ett beroende på paketnivå inte har etablerats från kodpaket B i kodpaket A, kan kodpaket B distribueras först till `/apps/a`. Om det sedan följs av kodpaket A, som distribueras till `/apps/a`, blir resultatet att den tidigare installerade `/apps/a/b` tas bort.

I detta fall:

+ Kodpaket A ska definiera `<repositoryStructurePackage>` i projektets databasstrukturpaket (som ska ha ett filter för `/apps`).
+ Kodpaket B ska definiera `<repositoryStructurePackage>` för kodpaket A eftersom kodpaket B distribueras till ett utrymme som delas av kodpaket A.

## Fel och felsökning

Om databasstrukturpaketen inte är korrekt konfigurerade rapporteras ett fel vid konstruktionen av Maven:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Det här felet anger att det inte finns någon `<repositoryStructurePackage>` som listar `/apps/some/path` i filterlistan för det här paketet.

## Ytterligare resurser

+ [Plugin-programmet FileVault Content Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
