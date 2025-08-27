---
title: Kontrollera och aktivera adaptiva Forms Core-komponenter i AEM Forms as a Cloud Service
description: Lär dig hur du kontrollerar om adaptiva Forms Core-komponenter är aktiverade och hur du aktiverar dem vid behov i AEM Forms as a Cloud Service.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
hide: true
hidefromtoc: true
source-git-commit: 3c1931d67e69d155e777c8761fe2bbbd21461ddf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Kontrollera och aktivera adaptiva Forms Core-komponenter {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | Den här artikeln |

Adaptiva Forms Core-komponenter och Headless Adaptive Forms är redan aktiverade för de flesta AEM Forms as a Cloud Service-kunder. På så sätt kan du skapa, publicera och leverera Core Components-baserade Adaptive Forms och Headless Forms med AEM Forms Cloud Service-instanser i flera kanaler.

## Kontrollera om adaptiva Forms Core-komponenter är aktiverade {#check-if-enabled}

Innan du följer några aktiveringssteg ska du kontrollera om adaptiva Forms Core-komponenter redan är aktiverade för din miljö:

### För nya AEM Forms as a Cloud Service-program

När du skapar ett nytt AEM Forms as a Cloud Service-program är adaptiva Forms Core-komponenter och Headless Adaptive Forms redan aktiverade för din miljö.

### För Cloud Service befintliga miljöer

Om din befintliga Cloud Service-miljö innehåller alternativet att [skapa Core Components-baserade Adaptive Forms](creating-adaptive-form-core-components.md) är adaptiva Forms Core-komponenter och Headless Adaptive Forms redan aktiverade för din miljö.

### Verifiera genom att kontrollera din databas

Så här bekräftar du att adaptiva Forms Core-komponenter är aktiverade för din miljö:

1. Klona AEM Forms as a Cloud Service-arkivet.

1. Öppna `[AEM Repository Folder]/all/pom.xml`-filen för din AEM Forms Cloud Service Git-databas.

1. Sök efter följande beroenden:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![leta reda på artefakten core-forms-components-af-core i all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Om det finns sådana beroenden aktiveras adaptiva Forms Core-komponenter för din miljö.

## När manuell aktivering krävs {#when-manual-enablement-needed}

Endast om du har ett äldre Forms as a Cloud Service-program där kärnkomponenter inte är aktiverade (bekräftas av kryssrutan ovan) måste du manuellt lägga till adaptiva Forms Core-komponentberoenden i din AEM as a Cloud Service-databas och distribuera databasen till dina Cloud Service-miljöer.

+++ Manuella aktiveringssteg 

>[!WARNING]
>
>Följ bara de här stegen om verifieringskontrollen ovan bekräftar att adaptiva Forms Core-komponenter INTE är aktiverade för din miljö.

Utför följande steg i listad ordning för att aktivera adaptiva Forms Core-komponenter och Headless Adaptive Forms för en AEM Forms as a Cloud Service-miljö:

![Aktivera kärnkomponenter och dynamiska adaptiva formulär](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## &#x200B;1. Klona din AEM Forms as a Cloud Service Git-databas {#clone-git-repository}

1. Logga in på [Cloud Manager](https://my.cloudmanager.adobe.com/) och välj organisation och program.

1. Gå till **pipelines**-kortet på sidan **Programöversikt** och klicka på knappen **Åtkomstrepoinformation** för att få tillgång till och hantera din Git-databas. Sidan innehåller följande information:

   * URL till Cloud Manager Git-databasen.
   * Autentiseringsuppgifter för Git-databasen (användarnamn och lösenord) Git-användarnamn.

   Klicka på **Generera lösenord** för att visa eller generera lösenordet.

1. Öppna terminalen eller kommandotolken på den lokala datorn och kör följande kommando:

   ```Shell
   git clone [Git Repository URL]
   ```

   Ange inloggningsuppgifterna när du uppmanas att göra det. Databasen klonas till din lokala dator.


## &#x200B;2. Lägg till adaptiva Forms Core-komponentberoenden i Git-databasen {#add-adaptive-forms-core-components-dependencies}

1. Öppna Git-databasmappen i en kodredigerare för oformaterad text. Exempel: VS-kod.
1. Öppna filen `[AEM Repository Folder]\pom.xml` för redigering.
1. Ersätt versioner av komponenterna `core.forms.components.version`, `core.forms.components.af.version` och `core.wcm.components.version` med versioner som anges i [dokumentationen för kärnkomponenter](https://github.com/adobe/aem-core-forms-components). Om komponenten inte finns lägger du till dessa komponenter.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![Uppge den senaste versionen av Forms Core Components](/help/forms/assets/latest-forms-component-version.png)

1. Lägg till följande beroenden i avsnittet Beroenden i filen `[AEM Repository Folder]\pom.xml` och spara filen.

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

1. Öppna filen `[AEM Repository Folder]/all/pom.xml` för redigering. Lägg till följande beroenden i avsnittet `<embeddeds>` och spara filen.

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
   >  Om du vill hitta din `${appId}` söker du efter termen `[AEM Repository Folder]/all/pom.xml` i filen `-packages/application/install`. Texten före termen `-packages/application/install` är din `${appId}`. Följande kod, `myheadlessform`, är till exempel `${appId}`.
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. Lägg till följande beroenden i `<dependencies>`-delen av filen `[AEM Repository Folder]/all/pom.xml` och spara filen:

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

1. Öppna `[AEM Repository Folder]/ui.apps/pom.xml` för redigering. Lägg till `af-core bundle`-beroendet och spara filen.

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

## &#x200B;3. Skapa och distribuera den uppdaterade koden

Distribuera den uppdaterade koden till din lokala utveckling och Cloud Service-miljöer för att aktivera Core Components i båda miljöerna:

* [Skapa och distribuera uppdaterad kod i en lokal utvecklingsmiljö (AEM as a Cloud Service SDK)](#core-components-on-aem-forms-local-sdk)

* [Skapa och driftsätt uppdaterad kod i en AEM Forms as a Cloud Service-miljö](#core-components-on-aem-forms-cs)

### Skapa och distribuera uppdaterad kod i en lokal utvecklingsmiljö {#core-components-on-aem-forms-local-sdk}

1. Öppna kommandotolken eller terminalen.

1. Navigera till rotkatalogen för Git-databasprojektet.

1. Kör följande kommando för att skapa paketet för din miljö:

   ```Shell
       mvn clean install
   ```



   När paketet har skapats finns det i [Git-databasmappen]\all\target\[appid].all-[version].zip

1. Använd [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) för att distribuera [AEM Archetype-projektmappen]\all\target\[appid].all-[version].zip-paketet på den lokala utvecklingsmiljön.


### Skapa och driftsätt uppdaterad kod i en AEM Forms as a Cloud Service-miljö {#core-components-on-aem-forms-cs}

1. Öppna terminalen eller kommandotolken.
1. Navigera till `[AEM Repository Folder]` och kör följande kommandon i den ordning som visas

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) när filerna har implementerats i Git-databasen.

   När pipeline-körningen har slutförts aktiveras adaptiva Forms Core-komponenter för motsvarande miljö. Dessutom har en adaptiv Forms-mall (Core Components) och Canvas 3.0-temat lagts till i din Forms as a Cloud Service-miljö, med alternativ för att anpassa och skapa Core Components-baserade Adaptive Forms.

+++

## Vanliga frågor {#faq}

### Vad är kärnkomponenter? {#core-components}

[Kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser.

### Vilka funktioner finns det för att aktivera kärnkomponenter? {#core-components-capabilities}

När de adaptiva Forms Core-komponenterna är aktiverade för din miljö läggs en tom Core Components-baserad Adaptive Form-mall och Canvas 3.0-tema till i din miljö. När du har aktiverat adaptiva Forms Core-komponenter för din miljö kan du:

* [Skapa grundkomponenter baserade på adaptiv Forms](/help/forms/creating-adaptive-form-core-components.md).
* [Skapa kärnkomponentbaserade adaptiva formulärmallar](/help/forms/template-editor.md).
* [Skapa anpassade teman för grundkomponentbaserade adaptiva formulärmallar](/help/forms/using-themes-in-core-components.md).
* [Servera Core Component-baserade adaptive Form-baserade JSON-representationer för kanaler som mobiler, webben, inbyggda appar och tjänster som kräver ett formulärs rubrikfria representation](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html).

### Hur vet jag om jag behöver aktivera adaptiva Forms Core-komponenter manuellt? {#manual-enablement-needed-faq}

De flesta kunder har redan aktiverat adaptiva Forms Core-komponenter. Du behöver bara aktivera dem manuellt om:

1. Du har ett äldre Forms as a Cloud Service-program som skapats innan Core Components inkluderades automatiskt
1. Verifieringskontrollen i avsnittet [Kontrollera om adaptiva Forms Core-komponenter är aktiverade](#check-if-enabled) bekräftar att nödvändiga beroenden saknas i din databas

Om du är osäker följer du verifieringsstegen i avsnittet [Kontrollera om adaptiva Forms Core-komponenter är aktiverade](#check-if-enabled) ovan.

### Varför kan inte kärnkomponentbaserade formulär återges i projekt?

Core Component-baserade formulär kan misslyckas med att återges på grund av en versionskonflikt mellan Forms Core Components-paketet och den version som ingår i projektets arketyp. Det här problemet inträffar oftast när den version som anges i projekttypen är lika med eller högre än den version som paketeras med Forms Core Components-paketet. Gör något av följande för att lösa problemet:

* Använd en lägre version av Forms Core Components-paketet i projektets arkityp.
* Ta bort Forms Core Components-beroendet från projekttypen eftersom den version som krävs redan ingår i AEM as a Cloud Service. Forms Core Components-paketet paketeras med AEM som ett molnbaserat SDK från och med version 2013, till exempel `AEM SDK v2025.3.20133.20250325T063357Z-250300`.

>[!MORELIKETHIS]
>
>* [Skapa ett anpassat formulär](/help/forms/creating-adaptive-form-core-components.md)
