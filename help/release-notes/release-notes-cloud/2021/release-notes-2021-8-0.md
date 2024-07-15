---
title: Versionsinformation för version 2021.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner. Exempel: för 2020 och 2021.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2021.8.0) är 26 augusti 2021.
Följande version (2021.9.0) är den 6 oktober 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt från augusti 2021](https://video.tv.adobe.com/v/336277) om du vill se en sammanfattning av de funktioner som lagts till.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* När du delar digitala resurser som en länk kan användaren kopiera URL:en till Urklipp direkt. Förbättringen gör att du kan dela resurser snabbare och bekvämare. Den här funktionen gör det möjligt att dela material snabbare och smidigt.

  ![Alternativet Kopiera URL när en resurs delas som en länk](/help/assets/assets/link-share-copy-URL-option.png)
  *Bild: När du delar en resurs som en länk kan du nu kopiera URL-adressen och dela den separat.*

* När du överför TXT-filer genereras en miniatyrbild automatiskt av resursens mikrotjänster. PNG-miniatyrbilden är en återgivning av en TXT-fil som gör det lättare för användare att identifiera innehållet eller filerna i viss utsträckning, utan att öppna filerna. Den här funktionen kräver ingen konfiguration och fungerar som standard.

  ![En återgivning av en TXT-fil genereras automatiskt av [!DNL Assets] i PNG-format](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *Bild: En återgivning av en TXT-fil genereras automatiskt så att du kan identifiera filen utan att öppna den.*

### Ny funktion i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

* Användarna kan nu sortera de resurser som visas i sökresultaten i kolumn- och kortvyn. Sorteringen fungerar på kolumnerna Namn, Skapad, Ändrad eller Ingen.

  ![Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyer ](/help/assets/assets/sort-searched-assets.png)
  *Figur: Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyer.*

### Fel som har åtgärdats i [!DNL Assets] {#assets-bugs-fixed}

* När en medlem i medverkargruppen navigerar till [!DNL Assets]-konsolen skapas en extra `POST`-begäran för att skapa en samling. Denna begäran är inte obligatorisk. Den misslyckas på grund av behörighetsproblem och skapar många fel i loggarna. (CQ-4328856)
* När användare visar en resurs och väljer [!UICONTROL Timeline] på snabbmenyn i den vänstra panelen visas ett fel. I loggarna loggas många varningar på grund av en felaktig fråga. (CQ-4328919)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* Tjänsten Automated forms conversion kan [konvertera PDF forms på italienska och portugisiska](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) till Adaptiv Forms.

* **Acroform-based Document of Record**: AEM Forms as a Cloud Service stöder användning av [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) som mall för arkivhandlingar förutom XFA-baserad formulärmall.

* **Microsoft® Azure-datalageranslutning**: Nu kan du [ansluta formulärdatamodellen till Microsoft® Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html). Med den kan du hämta och lagra adaptiva formulärdata i Microsoft® Azure Storage som en BLOB.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

* **Använd Adobe Sign-roller i ett adaptivt formulär** - Adobe Sign för företags- och företagsnivåer kan eventuellt utöka rollerna för avtalsmottagare, utöver bara signeraren, för att bättre matcha deras arbetsflödesbehov. Nu kan du göra det möjligt för alla mottagare av avtalet att konfigurera sin roll i ett adaptivt formulär, med signerare som standardroll.

* **Analytics for Adaptive Forms** - Nu kan du hämta in och spåra slutanvändarbeteende via Adobe Analytics for Adaptive Forms för att samla in slutanvändarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra slutanvändarens upplevelse.

* **Anslut enkelt AEM Forms med Microsoft® Dynamics och Salesforce.com** - Tjänsten tillhandahåller färdig datakällkonfiguration och datamodeller för Microsoft® Dynamics och Salesforce.com. Detta gör det snabbare och enklare för utvecklare att konfigurera Microsoft® Dynamics och Salesforce.com som datakällor för ett anpassat formulär.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Nytt användargränssnitt för kategoriväljare för förbättrad användarupplevelse, ökad effektivitet och bättre stöd för komplex produktkatalog

  ![Ny kategoriväljare](/help/assets/CIF/category-picker.png)

* Bättre stöd för A11Y för CIF kärnkomponenter

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.8.0 och 2021.7.0.

## Releasedatum {#release-date-cm-aug}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.8.0 är 12 augusti 2021.
Nästa version är planerad till 9 september 2021.

### Nyheter {#what-is-new-aug}

* Cloud Service kan nu visa serviceavtalsrapporter (SLA) i Cloud Manager. Detta kommer att göras tillgängligt successivt under de närmaste månaderna.
Se [SLA-rapportering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/sla-reporting.html).

* Typen och allvarlighetsgraden för kvalitetsreglerna IndexType och `IndexDamAssetLucene` har ändrats. De här felen är nu båda Buggar med blockerarens *allvarlighetsgrad*.

* Nya kvalitetsregler för Oak-index har införts för att omfatta asynkrona konfigurationer och Tika-konfigurationer.

* Öka det högsta antalet SSL-certifikat per program till 50.

* Självbetjäning som gör att användare kan skapa och hantera flera databaser med hjälp av Cloud Manager-gränssnittet.

* SonarQube läste historikdata för Git i onödan. På stora kodbaser kan detta leda till en onödig prestandaförbättring.

* Det finns nu ett API för att göra Maven-beroendecachen ogiltig per pipeline.

* Den version av AEM Project Archetype som används av Cloud Manager har uppdaterats till version 29.

### Felkorrigeringar {#bug-fixes-aug}

* Status för tillgänglig uppdatering ska inte visas när den senaste versionen är mindre än den aktuella versionen.

* Inledande introduktion misslyckades för nya organisationer med långa namn.

* När en pipeline aktiveras två gånger av någon anledning resulterar det ibland i att en av körningarna misslyckas med ett *`cannot update pipeline execution status`*-fel.

## Verktyget Innehållsöverföring {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för Content Transfer Tool v1.5.6 är 11 augusti 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* Ibland migrerades inte alla användare till målinstansen. För att åtgärda detta krävs CTT v1.5.6 tillsammans med aem-ethos-tools 1.2.354 eller senare version på AEM as a Cloud Service-målinstansen.

* Knappen **Stoppa inmatning** inaktiverades under importen till Publish-instansen. Detta är inte nödvändigt eftersom det inte finns något steg för monoåterställning vid intag av Publish.

* CTT rensade inte katalogen `/tmp` efter en lyckad extrahering. Detta kan leda till problem med diskutrymmet.
