---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: bed5a88a545efa4dbfe5c20f4713c0c6adb9847b
workflow-type: tm+mt
source-wordcount: '1541'
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

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2021.6.0 är 28 juni 2021.
Följande version (2021.7.0) kommer att vara den 29 juli 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt från juni 2021](https://video.tv.adobe.com/v/334296) om du vill se en sammanfattning av de funktioner som lagts till.

## XML-dokumentation för AEM som molntjänst {#xml-documentation}

### Nyheter {#what-is-new-xml-documentation}

* XML Documentation for AEM as a Cloud Service is now GA.
* Detta gör det möjligt för befintliga AEM Cloud Service-kunder att skaffa XML-dokumentationstillägg för import, skapande, hantering och leverans av tekniskt innehåll över flera kanaler, inklusive AEM webbplatser

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.6.0 och 2021.5.0.

### Releasedatum {#release-date-june-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.6.0 är 10 juni 2021.
Nästa version är planerad till 15 juli 2021.

### Nyheter {#what-is-new-junecm}

* Förhandsgranskningstjänsten kommer att distribueras rullande till alla program. Kunder meddelas i produkten när deras program är aktiverat för förhandsgranskningstjänsten. Mer information finns i [Åtkomst till förhandsgranskningstjänsten](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

* Maven Dependencies som laddas ned under byggfasen cachelagras nu mellan pipeline-körningar. Den här funktionen kommer att aktiveras för kunderna under de kommande veckorna.

* Namnet på programmet kan nu redigeras via dialogrutan Redigera program.

* Det standardförgreningsnamn som används både när projektet skapas och i det förvalda push-kommandot via Hantera Git-arbetsflöden har ändrats till `main`.

* Redigera programupplevelser i användargränssnittet har uppdaterats.

* Kvalitetsregeln `ImmutableMutableMixCheck` har uppdaterats för att klassificera `/oak:index`-noder som oföränderliga.

* Kvalitetsreglerna `CQBP-84` och `CQBP-84--dependencies` har konsoliderats till en enda regel. Som en del av den här konsolideringen identifierar genomsökningen av beroenden mer korrekt problem i tredjepartsberoenden som distribueras till AEM.

* För att undvika problem har segmentraderna Publicera AEM och Publicera dispatcher på sidan Miljöinformation konsoliderats.

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* En ny regel för kodkvalitet har lagts till för att validera strukturen för `damAssetLucene`-index. Mer information finns i [Anpassade DAM-resursindex Luceneak-index](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check).

* Sidan med miljöinformation visar nu flera domännamn för tjänsterna Publicera och Förhandsgranska (beroende på vad som är tillämpligt). Mer information finns i [Miljöinformation](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Felkorrigeringar {#bug-fixes-junecm}

* JCR-noddefinitioner som innehåller en ny rad efter att rotelementnamnet inte tolkades korrekt.

* API för listdatabaser filtrerar inte borttagna databaser.

* Ett felaktigt felmeddelande visades när ett ogiltigt värde angavs för schemasteget.

* Ibland kan användaren se en grön *aktiv*-status bredvid ett IP-Tillåtelselista även när konfigurationen inte har distribuerats.

* Vissa programredigeringssekvenser kan leda till att produktionsflödet inte kan skapas eller redigeras.

* Vissa programredigeringssekvenser kan resultera i att sidan **Översikt** visar ett missvisande meddelande om att köra programkonfigurationen igen.

## [!DNL Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#ga-features-assets}

* Med funktionen för innehållsautomatisering kan [!DNL Experience Manager Assets] utnyttja API:erna för [!DNL Adobe Creative Cloud] för att automatisera materialproduktionen i stor skala. Det förbättrar innehållets hastighet genom att dramatiskt minska den tid det tar och de iterationer som krävs för att skapa varianter av samma material. Funktionen kräver ingen programmering och fungerar inifrån DAM. Se [Generera variationer av resurser med hjälp av Creative Cloud-integrering](/help/assets/cc-api-integration.md).

* [[!DNL Adobe Asset Link] v3.0](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) för  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]och  [!DNL Adobe InDesign] v2.0 [[!DNL Adobe Asset Link] för ](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html)   [!DNL Adobe XD] finns. Den innehåller följande:

   * Stöd för [!DNL Assets Essentials].
   * Möjlighet att automatiskt ansluta till [!DNL Experience Manager] som [!DNL Cloud Service] eller [!DNL Assets Essentials].

* Med verktyget [Massingestor](/help/assets/add-assets.md#asset-bulk-ingestor) kan du lägga till metadata vid ett massintag.

### Nya funktioner som är tillgängliga i betaversionskanalen [!DNL Assets] {#beta-features-assets}

* Vyinställningarna har förbättrats så att användarna kan välja en standardvy och en standardsorteringsparameter.

   ![Ange standardvy i visningsinställningar](/help/assets/assets/view-settings-for-defaults.png)

* Länkdelningsfunktionen använder asynkrona nedladdningar som ökar nedladdningshastigheten.

* Användare kan söka efter och filtrera mapparna baserat på egenskapspredikat.

   ![Filtrera sökmappar med hjälp av sökpredikat](/help/assets/assets/search-folders-via-predicates.png)

* [!DNL Experience Manager Assets] bäddar in PDF-visningsprogrammet för att förhandsgranska de dokumentformat som stöds. Den drivs av [!DNL Adobe Document Cloud]. Med den här funktionen kan användarna förhandsgranska PDF-filer och andra flersidiga filer utan komplex bearbetning. Detta förbättrar funktionspariteten med [!DNL Experience Manager] 6.5. Kontrollerna i förhandsgranskningen är att zooma, navigera till sidor, avbryta dockning av kontroller och visa i helskärmsläge. Det inbyggda PDF-visningsprogrammet har stöd för filformaten AI, DOCX, INDD, PDF och PSD. Du kan kommentera själva resursen, men kommentarer och anteckningar i PDF-filen stöds inte.

   ![Förhandsgranska PDF-filer i  [!DNL Experience Manager] PDF Viewer](/help/assets/assets/preview-pdf-file-viewer.png)

* En förbättring av användarupplevelsen visar antalet resurser i en mapp. För mer än 1 000 resurser i en mapp visar [!DNL Assets] 1 000+.

   ![Antalet resurser i en mapp visas i gränssnittet](/help/assets/assets/browse-folder-number-of-assets.png)

* Du kan direkt använda ett metadatamatchema för en mapp i dess [!UICONTROL Properties].

   ![Lägg till metadatamatchemat från mappegenskaper](/help/assets/assets/metadata-schema-folder-properties.png)

### Fel som har korrigerats i [!DNL Assets] {#bugs-fixed-assets}

* När du lägger till en ägare till en undermapp lägger [!DNL Assets] även till samma användare som en ägare till den överordnade mappen. (CQ-4323737)
* När användaren lägger till resurser i samlingar och använder ett filter vid sökning i samlingar kan användaren inte visa samlingar i listvyn. (CQ-4323181)
* När användaren söker efter filer och mappar och väljer [!UICONTROL Files & Folders] visas bara filerna men inte mappen. (CQ-4319543)

## [!DNL Experience Manager Sites] som  [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#ga-features-sites}

* Publicera till förhandsgranskningsnivå visas nu som sidstatus i användargränssnittet för webbplatsadministratörer
* Publicera på förhandsgranskningsnivå nu med förhandsgransknings-URL:en i slutet av åtgärden och behåll URL:en i sidegenskaperna för senare referens

## [!DNL Adobe Experience Manager Forms] som  [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* Lagt till möjlighet att filtrera anpassade kolumner AEM Inkorgen.
* Lagt till möjlighet att använda temaredigeraren och stillagret i en adaptiv formulärredigerare för att formatera captcha-komponenten.
* Snabbare och exaktare för automatisk detektering av logiska avsnitt i PDF forms och konvertering av dessa till motsvarande adaptiva formulärpaneler.
* Flyttningsåtgärd har lagts till för att flytta en PDF- eller XDP-fil från en mapp till en annan.

### Betafunktion i [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: Med kommunikations-API:er kan du kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera slutliga formulärdokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera utskrifts-PDF:er från ett XFA-formulär i PDF- och Adobe Acrobat-format (AcroForm).

* **Variable Data Externalizer**: Du kan spara data AEM arbetsflödesvariabler i ett externt lagringssystem som hanteras av din organisation.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

### Fel som har korrigerats i [!DNL Forms] {#forms-bugs-fixed}

* När ett fält valideras innan data skickas till backend-tjänsten via FDM (Form Data Model), lyckas valideringen men tjänsten Form Data Model kan inte anropa eftervalideringen.
* När du skickar ett formulär som innehåller ett vanligt HTML-överföringsfält från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0-byte-fil tas emot i den andra änden. Detta är ett känt problem i Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Adobe Experience Manager Screens] som  [!DNL Cloud Service] {#screens}

I det här avsnittet beskrivs versionsinformationen för AEM Screens som en Cloud Service.

### Releasedatum {#release-date-june-screens}

Releasedatum för AEM Screens som Cloud Service är 24 juni 2021.

### Nyheter {#what-is-new-screens-june}

>[!NOTE]
>Se [AEM Screens som Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) Guide för grundläggande kunskaper som krävs för att installera, konfigurera och köra skärmar som en Cloud Service och länka till detaljerad teknisk dokumentation om koncept.

* Registreringshantering för flera enheter innebär att det går snabbare och effektivare att etablera stora mängder spelarenheter.

* Förbättrade sök- och filteralternativ för var och en av lagervyerna Enhet, Visning och Kanal.

* Ögonblicksbilden av enhetens hälsostatus sparar tid genom att ge en snabb översikt av kritisk status.

* På sidan med objektinformation finns en sammanfattning av den mest relevanta informationen för varje objekt i ditt projekt.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Nya referensdatatyper för CIF-produkt och kategori för innehållsfragment (Inkl. användargränssnittsstöd för produkt-/kategoriväljare)
* Ny kärnkomponent för Commerce Content Fragment
* Heltextbaserad e-handelssökning stöds i AEM
* Commerce Core Components stöder datainsamling i Adobe Commerce Sensei Recs
* Förbättrade SEO-vänliga URL:er för kategorisidor
* Stöd för anpassade HTTP-huvuden per plats/konfiguration

## Content Transfer Tool {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för Content Transfer Tool v1.5.4 är 28 juni 2021.

### Nyheter {#what-is-new-ctt-latest}

* Stöd för ett valfritt [pre-copy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)-steg som lagts till för att användas med CTT. Steg före kopiering kan användas för att avsevärt snabba upp extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten när AEM är konfigurerad att använda ett Amazon S3- eller Azure Blob Storage-datalager.

* Guardrail har lagts till i CTT för att förhindra användare från att stoppa ett intag och eventuellt skada data när det har nått den kritiska punkten under intagningsfasen.

* Extraheringsloggarna har blivit mer beskrivande och hjälper till vid felsökning.

* Lagt till mer beskrivande statusmeddelanden för förtäring i användargränssnittet.

### Felkorrigeringar {#bug-fixes-ctt-latest}

* När ett förtäring på Author-instansen stoppades skrev användargränssnittet över ett tidigare slutfört intag på Publish-instansen till `STOPPED` från `FINISHED`. Den här har åtgärdats.


