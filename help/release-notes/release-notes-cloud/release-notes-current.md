---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: c30470b321a4fba8c8de9becb62c518faff05498
workflow-type: tm+mt
source-wordcount: '1105'
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

* Med funktionen för innehållsautomatisering kan [!DNL Experience Manager Assets] utnyttja API:erna för [!DNL Adobe Creative Cloud] för att automatisera materialproduktionen i stor skala. Det förbättrar innehållets hastighet genom att dramatiskt minska den tid det tar och de iterationer som krävs för att skapa varianter av samma material. Funktionen kräver ingen kod och fungerar inifrån DAM.
* [!DNL Adobe Asset Link] v3.0 for  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]and  [!DNL Adobe InDesign] and  [!DNL Adobe Asset Link] v2.0 for  [!DNL Adobe XD] släpps. Den innehåller följande:

   * Stöd för [!DNL Assets Essentials].
   * Möjlighet att automatiskt ansluta till [!DNL Experience Manager] som [!DNL Cloud Service] eller [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Nya funktioner som är tillgängliga i betaversionskanalen [!DNL Assets] {#beta-features-assets}

* Vyinställningarna har förbättrats så att användarna kan välja en standardvy och en standardsorteringsparameter.
* Länkdelningsfunktionen använder asynkrona nedladdningar som ökar nedladdningshastigheten.
* Användare kan söka efter och filtrera mapparna baserat på egenskapspredikat.
* [!DNL Experience Manager Assets] bäddar in PDF Viewer-filen som används av  [!DNL Adobe Document Cloud] för att förhandsgranska de dokument som stöds. Med den här funktionen kan användarna förhandsgranska PDF-filer och andra flersidiga filer utan komplex bearbetning. Detta förbättrar funktionspariteten med [!DNL Experience Manager] 6.5.

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

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Nya referensdatatyper för CIF-produkt och kategori för innehållsfragment (Inkl. användargränssnittsstöd för produkt-/kategoriväljare)
* Ny kärnkomponent för Commerce Content Fragment
* Heltextbaserad e-handelssökning stöds i AEM
* Commerce Core Components stöder datainsamling i Adobe Commerce Sensei Recs
* Förbättrade SEO-vänliga URL:er för kategorisidor
* Stöd för anpassade HTTP-huvuden per plats/konfiguration


