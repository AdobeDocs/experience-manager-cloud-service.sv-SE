---
title: Versionsinformation för version 2021.6.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.6.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 är 28 juni 2021.
Följande version (2021.7.0) kommer att vara den 29 juli 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt för juni 2021](https://video.tv.adobe.com/v/334296) om du vill se en sammanfattning av de funktioner som lagts till.

## XML Documentation för AEM som molntjänst {#xml-documentation}

### Nyheter {#what-is-new-xml-documentation}

* XML Documentation för AEM as a Cloud Service är nu GA.
* Detta gör att befintliga AEM Cloud Service-kunder kan köpa XML Documentation-tillägg för import, skapande, hantering och leverans av tekniskt innehåll i flera kanaler, inklusive AEM sajter

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.6.0 och 2021.5.0.

### Releasedatum {#release-date-june-cm}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.6.0 är 10 juni 2021.
Nästa version är planerad till 15 juli 2021.

### Nyheter {#what-is-new-junecm}

* Förhandsgranskningstjänsten kommer att distribueras rullande till alla program. Kunder meddelas i produkten när deras program är aktiverat för förhandsgranskningstjänsten. Mer information finns i [Åtkomst till förhandsgranskningstjänsten](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

* Maven Dependencies som laddas ned under byggfasen cachelagras nu mellan pipeline-körningar. Den här funktionen kommer att aktiveras för kunderna under de kommande veckorna.

* Namnet på programmet kan nu redigeras via dialogrutan Redigera program.

* Det standardförgreningsnamn som används både när projektet skapas och i det förvalda push-kommandot via Hantera Git-arbetsflöden har ändrats till `main`.

* Redigera programupplevelser i användargränssnittet har uppdaterats.

* Kvalitetsregeln `ImmutableMutableMixCheck` har uppdaterats för att klassificera `/oak:index`-noder som oföränderliga.

* Kvalitetsreglerna `CQBP-84` och `CQBP-84--dependencies` har konsoliderats till en enda regel. Som en del av den här konsolideringen identifierar genomsökningen av beroenden mer korrekt problem i tredjepartsberoenden som distribueras till AEM.

* För att undvika problem har segmentraderna i Publish AEM och Publish Dispatcher konsoliderats på sidan Miljöinformation.

  ![Dispatcher-miljöer](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* En ny regel för kodkvalitet har lagts till för att validera strukturen för `damAssetLucene` index. Mer information finns i [Anpassade DAM-resurser, Lucene Oak-index](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check).

* Sidan med miljöinformation visar nu flera domännamn för Publish och förhandsgranskningstjänsterna (beroende på vad som är tillämpligt). Mer information finns i [Miljöinformation](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Felkorrigeringar {#bug-fixes-junecm}

* JCR-noddefinitioner som innehåller en ny rad efter att rotelementnamnet inte tolkades korrekt.

* API för listdatabaser filtrerar inte borttagna databaser.

* Ett felaktigt felmeddelande visades när ett ogiltigt värde angavs för schemasteget.

* Ibland kan användaren se en grön *active*-status bredvid ett IP-Tillåtelselista även när konfigurationen inte har distribuerats.

* Vissa programredigeringssekvenser kan leda till att produktionsflödet inte kan skapas eller redigeras.

* Vissa programredigeringssekvenser kan resultera i att sidan **Översikt** visar ett missvisande meddelande om att köra programkonfigurationen igen.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#ga-features-assets}

* Med funktionen för innehållsautomatisering kan [!DNL Experience Manager Assets] använda [!DNL Adobe Creative Cloud] API:er för att automatisera resursproduktionen i stor skala. Det förbättrar innehållets hastighet genom att dramatiskt minska den tid det tar och de iterationer som krävs för att skapa varianter av samma material. Funktionen kräver ingen kod och fungerar inifrån DAM.
* [!DNL Adobe Asset Link] v3.0 för [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] och [!DNL Adobe InDesign] och [!DNL Adobe Asset Link] v2.0 för [!DNL Adobe XD] har släppts. Den innehåller följande:

   * Stöd för [!DNL Assets Essentials].
   * Möjlighet att automatiskt ansluta till [!DNL Experience Manager] som [!DNL Cloud Service] eller [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Nya funktioner som är tillgängliga i betaversionskanalen [!DNL Assets] {#beta-features-assets}

* Vyinställningarna har förbättrats så att användarna kan välja en standardvy och en standardsorteringsparameter.
* Länkdelningsfunktionen använder asynkrona nedladdningar som ökar nedladdningshastigheten.
* Användare kan söka efter och filtrera mapparna baserat på egenskapspredikat.
* [!DNL Experience Manager Assets] bäddar in PDF Viewer från [!DNL Adobe Document Cloud] för att förhandsgranska de dokument som stöds. Med den här funktionen kan användare förhandsgranska PDF och andra flersidiga filer utan komplex bearbetning. Detta förbättrar funktionspariteten med [!DNL Experience Manager] 6.5.

### Fel som har åtgärdats i [!DNL Assets] {#bugs-fixed-assets}

* När du lägger till en ägare till en undermapp lägger [!DNL Assets] även till samma användare som en ägare till den överordnade mappen. (CQ-4323737)
* När användaren lägger till resurser i samlingar och använder ett filter vid sökning i samlingar kan användaren inte visa samlingar i listvyn. (CQ-4323181)
* Om användaren använder ett filter och väljer [!UICONTROL Files & Folders] när han söker efter filer och mappar visas bara filerna, men inte mappen. (CQ-4319543)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#ga-features-sites}

* Publish till förhandsgranskningsnivå visas nu som sidstatus i användargränssnittet för webbplatsadministratörer
* Publish to Preview Tier now surface preview URL at end the action and persistent the URL in page properties for later reference

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* Lagt till möjlighet att filtrera anpassade kolumner AEM Inkorgen.
* Lagt till möjlighet att använda temaredigeraren och stillagret i en adaptiv formulärredigerare för att formatera captcha-komponenten.
* Snabbare och exaktare för automatisk detektering av logiska avsnitt i PDF forms och konvertering av dessa till motsvarande adaptiva formulärpaneler.
* Flyttningsåtgärd har lagts till för att flytta en PDF- eller XDP-fil från en mapp till en annan.

### Beta-funktion i [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: Kommunikations-API:er hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera slutliga formulärdokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera PDF från ett XFA-formulär i PDF och Adobe Acrobat-formulär (AcroForm).

* **Variable Data Externalizer**: Du kan spara data AEM arbetsflödesvariabler i ett externt lagringssystem som hanteras av din organisation.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

### Fel som har åtgärdats i [!DNL Forms] {#forms-bugs-fixed}

* När ett fält valideras innan data skickas till backend-tjänsten via FDM (Form Data Model), lyckas valideringen men tjänsten Form Data Model kan inte anropa eftervalideringen.
* När du skickar ett formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0-byte-fil tas emot i den andra änden. Detta är ett känt problem i Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] som en [!DNL Cloud Service] {#screens}

I det här avsnittet beskrivs versionsinformationen för AEM Screens as a Cloud Service.

### Releasedatum {#release-date-june-screens}

Releasedatum för AEM Screens as a Cloud Service är 24 juni 2021.

### Nyheter {#what-is-new-screens-june}

>[!NOTE]
>Se [AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=sv-SE) Guide för grundläggande kunskaper som krävs för att installera, konfigurera och köra Screens as a Cloud Service samt länka till detaljerad teknisk dokumentation om koncept.

* Registreringshantering för flera enheter innebär att det går snabbare och effektivare att etablera stora mängder spelarenheter.

* Förbättrade sök- och filteralternativ för var och en av lagervyerna Enhet, Visning och Kanal.

* Ögonblicksbilden av enhetens hälsostatus sparar tid genom att ge en snabb översikt av kritisk status.

* På sidan med objektinformation finns en sammanfattning av den mest relevanta informationen för varje objekt i ditt projekt.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Nya CIF för produkt- och kategorireferensdatatyper för innehållsfragment (Inkl. användargränssnitt för produkt-/kategoriväljare)
* Ny kärnkomponent i Commerce Content Fragment
* Heltextbaserad e-handelssökning stöds i AEM
* Commerce Core Components har stöd för Adobe Commerce Sensei Recs datainsamling
* Förbättrade SEO-vänliga URL:er för kategorisidor
* Stöd för anpassade HTTP-huvuden per plats/konfiguration

## Verktyget Innehållsöverföring {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för Content Transfer Tool v1.5.4 är 28 juni 2021.

### Nyheter {#what-is-new-ctt-latest}

* Stöd för ett valfritt [pre-copy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=sv-SE)-steg som lagts till för att användas med CTT. Steg före kopiering kan användas för att avsevärt snabba upp extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten när AEM är konfigurerad att använda ett Amazon S3- eller Azure Blob Storage-datalager.

* Guardrail har lagts till i CTT för att förhindra användare från att stoppa ett intag och eventuellt skada data när det har nått den kritiska punkten under intagningsfasen.

* Extraheringsloggarna har blivit mer beskrivande och hjälper till vid felsökning.

* Lagt till mer beskrivande statusmeddelanden för förtäring i användargränssnittet.

### Felkorrigeringar {#bug-fixes-ctt-latest}

* När ett förtäring på författarinstansen stoppades skrev användargränssnittet över ett tidigare slutfört intag på Publish-instansen till `STOPPED` från `FINISHED`. Den här har åtgärdats.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.16 är 30 juni 2021.

### Nyheter {#what-is-new-bpa-latest}

* Det går att identifiera och rapportera om saknade underordnade noder i mappar under `/content/dam`.

* Möjlighet att identifiera och rapportera vilken version av Best Practices Analyzer som används.

### Felkorrigeringar {#bug-fixes-bpa-latest}

* Loggningsfel relaterat till en databasstruktur som inte stöds (URS) har åtgärdats.
