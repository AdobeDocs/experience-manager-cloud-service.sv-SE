---
title: Aktivera adaptiva Forms Core-komponenter i AEM Forms as a Cloud Service och lokala utvecklingsmiljö
seo-title: Step-by-Step Guide for enabling Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment
description: Lär dig hur du aktiverar adaptiva Forms Core Components på AEM Forms as a Cloud Service med vår steg-för-steg-guide. I vår självstudiekurs får du hjälp med processen så att du enkelt kan aktivera den här kraftfulla funktionen i din AEM Forms-miljö.
seo-description: Learn how to enable Adaptive Forms Core Components on AEM Forms as a Cloud Service with our step-by-step guide. Our tutorial walks you through the process, making it easy to enable this powerful feature for your AEM Forms environment.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---


# Aktivera adaptiva Forms Core-komponenter i AEM Forms as a Cloud Service och lokala utvecklingsmiljö {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | Den här artikeln |

Genom att aktivera adaptiva Forms Core-komponenter på AEM Forms as a Cloud Service kan du börja skapa, publicera och leverera Core Components-baserade adaptiva Forms och Headless Forms med hjälp av AEM Forms Cloud Service-instanser i flera kanaler. Du behöver en adaptiv Forms Core Components-aktiverad miljö för att kunna använda Headless Adaptive Forms.

## Överväganden

