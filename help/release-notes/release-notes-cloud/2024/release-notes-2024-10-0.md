---
title: Versionsinformation om 2024.10.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2024.10.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 7a63f04f-10f0-4879-bd06-4182bb288a9b
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---

# Versionsinformation 2024.10.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.10.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.10.0) är 31 oktober 2024. Nästa funktionsrelease (2024.11.0) planeras att släppas den 21 november 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för oktober 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3440501?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

**Moderniserade sidhändelser**

Följande AEM Sites-sidhändelser är nu tillgängliga som externt konsumerbara händelser som är baserade på AEM as a Cloud Service Eventing Platform. Händelserna kan behandlas via Adobe I/O för att interagera med externa processer.
* Sidan publicerad
* Sidan har inte publicerats
* Sidan har tagits bort

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktion, [generera varianter](/help/generative-ai/generate-variations.md), som nu är tillgängliga i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ditt Adobe-kontoteam och ta del av ditt bidrag i programmet.

**AEM REST OpenAPI för leverans av innehållsfragment**

[AEM REST OpenAPI för leverans av innehållsfragment](/help/headless/aem-content-fragment-delivery-with-openapi.md) är nu tillgängligt för AEM as a Cloud Service.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Funktion för tidig åtkomst i Dynamic Media {#dm-early-access}

**AI-genererade videobeskrivningar**

AI-genererade videobildtexter i Adobe Dynamic Media använder artificiell intelligens för att automatiskt generera bildtexter för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter i realtid. AI analyserar videons ljudspår för att transkribera tal och skapa bildtexter som kan redigeras för precision eller anpassning. Dessa bildtexter uppfyller tillgänglighetskraven och förbättrar engagemanget för videoklipp som förlitar sig på eller föredrar textbaserat videostöd.

[Skapa och skicka ett Adobe kundsupportärende](/help/assets/dynamic-media/video.md##enable-dash) om du vill få tidig åtkomst till AI-genererade bildtexter på ditt Dynamic Media-konto.

### Nya funktioner i vyn Assets {#assets-view-new-features}

**Schemalagda rapporter**

Rapporterna kan nu genereras automatiskt i Assets View enligt ett återkommande schema eller vid ett framtida datum, vilket minskar behovet av att identifiera datadrivna insikter.

![Schemalagda rapporter-](/help/assets/assets/scheduled-reports-tab.png)

### Nya funktioner i Content Hub {#content-hub-new-features}

**Hantering av digitala rättigheter för licensierade resurser**

Organisationer kan nu öka licensefterlevnaden och minimera risken för att dela mediefiler med licensieringsvillkor genom att utnyttja DRM för licensierade mediefiler för användare av Content Hub, vilket kräver att användare granskar och godkänner licensvillkoren innan de kan börja hämta licensierade mediefiler. Mer information finns i [Hantera licensierade mediefiler på Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

![download-multiple-license](/help/assets/assets/download-multiple-license.png)

**Resurskortets metadatakonfiguration**

Content Hub tillåter nu att du konfigurerar de viktigaste metadatafälten som du behöver visa på resurskortet till högst 6 fält. Mer information finns i avsnittet Resurskort i [Konfigurera Content Hub](/help/assets/configure-content-hub-ui-options.md#asset-card).

![nyckelmetadata på resurskortet](/help/assets/assets/asset-card-key-metadata.png)

**Konfigurera synlighet och hämtning av utgångna resurser**

Administratörer kan nu kontrollera om utgångna resurser behöver vara synliga på Content Hub. Om de utgångna resurserna blir synliga kan de även definiera om användare kan hämta dem. Mer information finns i avsnittet Utgånget Assets i [Konfigurera Content Hub](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub).

![Utgångna resurser på Content Hub](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Ny funktion i AEM Forms {#forms-new-features}

* [Förbättra användarupplevelsen med navigeringsknappar i panellayouter](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button): Nu kan du lägga till navigeringsknappar i panellayouterna, till exempel Vågräta flikar, Lodräta flikar, Dragspel eller Guide. Dessa knappar förbättrar användarupplevelsen genom att förenkla övergångar mellan paneler och fokusera på den valda panelen.

<!--* **Specify Display Styles for Document of Record (DoR) Components**: In an XFA file, you can now specify the display styles for Document of Record components. These styles can later be applied to the corresponding components in Adaptive Forms Editor.-->

### Nya funktioner i förhandsversionen av AEM Forms {#forms-new-prerelease-features}

* [Spara ett utkast automatiskt för Core Components-baserade Adaptive Forms](/help/forms/save-core-component-based-form-as-draft.md): Användare kan nu dra nytta av en autosparfunktion som sparar ett delvis ifyllt formulär som ett utkast automatiskt. De kan gå tillbaka senare för att slutföra ifyllningen på samma eller annan enhet. Den här funktionen förbättrar konverteringsgraden för organisationer genom att minska antalet ifyllda formulär, eftersom användarna inte behöver börja om från början.

* [Uppdatera Adobe Sign-omfång enkelt](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms): Du kan ändra omfånget för en Adobe Sign-konfiguration direkt från sidan AEM Cloud Configurations, vilket gör det snabbare och enklare att uppdatera befintliga konfigurationer.

* [Stöd för asynkrona funktioner i Adaptiv Forms](/help/forms/using-async-funct-in-rule-editor.md): När ditt adaptiva formulär kräver asynkrona åtgärder, t.ex. att vänta på externa processer eller datahämtning, kan du implementera dessa åtgärder med anpassade funktioner och konfigurera dem i regelredigeraren.

### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### AEM Forms AI Assistant

[Generativ AI för Adaptiv Forms](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features#aem-forms-ai-assistant-gen-ai) ger en helt ny nivå av kraft och enkelhet i dina formulärutvecklingsprocesser. Det gör att ni kan skapa bättre formulär snabbare än någonsin.

![Generativ AI-assistent, adaptiv Forms](/help/forms/assets/generative-ai-assistant.png)

De genererande AI-funktionerna är:

* **AI-assistenten för produktfrågor**: Få svar på dina formulärrelaterade frågor om AEM. AI-assistenten fungerar som din egen personliga kunskapsbas och ger insiktsfull vägledning och rekommendationer direkt inom plattformen.

* **Skapa anpassade formulär**: Skapa enkelt fullfjädrade formulär med generativa AI-uppmaningar. Adobe generativa AI genererar automatiskt användarvänliga formulär som minskar antalet avhopp och personaliserar upplevelsen.

* **Panelgenerering för Forms**: Generera formuläravsnitt som är anpassade efter specifika datainsamlingsbehov. Generera t.ex. avsnitt för insamling av betalningsinformation, kundpreferenser eller reseinformation.

* **Ändra formulärlayouter**: Experimentera med olika layouter och designer med hjälp av generativa AI-uppmaningar. Testa olika layouter som guiden eller flikvyer för att hitta den som passar ditt formulär bäst. Använd generativa AI-uppmaningar för att optimera formulären för mobilrespons och skapa visuellt engagerande formulär som användarna gillar.

* **Konfigurera Skicka-åtgärd**: Använd generativa AI-uppmaningar för att konfigurera en skicka-åtgärd utan problem för formuläret. Välj från ett bibliotek med färdiga skicka-åtgärder eller anpassade skicka-åtgärder som skapats och driftsatts av ditt utvecklingsteam.

>[!IMPORTANT]
>
> Är du intresserad av att delta i programmet för tidig åtkomst för något av Forms innovationer? Skicka ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) med en lista över funktioner som du är intresserad av.

## CIF Add-on {#cloud-services-cif}

### Felkorrigeringar {#bug-fixes-cif}

* Korrigerade gränssnittstester för att fungera korrekt med CIF kärnkomponenter.
* Ett problem med kategorins URL-format som inte fungerar som väntat i molninstansen har åtgärdats.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Konfiguration för att styra formuläröverföringar {#configuration-submissions}

För att styra formulärinskickade formulär för Coral- eller Foundation-formulär på specifika platser har AEM infört en ny konfiguration: `com.adobe.granite.ui.components.FormRestrict`. Den här konfigurationen består av två fält:

1. **Lägg till tillåtna sökvägar**: Anger sökvägarna där formuläråtgärder tillåts.
1. **Begränsa beteende**: Anger beteendet för begränsade sökvägar (sökvägar som inte ingår i tillåtelselista). Du kan välja mellan två alternativ:
   * **Popup** (standard): Visar ett popup-meddelande.
   * **Förhindra**:Blockerar formulärskickning.

>[!NOTE]
>
>Den här konfigurationen stöds inte för alla Coral- eller Foundation-formulär som finns under `/apps`, `/libs`, `/mnt/overlay` och `/mnt/override`.

### Självbetjänad loggvidarebefordran med alternativet Avancerat nätverk {#log-forwarding}

Medan AEM (inklusive Apache/Dispatcher) och CDN-loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har nu stöd för [vidarebefordran av ](/help/implementing/developing/introduction/log-forwarding.md) till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. AEM-loggar kan vidarebefordras över avancerade nätverkskonfigurationer, till exempel via en dedikerad IP-adress.

Den här funktionen konfigureras av användare på ett självbetjäningssätt och distribueras med [konfigurationspipeline](/help/operations/config-pipeline.md).

### Pipeline-fria URL-omdirigeringar för företagsanvändare {#pipeline-free-redirects}

Omdirigeringar på webbläsarsidan är användbara när en webbsida har tagits ned eller flyttats, eller i andra scenarier. Med [Pipeline-fria URL-omdirigeringar](/help/implementing/dispatcher/pipeline-free-url-redirects.md) kan du montera en Apache-omskrivningsfil på en publiceringsplats i AEM, där den läses in automatiskt - du behöver inte implementera filen i en källkontroll eller initiera en Cloud Manager-pipeline.

Du kan publicera filen som ska skrivas om genom att överföra den som en resurs, använda ACS Commons Rewrite Map Manager eller genom att interagera med ett anpassat användargränssnitt.

### Konfigurera pipeline för RDE:er {#config-pipeline-rdes}

Snabba utvecklingsmiljöer är ett kraftfullt verktyg för att snabbt distribuera och testa kod och konfiguration i en molnmiljö. De virtuella skrivborden har nu stöd för [synkronisering av konfiguration-YAML-filer](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline), inklusive CDN-inställningar som trafikfilterregler och begäran-/svarsomvandlingar samt loggvidarebefordran och andra konfigurationsalternativ. [Se den fullständiga listan](/help/operations/config-pipeline.md) med konfigurationsalternativ som stöds för mer information.

### Nya produktprofiler {#new-product-profiles}

När en ny AEM-miljö skapas visas produktprofiler automatiskt i Adobe Admin Console så att administratörer kan tilldela åtkomst till licensierade lösningar och funktioner.

Nya miljöer innehåller nu en uppdaterad uppsättning produktprofiler, vilket gör dem kompatibla med framtida funktioner, inklusive generering av API-autentiseringsuppgifter i Adobe Developer Console. Befintliga miljöer kommer att kunna uppdatera sina produktprofiler i en kommande version. [Läs mer](/help/onboarding/aem-cs-team-product-profiles.md).

### Nya AEM Developer Console (Public Beta) {#aem-developer-console-beta}

Prova en omgjord [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) som erbjuder en mer interaktiv upplevelse för felsökning av kod i molnmiljöer.

Vem som helst kan komma åt den offentliga betaversionen genom att klicka på knappen *Ny konsol tillgänglig* i den aktuella AEM Developer Console. Adobe tar gärna emot feedback, som du kan skicka med e-post till **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![OSGi Bundles-skärm i AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/sv/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

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
