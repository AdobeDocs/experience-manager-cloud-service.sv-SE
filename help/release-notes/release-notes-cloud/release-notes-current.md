---
title: Aktuell versionsinformation [!DNL Adobe Experience Manager] för en Cloud Service.
description: Aktuell versionsinformation [!DNL Adobe Experience Manager] för en Cloud Service.
translation-type: tm+mt
source-git-commit: d8cb22a5597e95bf4c74233b48553bb67bca09cb
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] Cloud Service 2020.10.0 är 28 oktober 2020.
Följande version (2020.11.0) kommer att vara den 1 december 2020.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **Project Archetype 24**: Den rekommenderade grunden för att starta ett nytt AEM-projekt har blivit bättre, nu med nya Adobe Client Data Layer, alternativ för att leverera webbplatsen i AMP och nya tilläggspunkter för att lägga till projekt-CSS/JS.

* **ContextHub-mappar**: Möjlighet att skapa målgruppsmappar för att enkelt ordna, hitta och välja målgruppssegment som kan användas för målinriktningsfunktioner i ContextHub.

## [!DNL Adobe Experience Manager Assets] som en Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]smart taggning**: Genom att utnyttja AI-modeller för att analysera videoinnehåll för objekt- och åtgärdsspecifika taggar kan DAM-användare lägga mindre tid på att lägga till taggar och mer tid på att utnyttja den omfattande information som exponeras för att leverera rätt upplevelse till kunderna. Se [Videor med smarta taggar](/help/assets/smart-tags-video-assets.md).

* **Förbättringar** i varumärkesportalen: Följande nya funktioner och mer finns i [!DNL Brand Portal]. Mer information finns i [[!DNL Brand Portal] versionsinformation](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Förbättrad nedladdning](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) för enklare, snabba nedladdningar. Ytterligare hämtningskonfigurationer kan konfigureras av administratörer för att ge en upplevelse som passar användare och företag.
   * Nu kan du navigera till filer, [samlingar](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)och delade länkar med ett enda klick från vilken sida som helst.
   * Användarna kan [välja och hämta specifika renderingar](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) nu. Det nya hämtningsalternativet för återgivning finns på panelen Återgivningar på sidan Resursinformation.
   * En tidsgräns på 15 minuter för gästanvändarsessioner ger en bättre upplevelse för alla samtidiga användare.

* **[!DNL Adobe Asset Link]version 2.1**: En ny version av [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) -tillägget för [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]och [!DNL Adobe InDesign] är tillgänglig. Det lägger till kompatibilitet med de senaste [!DNL Adobe Creative Cloud] programmen med version 2021, som släpptes i oktober 2020.

* **[!DNL Assets]Stöd** för WebP-filer: [!DNL Assets] som en Cloud Service har nu stöd för WebP-bildformat. WebP är ett framväxande bildformat som skapats av Google. Bilder i WebP-filformat kan inte skiljas åt visuellt från JPG- eller PNG-filer och filerna är mycket mindre. Lägre filstorlek förbättrar sidinläsningen och hjälper innehållsskaparna att leverera en snabbare webbupplevelse. Se [Skapa en standardbearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Vad är nytt? {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.10.2 som innehåller den senaste CIF Core Components version v1.4.0. Mer information finns på [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) .

* Frisläppta CIF-kärnkomponenter v1.4.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) .

### Bug Fixes {#bug-fixes-commerce}

* GraphQL-begäranden i produktkonsolen och väljare gjordes via HTTP-POST. Detta har åtgärdats för att säkerställa att Apollo GraphQL-klienten respekterar inställningen i GraphQL-klientens OSGi-konfiguration för att stödja GET-begäranden om detta har konfigurerats.

* CIF Cloud-konfigurationsgränssnittet visade knapparna Spara och stäng för konfigurationer i /lib och /apps/. Dessa är skrivskyddade och därför har användargränssnittet fast att bara visa stängningsknappen.


## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.11.0 är 12 november 2020.

### Nyheter {#what-is-new}

* Ett nytt menyalternativ, **Lokal inloggning** , är nu tillgängligt för användare från miljömenyalternativen på miljökortets och miljösammanfattningens sidor.

* Fliken **Lär dig** i Cloud Manager har uppdaterats med nya bilder i användargränssnittet.

### Bug Fixes {#bug-fixes-cloud-manager}

* Inläsningen av beroenden som gjorts före körningen av bygget krävde hämtning av ett Maven-plugin-program.
* Länken från molnhanterarens sidfot för att välja ett språk navigerar nu till rätt plats.
* Ibland startar inte SonarQube-processen under kodskanningen. Detta identifieras nu automatiskt och ett omstartsförsök görs.
* Alla befintliga produktionspipelinjer aktiveras automatiskt med Experience Audit-steget.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Arbetsflöden {#workflows}

* Stöd lades till för sökning av arbetsflödesinstanser baserat på arbetsflödets titel, arbetsflödesmodell, status, initierare, nyttolastsökväg och startdatum. Se [Sök efter arbetsflödesinstanser](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Content Transfer Tool {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Vad är nytt? {#what-is-new-ctt}

* Användarupplevelsen för loggar har förbättrats. Tidsstämplar har lagts till i loggarna för extrahering och inmatning. Meddelande har lagts till för att ange om loggarna är tomma.

### Bug Fixes {#ctt-bug-fixes}

* Innehållsöverföringsverktyget hoppade över innehållsfiler om migreringsuppsättningen innehöll sökvägar som delvis hade liknande filnamn. Den här har åtgärdats.
