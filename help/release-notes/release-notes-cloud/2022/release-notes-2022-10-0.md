---
title: Versionsinformation för version 2022.10.0 av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2022.10.0 av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8fce7c50-f322-4bcf-bd76-390faedfd5b7
source-git-commit: 89f23a590338561b4cfeb10b54a260a135ec2f08
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Versionsinformation 2022.10.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen i version 2022.10.0 av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell månadsversion (2022.10.0) är 10 november 2022. Nästa månadsutgåva (2023.1.0) planeras att släppas den 9 februari 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för oktober 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}


### Nya funktioner i [!DNL Sites] {#sites-features}

* The [Fliken Personalisering för Experience Fragments](/help/sites-cloud/authoring/fragments/content-fragments.md#personalization-experience-fragment) möjliggör funktioner för segmenteringsspecifikation för Experience Fragment Editor och flexibiliteten att skapa kapslade Experience Fragments, där sidhuvuds- och sidfotsvarianter kan skapas för flera segment. Före lanseringen av den här funktionen är AEM personalisering bara tillgängligt för webbplatssidor, men inte för Experience Fragments

* The [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) gör det nu möjligt att effektivt hantera översatta innehållsfragment. Åtkomst med ett klick har tillhandahållits för att visa alla språkkopior också. Användarna kan också filtrera tabellvyn efter de språkområden de är intresserade av.

![Språk för innehållsfragment](/help/release-notes/assets/cfconsole-languages.png)

* Minska sidinläsningstiden för besökare ytterligare genom att optimera inställningarna för bildstorlek i mallar. Mer information om bildkomponenten finns på [Core WCM Component](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Med Experience Manager Assets kan du nu överföra dokument i andra format som stöds och[förhandsgranska dem med det medföljande Document Cloud-visningsprogrammet](/help/assets/manage-pdf-documents.md). De format som stöds är TXT, RTF, DOC, DOCX, PPT, PPTX, XLS och XLSX.

  ![PDF-återgivning för andra format](/help/release-notes/assets/multi-page-other-formats.png)


### Nya funktioner i [!DNL Assets] prerelease {#prerelease-features-assets}

* Experience Manager Assets använder nu ett förbättrat ramverk för artificiell intelligens för smarta taggar i bilder. Den här innehållsintelligensen ger bättre relevans och precision för smarta taggar som är tillgängliga för alla bildresurser vid förtäring. Dessutom fylls orienteringsinformationen i `cq:tags`, vilket ger bättre sökresultat med orienteringsfiltret.

  Om du är intresserad av att delta i betaversionen, [fyll i formuläret](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) senast 14 november.

* Experience Manager Assets nu [stöder SAS-token](/help/assets/add-assets.md#asset-bulk-ingestor) utöver åtkomstnyckeln för autentisering vid anslutning till Azure Blob Storage-datakällan för inmatning av resurser med verktyget för massimport.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* **Adaptiv Forms-mallredigerare**: Med mallredigerare kan du fördefiniera den grundläggande strukturen och utseendet för Adaptiv Forms i en organisation. Den här versionen innehåller följande förbättringar för mallredigeraren:
   * **[Formulärdatamodell i mallredigerare](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: Du kan koppla ett formulärdatamodellschema till en anpassad formulärmall i mallredigeraren. Det minskar tiden det tar att skapa ett adaptivt formulär. Alternativet läggs också till i Adaptiv Forms-redigerare så att användare kan välja eller ändra formulärdatamodellen för befintliga formulär.
   * **[Dokument för post i mallredigeraren](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: Du kan nu standardisera dokumentgenereringen för alla formulär som skapas med en mall. Detta bidrar till att förbättra regelefterlevnaden och standardiseringen för organisationens krav.

* **[Starta guiden Adaptivt formulär från en AEM Sites-sida](/help/forms/embed-adaptive-form-aem-sites.md)**: AEM Sites-sidan har utökat stöd för Adaptive Forms. Nu kan du skapa ett adaptivt formulär eller bädda in ett befintligt adaptivt formulär medan du finns kvar på AEM Sites-sidan.
* **[Ändra visningsjustering för kryssrutor och alternativknappar i DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: Du kan nu ange önskad justering (Vågrät, Lodrät, Samma som Adaptiv Forms) för kryssrutan och alternativknappen i Postdokumentet. Med det här alternativet anger du placeringen av kryssrutor och alternativknappar i postdokumentet.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Författare kan dynamiskt berika produktlistor med Experience Fragments (exempel: placera banner mellan produktlistor).
* Listkomponenten har nu stöd för associerade produkt-/kategorisidor för att dynamiskt visa relaterade sidor.
* Stöd för komponenterna i Peregrine 12.5 har lagts till.
* Stöd för prisinläsning på klientsidan har lagts till i produktlasrar och karuseller.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nyheter {#what-is-new-foundation}

* AEM as a Cloud Service (Author Service) är nu integrerat med Unified Shell för att förbättra användarupplevelsen och sammanföra den med alla andra Experience Cloud-program. Se AEM som [Cloud Service i enhetligt gränssnitt](/help/overview/aem-cloud-service-on-unified-shell.md) för mer information.

* Som tidigare nämnts i versionsinformationen är nu användningen av administratörsskärmen för replikeringsagenten eller replikerings-API:t för distribution av innehållspaket som är större än 10 MB (noder med egenskaper, exklusive binärfiler) föråldrat och påtvingat. Se [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Arbetsflödet Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) för förslag på metoder för att replikera dessa stora innehållspaket.

* Dispatcher-konfigurationen refererar nu till en fil som listar vanliga frågeparametrar för marknadsföringskampanjer. Kunderna kan välja att avkommentera de parametrar som är relevanta för dem, vilket ger bättre cachning. Se [Parametrar för marknadsföringskampanjer](/help/implementing/dispatcher/caching.md#marketing-parameters) för mer information.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
