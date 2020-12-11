---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
translation-type: tm+mt
source-git-commit: 3aff98256eb26176bca52a49286bf2853290b5ef
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2020.11.0 är 2 december 2020.
Följande version (2020.12.0) kommer att vara den 17 december 2020

## [!DNL Adobe Experience Manager Sites] som en Cloud Service  {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* **[Startar Hierarkihantering](/help/sites-cloud/authoring/launches/managing-pages.md)  och  [framtida tidsförvrängning](/help/sites-cloud/authoring/launches/preview.md)**: Nytt gränssnitt för att lägga till/ta bort sidor vid en start, och när du bläddrar på en webbplats med Timewarp visas det framtida tillståndet i Launches.

* **[Modeller och redigerare för utökat innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)**: Nya alternativ för indatavalidering för olika datatyper, förbättrad datatyp för uppräkning med nya formulärvisualiseringar och modellnamnet för innehållsfragment visas och är sökbart i resursgränssnittet.

* **Sortera de Live Copy-sidor som är tillgängliga för utrullning**: Nytt alternativ för att sortera de Live Copy-sidor som är tillgängliga för utrullning med hjälp av egenskaperna  [!UICONTROL Name],  [!UICONTROL Last modified date]och  [!UICONTROL Last rollout date] . [!UICONTROL Last rollout date] för en sida är en ny egenskap.

## [!DNL Adobe Experience Manager Assets] som en Cloud Service  {#assets}

### Nyheter i [!DNL Assets] och [!DNL Dynamic Media] {#what-is-new-assets}

