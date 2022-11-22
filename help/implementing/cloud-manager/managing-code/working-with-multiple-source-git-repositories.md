---
title: Använda flera databaser
description: Lär dig hur du hanterar flera Git-databaser när du arbetar med Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: a7ae6d75d6820f48d3d45cb5830f888a87d51de1
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Använda flera databaser {#working-with-multiple-source-git-repos}

Lär dig hur du hanterar flera Git-databaser när du arbetar med Cloud Manager.

## Synkroniserar kundhanterade Git-databaser {#syncing-customer-managed-git-repositories}

Istället för att arbeta direkt med Cloud Managers Git-databas [kunderna kan arbeta med sin egen Git-databas](integrating-with-git.md) eller flera egna Git-databaser. I dessa fall bör en automatisk synkroniseringsprocess konfigureras för att säkerställa att Cloud Managers Git-databas alltid är uppdaterad.

Beroende på var kundens Git-databas finns kan en GitHub-åtgärd eller en kontinuerlig integreringslösning som Jenkins användas för att konfigurera automatiseringen. Med en automatisering på plats kan varje överföring till en kundägd Git-databas automatiskt vidarebefordras till Cloud Managers Git-databas.

En sådan automatisering för en enskild kundägd Git-databas är enkel, men om du vill konfigurera den för flera databaser måste du först konfigurera den. Innehållet från flera Git-databaser måste mappas till olika kataloger i en enda Cloud Manager Git-databas.  Molnhanterarens Git-databas måste etableras med en rotmask `pom.xml`, som listar de olika delprojekten i modulavsnittet.

Följande är ett exempel `pom.xml` för två kundägda Git-databaser.

* Det första projektet placeras i katalogen med namnet `project-a`.
* Det andra projektet placeras i katalogen med namnet `project-b`.

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

En sådan rot `pom.xml` överförs till en gren i Cloud Managers Git-databas. Därefter måste de två projekten konfigureras för att automatiskt vidarebefordra ändringar till Cloud Managers Git-databas.

En möjlig lösning är följande:

1. En GitHub-åtgärd kan utlösas av en push-åtgärd till en gren i projekt A.
1. Åtgärden checkar ut projekt A och Cloud Manager Git-databasen och kopierar allt innehåll från projekt A till katalogen `project-a` i Cloud Managers Git-databas.
1. Sedan implementeras och push-överförs ändringen.

En ändring av huvudgrenen i projekt A skickas till exempel automatiskt till huvudgrenen i Cloud Managers Git-databas. Det kan finnas en mappning mellan grenar som en push till en gren som heter `dev` i projekt A skickas till en gren med namnet `development` i Cloud Managers Git-databas. Liknande steg krävs för projekt B.

Beroende på förgreningsstrategin och arbetsflödena kan synkroniseringen konfigureras för olika grenar. Om den använda Git-databasen inte tillhandahåller ett koncept som liknar GitHub-åtgärder, är en integrering via Jenkins (eller liknande) också möjlig. I det här fallet utlöser en webkrok ett Jenkins-jobb som utför arbetet.

Följ de här stegen för att lägga till en ny, tredje källa eller databas.

1. Lägg till en ny GitHub-åtgärd i den nya databasen som överför ändringar från den databasen till Cloud Managers Git-databas.
1. Utför den åtgärden minst en gång för att se till att projektkoden finns i Cloud Managers Git-databas.
1. Lägg till en referens till den nya katalogen i rotmappen Maven `pom.xml` i Cloud Manager Git-databasen.

## Exempel på GitHub-åtgärd {#sample-github-action}

Detta är ett exempel på GitHub-åtgärd som utlöses av en överföring till huvudgrenen och sedan övergår till en underkatalog till Cloud Managers Git-databas. GitHub-åtgärderna måste förses med två hemligheter, `MAIN_USER` och `MAIN_PASSWORD`, för att kunna ansluta och överföra till Cloud Managers Git-databas.

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

Att använda en GitHub-åtgärd är mycket flexibelt. Alla mappningar mellan grenar i Git-databaserna kan utföras liksom all mappning av de separata Git-projekten till huvudprojektets kataloglayout.

>[!NOTE]
>
>Exempelskriptet använder `git add` för att uppdatera databasen. Detta förutsätter att borttagningar inkluderas. Beroende på standardkonfigurationen för Git kan detta behöva ersättas med `git add --all`.

## Exempel på Jenkins-jobb {#sample-jenkins-job}

Detta är ett exempelskript som kan användas i ett Jenkins-jobb eller liknande och som har följande flöde:

1. Den aktiveras av en ändring i en Git-databas.
1. Jenkins-jobbet checkar ut det senaste läget för projektet eller grenen.
1. Jobbet utlöser sedan det här skriptet.
1. Skriptet checkar i sin tur ut Cloud Managers Git-databas och implementerar projektkoden i en underkatalog.

Jenkins-jobbet måste förses med två hemligheter. `MAIN_USER` och `MAIN_PASSWORD`, för att kunna ansluta och överföra till Cloud Managers Git-databas.

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

Att använda ett Jenkins-jobb är mycket flexibelt. Alla mappningar mellan grenar i Git-databaserna kan utföras liksom all mappning av de separata Git-projekten till huvudprojektets kataloglayout.

>[!NOTE]
>
>Exempelskriptet använder `git add` för att uppdatera databasen. Detta förutsätter att borttagningar inkluderas. Beroende på standardkonfigurationen för Git kan detta behöva ersättas med `git add --all`.
