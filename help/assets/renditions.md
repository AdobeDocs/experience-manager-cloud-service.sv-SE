---
title: Visa och hantera renderingar i Experience Manager Assets
description: Läs om hur AEM Assets och Dynamic Media förenklar effektiv bildhantering med statiska och dynamiska bildåtergivningar.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Visa och hantera renderingar i Experience Manager Assets{#renditions}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Återgivningar i Adobe Experience Manager (AEM) är anpassade versioner av digitalt material, till exempel bilder, som utformats för olika enheter och plattformar för att ge optimala prestanda. AEM gör det enklare att skapa och hantera dessa renderingar, vilket förbättrar användarupplevelsen. Du kan skapa miniatyrbilder, optimera bilder för webben eller mobiler, lägga till vattenstämplar, visa och hämta dynamiska renderingar eller smarta beskärningsrenderingar och mycket annat.

Dynamic Media bildförinställningar och renderingar av Smart Crop främjar systematisk bildhantering som är anpassad efter varumärkesstandarder och maximerar varumärkets sammanhållning. Detta gör det enklare att snabbt hitta och använda dynamiska bildåtergivningar utan administratörsåtkomst.

Återgivningar klassificeras som statiska och dynamiska, och varje typ innehåller unika funktioner som beskrivs närmare.

## Statiska återgivningar {#static-renditions}

Statiska återgivningar är förgenererade versioner av digitala resurser, som vanligtvis skapas vid tillgångsintag eller ändring. Dessa renderingar är optimerade för specifika syften och plattformar, som webbminiatyrer, mobilvänliga format för responsiv design eller högupplösta versioner för utskrift, vilket ger en effektiv och enhetlig upplevelse.
Lär dig [hur du visar och hämtar ](#view-dynamic-renditions) statiska återgivningar i [!DNL Experience Manager Assets].

## Dynamiska renderingar {#dynamic-renditions}

Dynamiska återgivningar är anpassade versioner av resurser som skapats i realtid för att uppfylla specifika behov, som att ändra storlek på bilder baserat på enhetsupplösning eller beskära för att passa olika proportioner.
Med dessa renderingar kan organisationer leverera personaliserade och optimerade upplevelser till olika målgruppsbehov. Du kan visa och hämta dynamiska återgivningar i [!DNL Experience Manager Assets].

### Innan du börjar

* Du måste vara en licensierad AEM Dynamic Media-användare.

* Använd [!UICONTROL Admin view] för att konfigurera:
   * [Profiler för smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md)

  Du kan [växla vyn](/help/assets/assets-view-introduction.md#how-to-access-assets-view) senare för att förhandsgranska dynamiska återgivningar i vyn Assets.

### Visa och ladda ned dynamiska renderingar {#view-renditions}

Så här visar eller hämtar du dynamiska återgivningar av bilder i [!DNL Experience Manager Assets]:

1. Gå till **[!UICONTROL Assets Management]** > **[!UICONTROL Assets]**.

1. Navigera till lämplig resursmapp.

1. Klicka på bilden som du vill visa och klicka på **[!UICONTROL Details]**.

1. Klicka på **[!UICONTROL Renditions]** på den högra menyn. <br> Panelen **[!UICONTROL Renditions]** öppnas med de tillgängliga renderingarna **[!UICONTROL Dynamic]** och **[!UICONTROL Smart Crop]**.

   ![dynamiska återgivningar](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Klicka på den återgivning du behöver för att visa eller hämta.

1. Klicka på ikonen ![Hämta ](assets/do-not-localize/download-icon.png) bredvid den dynamiska återgivning som du behöver hämta. <br> Du kan också välja bildåtergivningen och klicka på alternativet **[!UICONTROL Download Rendition]** längst ned.

   Du kan klicka på ikonen ![Hämta ](assets/do-not-localize/download-icon.png) som finns längst upp i avsnittet **[!UICONTROL Smart Crop]** återgivningar om du vill hämta alla tillgängliga Smart Crop-återgivningar för resursen.

>[!NOTE]
>
>Dynamiska återgivningar visas bara om resurserna överförs från administrationsvyn.
