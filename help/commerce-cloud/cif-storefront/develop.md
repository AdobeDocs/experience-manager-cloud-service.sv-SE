---
title: Utveckla AEM Commerce för AEM as a Cloud Service
description: Lär dig hur du genererar ett e-handelsaktiverat AEM-projekt med AEM projekttyp. Lär dig hur du bygger och driftsätter projekt i en lokal utvecklingsmiljö med AEM as a Cloud Service SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---


# Utveckla AEM Commerce för AEM as a Cloud Service {#develop}

Utveckla AEM Commerce-projekt, som bygger på Commerce integration framework (CIF) for AEM as a Cloud Service, följer samma regler och bästa praxis som andra AEM-projekt på AEM as a Cloud Service. Granska följande först:

* [AEM projektstruktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md)
* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [AEM as a Cloud Service riktlinjer för utveckling](/help/implementing/developing/introduction/development-guidelines.md)

## Lokal utveckling med AEM as a Cloud Service SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

En lokal utvecklingsmiljö rekommenderas för CIF-projekt. CIF Add-On för AEM as a Cloud Service finns också för lokal utveckling. Den kan hämtas från [portalen för programdistribution.](/help/implementing/developing/tools/package-manager.md#software-distribution)

CIF Add-On finns som arkiv för Sling Feature. ZIP-filen som finns på Software Distribution Portal innehåller två Sling Feature-arkivfiler, en för AEM-författare och en för AEM publiceringsinstanser.

>[!TIP]
>
>**Ny på AEM as a Cloud Service?**
>>Ta en titt på [en mer detaljerad guide om hur du konfigurerar en lokal utvecklingsmiljö med AEM as a Cloud Service SDK.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)

### Nödvändig programvara {#required-software}

Följande bör installeras lokalt:

* [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
* [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
* [Node.js v10+](https://nodejs.org/en)
* [npm 6+](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

### Använda CIF Add-on {#accessing-add-on}

CIF-tillägget kan laddas ned som en zip-fil från [programdistributionsportalen.](/help/implementing/developing/tools/package-manager.md) ZIP-filen innehåller CIF-tillägget som **Sling Feature archive**, det är inte ett AEM-paket. SDK-listor kan köpas med en AEM as a Cloud Service-licens.

>[!TIP]
>
>Se till att du alltid använder den senaste CIF Add-On-versionen.

### Lokal installation {#local-setup}

Så här utvecklar du CIF Add-on lokalt med AEM as a Cloud Service SDK:

1. Skaffa de senaste AEM as a Cloud Service SDK.
1. Packa upp AEM .jar så att du kan skapa mappen `crx-quickstart`. Kör följande kommando:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Skapa en `crx-quickstart/install`-mapp.
1. Kopiera rätt fil för Sling Feature archive för CIF-tillägget till mappen `crx-quickstart/install`.

   * ZIP-filen för CIF-tillägget innehåller två Sling Feature-arkiv `.far`.
   * Se till att du använder rätt för AEM Author eller AEM Publish, beroende på hur du tänker köra AEM as a Cloud Service SDK lokalt.

1. Skapa en lokal systemmiljövariabel med namnet `COMMERCE_ENDPOINT` som innehåller slutpunkten för Adobe Commerce GraphQL.

   * Den här variabeln används av AEM för att ansluta till ditt handelssystem. CIF-tillägget innehåller en lokal omvänd proxy som gör Commerce GraphQL-slutpunkten tillgänglig lokalt. Den här proxyn används av CIF utvecklingsverktyg (produktkonsol och väljare) och för CIF klientkomponenter som gör direkta GraphQL-anrop.

   * Den här variabeln måste även ställas in för AEM as a Cloud Service-miljön. Mer information om variabler finns i [Konfigurera OSGi för AEM as a Cloud Service.](/help/implementing/deploying/configuring-osgi.md#local-development)

   * Exempel under macOS:

     ```bash
     export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

   * Exempel under Windows:

     ```bash
     set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

1. (Valfritt) Om du vill aktivera funktioner för mellanlagrade kataloger måste du skapa en integreringstoken för din Adobe Commerce-instans. Skapa token genom att följa stegen på [Komma igång](/help/commerce-cloud/cif-storefront/getting-started.md#staging).

   * Ange en OSGi-hemlighet med namnet `COMMERCE_AUTH_HEADER` till följande värde:

     ```xml
     Authorization: Bearer <Access Token>
     ```

   * Mer information om hemligheter finns i [Konfigurera OSGi för AEM as a Cloud Service.](/help/implementing/deploying/configuring-osgi.md#local-development)

1. Starta AEM as a Cloud Service SDK.

>[!NOTE]
>
>Se till att du startar AEM as a Cloud Service SDK i samma terminalfönster som systemvariabeln ställdes in i steg 5. Om du startar det i ett separat terminalfönster, eller om du dubbelklickar på .jar-filen, kontrollerar du att systemvariabeln är synlig.

Verifiera konfigurationen via OSGi-konsolen: `http://localhost:4502/system/console/osgi-installer`. Listan ska innehålla de CIF-tilläggspaket, innehållspaket och OSGi-konfigurationer som definieras i funktionsmodellfilen.

## Projektinställningar {#project}

Det finns två sätt att Bootstrap ditt CIF-projekt för AEM as a Cloud Service.

### Använd AEM Project Archetype {#project-archetype}

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype) är huvudverktyget för Bootstrap, ett förkonfigurerat projekt för att komma igång med CIF. CIF Core Components och alla nödvändiga konfigurationer kan inkluderas i ett genererat projekt med ytterligare ett alternativ.

>[!TIP]
>
>Använd alltid den senaste versionen av [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/releases) så att du kan generera projektet.

Se [användningsinstruktioner](https://github.com/adobe/aem-project-archetype#usage) för AEM Project Archetype om hur du genererar ett AEM-projekt. Använd alternativet `includeCommerce` om du vill inkludera CIF i projektet.

Till exempel:

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

CIF Core Components kan användas i alla projekt, antingen genom att inkludera det tillhandahållna `all`-paketet eller individuellt med CIF innehållspaket och relaterade OSGi-paket. Om du vill lägga till CIF Core-komponenter manuellt i ett projekt använder du följande beroenden:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Använd AEM Venia Reference Store {#venia-reference}

Ett andra alternativ för att starta ett CIF-projekt är att klona och använda [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store är ett exempel på hur CIF Core Components används för AEM. Det är avsett som en uppsättning med metodtips och en potentiell utgångspunkt för att utveckla din egen funktionalitet.

Börja med att klona Git-databasen och börja anpassa projektet efter dina behov.

>[!NOTE]
>
>Projektet Venia Reference Store innehåller två byggprofiler för AEM as a Cloud Service och AEM 6.5. Kontrollera [Viktigt om projekt.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) så att du kan se hur de används.

## Ytterligare resurser {#additional-resources}

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
