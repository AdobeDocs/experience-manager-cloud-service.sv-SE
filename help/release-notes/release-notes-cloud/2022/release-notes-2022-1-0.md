---
title: Versionsinformation för version 2022.1.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2022.1.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 1c40ab67-8fd7-4f29-b8c9-dd98b6d5b490
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# Versionsinformation 2022.1.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2022.1.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.1.0) är 3 februari 2022.
Följande version (2022.3.0) är den 31 mars 2022.

## Släpp video {#release-video}

Titta på videon [Januari 2022 Release Overview](https://video.tv.adobe.com/v/340120) om du vill se en sammanfattning av funktioner som lagts till i version 2022.1.0.

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* Knappen **[Aktivera frontpipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** är tillgänglig i spåret **Plats** i webbplatskonsolen för platser som använder v2-komponenten för sidkärnkomponenten. Med den här knappen konfigureras webbplatsen så att de teman som distribueras med Front End Pipeline läses in ovanpå befintliga klientbibliotek.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - Du kan nu använda AEM Dynamic Media-gränssnitt för att konfigurera allmänna inställningar och Publish-inställningar i stället för att behöva gå igenom Dynamic Media Classic skrivbordsprogram.

* [!DNL Dynamic Media] har nu stöd för hämtning, förhandsgranskning, uppspelning och publicering för MXF-videor. Anteckningar och videor som kan köpas för MXF-videor stöds ännu inte.

* När du har konfigurerat en anslutning mellan distributioner av fjärr-DAM och platser, blir resurserna på fjärr-DAM tillgängliga i Sites-distributionen. Du kan nu utföra [uppdaterings-, borttagnings-, namnbyt- och flyttåtgärderna](/help/assets/use-assets-across-connected-assets-instances.md) på fjärr-DAM-resurser eller -mappar. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen.

### Nya funktioner i betaversionskanalen [!DNL Assets] {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] ger nu flexibilitet att [konfigurera ett aliaskonto](/help/assets/dynamic-media/dm-alias-account.md) i användargränssnittet och säkerställer därmed att körklara Dynamic Media-URL:er och inbäddningskod för visningsprogram uppdateras. Detta påverkar SEO positivt för att återspegla uppdateringar som gjorts i ert företagskontext, t.ex. omprofilering.

* Du kan nu använda användargränssnittet [!DNL Experience Manager Assets] för att:

   * Konfigurera identifiering av dubblettresurser i en databas.

   * Konfigurera tillägg av digitala vattenstämplar till bilder.

* Administratörerna kan nu konfigurera e-posttjänsten för stora hämtningar. Det gör att användarna kan [aktivera e-postmeddelanden för stora hämtningar](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) från gränssnittet [!DNL Experience Manager Assets]. Användaren får ett e-postmeddelande med nedladdningslänken för den arkiverade zip-mappen när nedladdningen är klar.


* Funktionen [Hantera publikation](/help/assets/manage-publication.md) har förbättrats med ett förbättrat användargränssnitt. Användarna kan publicera eller avpublicera innehåll till och från det valda målet, [Lägg till innehåll](/help/assets/manage-publication.md#add-content) i publiceringslistan från hela DAM-databasen, [Inkludera mappinställningar](/help/assets/manage-publication.md#include-folder-settings) för att publicera innehåll i de valda mapparna och tillämpa filter, och [schemalägga publicering](/help/assets/manage-publication.md#publish-assets-later) för ett senare datum eller tid.

### Felkorrigeringar {#bug-fixes}

* Obearbetade resurser utan ursprunglig återgivning skickas till Asset compute för bearbetning när resurser migreras från AEM lokalt till molntjänster.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera formulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera PDF från XFA-PDF.
   * Generera PDF-, PostScript-, PCL- och ZPL-dokument i grupp genom att sammanfoga flera datauppsättningar med källmallar.

* **Anpassade teckensnitt för dokument med dokumentinformation och PDF som skapats med kommunikations-API:er**: Du kan nu använda teckensnitt som godkänts av varumärket i PDF-dokument som skapats med kommunikations-API:er för att anpassa dem efter organisationens krav.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

* **[Assembler API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: Sammanställ API:er för att kombinera, ordna om, förstärka och få information om PDF-dokument.


## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Förbättrade komponenter för myAccount
* Produktrekommendationskomponenten stöder ytterligare sidtyper (hemsida, kundvagn, orderbekräftelse)
* **Önsklista**
   * Inloggade besökare kan lägga till produkter i en önskelista
   * Du kan hantera önskelistan och dess produkter via mitt konto
   * Knappen&quot;Lägg till i önskelista&quot; kan aktiveras/inaktiveras på komponentnivå via en policy (exempel produktnivå, produktinformation)
   * Finns som kärnkomponent och i AEM Venia Storefront

<!-- Image was not found during PR validation despite correct path ![Wishlist](/help/assets/CIF/wantlist.png) -->

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Lanseringsdatumet för Cloud Manager i AEM as a Cloud Service 2022.01.0 är 20 januari 2022. Nästa version planeras till den 10 februari 2022.

### Nyheter {#what-is-new-cm}

* Cloud Manager [undviker att återskapa kodbasen när det upptäcker att samma Git-implementering används](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) vid körningar av flera helstackspipeline.
* För åtkomst till AEM-miljöloggen krävs nu produktprofilen **Deployment Manager**. Användare utan den här profilen ser en inaktiverad knapp i användargränssnittet.
* Gränssnittet tillåter inte konfiguration av pipeline i gränssnittet för ett program där Sites inte är aktiverat som en lösning.
* När du genererar ett Git-lösenord visas förfallodatumet.

### Felkorrigeringar {#bug-fixes-cm}

* Null-pekarundantag som påträffades i vissa frontendsdistributioner har korrigerats.
* Miljövariabler kan nu läggas till, uppdateras och tas bort när en miljö kör en gammal version av AEM.
* Steget för att skapa bilder markeras inte längre som FEL för rörledningar som i vissa sällsynta fall använde det schemalagda steget.
* För program med endast en databas visas databasens namn på körningsskärmen för pipeline.

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.8.6 är 3 februari 2022.

### Nyheter {#what-is-new-ctt}

* Innehållsvalidering - Användarna kan på ett tillförlitligt sätt avgöra om allt innehåll som extraherats av verktyget Innehållsöverföring har importerats till målinstansen. Om du vill använda den här funktionen aktiverar du den i `System Console` AEM källmiljön. Mer information finns i [Verifiera innehållsöverföringar - Komma igång](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html#getting-started).

### Felkorrigeringar {#bug-fixes-ctt}

* Vissa användare mappades inte eftersom användarmappningen var skiftlägeskänslig. Den här har åtgärdats. Användarmappning är inte längre skiftlägeskänslig.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.24 är 1 februari 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att identifiera och rapportera antalet resurser med och utan smarta taggar.
* Möjlighet att identifiera och rapportera vilken version av Core Component som används.
* Möjlighet att identifiera och rapportera om vilken typ av källnivå (författare eller Publish) där BPA utfördes.

### Felkorrigeringar {#bug-fixes-bpa}

* Logiken för BPA-storleksändring gjordes snabbare och effektivare.
* I vissa scenarier ökade inte BPA antalet analyserade när det kördes. Den här har åtgärdats.
