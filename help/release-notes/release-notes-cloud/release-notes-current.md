---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 29af6f91f5aeb6ad971a35637f1635e0b038a57f
workflow-type: tm+mt
source-wordcount: '1627'
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

Lanseringsdatumet [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] aktuell version (2021.8.0) är 26 augusti 2021.
Följande version (2021.9.0) är den 4 oktober 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt från augusti 2021](https://video.tv.adobe.com/v/336277) om du vill se en sammanfattning av de nya funktionerna.

## [!DNL Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* När användarna delar digitala resurser som en länk kan de kopiera URL:en till Urklipp direkt. Förbättringen gör att du kan dela resurser snabbare och bekvämare. Den här funktionen gör det möjligt att dela material snabbare och smidigt.

   ![Alternativet Kopiera URL när du delar en resurs som en länk](/help/assets/assets/link-share-copy-URL-option.png)
   *Bild: När du delar en resurs som en länk kan du nu kopiera URL-adressen och dela den separat.*

* När du överför TXT-filer genererar resursens mikrotjänster automatiskt en miniatyrbild. PNG-miniatyrbilden är en återgivning av TXT-filen som gör det lättare för användare att identifiera innehållet eller filerna i viss utsträckning, utan att öppna filerna. Den här funktionen kräver ingen konfiguration och fungerar som standard.

   ![En återgivning av en TXT-fil genereras automatiskt av  [!DNL Assets] i PNG-format](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Bild: En återgivning av en TXT-fil genereras automatiskt så att du lättare kan identifiera filen utan att öppna den.*

### Ny funktion i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

* Användarna kan nu sortera de resurser som visas i sökresultaten i kolumn- och kortvyn. Sorteringen fungerar på kolumnerna Namn, Skapad, Ändrad eller Ingen.

   ![Sortera sökresultaten  [!DNL Assets] i kolumn- och kortvyn](/help/assets/assets/sort-searched-assets.png)
   *Bild: Sortera sökresultaten  [!DNL Assets] i kolumn- och kortvyn.*

### Fel som har korrigerats i [!DNL Assets] {#assets-bugs-fixed}

* När en medlem i medverkargruppen navigerar till [!DNL Assets]-konsolen skapas en extra `POST`-begäran för att försöka skapa en samling. Denna begäran är inte obligatorisk, den misslyckas på grund av behörighetsproblem och skapar många fel i loggarna. (CQ-4328856)
* När användare visar en resurs och väljer [!UICONTROL Timeline] på popup-menyn i den vänstra panelen visas ett fel. I loggarna loggas många varningar på grund av en felaktig fråga. (CQ-4328919)

## [!DNL Experience Manager Forms] som  [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* AEM Archetype-projekt för Forms som Cloud Service innehåller nu [formulärdatamodeller för Microsoft Dynamics och Salesforce.com](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment).

* **Acroform-based Document of Record**: AEM Forms som Cloud Service har stöd för att använda  [Adobe Acrobat Form PDF (Acrobat PDF) ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) som en mall för arkivhandlingar förutom XFA-baserad formulärmall.

* **Microsoft Azure-dataarkivanslutning**: Du kan nu  [ansluta formulärdatamodellen till Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Det gör att du kan hämta och lagra adaptiva formulärdata till Microsoft Azure Storage som en BLOB.

### Betafunktion i [!DNL Forms] {#aug-what-is-new-forms-prerelease}

* **Enhetlig lagringskontakt:** Använd Enhetlig lagringskontakt för att externalisera processdata i kundhanterade databaser. Du kan till exempel
   * Möjliggör Forms Portals funktioner för att spara och återuppta samt lagra adaptiva formulärutkast i ett kundhanterat datalager.
   * Lagra AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga personuppgifter (SPD) i en kundhanterad databas.

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [Communication ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) API - använd XDP-mallar och XML-data för att generera trycksaker i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera tryckta PDF-filer från ett XFA-formulär i PDF- och Adobe Acrobat-format.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

### Nya funktioner i prerelease Channel [!DNL Forms] {#prerelease-features-forms}

* **Använd Adobe Sign-roller i ett adaptivt format**: Adobe Sign för företags- och företagsnivåer har möjlighet att utöka rollerna för avtalsmottagare, utöver bara signeraren, så att de bättre motsvarar deras arbetsflödesbehov. Du kan nu [aktivera varje mottagare av avtal att konfigurera sin roll i ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform), med signerare som standardroll.

* **Analytics for Adaptive Forms**: Nu kan du samla in och spåra användarbeteende via Adobe Analytics för Adaptive Forms för att få information om slutanvändarna. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

* **Anslut enkelt AEM Forms med Microsoft Dynamics och Salesforce.com**: Tjänsten tillhandahåller direkt konfiguration av datakällor och datamodeller för Microsoft Dynamics och Salesforce.com, vilket gör det  [snabbare och enklare för utvecklare att konfigurera Microsoft Dynamics och Salesforce.com som datakällor för ett anpassningsbart formulär](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html).

## [!DNL Experience Manager Screens] som  [!DNL Cloud Service] {#screens}

### Vad är nytt? {#what-is-new-screens}

* Skärmar som Cloud Service har nu stöd för grundläggande uppspelningsövervakning. Spelaren rapporterar nu olika uppspelningsmått för varje ping (standardvärdet är 30 sekunder). Baserat på mätvärden ger det möjlighet att upptäcka olika kantfall (fastnålade upplevelser, tom skärm, schemaläggningsproblem osv.). Med den här funktionen kan teamet fjärrövervaka om en spelare spelar upp innehåll, förbättrar reaktiviteten till tomma skärmar eller trasiga upplevelser i fältet och minskar risken för att slutanvändaren får en trasig upplevelse.
Mer information finns i [Grundläggande uppspelningsövervakning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring).

* Miniatyrbildsstöd för videor i stöds nu som Cloud Service på skärmar. Innehållsförfattare kan definiera en miniatyrbild för videoklipp så att bilden kan användas som platshållare och testa uppspelning och målgruppsanpassning av innehållet medan videon färdigställs av rätt team. Bilden kan också användas om videouppspelningen misslyckas.
Mer information finns i [Stöd för miniatyrbilder för videoklipp](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html).

### Felkorrigeringar {#bug-fixes-screens}

* Spelaren kunde inte visa innehåll från den inbäddade sidan och problemet är nu åtgärdat.

* Efter en lyckad inloggning hamnade navigeringen till standardsidan (kanalerna) i en intern serverfelsida.

* Associerade taggposter togs inte bort när spellistor togs bort.


## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Nytt användargränssnitt för kategoriväljare för förbättrad användarupplevelse, ökad effektivitet och bättre stöd för komplexa produktkataloger

   ![Ny kategoriväljare](/help/assets/CIF/category-picker.png)

* Bättre stöd för A11Y för CIF Core-komponenter

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.9.0 och 2021.8.0.

## Releasedatum {#release-date-cm-sept}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.9.0 är 9 september 2021.
Nästa version är planerad till 7 oktober 2021.

### Nyheter {#what-is-new-cm-sept}

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 30.

* Programkorten på Cloud Managers landningssida och den tillhörande upplevelsen har uppdaterats.

* Kodkvalitetsstegloggen innehåller nu utförlig loggningsinformation om OakPal-skanningen.

* Menyalternativen på sidan Aktivitet kommer nu att innehålla ett alternativ till **Hämta logg** för slutförda kodgeneratorkörningar. Om du väljer det här alternativet hämtas loggen för byggsteget.

* Om du klickar direkt på programkortet går du nu till sidan Översikt över Cloud Manager.


### Felkorrigeringar {#bug-fixes-sept}

* Användaren kommer nu att se ett mer begripligt meddelande när han/hon försöker lägga till ett nytt IP-Tillåtelselista i ett program som har nått det högsta tillåtna antalet IP-Tillåtelselista som kan konfigureras.

* Fel URL kopierades när menyalternativet Kopiera URL valdes på skärmen Databaser.

## Releasedatum {#release-date-cm-aug}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.8.0 är 12 augusti 2021.

### Nyheter {#what-is-new-aug}

* Cloud Service kan nu visa serviceavtalsrapporter (SLA) i Cloud Manager. Detta kommer att göras tillgängligt stegvis under de närmaste månaderna.
Mer information finns i [SLA-rapportering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html).

* Typen och allvarlighetsgraden för kvalitetsreglerna IndexType och `IndexDamAssetLucene` har ändrats. Dessa är nu båda Bugs of Blocker *serverity*.

* Nya kvalitetsregler för Oak-index har införts för att omfatta asynkrona konfigurationer och kodkonfigurationer.

* Öka det högsta antalet SSL-certifikat per program till 50.

* Självbetjäning som gör att användare kan skapa och hantera flera databaser via användargränssnittet i Cloud Manager.

* SonarQube läste historikdata för Git i onödan. På stora kodbaser kan detta leda till en onödig prestandaförbättring.

* Det finns nu ett API för att göra Maven-beroendecachen ogiltig per pipeline.

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 29.

### Felkorrigeringar {#bug-fixes-aug}

* Status för tillgänglig uppdatering ska inte visas när den senaste versionen är mindre än den aktuella versionen.

* Inledande introduktion misslyckades för nya organisationer med mycket långa namn.

* När en pipeline aktiveras två gånger av någon anledning resulterar det i att en av körningarna misslyckas med *det går inte att uppdatera pipelinekörningsstatus*-fel.

## Content Transfer Tool {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för Content Transfer Tool v1.5.6 är 11 augusti 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* I vissa fall migrerades inte alla användare till målinstansen. För att få den här korrigeringen krävs CTT v1.5.6 tillsammans med aem-ethos-tools 1.2.354 eller senare version på AEM som en Cloud Service-instans.

* Knappen **Stoppa inmatning** inaktiverades under hämtning till Publish-instansen. Detta är inte nödvändigt eftersom det inte finns något steg för monoåterställning vid publiceringsintag.

* CTT rensade inte katalogen `/tmp` efter en lyckad extrahering. Detta kan leda till problem med diskutrymmet.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa-latest}

Releasedatum för Best Practices Analyzer v2.1.18 är 2 september 2021.

### Nyheter {#what-is-new}

* Möjlighet att identifiera och rapportera totalt antal noder.

* Möjlighet att identifiera och rapportera om nodlagringstyp och -storlek.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA upptäckte felaktigt förekomsten av Commerce Integration Framework.

