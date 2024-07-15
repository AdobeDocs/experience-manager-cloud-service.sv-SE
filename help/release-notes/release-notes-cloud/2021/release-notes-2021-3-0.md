---
title: Versionsinformation för version 2021.3.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service versionsinformation för 2021.3.0."
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 är 25 mars 2021.
Följande version (2021.4.0) kommer att vara den 29 april 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [En progressiv webbprogramversion (PWA) av en webbplats ](/help/sites-cloud/authoring/sites-console/enable-pwa.md) kan nu aktiveras på projektnivå via enkel konfiguration.
* Modelltillägg för innehållsfragment - nu möjligt att definiera datatyper med flera rader som flerfältslista.
* Förbättringar i gränssnittet för innehållsfragmentredigeraren - kapslade underordnade fragment visas nu i vägbeskrivningar och förbättrad vy för åtgärder för publicering, spara och spara och avsluta

## [!DNL Adobe Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] utökar funktionerna för anslutna Assets så att de stöder användning av [!DNL Dynamic Media]-bilder i de kärnkomponenter som stöds. Se [Använd ansluten Assets](/help/assets/use-assets-across-connected-assets-instances.md).
* Experience Manager-administratörer kan schemalägga inmatningar av gruppresurser vid ett visst datum eller en viss tidpunkt. Administratörer kan även schemalägga återkommande frågor baserat på datum och tid. Se [massinläsning av resurser](/help/assets/add-assets.md#asset-bulk-ingestor).

### Felkorrigeringar i [!DNL Assets] {#bug-fixes-assets}

* Copyright-sidan visas inte när du försöker hämta flera rättighetshanterade resurser. (CQ-4314403)
* När du väljer att redigera en INDD-fil ändras upplösningen oväntat. (CQ-4317376)
* Det är bara den sista InDesignen i mallen som finns i renderingen PDF. (CQ-4317305)
* Det tar lång tid att öppna taggväljaren när väljaren är en del av ett komplext metadataschema. (CQ-4316426)
* När du överför en resurs med samma filnamn som en befintlig, visas inte dialogrutan för namnkonflikt för att uppmana användaren att skapa en version. (CQ-4315424)
* Egenskaper för mappmetadata kan anges och sparas på popup-menyn på mappens egenskapssida. När markeringen sparas i databasen visas den inte när mappmetadataegenskaperna öppnas igen. (CQ-4314429)
* Assets med filnamn som innehåller mellanslag eller specialtecken överförs med webbläsaren. (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

AEM Forms har hjälpt många organisationer att skapa fantastiska startupplevelser och registreringsupplevelser under årens lopp. Dessa upplevelser har hjälpt organisationer att konvertera leads till försäljning, bearbeta inhämtade kunddata, leverera responsiva upplevelser baserat på målgruppsprofilen och mycket mer. Nu finns AEM Forms som molntjänst.

Du kan använda [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) för att skapa digitala formulär, koppla formulär till befintliga datakällor, integrera formulär med Adobe Sign för att lägga till e-signaturer i formulär, generera arkiveringsdokument (Document of Record, DoR) för att arkivera skickade formulär som PDF-filer. Tjänsten kan också konvertera PDF forms till digitala blanketter. Förutom AEM Forms standardfunktioner erbjuder tjänsten flera inbyggda funktioner i molnet, som automatisk skalning, noll driftstopp för uppgraderingar och molnbaserad utvecklingsmiljö.

Du kan kontakta din Adobe-representant för att få en demo eller anmäla dig till tjänsten.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Stöd för Adobe Commerce 2.4.2

* Produktdetaljkomponenten kan nu användas och konfigureras på alla innehållssidor

* Lanserade CIF Venia Reference Site - 2021.03.25 som innehåller den senaste CIF Core Components version v1.9.0. Mer information finns i [CIF Venedig-referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25).

* Frisläppta CIF kärnkomponenter v1.9.0. Mer information finns i [CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0).


## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.3.0.

## Releasedatum {#release-date-cm-march}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.3.0 är 11 mars 2021.
Nästa version är planerad till den 8 april 2021.

### Nyheter {#what-is-new-march}

* Kunder som har miljöer med redan befintliga konfigurationer av anpassade domännamn för [IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) och [anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) kan se ett meddelande om sina tidigare konfigurationer och kan självbetjäna via användargränssnittet.

* Användare med nödvändig behörighet kan nu redigera ett program och göra följande på ett självbetjäningssätt:

   * Lägg till Sites-lösning i ett befintligt program med Assets eller omvänt.
   * Ta bort Sites eller Assets från ett befintligt program med både Sites och Assets.
   * Lägg till andra, outnyttjade lösningsberättigande antingen till ett befintligt program eller som ett nytt program.

* Etiketten **AEM Push Update** visas nu både för skärmarna *Pipeline Execution* och *Activity*.

* Om en miljö är i viloläge, men det även finns en tillgänglig AEM, prioriteras statusen **i viloläge** framför **Tillgänglig uppdatering**.

* Nu kan användare se sina Cloud Manager-roller genom att välja alternativet Visa Cloud Manager-roller efter att ha navigerat till ikonen Användarprofil (överst till höger) i Unified Shell.

* Etiketten **Ansökan om godkännande** har fått en ny etikett till **Produktionsgodkännande** för större tydlighet.

* Etiketten **Version** har fått en ny etikett till **Git-taggen** i körningsfönstret för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende: **Avbryt omedelbart** och **Godkänn omedelbart**.

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service SDK.

* Cloud Manager Production Pipeline kommer nu att innehålla funktionen [Testning av anpassat användargränssnitt](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Felkorrigeringar {#bug-fixes-cm-march}

* Paketversionshantering hoppades över i vissa fall under AEM push-uppgradering.

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* I svåra fall kan standardprogramnamnet som genereras när dialogrutan Lägg till program öppnas vara en dubblett av ett befintligt programnamn.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.

* Byggsteget startades om i onödan när kundbyggen resulterade i ogiltiga paket.

* Ibland kan användaren se en grön &quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när den konfigurationen inte har distribuerats.

* Alla befintliga produktionspipelines aktiveras automatiskt med Experience Audit-steget.

## Verktyget Innehållsöverföring {#content-transfer-tool}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.3.4 är 19 mars 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* CTT hoppade över innehåll från mappar med samma namn men med ett bindestreck i namnet. Den här har åtgärdats.

### Releasedatum {#release-date-ctt-march}

Releasedatum för innehållsöverföringsverktyget v1.3.0 är 4 mars 2021.

### Nyheter i verktyget Innehållsöverföring {#what-is-new-ctt-march}

* CTT installeras nu på `/apps` i stället för `/libs` webbläsarbokmärken på vissa sidor kanske inte längre är giltiga.
* När CTT är installerat måste användaren navigera ytterligare en nivå för att komma till sidan Innehållsöverföring. Mer information finns i [Använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html).

### Felkorrigeringar {#bug-fixes-ctt-march}

* När CTT migrerade innehåll från en viss sökväg drog det in resurser som inte hade med varandra att göra. Detta har åtgärdats

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.8 är 22 mars 2021.

### Nyheter i Best Practices Analyzer {#what-is-new-bpa}

* Möjlighet att filtrera bort ACS Commons-resultat från BPA-rapporten i användargränssnittet och från rapporten som exporterats som en CSV-fil.

## Kodomfaktoriseringsverktyg {#code-refactoring-tools}

### Nyheter i verktygen för kodkorrigering {#what-is-new-crt}

* Nya funktioner och förbättringar för Databasmodernisering. Se [GitHub-resurs: Databasmoderering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) för den senaste versionen.
   * Normalisera OSGi-konfigurationer (utom RepoInit-konfigurationer) till det önskade .cfg.json-formatet.
   * Byt namn på OSGi-konfigurationsmappar till det angivna formatet.
   * Generera ui.apps.structure-projektet.
   * Skapa analysmodulen.

* Nya funktioner och förbättringar för Dispatcher Converter. Se [GitHub-resurs: Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Skapa separata filer för olika inkluderingar i stället för att länka innehållet.
   * Möjlighet att hantera både mappsökväg för värdar och sökväg till värdfiler.
   * Generering av servergruppsfiler med stora kundkonfigurationer från 600 eller fler.
