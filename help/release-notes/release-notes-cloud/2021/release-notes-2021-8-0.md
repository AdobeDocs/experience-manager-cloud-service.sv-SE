---
title: Versionsinformation om 2021.8.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2021.8.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1031'
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

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2021.8.0) är 26 augusti 2021.
Följande version (2021.9.0) är den 6 oktober 2021.

## Släpp video {#release-video}

Ta en titt på [Versionsöversikt augusti 2021](https://video.tv.adobe.com/v/336277) video med en sammanfattning av tillagda funktioner.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* När användarna delar digitala resurser som en länk kan de kopiera URL:en till Urklipp direkt. Förbättringen gör att du kan dela resurser snabbare och bekvämare. Den här funktionen gör det möjligt att dela material snabbare och smidigt.

   ![Alternativet Kopiera URL när du delar en resurs som en länk](/help/assets/assets/link-share-copy-URL-option.png)
   *Bild: När du delar en resurs som en länk kan du nu kopiera URL-adressen och dela den separat.*

* När du överför TXT-filer genererar resursens mikrotjänster automatiskt en miniatyrbild. PNG-miniatyrbilden är en återgivning av TXT-filen som gör det lättare för användare att identifiera innehållet eller filerna i viss utsträckning, utan att öppna filerna. Den här funktionen kräver ingen konfiguration och fungerar som standard.

   ![En återgivning av en TXT-fil genereras automatiskt av [!DNL Assets] i PNG-format](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Bild: En återgivning av en TXT-fil genereras automatiskt så att du lättare kan identifiera filen utan att öppna den.*

### Ny funktion i [!DNL Assets] prerelease channel {#assets-prerelease-features}

* Användarna kan nu sortera de resurser som visas i sökresultaten i kolumn- och kortvyn. Sorteringen fungerar på kolumnerna Namn, Skapad, Ändrad eller Ingen.

   ![Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyer](/help/assets/assets/sort-searched-assets.png)
   *Bild: Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyn.*

### Fel som har åtgärdats i [!DNL Assets] {#assets-bugs-fixed}

* När en medlem i medverkargruppen navigerar till [!DNL Assets] Konsol, en extra `POST` begäran genereras för att försöka skapa en samling. Denna begäran är inte obligatorisk, den misslyckas på grund av behörighetsproblem och skapar många fel i loggarna. (CQ-4328856)
* När användare visar en resurs och väljer [!UICONTROL Timeline] på popup-menyn i den vänstra panelen visas ett fel. I loggarna loggas många varningar på grund av en felaktig fråga. (CQ-4328919)

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* automated forms conversion service kan [konvertera PDF forms till italienska och portugisiska](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) till Adaptiv Forms.

* **Acroform-based Document of Record**: AEM Forms as a Cloud Service stöder användning av [Adobe Acrobat Form PDF (Acrobat PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) som en mall för postdokument förutom XFA-baserad formulärmall.

* **Microsoft Azure-dataarkivanslutning**: Nu kan du [ansluta formulärdatamodell till Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Det gör att du kan hämta och lagra adaptiva formulärdata till Microsoft Azure Storage som en BLOB.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* **Använda Adobe Sign-roller i ett adaptivt formulär**: Adobe Sign för företags- och företagsnivåer har möjlighet att utöka rollerna för avtalsmottagare, utöver bara signeraren, så att de bättre motsvarar deras arbetsflödesbehov. Nu kan du göra det möjligt för alla mottagare av avtal att konfigurera sin roll i ett adaptivt formulär, med signerare som standardroll.

* **Analytics för Adaptive Forms**: Nu kan du samla in och spåra användarbeteende via Adobe Analytics för Adaptive Forms för att få information om slutanvändarna. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

* **Anslut enkelt AEM Forms med Microsoft Dynamics och Salesforce.com**: Tjänsten tillhandahåller direkt konfiguration av datakällor och datamodeller för Microsoft Dynamics och Salesforce.com, vilket gör det snabbare och enklare för utvecklare att konfigurera Microsoft Dynamics och Salesforce.com som datakällor för ett adaptivt formulär.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Nytt användargränssnitt för kategoriväljare för förbättrad användarupplevelse, ökad effektivitet och bättre stöd för komplexa produktkataloger

   ![Ny kategoriväljare](/help/assets/CIF/category-picker.png)

* Bättre stöd för A11Y för CIF Core-komponenter

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.8.0 och 2021.7.0.

## Releasedatum {#release-date-cm-aug}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.8.0 är 12 augusti 2021.
Nästa version är planerad till 9 september 2021.

### Nyheter {#what-is-new-aug}

* Cloud Service kan nu visa serviceavtalsrapporter (SLA) i Cloud Manager. Detta kommer att göras tillgängligt stegvis under de närmaste månaderna.
Se [SLA-rapportering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) om du vill veta mer.

* Typ och allvarlighetsgrad för IndexType och `IndexDamAssetLucene` kvalitetsreglerna har ändrats. Nu finns båda Bugs of Blocker *serverity*.

* Nya kvalitetsregler för Oak-index har införts för att omfatta asynkrona konfigurationer och kodkonfigurationer.

* Öka det högsta antalet SSL-certifikat per program till 50.

* Självbetjäning som gör att användare kan skapa och hantera flera databaser via användargränssnittet i Cloud Manager.

* SonarQube läste historikdata för Git i onödan. På stora kodbaser kan detta leda till en onödig prestandaförbättring.

* Det finns nu ett API för att göra Maven-beroendecachen ogiltig per pipeline.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 29.

### Felkorrigeringar {#bug-fixes-aug}

* Status för tillgänglig uppdatering ska inte visas när den senaste versionen är mindre än den aktuella versionen.

* Inledande introduktion misslyckades för nya organisationer med mycket långa namn.

* När en pipeline av någon anledning aktiveras två gånger resulterar det ibland i att en av körningarna misslyckas med *det går inte att uppdatera körningsstatus för pipeline* fel.

## Content Transfer Tool {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för Content Transfer Tool v1.5.6 är 11 augusti 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* I vissa fall migrerades inte alla användare till målinstansen. För att få den här korrigeringen krävs CTT v1.5.6 tillsammans med aem-ethos-tools 1.2.354 eller senare version på AEM as a Cloud Service målinstansen.

* The **Stoppa inmatning** -knappen inaktiverades under hämtning till Publish-instansen. Detta är inte nödvändigt eftersom det inte finns något steg för monoåterställning vid publiceringsintag.

* CTT rensade inte `/tmp` efter en lyckad extrahering. Detta kan leda till problem med diskutrymmet.
