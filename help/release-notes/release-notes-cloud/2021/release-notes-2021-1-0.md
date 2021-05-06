---
title: Versionsinformation för 2021.1.0-utgåvan av [!DNL Adobe Experience Manager] som en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service Release Notes for 2021.1.0.'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
translation-type: tm+mt
source-git-commit: b842f70bd53676d23229e24edb4a957ff7613824
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2021.1.0 är 3 februari 2021.
Följande version (2021.2.0) kommer att vara den 25 februari 2021.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service  {#sites}

* **[HTTP-API](/help/assets/content-fragments/assets-api-content-fragments.md)** för innehållsfragment: Lägg till/uppdatera och ta bort Content Fragment-varianter med HTTP API.

* **[GraphQL API for Content Fragment Delivery](/help/assets/content-fragments/graphql-api-content-fragments.md)**: Möjlighet att söka efter innehållsfragment med GraphQL-syntax och scheman baserade på Content Fragment-modeller, för utdata i JSON-format.

* **[Autentiseringsstöd för GraphQL API-begäranden](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**: Möjlighet att autentisera GraphQL API-begäranden med åtkomsttoken för API:er på serversidan.

* Förbättrade JSON-utdata från GraphQL API, inklusive möjligheten att skriva ut RTF i JSON-format och -språk.

* Stöd för att kapsla modeller för innehållsfragment så att kapslade strukturer för innehållsfragment kan skapas, via särskilda datatyper för Content Fragment Reference eller textbundna referenser för innehållsfragment i flerradiga textfält.

* Ytterligare valideringsregler finns i datatyperna Content Fragment model, inklusive&quot;unique&quot;,&quot;required&quot; och&quot;translatable&quot;.

* Märk upp Content Fragment-modeller och tillåt att Content Fragment kan skapas i en mapp med profiler utifrån taggar eller sökvägar.

* Användbarhetsförbättringar i redigeraren för innehållsfragment, inklusive publiceringsåtgärd och visning av modell som ett fragment baseras på.

* Möjlighet att förhandsgranska JSON-utdata direkt i Content Fragment-redigeraren.


## [!DNL Adobe Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] som  [!DNL Cloud Service] utökar funktionerna för smarta taggar så att de kan identifiera nyckelord och enheter i textbaserade resurser. Texten identifieras, indexeras och görs tillgänglig som metadata för att förbättra sökupplevelsen utan att någon konfiguration behövs. Se [Smarta taggar](/help/assets/smart-tags.md).

* MXF-filformat stöds nu. Se [Filformat som stöds](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce som Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Product Experience Management: Ny egenskapsflik för Commerce för Assets och Experience Fragments. På den här fliken kan du länka produkter/kategorier till Assets och Experience Fragments. På fliken visas även realtidsdata för länkade produkter/kategorier och en länk som visar information i produktkonsolen.

* Lanserade CIF Venia Reference Site - 2021.02.02 som innehåller den senaste CIF Core Components version v1.7.0. Mer information finns i [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02).

* Frisläppta CIF-kärnkomponenter v1.7.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0).

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.1.0 är 14 januari 2021.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Resursinstansen Production kan vid olika tillfällen visa status för varumärkesportalen på **miljöinformationssidan** som *Väntande* utan att tillåta användaren att vidta några åtgärder.

* När en avaktivering från molnhanteraren utlöstes visades ibland ett felmeddelande även när avviloläget startades.

* Sällsynta fall av fel som uppstått när miljön skapades eller togs bort har åtgärdats.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller felkorrigeringar för AEM Dispatcher Converter och Repository Modernizer och har även stöd för ett nytt verktyg - Index Converter. Läs [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) om du vill veta mer om det här plugin-programmet.

* Indexkonverteraren är ett verktyg som kan användas för att omvandla en kunds anpassade OAK-indexdefinitioner till AEM som en Cloud Service-kompatibel OAK-indexdefinitioner. Mer information finns i [Indexkonverteraren](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Ny funktion har lagts till i [Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) som skapar ett separat paket `ui.config` som innehåller alla OSGi-konfigurationer.

### Felkorrigeringar {#crt-bug-fixes}

* Flera felkorrigeringar har gjorts i verktygen AEM Dispatcher Converter och Repository Modernizer. Se [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) och [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEM som en Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### Nyheter {#what-is-new-foundation}

* Autentiserade API-anrop från server till server - Generera lämpliga åtkomsttoken för att göra autentiserade server-till-server-API-anrop mellan externa program och AEM som en Cloud Service-miljö. Läs mer genom att läsa [dokumentationen](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) eller genom att läsa igenom självstudiekursen[a3/>.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)

### SDK Build Analyzers {#sdk-build-analyzers}

AEM som Cloud Service SDK Build Analyzer Maven Plugin identifierar problem i ett maven-projekt, inklusive saknade beroenden. Det ger utvecklare möjlighet att upptäcka problem under den lokala utvecklingen, långt före distributionen till molnmiljöer med Cloud Manager.

Två nya analytiker har lagts till för den här versionen:

* repoinit analyzer
* bundle-nativecode

Mer information finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Verktyg för övergång till molnet{#code-transition-tools}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.2.2 är 1 februari 2021.

### Nyheter i [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Ny funktion och nytt användargränssnitt har lagts till i verktyget Innehållsöverföring - verktyget för användarmappning. Den här funktionen mappar automatiskt befintliga användare och grupper till deras Adobe Identity Management-system-ID som en del av innehållsmigreringsaktiviteten. Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).
* Verktyget Innehållsöverföring migrerar nu alla grupper och användare som det hänvisas till i migreringsuppsättningen, inklusive underordnade.
* Användarna kan välja vissa sökvägar under `/etc` när de skapar migreringsuppsättningar.
