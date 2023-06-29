---
title: Versionsinformation om 2020.11.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.11.0."
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 är 2 december 2020.
Följande version (2020.12.0) kommer att vara den 17 december 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* **[Startar hierarkihantering](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [Framtida Timewarp](/help/sites-cloud/authoring/launches/preview.md)**: Nytt gränssnitt för att lägga till/ta bort sidor vid en start, och när du bläddrar på en webbplats med Timewarp visas det framtida tillståndet i Launches.

* **[Modeller och redigerare för utökat innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)**: Nya alternativ för indatavalidering för olika datatyper, förbättrad datatyp för uppräkning med nya formulärvisualiseringar och modellnamnet för innehållsfragment visas och är sökbart i resursgränssnittet.

* **Sortera de Live Copy-sidor som är tillgängliga för utrullning**: Nytt alternativ för att sortera de Live Copy-sidor som är tillgängliga för utrullning med [!UICONTROL Name], [!UICONTROL Last modified date]och [!UICONTROL Last rollout date] egenskaper. The [!UICONTROL Last rollout date] för en sida är en ny egenskap som introducerats.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Nyheter i [!DNL Assets] och [!DNL Dynamic Media] {#what-is-new-assets}

* **Massintag av resurser**: Förse kunderna med en skalbar, molnbaserad importfunktion som använder [!DNL Experience Manager] as a Cloud Service arkitektur inklusive tillgångsmikrotjänster. Exempel på viktiga användningsområden är inhämtning i stor skala med övervakning, rapportering och schemaläggning, samtidigt som resurser kan överföras till molndatalager med hjälp av vanliga verktyg för molnöverföring. Se [verktyg för massinhämtning](/help/assets/add-assets.md#asset-bulk-ingestor).

  Det här verktyget är avsett för systemadministratörer, konsulter eller implementeringspartners. Den här funktionen tillåter storskaligt intag och används helst vid första intag eller vid enstaka stora intag. Använd [[!DNL Experience Manager] datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) eller [överföra med Assets-användargränssnittet](/help/assets/add-assets.md#upload-assets).

  ![Konfiguration av bulkimporterare](/help/assets/assets/bulk-import-config-low-res.png)

* Användarna kan nu sortera de digitala resurserna i kort- och kolumnvyerna.

  ![sortera resurser](/help/assets/assets/asset-sort-options.png)

* Följande förbättringar har gjorts för tillgänglighet i [!DNL Experience Manager Assets] i den här versionen. Mer information finns i [tillgänglighetsfunktioner i [!DNL Assets]](/help/assets/accessibility.md).

   * När du navigerar på tidslinjen med ett tangentbord kan Esc-tangenten komprimera alternativet Visa alla utan att förlora fokus.
   * När du navigerar med tangentbordets tabbtangent behåller taggfältet fokus när du har tagit bort den sista taggen från de tillagda taggarna.
   * [!DNL Experience Manager] -komponenter innehåller nu lämplig information för namn, roll och värde som ska användas av skärmläsare.
   * När du har tagit bort kombinationsrutan Typ/storlek, kombinationsrutan Länk, Kombinationsrutan Språk eller textredigeringsrutan, återgår tangentbordsfokus till nästa eller föregående element i användargränssnittet eller till ett mer relevant element i användargränssnittet.
   * När du håller pekaren över alternativ visas tips som Markera och Hämta. Användare som använder en skärmförstorare kanske inte ser filminiatyrbilderna på grund av dessa tips. Nu går det att behålla fokus när du har tagit bort alternativet med `Escape` nyckel.
   * När du väljer en stödrastercell från det stödraster som finns på sidan flyttas fokus till det åtgärdsfält som visas på skärmen.
   * Visuella användare kan skilja mellan normal text och en länk, eftersom visuella ledtrådar (underline- och chevron-ikoner) visas för länkar till alla lösningar i [!DNL Experience Manager] hemsida.

* **Gruppuppsättningsförinställningar i Dynamic Media**: Nu kan du automatisera skapandet och organiseringen av flera resurser i en bilduppsättning eller snurra när du överför resursfiler till en mapp, antingen individuellt eller genom att använda massinläsning.

  Se [Om förinställningar för gruppuppsättning](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Följande tillgänglighetsförbättringar är nu tillgängliga i [!DNL Dynamic Media]:

   * Skärmläsare (JAWS, Skärmläsaren) lägger till en berättarröst för menyalternativens namn, roll och läge på menyn Bädda in storlek.
   * Användare kan navigera i dialogrutan E-postlänk med `Tab` nyckel.
   * Arbetsflödet för att skapa videokodningsprofiler är mer användarvänligt med tanke på skärmläsarförbättringarna.
   * Vid navigering med `Tab` flyttar fokus till lämpliga element i användargränssnittet i arbetsflödet för att skapa en interaktiv video.
   * Sidan Publicera, Redigera resurs, sidan Redigera smarta beskärningar och sidan Redigera bilduppsättning har förbättrats så att de uppfyller webbstandarderna. AT-användare kan nu enkelt navigera på dessa sidor och vidta åtgärder som beskärningsbilder.
   * Visningsprogrammen har förbättrats så att användarna kan navigera med tangentbordet.
   * Användare av tangentbord och skärmläsare kan använda beskärningsfunktionen.
   * Tangentbordsanvändarna kan hantera de aktiveringspunkter som behövs bättre.

  Se [Tillgänglighet i [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Vad är nytt? {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.11.05 som innehåller den senaste CIF Core Components version v1.5.0. Se [CIF Venias referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) för mer information.

* Frisläppta CIF-kärnkomponenter v1.5.0. Se [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) för mer information.

### Felkorrigeringar {#bug-fixes-commerce}

* GraphQL-klientkonfigurationen lästes inte in korrekt när konfigurationen inte anges direkt i Sling CA-konfigurationen, men i en av de överordnade konfigurationerna. Den här har åtgärdats.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2020.11.0 är 12 november 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Ett nytt menyalternativ **Lokal inloggning** är nu tillgängligt för användare via alternativen på miljömenyn på **Miljö** kort och **Miljö** sammanfattningssidor.
Se [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md#login-locally) för mer information.

* The **Lär dig** i Cloud Manager har uppdaterats med nya bilder i användargränssnittet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Inläsningen av beroenden som gjorts före körningen av bygget krävde hämtning av ett Maven-plugin-program.
* Länken från molnhanterarens sidfot för att välja ett språk navigerar nu till rätt plats.
* Ibland startar inte SonarQube-processen under kodskanningen. Detta identifieras nu automatiskt och ett omstartsförsök görs.
* Alla befintliga produktionspipelines aktiveras automatiskt med Experience Audit-steget.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Arbetsflöden {#workflows}

* Stöd lades till för sökning av arbetsflödesinstanser baserat på arbetsflödets titel, arbetsflödesmodell, status, initierare, nyttolastsökväg och startdatum. Se [Sök efter arbetsflödesinstanser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Synkronisering av användardata på publiceringsnivå {#user-sync}

* Användardata, inklusive profilattribut och gruppmedlemskap, kan sparas på publiceringsnivån. Läs mer om den här funktionen i [Dokumentation för registrering, inloggning och användarprofil](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK Build Analyzers {#analyzers}

Den AEM as a Cloud Service SDK Build Analyzer Maven Plugin identifierar problem i ett maven-projekt, inklusive saknade beroenden. Det ger utvecklare möjlighet att upptäcka problem under den lokala utvecklingen, långt före distributionen till molnmiljöer med Cloud Manager. Mer information finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) och [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Övriga {#others-foundation}

Nytt [&quot;httpd -t&quot; syntax](/help/implementing/dispatcher/disp-overview.md#local-validation) kontrollera om det finns cache- och dispatcherkonfigurationer som körs under Cloud Manager-bygget, som också kan köras med AEM as a Cloud Service SDK:s Dispatcher Tools.

## Content Transfer Tool {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Version v1.1.12.

### Vad är nytt? {#what-is-new-ctt}

* Användarupplevelsen för loggar har förbättrats. Tidsstämplar har lagts till i loggarna för extrahering och inmatning. Meddelande har lagts till för att ange om loggarna är tomma.

### Felkorrigeringar {#ctt-bug-fixes}

* Innehållsöverföringsverktyget hoppade över innehållsfiler om migreringsuppsättningen innehöll sökvägar som delvis hade liknande filnamn. Den här har åtgärdats.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer är 13 november 2020.

### Nyheter i [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Molnberedskapsanalys är nu BPA (Best Practices Analyzer). BPA ger en metodutvärdering av den aktuella AEM och hjälper dig att utvärdera om du är redo att gå över från en befintlig AEM till AEM as a Cloud Service.

* En ny detektor har lagts till för att upptäcka användningen av `java.io.InputStream`, vilket kan orsaka problem om det används i AEM as a Cloud Service.

### Felkorrigeringar {#bpa-bug-fixes}

* Fel som orsakar positiva effekter relaterade till *textfield Foundation* -komponenten har åtgärdats.
