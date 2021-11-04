---
title: Versionsinformation för version 2020.10.0 av [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 15908636f916a55008513035e3072cf1b1cc5f1c
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 är 28 oktober 2020.
Följande version (2020.11.0) kommer att vara den 1 december 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* **[Core Components 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**: Adobe Experience Manager as a Cloud Service drar nytta av automatiska uppdateringar av den senaste versionen av Core Components. Version 2.12.0 innehåller de senaste förbättringarna från communityn. Förbättringarna omfattar [en ny formulärhanterare för POST,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) möjligheten att inkludera anpassad CSS, JavaScript och metadata [taggar via kontextmedveten konfiguration,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) och [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) för att förenkla integreringen av datalager i Adobe i anpassade komponenter. Se [lista över ändringar](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) i 2.12.0.

* **[Project Archetype 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: Den rekommenderade grunden för att starta ett nytt Experience Manager-projekt har förbättrats. Nu med nya [Adobe-klientdatalager](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html), alternativ till [leverera webbplatsen i AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) och nya [utökningspunkter för att lägga till projekt-CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub-mappar](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Möjlighet att skapa målgruppsmappar för att enkelt ordna, hitta och välja målgruppssegment som kan användas för målinriktningsfunktioner i ContextHub.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]smart taggning för video**: Genom att använda AI-modeller för att analysera videoinnehåll för objekt- och åtgärdsspecifika taggar kan DAM-användare lägga mindre tid på att lägga till taggar och mer tid på att använda den exponerade, omfattande informationen. Ni levererar i sin tur rätt upplevelse till kunderna. Se [Smart tagga videoresurser](/help/assets/smart-tags-video-assets.md).

* **Brand Portal-förbättringar**: Följande nya funktioner och mer finns i [!DNL Brand Portal]. Mer information finns i [[!DNL Brand Portal] versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Förbättrad nedladdning](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) för förenklad och snabb nedladdning. Ytterligare hämtningskonfigurationer kan konfigureras av administratörer för att ge en upplevelse som passar användare och företag.
   * Navigera till filer med ett klick, [Samlingar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)och Delade länkar är nu tillgängliga från alla sidor.
   * Användarna kan [välja och hämta specifika återgivningar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) nu. Det nya hämtningsalternativet för återgivning finns på panelen Återgivningar på sidan Resursinformation.
   * En tidsgräns på 15 minuter för gästanvändarsessioner ger en bättre upplevelse för alla samtidiga användare.

* **[!DNL Adobe Asset Link]version 2.1**: En ny version av [Adobe Asset Link](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) tillägg för [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]och [!DNL Adobe InDesign] är tillgängligt. Kompatibiliteten med de senaste [!DNL Adobe Creative Cloud] program med version 2021, släppt i oktober 2020.

* **[!DNL Assets]Stöd för WebP-filer**: [!DNL Assets] as a Cloud Service har nu stöd för WebP-bildformat. WebP är ett framväxande bildformat som skapas av Google. Bilder i WebP-filformat kan inte skiljas från JPG eller PNG-filer och filerna är mycket mindre. Lägre filstorlek förbättrar sidinläsningen och hjälper innehållsskaparna att leverera en snabbare webbupplevelse. Se hur du använder WebP i [skapa bearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#forms-oct-2021}

### Nyheter i [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics för Adaptive Forms**: Nu kan du fånga in och spåra beteenden hos både inloggade och ej inloggade (anonyma) via Adobe Analytics för Adaptive Forms för att samla in slutanvändarinsikter. Det hjälper företagsanvändare att fatta välgrundade beslut om anpassat formulärinnehåll, layout och format baserat på insamlade insikter.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms-oct-2021}

* **Externt AEM arbetsflödesdata för säker bearbetning**: Du kan lagra data AEM arbetsflödesvariabler som innehåller känsliga SPD-element (Personal Data) i en kundhanterad databas för säker bearbetning. När arbetsflödet bearbetas sparas inte data som lagras i arbetsflödesvariabler AEM databasen. Den hämtas på begäran från den kundhanterade databasen.

### Betafunktioner i [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) hjälper dig att kombinera en mall och XML-data för att generera dokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att anmäla dig till betaprogrammet.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Vad är nytt? {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.10.2 som innehåller den senaste CIF Core Components version v1.4.0. Se [CIF Venias referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) för mer information.

* Frisläppta CIF-kärnkomponenter v1.4.0. Se [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) för mer information.

### Felkorrigeringar {#bug-fixes-commerce}

* GraphQL-begäranden som fanns i produktkonsolen och väljarna gjordes via HTTP-POST. Problemet har åtgärdats för att säkerställa att Apollo GraphQL-klienten respekterar inställningen i GraphQL-klientens OSGi-konfiguration för att stödja GET-begäranden om detta har konfigurerats.

* CIF Cloud-konfigurationsgränssnittet visade knapparna Spara och stäng för konfigurationer i /lib och /apps/. Gränssnitten är skrivskyddade och därför är användargränssnittet fast att bara visa stängningsknappen.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i Experience Manager as a Cloud Service 2020.10.0 är 2 oktober 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Miljösidan har fått en ny design.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Cloud Manager &quot;build container&quot; har nu stöd för kompilering av projekt med antingen Java™ 8 eller Java™ 11. Stöd för Java™ 11 finns i Maven ToolChain System.

* Antalet miljövariabler per miljö har ökat till 200.

* På miljökortet på sidan Översikt visas nu upp till tre miljöer. Användarna kan välja **Visa alla** för att navigera till miljösammanfattningssidan för att visa en tabell med en fullständig lista över miljöer.
Se [Visningsmiljö](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) för mer information.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Knapparna Avbryt och Spara på sidan Redigering av icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utsändning när det inte finns några.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Arbetsflöden {#workflows}

* Stöd lades till för sökning av arbetsflödesinstanser baserat på arbetsflödets titel, arbetsflödesmodell, status, initierare, nyttolastsökväg och startdatum. Se [Sök efter arbetsflödesinstanser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Content Transfer Tool {#content-transfer-tool}

Läs mer om nyheter och uppdateringar för [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Version v1.1.12.

### Vad är nytt? {#what-is-new-ctt}

* Användarupplevelsen för loggar har förbättrats. Tidsstämplar har lagts till i loggarna för extrahering och inmatning. Meddelande har lagts till för att ange om loggarna är tomma.

### Felkorrigeringar {#ctt-bug-fixes}

* Innehållsöverföringsverktyget hoppade över innehållsfiler om migreringsuppsättningen innehöll sökvägar som delvis hade liknande filnamn.
