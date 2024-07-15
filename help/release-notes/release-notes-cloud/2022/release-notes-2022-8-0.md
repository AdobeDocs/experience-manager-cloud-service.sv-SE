---
title: Versionsinformation för version 2022.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2022.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Versionsinformation 2022.8.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2022.8.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.8.0) är 1 september 2022.
Nästa version (2022.10.0) är planerad till 10 november 2022.

## Släpp video {#release-video}

Titta på videon Augusti 2022 Release Overview om du vill se en sammanfattning av funktioner som lagts till i version 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* Med e-postkomponenten kan du skapa innehåll i AEM som sedan levereras som e-postmeddelanden via Campaign Classic. Huvudkomponenten för e-post:
   * baseras på [Core WCM-komponenten](https://github.com/adobe/aem-core-wcm-components) som stöder redigerbara mallar och formatsystemet.
   * innehåller 10 e-postoptimerade produktionsklara komponenter (Page, Container, Title, Text, Image, Button, Teaser, Experience Fragment, Content Fragment, Segmentation).
   * ger avancerad personalisering och segmentering tack vare att Campaign-variabler [infogas ](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) i de flesta dialogrutefält och den flexibla [segmenteringskomponenten](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * ger optimala e-postvänliga HTML-utdata, tack vare [CSS-formatinlinern](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), [HTML-attributinlinern](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation) och [HTML-saneraren](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * gör det möjligt att skapa e-postmeddelanden var som helst.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Sites] {#prerelease-features-sites}

* [Konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) ger användarna ett alternativ för att visa det totala antalet språkkopior som är associerade med ett innehållsfragment. Åtkomst med ett klick har tillhandahållits för att visa alla språkkopior också. Användarna kan också filtrera tabellvyn efter de språkområden de är intresserade av.

![Språk för innehållsfragment](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#features-assets}

* Du kan nu konfigurera Adobe Experience Manager Assets att [begränsa vilken typ av resurser som användare kan överföra baserat på MIME-typen](/help/assets/configure-asset-upload-restrictions.md).

  ![Resursöverföringsbegränsningar](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

* [Adaptiv Forms-guide](/help/forms/creating-adaptive-form.md): AEM Forms tillhandahåller en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden har en snabb fliknavigering där du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär. Den här versionen innehåller följande förbättringar av guiden:

   * Markera eller avmarkera fält: Med guiden kan du skapa ett adaptivt formulär baserat på JSON- och formulärdatamodellscheman. Nu kan du markera delmängder av fält i ett schema som ska inkluderas i ett anpassat formulär. De markerade fälten konverteras till motsvarande komponenter för datainhämtning från adaptiva formulär för att snabbt skapa de anpassade formulären.

   * Använd statiska mallar: Kunder som har investerat i statiska mallar kan fortsätta använda molnet med statiska mallar i guiden för att skapa anpassade formulär. Detta ger kunderna ytterligare tid att migrera gamla statiska mallar till moderna redigerbara mallar.

* [Ta bort dolda fält från en DoR-fil (Document of Record) vid bearbetning på serversidan](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): Du kan generera dokumentet med posten PDF för slutanvändare som bara innehåller de fält som var synliga för dem vid datainhämtning. När formuläret skickas validerar servern vilka fält som dolts för användaren baserat på inskickade data och utesluter att dokumentet är enhetligt.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Sammanslutning av AEM sidor till produkter och kategorier via AEM sidegenskaper plus en översikt i produktcockpit
  ![association för produktcockpitsida](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
