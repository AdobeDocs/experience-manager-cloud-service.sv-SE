---
title: Cloud Manager-databaser
description: Cloud Manager-databaser
source-git-commit: e5d52c92c9162a58cc1a8e4f5d1169d59ee13119
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# Cloud Manager-databaser {#cloud-manager-repos}

Databaser som skapas och är tillgängliga i Cloud Manager kan visas och hanteras via sidan Databaser.

>[!NOTE]
>Det finns en gräns på 300 databaser för alla program i ett visst företag (eller IMS-organisation).

## Lägga till och hantera databaser {#add-manage-repos}

Följ stegen nedan för att visa och hantera databaser i Cloud Manager:

1. På sidan **Programöversikt** klickar du på fliken **Databaser** och går till sidan **Databaser**.

1. Klicka på **Lägg till databas** för att starta guiden.

   >[!NOTE]
   >En användare i rollen Distributionshanterare eller Affärsägare måste vara inloggad för att kunna lägga till en databas.

   ![](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![](/help/implementing/cloud-manager/assets/repos/repo-1.png)

1. Välj **Spara**. Din nyskapade rapport visas i tabellen enligt nedan.

   >[!NOTE]
   >Databaser som skapas i Cloud Manager är också tillgängliga så att du kan välja bland dem under stegen för att lägga till eller redigera pipeline. Mer information finns i [Konfigurera CI-CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en). Det finns en enskild *primär*-databas eller en gren för en given pipeline. Med [stöd för Git-undermodul](#git-submodule-support) kan dock många sekundära grenar inkluderas vid byggtiden.

   ![](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

1. Du kan markera databasen och klicka på menyalternativen längst till höger i tabellen till **Kopiera databas-URL** eller **Visa och uppdatera** eller **Ta bort** databasen, vilket visas i bilden nedan.

   ![](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

## Ta bort en databas {#delete-repo}

Följ stegen nedan för att ta bort en databas i Cloud Manager:
>[!NOTE]
>Om du tar bort en databas:
>1. Gör det borttagna databasnamnet oanvändbart för nya databaser som kan skapas i framtiden. Ett felmeddelande som visas nedan visas i det här fallet:
   >*Databasnamnet måste vara unikt inom organisationen.*
>1. Gör den borttagna databasen otillgänglig i Cloud Manager och kan därför inte länkas till en pipeline.


1. På sidan **Programöversikt** klickar du på fliken **Databaser** och går till sidan **Databaser**.

1. Markera databasen och klicka på menyalternativen längst till höger i tabellen. Klicka på **Ta bort** om du vill ta bort databasen, enligt bilden nedan.

   ![](/help/implementing/cloud-manager/assets/repos/delete-repo.png)


## Stöd för Git-undermodul {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället. När Cloud Managers byggprocess körs, efter att databasen som konfigurerats för pipelinen har klonats och den konfigurerade grenen har checkats ut, körs kommandot om grenen innehåller en `.gitmodules`-fil i rotkatalogen.

```
$ git submodule update --init
```

Då checkas varje undermodul in i lämplig katalog. Den här tekniken är ett möjligt alternativ till https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html för organisationer som är bekväma med att använda Git-undermoduler och som inte vill hantera en extern sammanfogningsprocess.

Låt oss till exempel säga att det finns tre databaser, där var och en innehåller en gren med namnet main . I den&quot;primära&quot; databasen, d.v.s. den som konfigurerats i pipelines, har huvudgrenen en pom.xml-fil som deklarerar projekten i de två andra databaserna:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Detta resulterar i en `.gitmodules`-fil som ser ut så här:

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Mer information om Git-undermoduler finns i [referenshandboken för Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Tänk på följande när du använder Git-undermoduler:

* Git-URL:en måste vara exakt i den syntax som beskrivs ovan. Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i dessa URL:er.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Git-undermoduler lagras som specifika Git-implementeringar. När ändringar görs i undermodulens databas måste därför den implementering som refereras uppdateras, till exempel med `git submodule update --remote` .
* Om inte annat är nödvändigt rekommenderas starkt att undermoduler av typen&quot;ytlig&quot; används. Det gör du genom att köra `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.