* **Intag** av massresurser: Förse kunderna med en skalbar, molnbaserad tjänst för förtäring  [!DNL Experience Manager] som utnyttjar en Cloud Service-arkitektur, inklusive mikrotjänster för mediefiler. Exempel på viktiga användningsområden är inhämtning i stor skala med övervakning, rapportering och schemaläggning, samtidigt som resurser kan överföras till molndatalager med hjälp av vanliga verktyg för molnöverföring. Se [verktyg för massinhämtning av resurser](/help/assets/add-assets.md#asset-bulk-ingestor).
Det här verktyget är avsett för systemadministratörer, konsulter eller implementeringspartners. Den här funktionen tillåter storskaligt intag och används helst vid första intag eller vid enstaka stora intag. Använd [[!DNL Experience Manager] datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) eller [överföringen med Assets-användargränssnittet](/help/assets/add-assets.md#upload-assets) för mindre användningsjobb.

   ![Konfiguration av bulkimporterare](/help/assets/assets/bulk-import-config-low-res.png)

* Användarna kan nu sortera de digitala resurserna i kort- och kolumnvyerna.

   ![sortera resurser](/help/assets/assets/asset-sort-options.png)

* Följande förbättringar har gjorts för tillgänglighet i [!DNL Experience Manager Assets] i den här versionen. Mer information finns i [tillgänglighetsfunktioner i [!DNL Assets]](/help/assets/accessibility.md).

   * När du navigerar på tidslinjen med ett tangentbord kan Esc-tangenten komprimera alternativet Visa alla utan att förlora fokus.
   * När du navigerar med tangentbordets tabbtangent behåller taggfältet fokus när du har tagit bort den sista taggen från de tillagda taggarna.
   * [!DNL Experience Manager] -komponenter innehåller nu lämplig information för namn, roll och värde som ska användas av skärmläsare.
   * När du har tagit bort kombinationsrutan Typ/storlek, kombinationsrutan Länk, Kombinationsrutan Språk eller textredigeringsrutan, återgår tangentbordsfokus till nästa eller föregående element i användargränssnittet eller till ett mer relevant element i användargränssnittet.
   * När du håller pekaren över alternativ visas tips som Markera och Hämta. Användare som använder en skärmförstorare kanske inte ser filminiatyrbilderna på grund av dessa tips. Nu är det möjligt att behålla fokus när du har tagit bort alternativet med `Escape`-tangenten.
   * När du väljer en stödrastercell från det stödraster som finns på sidan flyttas fokus till det åtgärdsfält som visas på skärmen.
   * Visuella användare kan skilja mellan normal text och en länk, eftersom visuella ledtrådar (underline- och chevron-ikoner) visas för länkar till alla lösningar på startsidan för [!DNL Experience Manager].

* **Förinställningar för gruppuppsättning i Dynamic Media**: Nu kan du automatisera skapandet och organiseringen av flera resurser i en bilduppsättning eller snurra när du överför resursfiler till en mapp, antingen individuellt eller genom att använda massinläsning.

   Se [Om förinställningar för gruppuppsättning](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Följande tillgänglighetsförbättringar är nu tillgängliga i [!DNL Dynamic Media]:

   * Skärmläsare (JAWS, Skärmläsaren) lägger till en berättarröst för menyalternativens namn, roll och läge på menyn Bädda in storlek.
   * Användare kan navigera i dialogrutan E-postlänk med `Tab`-tangenten.
   * Arbetsflödet för att skapa videokodningsprofiler är mer användarvänligt med tanke på skärmläsarförbättringarna.
   * När du navigerar med `Tab`-tangenten flyttas fokus till lämpliga element i användargränssnittet i arbetsflödet för att skapa en interaktiv video.
   * Sidan Publicera, Redigera resurs, sidan Redigera smarta beskärningar och sidan Redigera bilduppsättning har förbättrats så att de uppfyller webbstandarderna. AT-användare kan nu enkelt navigera på dessa sidor och vidta åtgärder som beskärningsbilder.
   * Visningsprogrammen har förbättrats så att användarna kan navigera med tangentbordet.
   * Användare av tangentbord och skärmläsare kan använda beskärningsfunktionen.
   * Tangentbordsanvändarna kan hantera de aktiveringspunkter som behövs bättre.

   Se [Tillgänglighet i [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce som Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.11.05 som innehåller den senaste CIF Core Components version v1.5.0. Mer information finns i [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27).

* Frisläppta CIF-kärnkomponenter v1.5.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0).

### Felkorrigeringar {#bug-fixes-commerce}

* GraphQL-klientkonfigurationen lästes inte korrekt när konfigurationen inte anges direkt i Sling CA-konfigurationen, men i en av de överordnade konfigurationerna. Den här har åtgärdats.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.12.0 är 10 december 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Självbetjäningshantering för [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) och [anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Självbetjäningshantering för [IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* **Informationssidan för miljö** tillåter nu användare att hantera anpassade domännamn och IP-Tillåtelselista i sina miljöer.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Vissa förekomster av fel vid kodskanning utan att ge några resultat åtgärdade.

* Miljökortet visade inte **Lägg till**-knapp genomgående.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Arbetsflöden {#workflows}

* Stöd lades till för sökning av arbetsflödesinstanser baserat på arbetsflödets titel, arbetsflödesmodell, status, initierare, nyttolastsökväg och startdatum. Se [Förekomster av arbetsflöden för sökning](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Synkronisering av användardata på publiceringsnivå {#user-sync}

* Användardata, inklusive profilattribut och gruppmedlemskap, kan sparas på publiceringsnivån. Läs mer om den här funktionen i [dokumentationen för registrering, inloggning och användarprofil](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK Build Analyzers {#analyzers}

AEM som Cloud Service SDK Build Analyzer Maven Plugin identifierar problem i ett maven-projekt, inklusive saknade beroenden. Det ger utvecklare möjlighet att upptäcka problem under den lokala utvecklingen, långt före distributionen till molnmiljöer med Cloud Manager. Mer information finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) och [här](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Övriga {#others-foundation}

Ny [&quot;httpd -t&quot;-syntax](/help/implementing/dispatcher/disp-overview.md#local-validation)-kontroll för att se om det finns en cache- och dispatcherkonfiguration som körs under Cloud Manager-bygget, som också kan köras med AEM som en Cloud Services-SDK:s Dispatcher-verktyg.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller felkorrigeringar för AEM Dispatcher Converter och Repository Modernizer och har även stöd för ett nytt verktyg - Index Converter. Läs [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) om du vill veta mer om det här plugin-programmet.

* Indexkonverteraren är ett verktyg som kan användas för att omvandla en kunds anpassade OAK-indexdefinitioner till AEM som en Cloud Service-kompatibel OAK-indexdefinitioner.
Mer information finns i [Indexkonverteraren](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Ny funktion har lagts till i [Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) som skapar ett separat paket `ui.config` som innehåller alla OSGi-konfigurationer.

### Felkorrigeringar {#crt-bug-fixes}

* Flera felkorrigeringar har gjorts i verktygen AEM Dispatcher Converter och Repository Modernizer.
Se [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) och [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).