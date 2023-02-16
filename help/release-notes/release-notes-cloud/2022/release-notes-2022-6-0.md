---
title: Versionsinformation om 2022.6.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2022.6.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
source-git-commit: 7b21a8af886c8e1f209e3b7cc5d94de5c58be1ac
workflow-type: tm+mt
source-wordcount: '642'
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

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.6.0) är 30 juni 2022.

Nästa version (2022.7.0) är planerad till 8 augusti 2022.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för juni 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* En ny [användargränssnitt](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) är nu tillgängligt för innehållsadministratörer och innehållsförfattare att effektivt hantera (vidta åtgärder som att publicera, avpublicera, kopiera, flytta osv.), söka/filtrera och skapa innehållsfragment för Headless-fall.

   ![Konsol för innehållsfragment](/help/release-notes/assets/cf-ui.png)

* Den nya [Innehållsförteckningskomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) fungerar inte bara med kärnkomponenterna utan med alla komponenter, vilket automatiskt återger ToCS på innehållssidorna. Och eftersom den renderas på serversidan och cachas fullständigt av dispatchern är det också effektivt att läsa in den.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

Experience Manager Assets använder Adobe Sensei AI-funktioner hittills [skilja på färger i en bild och använda dem som taggar automatiskt vid förtäring](/help/assets/color-tag-images.md). Dessa taggar möjliggör förbättrad sökning baserat på bildens färgkomposition. Du kan konfigurera antalet färger, inom ett intervall av en till fyrtio, som är taggade till en bild så att du kan söka efter bilder baserade på dessa färger senare.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#forms-features}

* **[Integrera adaptiv Forms med Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: Nu kan du konfigurera ett adaptivt formulär så att det kör ett Microsoft® Power Automate Cloud-flöde när du skickar in det. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden.

* **Guide för att skapa ett adaptivt formulär**: Du kan använda en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden ger dig en snabb fliknavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

   ![Guide för att skapa ett adaptivt formulär](/help/release-notes/assets/wizard.png)

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Ny egenskapssida för produktcockpit för bättre och enklare översikt

![översikt över egenskaper för produktcockpit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Förbättrad kompatibilitet och tillförlitlighet för anslutningar från tredje part vid I/O-körning

* Förbättrat stöd för överskrivningar av GQL-klientkonfigurationen (ange t.ex. anpassad cachelagring)

* Flera slutpunkter för e-handel stöds nu direkt och kan konfigureras via Cloud Manager. Information finns i CIF-bloggen [här](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Felkorrigeringar {#bug-fixes-cif}

* Produktväljarfältet för flera värden visar att andra och ytterligare produkter är ogiltiga

* Produktväljaren döljs ibland bakom komponenter

## Tillägget Referensdemonstrationer {#cloud-services-demos}

### Vad är nytt? {#what-is-new-demos}

* Ny WKND Content &amp; Commerce-mall som utökar WKND med en E2E-shoppingupplevelse med produktkatalog, kundvagn, utcheckning och mitt konto. Den här mallen använder CIF och dess CIF Core-komponenter, och därför måste du även installera CIF-tillägget. Information finns i CIF-bloggen [här](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![WKND](/help/assets/CIF/wknd_shop.png)

![WKND-pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Vad är nytt? {#what-is-new-foundation}

* Som nämndes i versionsinformationen från maj (2022.5.0) finns alternativet Lägg till träd under administratörsskärmen för replikeringsagenten **Distribuera** har tagits bort. Paket med en trädhierarki av innehåll bör i stället replikeras med [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Publicera innehållsträd](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) arbetsflöde.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här.](/help/implementing/cloud-manager/release-notes/current.md)

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
