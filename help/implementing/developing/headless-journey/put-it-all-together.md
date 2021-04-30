---
title: Så här sätter du samman allt - din app och ditt innehåll i AEM utan rubriker
description: I den här delen av AEM Headless Developer Journey kan du lära dig hur du tar ditt AEM-projekt, inklusive innehållsfragment, dina GraphQL-anrop, dina REST API-anrop och programmet, och förbereder det för publicering.
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: e8eb9d2c96d24601e50c48f6846a8c8bac8b0252
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---

# Placera allt tillsammans - din app och ditt innehåll i AEM Headless {#put-it-all-together}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) lär du dig hur du tar ditt AEM, inklusive innehållsfragment, dina GraphQL-anrop, dina REST API-anrop och ditt program, och förbereder det för live-körning.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet om den AEM resan [Uppdatera ditt innehåll via AEM Assets API:er](update-your-content.md) lärde du dig att uppdatera ditt befintliga headless-innehåll i AEM via API, och du bör nu:

* Förstå AEM Assets HTTP API.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du förbereder ett eget AEM headless-projekt för publicering.

## Mål {#objective}

* Förstå det lokala utvecklingsarbetsflödet för AEM
* Installera AEM SDK för att få en lokal utvecklingsmiljö som du kan använda för att testa ditt innehåll i
* Läs om de utvecklingsverktyg du behöver för att arbeta utanför den lokala utvecklingsmiljön

## Arbetsflödet för lokal utveckling {#the-local-development-workflow}

Det lokala utvecklingsprojektet bygger på Apache Maven och använder Git för källkontroll. För att kunna uppdatera projektet kan utvecklarna använda den integrerade utvecklingsmiljö de föredrar, till exempel Eclipse, Visual Studio Code eller IntelliJ.

Om du vill testa kod- eller innehållsuppdateringar som ska importeras av ditt headless-program måste du distribuera uppdateringarna till en lokal AEM, som innehåller lokala instanser av AEM författare och publiceringsinstanser.

Observera skillnaden mellan de olika komponenterna i den lokala AEM, eftersom det är viktigt att testa uppdateringarna där de är som viktigast, till exempel testa innehållsuppdateringar på författaren eller testa ny kod på publiceringsinstansen.

I ett produktionssystem placeras en dispatcher och en http Apache-server alltid framför en AEM publiceringsinstans. De tillhandahåller cachelagring och säkerhetstjänster för AEM system, så det är viktigt att testa kod- och innehållsuppdateringar mot avsändaren också.

När du har testat allt och fungerar som det ska kan du nu överföra koduppdateringarna till en centraliserad Git-databas i Cloud Manager.

När uppdateringarna har överförts till Cloud Manager kan de distribueras till AEM som en Cloud Service med Cloud Managers CI/CD-pipeline.


## AEM SDK {#the-aem-sdk}

AEM SDK används för att skapa och distribuera anpassad kod. Den innehåller följande artefakter:

* Quickstart jar - en körbar jar-fil som kan användas för att ställa in både en författare och en publiceringsinstans
* Dispatcher-verktyg - Dispatcher-modulen och dess beroenden för Windows- och UNIX-baserade system
* Java API Jar - Java Jar/Maven Dependency som visar alla Java API:er som kan användas för att utveckla mot AEM
* Javadoc jar - javadocs for the Java API jar

## Installation av lokal utvecklingsmiljö {#local-development-environment}

För att kunna förbereda AEM headless-projekt för lansering måste du se till att alla delar av projektet fungerar bra.

För att göra det måste ni sätta ihop allt - kod, innehåll och konfiguration - och testa det i en lokal utvecklingsmiljö för att kunna vara redo live.

Den lokala utvecklingsmiljön består av tre huvudområden:

1. Det AEM projektet - det innehåller all kod, konfiguration och innehåll som AEM utvecklare kommer att arbeta med
1. Local AEM Runtime - lokala versioner av AEM författare och publiceringstjänster som ska användas för att distribuera kod från det AEM projektet
1. Local Dispatcher Runtime - en lokal version av Apache htttpd-webbservern som innehåller Dispatcher-modulen

## Utvecklingsverktyg {#development-tools}

Förutom AEM SDK behöver du ytterligare verktyg som gör det lättare att utveckla och testa kod och innehåll lokalt:

* Java
* Git
* Apache Maven
* Biblioteket Node.js
* Den utvecklingsmiljö du vill använda

Eftersom AEM är ett Java-program måste du installera Java och Java SDK som stöd för utveckling av AEM som en Cloud Service.

Git är det verktyg du kommer att använda för att hantera källkontrollen samt för att checka in ändringarna i Cloud Manager och sedan distribuera dem till en produktionsinstans.

AEM använder Apache Maven för att bygga projekt som skapats från AEM Maven Project-arkitypen. Alla större utvecklingsmiljöer har stöd för integrering av Maven.

Node.js är en JavaScript-körningsmiljö som används för att arbeta med de viktigaste resurserna i ett AEM ui.front-projekt. Node.js distribueras med npm, är de facto-pakethanteraren Node.js, som används för att hantera JavaScript-beroenden.

## What&#39;s Next {#what-is-next}

Du bör fortsätta din AEM resa utan trassel genom att nästa gång granska dokumentet [How to Go Live with Your Headless Application](go-live.md) där du faktiskt tar ditt AEM Headless-projekt live!

## Ytterligare resurser {#additional-resources}

* [Installation](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime)  av lokal utvecklingsmiljö - läs om hur du installerar de verktyg som behövs för att börja utveckla för AEM
* [AEM som Cloud Service-SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)  - titta närmare på AEM SDK