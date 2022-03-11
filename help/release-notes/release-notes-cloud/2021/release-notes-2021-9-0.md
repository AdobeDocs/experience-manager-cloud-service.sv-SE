---
title: Versionsinformation för 2021.9.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för 2021.9.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1572'
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

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2021.9.0) är 6 oktober 2021.
Följande version (2021.10.0) är den 4 november 2021.

## Släpp video {#release-video}

Ta en titt på [Versionsöversikt september 2021](https://video.tv.adobe.com/v/337381) video med en sammanfattning av tillagda funktioner.

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Ny funktion i [!DNL Sites] prerelease channel {#sites-prerelease-features}

* Modeller för innehållsfragment anges nu automatiskt i skrivskyddat läge när de har publicerats, för att undvika att direktsända API-frågor bryts efter att en redigerad modell har publicerats om. Användarna får en varning när de försöker redigera en publicerad modell. Du kan redigera när du har godkänt varningen.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Användarna kan nu sortera de resurser som visas i sökresultaten i kolumn- och kortvyn. Sorteringen fungerar på kolumnerna Namn, Skapad, Ändrad eller Ingen.

   ![Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyer](/help/assets/assets/sort-searched-assets.png)
   *Bild: Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyn.*

* Ett nytt API introduceras för programmässig bearbetning med hjälp av objektmikrotjänster. Utvecklare kan nu använda en befintlig bearbetningsprofil på mappnivå på en eller flera specifika resurser i en mapp. Bearbetningsprofilen tillämpas baserat på uppdateringar av anpassade metadataegenskaper. Se `AssetProcessor` i [[!DNL Experience Manager] API-referens](https://www.adobe.io/experience-manager/reference-materials/). Som tidigare är det möjligt att [använda resursmikrotjänster från användargränssnittet](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Använda Adobe Sign-roller i ett adaptivt formulär**: Adobe Sign för företags- och företagsnivåer har möjlighet att utöka rollerna för avtalsmottagare, utöver bara signeraren, så att de bättre motsvarar deras arbetsflödesbehov. Nu kan du [göra det möjligt för alla mottagare av avtal att konfigurera sin roll i ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), med signerare som standardroll.

* **Analytics för Adaptive Forms**: Nu kan du samla in och spåra användarbeteende via Adobe Analytics för Adaptive Forms för att få information om slutanvändarna. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

* **Koppla enkelt upp AEM Forms med Microsoft Dynamics och Salesforce**: Tjänsten tillhandahåller direkt konfiguration av datakälla och datamodeller för Microsoft Dynamics och Salesforce, vilket gör den [snabbare och enklare för utvecklare att konfigurera Microsoft Dynamics och Salesforce som datakällor för ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **E-signera ett anpassat formulär med DocuSign:** Du kan använda DocuSign för att e-signera ett anpassat formulär. Tjänsten tillhandahåller en anpassad skickaåtgärd för att använda DocuSign med ett adaptivt formulär. Du kan installera det paket som är tillgängligt på Programvarudistribution för att importera sändningsåtgärden.

### Betafunktioner i [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Enhetlig lagringsanslutning:** Använd Unified Storage Connector för att externalisera processdata i kundhanterade databaser. Du kan till exempel
   * Möjliggör Forms Portals funktioner för att spara och återuppta samt lagra adaptiva formulärutkast i ett kundhanterat datalager.
   * Lagra AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga personuppgifter (SPD) i en kundhanterad databas.

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera PDF-filer från ett XFA-formulär PDF och Adobe Acrobat-formulär.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att anmäla dig till betaprogrammet.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Ny flik för associerat e-handelsinnehåll i Sites editor ökar redigeringens effektivitet genom att snabbt få tillgång till relevant AEM för det aktuella sammanhanget

   ![Associerat e-handelsinnehåll](/help/assets/CIF/associated-commerce-content.png)

* Förbättrat användargränssnitt för produktväljare för bättre användarupplevelse, ökad effektivitet och stöd för komplexa produktkataloger

   ![Ny produktväljare](/help/assets/CIF/product-picker.png)

* Respektera egenskapen include_in_menu i navigeringskomponenten

### Felkorrigeringar {#bug-fixes-cif}

* Borttagning av menycache fungerar inte som förväntat

* JS-fel under AEM CS-driftsättningssteg och när komponenter på klientsidan inte används

* Det går inte att skapa CIF-molnkonfigurationen i mappar som har en sling:configs-nod

## [!DNL Experience Manager Screens] som [!DNL Cloud Service] {#screens}

### Vad är nytt? {#what-is-new-screens}

* as a Cloud Service skärmar har nu stöd för grundläggande uppspelningsövervakning. Spelaren rapporterar nu olika uppspelningsmått för varje ping (standardvärdet är 30 sekunder). Baserat på mätvärden ger det möjlighet att upptäcka olika kantfall (fastnålade upplevelser, tom skärm, schemaläggningsproblem osv.). Med den här funktionen kan teamet fjärrövervaka om en spelare spelar upp innehåll, förbättrar reaktiviteten till tomma skärmar eller trasiga upplevelser i fältet och minskar risken för att slutanvändaren får en trasig upplevelse.
Se [Grundläggande uppspelningsövervakning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) för mer information.

* Miniatyrbildsstöd för videor i stöds nu i as a Cloud Service skärmar. Innehållsförfattare kan definiera en miniatyrbild för videoklipp så att bilden kan användas som platshållare och testa uppspelning och målgruppsanpassning av innehållet medan videon färdigställs av rätt team. Bilden kan också användas om videouppspelningen misslyckas.
Se [Stöd för miniatyrbilder för videoklipp](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) för mer information.

### Felkorrigeringar {#bug-fixes-screens}

* Spelaren kunde inte visa innehåll från den inbäddade sidan och problemet är nu åtgärdat.

* Efter en lyckad inloggning hamnade navigeringen till standardsidan (kanalerna) i en intern serverfelsida.

* Associerade taggposter togs inte bort när spellistor togs bort.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nya funktioner i [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Avancerat nätverksbyggande**

>[!INFO]
>
>Den avancerade nätverksfunktionen ingår i version 2021.9.0 och kommer att aktiveras för kunder i mitten av oktober.

[!DNL Adobe Experience Manager] som [!DNL Cloud Service] erbjuder nu flera typer av avancerade nätverksfunktioner, bland annat:

* Flexibel portutgång för att utlösa trafik från icke-standardiserade portar. Nu möjligt utan att kontakta Adobe Support.
* Dedikerad IP-adress för utgångar för att ta ut trafik från AEM as a Cloud Service från en unik IP-adress, som nu stöder alla portar.
* VPN för att säkra trafiken mellan din infrastruktur och AEM as a Cloud Service.

Läs [dokumentation](/help/security/configuring-advanced-networking.md) för mer information, inklusive hur du självbetjänar avancerad nätverkstjänst med hjälp av API:er för Cloud Manager.

**Indexoptimeringar**

För att förbättra prestanda för sökfrågor och indexering används heltextindexet lucene-2 inte längre i [!DNL Adobe Experience Manager] som [!DNL Cloud Service] från den här versionen. För att ta bort detta fulltextindex i AEM miljöer i enlighet med AEM kunder arbetar Adobe Engineering individuellt och aktivt med kunderna för att få ett mjukt och hållbart borttagande av Lucene-fulltextindexet. Besök [!DNL Adobe Experience Manager] som [!DNL Cloud Service] [dokumentation](/help/operations/indexing.md#index-optimizations) för mer information och kontakta vår support direkt om du har några frågor.

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.9.0 och 2021.8.0.

## Releasedatum {#release-date-cm-sept}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.9.0 är 9 september 2021.
Nästa version är planerad till 7 oktober 2021.

### Nyheter {#what-is-new-cm-sept}

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 30.

* Programkorten på Cloud Managers landningssida och den tillhörande upplevelsen har uppdaterats.

* Kodkvalitetsstegloggen innehåller nu utförlig loggningsinformation om OakPal-skanningen.

* Menyalternativen på sidan Aktivitet kommer nu att innehålla ett alternativ för att **Hämtningslogg** för slutförda kodgeneratorkörningar. Om du väljer det här alternativet hämtas loggen för byggsteget.

* Om du klickar direkt på programkortet går du nu till sidan Översikt över Cloud Manager.

### Felkorrigeringar {#bug-fixes-sept}

* Användaren kommer nu att se ett mer begripligt meddelande när han/hon försöker lägga till ett nytt IP-Tillåtelselista i ett program som har nått det högsta tillåtna antalet IP-Tillåtelselista som kan konfigureras.

* Fel URL kopierades när menyalternativet Kopiera URL valdes på skärmen Databaser.

## Cloud Acceleration Manager {#cam}

### Releasedatum {#release-date-october-cam}

Releasedatum för Cloud Acceleration Manager är 4 oktober 2021.

### Vad är nytt? {#what-is-new-cam}

* Med Cloud Acceleration Manager kan användarna nu visa BPA-rapporter i en förhandsgranskning som kan skrivas ut, vilket gör det enkelt att skriva ut eller skriva ut till PDF för att det ska vara enkelt att dela. Se steg 6 och 7 i [Använda analyskort för metodtips](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Content Transfer Tool {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för innehållsöverföringsverktyget v1.6.0 är 4 oktober 2021.

### Nyheter {#what-is-new-ctt}

* Förbättrad användarmappning med en förenklad användarupplevelse, inklusive följande funktioner som listas nedan. Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * Testa anslutningen till API:t för användarhantering innan du kör användarmappningen
   * Hoppa över fel utan problem och fortsätt med aktiviteten Användarmappning
   * Användarmappning misslyckas inte längre om åtkomsttoken upphör att gälla (efter 24 timmar). Användarmappning kan köras igen från den plats där den senast stoppades.

* Om du vill öka CTT-tillförlitligheten kan innehåll hämtas till antingen Author-instansen eller Publish-instansen åt gången.

* När versioner inkluderas, banan `/var/audit` inkluderas automatiskt för att migrera granskningshändelser.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa-latest}

Releasedatum för Best Practices Analyzer v2.1.18 är 2 september 2021.

### Nyheter {#what-is-new}

* Möjlighet att identifiera och rapportera totalt antal noder.

* Möjlighet att identifiera och rapportera om nodlagringstyp och -storlek.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA upptäckte felaktigt förekomsten av Commerce Integration Framework.
