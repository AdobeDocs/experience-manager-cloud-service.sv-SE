---
title: Versionsinformation för version 2022.4.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2022.4.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Versionsinformation 2022.4.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2022.4.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.4.0) är 5 maj 2022.
Nästa version (2022.5.0) är planerad till 9 juni 2022.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt för april 2022](https://video.tv.adobe.com/v/342612?quality=12) om du vill se en sammanfattning av funktioner som lagts till i version 2022.4.0.

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* Datatyperna för innehållsmodellen kan nu definieras som [översättningsbar](/help/assets/content-fragments/content-fragments-models.md#properties) med en enkel kryssruta i innehållsmodellens redigerare. Dessutom uppdateras AEM översättningsregler och -konfigurationer automatiskt.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Du kan nu [sortera taggar](/help/assets/organize-assets.md#use-tags-to-organize-assets) i taggväljarfönstret i stigande eller fallande ordning baserat på taggnamn, skapandedatum eller ändringsdatum.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **Kommunikation - API:er för dokumenthantering stöds i Forms as a Cloud Service SDK**: [API:er för dokumenthantering](/help/forms/aem-forms-cloud-service-communications.md) hjälper dig att kombinera, ordna om och validera PDF-dokument. Nu kan du använda Communications - Document Generation APIs i en lokal utvecklingsmiljö med hjälp av AEM Forms as a Cloud Service SDK.

* **Använd anpassad XCI för att generera ett postdokument**: Nu kan du [använda en anpassad XCI-fil för att ange olika egenskaper för ett postdokument](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Det åsidosätter huvud-XCI med de anpassade ändringarna. Det ger bättre kontroll över genereringen av arkivhandlingar, ökar möjligheterna till personalisering och anpassning.

* **Använd osynlig CAPTCHA i adaptiv form**: Du kan använda den [osynliga CAPTCHA-kontrollen för att visa CAPTCHA-anropet endast om en misstänkt aktivitet inträffar](/help/forms/captcha-adaptive-forms.md). Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen. Det gör det lättare att bedöma om formulär ska fyllas i av människor utan att det behövs kryssrutor, minska anpassningsarbetet och förbättra slutanvändarens upplevelse.

* **Konfigurationer av formulärdatamodell**: Nu kan du [återanvända formulärdatamodellkonfigurationer i olika miljöer](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), vilket förenklar dataintegreringar och minskar IT-kostnaderna.


## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### SDK Build Analyzers {#sdk-build-analyzers}

AEM as a Cloud Service SDK Build Analyzer Maven Plugin identifierar problem i ett maven-projekt, inklusive saknade beroenden. Det ger utvecklare möjlighet att upptäcka problem under den lokala utvecklingen, långt före distributionen till molnmiljöer med Cloud Manager.

En ny analyserare har nyligen lagts till:

* `content-packages-validation` - validerar för korrekt formaterad innehållssyntax och struktur för paket som installeras under distributionen

Vi rekommenderar starkt att du uppdaterar ditt maven-projekt med den senaste versionen av analyseraren eller inkluderar analyseraren om du inte redan har gjort det. Mer information finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=sv-SE).

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Security {#foundation-security}

### Borttagning av TLS 1.0, 1.1

Från och med den 30 juni 2022 kommer Experience Manager as a Cloud Service att kräva säkrare nätverkskommunikation och datautbyte med användarsystem. AEM avser att enbart använda TLS (Transport Layer Security), 1.2-protokollet. Äldre TLS-versionerna 1.0 och 1.1 är nu inaktuella.

Om du fortsätter att använda äldre versioner av TLS som 1.0, 1.1 kan du förlora åtkomsten till Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
