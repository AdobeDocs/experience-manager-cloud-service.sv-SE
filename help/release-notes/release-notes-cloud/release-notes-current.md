---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d424b6f2e0a2ec40ab607dcbdcba3120c7f45a58
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för att lära dig mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av versionsinformation för Experience Cloud, prenumererar du på [produktuppdateringen för Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.11.0) är 21 november 2024. Nästa funktionsversion (2025.1.0) är planerad till 30 januari 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]Sidmallar med Universal Editor-redigering**

Gör snabbt om en Edge Delivery-sida till en sidmall. På så sätt kan du starta en ny sida med en fördefinierad struktur och innehåll i stället för en tom sida. [Läs mer](/help/sites-cloud/authoring/universal-editor/templates.md).

**[!DNL Edge Delivery Services]CSV-importerare för publicering via en AEM**

Hantera dina Edge Delivery-kalkylbladsdata (t.ex. omdirigeringar) effektivt i ditt kalkylbladsverktyg och ladda upp dem till AEM via den nya CSV-importeraren. [Läs mer](/help/edge/wysiwyg-authoring/tabular-data.md#importing).

### Förhandsversionsfunktioner i AEM Sites

Förbättrade [Content Fragment-referenser med unika ID-baserade referenser](/help/headless/graphql-api/uuid-reference-upgrade.md), vilket säkerställer stabila länkar som förblir giltiga även när resurser eller fragment flyttas, vilket eliminerar behovet av uppdateringar eller ompublicering. Aktuell begränsning: Sidreferenser stöds ännu inte med unika ID:n. Om det finns referenser till sidor i innehållsfragment bör den här funktionen inte användas.

### Tidiga Adobe-program {#sites-early-adopter}

**AEM REST OpenAPI för leverans av innehållsfragment**

[AEM REST OpenAPI för Content Fragment Delivery](/help/headless/aem-rest-openapi-content-fragment-delivery.md) är nu tillgängligt för AEM as a Cloud Service.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Tidiga åtkomstfunktioner i Dynamic Media {#dm-early-access}

**AI-genererade videobeskrivningar**

AI-genererade videobildtexter i Adobe Dynamic Media använder artificiell intelligens för att automatiskt generera bildtexter för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter i realtid. AI analyserar videons ljudspår för att transkribera tal och skapa bildtexter som kan redigeras för precision eller anpassning. Dessa bildtexter uppfyller tillgänglighetskraven och förbättrar engagemanget för videoklipp som förlitar sig på eller föredrar textbaserat videostöd.

[Skapa och skicka ett kundsupportärende](/help/assets/dynamic-media/video.md##enable-dash) om du vill få snabb tillgång till stöd för AI-genererade bildtexter på ditt Dynamic Media-konto.

**Dynamic Media leveransrapport**

Få leveransinsikter om mediefiler som levereras med Dynamic Media, med leveransantal på tillgångsnivå, referensinformation, resurssökväg i AEM Assets och unikt resurs-ID. Rapporter kan genereras för alla resurser som levereras via Dynamic Media för AEM Assets-databasen eller för en viss mapphierarki i AEM Assets. Insikter hjälper till att mäta avkastningen på levererade tillgångar, mäta kanalernas prestanda och ta hjälp av välgrundade resurshanteringsåtgärder för tillgångar.

[Skapa och skicka ett kundsupportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) om du vill få tidig åtkomst till Dynamic Media-leveransrapporten för ditt Dynamic Media-konto.

### Nya funktioner i vyn Assets {#assets-view-new-features}

**Panelen Dynamic Media**

I Assets-vyn kan du nu komma åt Dynamic Media och Dynamic Media med OpenAPI-renderingar från en separat panel som du har tillgång till. Du kan välja att kopiera leverans-URL:en eller hämta återgivningarna baserat på resurs- och återgivningstyp. Mer information finns i [Dynamic Media-renderingar](/help/assets/renditions.md#dynamic-media-renditions) och [Dynamic Media med OpenAPI-funktionsåtergivningar](/help/assets/renditions.md#dm-with-openapi-renditions).

![dynamiska återgivningar](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i AEM Forms {#forms-new-features}

* **[Uppdatera Adobe Sign-omfång enkelt](/help/forms/adobe-sign-integration-adaptive-forms.md)**: Du kan ändra omfånget för en Adobe Sign-konfiguration direkt från sidan AEM Cloud Configurations, vilket gör det snabbare och enklare att uppdatera befintliga konfigurationer.

* **[Stöd för asynkrona funktioner i Adaptiv Forms](/help/forms/using-async-funct-in-rule-editor.md)**: När ditt adaptiva formulär kräver asynkrona åtgärder, t.ex. att vänta på externa processer eller datahämtning, kan du implementera dessa åtgärder med anpassade funktioner och konfigurera dem i regelredigeraren.

### Förhandsversioner av funktioner i AEM Forms {#forms-new-prerelease-features}

* **Hantera publikation**: Du kan använda arbetsflödet Hantera publikation för att publicera eller avpublicera formulär i olika miljöer, vanligtvis från författarinstansen till publicerings- och förhandsgranskningsinstansen/instanserna. Användarna kan publicera, avpublicera eller schemalägga publiceringen på ett smidigt sätt.

* **[Spara ett utkast automatiskt för Core Components-baserade Adaptive Forms](/help/forms/save-core-component-based-form-as-draft.md)**: Användare kan nu dra nytta av en autosparfunktion som sparar ett delvis ifyllt formulär som ett utkast automatiskt. De kan gå tillbaka senare för att slutföra ifyllningen på samma eller annan enhet. Den här funktionen förbättrar konverteringsgraden för organisationer genom att minska antalet ifyllda formulär, eftersom användarna inte behöver börja om från början.

* **[Förbättringar av regelredigeraren](/help/forms/invoke-service-enhancements-rule-editor.md)**: För adaptiv Forms baserat på kärnkomponenter kan du nu fylla i listrutealternativ med hjälp av utdata från Invoke Service, ange repeterbara paneler med utdata från Invoke Service, ange enskilda paneler med utdata från Invoke Service och använda utdataparametern för Invoke Service för att validera andra fält.

* **[Förbättra användarupplevelsen med navigeringsknappar i panellayouter](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: Nu kan du lägga till navigeringsknappar i panellayouterna, till exempel Vågräta flikar, Lodräta flikar, Dragspel eller Guide. Dessa knappar förbättrar användarupplevelsen genom att förenkla övergångar mellan paneler och fokusera på den valda panelen.


### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### Integreringar

* **[Integrera adaptiv Forms med Adobe Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)**: AEM Forms as a Cloud Service innehåller nu ett lättanvänt alternativ för att ansluta adaptiv Forms med Adobe Marketo Engage. Tack vare den här integreringen kan du skapa Adaptiv Forms direkt med Marketo Engage lead-hämtning och relaterade anpassade objekt. Nu kan ni förifylla formulärfält med data från Marketo Engage och skicka tillbaka data för att automatisera arbetsflöden som smarta kampanjer och automatisering av e-post. Du kan också koppla ett adaptivt formulär till Munchkin-biblioteket för att spåra antalet besök, klick och inskickade formulär.

#### Adaptiv Forms och HTML5 Forms

* **[Skapa adaptiv Forms baserat på befintlig XFA-mall](/help/forms/create-adaptive-form-using-xfa-templates.md)**: Nu kan du skapa Core Component-baserad Adaptiv Forms med XFA-formulärmallar (*.XDP-filer). Detta underlättar för AEM Forms On-Premise-kunder med befintliga investeringar i XFA-teknik att använda AEM Forms as a Cloud Service.

* **HTML5 Forms (XFA-baserade webbformulär)**: Nu kan AEM Forms On-Premise-kunder som använder XFA-teknik enkelt gå över till AEM Forms as a Cloud Service samtidigt som de behåller sin befintliga användarupplevelse med HTML5 Forms (XFA-baserade webbformulär). Denna funktion gör att XFA-formulärmallar kan återges i HTML5-format, vilket gör att formulär blir tillgängliga på enheter som inte stöder XFA-baserad PDF forms.

  ![HTML Forms (XFA-baserade webbformulär)](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[Base64-kodad sträng stöds för bifogad fil](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**: Komponenten för bifogad fil i adaptiv Forms baserad på kärnkomponenter innehåller nu ett alternativ för att skicka bifogade filer som Base64-kodade strängar.

#### API:er för interaktiv kommunikation och kommunikation

* **Interaktiv kommunikationsredigerare**: Den interaktiva kommunikationsredigeraren är ett användarvänligt grafiskt kommunikationsdesignverktyg som förenklar skapandet av personaliserade, datadrivna korrespondenser och kan köras i alla moderna webbläsare. Det stöder smidig dataintegrering, intrikata logiska definitioner och multimedieintegrering, vilket säkerställer professionell och kompatibel dokumentgenerering, kommunikation och mallgenerering för olika affärsbehov.

  ![Interaktiv kommunikationsredigerare](/help/forms/assets/ic-editor.png)


* **[Kompatibilitetsförbättringar för PDF/A](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**: Nu kan du använda kommunikations-API:er för att konvertera PDF-dokument till PDF/A-format (1a, 2a, 3a) i arkiveringssyfte samtidigt som du säkerställer tillgänglighet och verifierar överensstämmelse med dessa standarder.


* **[Signatur-API (Document Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**: Ett nytt RESTful-API i kommunikations-API:er gör det enkelt att hantera PDF-signaturer. Den stöder åtgärder som:
   * Rensa signatur: Tar bort en signatur från ett angivet fält.
   * Ta bort signaturfält: Tar bort ett angivet signaturfält.


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## Tjänsten Automated forms conversion

* **[Konvertera PDF forms till Core Components-baserade adaptiva Forms](https://experienceleague.adobe.com/en/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**: nu kan du använda Automated forms conversion-tjänsten för att omvandla PDF forms-, AcroForms- eller XFA-baserade formulär till Core Components-baserade adaptiva Forms.


>[!IMPORTANT]
>
> Är du intresserad av att delta i programmet för tidig åtkomst för något av Forms innovationer? Skicka ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) med en lista över funktioner som du är intresserad av.## CIF tillägg {#cloud-services-cif}

## CIF {#cif}

### Felkorrigeringar {#bug-fixes-cif}

* Korrigerade gränssnittstester för att fungera korrekt med CIF kärnkomponenter.
* Ett problem med kategorins URL-format som inte fungerar som väntat i molninstansen har åtgärdats.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Förbättrad trädreplikeringsprestanda (och borttagning av Publish Content Tree Workflow) {#tree-replication-performance}

[Arbetsflödessteget för trädaktivering](/help/operations/replication.md#tree-activation) är ett nytt arbetsflödesmodellsteg som rekommenderas för replikering av hierarkier med djupgående innehåll. Observera att oberoende replikeringar (t.ex. genom snabb publicering eller hantering av publicering) kan fortsätta parallellt med arbetsflödet för trädreplikering. Detta är särskilt användbart om du behöver publicera tidskänsligt innehåll medan en gruppreplikering fortfarande pågår. Trädreplikeringssteget ersätter Publish Content Tree Workflow och dess relaterade arbetsflödessteg, som nu är inaktuellt.

### OpenAPI-baserade API:er - tidigt Adobe-program {#open-apis-earlyadopter}

Utvecklarna kan integrera AEM som Cloud Service i sina egna program och verktyg. Nya AEM as a Cloud Service-API:er följer OpenAPI-specifikationen och har som mål att vara konsekventa, väldokumenterade och användarvänliga. Autentiseringsuppgifter för slutpunkter som kräver autentisering genereras genom att Adobe Developer Console-projekt skapas.

Lär dig mer om [OpenAPI-baserade AEM-API:er](/help/implementing/developing/open-api-based-apis.md) och prova en [heltäckande självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) som visar konfiguration och användning.

De API-slutpunkter som anges nedan är tillgängliga som en del av ett program för tidig användning. Om du är intresserad kan du skicka ett e-postmeddelande till [aem-apis@adobe.com](mailto:aem-apis@adobe.com) med en beskrivning av hur du tänker använda dem.
* [API:er för innehållsfragment för webbplatser](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Webbplatser och API:er för Assets-mappar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge Computing - Request for Feedback! {#edge-computing-feedback}

Edge datoranvändning för databearbetning närmare webbläsaren, vilket har bl.a. kortare svarstider. Vi vill gärna veta om du tycker att den här tekniken är användbar i projekt AEM Publish Delivery och Edge Delivery Services och vad du tänker använda den till. Mejla [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med frågor och kommentarer!

### New AEM Developer Console (Public Beta) {#aem-developer-console-beta}

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
