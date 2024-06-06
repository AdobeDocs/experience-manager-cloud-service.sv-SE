---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: e6de1fc47eb2b9c3ba5b115c74b874016449bc20
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2024.5.0) är 30 maj 2024. Nästa version (2024.6.0) är planerad till 27 juni 2024.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon om versionsöversikten från maj 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner på webbplatser {#sites-new-features}

#### Integrering av AEM {#translation-integration}

Översättningsåtgärder och arbetsflöden för innehåll utlöser nu händelser som gör det möjligt att spåra relevanta processsteg och tillstånd från externa program. Följande händelser genereras. Användare kan prenumerera på händelser med Adobe Developer Console.

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### RUM-datatjänst (Real Use Monitoring) {#real-use-monitoring}

* **[RUM-datatjänsten (Real Use Monitoring) är nu GA](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** möjliggör datainsamling på klientsidan för AEM as a Cloud Service.
Tjänsten Real Use Monitoring, kundsidessamlingen, ger en mer exakt återgivning av interaktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det ger kunder med avancerade insikter om sidtrafik och prestanda. Det är en utmärkt möjlighet att lära sig mer om hur sidan fungerar och få insikter för att förbättra den.

#### AEM för Edge Delivery Services {#edge-enhancements}

Förbättrad stabilitet och olika förbättringar för en bättre redigeringsupplevelse.

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktioner, [generera variationer](/help/generative-ai/generate-variations.md), nu i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ert Adobe-kontoteam för att ta del av detta i programmet.

**Resursbläddring i Content Fragment Console**

Innehållsförfattare kan nu bläddra bland, visa och vidta åtgärder för bilder och andra resurser utan att behöva lämna konsolen Innehållsfragment.

![Resurssökning](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till aemcs-headless-adopter@adobe.com från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i administrationsvyn {#admin-view-new-features}

* WebM är nu en utdatafil som stöds i bearbetningsprofilen för video.
* MP4 stöds nu i den inbyggda integrationen av AEM i Express (import och export).

### Nya funktioner i resursvyn {#assets-view-new-features}

**Publicera material till AEM och Dynamic Media**

Med Experience Manager Assets kan du nu snabbt [publicera resurser på Experience Manager och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) använda resursvyn utan att växla till administrationsvyn. Du kan publicera resurser när du överför, bläddrar bland och söker efter resurser.

![kontrollera publiceringsstatus1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nya funktioner i förhandsversionen av AEM Forms {#forms-new-prerelease-features}

#### Förbättrad Visual Rule Editor för Core Component Based Adaptive Forms

Den här versionen innebär en betydande uppgradering av den visuella regelredigeraren för adaptiva formulär baserade på kärnkomponenter. Du kan nu:

* Skapa regler i Visual Rule Editor för att [åsidosätta standardmeddelanden om att formuläret har skickats in eller misslyckats](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* I den adaptiva Forms-regelredigeraren har du lagt till möjligheten att [välja olika typer av fält för WHEN-åtgärden](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* En formulärförfattare kan nu använda anpassade funktioner på [bearbeta data innan de skickas](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Använd [**Spara som utkast**](/help/forms/save-core-component-based-form-as-draft.md) funktioner för att spara delvis ifyllda formulär för senare inskickning. Detta är användbart i scenarier där användare måste avbryta ifyllandet av ett formulär och komma tillbaka till det senare.



### Tidiga Adobe-funktioner i AEM Forms {#forms-new-early-adopter-features}

AEM Forms Early Adobe Program ger dig unika möjligheter att få exklusiv tillgång till de senaste innovationerna åt alla andra och hjälper dig att utveckla dem.
Programmet ger tillgång till flera innovationer.

I den här versionsinformationen listas de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som finns inom programmet för tidig användning finns på [Dokumentation om AEM Forms Early Adobe-program](/help/forms/early-adopter-ea-features.md).

#### Förbättrade skyddsmetoder för robotar

AEM Forms har förbättrat sina säkerhetsfunktioner genom att lägga till stöd för två populära CAPTCHA-lösningar: Cloudflare Turnstile och hCaptcha. Detta lägger till Google reCAPTCHA, som ger användarna större valfrihet och flexibilitet när det gäller att skydda sina formulär mot inskickade bidrag från skräppost.

* **Molnformad vändning**: Denna friktionslösa CAPTCHA verifierar användarna genom en enkel utmaning som inte kräver någon explicit interaktion. De kan integreras smidigt i formulären och förbättrar användarupplevelsen.
* **hCaptcha**: Denna sekretessinriktade CAPTCHA erbjuder ett användarvänligt alternativ med fokus på datasekretess. Syftet är att skapa en balans mellan säkerhet och användarupplevelse.
* **Google reCAPTCHA**: AEM Forms fortsätter att stödja både reCAPTCHA v2 och reCAPTCHA Enterprise, som är en tillförlitlig och väletablerad lösning.

Genom att erbjuda flera CAPTCHA-alternativ har AEM Forms gett dig möjlighet att välja den lösning som bäst passar just dina behov.

Vill du integrera någon av dessa CAPTCHA-lösningar med din adaptiva Forms? I vår dokumentation finns detaljerade anvisningar för varje: [Molnformad vändning](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)och [Google reCAPTCHA](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Forms Service

Forms-tjänsten genererar interaktiv PDF forms för datainhämtning. Den kan också användas för att importera eller exportera data till och från ett befintligt interaktivt PDF-formulär och validera skickade data. Här är en beskrivning av funktionaliteten:

* **Återger Forms**: Generera ett interaktivt PDF-formulär från en mall som skapats med AEM Forms Designer och, eventuellt, XML-data. Detta skapar i stort sett ett ifyllbart PDF-formulär som kan fyllas i med data.
* **Extrahering och import av data**: Importera data till ett befintligt PDF-formulär och extrahera data från ett ifyllt PDF-formulär. Både XDP- och XML-dataformat stöds, och import till icke-XFA PDF forms (kallas även AcroForms) stöder dessutom FDF- och XFDF-data.
* **Dataverifiering**: Validera skickade data i XDP- eller XML-format mot en mall som skapats med AEM Forms Designer.

>[!IMPORTANT]
>
> Om du är intresserad av att delta i vårt tidiga Adobe-program för tidiga utvecklare skickar du ett mejl från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) för att begära åtkomst. Du kan begära åtkomst till alla eller alla specifika innovationer.


## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### OAuth Server-till-Server-autentiseringsuppgifter för integrering AEM andra Adobe-lösningar {#S2S-OAuth-credentials}

Adobe Developer Console används för att generera autentiseringsuppgifter för olika API:er. En av autentiseringstyperna, JWT (Service Account), har ersatts med autentiseringsuppgifter för OAuth Server-till-Server, som AEM Cloud Service nu stöder för integrering med andra Adobe-lösningar som Adobe Analytics och Adobe Target.

[Läs om borttagningen](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) och [lära dig hur du använder gränssnittet för AEM författare](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) för att konfigurera integreringar med andra Adobe-lösningar.

### Trafikrasch vid ursprungsvarningar {#traffic-spike-origin}

[Ta emot proaktiva meddelanden](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) via Åtgärdscenter när trafikmönster på ursprungsplatsen tyder på en DDoS-attack, vilket gör att du kan undersöka och konfigurera trafikfilterregler.

### Nya funktioner för RDE {#RDE-new-features}

[Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) gör att utvecklare snabbt kan driftsätta, granska och testa ändringar i molnet. Flera nya funktioner kommer att lanseras under juni-månaden. Vi bjuder också in dig direkt till Adobe Engineering på [RDE-indragskanal](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### RDE-stöd för frontkod med hjälp av webbplatsteman och webbplatsmallar {#rde-frontend}

[De lokala lagringsenheterna har nu stöd för slutkod](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) baserat på [webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) och [webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md), för tidiga användare. Med de lokala redigeringssystemen görs detta med hjälp av ett kommandoradsdirektiv i stället för ett [rörledning för frontend](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### Förbättrad loggning för RDE {#rde-logging}

När du felsöker kod i en RDE kan utvecklare nu [konfigurera och strömma loggar mer produktivt](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging), med kommandoraden och utan att ändra OSGI-egenskaper i versionskontrollen. Funktioner:

* deklarera loggnivåer per paket eller klassnivå
* anpassa loggutdataformatet
* strömma flera loggar parallellt

#### Förbättringar av RDE CLI {#rde-cli-enhancements}

Gränssnittet för RDE-kommandoraden har några nya funktioner som förbättrar utvecklarupplevelsen:

* [kommandot setup är interaktivt](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive), vilket gör det enklare att välja mellan organisationer, program och miljöer. Nu går det även att åsidosätta dessa värden på kommandoraden.
* [tyst läge](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) för en mindre detaljerad utskrift.
* [json-läge](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) för användbara utdata när de anropas programmatiskt.

### Nya meddelanden från Åtgärdscenter {#actions-center-notifications}

[Actions Center](/help/operations/actions-center.md) skickar e-postmeddelanden när viktiga incidenter inträffar eller om vi märker något om din kod eller konfiguration där du bör vidta proaktiva åtgärder. Det finns tre nya typer av meddelanden:

* för många utgående anslutningar via avancerad nätverksinfrastruktur
* användning av ett föråldrat tjänstanvändarmappningsformat
* en potentiell DDoS-attack pågår

### Tidiga Adobe-program {#foundation-early-adopter}

E-post **<aemcs-cdn-config-adopter@adobe.com>**, vilket av de tidiga adopterprogrammen nedan du är intresserad av.

#### Rensa innehåll på CDN med en självbetjäningsnyckel (Early Adobe Program) {#purge-cdn}

Registrera en CDN-rensnings-API-nyckel på ett självbetjäningssätt och använd den för att göra innehållet ogiltigt på CDN, antingen globalt eller för en eller flera resurser. [Läs mer](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Självbetjäningsskapande av X-AEM-Edge-Key för kundhanterad CDN (BYOCDN) (Early Adopter Program) {#byocdn-keys}

Tidigare krävdes en supportanmälan för att generera den X-AEM-Edge-Key som krävs för att konfigurera ett kundhanterat CDN. Detta kan nu göras på ett självbetjäningssätt genom en konfigurationsfil som distribueras med Configuration Pipeline, vilket tar bort eventuella förseningar när det gäller att komma igång med en ny miljö. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Omdirigeringar på klientsidan (tidig Adobe-program) {#client-side-redirects-early-adopter}

Konfigurera 301/302 klientomdirigeringar i källkontroll och distribuera till CDN. [Läs mer](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observera att det redan finns flera andra funktioner för [CDN-konfiguration](/help/implementing/dispatcher/cdn-configuring-traffic.md), inklusive begäran- och svarsomvandlingar och dirigering av trafik till externa webbplatser.

#### Varningar om trafikfilterregler (tidig Adobe-program) {#traffic-filter-rules-alerts-early-adopter}

Nyligen släppt [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md), som innehåller de valfria reglerna för brandvägg för webbprogram (WAF), låter dig konfigurera vilken trafik som ska tillåtas eller nekas.

Gå med i det tidiga adopterprogrammet så att du kan få varningar när trafikfilterreglerna aktiveras. E-postmeddelanden från Åtgärdscenter håller dig informerad när vissa trafikförhållanden inträffar så att du kan vidta lämpliga åtgärder.

#### Affärsanvändare kan deklarera omdirigeringar utanför Git (Early Adobe Program) {#apache-rewritemaps-early-adopter}

Ungefär som AEM 6.5, kommer Apache/dispatcher att importera omskrivningskartor som placerats på en viss plats i publiceringsdatabasen och läsa in dem, utan att någon pipeline-körning för webbnivån krävs. Detta öppnar möjligheter för en affärsanvändare att deklarera omdirigeringar med antingen ett kalkylblad eller ett användargränssnitt, som det som erbjuds av ACS Commons Redirect Map Manager eller som skapas som en del av ett kundprogram. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) för inläsning av dynamiskt innehåll (tidig Adobe-program) {#esi-early-adopter}

Hanterad CDN i Adobe har nu stöd för [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), ett markeringsspråk för sammanställning av dynamiskt webbinnehåll på kantnivå. Genom att ta med ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, medan du oftare hämtar mindre avsnitt från ursprungsläget som kräver högre uppdateringsintervall (nedre TTL-värden). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Stödlinjer {#guides}

* **Publicera ett ämne eller dess element till ett Experience Fragment**
Nu kan du publicera ett ämne eller dess element i ett Experience Fragment med hjälp av Experience Manager Guides. En Experience Fragment är en modulär innehållsenhet som integrerar både innehåll och layout.  Experience Fragments är avgörande och kan hjälpa er att skapa enhetliga och engagerande upplevelser.
* **Möjlighet att skicka metadata för ämnesresursen till utdata från Native PDF**
Du kan lägga till metadata för ämnesresursen när du genererar utdata för Native PDF. Med den här funktionen kan du lägga till specifika metadata för olika ämnen, som ämnesrubrik och författare, i avsnittets sidhuvuden och sidfötter.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Frigör färdplan för Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/en/docs/release-notes/experience-cloud/current).
Om du vill få ett månatligt e-postmeddelande om uppdateringar av versionsinformation för Experience Cloud prenumererar du på [Produktuppdatering Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html).
