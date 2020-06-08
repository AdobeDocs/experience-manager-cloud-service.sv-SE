---
title: Betydande förändringar i Adobe Experience Manager Assets som en molntjänst
description: Betydande ändringar av Adobe Experience Manager Assets i AEM Cloud-tjänsten jämfört med Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 37ff6912837ba78c90526e8f8322b9002e9a4304
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager som molntjänst innehåller många nya funktioner och möjligheter för att hantera dina AEM-projekt. Det finns dock många skillnader mellan Experience Manager Assets på plats eller i Adobe Managed Service jämfört med Experience Manager som en molntjänst. Det här dokumentet belyser de viktiga skillnaderna i Assets-funktioner. Andra ändringar finns i de allmänna [ändringarna av Experience Manager som en molntjänst](/help/release-notes/aem-cloud-changes.md).

De största skillnaderna jämfört med Experience Manager 6.5 är inom följande områden:

* [Tillgångsintag och överföring](#asset-ingestion).
* [Resursmikrotjänster för molnbearbetning](#asset-microservices).
* [Borttagning av klassiskt gränssnitt](#classic-ui).

## Tillgångsintag och överföring {#asset-ingestion}

Tillgångsuppladdning har optimerats för ökad effektivitet genom bättre skalning av tillgångsintag och snabbare överföringar. Produktfunktionerna (webbanvändargränssnitt, skrivbordsklienter) har uppdaterats. Detta kan dock påverka vissa befintliga anpassningar.

* I Experience Manager används principen om direkt binär åtkomst för överföring och hämtning och mikrotjänster för mediefiler för bearbetning. Se [översikt över tillgångsintag](/help/assets/asset-microservices-overview.md).
   * Tillgångsuppladdning [med direkt binär åtkomst](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Mer teknisk information finns i avsnittet om [direkt binär överföring av protokoll och API:er](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* Standardarbetsflödet **[!UICONTROL DAM Asset Update]** i tidigare versioner av AEM är inte längre tillgängligt. I stället erbjuder mikrotjänsterna en skalbar, lättillgänglig tjänst som täcker det mesta av standardbearbetningen av mediefiler (återgivningar, metadataextrahering, textrahering för indexering).
   * Se [konfigurera och använda asset microservices](/help/assets/asset-microservices-configure-and-use.md)
   * Om du vill ha anpassade arbetsflödessteg i bearbetningen kan du använda [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) .
* Resurser som kommer in via Package Manager kräver manuell ombearbetning med hjälp av åtgärden **[!UICONTROL Reprocess Asset]** i Assets-gränssnittet.

Standardåtergivningar som genereras med tillgångsmikrotjänster lagras på ett bakåtkompatibelt sätt i resurslagernoderna (samma namnkonventioner).

## Utveckla och testa mikrotjänster {#asset-microservices}

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. Resursmikrotjänster hjälper till att undvika behovet av tredjepartsverktyg och -metoder (som ImageMagick) och förenkla konfigurationer, samtidigt som de tillhandahåller färdiga funktioner för vanliga filtyper. Du kan nu bearbeta en [mängd olika filtyper](/help/assets/file-format-support.md) som omfattar fler färdiga format än vad som är möjligt med tidigare versioner av Experience Manager. Exempelvis är det nu möjligt att extrahera PSD- och PSB-format med miniatyrbilder som tidigare krävde tredjepartslösningar som ImageMagick. Du kan inte använda de komplexa konfigurationerna för ImageMagick för [!UICONTROL Processing Profiles] konfigurationen. Använd även [!DNL Dynamic Media] för MPEG-omkodning av videofilmer.

Resursmikrotjänster är en molnbaserad tjänst som automatiskt tillhandahålls och kopplas till Experience Manager i kundprogram och miljöer som hanteras i Cloud Manager. För att utöka eller anpassa Experience Manager kan utvecklarna använda befintligt innehåll eller befintliga resurser med återgivningar som genereras i en molnmiljö för att testa och validera koden med, visa och hämta resurser.

Om du vill göra en komplett validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med hjälp [av pipeline](/help/implementing/cloud-manager/configure-pipeline.md) och testar med fullständig körning av bearbetning av tillgångsmikrotjänster.

## Borttagning av Classic UI {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i Experience Manager som molntjänst. Standardgränssnittet är det pekaktiverade gränssnittet.
