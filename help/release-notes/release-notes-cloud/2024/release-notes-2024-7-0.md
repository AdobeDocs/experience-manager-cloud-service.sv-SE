---
title: Versionsinformation om 2024.7.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2024.7.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 6194df9d-8c3c-4c7f-be59-099b970a565a
source-git-commit: 47b6d7871201cd7dbc1db77620879e69bce4ad3a
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 0%

---

# Versionsinformation 2024.7.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.7.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2022 eller 2023.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

The release date of [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] current feature release (2024.7.0) is July 25, 2024. The next feature release (2024.8.0) is planned for August 29, 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Have a look at the July 2024 Release Overview video for a summary of the features added in the 2024.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Ny funktion i Experience Manager Sites {#new-feature-sites}

### Tidiga Adobe-program {#sites-early-adopter}

**Generera variationer**

Utnyttja GenAI genom AEM nya funktion, [generera varianter](/help/generative-ai/generate-variations.md), som nu är tillgängliga i Cloud Service. Generera variationer hjälper er att generera och skala innehåll med hjälp av generativ AI. Kontakta ditt Adobe-kontoteam och ta del av ditt bidrag i programmet.

**Resurssökning i Content Fragment Console**

Innehållsförfattare kan nu bläddra bland, visa och vidta åtgärder för bilder och andra resurser utan att behöva lämna konsolen Innehållsfragment.

![Resurssökning](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till aemcs-headless-adopter@adobe.com från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

**Överför resurser med resursväljaren**

Resursväljaren ger nu innehållsförfattare möjlighet att överföra det slutliga materialet direkt från väljaren, antingen genom att dra eller genom att bläddra i det lokala filsystemet. Den här funktionen gör att det går att överföra det slutliga materialet till DAM från valfritt program.

### Funktion för tidig åtkomst i Dynamic Media {#dm-early-access}

**AI-genererade videobeskrivningar**

AI-genererade videobildtexter i Adobe Dynamic Media använder artificiell intelligens för att automatiskt generera bildtexter för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter i realtid. AI analyserar videons ljudspår för att transkribera tal och skapa bildtexter som kan redigeras för precision eller anpassning. Dessa bildtexter uppfyller tillgänglighetskraven och förbättrar engagemanget för videoklipp som förlitar sig på eller föredrar textbaserat videostöd.

[Skapa och skicka ett Adobe kundsupportärende](/help/assets/dynamic-media/video.md##enable-dash) om du vill få tidig åtkomst till AI-genererade bildtexter på ditt Dynamic Media-konto.

### Nya funktioner i vyn Assets {#assets-view-new-features}

**Integrering av inloggningsuppgifter för innehåll**

Experience Manager Assets har nu stöd för inloggningsuppgifter för bildformat som stöds. Denna möjlighet ger information om resursens innehåll och hur den skapades, inklusive om den ändrades med hjälp av GenAI.

![Autentiseringsuppgifter för innehåll](/help/assets/assets/content-credentials.png)

**Visuella förhandsvisningar av mappinnehåll**

Experience Manager Assets visar nu förhandsvisningar av mappinnehåll i mappminiatyrbilden när du bläddrar eller söker efter innehåll, vilket gör det enklare att hitta resurser som finns i AEM Assets-databasen.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i AEM Forms {#forms-new-prerelease-features}

#### Förbättrad Visual Rule Editor för Core Component Based Adaptive Forms

Adaptive form authors can use repeatable form fields and out-of-the-box visual rule editor functions to create complex business logic in forms without needing customization or support from the development team.

### Tidig åtkomst-funktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna åt alla andra och hjälper dig att utveckla dem. Programmet ger tillgång till flera innovationer.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### Skapa adaptiva formulär med Universal Editor

Använd Adobe Experience Manager [Universal Editor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) för att skapa anpassningsbara formulär med WYSIWYG dra-och-släpp-redigering, för både headless och headful enrollment, som levereras via Edge Delivery Service. Med anpassningsbara formulärförfattare kan man enkelt skapa och starta experiment med varianter av formulären på webbsidorna. Detta gör att de kan avgöra vilka upplevelser som fungerar bäst för slutanvändarna.

>[!IMPORTANT]
>
> Om du är intresserad av att delta i Adobe Tidig åtkomst-program för tidig åtkomst skickar du ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) för att begära åtkomst. Du kan begära åtkomst till alla eller alla specifika innovationer.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Rensa innehåll vid CDN med en självserverbaserad API-nyckel {#purge-cdn}

Att ställa in TTL med HTTP-huvudet Cache-Control är ett effektivt sätt att balansera innehållets leveransprestanda och innehållets aktualitet. I scenarier där det är viktigt att leverera uppdaterat innehåll omedelbart kan det dock vara bra att rensa CDN-cachen direkt.

[Lär dig hur](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) kan självbetjäna konfigurationen av en rensnings-API-token med hjälp av Cloud Manager konfigurationsflöde, så att du kan [anropa rensnings-API:er](/help/implementing/dispatcher/cdn-cache-purge.md), med någon av dessa varianter:

* En URL
* Flera URL-adresser som använder en tagg
* Rensa fullständigt CDN-cache

### Self-Serve Configuration of X-AEM-Edge-Key for Customer-Managed CDN {#customermanaged-keys}

Tidigare krävdes en supportanmälan för att generera den X-AEM-Edge-Key som krävs för att konfigurera ett kundhanterat CDN. Det här arbetsflödet är nu självbetjäning genom att deklarera nyckelvärdet i en konfigurationsfil som distribueras med Configuration Pipeline, vilket tar bort eventuella förseningar när det gäller att starta en ny miljö. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

### Varningar om trafikfilterregler {#traffic-filter-rules-alerts}

Trafikfilterregler, som innehåller de valfria brandväggsreglerna för webbprogram (WAF), gör att du kan konfigurera vilken trafik som ska blockeras.

Nu kan du [prenumerera på aviseringar](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts) när trafikfilterreglerna aktiveras. E-postmeddelanden från Åtgärdscenter håller dig informerad om när vissa trafikförhållanden inträffar så att du kan vidta lämpliga åtgärder.

### Content Delivery related Tire Adobe Programs {#foundation-early-adopter}

Mejla **<aemcs-cdn-config-adopter@adobe.com>** som anger vilket av de tidiga adopterprogrammen nedan du är intresserad av.

#### Grundläggande autentisering vid CDN (Early Adobe Program) {#basicauth-cdn}

Skydda vissa innehållsresurser genom att öppna en enkel dialogruta för autentisering som kräver ett användarnamn och lösenord. Den här funktionen riktar sig främst till användarvänliga fall av autentisering, som affärsintressenter som granskar innehåll, i stället för att fungera som en heltäckande lösning för slutanvändarnas åtkomsträttigheter. Listan över användarnamn och lösenord som hanteras via en konfigurationsfil i Git som distribueras via Configuration Pipeline, med en referens till Cloud Manager-miljövariabler av hemlig typ. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Serveromdirigeringar (tidig Adobe-program) {#server-side-redirects-early-adopter}

Konfigurera 301/302 serveromdirigeringar i källkontroll och distribuera till CDN. [Läs mer](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observera att det redan finns flera andra funktioner för [CDN-konfiguration](/help/implementing/dispatcher/cdn-configuring-traffic.md), bland annat omvandlingar av begäranden och svar samt routning av trafik till platser utanför AEM.

#### Affärsanvändare kan deklarera omdirigeringar utanför Git (tidig Adobe-program) {#apache-rewritemaps-early-adopter}

Ungefär som i AEM 6.5 skriver Apache/dispatcher ingest om kartor som placerats på en viss plats i publiceringsdatabasen och läser in dem, utan att någon pipeline-körning behövs på webbnivån. På så sätt kan företagsanvändare deklarera omdirigeringar med hjälp av ett kalkylblad eller ett gränssnitt, som ACS Commons Redirect Map Manager eller ett anpassat program. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) for Loading Dynamic Content (Early Adobe Program) {#esi-early-adopter}

Adobe hanterade CDN har nu stöd för [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), ett markeringsspråk för dynamisk sammanställning av webbinnehåll på kantnivå. Genom att inkludera ESI-fragment kan du cachelagra hela HTML-sidan vid CDN med högre TTL-värden, samtidigt som du oftare hämtar de mindre avsnitt som kräver högre uppdateringsfrekvens (lägre TTL-värden) från ursprungsläget. <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

### Meddelanden från Content Health Related Actions Center om tidiga Adobe-program {#actions-center-notifications}

[Åtgärdscenter](/help/operations/actions-center.md) skickar e-postmeddelanden när viktiga incidenter inträffar, eller om något om koden eller konfigurationen visas, där du bör vidta förebyggande åtgärder. Adobe har nu introducerat flera nya typer av meddelanden som är kopplade till din innehållshälsa. Den här funktionen är tillgänglig via ett program som tagits i bruk tidigt. Kontakta Adobe kundtjänst om du vill delta.

#### Sidorna innehåller ett stort antal noder {#page-nodes}

Ett stort antal noder kan försämra återgivningsprestanda och minska sidinläsningstiden. Ta emot ett proaktivt meddelande via Åtgärdscenter när ett stort antal noder identifieras på en sida, vilket gör att du kan vidta nödvändiga åtgärder för att minska det totala antalet noder på en sida.

#### Stort antal arbetsflödesinstanser som körs {#running-workflows}

Arbetsflödesmotorns prestanda påverkas om det finns ett stort antal arbetsflöden som körs i redigeringsmiljön. Du får ett proaktivt meddelande via Åtgärdscenter när ett stort antal arbetsflödesinstanser som körs identifieras. Med den här processen kan du konfigurera ett rensningsjobb så att onödiga arbetsflöden avbryts.

#### Användare som lagts till direkt i anpassade grupper {#users-customgroups}

Du får ett proaktivt meddelande via Åtgärdscenter när användare läggs till direkt i anpassade grupper. Med den här processen kan du följa de bästa IMS-metoderna genom att lägga till användare i relevanta IMS-grupper och sedan inkludera dessa IMS-grupper som medlemmar i AEM-grupper.

#### JCR-innehåll saknas {#jcr-content}

Åtgärdscenter meddelar dig aktivt när JCR-innehåll saknas. På så sätt kan du lägga till innehåll som saknas och förhindra att vissa AEM Assets-funktioner misslyckas.

#### Slutförda arbetsflöden har inte rensats {#workflows}

Åtgärdscenter meddelar dig aktivt när slutförda arbetsflöden som är över 90 dagar gamla inte har rensats. Den här metoden hjälper till att förbättra prestanda för arbetsflödesmotorn genom att minska antalet arbetsflödesinstanser.

#### Sling-resurs saknas {#sling-resource}

Actions Center meddelar dig aktivt när en saknad Sling-resurs upptäcks. På så sätt kan du lägga till den saknade resursen och förhindra fel i vissa AEM Assets-funktioner.

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
