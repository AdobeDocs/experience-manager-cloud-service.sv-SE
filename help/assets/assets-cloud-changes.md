---
title: Betydande förändringar i Adobe Experience Manager Assets som en [!DNL Cloud Service]
description: Betydande förändringar av Adobe Experience Manager Assets i AEM [!DNL Cloud Service] jämfört med Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---


# Nollbara ändringar i Experience Manager Assets som [!DNL Cloud Service] {#notable-changes}

Adobe Experience Manager som [!DNL Cloud Service] har många nya funktioner och möjligheter att hantera dina AEM projekt. Det finns dock många skillnader mellan Experience Manager Assets på plats eller i Adobe Managed Service jämfört med Experience Manager som en [!DNL Cloud Service]. Det här dokumentet belyser de viktiga skillnaderna i Assets-funktioner.

De största skillnaderna jämfört med Experience Manager 6.5 är inom följande områden:

* [Tillgångsintag och överföring](#asset-ingestion).
* [Resursmikrotjänster för molnbaserad bearbetning](#asset-microservices).
* [Borttagning av klassiskt gränssnitt](#classic-ui).

>[!NOTE]
>
>Det här dokumentet markerar de anmärkningsvärda ändringarna av AEM Assets. Mer information om ändringar som gäller för Experience Manager som [!DNL Cloud Service] och andra moduler finns i:
>
>* [En introduktion till Adobe Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md)
>* En [översikt över AEM som a [!DNL Cloud Service] - What is New and What is Different](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/core-concepts/architecture.md) i Adobe Experience Manager as a [!DNL Cloud Service]
>* [Noterbara ändringar i AEM som en [!DNL Cloud Service]  (versionsinformation)](/help/release-notes/aem-cloud-changes.md)
>* [Betydande förändringar av AEM Sites som [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [Adobe Experience Manager som  [!DNL Cloud Service] självstudiekurser](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


## Tillgångsintag och överföring {#asset-ingestion}

Tillgångsuppladdning har optimerats för ökad effektivitet genom bättre skalning av tillgångsintag och snabbare överföringar. Produktfunktionerna (webbanvändargränssnitt, skrivbordsklienter) har uppdaterats. Detta kan dock påverka vissa befintliga anpassningar.

* Experience Manager använder principen om direkt binär åtkomst för överföring och nedladdning samt mikrotjänster för mediefiler för bearbetning. Se [översikt över tillgångsintag](/help/assets/asset-microservices-overview.md).
   * Resursöverföring [med direkt binär åtkomst](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Mer teknisk information finns i [protokollet för direkt binär överföring och API:erna](/help/assets/developer-reference-material-apis.md#upload-binary).
* Standardarbetsflödet **[!UICONTROL DAM Asset Update]** i tidigare versioner av AEM är inte längre tillgängligt. I stället erbjuder mikrotjänsterna en skalbar, lättillgänglig tjänst som täcker det mesta av standardbearbetningen av mediefiler (återgivningar, metadataextrahering, textrahering för indexering).
   * Se [konfigurera och använda objektmikrotjänster](/help/assets/asset-microservices-configure-and-use.md)
   * Om du vill ha anpassade arbetsflödessteg i bearbetningen kan du använda [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).
* Resurser som kommer in via Package Manager kräver manuell ombearbetning med åtgärden **[!UICONTROL Reprocess Asset]** i Assets-gränssnittet.

Standardåtergivningar som genereras med tillgångsmikrotjänster lagras på ett bakåtkompatibelt sätt i resurslagernoderna (samma namnkonventioner).

## Utveckla och testa tillgångsmikrotjänster {#asset-microservices}

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. Resursmikrotjänster hjälper till att undvika behovet av tredjepartsverktyg och -metoder (som ImageMagick) och förenkla konfigurationer, samtidigt som de tillhandahåller färdiga funktioner för vanliga filtyper. Du kan nu bearbeta ett [stort antal filtyper](/help/assets/file-format-support.md) som täcker fler format som är klara att användas än vad som är möjligt med tidigare versioner av Experience Manager. Exempelvis är det nu möjligt att extrahera PSD- och PSB-format med miniatyrbilder som tidigare krävde tredjepartslösningar som ImageMagick. Du kan inte använda de komplexa konfigurationerna för ImageMagick för [!UICONTROL Processing Profiles]-konfigurationen. Använd [!DNL Dynamic Media] för MPEG-omkodning av videofilmer och använd bearbetningsprofiler för [grundläggande omkodning av MP4-videofilmer](/help/assets/manage-video-assets.md#transcode-video).

Resursmikrotjänster är en molnbaserad tjänst som automatiskt tillhandahålls och kopplas till Experience Manager i kundprogram och miljöer som hanteras i Cloud Manager. För att utöka eller anpassa Experience Manager kan utvecklarna använda det befintliga innehållet eller de befintliga resurserna med återgivningar som genererats i en molnmiljö för att testa och validera koden med, visa och hämta resurser.

Om du vill göra en fullständig validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med [pipeline](/help/implementing/cloud-manager/configure-pipeline.md) och testar med fullständig körning av bearbetning av tillgångsmikrotjänster.

## Ta bort det klassiska användargränssnittet {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i Experience Manager som [!DNL Cloud Service]. Standardgränssnittet är det pekaktiverade gränssnittet.
