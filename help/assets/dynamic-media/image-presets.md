---
title: Använd förinställningar för dynamiska mediabilder
description: Lär dig hur du använder bildförinställningar i Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: ad21b52e-594f-4421-9b5a-2382d032ec5a
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# Använd förinställningar för dynamiska mediabilder {#applying-image-presets}

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

Med bildförinställningar kan resurser dynamiskt leverera bilder i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt. Du kan välja en förinställning när du exporterar för att formatera om bilder till specifikationer som administratören har angett.

Du kan dessutom välja en bildförinställning som är responsiv (anges av knappen **[!UICONTROL RESS]** när du har markerat den).

[Administratörer kan skapa och konfigurera bildförinställningar](managing-image-presets.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar. Den använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart bildbehandling](imaging-faq.md).

Du kan använda en bildförinställning på en bild när du vill förhandsvisa den.

**Så här använder du förinställningar för dynamiska mediabilder:**

1. Öppna resursen och markera listrutan i den vänstra listen och välj sedan **[!UICONTROL Renditions]**.

   >[!NOTE]
   >
   >* Statiska återgivningar visas i den övre halvan av rutan. Dynamiska återgivningar visas i den nedre halvan. Om du bara använder dynamiska återgivningar kan du använda URL-adressen för att visa bilden. Knappen **[!UICONTROL URL]** visas bara om du väljer en dynamisk återgivning. Knappen **[!UICONTROL RESS]** visas bara om du väljer en responsiv bildförinställning.
   >
   >* Systemet visar flera återgivningar när du väljer **[!UICONTROL Renditions]** i detaljvyn för en resurs. Du kan öka antalet förinställningar som visas. Se [Öka antalet bildförinställningar som visas](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Gör något av följande:

   * Om du vill förhandsgranska bildförinställningen väljer du en dynamisk återgivning.
   * Om du vill visa popup-fönstret väljer du **[!UICONTROL URL]**, **[!UICONTROL Embed]** eller **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Om resursen *och* inte har publicerats än är knappen **[!UICONTROL URL]** (eller URL- och RESS-knapparna, om tillämpligt) inte tillgänglig.
   >
   >Observera också att bildförinställningar automatiskt publiceras på en Dynamic Media S7-server.
