---
title: Versionsinformation för 2022.5.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för 2022.5.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
source-git-commit: fe19e99baa921247f86542c6643c1faf837e7d91
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Versionsinformation 2022.5.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för 2022.5.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.5.0) är 9 juni 2022.
Nästa version (2022.6.0) är planerad till 30 juni 2022.

## Släpp video {#release-video}

Titta på videon om versionsöversikten från maj 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] prerelease channel {#prerelease-features-sites}

* Olika GraphQL-funktioner
* A [ny konsol](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) optimerad för Headless-användning av Content Fragments

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [Dynamic Media Smart Imaging](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) har nu stöd för AVIF-filformat - ytterligare förbättring av Google Core Web Vital (Störst Contentful Paint), med AVIF som ger 20 % extra storleksminskning jämfört med WebP. Totalt ger AVIF upp till 41 % genomsnittlig storleksminskning över JPEG (i vissa bilder till och med upp till 76 %).

* [!UICONTROL Experience Manager Assets Brand Portal] kör nu automatiska jobb var tolfte timme för att ta bort alla Brand Portal-resurser som publicerats till AEM. Därför behöver du inte ta bort resurserna i Contribute-mappen manuellt för att mappstorleken ska hållas under tröskelvärdet. Se [Nyheter i Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

### Nya funktioner i [!DNL Assets] prerelease channel {#prerelease-features-assets}

Experience Manager Assets använder Adobe Sensei AI-funktioner hittills [skilja på färger i en bild och använda dem som taggar automatiskt vid förtäring](/help/assets/color-tag-images.md). Dessa taggar möjliggör förbättrad sökning baserat på bildens färgkomposition. Du kan konfigurera antalet färger, inom intervallet 1 till 40, som taggas i en bild så att du kan söka efter bilder baserade på dessa färger senare.


## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* **Integrera adaptiv Forms med Microsoft® Power Automate**: Du kan nu konfigurera ett adaptivt formulär så att det kör ett Microsoft® Power Automate Cloud-flöde när du skickar in det. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

* **Guide för att skapa ett adaptivt formulär**: Du kan använda en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden ger dig en snabb fliknavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

  ![Guide för att skapa ett adaptivt formulär](/help/release-notes/assets/wizard.png)

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Snabb åtkomst till produktcockpit: Få enkelt tillgång till detaljerad produktinformation med ett enda klick i Sites Editor

<!-- Image was not found during PR validation despite correct path   ![Enable wantlist](/help/assets/CIF/enable-wishlist.png) -->

* Stöd för ytterligare marknadsföringskomponenter: Komponenter kan konfigureras för att visa ett tillägg till varukorgen och tillägg till önskad lista för att ringa till åtgärd

  ![Kortkommando för webbplatsredigeraren till produktcockpit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Nyheter {#what-is-new-foundation}

* Alternativet Lägg till träd under administratörsskärmen för replikeringsagenten **Fliken Distribuera**, som tidigare meddelats som borttagen, togs bort den 20 juni 2022 eller snart därefter. Paket med en trädhierarki av innehåll bör i stället replikeras med [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Arbetsflödet Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow).

* Användning av administratörsskärmen för replikeringsagenten eller replikerings-API:t för distribution av innehållspaket som är större än 10 MB (noder med egenskaper, exklusive binärfiler) är föråldrat och verkställt den 12 september 2022 eller snart därefter. Istället [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Arbetsflödet Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) måste användas för att replikera dessa stora innehållspaket. I juli visas ett varningsmeddelande på administratörsskärmen för replikeringsagenten **Fliken Distribuera** om du försöker replikera dessa stora innehållspaket och även i AEM fellogg när replikerings-API används för att replikera dessa stora innehållspaket. I september ersattes varningarna av fel. Anpassa processerna därefter.

### Nya funktioner i [!DNL Experience Manager] prerelease channel {#prerelease-features-foundation}

* AEM as a Cloud Service är nu integrerat med Unified Shell för att förbättra användarupplevelsen och göra den enhetlig med alla andra Experience Cloud-program. Se [AEM as a Cloud Service on Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) för mer information.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Security {#foundation-security}

### Borttagning av TLS 1.0, 1.1

Från och med den 30 juni 2022 kommer Experience Manager as a Cloud Service att kräva säkrare nätverkskommunikation och datautbyte med användarsystem. AEM använder enbart TLS (Transport Layer Security), 1.2-protokollet. Äldre TLS-versionerna 1.0 och 1.1 är nu inaktuella.

Om du fortsätter att använda äldre versioner av TLS som 1.0, 1.1 kan du förlora åtkomsten till Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
