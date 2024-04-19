---
title: Visa och hantera renderingar i Experience Manager Assets
description: Läs om hur AEM Assets och Dynamic Media förenklar effektiv bildhantering med statiska och dynamiska bildåtergivningar.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
source-git-commit: 4627eb00ba910d1ad2920db15a87761bd7e4a0c0
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Visa och hantera renderingar i Experience Manager Assets{#renditions}

Återgivningar i Adobe Experience Manager (AEM) är anpassade versioner av digitalt material, till exempel bilder, som utformats för olika enheter och plattformar för att ge optimala prestanda. AEM gör det enklare att skapa och hantera dessa renderingar, vilket förbättrar användarupplevelsen. Du kan skapa miniatyrbilder, optimera bilder för webben eller mobiler, lägga till vattenstämplar, visa och hämta dynamiska renderingar eller smarta beskärningsrenderingar och mycket annat.

Dynamic Media bildförinställningar och renderingar av Smart Crop främjar systematisk bildhantering som är anpassad efter varumärkesstandarder och maximerar varumärkets sammanhållning. Detta gör det enklare att snabbt hitta och använda dynamiska bildåtergivningar utan administratörsåtkomst.

Återgivningar klassificeras som statiska och dynamiska, och varje typ innehåller unika funktioner som beskrivs närmare.

## Statiska återgivningar {#static-renditions}

Statiska återgivningar är förgenererade versioner av digitala resurser, som vanligtvis skapas vid tillgångsintag eller ändring. Dessa renderingar är optimerade för specifika syften och plattformar, som webbminiatyrer, mobilvänliga format för responsiv design eller högupplösta versioner för utskrift, vilket ger en effektiv och enhetlig upplevelse.
Läs [visa och ladda ned](#view-dynamic-renditions) statiska återgivningar i [!DNL Experience Manager Assets].

## Dynamiska renderingar {#dynamic-renditions}

Dynamiska återgivningar är anpassade versioner av resurser som skapats i realtid för att uppfylla specifika behov, som att ändra storlek på bilder baserat på enhetsupplösning eller beskära för att passa olika proportioner.
Med dessa renderingar kan organisationer leverera personaliserade och optimerade upplevelser till olika målgruppsbehov. Du kan visa och hämta dynamiska återgivningar i [!DNL Experience Manager Assets].

### Innan du börjar

* Du måste vara en licensierad AEM Dynamic Media-användare.

* Använd [!UICONTROL Admin view] för att konfigurera:
   * [Profiler för smart beskärning](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md)

  Du kan [växla vy](/help/assets/assets-view-introduction.md#how-to-access-assets-view) senare för att förhandsvisa dynamiska återgivningar i resursvyn.

### Visa och ladda ned dynamiska renderingar {#view-renditions}

Visa eller hämta dynamiska återgivningar av bilder i [!DNL Experience Manager Assets]gör du så här:

1. Gå till **[!UICONTROL Assets Management]** > **[!UICONTROL Assets]**.

1. Navigera till lämplig resursmapp.

1. Klicka på bilden som du vill visa och klicka på **[!UICONTROL Details]**.

1. Klicka på **[!UICONTROL Renditions]**. <br> The **[!UICONTROL Renditions]** öppnas med den tillgängliga panelen **[!UICONTROL Dynamic]** och **[!UICONTROL Smart Crop]** renderingar.

   ![dynamiska återgivningar](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Klicka på den återgivning du behöver för att visa eller hämta.

1. Klicka på ![hämtningsikon](assets/do-not-localize/download-icon.png) -ikonen bredvid den dynamiska återgivning som du behöver ladda ned. <br> Du kan också välja bildåtergivning och klicka på **[!UICONTROL Download Rendition]** längst ned.

   Du kan klicka på ![hämtningsikon](assets/do-not-localize/download-icon.png) ikonen är tillgänglig längst upp på **[!UICONTROL Smart Crop]** återgivningsavsnitt om du vill hämta alla tillgängliga Smart Crop-återgivningar för den resursen.

>[!NOTE]
>
>Dynamiska återgivningar visas bara om resurserna överförs från administrationsvyn.
