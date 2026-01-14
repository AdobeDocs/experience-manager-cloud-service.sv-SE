---
title: Versionsinformation för version 2020.10.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] Versionsinformation om as a Cloud Service för 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 är 28 oktober 2020.
Följande version (2020.11.0) kommer att vara den 1 december 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* **[Core Components 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=sv-SE)**: Adobe Experience Manager as a Cloud Service drar nytta av automatiska uppdateringar av den senaste versionen av Core Components. Version 2.12.0 innehåller de senaste förbättringarna från communityn. Bland förbättringarna finns [en ny POST-formulärhanterare;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html?lang=sv-SE#post-data) möjlighet att inkludera anpassade CSS-, JavaScript- och metadata [-taggar via kontextmedveten konfiguration;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html?lang=sv-SE#context-aware-loading) och ett [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html?lang=sv-SE#enabling-custom-components)-verktyg för att förenkla integreringen av Adobe datalager i anpassade komponenter. Se [listan över ändringar](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) i 2.12.0.

* **[Project Archetype 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE)**: Den rekommenderade grunden för att starta ett nytt Experience Manager-projekt har förbättrats. Nu ingår det nya [Adobe-klientdatalagret](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=sv-SE), alternativet att [leverera webbplatsen i AMP](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=sv-SE) och nya [tilläggspunkter för att lägga till projekt-CSS/JS](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html?lang=sv-SE#context-aware-loading).

* **[ContextHub-mappar](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Möjlighet att skapa målgruppsmappar för att enkelt ordna, hitta och välja målgruppssegment som ska användas för målinriktningsfunktioner för ContextHub-erbjudanden.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe AI]strömlinjeformad smart taggning av video**: Genom att använda AI-modeller för att analysera videoinnehåll för objekt- och åtgärdsspecifika taggar kan DAM-användare lägga mindre tid på att lägga till taggar och mer tid på att använda den exponerade, omfattande informationen. Ni levererar i sin tur rätt upplevelse till kunderna. Se [Videoresurser för smarta taggar](/help/assets/smart-tags-for-videos.md).

* **Brand Portal-förbättringar**: Följande nya funktioner och mer finns i [!DNL Brand Portal]. Mer information finns i [[!DNL Brand Portal] versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html?lang=sv-SE).

   * [Förbättrad nedladdningsupplevelse](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=sv-SE) för enklare, snabba nedladdningar. Ytterligare hämtningskonfigurationer kan konfigureras av administratörer för att ge en upplevelse som passar användare och företag.
   * Du kan nu navigera till filer, [samlingar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html?lang=sv-SE) och delade länkar med ett enda klick från vilken sida som helst.
   * Användare kan [välja och hämta specifika återgivningar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=sv-SE#download-assets-from-asset-details-page) nu. Det nya hämtningsalternativet för återgivning finns på panelen Återgivningar på sidan Resursinformation.
   * En tidsgräns på 15 minuter för gästanvändarsessioner ger en bättre upplevelse för alla samtidiga användare.

* **[!DNL Adobe Asset Link]version 2.1**: En ny version av [Adobe Asset Link](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html)-tillägget för [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] och [!DNL Adobe InDesign] är tillgänglig. Den lägger till kompatibilitet med de senaste [!DNL Adobe Creative Cloud]-programmen med version 2021, som släpptes i oktober 2020.

* **[!DNL Assets]Stöd för WebP-filer**: [!DNL Assets] as a Cloud Service har nu stöd för WebP-bildformat. WebP är ett framväxande bildformat som skapas av Google. Bilder i WebP-filformat kan inte särskiljas visuellt från JPG- eller PNG-filer och filerna är mycket mindre. Lägre filstorlek förbättrar sidinläsningen och hjälper innehållsskaparna att leverera en snabbare webbupplevelse. Se hur du använder WebP i [skapa bearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### Nyheter i [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**: Nu kan du samla in och spåra beteenden för både inloggad och ej inloggad (anonym) med Adobe Analytics for Adaptive Forms för att samla in användarinsikter. Det hjälper företagsanvändare att fatta välgrundade beslut om anpassat formulärinnehåll, layout och format baserat på insamlade insikter.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Gör AEM Workflow-data externt för säker bearbetning**: Du kan lagra processdata för AEM Workflow-variabler som innehåller känsliga SPD-element (Personal Data) i en kundhanterad databas för säker bearbetning. När arbetsflödet bearbetas sparas inte data som lagras i arbetsflödesvariabler i AEM-databasen. Den hämtas på begäran från den kundhanterade databasen.

### Beta-funktioner i [!DNL Forms]  {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) hjälper dig att kombinera en mall och XML-data för att generera dokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.10.2 som innehåller den senaste versionen av CIF Core Components v1.4.0. Mer information finns i [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2).

* Lanserade CIF Core Components v1.4.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0).

### Felkorrigeringar {#bug-fixes-commerce}

* GraphQL-begäranden som fanns i produktkonsolen och väljarna gjordes via HTTP POST. Problemet har åtgärdats för att säkerställa att Apollo GraphQL-klienten respekterar inställningen i GraphQL klient-OSGi-konfigurationen som stöder GET-begäranden om den är konfigurerad.

* Användargränssnittet för CIF Cloud-konfigurationen visade knapparna Spara och stäng för konfigurationer i /lib och /apps/. Gränssnitten är skrivskyddade och därför är användargränssnittet fast att bara visa stängningsknappen.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i Experience Manager as a Cloud Service 2020.10.0 är 2 oktober 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Miljösidan har fått en ny design.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Cloud Manager&quot;build container&quot; har nu stöd för kompilering av projekt med antingen Java™ 8 eller Java™ 11. Stöd för Java™ 11 finns i Maven ToolChain System.

* Antalet miljövariabler per miljö har ökat till 200.

* På miljökortet på sidan Översikt visas nu upp till tre miljöer. Användare kan välja knappen **Visa alla** för att navigera till sammanfattningssidan för miljö och visa en tabell med en fullständig lista över miljöer.
Mer information finns i [Visningsmiljö](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Länken från Cloud Manager till Developer Console var inkorrekt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visade inte möjligheten att avviloläge/viloläge för sandlådeprogrammets miljö.

* Knapparna Avbryt och Spara på sidan Redigering av icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland både publicerings- och Dispatcher-segment när sådana saknas.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Arbetsflöden {#workflows}

* Stöd lades till för sökning av arbetsflödesinstanser baserat på arbetsflödets titel, arbetsflödesmodell, status, initierare, nyttolastsökväg och startdatum. Se [Sök efter arbetsflödesinstanser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html?lang=sv-SE).

## Verktyget Innehållsöverföring {#content-transfer-tool}

Läs mer om nyheter och uppdateringar för [Innehållsöverföringsverktyget](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=sv-SE) version 1.1.12.

### Nyheter {#what-is-new-ctt}

* Användarupplevelsen för loggar har förbättrats. Tidsstämplar har lagts till i loggarna för extrahering och inmatning. Meddelande har lagts till för att ange om loggarna är tomma.

### Felkorrigeringar {#ctt-bug-fixes}

* Innehållsöverföringsverktyget hoppade över innehållsfiler om migreringsuppsättningen innehöll sökvägar som delvis hade liknande filnamn.
