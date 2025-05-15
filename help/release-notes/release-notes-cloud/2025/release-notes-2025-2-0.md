---
title: Versionsinformation om 2025.2.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2025.2.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: b893663d-35f1-43ae-a029-4c249b117f2d
source-git-commit: 7eabd6199467d4e42f6bf7914de0d7ba7a3f9733
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 0%

---

# Versionsinformation 2025.2.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2025.2.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.2.0) är 4 mars 2025. Nästa version (2025.3.0) är planerad till 27 mars 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten från februari 2025 om du vill se en sammanfattning av funktioner som lagts till i version 2025.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3458080?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i AEM Sites {#new-features-sites}

**Automatisk taggning för innehållsfragment**

När du skapar innehållsfragment kan du nu automatiskt ärva taggar som har tilldelats innehållsmodellen. Detta möjliggör kraftfull automatisk klassificering av innehåll som lagras i innehållsfragment.

**Stöd för UUID för innehållsfragment**

Stöd för Content Fragment UUID är nu GA. Den nya funktionen ändrar inte det banbaserade beteendet för åtgärder i AEM, till exempel move, rename, rollout, där banorna automatiskt justeras, men det kan göra det enklare och stabilare att använda externa innehållsfragment, särskilt när du använder GraphQL-frågor som direkt riktar in enskilda fragment med ByPath-frågor. Sådana frågor kan brytas om en fragmentsökväg ändras. När du använder den nya ById-frågetypen är frågan nu stabil eftersom UUID för ett fragment inte ändras i fall där sökvägar gör det.

**Dynamiska media med stöd för OpenAPI i Content Fragment Editor och GraphQL**

Assets som lagras i andra AEM as a Cloud Service-program än Content Fragments, och som aktiveras med nya Dynamic Media med OpenAPI-funktioner, kan nu användas i Content Fragments. Bildväljaren i den nya Content Fragment Editor tillåter nu att du väljer &quot;fjärrdatabaser&quot; som källa för bildresurser som ska refereras i fragmentet. När sådana innehållsfragment levereras med AEM GraphQL, innehåller JSON-svaret nu nödvändiga egenskaper för fjärrresurser (assetId, databaseId) så att klientapplikationer kan skapa respektive Dynamic Media med OpenAPI-URL:er för att hämta bilden.

**Utrullning av innehållsfragmentredigerare**

Vi fortsätter att aktivera den nya gränssnittsbaserade redigeraren för innehållsfragment i AEM as a Cloud Service. Efter att ha blivit standard för alla Cloud Service Developer-miljöer i november 2024 kommer den att anges som standard för alla scenmiljöer den 1 april 2025 och för alla produktionsmiljöer den 1 maj 2025. I samtliga fall har användarna fortfarande möjlighet att återgå till den traditionella redigeraren för innehållsfragment i AEM Touch-gränssnittet.

**Översättnings-HTTP API**

