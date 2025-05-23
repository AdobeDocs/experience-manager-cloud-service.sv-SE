---
title: Stöd för Git-undermodul
description: Lär dig hur du kan använda Git-undermoduler för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0712ba8918696f4300089be24cad3e4125416c02
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Stöd för Git-undermodul för Adobe-databaser {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.

När Cloud Manager byggprocess körs klonas pipeline-databasen och grenen checkas ut. Om det finns en `.gitmodules`-fil i förgreningens rotkatalog körs motsvarande kommando.

Följande kommando checkar ut varje undermodul i lämplig katalog.

```
$ git submodule update --init
```

Den här tekniken erbjuder ett alternativ till den lösning som beskrivs i [Arbeta med flera Source Git-databaser](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md). Det är idealiskt för organisationer som är bekväma med Git-undermoduler och som föredrar att inte hantera en extern sammanfogningsprocess.

Anta till exempel att det finns tre databaser. Varje databas innehåller en enskild gren med namnet `main`. I den primära databasen, d.v.s. den som konfigurerats i pipelines, har grenen `main` en `pom.xml`-fil som deklarerar projekten i de andra två databaserna:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

Sedan lägger du till undermoduler för de två andra databaserna:

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Resultatet är en `.gitmodules`-fil som liknar följande:

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Se även [Git-referenshandboken](https://git-scm.com/book/en/v2/Git-Tools-Submodules) för mer information om Git-undermoduler.

## Användningsinformation {#usage-notes}

* Git-URL:en måste vara exakt i den syntax som beskrivs i föregående avsnitt.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i Git-URL:er.
* Om inget annat är nödvändigt rekommenderar Adobe att du använder korta undermoduler genom att köra följande:
  `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.
* Git-undermodulreferenser lagras för specifika Git-implementeringar. Detta innebär att när ändringar görs i undermodulens databas måste implementeringen som refereras uppdateras.
Du kan till exempel använda följande:

  `git submodule update --remote`

## Stöd för Git-undermodul för privata databaser {#private-repositories}

Stöd för Git-undermoduler i [privata databaser](private-repositories.md) liknar vanligtvis deras användning med Adobe-databaser.

När du har konfigurerat din `pom.xml`-fil och kört `git submodule`-kommandona måste du lägga till en `.gitmodules`-fil i rotkatalogen i aggregeringsdatabasen för att Cloud Manager ska känna igen undermodulens konfiguration.

![.gitmodules-fil](assets/gitmodules.png)

![Aggregator](assets/aggregator.png)

### Användningsinformation {#usage-notes-recommendations-private-repos}

* Git-URL:er för delmodulen kan vara i HTTPS- eller SSH-format, men måste peka på en GitHub.com. Det går inte att lägga till en Adobe-databasundermodul i en GitHub-aggregeringsdatabas eller den omvända.
* GitHub-undermoduler måste vara tillgängliga för Adobe GitHub-appen.
* [Begränsningarna med att använda Git-undermoduler med Adobe-hanterade databaser ](#limitations-recommendations) gäller också.
