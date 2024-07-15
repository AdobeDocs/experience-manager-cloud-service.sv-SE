---
title: Utveckla AEM Commerce för AEM as a Cloud Service
description: Lär dig hur du skapar ett e-handelsaktiverat AEM med AEM projekttyp. Lär dig hur du bygger och distribuerar projektet till en lokal utvecklingsmiljö med AEM as a Cloud Service SDK.
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

Utveckla AEM Commerce-projekt, som baseras på Commerce integration framework (CIF) för AEM as a Cloud Service, följer samma regler och bästa praxis som andra AEM projekt på AEM as a Cloud Service. Granska följande först:

- [AEM-projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)
- [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Utvecklingsriktlinjer för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)

## Lokal utveckling med AEM as a Cloud Service SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

En lokal utvecklingsmiljö rekommenderas för CIF. CIF Add-On för AEM as a Cloud Service finns även för lokal utveckling. Den kan hämtas från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF Add-On finns som arkiv för Sling Feature. ZIP-filen som finns på Software Distribution Portal innehåller två Sling Feature-arkivfiler, en för AEM och en för AEM.

**Ny på AEM as a Cloud Service?** [En mer detaljerad guide till hur du konfigurerar en lokal utvecklingsmiljö med AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### Nödvändig programvara

Följande bör installeras lokalt:

- [SDK för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Åtkomst till CIF

Det CIF tillägget kan laddas ned som en zip-fil från [programdistributionsportalen](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). ZIP-filen innehåller CIF som **Sling Feature Archive**, det är inte ett AEM. SDK-listor är tillgängliga med en AEM as a Cloud Service-licens.

>[!TIP]
>
>Se till att du alltid använder den senaste CIF Add-On-versionen.

### Lokal installation

För lokal CIF med hjälp av AEM as a Cloud Service SDK:

1. Skaffa senaste AEM as a Cloud Service SDK
1. Packa upp AEM .jar så att du kan skapa mappen `crx-quickstart`, kör:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Skapa en `crx-quickstart/install`-mapp
1. Kopiera rätt fil för Sling Feature Archive för CIF i mappen `crx-quickstart/install`.

   Den CIF ZIP-tilläggsfilen innehåller två Sling Feature Archive `.far`-filer. Se till att du använder rätt för AEM författare eller AEM Publish, beroende på hur du tänker köra det lokala AEM as a Cloud Service SDK.

1. Skapa en lokal systemmiljövariabel med namnet `COMMERCE_ENDPOINT` som innehåller slutpunkten för Adobe Commerce GraphQL.

   Exempel på macOS X:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Exempelfönster:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Den här variabeln används av AEM för att ansluta till ditt handelssystem. Tillägget CIF innehåller också en lokal omvänd proxy som gör slutpunkten för Commerce GraphQL tillgänglig lokalt. Den här proxyn används av CIF (produktkonsol och väljare) och för de komponenter på klientsidan som utför direkta GraphQL-anrop CIF.

   Den här variabeln måste även ställas in för AEM as a Cloud Service-miljön. Mer information om variabler finns i [Konfigurera OSGi för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. (Valfritt) Om du vill aktivera funktioner för mellanlagrade kataloger måste du skapa en integreringstoken för din Adobe Commerce-instans. Skapa token genom att följa stegen på [Komma igång](./getting-started.md#staging).

   Ange en OSGi-hemlighet med namnet `COMMERCE_AUTH_HEADER` till följande värde:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Mer information om hemligheter finns i [Konfigurera OSGi för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. Starta AEM as a Cloud Service SDK

>[!NOTE]
>
>Se till att du startar AEM as a Cloud Service SDK i samma terminalfönster som systemvariabeln var inställd i steg 5. Om du startar det i ett separat terminalfönster, eller om du dubbelklickar på .jar-filen, kontrollerar du att systemvariabeln är synlig.

Verifiera konfigurationen via OSGI-konsolen: `http://localhost:4502/system/console/osgi-installer`. Listan ska innehålla de CIF tilläggspaketen, innehållspaketet och OSGI-konfigurationer som definieras i funktionsmodellfilen.

## Projektinställningar {#project}

Det finns två sätt att göra ditt CIF till AEM as a Cloud Service.

### Använd AEM projekttyp

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype) är huvudverktyget för ett förkonfigurerat projekt som du kan komma igång med CIF i Bootstrap. CIF kärnkomponenter och alla nödvändiga konfigurationer kan inkluderas i ett genererat projekt med ytterligare ett alternativ.

>[!TIP]
>
>Använd alltid den senaste versionen av [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/releases) så att du kan generera projektet.

Se AEM [användningsinstruktioner](https://github.com/adobe/aem-project-archetype#usage) om hur du genererar ett AEM projekt. Använd alternativet `includeCommerce` om du vill inkludera CIF i projektet.

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

CIF kärnkomponenter kan användas i alla projekt, antingen genom att inkludera det angivna `all`-paketet eller individuellt med det CIF innehållspaketet och relaterade OSGI-paket. Använd följande beroenden om du vill lägga till CIF kärnkomponenter manuellt i ett projekt:

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

Ett andra alternativ för att starta ett CIF projekt är att klona och använda [AEM Venedig Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store är ett exempel på referensarkivprogram som demonstrerar användningen av CIF Core Components for AEM. Det är avsett som en uppsättning med metodtips och en potentiell utgångspunkt för att utveckla din egen funktionalitet.

Börja med att klona Git-databasen och börja anpassa projektet efter dina behov.

>[!NOTE]
>
>Projektet Venia Reference Store innehåller två byggprofiler för AEM as a Cloud Service och AEM 6.5. Kontrollera [Viktigt om projekt.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) så att du kan se hur de används.

## Ytterligare resurser

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia)
- [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