AEM Translation HTTP REST API som har varit i läget tidig adopter ett tag är nu GA. Dokumentationen finns [här.](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/translation/) API:t tillåter automatisering av nödvändiga steg i översättningshanteringsprocessen för innehåll i AEM.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i AEM Assets {#new-features-assets}

**Dynamic Media - ny paketeringsstruktur**

Nu finns en uppdaterad paketeringsstruktur för dynamiska media som bättre motsvarar marknadens förväntningar och ger support. Den nya förpackningsstrukturen omfattar

* Dynamic Media Prime, som innehåller Dynamic Media med OpenAPI:er och video för bättre leverans.

* Dynamic Media Ultimate har dessutom funktioner för leverans och omvandling för att klara tyngre användningsbehov.

Du måste ha Assets as a Cloud Service Prime eller Ultimate för att kunna dra nytta av den nya paketeringsstrukturen.

**AI-genererade videobeskrivningar**

AI-genererade videobildtexter i Adobe Dynamic Media använder artificiell intelligens för att automatiskt generera bildtexter för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter. Bildtexter genereras från det ursprungliga ljudet, eventuella ytterligare ljudspår eller extra bildtexter finns på fliken Bildtexter och ljud på videoegenskapssidan. Med stöd för över 60 språk kan bildtexter granskas och förhandsgranskas innan videon publiceras.

**Anpassa sökfilter**

Med anpassade sökfilter blir det enklare att hitta relevant information. Det gör det möjligt att göra mer skräddarsydda sökningar och filtrera data efter specifika attribut som märke, produkt, kategori eller andra nyckelidentifierare. Detta förbättrar organisationen, minskar tiden för att gå miste om irrelevanta resultat och möjliggör snabbare beslutsfattande. Det har också stöd för skalbarhet eftersom stora datauppsättningar blir enklare att navigera i och analysera.

![anpassa sökfilter](/help/assets/assets/custom-search-filters.png)

### Tidig åtkomst-funktioner i Content Hub {#early-access-content-hub}

I Content Hub kan du nu visa och hämta dynamiska och smarta beskärningsrenderingar utöver de befintliga statiska renderingarna. Som Content Hub-administratör kan du även konfigurera tillgängligheten för dessa återgivningar för användare med användargränssnittet för konfiguration.

![dynamiska återgivningar](/help/assets/assets/download-single-asset-renditions-dynamic.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### HTML e-postmallar i adaptiv Forms

Med adaptiv Forms kan du använda [HTML e-postmallar](/help/forms/html-email-templates-in-adaptive-forms.md). Med HTML e-postmallar kan du skicka snygga, personliga och visuellt tilltalande e-postmeddelanden när ett formulär skickas. Dessa e-postmeddelanden kan anpassas med formulärdata och förbättras med olika e-posttaggar, som bilder och länkar. Med Adaptive Forms kan du antingen ladda upp en fil som innehåller en HTML-mall eller använda en vanlig textredigerare för att skapa mallarna.

![HTML e-postmallar](/help/forms/assets/html-email.png)

#### Förbättrat molnlagringsstöd: Direktöverföring av PDF till Azure Blob Storage

AEM Forms API:er för dokumentgenerering gör nu att du kan [överföra genererade PDF-dokument](/help/forms/early-access-ea-features.md#doc-generation-api) direkt till Azure Blob Storage. Den här förbättringen effektiviserar lagring och hämtning, vilket förbättrar effektiviteten och integreringen med molnarbetsflöden.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Stöd för Java 21 {#java21}

Som nämndes i versionsinformationen för januari kan du nu skapa kod med Java 21, som innehåller nya funktioner (t.ex. mönstermatchning för switch-satser, fasta klasser) och prestandaförbättringar. Java 17-byggen stöds också nyligen. Konfigurationssteg, inklusive uppdatering av projekt- och biblioteksversioner för Maven, finns i artikeln [Byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Den mer prestandaanpassade Java 21 **runtime** distribueras automatiskt när en Java 17- eller 21-version upptäcks. Vi rekommenderar dock att du går med i Java 21-miljön för miljöer som byggts med Java 11 genom att skicka ett e-postmeddelande till [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Läs mer om [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> I februari distribuerades Java 21 **runtime** till dev-/RDE-miljöer (utöver de som redan byggts med Java 17 eller 21, som redan har Java 21-runtime). Java 21 kommer att användas i scen-/produktionsmiljöer i april.

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

Lär dig mer om [OpenAPI-baserade AEM API:er](/help/implementing/developing/open-api-based-apis.md) och prova en [heltäckande självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) som visar konfiguration och användning.

De API-slutpunkter som anges nedan är tillgängliga som en del av ett program för tidig användning. Om du är intresserad kan du skicka ett e-postmeddelande till [aem-apis@adobe.com](mailto:aem-apis@adobe.com) med en beskrivning av hur du tänker använda dem.

* [API:er för innehållsfragment för webbplatser](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Webbplatser och API:er för Assets-mappar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Nya AEM Developer Console (Public Beta) {#aem-developer-console-beta}

Prova en omgjord [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) som erbjuder en mer interaktiv upplevelse för felsökning av kod i molnmiljöer.

Vem som helst kan komma åt den offentliga betaversionen genom att klicka på knappen *Ny konsol tillgänglig* i den aktuella AEM Developer Console. Adobe tar gärna emot feedback, som du kan skicka med e-post till [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Universal Editor {#universal-editor}

Du hittar en fullständig lista över universella redigeringsversioner [här](/help/release-notes/universal-editor/current.md).

## Generera variationer {#generate-variations}

Du hittar en fullständig lista över versioner av Generera variationer [här](/help/generative-ai/release-notes-generate-variations.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/en/docs/release-notes/experience-cloud/current).
