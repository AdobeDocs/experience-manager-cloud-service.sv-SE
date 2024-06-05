---
title: Versionsinformation om 2022.6.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2022.6.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# Versionsinformation 2022.6.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för 2022.6.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.6.0) är 30 juni 2022.

Nästa version (2022.7.0) är planerad till 8 augusti 2022.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för juni 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* En ny [användargränssnitt](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) är nu tillgängligt för innehållsadministratörer och innehållsförfattare som effektivt kan hantera (till exempel publicera, avpublicera, kopiera, flytta och så vidare), söka/filtrera och skapa innehållsfragment för Headless-fall.

  ![Konsol för innehållsfragment](/help/release-notes/assets/cf-ui.png)

* Den nya [Innehållsförteckning, komponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) fungerar inte bara med kärnkomponenterna utan med alla komponenter, vilket automatiskt återger ToCS på innehållssidorna. Och eftersom den renderas på serversidan och cachas fullständigt av dispatchern är det också effektivt att läsa in den.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

Experience Manager Assets använder Adobe Sensei AI-funktioner hittills [skilja på färger i en bild och använda dem som taggar automatiskt vid förtäring](/help/assets/color-tag-images.md). Dessa taggar möjliggör förbättrad sökning baserat på bildens färgkomposition. Du kan konfigurera antalet färger, inom intervallet 1 till 40, som taggas i en bild så att du kan söka efter bilder baserade på dessa färger senare.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#forms-features}

* **[Integrera adaptiv Forms med Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: Du kan nu konfigurera ett adaptivt formulär så att det kör ett Microsoft® Power Automate Cloud-flöde när du skickar in det. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

* **Guide för att skapa ett adaptivt formulär**: Du kan använda en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden ger dig en snabb fliknavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

  ![Guide för att skapa ett adaptivt formulär](/help/release-notes/assets/wizard.png)

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Ny egenskapssida för produktcockpit för bättre och enklare översikt

![översikt över egenskaper för produktcockpit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Förbättrad kompatibilitet och tillförlitlighet för tredjepartsanslutningar i I/O-miljön

* Förbättrat stöd för överskrivningar av GQL-klientkonfigurationen (ange t.ex. anpassad cachelagring)

* Flera slutpunkter för e-handel stöds nu direkt och kan konfigureras via Cloud Manager. Information finns i CIF blogg [här](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Felkorrigeringar {#bug-fixes-cif}

* Produktväljarfältet för flera värden visar att andra och ytterligare produkter är ogiltiga

* Produktväljaren döljs ibland bakom komponenter

## Tillägget Referensdemonstrationer {#cloud-services-demos}

### Nyheter {#what-is-new-demos}

* Ny WKND Content &amp; Commerce-mall som omfattar WKND och en E2E-shoppingupplevelse med produktkatalog, kundvagn, utcheckning och mitt konto. I den här mallen används CIF och dess CIF kärnkomponenter, och du måste därför även installera det CIF tillägget. Information finns i CIF blogg [här](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![WKND](/help/assets/CIF/wknd_shop.png)

![WKND-pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Nyheter {#what-is-new-foundation}

* Som nämndes i versionsinformationen från maj (2022.5.0) finns alternativet Lägg till träd under administratörsskärmen för replikeringsagenten **Distribuera** har tagits bort. Paket med en trädhierarki av innehåll bör i stället replikeras med [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Publicera innehållsträd](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) arbetsflöde.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
