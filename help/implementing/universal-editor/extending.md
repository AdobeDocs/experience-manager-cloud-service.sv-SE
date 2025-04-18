---
title: Utöka den universella redigeraren
description: Lär dig mer om de olika alternativen för att utöka funktionerna i Universell redigerare så att du kan tillgodose behoven hos dina innehållsförfattare.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0cab4a807be4aa402667feddb6a948f0d2db371f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Utöka den universella redigeraren {#extending}

Lär dig mer om de olika alternativen för att utöka funktionerna i Universell redigerare så att du kan tillgodose behoven hos dina innehållsförfattare.

>[!TIP]
>
>Universal Editor erbjuder även flera [anpassningsalternativ](/help/implementing/universal-editor/customizing.md) som gör att du bättre kan uppfylla dina projektbehov.

## Tillägg {#extensions}

Som en Adobe Experience Cloud-tjänst kan du utöka den universella redigerarens användargränssnitt med App Builder och Experience Manager. Adobe har många färdiga tillägg som du kan använda i ditt projekt.

* **[AEM produktväljare för Universal Editor](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: Integrera Adobe Commerce-data genom att markera eller ta bort produktdata från redigeraren.
* **[Innehållsutkast för Universal Editor](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: Skapa, redigera och hantera flera utkast av innehåll.
* **[Konfigurerbar resursväljare](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: Aktivera val av resurser från andra databaser än den som används av den redigerade sidan.
* **Forms Regelredigerare**: Lägg till dynamiskt beteende i AEM Forms-fält visuellt, utan kodning.
* **[Exportera innehållsfragment till Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: Exportera innehållsfragment som skapats i Adobe Experience Manager as a Cloud Service till Adobe Target för att användas som erbjudanden i Target-aktiviteter för att testa och personalisera upplevelser i stor skala.
* **[Arbetsflöden för innehållsfragment](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: Initiera ett AEM-arbetsflöde för valda innehållsfragment.

## Utöka användargränssnittet {#extending-ui}

UI-tilläggen för Universal Editor är JavaScript-program som skapats med Adobe App Builder. Med samma verktyg kan du också lägga till egna knappar och åtgärder i rubrikmenyn och egenskapspanelen samt skapa egna händelser för den universella redigeraren.

Om du vill utforska möjligheterna att skapa egna tillägg kan du läsa följande resurser:

1. [UI-utökningsbarhet](https://developer.adobe.com/uix/docs/) - Det här är utvecklardokumentationen för UI-tillägg.
1. [Guider för användargränssnittstillägg](https://developer.adobe.com/uix/docs/guides/) - stegvisa instruktioner för hur du utvecklar egna tillägg
1. [Gränssnittstilläggen för Universell redigerare](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Universell redigeringsspecifik tilläggspunktsdokumentation

>[!TIP]
>
>Om du föredrar att lära dig som exempel kan du titta i självstudiekursen [AEM UI extensibility](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Även om den fokuserar på att utöka konsolen för innehållsfragment är begreppen för att implementera ett UI-tillägg i den universella redigeraren desamma.

[Med Extension Manager i AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/) kan du aktivera eller inaktivera tillägg per instans, få åtkomst till Adobe förstahandstillägg, inklusive de för Universal Editor, och mycket annat.

## Tilläggspunkter {#extension-points}

Förutom UI-utbyggbarhet erbjuder den universella redigeraren många andra flexibla tilläggspunkter som möjliggör smidig integrering av anpassade affärskrav.

* **[Block](/help/edge/developer/block-collection.md)**: I enkelt JSON-format kan projekt justera blocken och UE-funktionerna som är tillgängliga för att skapa innehåll.
* **[Anpassat användargränssnitt](#extending-ui)**: Tillägg kan visa nödvändigt gränssnitt i sidopaneler eller modala dialogrutor.
* **[Händelser](/help/implementing/universal-editor/events.md)**: Tillägg tar emot händelser om författarens åtgärder och val på sidan för att svara korrekt.
