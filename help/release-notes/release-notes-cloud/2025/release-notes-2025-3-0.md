---
title: Versionsinformation om 2025.3.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2025.3.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: b1a551aeebd0b3c5cf8111bf30341bd4ac41536f
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Versionsinformation 2025.3.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2025.3.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.3.0) är 27 mars 2025. Nästa funktionsversion (2025.4.0) är planerad till 24 april 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440924?quality=12&captions=swe)

-->

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i Dynamic Media {#new-features-dynamic-media}

**Stöd för långa formulär för videor som levereras med Dynamic Media med Open API**

Dynamic Media med OpenAPI har nu stöd för videor med långa format. Videor med långa format kan hantera upp till 50 GB och 2 timmar.

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

Fliken Bandbredd i Dynamic Media Classic rapportkontrollpanel stöds inte längre från och med april 2025.

Se [Bandbredd och lagring, rapporttyper](https://experienceleague.adobe.com/sv/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


## Nya funktioner i vyn Assets {#new-features-assets-view}


**Stöd för rottaggar**

AEM Assets har nu stöd för att mappa en taggegenskap i ett metadataformulär till anpassade metadata. Som administratör kan du dessutom begränsa tillgängligheten för taggar till användare genom att begränsa åtkomsten till en viss rottagg och de taggar som finns under rottaggen.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### HTML e-postmallar i adaptiv Forms

Med adaptiv Forms kan du använda [HTML e-postmallar](/help/forms/html-email-templates-in-adaptive-forms.md). Med HTML e-postmallar kan du skicka snygga, personliga och visuellt tilltalande e-postmeddelanden när ett formulär skickas. Dessa e-postmeddelanden kan anpassas med formulärdata och förbättras med olika e-posttaggar, som bilder och länkar. Med Adaptive Forms kan du antingen ladda upp en fil som innehåller en HTML-mall eller använda en vanlig textredigerare för att skapa mallarna.

![HTML e-postmallar](/help/forms/assets/html-email.png)

#### Förbättrat molnlagringsstöd: Direktöverföring av PDF till Azure Blob Storage

Med API:er för AEM Forms-dokumentgenerering kan du nu [överföra genererade PDF-dokument](/help/forms/early-access-ea-features.md#doc-generation-api) direkt till Azure Blob Storage. Den här förbättringen effektiviserar lagring och hämtning, vilket förbättrar effektiviteten och integreringen med molnarbetsflöden.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Stöd för Java 21 {#java21}

Från och med januariversionen kan du skapa kod med Java 21 och Java 17. Du får tillgång till nya funktioner som mönstermatchning, fasta klasser och olika prestandaförbättringar. Konfigurationssteg, inklusive uppdatering av projekt- och biblioteksversioner för Maven, finns i artikeln [Byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Den mer prestandaanpassade Java 21 **runtime** distribueras automatiskt när en Java 17- eller 21-version upptäcks. Adobe rekommenderar dock att du går med i Java 21-miljön för miljöer som byggts med Java 11 genom att skicka ett e-postmeddelande till [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Läs mer om [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Java 21 **runtime** distribuerades till dina dev/RDE-miljöer i februari. Den kommer att användas i dina scen-/produktionsmiljöer den 28 och 29 april **.** Observera att **byggkoden** med Java 21 (eller Java 17) är oberoende av Java 21-miljön - du måste vidta åtgärder explicit för att skapa kod med Java 21 (eller Java 17).

### AEM Log-Forwarding till fler destinationer - Beta Program {#log-forwarding-earlyadopter}

I betaversionen kan du nu vidarebefordra AEM-loggar till New Relic (med HTTPS), Amazon S3 och Sumo Logic. Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds, men inte CDN-loggar. E-post [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för åtkomst.

Medan loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har redan stöd för (GA) AEM- och CDN-loggvidarebefordran till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. Den här funktionen är konfigurerad på ett självbetjäningssätt och distribueras med Config Pipeline.

Läs mer i [dokumentationen för vidarebefordran av loggfiler](/help/implementing/developing/introduction/log-forwarding.md).

### Edge Computing - Request for Feedback! {#edge-computing-feedback}

Edge datoranvändning för databearbetning närmare webbläsaren, vilket har bl.a. kortare svarstider. Adobe vill gärna veta om du tycker att den här tekniken är användbar för AEM Publish Delivery och Edge Delivery Services. Dessutom kan du tala om för oss vad du tänkt dig när du använder den som indata i produktfärdplanen.

Några möjliga användningsexempel:

* Autentisering med en IdP för att ge åtkomst till innehåll
* Återge dynamiskt (personaliserat, lokaliserat) innehåll baserat på geopositionering, enhetstyp, användarattribut osv.
* Avancerad bildbehandling
* Mittprogram mellan CDN och ett ursprung
* Ett lager mellan webbläsaren och ett tredjeparts-API, kanske för att formatera om API-svaret
* Samla in data från flera källor för att göra det enklare för klientwebbläsaren att återge dem

Mejla [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med frågor och kommentarer!

### OpenAPI-baserade API:er - tidigt Adobe-program {#open-apis-earlyadopter}

Utvecklare kan integrera AEM som Cloud Service-funktioner i sina egna program och verktyg. Nya AEM as a Cloud Service-API:er följer OpenAPI-specifikationen och har som mål att vara konsekventa, väldokumenterade och användarvänliga. Autentiseringsuppgifter för slutpunkter som kräver autentisering genereras genom att Adobe Developer Console-projekt skapas.

Lär dig mer om [OpenAPI-baserade AEM API:er](/help/implementing/developing/open-api-based-apis.md) och prova en [heltäckande självstudiekurs](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) som visar konfiguration och användning.

De API-slutpunkter som anges nedan är tillgängliga som en del av ett program för tidig användning. Om du är intresserad kan du skicka ett e-postmeddelande till [aem-apis@adobe.com](mailto:aem-apis@adobe.com) med en beskrivning av hur du tänker använda dem.

* [API:er för innehållsfragment för webbplatser](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Webbplatser och API:er för Assets-mappar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Nya AEM Developer Console (Public Beta) {#aem-developer-console-beta}

Prova en omgjord [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) som erbjuder en mer interaktiv upplevelse för felsökning av kod i molnmiljöer.

Vem som helst kan komma åt den offentliga betaversionen genom att klicka på knappen *Ny konsol tillgänglig* i den aktuella AEM Developer Console. Adobe tar gärna emot feedback, som du kan skicka med e-post till [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/sv/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2025-releases/2502-release/whats-new-2025-02-0).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Universal Editor {#universal-editor}

Du hittar en fullständig lista över universella redigeringsversioner [här](/help/release-notes/universal-editor/current.md).

## Generera variationer {#generate-variations}

Du hittar en fullständig lista över versioner av Generera variationer [här](/help/generative-ai/release-notes-generate-variations.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/sv/docs/release-notes/experience-cloud/current).
