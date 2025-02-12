---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: cdf1a62ca7c8d25b146cb7b6c1329f064e42df56
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.1.0) är 30 januari 2025. Nästa funktionsversion (2025.2.0) är planerad till den 27 februari 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

**Kommentarer för innehållsfragmentredigeraren är nu allmänt tillgängliga**

Samarbeta enkelt med kollegor när du skapar AEM Content Fragments med den nya och moderniserade kommentarstjänsten i AEM Content Fragment Editor.
[Läs mer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment).

**Innehållsfragmentsredigeraren och administratörens användargränssnitt, uppdaterat stöd för AEM as a Cloud Service-versioner**

Den lägsta AEM as a Cloud Service-version som stöds för nya användargränssnitt för Content Fragment Admin och Editor är nu 2023.8.13099. Tidigare versioner från före den allmänna tillgänglighetsversionen av de nya användargränssnitten stöds inte längre

### Tidiga Adobe-program {#sites-early-adopter}

**Förbättrade innehållsfragment**

Förbättrad referens för [innehållsfragment med unika ID-baserade referenser](/help/headless/graphql-api/uuid-reference-upgrade.md), vilket gör att GraphQL-frågor för enskilda innehållsfragment kan förbli stabila även om fragmentet har flyttats till en annan plats. Detta är nu möjligt med ByID-frågor. Banor kan ändras och kan eventuellt bryta ByPath-frågor, men UUID:n är stabila. De nya ID:n kan också returneras som egenskaper i frågor eller andra tillämpliga API-begäranden. Aktuell begränsning (2025.1): Sidreferenser stöds ännu inte med unika ID:n. Om det finns referenser till sidor i innehållsfragment bör den här funktionen inte användas. Begränsningen planeras att tas bort i nästa version av AEM as a Cloud Service.

**AEM REST OpenAPI för leverans av innehållsfragment**

[AEM REST OpenAPI för leverans av innehållsfragment](/help/headless/aem-rest-openapi-content-fragment-delivery.md) är nu tillgängligt för AEM as a Cloud Service.

### Föråldrade funktioner {#sites-deprecated}

#### SPA Editor {#spa-editor}

[SPA-redigeraren](/help/implementing/developing/hybrid/introduction.md) har tagits bort för nya projekt från och med version 2025.1.0. SPA-redigeraren stöds fortfarande för befintliga projekt, men bör inte användas för nya projekt.

De redigerare som rekommenderas för hantering av headless-innehåll i AEM är nu:

* [Den universella redigeraren](/help/edge/wysiwyg-authoring/authoring.md) för visuell redigering.
* [Innehållsfragmentsredigeraren](/help/assets/content-fragments/content-fragments-managing.md) för formulärbaserad redigering.

#### PWA Features {#pwa-features}

