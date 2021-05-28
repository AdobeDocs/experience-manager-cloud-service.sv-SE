---
title: Versionsinformation för version 2020.10.0 av [!DNL Adobe Experience Manager] som Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service Release Notes för 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service 2020.10.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] som en Cloud Service 2020.10.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2020.10.0 är 28 oktober 2020.
Följande version (2020.11.0) kommer att vara den 1 december 2020.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* **[Core Components 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**: AEM som en Cloud Service har nytta av automatiska uppdateringar av den senaste utgåvan av Core Components. Version 2.12.0 innehåller de senaste förbättringarna från användargruppen, som [en ny formulärhanterare för POSTER;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) möjlighet att inkludera anpassade CSS-, Javascript- och metadata [taggar via kontextmedveten konfiguration;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) och ett [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)-verktyg för att förenkla integreringen av Adobe datalager i anpassade komponenter. Se [listan över ändringar](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) i 2.12.0.

* **[Project Archetype 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: Den rekommenderade grunden för att starta ett nytt AEM-projekt har blivit bättre, nu med nya  [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html), möjlighet att  [leverera webbplatsen i AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) och nya  [tilläggspunkter för att lägga till projekt-CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub-mappar](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Möjlighet att skapa målgruppsmappar för att enkelt ordna, hitta och välja målgruppssegment som kan användas för målinriktningsfunktioner i ContextHub.

## [!DNL Adobe Experience Manager Assets] som en Cloud Service {#assets}

* **[!DNL Adobe Sensei]smart taggning**: Genom att utnyttja AI-modeller för att analysera videoinnehåll för objekt- och åtgärdsspecifika taggar kan DAM-användare lägga mindre tid på att lägga till taggar och mer tid på att utnyttja den omfattande information som exponeras för att leverera rätt upplevelse till kunderna. Se [Smart-tagg för videomaterial](/help/assets/smart-tags-video-assets.md).

* **Brand Portal-förbättringar**: Följande nya funktioner och mer finns i  [!DNL Brand Portal]. Mer information finns i [[!DNL Brand Portal] versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Förbättrade ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) nedladdningsupplevelser för enklare och snabbare nedladdning. Ytterligare hämtningskonfigurationer kan konfigureras av administratörer för att ge en upplevelse som passar användare och företag.
   * Enklicksnavigering till filer, [Samlingar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) och Delade länkar är nu möjligt från vilken sida som helst.
   * Användarna kan [välja och hämta specifika renderingar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) nu. Det nya hämtningsalternativet för återgivning finns på panelen Återgivningar på sidan Resursinformation.
   * En tidsgräns på 15 minuter för gästanvändarsessioner ger en bättre upplevelse för alla samtidiga användare.

* **[!DNL Adobe Asset Link]version 2.1**: En ny version av  [Adobe Asset ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Linkextension för  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]och  [!DNL Adobe InDesign] finns tillgänglig. Den lägger till kompatibilitet med de senaste [!DNL Adobe Creative Cloud]-programmen med version 2021, som släpptes i oktober 2020.

* **[!DNL Assets]Stöd** för WebP-filer:  [!DNL Assets] som en Cloud Service har nu stöd för WebP-bildformat. WebP är ett framväxande bildformat som skapats av Google. Bilder i WebP-filformat kan inte skiljas åt visuellt från JPG- eller PNG-filer och filerna är mycket mindre. Lägre filstorlek förbättrar sidinläsningen och hjälper innehållsskaparna att leverera en snabbare webbupplevelse. Se hur du använder WebP i [skapa bearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce som Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.10.2 som innehåller den senaste CIF Core Components version v1.4.0. Mer information finns i [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2).

* Frisläppta CIF-kärnkomponenter v1.4.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0).

### Felkorrigeringar {#bug-fixes-commerce}

* GraphQL-begäranden i produktkonsolen och väljare gjordes via HTTP-POST. Detta har åtgärdats för att säkerställa att Apollo GraphQL-klienten respekterar inställningen i GraphQL-klientens OSGi-konfiguration för att stödja GET-begäranden om detta har konfigurerats.

* CIF Cloud-konfigurationsgränssnittet visade knapparna Spara och stäng för konfigurationer i /lib och /apps/. Dessa är skrivskyddade och därför har användargränssnittet fast att bara visa stängningsknappen.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.10.0 är 2 oktober 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Miljösidan har fått en ny design.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Molnhanterarens byggbehållare har nu stöd för kompilering av projekt med antingen Java 8 eller Java 11. Stöd för Java 11 finns i Maven ToolChain System.

* Antalet miljövariabler per miljö har ökat till 200.

* Miljökortet på sidan Översikt visar nu upp till tre miljöer. Användare kan välja knappen **Visa alla** för att navigera till sammanfattningssidan för miljö och visa en tabell med en fullständig lista över miljöer.
Mer information finns i [Visningsmiljö](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Knapparna Avbryt och Spara på sidan Redigering av icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Arbetsflöden {#workflows}

* Stöd lades till för sökning av arbetsflödesinstanser baserat på arbetsflödets titel, arbetsflödesmodell, status, initierare, nyttolastsökväg och startdatum. Se [Förekomster av arbetsflöden för sökning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Content Transfer Tool {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för [verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Version v1.1.12.

### Nyheter {#what-is-new-ctt}

* Användarupplevelsen för loggar har förbättrats. Tidsstämplar har lagts till i loggarna för extrahering och inmatning. Meddelande har lagts till för att ange om loggarna är tomma.

### Felkorrigeringar {#ctt-bug-fixes}

* Innehållsöverföringsverktyget hoppade över innehållsfiler om migreringsuppsättningen innehöll sökvägar som delvis hade liknande filnamn. Den här har åtgärdats.
