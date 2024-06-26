---
title: Utveckla AEM Commerce för AEM as a Cloud Service
description: Lär dig hur du skapar ett e-handelsaktiverat AEM med AEM projekttyp. Lär dig hur du skapar och distribuerar projektet till en lokal utvecklingsmiljö med AEM as a Cloud Service SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 2%

---

# Utveckla AEM Commerce för AEM as a Cloud Service {#develop}

Utveckla AEM Commerce-projekt, som bygger på Commerce integration framework (CIF) för AEM as a Cloud Service, följer samma regler och bästa praxis som andra AEM projekt på AEM as a Cloud Service. Granska följande först:

- [AEM-projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)
- [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Utvecklingsriktlinjer för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)

## Lokal utveckling med AEM as a Cloud Service SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

En lokal utvecklingsmiljö rekommenderas för CIF. CIF Add-On för AEM as a Cloud Service är också tillgänglig för lokal utveckling. Den kan laddas ned från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF Add-On finns som arkiv för Sling Feature. ZIP-filen som finns på Software Distribution Portal innehåller två Sling Feature-arkivfiler, en för AEM och en för AEM.

**Är du inte AEM as a Cloud Service?** Checka ut [en mer detaljerad guide till hur du konfigurerar en lokal utvecklingsmiljö med AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### Nödvändig programvara

Följande bör installeras lokalt:

- [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Åtkomst till CIF

Tillägget CIF kan laddas ned som en zip-fil från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). ZIP-filen innehåller CIF som **Arkiv med försäljningsfunktioner**, det är inte ett AEM paket. SDK-listor är tillgängliga med en AEM as a Cloud Service licens.

>[!TIP]
>
>Se till att du alltid använder den senaste CIF Add-On-versionen.

### Lokal installation

För lokal CIF-tilläggsutveckling med AEM as a Cloud Service SDK:

1. Hämta den senaste AEM as a Cloud Service SDK
1. Packa upp AEM .jar så att du kan skapa `crx-quickstart` mapp, kör:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Skapa en `crx-quickstart/install` mapp
1. Kopiera rätt fil för Sling Feature archive för CIF i `crx-quickstart/install` mapp.

   Den CIF ZIP-tilläggsfilen innehåller två Sling Feature-arkiv `.far` filer. Se till att du använder rätt för AEM författare eller AEM publicering, beroende på hur du tänker köra den lokala AEM as a Cloud Service SDK:n.

1. Skapa en lokal systemmiljövariabel med namnet `COMMERCE_ENDPOINT` håller slutpunkten för Adobe Commerce GraphQL.

   Exempel på macOS X:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Exempelfönster:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Den här variabeln används av AEM för att ansluta till ditt handelssystem. Tillägget CIF innehåller också en lokal omvänd proxy som gör slutpunkten för Commerce GraphQL tillgänglig lokalt. Den här proxyn används av CIF (produktkonsol och väljare) och för de komponenter på klientsidan som utför direkta GraphQL-anrop CIF.

   Den här variabeln måste även ställas in för den AEM as a Cloud Service miljön. Mer information om variabler finns i [Konfigurera OSGi för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. (Valfritt) Om du vill aktivera funktioner för mellanlagrade kataloger måste du skapa en integreringstoken för din Adobe Commerce-instans. Följ stegen på [Komma igång](./getting-started.md#staging) för att skapa token.

   Ange en OSGi-hemlighet med namnet `COMMERCE_AUTH_HEADER` till följande värde:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Mer information om hemligheter finns i [Konfigurera OSGi för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. Starta AEM as a Cloud Service SDK

>[!NOTE]
>
>Se till att du startar AEM as a Cloud Service SDK i samma terminalfönster som systemvariabeln var inställd i steg 5. Om du startar det i ett separat terminalfönster, eller om du dubbelklickar på .jar-filen, kontrollerar du att systemvariabeln är synlig.

Verifiera konfigurationen via OSGI-konsolen: `http://localhost:4502/system/console/osgi-installer`. Listan ska innehålla de CIF tilläggspaketen, innehållspaketet och OSGI-konfigurationer som definieras i funktionsmodellfilen.

## Projektinställningar {#project}

Det finns två sätt att göra ditt CIF as a Cloud Service AEM Bootstrap.

### Använd AEM projekttyp

The [AEM Project Archettype](https://github.com/adobe/aem-project-archetype) är huvudverktyget för ett förkonfigurerat projekt för att komma igång med CIF Bootstrap. CIF kärnkomponenter och alla nödvändiga konfigurationer kan inkluderas i ett genererat projekt med ytterligare ett alternativ.

>[!TIP]
>
>Använd alltid den senaste versionen av [AEM Project Archettype](https://github.com/adobe/aem-project-archetype/releases) så att du kan generera projektet.

Se AEM Project Archetype [användningsinstruktioner](https://github.com/adobe/aem-project-archetype#usage) om hur du skapar ett AEM projekt. Om du vill inkludera CIF i projektet använder du `includeCommerce` alternativ.

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

CIF kärnkomponenter kan användas i alla projekt, antingen med de medföljande `all` paketera eller individuellt med hjälp av CIF och tillhörande OSGI-paket. Använd följande beroenden om du vill lägga till CIF kärnkomponenter manuellt i ett projekt:

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

Ett andra alternativ för att starta ett CIF är att klona och använda [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store är ett exempel på referensarkivprogram som demonstrerar användningen av CIF Core Components for AEM. Det är avsett som en uppsättning med metodtips och en potentiell utgångspunkt för att utveckla din egen funktionalitet.

Börja med att klona Git-databasen och börja anpassa projektet efter dina behov.

>[!NOTE]
>
>Projektet Venia Reference Store innehåller två byggprofiler för AEM as a Cloud Service och AEM 6.5. Kontrollera [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) så att du kan se hur de används.

## Ytterligare resurser

- [AEM Project Archettype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
