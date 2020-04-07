---
title: Betydande förändringar i Adobe Experience Manager Assets som en molntjänst
description: Betydande ändringar av Adobe Experience Manager Assets i AEM Cloud-tjänsten jämfört med Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager som molntjänst innehåller många nya funktioner och möjligheter för att hantera dina AEM-projekt. Det finns dock många skillnader mellan Experience Manager Assets på plats eller i Adobe Managed Service jämfört med Experience Manager som en molntjänst. Det här dokumentet visar de viktiga skillnaderna.

>[!NOTE]
>
>Det här dokumentet markerar de betydande ändringar som är specifika för Experience Manager Assets som en molntjänst. Se de allmänna [ändringarna av Experience Manager som en molntjänst](/help/release-notes/aem-cloud-changes.md).

De största skillnaderna jämfört med Experience Manager 6.5 är inom följande områden:

* [Tillgångsintag](#asset-ingestion)
* [Borttagning av Classic UI](#classic-ui)

## Tillgångsintag {#asset-ingestion}

Tillgångsuppladdning har optimerats för ökad effektivitet genom bättre skalning av tillgångsintag och snabbare överföringar. Produktfunktionerna (webbanvändargränssnitt, skrivbordsklienter) har uppdaterats. Detta kan dock påverka vissa befintliga anpassningar.

* I Experience Manager används principen om direkt binär åtkomst för överföring och hämtning och mikrotjänster för mediefiler för bearbetning. Se [översikt över tillgångsintag](/help/assets/asset-microservices-overview.md).
   * Tillgångsuppladdning [med direkt binär åtkomst](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Mer teknisk information finns i avsnittet om [direkt binär överföring av protokoll och API:er](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* Standardarbetsflödet **[!UICONTROL DAM-resursuppdatering]** i tidigare versioner av AEM är inte längre tillgängligt. I stället erbjuder mikrotjänsterna en skalbar, lättillgänglig tjänst som täcker det mesta av standardbearbetningen av mediefiler (återgivningar, metadataextrahering, textrahering för indexering).
   * Se [konfigurera och använda asset microservices](/help/assets/asset-microservices-configure-and-use.md)
   * Om du vill ha anpassade arbetsflödessteg i bearbetningen kan du använda [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) .
* Resurser som kommer in via Package Manager kräver manuell ombearbetning med åtgärden **[!UICONTROL Återbearbeta resurs]** i Assets-gränssnittet.

Standardåtergivningar som genereras med tillgångsmikrotjänster lagras på ett bakåtkompatibelt sätt i resurslagernoderna (samma namnkonventioner).

## Utveckla och testa mikrotjänster {#developing-testing-asset-microservices}

Resursmikrotjänster är en inbyggd molntjänst som automatiskt tillhandahålls och kopplas till Experience Manager i kundprogram och miljöer som hanteras i Cloud Manager. Utvecklare som arbetar med att utöka eller anpassa Experience Manager kan använda befintligt innehåll (eller resurser med återgivningar som genererats i en molnmiljö) för att testa och validera sin kod med, visa och hämta resurser.

Om du vill göra en komplett validering av koden och processen, inklusive tillgångsinmatning och bearbetning, distribuerar du kodändringarna till en molnmiljö med hjälp av pipeline och testar med fullständig körning av bearbetning av tillgångsmikrotjänster.

## Borttagning av Classic UI {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i Experience Manager som molntjänst.
