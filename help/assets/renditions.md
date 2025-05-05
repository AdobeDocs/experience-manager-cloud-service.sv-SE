---
title: Visa och hantera renderingar i Experience Manager Assets
description: Läs om hur AEM Assets och Dynamic Media förenklar effektiv bildhantering med statiska och dynamiska bildåtergivningar.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# Visa och hantera renderingar i Experience Manager Assets{#renditions}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Återgivningar i Adobe Experience Manager (AEM) är anpassade versioner av digitalt material, till exempel bilder, som utformats för olika enheter och plattformar för att ge optimala prestanda. AEM underlättar framtagning och hantering av dessa renderingar, vilket förbättrar användarupplevelsen. Du kan skapa miniatyrbilder, optimera bilder för webben eller mobiler, lägga till vattenstämplar, visa och hämta dynamiska renderingar eller renderingar med Smart Crop och mycket annat.

Dynamic Media-förinställningar och Smart Crop-renderingar främjar systematisk bildhantering som är anpassad efter varumärkesstandarder och maximerar varumärkets sammanhållning. Detta gör det enklare att snabbt hitta och använda dynamiska bildåtergivningar utan administratörsåtkomst.

Återgivningar klassificeras som statiska och dynamiska, och varje typ innehåller unika funktioner som beskrivs närmare.

## Statiska återgivningar {#static-renditions}

Statiska återgivningar är förgenererade versioner av digitala resurser, som vanligtvis skapas vid tillgångsintag eller ändring. Dessa renderingar är optimerade för specifika syften och plattformar, som webbminiatyrer, mobilvänliga format för responsiv design eller högupplösta versioner för utskrift, vilket ger en effektiv och enhetlig upplevelse.
Lär dig hur du [visar och hämtar statiska återgivningar](#view-and-download-static-renditions) i Experience Manager Assets.

### Visa och hämta statiska återgivningar{#view-and-download-static-renditions}

Följ de här stegen för att visa resursåtergivningarna och hämta dem:

1. I Assets-vyn klickar du på **Assets**, navigerar till en mapp, väljer en resurs och klickar på **Information**.
1. Klicka på återgivningens ikon som finns i den högra rutan.
1. Markera en återgivning om du vill förhandsgranska den och klicka på ![hämtningsikonen](/help/assets/assets/download-icon.svg) för att hämta den.

   ![Visa och hämta dynamiska återgivningar](/help/assets/assets/view-download-static-rendition.png)

## Dynamiska renderingar {#dynamic-renditions}

Dynamiska återgivningar är anpassade versioner av resurser som skapats i realtid för att uppfylla specifika behov, som att ändra storlek på bilder baserat på enhetsupplösning eller beskära för att passa olika proportioner.
Med dessa renderingar kan organisationer leverera personaliserade och optimerade upplevelser till olika målgruppsbehov. Du kan visa och hämta dynamiska återgivningar i Experience Manager Assets.

## Dynamiska medierenderingar {#dynamic-media-renditions}

### Innan du börjar

* Du måste ha licens för AEM Dynamic Media.
* Använd [!UICONTROL Admin view] för att konfigurera:
   * [Profiler för smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md)

  Du kan [växla vyn](/help/assets/assets-view-introduction.md#how-to-access-assets-view) senare för att förhandsgranska dynamiska återgivningar i vyn Assets.
* Publicera material på Dynamic Media för att göra Dynamic Media-renderingar tillgängliga i Assets-vyn. Mer information finns i [Publicera Assets till AEM och Dynamic Media](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm).


### Visa och hämta dynamiska medierenderingar {#view-download-dm-renditions}

Så här visar eller hämtar du dynamiska återgivningar av bilder i Experience Manager Assets:

1. Gå till **[!UICONTROL Assets Management]** > **[!UICONTROL Assets]**.

1. Navigera till lämplig resursmapp.

1. Klicka på resursen som du vill visa och klicka på **[!UICONTROL Details]**.

1. Klicka på ikonen **[!UICONTROL Dynamic Media]** på den högra menyn. Panelen **[!UICONTROL Dynamic Media]** visar återgivningar av Dynamic Media och Smart Crop.

   ![dynamiska återgivningar](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Markera återgivningen som ska förhandsgranskas och klicka på **Kopiera URL** för att kopiera URL:en för den valda återgivningen. Klicka på **Hämta återgivning** för att hämta återgivningar av bildresurser.
1. Markera återgivningen för smart beskärning om du vill förhandsgranska och klicka på **Kopiera URL** om du vill kopiera URL-adressen för den valda återgivningen.
1. Klicka på ikonen ![Hämta](assets/do-not-localize/download-icon.png) om du vill hämta alla tillgängliga Smart Crop-återgivningar som en zip-fil.
   ![hämtningsikon](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >Dessa återgivningar är bara tillgängliga för bildresurser.

## Dynamic Media med OpenAPI Capabilities renditions {#dm-with-openapi-renditions}

### Innan du börjar

* Du måste ha licens för AEM Dynamic Media.
* Assets måste godkännas för visning av Dynamic Media med OpenAPI-funktioner. Mer information finns i [Godkänn resurser i Experience Manager](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* Dynamiska media med OpenAPI-funktioner måste vara aktiverade på din AEM as a Cloud Service-instans.

### Visa Dynamic Media med OpenAPI-funktioner {#view-download-dm-with-openapi-renditions}

1. Markera resursen och klicka på **Information**.
1. Klicka på ikonen Dynamic Media som finns i den högra rutan. Panelen Dynamiska media visar återgivningen av Dynamic Media med OpenAPI-funktioner för alla resurstyper.
   ![hämtningsikon](/help/assets/assets/dm-with-open-api-copy-url.png)
1. Välj alternativet **Dynamiska media med OpenAPI** och klicka sedan på **Kopiera URL** för att kopiera resursens leverans-URL.


