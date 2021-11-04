---
title: Betydande ändringar i [!DNL Adobe Experience Manager Assets] som [!DNL Cloud Service]
description: Betydande ändringar i [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] as compared to [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: e07529f73a3c0b39cb51afb4f3545a9094ce48ef
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# Betydande ändringar i [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] som [!DNL Cloud Service] innehåller många nya funktioner och möjligheter för att hantera dina Experience Manager-projekt. Det finns många skillnader mellan [!DNL Experience Manager Assets] lokal eller värdbaserad som hanterad tjänst från Adobe jämfört med [!DNL Experience Manager] som [!DNL Cloud Service]. I den här artikeln beskrivs de viktigaste skillnaderna för [!DNL Assets] funktioner.

De viktigaste skillnaderna jämfört med [!DNL Experience Manager] 6.5 omfattar följande områden:

* [Intag, överföring och bearbetning av material](#asset-ingestion).
* [Resursmikrotjänster för molnbaserad bearbetning](#asset-microservices).
* [Borttagning av Classic UI](#classic-ui).

## Intag, bearbetning och distribution av material {#asset-ingestion-distribution}

Tillgångsuppladdningen är optimerad för ökad effektivitet genom bättre skalning av intag, snabbare uppladdning, snabbare bearbetning med hjälp av mikrotjänster och bulkinhämtning. Produktfunktionerna (webbanvändargränssnitt, skrivbordsklienter) uppdateras. Detta kan även påverka vissa befintliga anpassningar.

* [!DNL Experience Manager] använder principen om direkt binär åtkomst för att ladda upp och ned resurser och använder tillgångsmikrotjänster för att bearbeta resurser. Se [översikt över mikrotjänster](/help/assets/asset-microservices-overview.md).
   * Överföring av tillgångar [med direkt binär åtkomst](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Mer teknisk information finns i [direkt binärt överföringsprotokoll och API:er](/help/assets/developer-reference-material-apis.md#upload-binary).
   * En jämförelse av tillgängliga API-metoder för grundläggande CRUD-åtgärder finns på [API:er och tillgångsåtgärder](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Standardarbetsflödet **[!UICONTROL DAM Asset Update]** i tidigare versioner av [!DNL Experience Manager] är inte längre tillgängligt. I stället erbjuder mikrotjänsterna en skalbar, lättillgänglig tjänst som täcker det mesta av standardbearbetningen av resurser (återgivningar, metadataextrahering och textextrahering för indexering).
   * Se [konfigurera och använda mikrotjänster för resurser](/help/assets/asset-microservices-configure-and-use.md)
   * Om du vill ha anpassade arbetsflödessteg i bearbetningen [efterbehandlingsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) kan användas.

* Webbplatskomponenterna som levererar en binär fil utan omformning kan använda direkt hämtning. Sling GET-servern uppdateras så att utvecklarna kan göra detta som standard. Webbplatskomponenterna som levererar ett binärformat med viss omformning (till exempel ändrar storlek på det via en server) kan fortsätta fungera som de är.

Standardåtergivningarna som genereras med tillgångsmikrotjänster lagras på ett bakåtkompatibelt sätt i resursdatabasnoderna med samma namnkonventioner.

## Utveckla och testa mikrotjänster {#asset-microservices}

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. Resursmikrotjänster hjälper till att undvika behovet av återgivningsverktyg och -metoder från tredje part (som [!DNL ImageMagick]) och förenkla konfigurationer, samtidigt som du får färdiga funktioner för vanliga filtyper. You can now process a [broad range of file types](/help/assets/file-format-support.md) covering more formats out-of-the-box than what is possible with previous versions of Experience Manager. For example, thumbnail extraction of PSD and PSB formats is now possible that previously required third-party solutions such as [!DNL ImageMagick]. You cannot use the complex configurations of [!DNL ImageMagick] for the [!UICONTROL Processing Profiles] configuration. Use [!DNL Dynamic Media] for advanced FFmpeg transcoding of videos and use processing profiles for [basic transcoding of MP4 videos](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices is a cloud-native service that is automatically provisioned and wired to [!DNL Experience Manager] in customer programs and environments managed in Cloud Manager. Utöka eller anpassa [!DNL Experience Manager]kan utvecklarna använda befintligt innehåll eller befintliga resurser med återgivningar som genererats i en molnmiljö för att testa och validera koden med, visa och hämta resurser.

Om du vill göra en komplett validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med [pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) och testa med ett fullständigt genomförande av behandlingen av inventariemärkningstjänster.

## Feature parity with [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] som [!DNL Cloud Service] innehåller många nya funktioner och fler prestandaförbättringar för befintliga funktioner. När du går från [!DNL Experience Manager] 6,5 till [!DNL Experience Manager] som [!DNL Cloud Service]kan du lägga märke till att vissa funktioner antingen fungerar annorlunda, inte är tillgängliga eller är delvis tillgängliga. The following is a list of such features. In addition, see the [deprecated and removed features](/help/release-notes/deprecated-removed-features.md).

| Funktion eller användningsfall | Status i [!DNL Experience Manager] som [!DNL Cloud Service] | Kommentarer |
|-----|-----|-----|
| [Identifiering av duplicerade resurser](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Fungerar annorlunda. | See [how it worked in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [For Placement Only (FPO) renditions](/help/assets/configure-fpo-renditions.md) | Fungerar annorlunda | Vid bearbetning av profiler används objektmikrotjänster för att generera FPO-återgivningar. I Experience Manager 6.5, en tredjepartslösning som [!DNL ImageMagick] var tillgänglig för att generera återgivningarna. |
| Återskrivning av metadata | Fungerar annorlunda | Disabled by default. Aktivera motsvarande startprogram för arbetsflödet om det behövs. Writeback is handled by asset microservices. |
| Bearbetning av resurser som överförts med hjälp av Package Manager | Needs manual intervention. | Bearbeta manuellt med **[!UICONTROL Reprocess Asset]** åtgärd. |
| MIME-typidentifiering | Stöds inte. | Om du överför en digital resurs utan ett tillägg eller med ett felaktigt tillägg kanske den inte bearbetas som du vill. Användarna kan fortfarande lagra de binära filerna utan filtillägg i DAM. Se [MIME-typidentifiering i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generering av deltillgångar för sammansatta tillgångar | Stöds inte. | Beroende användningsfall som kommentarer kanske inte uppfylls. Se [skapa underresurser i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). PDF preview of some file types is available starting [2021.7.0 release](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Startsida | Stöds inte. | Se [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extrahera resurser från ZIP-arkiv | Stöds inte. | Se [ZIP-extrahering i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Värderingar av tillgångar | Stöds inte. | Värderingswidgeten i metadataramedigeraren stöds inte. |
| filtret Innehållsdisposition | Stöds inte. | Ett vanligt användningsexempel `ContentDispositionFilter` ska låta administratörer konfigurera [!DNL Experience Manager] för att skicka HTML-filer och öppna PDF i stället för att ladda ned dem. På Publish-instanserna kan du hantera dispositionen med Dispatcher-konfigurationen. På författarinstanserna rekommenderar Adobe inte att du ändrar Content Disposition-huvudet. Se [Innehållsdispositionsfilter i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| [Hämta rapport](/help/assets/asset-reports.md) | Stöds inte. | För tillfället är den hämtningsrapport som innehåller information om resursanvändning inte tillgänglig. Se [ladda ned rapport i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html). |
| Product photoshoot template | Stöds inte. | Se [produktfotofotografimall i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Smart översättning | Stöds inte. | [Smart översättning](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) stöds inte i [!DNL Experience Manager] som [!DNL Cloud Service]. |
| WebDAV | Stöds inte. | Information om alternativ finns i [[!DNL Creative Cloud] integration](/help/assets/aem-cc-integration-best-practices.md) eller [Referensmaterial för utvecklare](/help/assets/developer-reference-material-apis.md). |
| Klassiskt användargränssnitt | Stöds inte. | Endast det Touch-aktiverade användargränssnittet är tillgängligt. |

>[!MORELIKETHIS]
>
>Följande resurser är tillgängliga för [!DNL Experience Manager] som [!DNL Cloud Service]:
>
>* [List of deprecated and removed features](/help/release-notes/deprecated-removed-features.md)
>* [En introduktion](/help/overview/introduction.md)
>* [Vad är nytt och annorlunda?](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/overview/architecture.md)
>* [Betydande ändringar](/help/release-notes/aem-cloud-changes.md)
>* [Betydande ändringar [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Videosjälvstudiekurser](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

