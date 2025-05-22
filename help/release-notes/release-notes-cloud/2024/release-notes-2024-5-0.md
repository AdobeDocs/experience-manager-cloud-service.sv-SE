---
title: Versionsinformation om 2024.5.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2024.5.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 7b7a27f9-ba57-4eb2-9fcb-653b5213af04
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '1943'
ht-degree: 0%

---

# Versionsinformation 2024.5.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.5.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=sv-SE) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.5.0) är 30 maj 2024. Nästa version (2024.6.0) är planerad till 27 juni 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon om versionsöversikten från maj 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3448066?quality=12&captions=swe)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner på webbplatser {#sites-new-features}

#### AEM Translation Integration {#translation-integration}

Översättningsåtgärder och arbetsflöden för innehåll utlöser nu händelser som gör det möjligt att spåra relevanta processsteg och tillstånd från externa program. Följande händelser genereras. Användare kan prenumerera på evenemang med Adobe Developer Console.

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

#### Drifttelemetritjänst {#real-use-monitoring}

* **[Drifttelemetritjänsten är nu GA](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** som aktiverar datainsamling på klientsidan för AEM as a Cloud Service.
Tjänsten Real Use Monitoring, kundsidessamlingen, ger en mer exakt återgivning av interaktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det ger kunder med avancerade insikter om sidtrafik och prestanda. Det är en utmärkt möjlighet att lära sig mer om hur sidan fungerar och få insikter för att förbättra den.

#### AEM Authoring for Edge Delivery Services {#edge-enhancements}

Förbättrad stabilitet och olika förbättringar för en bättre redigeringsupplevelse.

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktion, [generera varianter](/help/generative-ai/generate-variations.md), som nu är tillgängliga i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ditt Adobe-kontoteam och ta del av ditt bidrag i programmet.

**Resurssökning i Content Fragment Console**

Innehållsförfattare kan nu bläddra bland, visa och vidta åtgärder för bilder och andra resurser utan att behöva lämna konsolen Innehållsfragment.

![Resurssökning](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till aemcs-headless-adopter@adobe.com från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i administrationsvyn {#admin-view-new-features}

* WebM är nu en utdatafil som stöds i bearbetningsprofilen för video.
* MP4 stöds nu i den inbyggda integreringen av AEM i Express (import och export).

### Nya funktioner i vyn Assets {#assets-view-new-features}

**Publicera resurser på AEM och Dynamic Media**

Med Experience Manager Assets kan du nu snabbt [publicera resurser till Experience Manager och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) med Assets-vyn utan att växla till administrationsvyn. Du kan publicera resurser när du överför, bläddrar bland och söker efter resurser.

![kontrollera publiceringsstatus1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nya funktioner i förhandsversionen av AEM Forms {#forms-new-prerelease-features}

#### Förbättrad Visual Rule Editor för Core Component Based Adaptive Forms

Den här versionen innebär en betydande uppgradering av den visuella regelredigeraren för adaptiva formulär baserade på kärnkomponenter. Du kan nu:

* Skapa regler i redigeraren för visuell regel för att [åsidosätta standardmeddelanden om att formuläret har skickats in eller misslyckats](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* I den adaptiva Forms-regelredigeraren lade till möjligheten att [välja olika typer av fält för WHEN-åtgärden](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* En formulärförfattare kan nu använda anpassade funktioner på [förbearbeta data innan de skickas in](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Använd funktionen [**Spara som utkast**](/help/forms/save-core-component-based-form-as-draft.md) om du vill spara delvis ifyllda formulär som kan skickas senare. Detta är användbart i scenarier där användare måste avbryta ifyllandet av ett formulär och komma tillbaka till det senare.



### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna åt alla andra och hjälper dig att utveckla dem. Programmet ger tillgång till flera innovationer.

I den här versionsinformationen listas de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### Förbättrade skyddsmetoder för robotar

AEM Forms har förbättrat sina säkerhetsfunktioner genom att lägga till stöd för två populära CAPTCHA-lösningar: Cloudflare Turnstile och hCaptcha. Detta lägger till Google reCAPTCHA, som ger användarna större valfrihet och flexibilitet när det gäller att skydda sina formulär mot inskickade bidrag från skräppost.

* **Cloudflare Turnstle**: Den här friktionslösa CAPTCHA verifierar användare genom en enkel utmaning som inte kräver explicit interaktion. De kan integreras smidigt i formulären och förbättrar användarupplevelsen.
* **hCaptcha**: Denna sekretessfokuserade CAPTCHA erbjuder ett användarvänligt alternativ med fokus på datasekretess. Syftet är att skapa en balans mellan säkerhet och användarupplevelse.
* **Google reCAPTCHA**: AEM Forms har fortsatt stöd för både reCAPTCHA v2 och reCAPTCHA Enterprise, vilket är en tillförlitlig och väletablerad lösning.

Genom att erbjuda flera CAPTCHA-alternativ har AEM Forms gett dig möjlighet att välja den lösning som bäst passar just dina behov.

Vill du integrera någon av dessa CAPTCHA-lösningar med din adaptiva Forms? I vår dokumentation finns detaljerade anvisningar för varje: [Cloudflare Turnstile](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) och [Google reCAPTCHA](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Forms Service

Forms-tjänsten genererar interaktiv PDF forms för datainhämtning. Den kan också användas för att importera eller exportera data till och från ett befintligt interaktivt PDF-formulär och validera skickade data. Här är en beskrivning av funktionaliteten:

* **Återge Forms**: Generera ett interaktivt PDF-formulär från en mall som skapats med AEM Forms Designer och, eventuellt, XML-data. Detta skapar i stort sett ett ifyllbart PDF-formulär som kan fyllas i med data.
* **Dataextrahering och import**: Importera data till ett befintligt PDF-formulär och extrahera data från ett ifyllt PDF-formulär. Både XDP- och XML-dataformat stöds, och import till icke-XFA PDF forms (även kallat AcroForms) stöder dessutom FDF- och XFDF-data.
* **Dataverifiering**: Verifiera skickade data i XDP- eller XML-format mot en mall som skapats med AEM Forms Designer.

>[!IMPORTANT]
>
> Om du är intresserad av att delta i vårt Tidig åtkomst-program för tidig åtkomst skickar du ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) för att begära åtkomst. Du kan begära åtkomst till alla eller alla specifika innovationer.


## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### OAuth Server-till-Server-autentiseringsuppgifter för AEM-integrering med andra Adobe-lösningar {#S2S-OAuth-credentials}

Adobe Developer Console används för att generera autentiseringsuppgifter för att komma åt olika API:er. En av autentiseringstyperna, JWT (Service Account), har ersatts med autentiseringsuppgifter för OAuth Server-till-Server, som AEM Cloud-tjänsten nu stöder för integrering med andra Adobe-lösningar som Adobe Analytics och Adobe Target.

[Läs om borttagningen](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) och [lär dig hur du använder användargränssnittet för AEM-författare](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) för att konfigurera integreringar med andra Adobe-lösningar.

### Trafikrasch vid ursprungsvarningar {#traffic-spike-origin}

[Ta emot proaktiva meddelanden](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) via Åtgärdscenter när trafikmönster på origo indikerar en DDoS-attack, så att du kan undersöka och konfigurera trafikfilterregler.

### Nya funktioner för RDE {#RDE-new-features}

[Med Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) kan utvecklare snabbt distribuera, granska och testa ändringar i molnet. Flera nya funktioner kommer att lanseras under juni-månaden. Du kan även kontakta Adobe tekniker direkt på [RDE Discord-kanalen](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### RDE-stöd för frontkod med hjälp av webbplatsteman och webbplatsmallar {#rde-frontend}

[De lokala lagringsplatserna har nu stöd för slutkod](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) baserat på [webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) och [webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) för användare som använder tidigare. Med RDE:er görs detta med hjälp av ett kommandoradsdirektiv i stället för en [frontendpipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### Förbättrad loggning för RDE {#rde-logging}

När du felsöker kod i en RDE kan utvecklare nu [konfigurera och strömma loggar mer produktivt](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging) med kommandoraden och utan att ändra OSGI-egenskaper i versionskontrollen. Funktioner:

* deklarera loggnivåer per paket eller klassnivå
* anpassa loggutdataformatet
* strömma flera loggar parallellt

#### Förbättringar av RDE CLI {#rde-cli-enhancements}

Gränssnittet för RDE-kommandoraden har några nya funktioner som förbättrar utvecklarupplevelsen:

* [kommandot setup är interaktivt](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive) vilket gör det enklare att välja mellan organisationer, program och miljöer. Nu går det även att åsidosätta dessa värden på kommandoraden.
* [tyst läge](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) för mindre utförliga utdata.
* [json-läge](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) för användbara utdata när de anropas programmatiskt.

### Nya meddelanden från Åtgärdscenter {#actions-center-notifications}

[Åtgärdscenter](/help/operations/actions-center.md) skickar e-postmeddelanden när viktiga incidenter inträffar, eller om vi noterar något om koden eller konfigurationen där du bör vidta förebyggande åtgärder. Det finns tre nya typer av meddelanden:

* för många utgående anslutningar via avancerad nätverksinfrastruktur
* användning av ett föråldrat tjänstanvändarmappningsformat
* en potentiell DDoS-attack pågår

### Tidiga Adobe-program {#foundation-early-adopter}

Mejla **<aemcs-cdn-config-adopter@adobe.com>** som anger vilket av de tidiga adopterprogrammen nedan du är intresserad av.

#### Rensa innehåll på CDN med en självbetjäningsnyckel (Early Adobe Program) {#purge-cdn}

Registrera en CDN-rensnings-API-nyckel på ett självbetjäningssätt och använd den för att göra innehållet ogiltigt på CDN, antingen globalt eller för en eller flera resurser. [Läs mer](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Självbetjäningsskapande av X-AEM-Edge-Key för kundhanterad CDN (BYOCDN) (Early Adobe Program) {#byocdn-keys}

Tidigare krävdes en supportanmälan för att generera den X-AEM-Edge-Key som krävs för att konfigurera ett kundhanterat CDN. Detta kan nu göras på ett självbetjäningssätt genom en konfigurationsfil som distribueras med Configuration Pipeline, vilket tar bort eventuella förseningar när det gäller att komma igång med en ny miljö. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Omdirigeringar på serversidan (tidig Adobe-program) {#server-side-redirects-early-adopter}

Konfigurera 301/302 serveromdirigeringar i källkontroll och distribuera till CDN. [Läs mer](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observera att det redan finns flera andra funktioner för [CDN-konfiguration](/help/implementing/dispatcher/cdn-configuring-traffic.md), bland annat omvandlingar av begäranden och svar samt routning av trafik till platser utanför AEM.

#### Varningar om trafikfilterregler (tidig Adobe-program) {#traffic-filter-rules-alerts-early-adopter}

Med de nyligen släppta [trafikfilterreglerna](/help/security/traffic-filter-rules-including-waf.md), som innehåller de valfria brandväggsreglerna för webbprogram (WAF), kan du konfigurera vilken trafik som ska tillåtas eller nekas.

Gå med i det tidiga adopterprogrammet så att du kan få varningar när trafikfilterreglerna aktiveras. E-postmeddelanden från Åtgärdscenter håller dig informerad när vissa trafikförhållanden inträffar så att du kan vidta lämpliga åtgärder.

#### Affärsanvändare kan deklarera omdirigeringar utanför Git (Early Adobe Program) {#apache-rewritemaps-early-adopter}

På liknande sätt som i AEM 6.5, kommer Apache/dispatcher att importera omskrivningskartor som placerats på en viss plats i publiceringsdatabasen och läsa in dem, utan att någon implementering av en pipeline på webbnivå krävs. Detta öppnar möjligheter för en affärsanvändare att deklarera omdirigeringar med antingen ett kalkylblad eller ett användargränssnitt, som det som erbjuds av ACS Commons Redirect Map Manager eller som skapas som en del av ett kundprogram. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) for Loading Dynamic Content (Early Adobe Program) {#esi-early-adopter}

Adobe hanterade CDN har nu stöd för [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), ett markeringsspråk för dynamisk sammanställning av webbinnehåll på kantnivå. Genom att inkludera ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, samtidigt som du oftare hämtar de mindre avsnitt som kräver högre uppdateringsfrekvens (lägre TTL-värden) från ursprungsläget. <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] stödlinjer {#guides}

* **Publicera ett ämne eller dess element till ett Experience Fragment**
Nu kan du publicera ett ämne eller dess element i ett Experience Fragment i Experience Manager Guides. En Experience Fragment är en modulär innehållsenhet som integrerar både innehåll och layout.  Experience Fragments är avgörande och kan hjälpa er att skapa enhetliga och engagerande upplevelser.
* **Möjlighet att skicka metadata för ämnesresursen till inbyggda PDF-utdata**
Du kan lägga till metadata för ämnesresursen när du genererar inbyggda PDF-utdata. Med den här funktionen kan du lägga till specifika metadata för olika ämnen, som ämnesrubrik och författare, i avsnittets sidhuvuden och sidfötter.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/sv/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/sv/docs/release-notes/experience-cloud/current).
Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).
