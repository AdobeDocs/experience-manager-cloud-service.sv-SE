---
title: Versionsinformation för version 2024.9.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2024.9.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: 0c4db1b70aa665e1802a316ece26db1e06f40b24
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---

# Versionsinformation 2024.9.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.9.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för att lära dig mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av versionsinformation för Experience Cloud, prenumererar du på [produktuppdateringen för Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.9.0) är 26 september 2024. Nästa funktionsrelease (2024.10.0) planeras till 31 oktober 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för september 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Ny funktion i Experience Manager Sites {#new-feature-sites}

#### Översättningshantering {#translation-management}

AEM översättningsarbetsflöden och API-åtgärder utlöser nu händelser som ger insikter om förändringar i översättningsjobbens tillstånd. Användare kan prenumerera på dessa evenemang via Adobe Developer Console. Mer information om API:t för AEM översättningshantering finns i [här](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/).

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom att AEM nya funktioner, [generera varianter](/help/generative-ai/generate-variations.md), som nu är tillgängliga i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ert Adobe-kontoteam för att ta del av detta i programmet.


## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Tidig åtkomst i Dynamic Media {#dm-early-access}

**AI-genererade videobeskrivningar**

AI-genererade videobildtexter i Adobe Dynamic Media använder artificiell intelligens för att automatiskt generera bildtexter för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter i realtid. AI analyserar videons ljudspår för att transkribera tal och skapa bildtexter som kan redigeras för precision eller anpassning. Dessa bildtexter uppfyller tillgänglighetskraven och förbättrar engagemanget för videoklipp som förlitar sig på eller föredrar textbaserat videostöd.

