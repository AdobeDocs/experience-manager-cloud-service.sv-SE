---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
translation-type: tm+mt
source-git-commit: 707c5daf5c48b2054fd684b4557143fbd8d873c7
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] som en Cloud Service.

>[!NOTE]
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2021.2.0 är 25 februari 2021.
Följande version (2021.3.0) kommer att vara den 25 mars 2021.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service  {#sites}

* **[RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)**: Stöd för visning och redigering av externa SPA i AEM.

* **[Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Lagt till möjlighet att ladda upp ett fristående enkelsidigt program till en AEM, lägga till redigerbara innehållsavsnitt och aktivera redigering.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

## Nyheter i [!DNL Assets] {#what-is-new-assets}

* Företag kan nu hämta resurser med [!DNL Brand Portal]. Funktionen för resurskälla utnyttjar [!DNL Brand Portal] för att hjälpa kunderna att interagera med byråanvändare för att hämta resurser för nya marknadsföringskampanjer, fotografier och projekt. Se [resurskälla i [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html).

* I användningsrapporten för [!DNL Brand Portal] visas nu endast de aktiva användarna. De inaktiva användarna visas inte nu. Aktiva användare är de vars konto har tilldelats en produktprofil i [!DNL Admin Console]. Se [[!DNL Brand Portal] rapporter](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* I [!DNL Brand Portal] har en ny hämtningsinställning införts som gör att du kan skapa separata mappar för varje resurs när du hämtar mappar, samlingar och så vidare. Se [hämtningsinställningar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## Felkorrigeringar i [!DNL Assets] {#bug-fixes-assets}

* När en ny version av en befintlig resurs skapas efter att namnkonflikten har lösts, skrivs metadata för den ursprungliga resursen över. (CQ-4313594)
* När en resurs med lång anteckningstext skrivs ut beskärs anteckningstexten, även om det finns utrymme. (CQ-4314101)
* När flera resurser har valts för att uppdatera egenskaperna inträffar ibland ett fel eller så uppdateras egenskaperna för en avmarkerad resurs. (CQ-4316532)
* När du försöker öppna [!UICONTROL Assets Admin Search Rail] är sidan tom och om du klickar på [!UICONTROL Edit] > [!UICONTROL Settings] genereras ett fel. (CQ-4315079)

## Adobe Experience Manager Commerce som Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Product Experience Management: Berika katalogsidorna individuellt med Experience Fragments.

* Utökade egenskaper för produktkonsolen för att visa länkade resurser och upplevelsefragment, inklusive åtgärder för att snabbt navigera till det associerade innehållet.

* Lanserade CIF Venia Reference Site - 2021.02.24 som innehåller den senaste CIF Core Components version v1.8.0. Mer information finns i [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24).

* Frisläppta CIF-kärnkomponenter v1.8.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0).

## Cloud Manager {#cloud-manager}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.3.0.

## Releasedatum {#release-date-cm-march}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.3.0 är 11 mars 2021.


### Nyheter {#what-is-new-march}

* Kunder som har miljöer med befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat och anpassade domännamn ser ett meddelande om sina tidigare konfigurationer och kommer att kunna använda självbetjäning via användargränssnittet.

* Användare med nödvändig behörighet kan nu redigera program och göra följande på ett självbetjäningssätt.

* Etiketten AEM push-uppdatering visas nu för både Pipeline Execution och Activity screens.

* Om en miljö är i viloläge men det även finns en AEM tillgänglig, prioriteras statusen&quot;Viloläge&quot; framför&quot;Tillgänglig uppdatering&quot;.

* Användarna kan nu se sin molnhanterarroll(er) genom att välja alternativet Visa molnhanterarroll(er) efter att ha navigerat till ikonen Användarprofil (överst till höger) i Unified Shell.

* Etiketten&quot;Ansökan om godkännande&quot; har ändrats till&quot;Produktionsgodkännande&quot; för större tydlighet.

* Versionsetiketten har ändrats till&quot;Git-tagg&quot; i körningsfönstret för produktionspipeline.

* Etiketterna som definierar beteendet när viktiga mätvärden inte uppfyller det definierade tröskelvärdet har märkts om för att återspegla deras verkliga beteende - Avbryt omedelbart och godkänn omedelbart.

* Listorna över klass- och metodborttagning har uppdaterats baserat på version `2021.3.4997.20210303T022849Z-210225` av AEM Cloud Service-SDK.

* Produktionspipelinen för Cloud Manager kommer nu att innehålla testning av anpassade användargränssnitt.

### Felkorrigeringar {#bug-fixes-cm-march}

* Paketversionshantering hoppades över i vissa fall under AEM push-uppgradering.

* Vissa kvalitetsproblem upptäcktes inte korrekt när paket bäddats in i andra paket.

* I svåra fall kan standardprogramnamnet som genereras när dialogrutan Lägg till program öppnas vara en dubblett av ett befintligt programnamn.

* Om användaren navigerar bort från sidan för pipeline-körning omedelbart efter att ha startat en pipeline visas ett felmeddelande om att åtgärden misslyckades, även om körningen faktiskt startar.

* Byggsteget startades om i onödan när kundbyggen resulterade i ogiltiga paket.

* Ibland kan användaren se en grön &quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när den konfigurationen inte har distribuerats.

* Alla befintliga produktionspipelinjer aktiveras automatiskt med Experience Audit-steget.


### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.2.0 är 11 februari 2021.

### Nyheter {#what-is-new-cloud-manager}


* Resurskunder kan nu välja när och var de ska distribuera sin Brand Portal-instans på ett självbetjäningssätt via användargränssnittet i Cloud Manager. För ett vanligt (icke-sandlådeprogram) program med Assets-lösning kan Brand Portal nu etableras i produktionsmiljön. Etableringen kan bara göras en gång i produktionsmiljön.

* Den AEM Project Archetype som används i Project och Sandbox Creation har uppdaterats till version 25.

* Listan med föråldrade API:er som identifieras vid kodskanning har förfinats så att den innehåller ytterligare klasser och metoder som har tagits bort i den senaste SDK-versionen av Cloud Servicen.

* SonarQube-profilen för Cloud Manager har uppdaterats för att ta bort Sonar-regelbläckfisk:S2142. Detta kommer inte längre att orsaka en konflikt med kontrollerna för trådavbrott.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan lägga till/uppdatera domännamn för tillfället eftersom den associerade miljön antingen har en pågående pipeline kopplad till sig eller som väntar på godkännande.

* Egenskaper som angetts i kundens `pom.xml`-filer som har prefixats med sonar kommer nu att tas bort dynamiskt för att undvika problem med bygg- och kvalitetsskanning.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* Ytterligare regler för kodkvalitet har lagts till för att täcka problem med Cloud Servicens kompatibilitet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Det är inte längre skiftlägeskänsligt att matcha SSL-certifikat mot ett domännamn.

* Molnhanterarens användargränssnitt informerar nu en användare om att certifikatets privata nycklar inte uppfyller 2 048-bitarsgränsen med ett felmeddelande.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* I vissa fall kan ett internt problem leda till att miljön tas bort.

* En del pipeline-fel rapporterades felaktigt som pipeline-fel.

## Content Transfer Tool {#content-transfer-tool}

### Releasedatum {#release-date-ctt-march}

Releasedatum för innehållsöverföringsverktyget v1.3.0 är 4 mars 2021.

### Nyheter i verktyget Innehållsöverföring {#what-is-new-ctt-march}

* CTT installeras nu på `/apps` i stället för `/libs` webbläsarbokmärken på vissa sidor kanske inte längre är giltiga.
* När CTT är installerat måste användaren navigera ytterligare en nivå för att komma till sidan Innehållsöverföring. Mer information finns i [Använda verktyget för innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html).

### Felkorrigeringar {#bug-fixes-ctt-march}

* När CTT migrerade innehåll från en viss sökväg drog det in resurser som inte hade med varandra att göra. Detta har åtgärdats


### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.2.4 är 10 februari 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* Vid mappning av flera användare mappades vissa användares IMS-ID felaktigt. Den här har åtgärdats.

### Releasedatum {#release-date-ctt-feb}

Releasedatum för innehållsöverföringsverktyget v1.2.2 är 1 februari 2021.

### Nyheter i verktyget Innehållsöverföring {#what-is-new-ctt}

* Ny funktion och nytt användargränssnitt har lagts till i verktyget Innehållsöverföring - verktyget för användarmappning. Den här funktionen mappar automatiskt befintliga användare och grupper till deras Adobe Identity Management-system-ID som en del av innehållsmigreringsaktiviteten.
Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).
* Verktyget Innehållsöverföring migrerar nu alla grupper och användare som det hänvisas till i migreringsuppsättningen, inklusive underordnade.
* Användarna kan välja vissa sökvägar under `/etc` när de skapar migreringsuppsättningar.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.2 är 18 februari 2021.

### Nyheter i Best Practices Analyzer {#what-is-new-bpa}

* Möjlighet att upptäcka användning av AEM Forms och AEM Forms och ange områden som är relevanta för migrering till AEM Forms som Cloud Service.
* Möjlighet att upptäcka och rapportera användning och antal anpassade komponenter och mallar.
* Möjlighet att identifiera vilken typ av nodarkiv och datalager som används.
* Möjlighet att upptäcka användningen av Dynamic Media.
* Möjlighet att identifiera den Java-version som används.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i Code Refactoring Tools {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller flera felkorrigeringar för Repository Modernizer.
Mer information om detta plugin-program finns i [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits).

### Felkorrigeringar {#bug-fixes-crt}

* Flera felkorrigeringar har gjorts i Repository Modernizer.
Se [GitHub-resurs: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) om du vill ha mer information.








