---
title: Utveckla AEM för AEM som Cloud Service
description: Lär dig hur du skapar ett e-handelsaktiverat AEM med AEM projekttyp. Lär dig hur du bygger och distribuerar projektet till en lokal utvecklingsmiljö med AEM som Cloud Service-SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 7%

---


# Utveckla AEM för AEM som Cloud Service {#develop}

Utveckla AEM handelsprojekt som bygger på Commerce Integration Framework (CIF) för AEM som Cloud Service följer samma regler och bästa praxis som andra AEM på AEM. Granska dessa först:

- [AEM-projektstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Utvecklingsriktlinjer för AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Lokal utveckling med AEM som Cloud Service-SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

En lokal utvecklingsmiljö rekommenderas för arbete med CIF-projekt. CIF-tillägget för AEM som en Cloud Service-miljö är även tillgängligt för lokal utveckling. Den kan laddas ned från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF-tillägget tillhandahålls som ett arkiv för försäljningsfunktioner. ZIP-filen som finns på Software Distribution Portal innehåller två Sling Feature-arkivfiler, en för AEM och en för AEM publiceringsinstanser.

**Är du inte AEM som Cloud Service?** Ta en titt på [en mer detaljerad guide till hur du konfigurerar en lokal utvecklingsmiljö med AEM som Cloud Service-SDK](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### Nödvändig programvara

Följande bör installeras lokalt:

- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Åtkomst till CIF-tillägget

The CIF add-on can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). ZIP-filen innehåller CIF-tillägget som arkiv för **Sling-funktioner**, det är inte ett AEM. Observera att åtkomsten till SDK-listorna är begränsad till dem som har AEM som Cloud Service-licens.

>[!TIP]
>
>Se till att du alltid använder den senaste CIF-tilläggsversionen.

### Lokal installation

För lokal utveckling av CIF-tillägg med AEM som Cloud Service-SDK följer du stegen nedan:

1. Få de senaste AEM som Cloud Service SDK
2. Packa upp AEM .jar och skapa `crx-quickstart` mappen. Kör:

   ```bash
   java -jar <jar name> -unpack
   ```

3. Skapa en `crx-quickstart/install` mapp
4. Kopiera rätt fil för Sling Feature archive för CIF-tillägget till `crx-quickstart/install` mappen.

   ZIP-tilläggsfilen CIF innehåller två Sling Feature Archive- `.far` filer. Se till att använda rätt för AEM Author eller AEM Publish, beroende på hur du tänker köra den lokala AEM som en Cloud Service-SDK.

5. Skapa en lokal systemmiljövariabel med namnet `COMMERCE_ENDPOINT` som innehåller Magento GraphQL-slutpunkten.

   Exempel på Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Exempelfönster:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Den här variabeln måste även ställas in för AEM som en Cloud Service-miljö.

6. Starta AEM som en Cloud Service-SDK

7. Starta den lokala GraphQL-proxyservern

   Om du vill göra Magento GraphQL-slutpunkten tillgänglig lokalt för CIF-tillägget och CIF-komponenterna använder du följande kommando. GraphQL-slutpunkten är sedan tillgänglig på `http://localhost:3002/graphql`.
Exempel på Mac OSX:

   ```bash
   npx local-cors-proxy --proxyUrl https://demo.magentosite.cloud --port 3002 --proxyPartial ''
   ```

   Exempelfönster:

   ```bash
   npx local-cors-proxy --proxyUrl https://demo.magentosite.cloud --port 3002 --proxyPartial '""'
   ```
   Argumentet `--proxyPartial` måste ta emot en tom sträng.

   Du kan testa den lokala GraphQL-proxyn genom att peka på ett GraphQL-frågeverktyg för att `http://localhost:3002/graphql` testa några frågor.

8. Logga in på AEM SDK och konfigurera CIF så att den lokala GraphQL-proxyservern används

   Navigera till CIF-Cloud Servicens konfiguration (Verktyg > Cloud Services > CIF-konfiguration). Öppna egenskapsvyn för den konfiguration som används av ditt projekt.

   Använd den lokala proxyserverslutpunkten för egenskapen `GraphQL Proxy Path` för `http://localhost:3002/graphql`egenskapen. Spara konfigurationen.

>[!NOTE]
>
>Skjut inte in konfigurationen för steg 8 i projektrapporten. Den här konfigurationen krävs bara för en lokal utvecklingsinställning. AEM som en Cloud Service-miljö har redan konfigurerats med GraphQL-proxyn under introduktionen.

Verifiera konfigurationen via OSGI-konsolen:`http://localhost:4502/system/console/osgi-installer`. Listan ska innehålla CIF-tilläggsrelaterade paket, innehållspaket och OSGI-konfigurationer enligt definitionen i funktionsmodellfilen.

## Projektinställningar {#project}

Det finns två sätt att starta CIF-projekt för AEM som Cloud Service.

### Använd AEM projekttyp

Den [AEM projekttypen](https://github.com/adobe/aem-project-archetype) är det viktigaste verktyget för att starta ett förkonfigurerat projekt för att komma igång med CIF. CIF Core Components och alla nödvändiga konfigurationer kan inkluderas i ett genererat projekt med ett extra alternativ.

>[!TIP]
>
>Använd [AEM Project Archetype 24 eller senare](https://github.com/adobe/aem-project-archetype/releases) för att generera projektet.

Se AEM [användningsinstruktioner](https://github.com/adobe/aem-project-archetype#usage) för Project Archetype om hur du skapar ett AEM projekt. Om du vill inkludera CIF i projektet använder du `includeCommerce` alternativet.

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

CIF Core Components kan användas i alla projekt, antingen genom att inkludera det medföljande `all` paketet eller individuellt med CIF-innehållspaketet och tillhörande OSGI-buntar. Om du vill lägga till CIF-kärnkomponenter manuellt i ett projekt använder du följande beroenden:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
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

Ett annat alternativ för att starta ett CIF-projekt är att klona och använda [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store är ett exempel på en butiksapplikation som demonstrerar användningen av CIF Core Components för AEM. Det är avsett som en uppsättning med bästa praxis och som en potentiell startpunkt för att utveckla din egen funktionalitet.

För att komma igång med Venia Reference Store behöver du bara klona Git-databasen och börja anpassa projektet efter dina behov.

>[!NOTE]
>
>Projektet Venia Reference Store innehåller två byggprofiler för AEM som Cloud Service och AEM 6.5. Kontrollera [projektet readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) för att se hur de används.

## Ytterligare resurser

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
