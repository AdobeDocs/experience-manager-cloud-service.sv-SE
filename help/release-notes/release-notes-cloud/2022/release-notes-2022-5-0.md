---
title: Versionsinformation om 2022.5.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2022.5.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Versionsinformation 2022.5.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktioner i 2022.5.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.5.0) är 9 juni 2022.
Nästa version (2022.6.0) är planerad till 30 juni 2022.

## Släpp video {#release-video}

Titta på videon om versionsöversikten från maj 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Sites] {#prerelease-features-sites}

* Olika GraphQL-funktioner
* En [ny konsol](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) som är optimerad för Headless-användning av innehållsfragment

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [Dynamic Media Smart Imaging](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) har nu stöd för AVIF-filformat - ytterligare förbättring av Google Core Web Vital (Störst Contentful Paint), med AVIF som ger en extra storleksminskning på 20 % jämfört med WebP. Totalt ger AVIF upp till 41 % genomsnittlig storleksminskning jämfört med JPEG (i vissa bilder till och med upp till 76 %).

* [!UICONTROL Experience Manager Assets Brand Portal] kör nu automatiska jobb var tolfte timme för att ta bort alla Brand Portal-resurser som publicerats till AEM. Därför behöver du inte ta bort resurserna i Contribute-mappen manuellt för att mappstorleken ska hållas under tröskelvärdet. Se [Nyheter i Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=sv-SE).

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Assets] {#prerelease-features-assets}

Experience Manager Assets använder Adobe AI-funktioner för att nu [skilja mellan färger i en bild och använda dem som taggar automatiskt vid förtäring](/help/assets/color-tag-images.md). Dessa taggar möjliggör förbättrad sökning baserat på bildens färgkomposition. Du kan konfigurera antalet färger, inom intervallet 1 till 40, som taggas i en bild så att du kan söka efter bilder baserade på dessa färger senare.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

* **Integrera adaptiv Forms med Microsoft® Power Automate**: Nu kan du konfigurera ett adaptivt formulär så att ett Microsoft® Power Automate Cloud-flöde körs när det skickas. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

* **Guiden för att skapa ett adaptivt formulär**: Du kan använda en användarvänlig guide för att snabbt skapa adaptiv Forms. Guiden ger dig en snabb fliknavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

  ![Guiden för att skapa ett anpassat formulär](/help/release-notes/assets/wizard.png)

## CIF Add-on {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Snabb åtkomst till produktcockpit: Få enkelt tillgång till detaljerad produktinformation med ett enda klick i Sites Editor

<!-- Image was not found during PR validation despite correct path   ![Enable wantlist](/help/assets/CIF/enable-wishlist.png) -->

* Stöd för ytterligare marknadsföringskomponenter: Komponenter kan konfigureras för att visa ett tillägg i kundvagnen och tillägg i önskelistan i call-to-action

  ![Kortkommando för webbplatsredigeraren till produktcockpit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nyheter {#what-is-new-foundation}

* Alternativet Lägg till träd under administratörsskärmen för replikeringsagenten **fliken Distribuera**, som tidigare meddelats som borttagen, togs bort den 20 juni 2022 eller snart därefter. Paket med en trädhierarki av innehåll ska i stället replikeras med [Hantera publikation](/help/operations/replication.md#manage-publication) eller arbetsflödet [Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow).

* Användning av administratörsskärmen för replikeringsagenten eller replikerings-API:t för distribution av innehållspaket som är större än 10 MB (noder med egenskaper, exklusive binärfiler) är föråldrat och verkställt den 12 september 2022 eller snart därefter. I stället måste arbetsflödet [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) användas för att replikera dessa stora innehållspaket. I juli visas ett varningsmeddelande på **fliken Distribuera** på administratörsskärmen för replikeringsagenten om du försöker replikera dessa stora innehållspaket och även i AEM fellogg när replikerings-API:t används för att replikera dessa stora innehållspaket. I september ersattes varningarna av fel. Anpassa processerna därefter.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service är nu integrerat med Unified Shell för att förbättra användarupplevelsen och göra den enhetlig med alla andra Experience Cloud-program. Mer information finns i [AEM as a Cloud Service i Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md).

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Security {#foundation-security}

### Borttagning av TLS 1.0, 1.1

Från och med 30 juni 2022 kommer Experience Manager as a Cloud Service att kräva säkrare nätverkskommunikation och datautbyte med användarsystem. AEM använder enbart TLS (Transport Layer Security), 1.2-protokollet. Äldre TLS-versionerna 1.0 och 1.1 är nu inaktuella.

Om du fortsätter att använda äldre versioner av TLS som 1.0, 1.1 kan du förlora åtkomsten till Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
