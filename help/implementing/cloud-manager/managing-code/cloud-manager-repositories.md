---
title: Cloud Manager-databaser
description: Lär dig hur du skapar, visar och tar bort Git-databaser i Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Cloud Manager-databaser {#cloud-manager-repos}

Lär dig hur du skapar, visar och tar bort Git-databaser i Cloud Manager.

>[!NOTE]
>
>Det finns en gräns på 300 databaser i alla program i ett visst företag eller i en IMS-organisation.

## Lägga till och hantera databaser {#add-manage-repos}

Följ de här stegen för att visa och hantera databaser i Cloud Manager.

1. Från **Programöversikt** sida, klicka på **Databaser** och navigera till **Databaser** sida.

1. Klicka på **Lägg till databas** för att starta guiden.

   ![Knappen Lägg till databas](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Ange namn och beskrivning enligt begäran och klicka på **Spara**.

   ![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/assets/repos/repo-1.png)

När guiden stängs visas den nya databasen i tabellen.

Du kan markera databasen i tabellen och klicka på ellipsknappen och välja **Kopiera databas-URL**, **Visa och uppdatera**, eller **Ta bort**.

![Databasalternativ](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Databaser som skapas i Cloud Manager kan du också välja när du lägger till eller redigerar pipelines. Se dokumentet [CI-CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) om du vill veta mer.

Det finns en enda primär databas eller en gren för en given pipeline. Med [stöd för Git-delmodul](#git-submodule-support)kan många sekundära grenar inkluderas vid byggtillfället.

>[!NOTE]
>
>En användare måste ha rollen **Distributionshanteraren** eller **Företagsägare** för att kunna lägga till en databas.

## Ta bort en databas {#delete-repo}

Om du tar bort en databas:

* Gör det borttagna databasnamnet oanvändbart för nya databaser som kan skapas i framtiden.
   * Felmeddelandet `Repository name should be unique within organization.` visas i sådana fall.
* Gör den borttagna databasen otillgänglig i Cloud Manager och inte tillgänglig för länkning till en pipeline.

Följ dessa för att ta bort en databas i Cloud Manager.

1. Från **Programöversikt** sida, klicka på **Databaser** och navigera till **Databaser** sida.

1. Markera databasen och klicka på ellipsknappen och välj **Ta bort** för att ta bort databasen.

   ![Ta bort databas](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Stöd för Git-undermodul {#git-submodule-support}

Git-undermoduler kan användas för att sammanfoga innehåll från flera grenar i Git-databaser vid byggtillfället.

När Cloud Managers byggprocess körs, efter att databasen som konfigurerats för pipelinen klonats och den konfigurerade grenen checkas ut, om grenen innehåller en `.gitmodules` -filen i rotkatalogen körs kommandot.

Med följande kommando checkas varje undermodul ut i lämplig katalog.

```
$ git submodule update --init
```

Den här tekniken är ett möjligt alternativ till den lösning som beskrivs i dokumentet [Arbeta med Git-databaser med flera källor](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) för organisationer som känner sig bekväma med att använda Git-undermoduler och inte vill hantera en extern sammanfogningsprocess.

Låt oss till exempel säga att det finns tre databaser, där var och en innehåller en gren med namnet `main`. I den primära databasen, dvs. den som konfigurerats i pipelines, `main` grenen har en `pom.xml` fil som deklarerar projekten i de två andra databaserna.

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

Sedan lägger du till undermoduler för de två andra databaserna.

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Detta resulterar i en `.gitmodules` -fil som liknar följande:

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

Mer information om Git-undermoduler finns i [Git-referenshandbok.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Begränsningar och Recommendations {#limitations-recommendations}

Tänk på följande begränsningar när du använder Git-undermoduler.

* Git-URL:en måste vara exakt i den syntax som beskrivs i föregående avsnitt.
* Det finns bara stöd för undermoduler i roten av förgreningen.
* Av säkerhetsskäl ska du inte bädda in autentiseringsuppgifter i Git-URL:er.
* Om inget annat är nödvändigt rekommenderas en kort undermodul.
   * Om du vill göra det kör du `git config -f .gitmodules submodule.<submodule path>.shallow true` för varje undermodul.
* Git-undermodulreferenser lagras för specifika Git-implementeringar. Detta innebär att när ändringar görs i undermodulens databas måste implementeringen som refereras uppdateras.
   * Genom att till exempel använda `git submodule update --remote`
