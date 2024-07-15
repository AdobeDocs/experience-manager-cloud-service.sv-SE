---
title: Komma igång med Adaptiv Forms.
description: Lär dig hur du skapar mobilresponsiva adaptiva Forms med vår stegvisa självstudiekurs. Dessa formulär kan anpassas sömlöst mellan olika enheter och ger en smidig upplevelse.
keywords: Adaptiv Forms, responsiv Forms, HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: b59cb56c-9629-48e4-b5c9-a861013a1360
source-git-commit: af58a784f24f212962ad73f11015fb788493d8b5
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---

# Skapa ett adaptivt formulär (kärnkomponenter) - självstudiekurs

I den här tiden förväntar man sig en mobilvänlig upplevelse i alla interaktioner, och blanketterna är inget undantag. Anpassningsbara formulär kan hjälpa er att skapa formulär som inte bara är mobilvänliga utan också förbättrar användarengagemanget och minskar tiden det tar att fylla i dem.

I den här självstudiekursen får du en stegvis vägledning om hur du skapar ett anpassat formulär. Den är indelad i ett användningsfall och flera guider, som var och en lär dig hur du lägger till en ny funktion i ett anpassat formulär.

I slutet av självstudiekursen kan du:

* Skapa ett anpassningsbart formulär och dess datamodell
* Formatera ditt anpassningsbara formulär
* Bygg affärsregler med redigeraren för anpassade formulärregler
* förifylla anpassningsbara formulärfält
* Lägg till e-signaturer i formuläret
* Protect formuläret från start med Google reCAPTCHA
* Lokalisera ditt anpassningsbara formulär för olika språk
* Konfigurera formuläret för att producera strukturerade data
* Konfigurera formuläret för att skicka data till en REST-slutpunkt
* Publish ditt adaptiva formulär


## Varför skapa ett formulär som bygger på kärnkomponenter?

AEM Forms tillhandahåller Foundation Components och Core Components för att skapa formulärupplevelser. Kärnkomponenterna är det moderna och rekommenderade sättet att skapa nya formulärupplevelser. Varför använda kärnkomponenter? De här komponenterna är enkla, med öppen källkod (finns för github), har bra Google Lighthuse- och webbinarier, är kompatibla med hjälpmedel och har alla de välbekanta funktionerna i AEM Sites (som versionshantering och lokalisering). Dessutom är de här komponenterna enklare att formatera och du kan enkelt anpassa deras utseende enligt företagets riktlinjer för varumärkesanpassning. Dessa har inga beroenden från tredje part, och utvecklare med kunskap om JavaScript och CSS kan enkelt anpassa dessa komponenter.

![Varför skapa Core Components-baserade Adaptive Forms? De här komponenterna är lätta, enklare att formatera, har hög ljusstyrka, stöder tillgänglighetsstandarder, är enkelt anpassningsbara, har öppen källkod, finns på github, är inte beroende av bibliotek från tredje part och har nästan ingen inlärningskurva för AEM utvecklare och AEM författare Förutom AEM Forms Core Components har de alla funktioner som finns i AEM WCM Core Components.](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## Användningsfall: Effektiv förkvalificering av bostadslån med adaptiv Forms

I den här självstudiekursen skapar du ett anpassat formulär för en stor bank. Användningsexempel:

Potentiella köpare besöker bankens webbplats eller filial för att utforska alternativ för bostadslån. Den traditionella programprocessen är lång och överväldigande och kräver ofta dokumentation i förväg. Detta hindrar vissa köpare från att starta processen, vilket förhindrar både bankens huvudgenerering och köparens möjlighet att tryggt söka efter sina drömhem.

Du ska ta fram en interaktiv blankett för förkvalificering av bostadslån. Detta formulär skulle samla in grundläggande information, förkvalificera låntagaren utifrån deras indata, erbjuda beräknade lånebelopp, potentiella nedbetalningsbehov och räntor baserade på olika lånetyper. Användare som är kvalificerade i förväg kan initiera en fullständig låneansökan direkt från blanketten för förhandsgodkännande.

Formuläret skulle byggas med anpassningsbara formulär. Detta ger en personaliserad upplevelse och samlar samtidigt in nödvändiga ekonomiska uppgifter för korrekt förkvalificering av bostadslån.

När du är klar med självstudiekursen ser ditt formulär ut och fungerar så här:

![Lägg till ett arbetsformulär här](/help/forms/assets/cc-tutorial-final-form.png)

## Konfigurera utvecklingsmiljö

Du kan skapa och testa det adaptiva formuläret direkt på den lokala datorn innan du distribuerar det till en Cloud Service-miljö. Adobe tillhandahåller en AEM SDK för lokal utveckling som du kan använda

* Skapa, anpassa och testa formulär lokalt.
* Utforma teman för formulär och bygg konfigurationer lokalt,
* Distribuera enkelt dina färdiga resurser till molnet.

Lokal utveckling med AEM SDK sparar tid och förenklar utvecklingsprocessen


**Klar att börja?**

1. [Konfigurera utvecklingsverktyg för AEM projekt](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects): Hämta och installera den senaste versionen av [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up), [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git), [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js) och [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven). Du kan även installera en vanlig textredigerare. Exemplen i den här självstudiekursen är baserade på Visual Studio Code.

1. [Installera AEM SDK](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development): Hämta och installera den senaste versionen av AEM SDK. Detta är de verktyg som behövs för AEM. Anteckna versionen av AEM SDK.

   ![Programvarudistribution](/help/forms/assets/software-distribution.png)

   ![installera AEM SDK](/help/forms/assets/start-aem-sdk.png)

1. [Lägg till AEM Forms-tillägget](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users): Hämta och installera AEM Forms-tilläggsmatchningen till den version av ditt AEM-SDK som finns på [Software Distribution](https://experience.adobe.com/#/downloads)-portalen.
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++Installera AEM Forms Add-on:

   Installera AEM Forms Add-on:

   1. Stoppa AEM SDK.
   1. Lägg till AEM Forms-tilläggsfilen (.far) i mappen `AEM SDK/crx-quickstart/install`,
   1. Starta om AEM SDK.

+++

1. [Konfigurera användarbehörigheter](/help/forms/setup-local-development-environment.md#configure-users-and-permissions): Skapa användare med utvecklings-, redigerings- och andra behörigheter och lägg till dessa användare i fördefinierade formulärgrupper.


1. [Lägg till adaptiva Forms-mallar](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype): Använd AEM 48 eller senare för att skapa ett nytt AEM och distribuera det till din AEM SDK. Projektet lägger till adaptiva Forms-mallar i AEM SDK.

   ![Adaptiva formulärmallar](/help/forms/assets/adaptive-forms-templates.png)

   +++Lägg till adaptiva Forms-mallar i AEM SDK:

   1. Kör kommandot nedan för att skapa ett AEM projekt.

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![AEM-Archetyoe-Project](/help/forms/assets/aem-archetype-project.png)

   1. Distribuera projektet till din lokala utvecklingsmiljö. Du kan använda följande kommando för att distribuera till den lokala utvecklingsmiljön

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   När du har distribuerat AEM kan du se adaptiva Forms-mallar i din miljö.

+++


Detaljerade instruktioner och stegvisa anvisningar om hur du konfigurerar din lokala AEM Forms-utvecklingsmiljö finns i artikeln [Konfigurera lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md) .



## Nästa steg

När du har konfigurerat utvecklingsmiljön kan du skapa ett anpassat formulär. I nästa artikel lär du dig att

* Skapa ett anpassat formulär från den tomma mallen
* Layoutfält för att visa och enkelt ta emot information.
* Förhandsgranska formuläret.

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->
