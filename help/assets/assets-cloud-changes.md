---
title: Noterbara ändringar i [!DNL Adobe Experience Manager Assets] som a [!DNL Cloud Service]
description: Betydande ändringar av [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] jämfört med [!DNL Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: db08a4365d264383cc143727e423ac9886bed66c
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---


# Nollbara ändringar i [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] som en  [!DNL Cloud Service] innehåller många nya funktioner och möjligheter för att hantera dina Experience Manager-projekt. Det finns många skillnader mellan [!DNL Experience Manager Assets] lokal eller värdbaserad som hanterad tjänst i Adobe jämfört med [!DNL Experience Manager] som en [!DNL Cloud Service]. I den här artikeln beskrivs de viktiga skillnaderna för [!DNL Assets]-funktioner.

De största skillnaderna jämfört med [Experience Manager] 6.5 är i följande områden:

* [Intag, överföring och bearbetning](#asset-ingestion) av resurser.
* [Resursmikrotjänster för molnbaserad bearbetning](#asset-microservices).
* [Borttagning av klassiskt gränssnitt](#classic-ui).

## Tillgångsintag och -bearbetning {#asset-ingestion}

Tillgångsuppladdningen är optimerad för ökad effektivitet genom bättre skalning av intag, snabbare uppladdning, snabbare bearbetning med hjälp av mikrotjänster och bulkinhämtning. Produktfunktionerna (webbanvändargränssnitt, skrivbordsklienter) uppdateras. Detta kan även påverka vissa befintliga anpassningar.

* [!DNL Experience Manager] använder principen om direkt binär åtkomst för att ladda upp och ned resurser och använder tillgångsmikrotjänster för att bearbeta resurser. Se [översikt över mikrotjänster](/help/assets/asset-microservices-overview.md).
   * Resursöverföring [med direkt binär åtkomst](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Mer teknisk information finns i [protokoll för direkt binär överföring och API:er](/help/assets/developer-reference-material-apis.md#upload-binary).
   * En jämförelse av tillgängliga API-metoder för grundläggande CRUD-åtgärder finns i [API:er och tillgångsåtgärder](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Standardarbetsflödet **[!UICONTROL DAM Asset Update]** i tidigare versioner av [!DNL Experience Manager] är inte längre tillgängligt. I stället erbjuder mikrotjänsterna en skalbar, lättillgänglig tjänst som täcker det mesta av standardbearbetningen av resurser (återgivningar, metadataextrahering och textextrahering för indexering).
   * Se [konfigurera och använda tillgångsmikrotjänster](/help/assets/asset-microservices-configure-and-use.md)
   * Om du vill ha anpassade arbetsflödessteg i bearbetningen kan du använda [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).
* Återskrivning av metadata stöds inte. Se [metadatatillbakaskrivning i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html).
* Resurser som överförs med Package Manager kräver manuell ombearbetning med **[!UICONTROL Reprocess Asset]**-åtgärden i [!DNL Assets]-användargränssnittet.
* [!DNL Assets] identifierar inte automatiskt MIME-typen för överförda resurser. En digital resurs utan ett tillägg eller med ett felaktigt tillägg bearbetas inte som du vill. När du till exempel överför sådana resurser händer ingenting eller så kan en felaktig bearbetningsprofil gälla för resursen. Användarna kan fortfarande lagra de binära filerna utan filtillägg i DAM. Se [MIME-typdetektering i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html).
* [!DNL Experience Manager] som a  [!DNL Cloud Service] inte genererar delresurser för sammansatta resurser. Se [Skapa delresurser i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets).
* [!DNL Assets] Startsidan är inte tillgänglig. Se [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html).
* Dubblerad tillgångsidentifiering fungerar annorlunda jämfört med [hur den fungerade i [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html).
* För FPO-återgivningar (placement only) genereras olika jämfört med tidigare [!DNL Experience Manager]-versioner. Se [FPO-återgivning för [!DNL Experience Manager] som en [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html).

Standardåtergivningar som genereras med tillgångsmikrotjänster lagras på ett bakåtkompatibelt sätt i resursdatabasnoderna med samma namnkonventioner.

## Utveckla och testa tillgångsmikrotjänster {#asset-microservices}

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. Resursmikrotjänster hjälper till att undvika behovet av tredjepartsverktyg och -metoder (som ImageMagick) och förenkla konfigurationer, samtidigt som de tillhandahåller färdiga funktioner för vanliga filtyper. Du kan nu bearbeta ett [stort antal filtyper](/help/assets/file-format-support.md) som täcker fler format som är klara att användas än vad som är möjligt med tidigare versioner av Experience Manager. Exempelvis är det nu möjligt att extrahera PSD- och PSB-format med miniatyrbilder som tidigare krävde tredjepartslösningar som ImageMagick. Du kan inte använda de komplexa konfigurationerna för ImageMagick för [!UICONTROL Processing Profiles]-konfigurationen. Använd [!DNL Dynamic Media] för avancerad MPEG-omkodning av videofilmer och använd bearbetningsprofiler för [grundläggande omkodning av MP4-videofilmer](/help/assets/manage-video-assets.md#transcode-video).

Resursmikrotjänster är en molnbaserad tjänst som automatiskt tillhandahålls och kopplas till [!DNL Experience Manager] i kundprogram och miljöer som hanteras i Cloud Manager. För att utöka eller anpassa [!DNL Experience Manager] kan utvecklarna använda befintligt innehåll eller befintliga resurser med återgivningar som genereras i en molnmiljö för att testa och validera koden med, visa och hämta resurser.

Om du vill göra en fullständig validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med [pipeline](/help/implementing/cloud-manager/configure-pipeline.md) och testar med fullständig körning av bearbetning av tillgångsmikrotjänster.

## Ta bort det klassiska användargränssnittet {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i [!DNL Experience Manager] som [!DNL Cloud Service]. Endast det pekaktiverade användargränssnittet är tillgängligt.

>[!MORELIKETHIS]
>
>Följande resurser är tillgängliga för [!DNL Experience Manager] som [!DNL Cloud Service]:
>
>* [En introduktion](/help/overview/introduction.md)
>* [Vad är nytt och annorlunda?](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/core-concepts/architecture.md)
>* [Betydande ändringar](/help/release-notes/aem-cloud-changes.md)
>* [Betydande ändringar [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Videosjälvstudiekurser](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

