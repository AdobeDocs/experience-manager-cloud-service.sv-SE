---
title: Versionsinformation om 2024.8.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2024.8.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: dd1d4b8f-8331-4e97-a754-37e720974db6
source-git-commit: 61b40acf4f51c16a694b7c3b13ee1c480670ee3f
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# Versionsinformation 2024.8.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.8.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.8.0) är 29 augusti 2024. Nästa funktionsrelease (2024.9.0) planeras att släppas den 26 september 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon Augustiversionen 2024 med en sammanfattning av funktioner som lagts till i version 2024.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Ny funktion i Experience Manager Sites {#new-feature-sites}

**AEM Authoring for Edge Delivery Services**

Befintliga [arv](/help/sites-cloud/authoring/universal-editor/inheritance.md)-funktioner för platser stöds nu:

* [AEM Launches](/help/sites-cloud/authoring/launches/overview.md)
* [MSM](/help/sites-cloud/administering/msm/overview.md) på sidnivå

Dessutom stöds nu följande sidhanteringsfunktioner:

* [AEM-taggar](/help/sites-cloud/authoring/sites-console/tags.md) kan exporteras som en [taxonomi](/help/edge/wysiwyg-authoring/taxonomy.md) till Edge Delivery Services.
* [Mallar](/help/sites-cloud/authoring/universal-editor/templates.md) för Edge Delivery Services kommer snart!

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktion, [generera varianter](/help/generative-ai/generate-variations.md), som nu är tillgängliga i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ditt Adobe-kontoteam och ta del av ditt bidrag i programmet.


## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i vyn Assets {#assets-view-new-features}

**Uppdaterad generering av Adobe Firefly-bilder**

Assets as a Cloud Service använder nu den senaste widgeten från Firefly som gör att du kan generera bilder i olika format med Adobe Firefly. Genom att definiera format, komposition, dimensioner med mera i den inbyggda Firefly-redigeraren kan du snabbt skapa och spara de resurser du behöver direkt i AEM Assets-databasen för omedelbar användning.

![Adobe Firefly bildgenerering](/help/assets/assets/bugatti-type-57.png)

**Stöd för PSB-filer**

Assets as a Cloud Service har nu stöd för Photoshop stora dokument (PSB-filer) utöver det befintliga stödet för PSD-filer.

### Nya förbättringar i Content Hub {#content-hub-new-enhancements}

* Bättre hantering av långa filnamn, enkel utökning av hela namnet med verktygstips.
* Förbättrade miniatyrbilder som bättre passar innehållets proportioner och täcker större innehållsområden.
* En anpassad miniatyrbildsupplevelse från AEM stöds med innehållsnavet.
* Förbättrad färgsökning.
* Förbättrade konfigurationer sparar upplevelser.
* Förbättrad informationssida för samlingar som återspeglar skaparens namn.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i förhandsversionen av AEM Forms {#forms-new-prerelease-features}

#### Autospara ett utkast för Core Components based Adaptive Forms

Användarna kan nu dra nytta av en autosparfunktion som automatiskt sparar ett delvis ifyllt formulär som ett utkast. De kan gå tillbaka senare för att slutföra ifyllningen på samma eller annan enhet. Den här funktionen förbättrar konverteringsgraden för organisationer genom att minska antalet blanketter som tas bort, eftersom man inte behöver börja om från början.


### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### AEM Forms AI Assistant

Generativ AI för Adaptive Forms ger en helt ny nivå av kraft och enkelhet i era formulärutvecklingsprocesser. Det gör att ni kan skapa bättre formulär snabbare än någonsin.

![Generativ AI-assistent, adaptiv Forms](/help/forms/assets/generative-ai-assistant.png)

De genererande AI-funktionerna är:

* **AI-assistenten för produktfrågor**: Få svar på dina formulärrelaterade frågor om AEM. AI-assistenten fungerar som din egen personliga kunskapsbas och ger insiktsfull vägledning och rekommendationer direkt inom plattformen.

* **Skapa anpassade formulär**: Skapa enkelt fullfjädrade formulär med generativa AI-frågor. Vår generativa AI genererar automatiskt användarvänliga formulär som minskar bortfall och personaliserar upplevelsen.

* **Panelgenerering för Forms**: Generera formuläravsnitt som är anpassade efter specifika datainsamlingsbehov. Generera t.ex. avsnitt för insamling av betalningsinformation, kundpreferenser eller reseinformation.

* **Ändra formulärlayouter**: Experimentera med olika layouter och designer med hjälp av allmänna AI-prompter. Testa olika layouter som guiden eller flikvyer för att hitta den som passar ditt formulär bäst. Använd Generative AI-prompter för att optimera formulären för mobilrespons och skapa visuellt engagerande formulär som användarna gillar.

* **Konfigurera Skicka-åtgärd**: Använd generativa AI-uppmaningar för att enkelt konfigurera en skicka-åtgärd för formuläret. Välj från ett bibliotek med färdiga skicka-åtgärder eller från en lista med anpassade skicka-åtgärder som skapats och driftsatts av ditt eget utvecklingsteam.

>[!IMPORTANT]
>
> Om du är intresserad av att delta i programmet för tidig åtkomst av någon anledning skickar du ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) med en lista över funktioner du är intresserad av.


## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Content Delivery related Tire Adobe Programs {#foundation-early-adopter}

Mejla **<aemcs-cdn-config-adopter@adobe.com>** som anger vilket av de tidiga adopterprogrammen nedan du är intresserad av.

#### Grundläggande autentisering vid CDN (Early Adobe Program) {#basicauth-cdn}

Skydda vissa innehållsresurser genom att öppna en enkel dialogruta för autentisering som kräver ett användarnamn och lösenord. Den här funktionen riktar sig främst till användarvänliga fall av autentisering, som affärsintressenter som granskar innehåll, i stället för att fungera som en heltäckande lösning för slutanvändarnas åtkomsträttigheter. Listan över användarnamn och lösenord som hanteras via en konfigurationsfil i Git som distribueras via Configuration Pipeline, med en referens till Cloud Manager-miljövariabler av hemlig typ. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Omdirigeringar på klientsidan (tidigt Adobe-program) {#client-side-redirects-early-adopter}

Konfigurera 301/302 klientomdirigeringar i källkontroll och distribuera till CDN. [Läs mer](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observera att det redan finns flera andra funktioner för [CDN-konfiguration](/help/implementing/dispatcher/cdn-configuring-traffic.md), bland annat omvandlingar av begäranden och svar samt routning av trafik till platser utanför AEM.

#### Affärsanvändare kan deklarera omdirigeringar utanför Git (tidig Adobe-program) {#apache-rewritemaps-early-adopter}

Ungefär som i AEM 6.5 skriver Apache/dispatcher ingest om kartor som placerats på en viss plats i publiceringsdatabasen och läser in dem, utan att någon pipeline-körning behövs på webbnivån. På så sätt kan företagsanvändare deklarera omdirigeringar med hjälp av ett kalkylblad eller ett gränssnitt, som ACS Commons Redirect Map Manager eller ett anpassat program. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) for Loading Dynamic Content (Early Adobe Program) {#esi-early-adopter}

Adobe hanterade CDN har nu stöd för [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), ett markeringsspråk för dynamisk sammanställning av webbinnehåll på kantnivå. Genom att inkludera ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, samtidigt som du oftare hämtar de mindre avsnitt som kräver högre uppdateringsfrekvens (lägre TTL-värden) från ursprungsläget. <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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
