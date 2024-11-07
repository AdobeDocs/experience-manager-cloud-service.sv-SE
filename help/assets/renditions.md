---
title: Visa och hantera renderingar i Experience Manager Assets
description: Läs om hur AEM Assets och Dynamic Media förenklar effektiv bildhantering med statiska och dynamiska bildåtergivningar.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: a3a6456dec178c36c9fe8acfb6f98915fc86e490
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Visa och hantera renderingar i Experience Manager Assets{#renditions}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Återgivningar i Adobe Experience Manager (AEM) är anpassade versioner av digitalt material, till exempel bilder, som utformats för olika enheter och plattformar för att ge optimala prestanda. AEM gör det enklare att skapa och hantera dessa renderingar, vilket förbättrar användarupplevelsen. Du kan skapa miniatyrbilder, optimera bilder för webben eller mobiler, lägga till vattenstämplar, visa och hämta dynamiska renderingar eller renderingar med Smart Crop och mycket annat.

Dynamic Media bildförinställningar och renderingar av Smart Crop främjar systematisk bildhantering som är anpassad efter varumärkesstandarder och maximerar varumärkets sammanhållning. Detta gör det enklare att snabbt hitta och använda dynamiska bildåtergivningar utan administratörsåtkomst.

Återgivningar klassificeras som statiska och dynamiska, och varje typ innehåller unika funktioner som beskrivs närmare.

## Statiska återgivningar {#static-renditions}

Statiska återgivningar är förgenererade versioner av digitala resurser, som vanligtvis skapas vid tillgångsintag eller ändring. Dessa renderingar är optimerade för specifika syften och plattformar, som webbminiatyrer, mobilvänliga format för responsiv design eller högupplösta versioner för utskrift, vilket ger en effektiv och enhetlig upplevelse.
Lär dig [hur du visar och hämtar ](#view-dynamic-renditions) statiska återgivningar i [!DNL Experience Manager Assets].

## Dynamiska renderingar {#dynamic-renditions}

Dynamiska återgivningar är anpassade versioner av resurser som skapats i realtid för att uppfylla specifika behov, som att ändra storlek på bilder baserat på enhetsupplösning eller beskära för att passa olika proportioner.
Med dessa renderingar kan organisationer leverera personaliserade och optimerade upplevelser till olika målgruppsbehov. Du kan visa och hämta dynamiska återgivningar i [!DNL Experience Manager Assets].

## Dynamic Media renderingar {#dynamic-media-renditions}

### Innan du börjar

* Du måste vara en licensierad AEM Dynamic Media-användare.
* Använd [!UICONTROL Admin view] för att konfigurera:
   * [Profiler för smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md)

  Du kan [växla vyn](/help/assets/assets-view-introduction.md#how-to-access-assets-view) senare för att förhandsgranska dynamiska återgivningar i vyn Assets.
* Publish-material till Dynamic Media för att göra Dynamic Media-renderingar tillgängliga i Assets-vyn. Mer information finns i [Publish Assets till AEM och Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm).


### Visa och ladda ned Dynamic Media-renderingar {#view-download-dm-renditions}

Så här visar eller hämtar du dynamiska återgivningar av bilder i Experience Manager Assets:

1. Gå till **[!UICONTROL Assets Management]** > **[!UICONTROL Assets]**.

1. Navigera till lämplig resursmapp.

1. Klicka på resursen som du vill visa och klicka på **[!UICONTROL Details]**.

1. Klicka på ikonen **[!UICONTROL Dynamic Media]** på den högra menyn. På panelen **[!UICONTROL Dynamic Media]** visas återgivningar för Dynamic Media och Smart Crop.

   ![dynamiska återgivningar](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Markera återgivningen som ska förhandsgranskas och klicka på **Kopiera URL** för att kopiera URL:en för den valda återgivningen. Klicka på **Hämta återgivning** för att hämta återgivningar av bildresurser.
1. Markera återgivningen för smart beskärning om du vill förhandsgranska och klicka på **Kopiera URL** om du vill kopiera URL-adressen för den valda återgivningen.
1. Klicka på ikonen ![Hämta](assets/do-not-localize/download-icon.png) om du vill hämta alla tillgängliga Smart Crop-återgivningar som en zip-fil.
   ![hämtningsikon](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >Dessa återgivningar är bara tillgängliga för bildresurser.

## Dynamic Media med OpenAPI Capabilities-renderingar {#dm-with-openapi-renditions}

### Innan du börjar

* Du måste vara en licensierad AEM Dynamic Media-användare.
* Assets måste godkännas för visning av Dynamic Media med OpenAPI-funktionsåtergivningar. Mer information finns i [Godkänn resurser i Experience Manager](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* Dynamic Media med OpenAPI-funktioner måste aktiveras på din AEM as a Cloud Service-instans.

### Visa Dynamic Media med OpenAPI Capabilities-renderingar {#view-download-dm-with-openapi-renditions}

1. Markera resursen och klicka på **Information**.
1. Klicka på ikonen Dynamic Media som finns i den högra rutan. På panelen Dynamic Media visas Dynamic Media med OpenAPI-funktioner för alla resurstyper.
   ![hämtningsikon](/help/assets/assets/dm-with-open-api-copy-url.png)
1. Välj alternativet **Dynamic Media med OpenAPI** och klicka sedan på **Kopiera URL** för att kopiera resursens leverans-URL.


