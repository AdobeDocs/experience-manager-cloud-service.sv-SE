---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: d977ff765accb650daff4c35f2668489454305cd
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] som en Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Lanseringsdatumet [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] aktuell version (2021.7.0) är 29 juli 2021.
Följande version (2021.8.0) är den 26 augusti 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt från juli 2021](https://video.tv.adobe.com/v/335580) om du vill se en sammanfattning av de nya funktionerna.

## Experience Manager Foundation som Cloud Service {#foundation}

### Nyheter {#what-is-new-foundation}

* Flexiblare konfiguration: Det blir enklare att organisera projekt. Du kan nu t.ex. inkludera flera regelfiler för omskrivning som återspeglar webbplatsens struktur. [Lär dig mer ](/help/implementing/dispatcher/disp-overview.md#validation-debug) om det här flexibla läget, inklusive hur du strukturerar din dispatcherkonfiguration för att kunna utnyttja det.
* Gränssnittet för trädreplikering under replikeringsagentens &quot;Distribuera&quot;-flik bör betraktas som inaktuellt och kommer att tas bort efter den 30 september. [Lär dig ](/help/operations/replication.md#tree-activation) om strategier för aboutalternativ replikering.
* Paketet `org.apache.sling.datasource-1.0.4.jar` för att skicka datakällor har tagits bort eftersom det har föråldrade funktioner och inte används av kunder.

## [!DNL Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Med funktionen för innehållsautomatisering kan [!DNL Experience Manager Assets] utnyttja API:erna för [!DNL Adobe Creative Cloud] för att automatisera materialproduktionen i stor skala. Det förbättrar innehållets hastighet genom att dramatiskt minska den tid det tar och de iterationer som krävs för att skapa varianter av samma material. Funktionen kräver ingen programmering och fungerar inifrån DAM. Se [generera variationer av resurser med hjälp av Creative Cloud-integrering](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] innehåller  [!DNL Document Cloud] PDF Viewer för att förhandsgranska PDF-dokument internt. Med den här funktionen kan användarna förhandsgranska flersidiga PDF-filer utan bearbetning eller konvertering. Den här funktionen förbättrar pariteten med [!DNL Experience Manager] 6.5. De kontroller som är tillgängliga i visningsprogrammet är bland annat zoomning, navigering till sidor, avdockningskontroller och visning i helskärmsläge. Användarna kan också förhandsgranska och hoppa till sidor och bokmärken. Kommentarer i själva filen stöds och kommentarer och kommentarer i innehållet i PDF-filen läggs till i en framtida version.

   ![Förhandsgranska PDF-filer i  [!DNL Experience Manager] PDF Viewer](/help/assets/assets/preview-pdf-file-viewer.png)

* Länkdelningsfunktionen använder asynkrona nedladdningar som ökar nedladdningshastigheten. Se [Hämta resurser som delas med länkdelning](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Hämta inkorg](/help/assets/assets/download-inbox.png)

* Vyinställningarna har förbättrats så att användarna kan välja en standardvy och en standardsorteringsparameter.

   ![Ange standardvy i  [!UICONTROL View Settings]](/help/assets/assets/view-settings-for-defaults.png)

* Användare kan söka efter och filtrera mapparna baserat på egenskapspredikat.

   ![Filtrera sökmappar med hjälp av sökpredikat](/help/assets/assets/search-folders-via-predicates.png)

### Nya funktioner som är tillgängliga i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* När du delar digitala resurser som en länk kan användarna kopiera URL:en till Urklipp. Förbättringen gör att du kan dela resurser snabbare och bekvämare.

### Fel som har korrigerats i [!DNL Assets] {#assets-bugs-fixed}

API:t `com.day.cq.dam.api.collection.SmartCollection` är inte tillgängligt i [!DNL Experience Manager] som en [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] som  [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* Du kan nu använda tjänsten Automated forms conversion för att [konvertera PDF forms på franska, tyska och spanska ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) till anpassningsbara formulär.
* En separat panel har lagts till i mallredigeraren för att visa fel som rör adaptiva formulärkomponenter. Det bidrar till att konsolidera alla adaptiva formulärfel på en plats och minskar upplösningstiden.

### Nya funktioner i prerelease Channel [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [Communication ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) API - använd XDP-mallar och XML-data för att generera trycksaker i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera tryckta PDF-filer från ett XFA-formulär i PDF- och Adobe Acrobat-format.

* **Variable Data Externalizer**: Du kan spara data AEM arbetsflödesvariabler i ett externt lagringssystem som hanteras av din organisation.

* **Acroform-based Document of Record**: Du kan även  [använda Adobe Acrobat Form PDF (Acrobat PDF) ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) som mall för arkivhandlingar förutom XFA-baserad formulärmall.

* **Microsoft Azure-dataarkivanslutning**: Du kan nu  [ansluta formulärdatamodellen till Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Det gör att du kan hämta och lagra adaptiva formulärdata till Microsoft Azure Storage som en BLOB.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* CIF Core Components v2
   * Förenklade och förbättrade konfigurationer för PDP/PLP URL och SEO
   * Visuell indikator för mellanlagrade produktdata i redigeringsläge för bättre synlighet för kommande ändringar
   * Ny platskarta för innehålls- och e-handelssidor

* Stöd för [Adobe Commerce Sensei-produktrekommendation, som drivs av Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) i AEM Storefront med fördefinierade eller direkt skapade rekommendationer

## [!DNL Experience Manager Screens] som  [!DNL Cloud Service] {#screens}

### Felkorrigeringar {#bug-fixes-screens}

* Inställningarna för innehållsleverantören valideras nu när du skapar eller uppdaterar.

* Alla visningsvyer har en mappkolumn.

* Du kan expandera Innehållsstruktur för skärmar.

* `bulk-offline-update-service` saknade alla behörigheter för vissa miljöer.

* Hjälplänken har uppdaterats för att matcha den nya dokumentationen för skärmar i molnet.

* Det går nu att ta bort spellistor och inte tillåta att spellistor med tilldelade spelare tas bort.

* Player hämtar nu resurser igen när ALL-cachen har rensats.

* Upprepa schemaläggning fungerar nu om *Sluttiden* är inställd för följande dag.

* `Back&Forward` fungerar nu i skärmar som ett Cloud Service-gränssnitt.

* Taggar med samma namn men olika namnutrymmen kunde inte skapas tidigare.

## XML-dokumentation för Experience Manager som Cloud Service {#xml-documentation}

### Vad är nytt? {#what-is-new-xml-documentation}

XML-dokumentation för Experience Manager som Cloud Service är vanligtvis tillgänglig. Experience Manager kan som Cloud Service köpa in XML-dokumentation och dessutom importera, skapa, hantera och leverera tekniskt innehåll i flera kanaler, inklusive Experience Manager Sites.

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.7.0.

### Releasedatum {#release-cm-july}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.7.0 är 15 juli 2021.
Nästa version är planerad till den 12 augusti 2021.

### Nyheter {#what-is-new-cm-july}

* Kunderna kan nu använda Azul 8 och 11 JDK:er för sina Cloud Manager-byggprocesser och kan antingen välja att använda en av dessa JDK:er för verktygskedjor-kompatibla Maven-plugins *eller* hela Maven-processkörningen.

* IP för utgående utgång loggas nu i loggfilen för byggsteget.

* Scen- och produktionsmiljöer som kör äldre versioner av AEM rapporterar nu statusen **Tillgänglig uppdatering**.

* Det högsta antalet SSL-certifikat som stöds har ökat till 20 per program.

* Det maximala antalet domäner som kan konfigureras har ökat till 500 per miljö.

* Knapparna **Hantera Git** har ändrats till **Använd Git-information** och dialogrutan har uppdaterats visuellt.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 28.

### Felkorrigeringar {#bug-fixes-cm-july}

* I vissa situationer var Förhandsgranskning inte ett tillgängligt alternativ när en IP-Tillåtelselista skulle bindas till en miljö.

* Manuell navigering till sidan med körningsinformation för en körning som inte finns visade inte på något fel, bara en oändlig inläsningsskärm.

* Felmeddelandet som visades när det maximala antalet SSL-certifikat nåddes var inte till någon hjälp.

* I vissa fall kan det finnas en diskrepans i releaseversionen som visas på pipeline-kortet på sidan **Översikt**.

* Guiden Lägg till program angav felaktigt att namnet inte kan ändras efter att det har skapats.

### Kända fel {#known-issues-cm-july}

Kunder som byter till Azul JDK bör vara medvetna om att inte alla befintliga program kompileras utan fel i Azul JDK. Vi rekommenderar att du testar lokalt innan du byter.

## Cloud Acceleration Manager {#cam}

### Releasedatum {#release-date-july-cam}

Releasedatum för Cloud Acceleration Manager är 15 juli 2021.

### Vad är nytt? {#what-is-new-cam}

Cloud Acceleration Manager är en molnbaserad applikation som är utformad för att vägleda era IT-team under hela övergångsresan, från planering till live Cloud Service. Konfigurera era team för en framgångsrik migrering med bästa praxis, tips, dokumentation och verktyg som rekommenderas av Adobe för att hjälpa er att AEM som Cloud Service under hela kundresan. Läs mer [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Kolla den här [demonstrationsvideon om Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