[Funktionerna för det progressiva webbprogrammet (PWA) ](/help/sites-cloud/authoring/sites-console/enable-pwa.md) för AEM Sites är föråldrade för nya projekt från och med version 2025.1.0. Den här funktionen stöds fortfarande för befintliga projekt, men bör inte användas för nya projekt

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i AEM Assets {#new-features-assets}

**Dynamiska mediamallar**

Anpassa bild- och textbanners direkt med en lättanvänd WYSIWYG Dynamic Media Template Editor, genom att bädda in webbadressen i valfritt program från första eller tredje part, för att skapa engagerande upplevelser med uppdateringar av bannerinnehåll i realtid.

![dynamiska återgivningar](/help/assets/assets/dm-templates-smart-text-resize.png)

**Leveransrapporter för dynamiska media**

Få leveransinsikter om mediefiler som levereras via Dynamic Media, inklusive leveransantal på tillgångsnivå, referensinformation, resurssökvägar i AEM Assets och unika medie-ID:n. Generera rapporter för alla resurser i AEM Assets-databasen eller specifika mapphierarkier. Med dessa insikter kan ni mäta avkastningen på levererade resurser, utvärdera kanalernas prestanda och fatta välgrundade beslut för resurshantering.

![dynamiska återgivningar](/help/assets/assets/referrer.png)

**Dynamic Media Multi-audio och caption**

[Stöd för flera bildtexter och flerljudspår för videofilmer i dynamiska media](/help/assets/dynamic-media/video.md#about-msma) - Nu kan du enkelt lägga till flera bildtexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för en global publik. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera beskrivningar och ljudspår från en enda flik i användargränssnittet.

**Dynamisk adaptiv strömning över HTTP-stöd**

Nytt protokollstöd har startats (DASH - Dynamic Adaptive Streaming over HTTP) för adaptiv strömning i Dynamic Media-leverans (med CMAF aktiverat):

* Adaptiv direktuppspelning (DASH/HLS) ger en bättre användarupplevelse för videor.

* DASH är det internationella standardprotokollet för strömning av adaptiv video och används ofta i branschen

**Resursrelationer**

Assets View har nu stöd för att visa och redigera resursrelationer på en förenklad resurspanel. Lägg enkelt in relationer som Source och Derivative i materialet så att användarna kan hitta relevant hjälteinnehåll effektivare.

**Bearbeta resurser igen**

Assets-vyn har nu stöd för återbearbetning av resurser som finns i en mapp. Du kan välja att antingen använda alternativet **Fullständig process** eller använda avancerade alternativ, som till exempel standardåtergivningar för förhandsgranskning, metadata, arbetsflöde för efterbearbetning och bearbetningsprofil.

### Tidig åtkomst-funktioner i AEM Assets {#early-access-features-assets}

**AI-genererade videobeskrivningar**

AI-genererade videobildtexter i Adobe Dynamic Media använder artificiell intelligens för att automatiskt generera bildtexter för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter i realtid. Bildtexter genereras från det ursprungliga ljudet, eventuella ytterligare ljudspår eller extra bildtexter som finns på fliken Bildtexter och ljud på videoegenskapssidan. Med stöd för över 60 språk kan bildtexter granskas och förhandsgranskas innan videon publiceras.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i AEM Forms {#forms-new-features}

#### Hantera publikation

Du kan använda arbetsflödet Hantera publikation för att publicera eller avpublicera formulär i olika miljöer, vanligtvis från författarinstansen till publicerings- och förhandsgranskningsinstanserna. Användarna kan publicera, avpublicera eller schemalägga publiceringen på ett smidigt sätt.

#### Autospara ett utkast för Core Components based Adaptive Forms

Användare kan nu dra nytta av en [funktion för att spara automatiskt](/help/forms/save-core-component-based-form-as-draft.md) som ett delvis ifyllt formulär som ett utkast. De kan gå tillbaka senare för att slutföra ifyllningen på samma eller annan enhet. Den här funktionen förbättrar konverteringsgraden för organisationer genom att minska antalet ifyllda formulär, eftersom användarna inte behöver börja om från början.

#### Förbättrad regelredigerare

För Adaptiv Forms baserat på kärnkomponenter kan du använda [utdata från Invoke Service för att fylla i nedrullningsbara alternativ och ange repeterbara eller individuella paneler](/help/forms/invoke-service-enhancements-rule-editor.md). Dessutom kan dessa utdata användas för att validera andra fält.

#### Förbättra användarupplevelsen med navigeringsknappar i panellayouter

Nu kan du lägga till navigeringsknappar i panellayouterna, till exempel Vågräta flikar, Lodräta flikar, Dragspel eller Guide. Dessa knappar [förbättrar användarupplevelsen genom att förenkla övergångar mellan paneler och fokusera på den valda panelen](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button).


### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### HTML e-postmallar i Adaptiv Forms

Med adaptiv Forms kan du använda [HTML e-postmallar](/help/forms/html-email-templates-in-adaptive-forms.md). Med HTML e-postmallar kan du skicka snygga, personliga och visuellt tilltalande e-postmeddelanden när ett formulär skickas. Dessa e-postmeddelanden kan anpassas med formulärdata och förbättras med olika e-posttaggar, som bilder och länkar. Med Adaptive Forms kan du antingen ladda upp en fil som innehåller en HTML-mall eller använda en vanlig textredigerare för att skapa mallarna.

![HTML e-postmallar](/help/forms/assets/html-email.png)

#### Förbättrat molnlagringsstöd: Direktöverföring av PDF till Azure Blob Storage

AEM Forms API:er för dokumentgenerering gör nu att du kan [överföra genererade PDF-dokument direkt till Azure Blob Storage](/help/forms/early-access-ea-features.md#doc-generation-api). Den här förbättringen effektiviserar lagring och hämtning, vilket förbättrar effektiviteten och integreringen med molnarbetsflöden.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Stöd för Java 21 {#java21}

Nu kan du skapa kod med Java 21, som innehåller nya funktioner (t.ex. mönstermatchning för switch-satser, fasta klasser) och prestandaförbättringar. Java 17-byggen stöds också nyligen. Konfigurationssteg, inklusive uppdatering av projekt- och biblioteksversioner för Maven, finns i artikeln [Byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Den mer prestandaanpassade Java 21 **runtime** distribueras automatiskt när en Java 17- eller 21-version upptäcks. Vi rekommenderar dock att du går med i Java 21-miljön för miljöer som byggts med Java 11 genom att skicka ett e-postmeddelande till [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Läs mer om [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Java 21 **runtime** distribueras gradvis till **alla** -miljöer (förutom de som redan byggts med Java 17 eller 21, som redan har Java 21-körning), med början från sandlådor och dev/RDE i februari och sedan fas/produktion i april.

### Sandlådeprogram har stöd för konfigureringspipelines {#sandbox-config-pipelines}

Sandlådeprogram har nu stöd för konfigureringspipelines, som kan konfigureras i Cloud Manager för att distribuera AML-filer som finns i Git.

[Läs mer](/help/operations/config-pipeline.md) om konfigureringspipelines, som gör det möjligt att konfigurera CDN, vidarebefordra loggar och rensa/granska loggtömningsunderhållsaktiviteter.

### OpenAPI-baserade API:er - tidigt Adobe-program {#open-apis-earlyadopter}

Utvecklare kan integrera AEM som Cloud Service-funktioner i sina egna program och verktyg. Nya AEM as a Cloud Service-API:er följer OpenAPI-specifikationen och har som mål att vara konsekventa, väldokumenterade och användarvänliga. Autentiseringsuppgifter för slutpunkter som kräver autentisering genereras genom att Adobe Developer Console-projekt skapas.

Lär dig mer om [OpenAPI-baserade AEM API:er](/help/implementing/developing/open-api-based-apis.md) och prova en [heltäckande självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) som visar konfiguration och användning.

De API-slutpunkter som anges nedan är tillgängliga som en del av ett program för tidig användning. Om du är intresserad kan du skicka ett e-postmeddelande till [aem-apis@adobe.com](mailto:aem-apis@adobe.com) med en beskrivning av hur du tänker använda dem.

* [API:er för innehållsfragment för webbplatser](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Webbplatser och API:er för Assets-mappar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge Computing - Request for Feedback! {#edge-computing-feedback}

Edge datoranvändning för databearbetning närmare webbläsaren, vilket har bl.a. kortare svarstider. Adobe vill gärna veta om du tycker att den här tekniken är användbar för AEM Publish Delivery och Edge Delivery Services. Dessutom kan du tala om för oss vad du tänkt dig när du använder den som indata i produktfärdplanen. Mejla [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med frågor och kommentarer!

### Nya AEM Developer Console (Public Beta) {#aem-developer-console-beta}

Prova en omgjord [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) som erbjuder en mer interaktiv upplevelse för felsökning av kod i molnmiljöer.

Vem som helst kan komma åt den offentliga betaversionen genom att klicka på knappen *Ny konsol tillgänglig* i den aktuella AEM Developer Console. Adobe tar gärna emot feedback, som du kan skicka med e-post till [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

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
