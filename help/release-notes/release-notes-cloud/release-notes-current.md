---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a2cdc7c4e9d3dfd52ca76afcf951fa67b279918a
workflow-type: tm+mt
source-wordcount: '771'
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

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.5.0) är 9 juni 2022.
Nästa version (2022.6.0) är planerad till 30 juni 2022.

## Släpp video {#release-video}

Titta på videon om versionsöversikten från maj 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] prerelease channel {#prerelease-features-sites}

* Olika GraphQL-funktioner
* En ny konsol som är optimerad för Headless-användning av Content Fragments

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [Dynamic Media Smart Imaging](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) har nu stöd för AVIF-filformat - ytterligare förbättring av Google Core Web Vital (Störst Contentful Paint), med AVIF som ger 20 % extra storleksminskning jämfört med WebP. Totalt ger AVIF upp till 41 % genomsnittlig storleksminskning över JPEG (i vissa bilder till och med upp till 76 %).

* [!UICONTROL Experience Manager Assets Brand Portal] kör nu automatiska jobb var tolfte timme för att ta bort alla Brand Portal-resurser som publicerats till AEM. Därför behöver du inte ta bort resurserna i Contribute-mappen manuellt för att mappstorleken ska hållas under tröskelvärdet. Se [Nyheter i Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

### Nya funktioner i [!DNL Assets] prerelease channel {#prerelease-features-assets}

Experience Manager Assets använder Adobe Sensei AI-funktioner hittills [skilja på färger i en bild och använda dem som taggar automatiskt vid förtäring](../../assets/color-tag-images.md). Dessa taggar möjliggör förbättrad sökning baserat på bildens färgkomposition. Du kan konfigurera antalet färger, inom ett intervall av en till fyrtio, som är taggade till en bild så att du kan söka efter bilder baserade på dessa färger senare.


## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* **Integrera adaptiv Forms med Microsoft® Power Automate**: Nu kan du konfigurera ett adaptivt formulär så att det kör ett Microsoft® Power Automate Cloud-flöde när du skickar in det. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

* **Guide för att skapa ett adaptivt formulär**: Du kan använda en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden ger dig en snabb fliknavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

   ![Guide för att skapa ett adaptivt formulär](/help/release-notes/assets/wizard.png)

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Ny egenskapssida för produktcockpit för bättre och enklare översikt

![översikt över egenskaper för produktcockpit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Förbättrad kompatibilitet och tillförlitlighet för anslutningar från tredje part vid I/O-körning

* Förbättrat stöd för överskrivningar av GQL-klientkonfiguration (t.ex. ange anpassad cachelagring)

### Felkorrigeringar {#bug-fixes-cif}

* Produktväljarfältet för flera värden visar att andra och ytterligare produkter är ogiltiga

* Produktväljaren döljs ibland bakom komponenter

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Vad är nytt? {#what-is-new-foundation}

* Alternativet Lägg till träd under administratörsskärmen för replikeringsagenten **Fliken Distribuera** som tidigare meddelats som utgått, kommer att tas bort den 20 juni 2022 eller snart därefter. Paket med en trädhierarki av innehåll bör i stället replikeras med [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Arbetsflödet Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow).

* Användning av administratörsskärmen för replikeringsagenten eller replikerings-API:t för distribution av innehållspaket som är större än 10 MB (noder med egenskaper, exklusive binärfiler) är föråldrat och kommer att tillämpas den 12 september 2022 eller snart därefter. Istället [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Arbetsflödet Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) måste användas för att replikera dessa stora innehållspaket. I juli visas ett varningsmeddelande på administratörsskärmen för replikeringsagenten **Fliken Distribuera** om du försöker replikera dessa stora innehållspaket och även i AEM fellogg när replikerings-API används för att replikera dessa stora innehållspaket. I september kommer varningar att ersättas av fel. Justera processerna därefter.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Security {#foundation-security}

### Borttagning av TLS 1.0, 1.1

Från och med den 30 juni 2022 kommer Experience Manager as a Cloud Service att kräva säkrare nätverkskommunikation och datautbyte med användarsystem. AEM använder enbart TLS (Transport Layer Security), 1.2-protokollet. Äldre TLS-versioner 1.0 och 1.1 kommer att bli inaktuella.

Om du fortsätter att använda äldre versioner av TLS som 1.0, 1.1 kan du förlora åtkomsten till Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