[Skapa och skicka ett kundsupportärende](/help/assets/dynamic-media/video.md##enable-dash) om du vill få snabb tillgång till stöd för AI-genererade bildtexter på ditt Dynamic Media-konto.

### Nya funktioner i Resursväljaren {#asset-selector-new-features}

Resursväljaren har nu stöd för att bläddra bland samlingar för att hitta den önskade resursen.
![Resursväljarsamlingar](/help/assets/assets/collections-rail-modal-view.png)

### Nya funktioner i Content Hub {#content-hub-new-features}

Administratörer kan nu kontrollera om utgångna resurser behöver vara synliga på Content Hub. Om de utgångna resurserna blir synliga kan de även definiera om användare kan hämta dem.

![Utgångna resurser på Content Hub](/help/assets/assets/view-download-expired-assets.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i förhandsversionen av AEM Forms {#forms-new-prerelease-features}

#### Autospara ett utkast för Core Components based Adaptive Forms

Användarna kan nu dra nytta av en autosparfunktion som automatiskt sparar ett delvis ifyllt formulär som ett utkast. De kan gå tillbaka senare för att slutföra ifyllningen på samma eller annan enhet. Den här funktionen förbättrar konverteringsgraden för organisationer genom att minska antalet ifyllda formulär, eftersom användarna inte behöver börja om från början.


### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### AEM Forms AI Assistant

Generativ AI för Adaptive Forms ger en helt ny nivå av kraft och enkelhet i era formulärutvecklingsprocesser. Det gör att ni kan skapa bättre formulär snabbare än någonsin.

![Generativ AI-assistent, adaptiv Forms](/help/forms/assets/generative-ai-assistant.png)

De genererande AI-funktionerna är:

* **AI-assistenten för produktfrågor**: Få svar på dina AEM formulärrelaterade frågor direkt. AI-assistenten fungerar som din egen personliga kunskapsbas och ger insiktsfull vägledning och rekommendationer direkt inom plattformen.

* **Skapa anpassade formulär**: Skapa enkelt fullfjädrade formulär med generativa AI-uppmaningar. Adobe generative AI genererar automatiskt användarvänliga formulär som minskar bortfall och personaliserar upplevelsen.

* **Panelgenerering för Forms**: Generera formuläravsnitt som är anpassade efter specifika datainsamlingsbehov. Generera t.ex. avsnitt för insamling av betalningsinformation, kundpreferenser eller reseinformation.

* **Ändra formulärlayouter**: Experimentera med olika layouter och designer med hjälp av generativa AI-uppmaningar. Testa olika layouter som guiden eller flikvyer för att hitta den som passar ditt formulär bäst. Använd generativa AI-uppmaningar för att optimera formulären för mobilrespons och skapa visuellt engagerande formulär som användarna gillar.

* **Konfigurera Skicka-åtgärd**: Använd generativa AI-uppmaningar för att konfigurera en skicka-åtgärd utan problem för formuläret. Välj från ett bibliotek med färdiga skicka-åtgärder eller anpassade skicka-åtgärder som skapats och driftsatts av ditt utvecklingsteam.

>[!IMPORTANT]
>
> Är du intresserad av att delta i programmet för tidig åtkomst för något av Forms innovationer? Skicka ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) med en lista över funktioner som du är intresserad av.

## CIF {#cloud-services-cif}

### Förbättringar {#improvements-fixes-cif}

* Gör kategorigränsen anpassningsbar.

### Felkorrigeringar {#bug-fixes-cif}

* Commerce-fälten är inte korrekt integrerade med Assets metadataschredigerare.
* Problem med Carousel Products Multifield för dra och släpp.
* Problem med Carousel Category Multifield för dra och släpp.
* Det går inte att klicka på menyerna i sidinformationen på kategoritexten och produktredigeringssidan.
* Ordernummer visas inte på orderbekräftelsesidan.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Edge Side Includes (ESI) för inläsning av dynamiskt innehåll {#esi}

Hanterad CDN i Adobe har nu stöd för [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), ett markeringsspråk för dynamisk sammanställning av webbinnehåll på kantnivå. Genom att ta med ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, medan du oftare hämtar mindre avsnitt från ursprungsläget som kräver högre uppdateringsintervall (nedre TTL-värden). Den här funktionen kommer att lanseras gradvis.

### Grundläggande autentisering vid CDN {#basicauth-cdn}

Protect vissa innehållsresurser genom att öppna en enkel autentiseringsdialogruta som kräver användarnamn och lösenord. Den här funktionen riktar sig främst till användarvänliga fall av autentisering, som affärsintressenter som granskar innehåll, i stället för att fungera som en heltäckande lösning för slutanvändarnas åtkomsträttigheter. Listan över användarnamn och lösenord hanteras via en konfigurationsfil i Git som distribueras via Config Pipeline, med en referens till Cloud Manager-miljövariabler av hemlig typ. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

### Omdirigeringar på klientsidan {#client-side-redirects}

Deklarera [omdirigering av webbläsare](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) i en konfigurationsfil som distribueras till och utvärderas vid CDN. Detta kan vara användbart för scenarier som borttagning av sidor, ändrad webbplatsstruktur och SEO-optimering.

### New AEM Developer Console (Public Beta) {#aem-developer-console-beta}

Prova en omgjord [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) som erbjuder en mer interaktiv upplevelse för felsökning av kod i molnmiljöer.

Vem som helst kan komma åt den offentliga betaversionen genom att klicka på knappen *Ny konsol tillgänglig* i den aktuella AEM Developer Console. Adobe välkomnar feedback, som du kan skicka via e-post till **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![OSGi Bundles-skärm i AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### Affärsanvändare kan deklarera omdirigeringar utanför Git (tidig Adobe-program) {#apache-rewritemaps-early-adopter}

Ungefär som i AEM 6.5 skriver Apache/dispatcher ingests om kartor som placerats på en viss plats i publiceringsdatabasen och läser in dem utan att någon pipeline-körning behövs på webbnivån. På så sätt kan företagsanvändare deklarera omdirigeringar med hjälp av ett kalkylblad eller ett gränssnitt, som ACS Commons Redirect Map Manager eller ett anpassat program. Gå med i det tidiga adopterprogrammet genom att skicka **<aemcs-cdn-config-adopter@adobe.com>** med e-post.

### Config Pipeline for RDEs (Early Adobe Program) {#config-pipeline-rdes-early-adopter}

[Konfigurationspipeline](/help/operations/config-pipeline.md) används för att distribuera dynamiska filkonfigurationer, inklusive CDN-alternativ (trafikfilterregler, begäran-/svarsomformningar och så vidare). Delta i det tidiga adopterprogrammet genom att skicka **<aemcs-cdn-config-adopter@adobe.com>** med e-post för att distribuera samma konfigurationer till RDE (Rapid Development Environment), som använder ett CLI.

## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

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
