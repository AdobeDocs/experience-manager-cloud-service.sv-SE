---
title: Versionsinformation om 2022.6.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2022.6.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Versionsinformation 2022.6.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktioner i 2022.6.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.6.0) är 30 juni 2022.

Nästa version (2022.7.0) är planerad till 8 augusti 2022.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för juni 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* Ett nytt [användargränssnitt](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) är nu tillgängligt för innehållsadministratörer och innehållsförfattare som effektivt kan hantera (till exempel publicera, avpublicera, kopiera, flytta och så vidare), söka/filtrera och skapa innehållsfragment för Headless-fall.

  ![Konsol för innehållsfragment](/help/release-notes/assets/cf-ui.png)

* Den nya [innehållsförteckningskomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) fungerar inte bara med kärnkomponenterna utan med alla komponenter, så att ToCS återges automatiskt på innehållssidor. Och eftersom den renderas på serversidan och cachas fullständigt av dispatchern är det också effektivt att läsa in den.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

Experience Manager Assets använder Adobe AI-funktioner för att nu [skilja mellan färger i en bild och använda dem som taggar automatiskt vid förtäring](/help/assets/color-tag-images.md). Dessa taggar möjliggör förbättrad sökning baserat på bildens färgkomposition. Du kan konfigurera antalet färger, inom intervallet 1 till 40, som taggas i en bild så att du kan söka efter bilder baserade på dessa färger senare.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#forms-features}

* **[Integrera adaptiv Forms med Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: Nu kan du konfigurera ett adaptivt formulär så att ett Microsoft® Power Automate Cloud-flöde körs när det skickas. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

* **Guiden för att skapa ett adaptivt formulär**: Du kan använda en användarvänlig guide för att snabbt skapa adaptiv Forms. Guiden ger dig en snabb fliknavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

  ![Guiden för att skapa ett anpassat formulär](/help/release-notes/assets/wizard.png)

## CIF Add-on {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Ny egenskapssida för produktcockpit för bättre och enklare översikt

![egenskapsöversikt för produktcockpit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Förbättrad kompatibilitet och tillförlitlighet för tredjepartsanslutningar i I/O-miljön

* Förbättrat stöd för överskrivningar av GQL-klientkonfigurationen (ange t.ex. anpassad cachelagring)

* Flera slutpunkter för e-handel stöds nu direkt och kan konfigureras via Cloud Manager. Mer information finns i CIF-bloggen [här](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Felkorrigeringar {#bug-fixes-cif}

* Produktväljarfältet för flera värden visar att andra och ytterligare produkter är ogiltiga

* Produktväljaren döljs ibland bakom komponenter

## Tillägget Referensdemonstrationer {#cloud-services-demos}

### Nyheter {#what-is-new-demos}

* Ny WKND Content &amp; Commerce-mall som omfattar WKND och en E2E-shoppingupplevelse med produktkatalog, kundvagn, utcheckning och mitt konto. I den här mallen används CIF och dess CIF Core Components, och du måste därför även installera CIF-tillägget. Mer information finns i CIF-bloggen [här](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![WKND shop](/help/assets/CIF/wknd_shop.png)

![WKND-pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nyheter {#what-is-new-foundation}

* Som nämndes i versionsinformationen från maj (2022.5.0) togs alternativet &quot;Lägg till träd&quot; bort under administratörsfliken **Distribuera** på replikeringsagentens administratörsskärm. Paket med en trädhierarki av innehåll ska i stället replikeras med [Hantera publikation](/help/operations/replication.md#manage-publication) eller arbetsflödet [Publicera innehållsträd](/help/operations/replication.md#manage-publication#publish-content-tree-workflow).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
