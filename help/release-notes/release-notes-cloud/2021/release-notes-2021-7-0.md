---
title: Versionsinformation för version 2021.7.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.7.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020 och 2021.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2021.7.0) är 29 juli 2021.
Följande version (2021.8.0) är den 26 augusti 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt från juli 2021](https://video.tv.adobe.com/v/335580) för en sammanfattning av de funktioner som lagts till.

## Experience Manager Foundation as a Cloud Service {#foundation}

### Nyheter {#what-is-new-foundation}

* Flexiblare Dispatcher-konfiguration: Projekten kan struktureras enklare. Du kan nu t.ex. inkludera flera regelfiler för omskrivning som återspeglar webbplatsens struktur. [Lär dig mer om](/help/implementing/dispatcher/disp-overview.md#validation-debug) det här flexibla läget, inklusive hur du strukturerar din Dispatcher-konfiguration så att du kan utnyttja den.
* Gränssnittet för trädreplikering på fliken Distribuera i replikeringsagenten bör betraktas som inaktuellt och har tagits bort efter den 30 september 2021. [Läs mer om ](/help/operations/replication.md#tree-activation) alternativa replikeringsstrategier.
* Paketet `org.apache.sling.datasource-1.0.4.jar` för stöd för ling-datakälla har tagits bort eftersom det har inaktuella funktioner och inte används av kunder.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Med funktionen för innehållsautomatisering kan [!DNL Experience Manager Assets] använda [!DNL Adobe Creative Cloud] API:er för att automatisera resursproduktionen i stor skala. Det förbättrar innehållets hastighet genom att dramatiskt minska den tid det tar och de iterationer som krävs för att skapa varianter av samma material. Funktionen kräver ingen programmering och fungerar inifrån DAM. Se [generera variationer av resurser med hjälp av Creative Cloud-integrering](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] innehåller [!DNL Document Cloud] PDF Viewer för att förhandsgranska PDF-dokument internt. Med den här funktionen kan användare förhandsgranska flersidiga PDF-filer utan bearbetning eller konvertering. Den här funktionen förbättrar pariteten med [!DNL Experience Manager] 6.5. De kontroller som är tillgängliga i visningsprogrammet är bland annat zoomning, navigering till sidor, avdockningskontroller och visning i helskärmsläge. Användarna kan också förhandsgranska och hoppa till sidor och bokmärken. Kommentarer i själva filen stöds. Kommentarer och kommentarer om innehåll i filen PDF planeras för en framtida version.

  ![Förhandsgranska PDF-filer i [!DNL Experience Manager] med PDF Viewer](/help/assets/assets/preview-pdf-file-viewer.png)

* Funktionen för hämtning av länkdelning använder asynkrona nedladdningar som ökar nedladdningshastigheten. Mer information finns i [Hämta resurser som delas med länkdelning](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Hämta inkorgen](/help/assets/assets/download-inbox.png)

* Vyinställningarna har förbättrats så att användarna kan välja en standardvy och en standardsorteringsparameter.

  ![Ange standardvy i [!UICONTROL View Settings]](/help/assets/assets/view-settings-for-defaults.png)

* Användare kan söka efter och filtrera mapparna baserat på egenskapspredikat.

  ![Filtrera sökmappar med hjälp av sökpredikat](/help/assets/assets/search-folders-via-predicates.png)

### Nya funktioner som är tillgängliga i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* När du delar digitala resurser som en länk kan användarna kopiera URL-adressen till Urklipp. Förbättringen gör att du kan dela resurser snabbare och bekvämare.

### Fel som har åtgärdats i [!DNL Assets] {#assets-bugs-fixed}

API:t `com.day.cq.dam.api.collection.SmartCollection` är inte tillgängligt i [!DNL Experience Manager] som [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* Du kan nu använda tjänsten Automated forms conversion för att [konvertera PDF forms på franska, tyska och spanska ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) till anpassningsbara formulär.
* En separat panel har lagts till i mallredigeraren för att visa fel som rör adaptiva formulärkomponenter. Det bidrar till att konsolidera alla adaptiva formulärfel på en plats och minskar upplösningstiden.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera PDF-filer från ett XFA-formulär i PDF och Adobe Acrobat-formulär.

* **Variable Data Externalizer**: Du kan spara data AEM arbetsflödesvariabler i ett externt lagringssystem som hanteras av din organisation.

* **Acrobat-baserat postdokument**: Du kan även [använda Adobe Acrobat Form PDF (Acrobat PDF)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) som en mall för postdokument förutom XFA-baserad formulärmall.

* **Microsoft® Azure-datalageranslutning**: Nu kan du [ansluta formulärdatamodellen till Microsoft® Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html). Med den kan du hämta och lagra adaptiva formulärdata i Microsoft® Azure Storage som en BLOB.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* CIF Core Components v2
   * Förenklade och förbättrade konfigurationer för PDP/PLP URL och SEO
   * Visuell indikator för mellanlagrade produktdata i redigeringsläge för bättre synlighet för kommande ändringar
   * Ny platskarta för innehålls- och e-handelssidor

* Stöd för [Adobe Commerce Sensei produktrekommendation från Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) i AEM Storefront med fördefinierade eller direkt skapade rekommendationer

## [!DNL Experience Manager Screens] som en [!DNL Cloud Service] {#screens}

### Felkorrigeringar {#bug-fixes-screens}

* Inställningarna för innehållsleverantören valideras nu när de skapas eller uppdateras.

* Alla visningsvyer har en mappkolumn.

* Du kan expandera Screens innehållsstruktur.

* `bulk-offline-update-service` saknade alla behörigheter för vissa miljöer.

* Hjälplänken har uppdaterats för att matcha den nya dokumentationen för skärmar i molnet.

* Det går nu att ta bort tilldelningen av spellistor och inte ta bort spellistor med tilldelade spelare.

* Spelaren laddar nu ned Assets igen när &quot;ALL&quot;-cachen rensas.

* Upprepa schemaläggning fungerar nu om *sluttiden* är inställd för följande dag.

* `Back&Forward` fungerar nu i Screens as a Cloud Service.

* Taggar med samma namn men olika namnutrymmen kunde inte skapas tidigare.

## XML Documentation för Experience Manager as a Cloud Service {#xml-documentation}

### Nyheter {#what-is-new-xml-documentation}

XML Documentation för Experience Manager as a Cloud Service finns i allmänhet att tillgå. Med det kan kunder som har Experience Manager as a Cloud Service köpa ett XML Documentation-tillägg för att importera, skapa, hantera och leverera tekniskt innehåll i flera kanaler, inklusive Experience Manager Sites.

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.7.0.

### Releasedatum {#release-cm-july}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.7.0 är 15 juli 2021.
Nästa version är planerad till den 12 augusti 2021.

### Nyheter {#what-is-new-cm-july}

* Kunder kan nu använda Azul 8 och 11 JDK:er för Cloud Manager-byggprocesser och kan antingen välja att använda en av dessa JDK:er för verktygskedjor-kompatibla Maven-plugins *eller* hela Maven-processkörningen.

* IP-adressen för utgående utgång är nu loggad i loggfilen för byggsteget.

* Scen- och produktionsmiljöer som kör äldre versioner av AEM rapporterar nu statusen **Uppdatering tillgänglig**.

* Det högsta antalet SSL-certifikat som stöds har ökat till 20 per program.

* Det maximala antalet domäner som kan konfigureras har ökat till 500 per miljö.

* Knappen **Hantera Git** har fått namnet **Åtkomst till Git-information** och dialogrutan har uppdaterats visuellt.

* Den version av AEM Project Archetype som används av Cloud Manager har uppdaterats till version 28.

### Felkorrigeringar {#bug-fixes-cm-july}

* I vissa situationer var Förhandsvisning inte ett tillgängligt alternativ när en IP-tillåtelselista skulle bindas till en miljö.

* Manuell navigering till sidan med körningsinformation för en körning som inte finns visade inte på något fel, bara en oändlig inläsningsskärm.

* Felmeddelandet som visades när maximalt antal SSL-certifikat nåddes var inte till någon hjälp.

* I vissa fall kan det finnas en diskrepans i den officiella versionen som visas på pipeline-kortet på sidan **Översikt**.

* Guiden Lägg till program angav felaktigt att namnet inte kan ändras efter att det har skapats.

### Kända fel {#known-issues-cm-july}

Kunder som byter till Azul JDK bör känna till att inte alla befintliga program kompileras utan fel i Azul JDK. Adobe rekommenderar att du testar lokalt innan du byter.

## Cloud Acceleration Manager {#cam}

### Releasedatum {#release-date-july-cam}

Releasedatum för Cloud Acceleration Manager är 15 juli 2021.

### Nyheter {#what-is-new-cam}

Cloud Acceleration Manager är en molnbaserad applikation som utformats för att vägleda era IT-team under hela övergångsperioden, från planering till Cloud Service. Konfigurera teamet för en lyckad migrering med bästa praxis, tips, dokumentation och verktyg som rekommenderas av Adobe för att hjälpa till att AEM som Cloud Service under hela kundresan. Läs mer [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/getting-started-cam.html).

>[!NOTE]
>
> Kolla in den här [demonstrationsvideon om Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
