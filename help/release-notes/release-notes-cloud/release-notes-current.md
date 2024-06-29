---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 1e5a32625377cb564c859a6fdaf1ecef6ebebe9e
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2024.6.0) är 27 juni 2024. Nästa funktionsversion (2024.7.0) är planerad till 25 juli 2024.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Ny funktion i Experience Manager Sites {#new-feature-sites}

**RUM-datatjänst (Real Use Monitoring)** {#real-use-monitoring}

The [RUM-datatjänst (Real Use Monitoring)](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/shwetad-patch-1/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service) är nu allmänt tillgängligt, vilket möjliggör datainsamling på klientsidan för AEM as a Cloud Service. Den här tjänsten ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det ger kunderna avancerade insikter om sidtrafik och prestanda, vilket utgör en värdefull möjlighet att förstå och förbättra sidprestanda.

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktioner, [generera variationer](/help/generative-ai/generate-variations.md), nu i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ert Adobe-kontoteam för att ta del av detta i programmet.

**Resursbläddring i Content Fragment Console**

Innehållsförfattare kan nu bläddra bland, visa och vidta åtgärder för bilder och andra resurser utan att behöva lämna konsolen Innehållsfragment.

![Resurssökning](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till aemcs-headless-adopter@adobe.com från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i Experience Manager Assets {#new-features-assets}



**Content Hub**

Content Hub ingår som en del av Experience Manager Assets as a Cloud Service för att demokratisera tillgången till varumärkesinnehåll för organisationer och deras affärspartners. Med Content Hub kan du enkelt hitta och distribuera material, återanvända och skapa nya varumärkesanpassade varianter och snabba upp aktiveringen i stor skala.

![Content Hub användargränssnitt](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Media med OpenAPI-funktioner**

Dynamic Media med OpenAPI-funktioner utökar DAM-funktionaliteten över Adobe och tredjepartsapplikationer, vilket ger åtkomst till varumärkesgodkända digitala resurser i alla kanaler via resursväljaren eller OpenAPI-stacken. Nyckeltoner - inga binära kopior, resurser optimeras och omformas i toppen för att ge snabba prestanda och resurser som är offentliga eller säkra.

![Nytt dataflödesdiagram för Dynamic Media](/help/assets/assets/dm-openapi-dfd.png)


### Nya funktioner i vyn Assets {#assets-view-new-features}

**Fler alternativ finns på kontrollpanelen för Assets Insights**

Antal tillgångar efter resurstyp och storlek finns nu på instrumentpanelen för Assets Insights. Dessa alternativ levererar realtidsdata i visningsmiljön i Assets. De anger antalet och procentandelen tillgångar per storleksintervall och resurstyp.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nya funktioner i AEM Forms {#forms-new-prerelease-features}

#### Förbättrad Visual Rule Editor för Core Component Based Adaptive Forms

Den här versionen innebär en betydande uppgradering av Visual Rule Editor för adaptiva formulär baserade på kärnkomponenter. Du kan nu:

* Skapa regler i Visual Rule Editor för att [åsidosätta standardmeddelanden om att formuläret har skickats in eller misslyckats](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* I den adaptiva Forms-regelredigeraren har du lagt till möjligheten att [välja olika typer av fält för WHEN-åtgärden](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* En formulärförfattare kan nu använda anpassade funktioner på [bearbeta data innan de skickas](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Använd [**Spara som utkast**](/help/forms/save-core-component-based-form-as-draft.md) funktioner för att spara delvis ifyllda formulär för senare inskickning. Den här funktionen är användbar i scenarier där användare måste avbryta ifyllandet av ett formulär och komma tillbaka till det senare.

### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna åt alla andra och hjälper dig att utveckla dem. Programmet ger tillgång till flera innovationer.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som finns inom programmet för tidig åtkomst finns på [Dokumentation för AEM Forms Early Access Program](/help/forms/early-access-ea-features.md).

#### Förbättrade skyddsmetoder för robotar

AEM Forms har förbättrat sina säkerhetsfunktioner genom att lägga till stöd för två populära CAPTCHA-lösningar: Cloudflare Turnstile och hCaptcha. Den här funktionen kompletterar Google reCAPTCHA och ger användarna ytterligare alternativ. Det ger större flexibilitet när det gäller att skydda sina formulär mot inskickade bidrag från stötar och skräppost.

* **Molnformad vändning**: Denna friktionslösa CAPTCHA verifierar användarna genom en enkel utmaning som inte kräver någon explicit interaktion. De kan integreras smidigt i formulären och förbättrar användarupplevelsen.
* **hCaptcha**: Denna sekretessinriktade CAPTCHA erbjuder ett användarvänligt alternativ med fokus på datasekretess. Syftet är att skapa en balans mellan säkerhet och användarupplevelse.
* **Google reCAPTCHA**: AEM Forms fortsätter att stödja både reCAPTCHA v2 och reCAPTCHA Enterprise, som är en tillförlitlig och väletablerad lösning.

Genom att erbjuda flera CAPTCHA-alternativ har AEM Forms gett dig möjlighet att välja den lösning som bäst passar just dina behov.

Vill du integrera någon av dessa CAPTCHA-lösningar med din adaptiva Forms? Adobe-dokumentation innehåller detaljerade anvisningar för varje: [Molnformad vändning](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)och [Google reCAPTCHA](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Forms Service

Forms-tjänsten genererar interaktiv PDF forms för datainhämtning. Den kan också användas för att importera eller exportera data till och från ett befintligt interaktivt PDF-formulär och validera skickade data. Här är en beskrivning av funktionaliteten:

* **Återger Forms**: Generera ett interaktivt PDF-formulär från en mall som skapats med AEM Forms Designer och, eventuellt, XML-data. Den här funktionen skapar ett ifyllbart PDF-formulär som kan fyllas i med data.
* **Extrahering och import av data**: Importera data till ett befintligt PDF-formulär och extrahera data från ett ifyllt PDF-formulär. Både XDP- och XML-dataformat stöds, och import till icke-XFA PDF forms (kallas även AcroForms) stöder dessutom FDF- och XFDF-data.
* **Dataverifiering**: Validera skickade data i XDP- eller XML-format mot en mall som skapats med AEM Forms Designer.

>[!IMPORTANT]
>
> Om du är intresserad av att gå med i Adobe Tidig Access Program för tidig åtkomst skickar du ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) för att begära åtkomst. Du kan begära åtkomst till alla eller alla specifika innovationer.


## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Meddelanden från Content Health Related Actions Center om tidiga Adobe-program {#actions-center-notifications}

[Actions Center](/help/operations/actions-center.md) skickar e-postmeddelanden när viktiga incidenter inträffar eller om något om koden eller konfigurationen visas, där du bör vidta proaktiva åtgärder. Adobe har nu introducerat flera nya typer av meddelanden som är kopplade till din innehållshälsa. Den här funktionen är tillgänglig via ett program som tagits i bruk tidigt. Kontakta Adobe kundtjänst om du vill delta.

#### Sidorna innehåller ett stort antal noder {#page-nodes}

Ett stort antal noder kan försämra återgivningsprestanda och minska sidinläsningstiden. Ta emot ett proaktivt meddelande via Åtgärdscenter när ett stort antal noder identifieras på en sida, vilket gör att du kan vidta nödvändiga åtgärder för att minska det totala antalet noder på en sida.

#### Stort antal arbetsflödesinstanser som körs {#running-workflows}

Arbetsflödesmotorns prestanda påverkas om det finns ett stort antal arbetsflöden som körs i redigeringsmiljön. Du får ett proaktivt meddelande via Åtgärdscenter när ett stort antal arbetsflödesinstanser som körs identifieras. Med den här processen kan du konfigurera ett rensningsjobb så att onödiga arbetsflöden avbryts.

#### Användare som lagts till direkt i anpassade grupper {#users-customgroups}

Du får ett proaktivt meddelande via Åtgärdscenter när användare läggs till direkt i anpassade grupper. Med den här processen kan du följa de bästa IMS-metoderna genom att lägga till användare i relevanta IMS-grupper och sedan inkludera dessa IMS-grupper som medlemmar i AEM.

#### JCR-innehåll saknas {#jcr-content}

Åtgärdscenter meddelar dig aktivt när JCR-innehåll saknas. På så sätt kan du lägga till innehåll som saknas och förhindra att vissa AEM Assets-funktioner misslyckas.

#### Slutförda arbetsflöden har inte rensats {#workflows}

Åtgärdscenter meddelar dig aktivt när slutförda arbetsflöden som är över 90 dagar gamla inte har rensats. Den här metoden hjälper till att förbättra prestanda för arbetsflödesmotorn genom att minska antalet arbetsflödesinstanser.

#### Sling-resurs saknas {#sling-resource}

Actions Center meddelar dig aktivt när en saknad Sling-resurs upptäcks. På så sätt kan du lägga till den saknade resursen och förhindra fel i vissa AEM Assets-funktioner.

### Content Delivery related Tire Adobe Programs {#foundation-early-adopter}

E-post **<aemcs-cdn-config-adopter@adobe.com>**, vilket av de tidiga adopterprogrammen nedan du är intresserad av.

#### Grundläggande autentisering vid CDN (Early Adobe Program) {#basicauth-cdn}

Protect vissa innehållsresurser genom att öppna en enkel autentiseringsdialogruta som kräver användarnamn och lösenord. Den här funktionen riktar sig främst till användarvänliga fall av autentisering, som affärsintressenter som granskar innehåll, i stället för att fungera som en heltäckande lösning för slutanvändarnas åtkomsträttigheter. Listan över användarnamn och lösenord som hanteras via en konfigurationsfil i Git som distribueras via Configuration Pipeline, med en referens till Cloud Manager-miljövariabler av hemlig typ. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Rensa innehåll på CDN med en självbetjäningsnyckel (Early Adobe Program) {#purge-cdn}

Registrera en CDN-rensnings-API-nyckel på ett självbetjäningssätt och använd den för att göra innehållet ogiltigt på CDN, antingen globalt eller för en eller flera resurser. [Läs mer](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Självserverframtagning av X-AEM-Edge-nyckel för kundhanterat CDN (BYOCDN) (tidig Adobe-program) {#byocdn-keys}

Tidigare krävdes en supportanmälan för att generera den X-AEM-Edge-Key som krävs för att konfigurera ett kundhanterat CDN. Resultatet kan nu uppnås på ett självbetjäningssätt genom en konfigurationsfil som distribueras med Configuration Pipeline, vilket tar bort eventuella förseningar när det gäller att komma igång med en ny miljö. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Omdirigeringar på klientsidan (tidigt Adobe-program) {#client-side-redirects-early-adopter}

Konfigurera 301/302 klientomdirigeringar i källkontroll och distribuera till CDN. [Läs mer](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observera att det redan finns flera andra funktioner för [CDN-konfiguration](/help/implementing/dispatcher/cdn-configuring-traffic.md), inklusive begäran- och svarsomvandlingar och dirigering av trafik till externa webbplatser.

#### Varningar om trafikfilterregler (tidig Adobe-program) {#traffic-filter-rules-alerts-early-adopter}

Nyligen släppt [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md), som innehåller de valfria reglerna för brandvägg för webbprogram (WAF), låter dig konfigurera vilken trafik som ska tillåtas eller nekas.

Gå med i det tidiga adopterprogrammet så att du kan få varningar när trafikfilterreglerna aktiveras. E-postmeddelanden från Åtgärdscenter håller dig informerad om när vissa trafikförhållanden inträffar så att du kan vidta lämpliga åtgärder.

#### Affärsanvändare kan deklarera omdirigeringar utanför Git (tidig Adobe-program) {#apache-rewritemaps-early-adopter}

Ungefär som AEM 6.5, skriver Apache/dispatcher ingest om kartor som placerats på en viss plats i publiceringsdatabasen och läser in dem, utan att någon pipeline-körning behövs på webbnivån. På så sätt kan företagsanvändare deklarera omdirigeringar med hjälp av ett kalkylblad eller ett gränssnitt, som ACS Commons Redirect Map Manager eller ett anpassat program. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) for Loading Dynamic Content (Early Adobe Program) {#esi-early-adopter}

Hanterad CDN i Adobe har nu stöd för [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), ett markeringsspråk för sammanställning av dynamiskt webbinnehåll på kantnivå. Genom att ta med ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, medan du oftare hämtar mindre avsnitt från ursprungsläget som kräver högre uppdateringsintervall (nedre TTL-värden). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/en/docs/release-notes/experience-cloud/current).
Om du vill få ett månatligt e-postmeddelande om uppdateringar av versionsinformation för Experience Cloud prenumererar du på [Produktuppdatering Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html).
