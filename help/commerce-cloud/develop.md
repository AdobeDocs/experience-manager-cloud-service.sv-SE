---
title: Utveckla AEM för AEM som Cloud Service
description: Lär dig hur du skapar ett e-handelsaktiverat AEM med AEM projekttyp. Lär dig hur du bygger och distribuerar projektet till en lokal utvecklingsmiljö med AEM som Cloud Service-SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
source-git-commit: 64221be65eb54e1edba7e0353bc290a5340063e7
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 4%

---

# Utveckla AEM för AEM som Cloud Service {#develop}

Utveckla AEM handelsprojekt som bygger på Commerce Integration Framework (CIF) för AEM som Cloud Service följer samma regler och bästa praxis som andra AEM på AEM. Granska dessa först:

- [AEM-projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Utvecklingsriktlinjer för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Lokal utveckling med AEM som Cloud Service-SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

En lokal utvecklingsmiljö rekommenderas för arbete med CIF-projekt. Det CIF-tillägg som anges för AEM som en Cloud Service är även tillgängligt för lokal utveckling. Den kan laddas ned från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF-tillägget tillhandahålls som ett arkiv för försäljningsfunktioner. ZIP-filen som finns på Software Distribution Portal innehåller två Sling Feature-arkivfiler, en för AEM och en för AEM publiceringsinstanser.

**Är du inte AEM som Cloud Service?** Ta en titt på  [en mer detaljerad guide till hur du konfigurerar en lokal utvecklingsmiljö med AEM som Cloud Service-SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### Nödvändig programvara

Följande bör installeras lokalt:

- [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)  (3.3.9 eller senare)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Åtkomst till CIF-tillägget

CIF-tillägget kan laddas ned som en zip-fil från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). ZIP-filen innehåller CIF-tillägget som **Sling Feature archive**, det är inte ett AEM. Observera att åtkomsten till SDK-listorna är begränsad till dem som har AEM som Cloud Service-licens.

>[!TIP]
>
>Se till att du alltid använder den senaste CIF-tilläggsversionen.

### Lokal installation

För lokal utveckling av CIF-tillägg med AEM som Cloud Service-SDK följer du stegen nedan:

1. Få de senaste AEM som Cloud Service SDK
1. Packa upp AEM .jar för att skapa mappen `crx-quickstart`, kör:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Skapa en `crx-quickstart/install`-mapp
1. Kopiera rätt fil för Sling Feature archive för CIF-tillägget till mappen `crx-quickstart/install`.

   ZIP-tilläggsfilen för CIF innehåller två Sling Feature archive `.far`-filer. Se till att använda rätt för AEM Author eller AEM Publish, beroende på hur du tänker köra den lokala AEM som en Cloud Service-SDK.

1. Skapa en lokal systemmiljövariabel med namnet `COMMERCE_ENDPOINT` som innehåller Magento GraphQL-slutpunkten.

   Exempel på Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourmagentosystem>/graphql
   ```

   Exempelfönster:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourmagentosystem>/graphql
   ```

   Den här variabeln används av AEM för att ansluta till ditt handelssystem. Dessutom innehåller CIF-tillägget en lokal omvänd proxy som gör Commerce GraphQL-slutpunkten tillgänglig lokalt. Detta används av CIF-redigeringsverktygen (produktkonsol och väljare) och för CIF-komponenter på klientsidan som gör direkta GraphQL-anrop.

   Den här variabeln måste även ställas in för AEM som en Cloud Service-miljö. Mer information om variabler finns i [Konfigurera OSGi för AEM som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. (Valfritt) Om du vill aktivera mellanlagrade katalogfunktioner måste du skapa en integreringstoken för din Magento-instans. Följ stegen på [Komma igång](./getting-started.md#staging) för att skapa token.

   Ange en OSGi-hemlighet med namnet `COMMERCE_AUTH_HEADER` till följande värde:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Mer information om hemligheter finns i [Konfigurera OSGi för AEM som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. Starta AEM som en Cloud Service-SDK

>[!NOTE]
>
>Se till att du AEM som Cloud Service-SDK i samma terminalfönster som systemvariabeln var inställd i steg 5. Om du startar programmet i ett separat terminalfönster eller dubbelklickar på .jar-filen kontrollerar du att systemvariabeln är synlig.

Verifiera konfigurationen via OSGI-konsolen: `http://localhost:4502/system/console/osgi-installer`. Listan ska innehålla CIF-tilläggsrelaterade paket, innehållspaket och OSGI-konfigurationer enligt definitionen i funktionsmodellfilen.

## Projektinställningar {#project}

Det finns två sätt att starta CIF-projekt för AEM som Cloud Service.

### Använd AEM projekttyp

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype) är huvudverktyget för att starta ett förkonfigurerat projekt för att komma igång med CIF. CIF Core Components och alla nödvändiga konfigurationer kan inkluderas i ett genererat projekt med ett extra alternativ.

>[!TIP]
>
>Använd [AEM Project Archetype 24 eller senare](https://github.com/adobe/aem-project-archetype/releases) för att generera projektet.

Se AEM Project Archetype [användningsinstruktioner](https://github.com/adobe/aem-project-archetype#usage) om hur du skapar ett AEM projekt. Om du vill inkludera CIF i projektet använder du alternativet `includeCommerce`.

Till exempel:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF Core Components kan användas i alla projekt, antingen genom att inkludera det medföljande `all`-paketet eller individuellt med CIF-innehållspaketet och relaterade OSGI-paket. Om du vill lägga till CIF-kärnkomponenter manuellt i ett projekt använder du följande beroenden:

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

### Använd AEM Venia Reference Store

Ett andra alternativ för att starta ett CIF-projekt är att klona och använda [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store är ett exempel på en butiksapplikation som demonstrerar användningen av CIF Core Components för AEM. Det är avsett som en uppsättning med metodtips och en potentiell utgångspunkt för att utveckla din egen funktionalitet.

För att komma igång med Venia Reference Store behöver du bara klona Git-databasen och börja anpassa projektet efter dina behov.

>[!NOTE]
>
>Projektet Venia Reference Store innehåller två byggprofiler för AEM som Cloud Service och AEM 6.5. Kontrollera [projektets readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) för att se hur de används.

## Ytterligare resurser

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
