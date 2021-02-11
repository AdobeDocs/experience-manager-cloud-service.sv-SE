---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
translation-type: tm+mt
source-git-commit: bca0519b3f27ee21df41b2292d19e330c4aa5f7d
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2021.1.0 är 3 februari 2021.
Följande version (2021.2.0) kommer att vara den 25 februari 2021.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service  {#sites}

### Headless Content Management {#headless}

* **[GraphQL API for Content Fragment Delivery](/help/assets/content-fragments/graphql-api-content-fragments.md)**: Möjlighet att söka efter innehållsfragment med GraphQL-syntax och scheman baserade på Content Fragment-modeller, för utdata i JSON-format.

* **[Autentiseringsstöd för GraphQL API-begäranden](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**: Möjlighet att autentisera GraphQL API-begäranden med åtkomsttoken för API:er på serversidan.

* **[RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)**: Stöd för visning och redigering av externa SPA i AEM.

* **[Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Lagt till möjlighet att ladda upp ett fristående enkelsidigt program till en AEM, lägga till redigerbara innehållsavsnitt och aktivera redigering.

* Förbättrade JSON-utdata från GraphQL API, inklusive möjligheten att skriva ut RTF i JSON-format och -språk.

* Stöd för att kapsla modeller för innehållsfragment så att kapslade strukturer för innehållsfragment kan skapas, via särskilda datatyper för Content Fragment Reference eller textbundna referenser för innehållsfragment i flerradiga textfält.

* Ytterligare valideringsregler finns i datatyperna Content Fragment model, inklusive&quot;unique&quot;,&quot;required&quot; och&quot;translatable&quot;.

* Märk upp Content Fragment-modeller och tillåt att Content Fragment kan skapas i en mapp med profiler utifrån taggar eller sökvägar.

* Användbarhetsförbättringar i redigeraren för innehållsfragment, inklusive publiceringsåtgärd och visning av modell som ett fragment baseras på.

* Möjlighet att förhandsgranska JSON-utdata direkt i Content Fragment-redigeraren.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

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

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.2.0 är 11 februari 2021.

### Nyheter {#what-is-new-cloud-manager}

* Produktionspipelinen för Cloud Manager kommer nu att innehålla testning av anpassade användargränssnitt.

* Resurskunder kan nu välja när och var de ska distribuera sin Brand Portal-instans på ett självbetjäningssätt via användargränssnittet i Cloud Manager. För ett vanligt (icke-sandlådeprogram) program med Assets-lösning kan Brand Portal nu etableras i produktionsmiljön. Etableringen kan bara göras en gång i produktionsmiljön.

* Den AEM Project Archetype som används i Project och Sandbox Creation har uppdaterats till version 25.

* Listan med föråldrade API:er som identifieras vid kodskanning har förfinats så att den innehåller ytterligare klasser och metoder som har tagits bort i den senaste SDK-versionen av Cloud Servicen.

* SonarQube-profilen för Cloud Manager har uppdaterats för att ta bort Sonar-regelbläckfisk:S2142. Detta kommer inte längre att orsaka en konflikt med kontrollerna för trådavbrott.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan lägga till/uppdatera domännamn för tillfället eftersom den associerade miljön antingen har en pågående pipeline kopplad till sig eller väntar på godkännandesteget.

* Egenskaper som angetts i kundens `pom.xml`-filer som har prefixats med sonar kommer nu att tas bort dynamiskt för att undvika problem med bygg- och kvalitetsskanning.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Det är inte längre skiftlägeskänsligt att matcha SSL-certifikat mot ett domännamn.

* Molnhanterarens användargränssnitt meddelar nu användaren om de privata certifikatnycklarna inte uppfyller 2048-bitarsgränsen med ett felmeddelande.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* I vissa fall kan ett internt problem leda till att miljön tas bort.

* En del pipeline-fel rapporterades felaktigt som pipeline-fel.

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
