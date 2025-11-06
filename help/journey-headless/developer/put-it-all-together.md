---
title: Sammanställ allt - din app och ditt innehåll i AEM Headless
description: I den här delen av AEM Headless Developer Journey kan du lära dig hur du tar ditt AEM-projekt, inklusive innehållsfragment, dina GraphQL-samtal, dina REST API-anrop och programmet, och förbereder det för publicering.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Sammanställ allt - din app och ditt innehåll i AEM Headless {#put-it-all-together}

I den här delen av [AEM Headless Developer Journey](overview.md) får du lära dig hur du använder AEM utvecklingsverktyg och Headless SDK för att sätta ihop programmen.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM resa [How to Update Your Content via AEM Assets APIs](update-your-content.md) lärde du dig att uppdatera ditt befintliga headless-innehåll i AEM via API, och du bör nu:

* Förstå AEM Assets HTTP API.

## Syfte {#objective}

I den här artikeln får du veta hur du sätter ihop AEM headless-program genom att:

* Lär dig mer om AEM Headless SDK och de utvecklingsverktyg som krävs
* Konfigurera en lokal utvecklingsmiljö för att simulera ditt innehåll innan det publiceras
* Grundläggande om AEM innehållsreplikering

## AEM SDK {#the-aem-sdk}

AEM SDK används för att skapa och distribuera anpassad kod. Det är huvudverktyget som du behöver så att du kan utveckla och testa programmet utan huvud innan du publicerar det. Den innehåller följande artefakter:

* Quickstart jar - en körbar jar-fil som kan användas för att ställa in både författare och publiceringsinstans
* Dispatcher-verktyg - Dispatcher-modulen och dess beroenden för Windows- och UNIX®-baserade system
* Java™ API Jar - Java™ Jar/Maven Dependency som visar alla Java™-API:er som kan användas för att utveckla mot AEM
* Javadoc jar - javadocs for the Java™ API jar

## AEM Headless SDK {#the-aem-headless-sdk}

AEM **Headless SDK** skiljer sig från AEM SDK och är en uppsättning bibliotek som klienter kan använda för att snabbt och enkelt interagera med AEM Headless API:er via HTTP.

Mer information finns i [AEM Headless SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=sv-SE).

## Ytterligare utvecklingsverktyg {#additional-development-tools}

Förutom AEM SDK behöver du ytterligare verktyg som underlättar utveckling och testning av kod och innehåll lokalt:

* Java™
* Git
* Apache Maven
* The Node.js library
* Den utvecklingsmiljö du vill använda

Eftersom AEM är ett Java™-program måste du installera Java™ och Java™ SDK för att stödja utvecklingen av AEM as a Cloud Service.

Git är det ni använder för att hantera källkontroll och för att checka in ändringarna i Cloud Manager och sedan distribuera dem till en produktionsinstans.

AEM använder Apache Maven för att bygga projekt som genererats från AEM Maven Project Archetype. Alla större utvecklingsmiljöer har stöd för integrering av Maven.

Node.js är en JavaScript-körningsmiljö som används för att arbeta med de främsta resurserna i ett AEM-projekts `ui.frontend`-underprojekt. Node.js distribueras med npm, som är de facto-pakethanteraren Node.js, som används för att hantera JavaScript-beroenden.

## Lathund för komponenter i ett AEM-system {#components-of-an-aem-system-at-a-glance}

Nu ska vi titta närmare på de olika delarna av en AEM-miljö.

En komplett AEM-miljö består av en författare, en publiceringsversion och en Dispatcher. Samma komponenter är tillgängliga i den lokala utvecklingsmiljön så att du kan göra det enklare för dig att förhandsgranska kod och innehåll innan du publicerar.

* **Författartjänsten** är den plats där interna användare skapar, hanterar och förhandsgranskar innehåll.

* **Publiceringstjänsten** betraktas som Live-miljön och är vanligtvis den slutanvändare som interagerar med. Innehåll som har redigerats och godkänts av författartjänsten distribueras till publiceringstjänsten. Det vanligaste distributionsmönstret med AEM headless-program är att ha produktionsversionen av programmet ansluten till en AEM Publish-tjänst.

* **Dispatcher** är en statisk webbserver som utökas med modulen AEM Dispatcher. Den cachelagrar webbsidor som skapats av publiceringsinstansen för att förbättra prestandan.

## Arbetsflödet för lokal utveckling {#the-local-development-workflow}

Det lokala utvecklingsprojektet bygger på Apache Maven och använder Git för källkontroll. För att uppdatera projektet kan utvecklarna använda den integrerade utvecklingsmiljö de föredrar, till exempel Eclipse, Visual Studio Code eller IntelliJ.

Om du vill testa kod- eller innehållsuppdateringar som är inkapslade av ditt headless-program måste du distribuera uppdateringarna till den lokala AEM-miljön, som innehåller lokala instanser av AEM författare och publiceringstjänster.

Observera skillnaden mellan de olika komponenterna i den lokala AEM-miljön, eftersom det är viktigt att testa uppdateringarna där de är som viktigast. Testa till exempel innehållsuppdateringar på författaren eller testa ny kod på publiceringsinstansen.

I ett produktionssystem placeras en Dispatcher- och en http Apache-server alltid framför en publiceringsinstans i AEM. De tillhandahåller cachelagring och säkerhetstjänster för AEM-systemet, så det är oerhört viktigt att testa kod- och innehållsuppdateringar mot Dispatcher också.

## Förhandsgranska kod och innehåll lokalt med den lokala utvecklingsmiljön {#previewing-your-code-and-content-locally-with-the-local-development-environment}

För att förbereda AEM headless-projekt för lansering måste du se till att alla projektdelar fungerar som de ska.

För att göra det måste ni sätta ihop allt: kod, innehåll och konfiguration, och testa det i en lokal utvecklingsmiljö för att kunna vara redo live.

Den lokala utvecklingsmiljön består av tre huvudområden:

1. AEM Project - det här projektet innehåller all kod, konfiguration och innehåll som AEM-utvecklare kommer att arbeta med
1. Local AEM Runtime - lokala versioner av AEM-författaren och publiceringstjänster som används för att distribuera kod från AEM-projektet
1. Den lokala Dispatcher-miljön - en lokal version av Apache htttpd-webbservern som innehåller Dispatcher-modulen

När den lokala utvecklingsmiljön har konfigurerats kan du simulera innehåll som skickas till React-appen genom att distribuera en statisk nodserver lokalt.

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## What&#39;s Next {#whats-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey bör du:

* Lär känna AEM utvecklingsverktyg
* Förstå arbetsflödet för lokal utveckling

Fortsätt din resa utan AEM genom att nästa gång granska dokumentet [Så här gör du live med ditt Headless-program](/help/journey-headless/developer/go-live.md) där du faktiskt kan publicera ditt AEM Headless-projekt!

## Ytterligare resurser {#additional-resources}

* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Konfigurera en lokal AEM-miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=sv-SE)
* [AEM Headless SDK för webbläsare på klientsidan (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [AEM Headless SDK för server-side/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [AEM Headless SDK for Java™](https://github.com/adobe/aem-headless-client-java)
* [Introduktion till AEM som Headless CMS](/help/headless/introduction.md)
* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=sv-SE)
* [Självstudiekurser för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=sv-SE)
