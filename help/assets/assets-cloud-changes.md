---
title: Nollbara ändringar i [!DNL Adobe Experience Manager Assets] som en [!DNL Cloud Service]
description: Betydande ändringar av  [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] som a [!DNL Cloud Service] jämfört med  [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User, Leader, Architect, Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 979c4accca8b271ba2ff0ba176985c94b6d469c7
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Nollbara ändringar av [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#notable-changes}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!DNL Adobe Experience Manager] som [!DNL Cloud Service] har många nya funktioner och möjligheter att hantera dina Experience Manager-projekt. Det finns många skillnader mellan [!DNL Experience Manager Assets] lokal eller värdbaserad som hanterad Adobe-tjänst jämfört med [!DNL Experience Manager] som en [!DNL Cloud Service]. I den här artikeln beskrivs de viktiga skillnaderna för [!DNL Assets]-funktioner.

De största skillnaderna jämfört med [!DNL Experience Manager] 6.5 är inom följande områden:

* [Tillgångsinmatning, överföring och bearbetning](#asset-ingestion).
* [Resursmikrotjänster för molnbaserad bearbetning](#asset-microservices).
* [Det klassiska användargränssnittet ](#classic-ui) tas bort.

## Intag, bearbetning och distribution av material {#asset-ingestion-distribution}

Tillgångsuppladdningen är optimerad för ökad effektivitet genom bättre skalning av intag, snabbare uppladdning, snabbare bearbetning med hjälp av mikrotjänster och bulkinhämtning. Produktfunktionerna (webbanvändargränssnitt, skrivbordsklienter) uppdateras. Dessutom kan detta påverka vissa befintliga anpassningar.

* [!DNL Experience Manager] använder principen för direkt binär åtkomst för att överföra och hämta resurser och använder resursmikrotjänster för att bearbeta resurser. Se en [översikt över mikrotjänster](/help/assets/asset-microservices-overview.md).
   * Resursöverföring [ med direkt binär åtkomst](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Mer teknisk information finns i [protokoll för direkt binär överföring och API:er](/help/assets/developer-reference-material-apis.md#upload-binary).
   * En jämförelse av tillgängliga API-metoder för grundläggande CRUD-åtgärder finns i [API:er och tillgångsåtgärder](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Standardarbetsflödet **[!UICONTROL DAM Asset Update]** i tidigare versioner av [!DNL Experience Manager] är inte längre tillgängligt. I stället erbjuder mikrotjänsterna en skalbar, lättillgänglig tjänst som täcker det mesta av standardbearbetningen av resurser (återgivningar, metadataextrahering och textextrahering för indexering).
   * Se [konfigurera och använda resursmikrotjänster](/help/assets/asset-microservices-configure-and-use.md)
   * Om du vill ha anpassade arbetsflödessteg i bearbetningen kan du använda [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).

* Webbplatskomponenterna som levererar en binär fil utan omformning kan använda direkt hämtning. Sling GET-servleten uppdateras som standard för att aktivera den här funktionen. Webbplatskomponenterna som levererar ett binärformat med viss omformning (till exempel ändrar storlek på det via en server) kan fortsätta fungera som de är.

Standardåtergivningarna som genereras med tillgångsmikrotjänster lagras på ett bakåtkompatibelt sätt i resursdatabasnoderna med samma namnkonventioner.

## Utveckla och testa mikrotjänster {#asset-microservices}

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. Resursmikrotjänster hjälper till att undvika behovet av återgivningsverktyg och -metoder från tredje part (som [!DNL ImageMagick]) och förenkla konfigurationer, samtidigt som de tillhandahåller färdiga funktioner för vanliga filtyper. Du kan nu bearbeta ett [brett urval av filtyper](/help/assets/file-format-support.md) som täcker fler format som är klara att användas än vad som är möjligt med tidigare versioner av Experience Manager. Miniatyrbildextrahering av PSD och PSB-format är nu möjligt eftersom tidigare krävda tredjepartslösningar som [!DNL ImageMagick]. Du kan inte använda de komplexa konfigurationerna för [!DNL ImageMagick] för konfigurationen [!UICONTROL Processing Profiles]. Använd [!DNL Dynamic Media] för avancerad MPEG-omkodning av videofilmer och använd bearbetningsprofiler för [grundläggande omkodning av MP4-videofilmer](/help/assets/manage-video-assets.md#transcode-video).

Resursmikrotjänster är en molnbaserad tjänst som automatiskt etableras och ansluts till [!DNL Experience Manager] i kundprogram och miljöer som hanteras i Cloud Manager. För att utöka eller anpassa [!DNL Experience Manager] kan utvecklare använda befintligt innehåll eller befintliga resurser med återgivningar som genererats i en molnmiljö. Detta gör att de kan testa och validera sin kod genom att använda, visa och hämta resurser.

Om du vill göra en fullständig validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med [pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) och testar med fullständig körning av bearbetning av tillgångsmikrotjänster.

## Funktionsparitet med [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] som [!DNL Cloud Service] innehåller många nya funktioner och fler prestandaförbättringar för befintliga funktioner. När du går från [!DNL Experience Manager] 6.5 till [!DNL Experience Manager] som [!DNL Cloud Service] kan du dock märka att vissa funktioner antingen fungerar annorlunda, inte är tillgängliga eller är delvis tillgängliga. Nedan följer en lista över sådana funktioner. Se även de [borttagna och borttagna funktionerna](/help/release-notes/deprecated-removed-features.md).

| Funktion eller användningsfall | Status i [!DNL Experience Manager] som [!DNL Cloud Service] | Kommentar |
|-----|-----|-----|
| [Dubblerad resursidentifiering](/help/assets/detect-duplicate-assets.md) | Detta fungerar annorlunda | Se [hur det fungerade i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/duplicate-detection). |
| [För FPO-återgivningar (Placement Only)](/help/assets/configure-fpo-renditions.md) | Detta fungerar annorlunda | Vid bearbetning av profiler används objektmikrotjänster för att generera FPO-återgivningar. I Experience Manager 6.5 fanns en tredjepartslösning som [!DNL ImageMagick] tillgänglig för att generera renderingarna. |
| Tillbakaskrivning av metadata | Detta fungerar annorlunda | Inaktiverad som standard. Aktivera motsvarande startprogram för arbetsflödet om det behövs. Resursmikrotjänsterna hanterar tillbakaskrivningen. |
| Bearbetning av resurser som överförts med hjälp av Package Manager | Detta kräver manuell åtgärd | Bearbeta manuellt med åtgärden **[!UICONTROL Reprocess Asset]**. |
| MIME-typdetektering | Stöds inte. | Om du överför en digital resurs utan ett tillägg eller med ett felaktigt tillägg kanske den inte bearbetas som du vill. Användarna kan fortfarande lagra de binära filerna utan filnamnstillägg i DAM. Se [MIME-typdetektering i [!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/administer/detect-asset-mime-type-with-tika). |
| Generering av deltillgångar för sammansatta tillgångar | Stöds inte. | Beroende användningsexempel som anteckningar kanske inte uppfylls. Se [Skapa underresurser i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/managing-linked-subassets#generate-subassets). Förhandsgranskning i PDF av vissa filtyper är tillgänglig från och med [2021.7.0-utgåvan](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Redigera bilder | Stöds inte | Det går inte att redigera resurser i Experience Manager as a Cloud Service. Se [hur det fungerade i Experience Manager 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/manage-assets#editing-images). |
| Startsida | Stöds inte | Se [[!DNL Assets] Startsidan i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/using/assets-home-page) |
| Extrahera resurser från ZIP-arkiv | Stöds inte | Se [ZIP-extrahering i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/manage-assets#extractzip). |
| Assets betyg | Stöds inte | Värderingswidgeten i metadataramedigeraren stöds inte. |
| filtret Innehållsdisposition | Stöds inte | Ett vanligt användningsexempel för `ContentDispositionFilter` är att låta administratörer konfigurera [!DNL Experience Manager] så att HTML-filer kan hanteras och PDF-filer öppnas infogat i stället för att de kan hämtas. På publiceringsinstanserna kan du hantera dispositionen med Dispatcher-konfigurationen. I redigeringsinstanserna rekommenderar inte Adobe att du ändrar Content Disposition-huvudet. Se [Filtret Innehållsförskjutning i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/content-disposition-filter). |
| Produktfotografimall | Stöds inte | Se [produktfotofotografimall i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/authoring/projects/managing-product-information). |
| Smart översättning | Stöds inte | Smart översättning stöds inte i [!DNL Experience Manager] som [!DNL Cloud Service]. |
| WebDAV | Stöds inte | Mer information om alternativ finns i [[!DNL Creative Cloud] integration](/help/assets/aem-cc-integration-best-practices.md) eller [referensmaterial för utvecklare](/help/assets/developer-reference-material-apis.md). |
| Klassiskt användargränssnitt | Stöds inte | Endast ett användargränssnitt med pekfunktion är tillgängligt. |

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>Följande resurser är tillgängliga för [!DNL Experience Manager] som [!DNL Cloud Service]:
>
>* [Lista över borttagna och borttagna funktioner](/help/release-notes/deprecated-removed-features.md)
>* [En introduktion](/help/overview/introduction.md)
>* [Vad är nytt och annorlunda?](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/overview/architecture.md)
>* [Antagbara ändringar](/help/release-notes/aem-cloud-changes.md)
>* [Antagbara ändringar [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Videosjälvstudiekurser](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/overview)
