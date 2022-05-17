---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 4fce645a436f820181fd3f0b98c1826e2e1b7195
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

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

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.4.0) är 5 maj 2022.
Nästa version (2022.5.0) är planerad till 2 juni 2022.

## Släpp video {#release-video}

Ta en titt på [Versionsöversikt april 2022](https://video.tv.adobe.com/v/342612?quality=12) video med en sammanfattning av funktioner som lagts till i version 2022.4.0.

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* Datatyperna för innehållsmodellen kan nu definieras som [översättningsbar](/help/assets/content-fragments/content-fragments-models.md#properties) med en enkel kryssruta i innehållsmodellens redigerare. Dessutom uppdateras AEM översättningsregler och -konfigurationer automatiskt.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Nu kan du [sortera taggar](/help/assets/organize-assets.md#use-tags-to-organize-assets) i taggväljarfönstret i stigande eller fallande ordning baserat på taggnamn, skapandedatum eller ändringsdatum.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **Kommunikation - Stöd för API:er för dokumenthantering i Forms as a Cloud Service SDK**: [API:er för dokumenthantering](/help/forms/aem-forms-cloud-service-communications.md) kan du kombinera, ordna om och validera PDF-dokument. Nu kan du använda Communications - Document Generation APIs i en lokal utvecklingsmiljö med hjälp av AEM Forms as a Cloud Service SDK.

* **Använd anpassad XCI för att generera ett postdokument**: Nu kan du [använda en anpassad XCI-fil för att ange olika egenskaper för ett postdokument](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Den åsidosätter det överordnad XCI med de anpassade ändringarna. Det ger bättre kontroll över genereringen av arkivhandlingar, ökar möjligheterna till personalisering och anpassning.

* **Använd osynlig CAPTCHA i ett adaptivt formulär**: Du kan använda [osynlig CAPTCHA för att visa CAPTCHA-utmaning endast vid misstänkt aktivitet](/help/forms/captcha-adaptive-forms.md). Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen. Det gör det lättare att bedöma om formulär ska fyllas i av människor utan att det behövs kryssrutor, minska anpassningsarbetet och förbättra slutanvändarens upplevelse.

* **Konfigurationer av formulärdatamodell**: Nu kan du [återanvänd formulärdatamodellskonfigurationer i olika miljöer](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), förenklar dataintegreringar och minskar IT-kostnaderna.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Snabb åtkomst till produktcockpit: Få enkelt tillgång till detaljerad produktinformation med ett enda klick i Sites Editor

   ![Aktivera önskelista](/help/assets/CIF/enable-wishlist.png)

* Stöd för ytterligare marknadsföringskomponenter: Komponenter kan konfigureras för att visa ett anrop till åtgärd för tillägg i varukorgen och tilläggslistan

   ![Kortkommando för webbplatsredigeraren till produktcockpit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### SDK Build Analyzers {#sdk-build-analyzers}

Den AEM as a Cloud Service SDK Build Analyzer Maven Plugin identifierar problem i ett maven-projekt, inklusive saknade beroenden. Det ger utvecklare möjlighet att upptäcka problem under den lokala utvecklingen, långt före distributionen till molnmiljöer med Cloud Manager.

En ny analyserare har nyligen lagts till:

* `content-packages-validation` - validerar för korrekt formaterad innehållssyntax och struktur för paket som ska installeras under distributionen

Vi rekommenderar starkt att du uppdaterar ditt maven-projekt med den senaste versionen av analyseraren eller inkluderar analyseraren om du inte redan har gjort det. Mer information finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Security {#foundation-security}

### Borttagning av TLS 1.0, 1.1

Från och med den 30 juni 2022 kommer Experience Manager as a Cloud Service att kräva säkrare nätverkskommunikation och datautbyte med användarsystem. AEM använder enbart TLS (Transport Layer Security), 1.2-protokollet. Äldre TLS-versioner 1.0 och 1.1 kommer att bli inaktuella.

Om du fortsätter att använda äldre versioner av TLS som 1.0, 1.1 kan du förlora åtkomsten till Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
