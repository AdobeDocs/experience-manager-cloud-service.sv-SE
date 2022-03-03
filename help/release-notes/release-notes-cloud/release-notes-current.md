---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 08ed7f06b60ab65a0060c4fa00f902006f3afbdd
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.1.0) är 3 februari 2022.
Följande version (2022.2.0) är den 10 mars 2022.

## Släpp video {#release-video}

Ta en titt på [Versionsöversikt januari 2022](https://video.tv.adobe.com/v/340120) video med en sammanfattning av funktioner som lagts till i version 2022.1.0.

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* The **[Aktivera frontdelspipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** finns i **Plats** i Sites-konsolen för platser som använder v2 för Page Core-komponenten. Med den här knappen konfigureras webbplatsen så att de teman som distribueras med Front End Pipeline läses in ovanpå befintliga klientbibliotek.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - Du kan nu använda AEM Dynamic Media gränssnitt för att konfigurera allmänna inställningar och publiceringsinställningar i stället för att behöva gå igenom Dynamic Media Classic datorprogram.

* [!DNL Dynamic Media] har nu stöd för inhämtning, förhandsgranskning, uppspelning och publicering av MXF-videor. Anteckningar och videor som kan köpas för MXF-videor stöds ännu inte.

* När du har konfigurerat en anslutning mellan distributioner av fjärr-DAM och platser, blir resurserna på fjärr-DAM tillgängliga i Sites-distributionen. Nu kan du utföra [uppdatera, ta bort, byta namn på och flytta åtgärder](/help/assets/use-assets-across-connected-assets-instances.md) på DAM-fjärrresurserna eller -mapparna. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen.

### Nya funktioner i [!DNL Assets] prerelease channel {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] ger nu flexibilitet att [konfigurera ett aliaskonto](../../assets/dynamic-media/dm-alias-account.md) i användargränssnittet, vilket säkerställer att färdiga Dynamic Media-URL:er och inbäddningskod för visningsprogram uppdateras. Detta påverkar SEO positivt för att återspegla uppdateringar som gjorts i ert företagskontext, t.ex. omprofilering.

* Nu kan du använda [!DNL Experience Manager Assets] till

   * Konfigurera identifiering av dubblettresurser i en databas.

   * Konfigurera tillägg av digitala vattenstämplar till bilder.

* Administratörerna kan nu konfigurera e-posttjänsten för stora hämtningar. Det gör att användarna kan [aktivera e-postmeddelanden för stora nedladdningar](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) från [!DNL Experience Manager Assets] gränssnitt. Användaren får ett e-postmeddelande med nedladdningslänken för den arkiverade zip-mappen när nedladdningen är klar.


* The [Hantera publikation](/help/assets/manage-publication.md) har förbättrats med ett förbättrat användargränssnitt. Användarna kan publicera eller avpublicera innehåll till och från det valda målet, [Lägg till innehåll](/help/assets/manage-publication.md#add-content) till publiceringslistan från DAM-databasen, [Inkludera mappinställningar](/help/assets/manage-publication.md#include-folder-settings) för att publicera innehållet i de valda mapparna och tillämpa filter, och [schemaläggning](/help/assets/manage-publication.md#publish-assets-later) till ett senare datum eller en senare tid.

### Felkorrigeringar {#bug-fixes}

* Obearbetade resurser utan ursprunglig återgivning skickas till Asset compute för bearbetning när resurser migreras från AEM lokalt till molntjänster.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   * Generera dokument genom att fylla i mallfiler med XML-data.
   * Generera formulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   * Generera PDF från XFA-PDF.
   * Generera PDF-, PostScript-, PCL- och ZPL-dokument genom att sammanfoga flera datauppsättningar med källmallar.

* **Anpassade teckensnitt för dokument i dokumentformat och PDF som skapats med kommunikationsAPI:er**: Nu kan du använda typsnitt som är godkända av varumärket i PDF-dokument som genererats med kommunikations-API:er för att anpassa dig till organisationens krav.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* **[Assembler API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: Sammanställ API:er för att kombinera, ordna om, förbättra och få information om PDF-dokument.


## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Förbättrade komponenter för myAccount
* Produktrekommendationskomponenten stöder ytterligare sidtyper (hemsida, kundvagn, orderbekräftelse)
* **Önsklista**
   * Inloggade besökare kan lägga till produkter i en önskelista
   * Du kan hantera önskelistan och dess produkter via mitt konto
   * Knappen&quot;Lägg till i önskelista&quot; kan aktiveras/inaktiveras på komponentnivå via en policy (exempel produktnivå, produktinformation)
   * Finns som kärnkomponent och i AEM Venia Storefront

![Önsklista](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2022.01.0 är 20 januari 2022. Nästa version är planerad till den 10 februari 2022.

### Nyheter {#what-is-new-cm}

* Cloud Manager kommer att [undvika att återskapa kodbasen när den upptäcker att samma Git-implementering används](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) i flera fullständiga pipeline-körningar.
* För att få åtkomst till AEM måste du **Distributionshanteraren** produktprofil. Användare utan den här profilen ser en inaktiverad knapp i användargränssnittet.
* Gränssnittet tillåter inte konfiguration av pipeline i gränssnittet för ett program där Sites inte är aktiverat som en lösning.
* När du genererar ett Git-lösenord visas förfallodatumet.

### Felkorrigeringar {#bug-fixes-cm}

* Null-pekarundantag som påträffades i vissa frontendsdistributioner har korrigerats.
* Miljövariabler kan nu läggas till, uppdateras och tas bort när en miljö kör en gammal version av AEM.
* Steget för att skapa bilder markeras inte längre som FEL för rörledningar som i vissa sällsynta fall använde det schemalagda steget.
* För program med endast en databas visas databasens namn på körningsskärmen för pipeline.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.8.6 är 3 februari 2022.

### Nyheter {#what-is-new-ctt}

* Innehållsvalidering - Användare kan på ett tillförlitligt sätt avgöra om allt innehåll som extraherats med verktyget Innehållsöverföring har importerats till målinstansen. Om du vill använda den här funktionen måste du aktivera den i `System Console` i AEM. Se [Verifierar innehållsöverföringar - Komma igång](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) för mer information.

### Felkorrigeringar {#bug-fixes-ctt}

* Vissa användare mappades inte eftersom användarmappningen var skiftlägeskänslig. Den här har åtgärdats. Användarmappning är inte längre skiftlägeskänslig.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.24 är 1 februari 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att identifiera och rapportera antalet resurser med och utan smarta taggar.
* Möjlighet att identifiera och rapportera vilken version av Core Component som används.
* Möjlighet att identifiera och rapportera om typen av källnivå (författare eller publicering) där BPA utfördes.

### Felkorrigeringar {#bug-fixes-bpa}

* Logiken för BPA-storleksändring gjordes snabbare och effektivare.
* I vissa scenarier ökade inte BPA antalet analyserade när det kördes. Den här har åtgärdats.
