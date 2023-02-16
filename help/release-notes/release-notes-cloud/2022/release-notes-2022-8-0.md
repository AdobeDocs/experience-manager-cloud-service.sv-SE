---
title: Versionsinformation för 2022.8.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för 2022.8.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
source-git-commit: 7b21a8af886c8e1f209e3b7cc5d94de5c58be1ac
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.8.0) är 1 september 2022.
Nästa version (2022.10.0) är planerad till 10 november 2022.

## Släpp video {#release-video}

Titta på videon Augusti 2022 Release Overview om du vill se en sammanfattning av funktioner som lagts till i version 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* Med e-postkomponenten kan du skapa innehåll i AEM som sedan levereras som e-post via Campaign Classic. Huvudkomponenten för e-post:
   * baseras på [Core WCM Component](https://github.com/adobe/aem-core-wcm-components) som har stöd för redigerbara mallar och stilsystemet.
   * innehåller 10 e-postoptimerade produktionsklara komponenter (Page, Container, Title, Text, Image, Button, Teaser, Experience Fragment, Content Fragment, Segmentation).
   * ger avancerad personalisering och segmentering tack vare [infogning av Campaign-variabler](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) i de flesta dialogrutefälten och i de flexibla [Segmenteringskomponent](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * ger optimala e-postvänliga HTML-resultat tack vare [Inline för CSS-format](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), [Inliner för HTML-attribut](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)och [HTML sanitizer](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * gör det möjligt att skapa e-postmeddelanden var som helst.

### Nya funktioner i [!DNL Sites] prerelease channel {#prerelease-features-sites}

* The [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ger användarna möjlighet att visa det totala antalet språkkopior som är associerade med ett innehållsfragment. Åtkomst med ett klick har tillhandahållits för att visa alla språkkopior också. Användarna kan också filtrera tabellvyn efter de språkområden de är intresserade av.

![Språk för innehållsfragment](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#features-assets}

* Nu kan du konfigurera Adobe Experience Manager Assets till [begränsa vilken typ av resurser som användare kan överföra baserat på MIME-typen](/help/assets/configure-asset-upload-restrictions.md).

   ![Begränsningar för överföring av tillgångar](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* [Adaptiv Forms-guide](/help/forms/creating-adaptive-form.md): AEM Forms har en användarvänlig guide för att snabbt skapa Adaptive Forms. Guiden har en snabb fliknavigering där du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär. Den här versionen innehåller följande förbättringar av guiden:

   * Markera eller avmarkera fält: Med guiden kan du skapa ett adaptivt formulär baserat på scheman för JSON och Formulärdatamodell. Nu kan du markera delmängder av fält i ett schema som ska inkluderas i ett anpassat formulär. De markerade fälten konverteras till motsvarande komponenter för datainhämtning från adaptiva formulär för att snabbt skapa de anpassade formulären.

   * Använd statiska mallar: Kunder som har investerat i statiska mallar kan fortsätta använda molnet genom att använda statiska mallar i guiden för att skapa anpassade formulär. Detta ger kunderna ytterligare tid att migrera gamla statiska mallar till moderna redigerbara mallar.

* [Ta bort dolda fält från ett DoR-dokument (Document of Record) vid bearbetning på serversidan](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): Du kan generera dokumentet med posten PDF för slutanvändare som bara innehåller de fält som var synliga för dem under datainhämtningen. När formuläret skickas validerar servern vilka fält som dolts för slutanvändaren baserat på inskickade data och utesluter att dokumentet är enhetligt.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Sammanslutning av AEM sidor till produkter och kategorier via AEM sidegenskaper plus en översikt i produktcockpit
   ![association för produktcockpitsida](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här.](/help/implementing/cloud-manager/release-notes/current.md)

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
