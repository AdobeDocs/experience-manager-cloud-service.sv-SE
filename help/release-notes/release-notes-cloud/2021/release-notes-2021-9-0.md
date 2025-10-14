---
title: Versionsinformation för version 2021.9.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.9.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020 och 2021.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2021.9.0) är 6 oktober 2021.
Följande version (2021.10.0) är den 4 november 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt för september 2021](https://video.tv.adobe.com/v/337381) om du vill se en sammanfattning av de nya funktionerna.

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Ny funktion i betaversionskanalen [!DNL Sites] {#sites-prerelease-features}

* Modeller för innehållsfragment anges nu automatiskt i ett skrivskyddat läge när de har publicerats, så att du inte oavsiktligt kan bryta aktiva API-frågor efter att ha publicerat om en redigerad modell. Användarna får en varning när de försöker redigera en publicerad modell. Du kan redigera när du har godkänt varningen.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Användarna kan nu sortera de resurser som visas i sökresultaten i kolumn- och kortvyn. Sorteringen fungerar på kolumnerna Namn, Skapad, Ändrad eller Ingen.

  ![Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyer &#x200B;](/help/assets/assets/sort-searched-assets.png)
  *Figur: Sortera sökresultaten i [!DNL Assets] i kolumn- och kortvyer.*

* Ett nytt API introduceras för programmässig bearbetning med hjälp av objektmikrotjänster. Utvecklare kan nu använda en befintlig bearbetningsprofil på mappnivå på en eller flera specifika resurser i en mapp. Bearbetningsprofilen tillämpas baserat på uppdateringar av anpassade metadataegenskaper. Se `AssetProcessor` i [[!DNL Experience Manager] API-referensen](https://developer.adobe.com/experience-manager/reference-materials/). Som tidigare är det möjligt att [använda resursmikrotjänster från användargränssnittet](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature by way of CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Använd Adobe Sign-roller i ett adaptivt formulär** - Med Adobe Sign för företags- och företagsnivåer kan du utöka rollerna för avtalsmottagare, utöver bara signeraren, för att bättre matcha deras arbetsflödesbehov. Du kan nu [aktivera varje mottagare av avtalet att konfigurera sin roll i ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html?lang=sv-SE#addsignerstoanadaptiveform) med signerare som standardroll.

* **Analytics for Adaptive Forms** - Nu kan du hämta in och spåra slutanvändarbeteende med Adobe Analytics for Adaptive Forms för att samla in slutanvändarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra slutanvändarens upplevelse.

* **Anslut enkelt Adobe Experience Manager (AEM) Forms till Microsoft® Dynamics och Salesforce** - Tjänsten tillhandahåller färdig datakällkonfiguration och datamodeller för Microsoft® Dynamics och Salesforce. Detta gör det [snabbare och enklare för utvecklare att konfigurera Microsoft® Dynamics och Salesforce som datakällor för ett adaptivt formulär](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=sv-SE).

* **E-signera ett anpassat formulär med DocuSign** - Du kan använda DocuSign för att e-signera ett anpassat formulär. Tjänsten tillhandahåller en anpassad skickaåtgärd för att använda DocuSign med ett adaptivt formulär. Du kan installera det paket som är tillgängligt på Programvarudistribution för att importera sändningsåtgärden.

### Beta-funktioner i [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Enhetlig lagringsanslutning** - Använd Unified Storage Connector för att externalisera processdata i kundhanterade databaser. Du kan till exempel
   * Möjliggör Forms Portals funktioner för att spara och återuppta samt lagra adaptiva blankettutkast i ett kundhanterat datalager.
   * Lagra AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga personuppgifter (SPD) i en kundhanterad databas.

* **[!DNL AEM Forms as a Cloud Service - Communications]** - [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html?lang=sv-SE) hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera PDF-filer från ett XFA-formulär i PDF och Adobe Acrobat-formulär.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Den nya fliken&quot;Associerat e-handelsinnehåll&quot; i AEM Sites Editor ökar redigerarens effektivitet genom att snabbt få tillgång till relevant AEM produktinnehåll för det aktuella sammanhanget

  ![Associerat e-handelsinnehåll](/help/assets/CIF/associated-commerce-content.png)

* Förbättrat användargränssnitt för produktväljare för bättre användarupplevelse, ökad effektivitet och stöd för komplexa produktkataloger

  ![Ny produktväljare](/help/assets/CIF/product-picker.png)

* Respektera egenskapen include_in_menu i navigeringskomponenten

### Felkorrigeringar {#bug-fixes-cif}

* Borttagning av menycache fungerar inte som förväntat

* JS-fel under AEM CS-driftsättningssteget och när komponenter på klientsidan inte används

* Det går inte att skapa CIF molnkonfiguration i mappar som har en sling:configs-nod

## [!DNL Experience Manager Screens] som en [!DNL Cloud Service] {#screens}

### Nyheter {#what-is-new-screens}

* Screens as a Cloud Service har nu stöd för grundläggande uppspelningsövervakning. Spelaren rapporterar nu olika uppspelningsmått för varje ping (standardvärdet är 30 sekunder). Baserat på mätvärden kan programmet identifiera olika kantfall (fastnålade upplevelser, tom skärm, schemaläggningsproblem osv.). Med den här funktionen kan teamet fjärrövervaka om en spelare spelar upp innehåll på rätt sätt. Det förbättrar reaktiviteten till tomma skärmar eller trasiga upplevelser på fältet och minskar risken för att användaren får en trasig upplevelse.
Mer information finns i [Grundläggande uppspelningsövervakning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=sv-SE#playback-monitoring).

* Miniatyrbildsstöd för videor i stöds nu i Screens as a Cloud Service. Innehållsförfattaren kan definiera en miniatyrbild för videoklipp så att bilden används som platshållare och testar uppspelning och målgruppsanpassning av innehållet medan videon färdigställs av rätt team. Bilden kan också användas om videouppspelningen misslyckas.
Mer information finns i [Stöd för miniatyrbilder för videoklipp](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html?lang=sv-SE).

### Felkorrigeringar {#bug-fixes-screens}

* Spelaren kunde inte visa innehåll från den inbäddade sidan och problemet är nu åtgärdat.

* När inloggningen lyckades hamnade navigeringen till standardsidan (kanalerna) i en intern serverfelsida.

* Associerade taggposter togs inte bort när spellistor togs bort.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nya funktioner i [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Avancerade nätverk**

>[!INFO]
>
>Den avancerade nätverksfunktionen ingår i version 2021.9.0 och aktiverades för kunder i mitten av oktober 2021.

[!DNL Adobe Experience Manager] som [!DNL Cloud Service] erbjuder nu flera typer av avancerade nätverksfunktioner, bland annat:

* Flexibel portutgång för att utlösa trafik från icke-standardiserade portar. Nu möjligt utan att kontakta Adobe Support.
* Dedikerad IP-adress för utgångar för att ta ut trafik från AEM as a Cloud Service från en unik IP-adress, som nu stöder alla portar.
* VPN för att säkra trafiken mellan din infrastruktur och AEM as a Cloud Service.

Läs [dokumentationen](/help/security/configuring-advanced-networking.md) om du vill ha mer information, bland annat om hur du självbetjänar avancerade nätverk med Cloud Manager API:er.

**Indexoptimeringar**

För att förbättra prestanda för sökfrågor och indexering används heltextindexet lucene-2 inte längre som [!DNL Cloud Service] i [!DNL Adobe Experience Manager] från den här versionen. För att ta bort detta fulltextindex i AEM miljöer i enlighet med AEM kunder arbetar Adobe Engineering individuellt och aktivt med kunderna för att få ett mjukt och hållbart borttagande av Lucene-fulltextindexet. Gå till [!DNL Adobe Experience Manager] som [!DNL Cloud Service] [dokumentation](/help/operations/indexing.md#index-optimizations) om du vill ha mer information och kontakta Adobe support direkt om du har frågor.

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.9.0 och 2021.8.0.

## Releasedatum {#release-date-cm-sept}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.9.0 är 9 september 2021.
Nästa version är planerad till 7 oktober 2021.

### Nyheter {#what-is-new-cm-sept}

* Den version av AEM Project Archettype som används av Cloud Manager har uppdaterats till version 30.

* Programkorten på Cloud Manager landningssida och tillhörande upplevelser har uppdaterats.

* Kodkvalitetsstegloggen innehåller nu utförlig loggningsinformation om OakPal-skanningen.

* Menyalternativen på sidan Aktivitet innehåller nu ett alternativ för att **hämta logg** för slutförda kodgeneratorkörningar. Om du väljer det här alternativet hämtas loggen för byggsteget.

* Om du klickar direkt på programkortet går du nu till sidan Cloud Manager Overview.

### Felkorrigeringar {#bug-fixes-sept}

* Användarna ser nu ett mer begripligt meddelande när de försöker lägga till ett IP-tillåtelselista i ett program som har nått det högsta tillåtna antalet IP-tillåtelselista som kan konfigureras.

* Fel URL kopierades när menyalternativet Kopiera URL valdes på skärmen Databaser.

## Cloud Acceleration Manager {#cam}

### Releasedatum {#release-date-october-cam}

Releasedatum för Cloud Acceleration Manager är 4 oktober 2021.

### Nyheter {#what-is-new-cam}

* Cloud Acceleration Manager ger nu användare möjlighet att visa BPA-rapporterna i en förhandsgranskning som går att skriva ut, vilket gör det enkelt att skriva ut eller skriva ut till PDF för att det ska vara enkelt att dela dem. Se steg 6 och 7 i [Använda analysverktyget för bästa praxis](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=sv-SE#best-practices-analysis).

## Verktyget Innehållsöverföring {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för innehållsöverföringsverktyget v1.6.0 är 4 oktober 2021.

### Nyheter {#what-is-new-ctt}

* Förbättrad användarmappning med en förenklad användarupplevelse, inklusive följande funktioner som listas nedan. Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=sv-SE#using-user-mapping-tool).
   * Testa anslutningen till API:t för användarhantering innan du kör användarmappningen
   * Hoppa över fel utan problem och fortsätt med aktiviteten Användarmappning
   * Användarmappning misslyckas inte längre om åtkomsttoken upphör att gälla (efter 24 timmar). Användarmappning kan köras igen från den plats där den senast stoppades.

* Om du vill öka CTT-tillförlitligheten kan innehåll importeras till antingen Author-instansen eller Publish-instansen åt gången.

* När versioner inkluderas inkluderas sökvägen `/var/audit` automatiskt för att migrera granskningshändelser.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa-latest}

Releasedatum för Best Practices Analyzer v2.1.18 är 2 september 2021.

### Nyheter {#what-is-new}

* Möjlighet att identifiera och rapportera det totala antalet noder.

* Möjlighet att identifiera och rapportera om nodlagringstyp och -storlek.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA upptäckte felaktigt förekomsten av Commerce integration framework.
