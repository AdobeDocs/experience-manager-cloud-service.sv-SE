---
title: Betydande ändringar i [!DNL Adobe Experience Manager Assets] som [!DNL Cloud Service]
description: Betydande ändringar i [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] som [!DNL Cloud Service] jämfört med [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 1%

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

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. Resursmikrotjänster hjälper till att undvika behovet av återgivningsverktyg och -metoder från tredje part (som [!DNL ImageMagick]) och förenkla konfigurationer, samtidigt som du får färdiga funktioner för vanliga filtyper. Du kan nu bearbeta en [många olika filtyper](/help/assets/file-format-support.md) som täcker fler format som är färdiga än vad som är möjligt med tidigare versioner av Experience Manager. Exempelvis kan miniatyrbildsextrahering av PSD- och PSB-format nu förekomma om det tidigare krävdes tredjepartslösningar som [!DNL ImageMagick]. Du kan inte använda de komplexa konfigurationerna i [!DNL ImageMagick] för [!UICONTROL Processing Profiles] konfiguration. Använd [!DNL Dynamic Media] för avancerad MPEG-omkodning av videor och använd bearbetningsprofiler för [grundläggande omkodning av MP4-videor](/help/assets/manage-video-assets.md#transcode-video).

Resursmikrotjänster är en molnbaserad tjänst som automatiskt tillhandahålls och kopplas till [!DNL Experience Manager] i kundprogram och miljöer som hanteras i Cloud Manager. Utöka eller anpassa [!DNL Experience Manager]kan utvecklarna använda befintligt innehåll eller befintliga resurser med återgivningar som genererats i en molnmiljö för att testa och validera koden med, visa och hämta resurser.

Om du vill göra en komplett validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med [pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) och testa med ett fullständigt genomförande av behandlingen av inventariemärkningstjänster.

## Paritet med [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] som [!DNL Cloud Service] innehåller många nya funktioner och fler prestandaförbättringar för befintliga funktioner. När du går från [!DNL Experience Manager] 6,5 till [!DNL Experience Manager] som [!DNL Cloud Service]kan du lägga märke till att vissa funktioner antingen fungerar annorlunda, inte är tillgängliga eller är delvis tillgängliga. Nedan följer en lista över sådana funktioner. Se även [borttagna och borttagna funktioner](/help/release-notes/deprecated-removed-features.md).

| Funktion eller användningsfall | Status i [!DNL Experience Manager] som [!DNL Cloud Service] | Kommentarer |
|-----|-----|-----|
| [Identifiering av duplicerade resurser](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Fungerar annorlunda | Se [hur det fungerade [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [För FPO-återgivningar (Placement Only)](/help/assets/configure-fpo-renditions.md) | Fungerar annorlunda | Vid bearbetning av profiler används objektmikrotjänster för att generera FPO-återgivningar. I Experience Manager 6.5, en tredjepartslösning som [!DNL ImageMagick] var tillgänglig för att generera återgivningarna. |
| Återskrivning av metadata | Fungerar annorlunda | Inaktiverad som standard. Aktivera motsvarande startprogram för arbetsflödet om det behövs. Återskrivning hanteras av resursmikrotjänster. |
| Bearbetning av resurser som överförts med hjälp av Package Manager | Kräver manuell åtgärd | Bearbeta manuellt med **[!UICONTROL Reprocess Asset]** åtgärd. |
| MIME-typidentifiering | Stöds inte. | Om du överför en digital resurs utan ett tillägg eller med ett felaktigt tillägg kanske den inte bearbetas som du vill. Användarna kan fortfarande lagra de binära filerna utan filtillägg i DAM. Se [MIME-typidentifiering i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generering av deltillgångar för sammansatta tillgångar | Stöds inte. | Beroende användningsfall som kommentarer kanske inte uppfylls. Se [skapa underresurser i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). Förhandsgranskning av vissa filtyper i PDF är tillgänglig från [2021.7.0-utgåvan](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Redigera bilder | Stöds inte | Det går inte att redigera resurser på Experience Manager-as a Cloud Service. Se [hur det fungerade i Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Startsida | Stöds inte | Se [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extrahera resurser från ZIP-arkiv | Stöds inte | Se [ZIP-extrahering i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Värderingar av tillgångar | Stöds inte | Värderingswidgeten i metadataramedigeraren stöds inte. |
| filtret Innehållsdisposition | Stöds inte | Ett vanligt användningsexempel `ContentDispositionFilter` ska låta administratörer konfigurera [!DNL Experience Manager] för att skicka HTML-filer och öppna PDF i stället för att ladda ned dem. På Publish-instanserna kan du hantera dispositionen med Dispatcher-konfigurationen. På författarinstanserna rekommenderar Adobe inte att du ändrar Content Disposition-huvudet. Se [Innehållsdispositionsfilter i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| Produktfotografimall | Stöds inte | Se [produktfotofotografimall i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Smart översättning | Stöds inte | [Smart översättning](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) stöds inte i [!DNL Experience Manager] som [!DNL Cloud Service]. |
| WebDAV | Stöds inte | Information om alternativ finns i [[!DNL Creative Cloud] integration](/help/assets/aem-cc-integration-best-practices.md) eller [Referensmaterial för utvecklare](/help/assets/developer-reference-material-apis.md). |
| Klassiskt användargränssnitt | Stöds inte | Endast det Touch-aktiverade användargränssnittet är tillgängligt. |

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

>[!MORELIKETHIS]
>
>Följande resurser är tillgängliga för [!DNL Experience Manager] som [!DNL Cloud Service]:
>
>* [Lista över borttagna och borttagna funktioner](/help/release-notes/deprecated-removed-features.md)
>* [En introduktion](/help/overview/introduction.md)
>* [Vad är nytt och annorlunda?](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/overview/architecture.md)
>* [Betydande ändringar](/help/release-notes/aem-cloud-changes.md)
>* [Betydande ändringar [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Videosjälvstudiekurser](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