* När du skapar ett nytt as a Cloud Service AEM Forms-program [Adaptiva Forms Core-komponenter och Headless Adaptive Forms är redan aktiverade för din miljö](#are-adaptive-forms-core-components-enabled-for-my-environment).

* Om du har ett äldre as a Cloud Service Forms-program där Core Components är [inte aktiverad](#enable-components)kan du [lägg till adaptiva Forms Core-komponentberoenden](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) till din AEM as a Cloud Service lagringsplats och distribuera databasen till dina Cloud Service för att möjliggöra Headless Adaptive Forms.

* Om din befintliga Cloud Service-miljö innehåller alternativ för att [skapa grundläggande komponentbaserade adaptiva Forms](creating-adaptive-form-core-components.md), adaptiva Forms Core-komponenter och Headless Adaptive Forms är redan aktiverade för din miljö och du kan använda Core Component-baserad Adaptive Forms som headless-formulär för kanaler som mobiler, webben, inbyggda appar och tjänster som kräver en headlessrepresentation av Adaptive Forms.


## Aktivera adaptiva Forms Core-komponenter och Headless Adaptive Forms {#enable-headless-forms}

Utför följande steg i listad ordning för att aktivera adaptiva Forms Core-komponenter och Headless Adaptive Forms för en as a Cloud Service AEM Forms-miljö


![Möjliggör centrala komponenter och headless adaptive forms](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. Klona din AEM Forms as a Cloud Service Git-databas {#clone-git-repository}

1. Logga in på [Cloud Manager](https://my.cloudmanager.adobe.com/) och väljer organisation och program.

1. Navigera till **Pipelines** från **Programöversikt** klickar du på **Åtkomst till svarsinformation** för att komma åt och hantera din Git-databas. Sidan innehåller följande information:

   * URL till Cloud Manager Git-databasen.
   * Autentiseringsuppgifter för Git-databasen (användarnamn och lösenord) Git-användarnamn.

   Klicka **Generera lösenord** för att visa eller generera lösenordet.

1. Öppna terminalen eller kommandotolken på den lokala datorn och kör följande kommando:

   ```Shell
   git clone [Git Repository URL]
   ```

   Ange inloggningsuppgifterna när du uppmanas att göra det. Databasen klonas till din lokala dator.


## 2. Lägg till adaptiva Forms Core-komponentberoenden i Git-databasen {#add-adaptive-forms-core-components-dependencies}

1. Öppna Git-databasmappen i en kodredigerare för oformaterad text. Exempel: VS-kod.
1. Öppna `[AEM Repository Folder]\pom.xml` fil för redigering.
1. Ersätt versioner av `core.forms.components.version`, `core.forms.components.af.version` och `core.wcm.components.version` komponenter med versioner angivna i [kärnkomponentdokumentation](https://github.com/adobe/aem-core-forms-components). Om komponenten inte finns lägger du till dessa komponenter.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![Uppge den senaste versionen av Forms Core Components](/help/forms/assets/latest-forms-component-version.png)

1. I avsnittet Beroenden i `[AEM Repository Folder]\pom.xml` lägger du till följande beroenden och sparar filen.

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. Öppna `[AEM Repository Folder]/all/pom.xml` fil för redigering. Lägg till följande beroenden i `<embeddeds>` och spara filen.

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  Ersätt `${appId}` med ditt appId.
   >
   >  Hitta `${appId}`, i `[AEM Repository Folder]/all/pom.xml` -fil, söka i `-packages/application/install` term. Texten före `-packages/application/install` termen `${appId}`. Följande kod, till exempel `myheadlessform` är `${appId}`.
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. I `<dependencies>` i `[AEM Repository Folder]/all/pom.xml` lägger du till följande beroenden och sparar filen:

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. Öppna `[AEM Repository Folder]/ui.apps/pom.xml` för redigering. Lägg till `af-core bundle` beroende och spara filen.

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >Kontrollera att följande adaptiva Forms Core Components-artefakter inte ingår i ditt projekt.
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > och
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. Spara och stäng filen.

## 3. Skapa och distribuera den uppdaterade koden

Distribuera den uppdaterade koden till din lokala utvecklingsmiljö och Cloud Service för att aktivera Core Components i båda miljöerna:

* [Skapa och distribuera uppdaterad kod i en lokal utvecklingsmiljö (AEM as a Cloud Service SDK)](#core-components-on-aem-forms-local-sdk)

* [Skapa och driftsätt uppdaterad kod i en as a Cloud Service AEM Forms-miljö](#core-components-on-aem-forms-cs)

### Skapa och distribuera uppdaterad kod i en lokal utvecklingsmiljö {#core-components-on-aem-forms-local-sdk}

1. Öppna kommandotolken eller terminalen.

1. Navigera till rotkatalogen för Git-databasprojektet.

1. Kör följande kommando för att skapa paketet för din miljö:

   ```Shell
       mvn clean install
   ```



   När paketet har skapats hittar du det på [Git-databasmapp]\all\target\[appid].all-[version].zip

1. Använd [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) för att distribuera [AEM Archetype-projektmapp]\all\target\[appid].all-[version]ZIP-paket i lokal utvecklingsmiljö.


### Skapa och driftsätt uppdaterad kod i en as a Cloud Service AEM Forms-miljö {#core-components-on-aem-forms-cs}

1. Öppna terminalen eller kommandotolken.
1. Navigera till `[AEM Repository Folder]` och kör följande kommandon i den ordning de visas

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. När filerna har implementerats i Git-databasen, [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   När pipeline-körningen har slutförts aktiveras adaptiva Forms Core-komponenter för motsvarande miljö. Dessutom har en adaptiv Forms-mall (Core Components) och Canvas 3.0-temat lagts till i Forms as a Cloud Service miljö, med alternativ för att anpassa och skapa Core Components-baserade Adaptive Forms.


## Vanliga frågor {#faq}

### Vad är kärnkomponenter? {#core-components}

The [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser.

### Vilka funktioner finns det för att aktivera kärnkomponenter? {#core-components-capabilities}

När de adaptiva Forms Core-komponenterna är aktiverade för din miljö läggs en tom Core Components-baserad Adaptive Form-mall och Canvas 3.0-tema till i din miljö. När du har aktiverat adaptiva Forms Core-komponenter för din miljö kan du:

* [Skapa grundkomponenter baserade på adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md).
* [Skapa grundkomponentbaserade adaptiva formulärmallar](/help/forms/template-editor.md).
* [Skapa egna teman för grundkomponentbaserade adaptiva formulärmallar](/help/forms/using-themes-in-core-components.md).
* [Servera Core Component-baserade Adaptive Form JSON-representationer för kanaler som mobiler, webben, inbyggda appar och tjänster som kräver att ett formulär visas utan rubrik](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html).

### Är adaptiva Forms Core-komponenter aktiverade för min miljö? {#enable-components}

Så här kontrollerar du att adaptiva Forms Core-komponenter är aktiverade för din miljö:

1. [Klona din AEM Forms as a Cloud Service databas](#1-clone-your-aem-forms-as-a-cloud-service-git-repository).

1. Öppna `[AEM Repository Folder]/all/pom.xml` -fil för din AEM Forms Cloud Service Git-databas.

1. Sök efter följande beroenden:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![leta reda på artefakten core-forms-components-af-core i all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Om det finns beroenden aktiveras adaptiva Forms Core-komponenter för din miljö.

