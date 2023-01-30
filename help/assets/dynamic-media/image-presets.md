---
title: Använd Dynamic Media-bildförinställningar
description: Lär dig hur du använder bildförinställningar i Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: ad21b52e-594f-4421-9b5a-2382d032ec5a
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 3%

---

# Använd Dynamic Media-bildförinställningar {#applying-image-presets}

Med bildförinställningar kan resurser dynamiskt leverera bilder i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt. Du kan välja en förinställning när du exporterar för att formatera om bilder till specifikationer som administratören har angett.

Dessutom kan du välja en bildförinställning som är responsiv (anges av **[!UICONTROL RESS]** när du har valt den).

[Administratörer kan skapa och konfigurera bildförinställningar](managing-image-presets.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar. Den använder intelligens under de sista millisekunderna för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](imaging-faq.md) för mer information.

Du kan använda en bildförinställning på en bild när du vill förhandsvisa den.

**Så här använder du Dynamic Media-bildförinställningar:**

1. Öppna resursen och markera listrutan i den vänstra listen och välj sedan **[!UICONTROL Renditions]**.

   >[!NOTE]
   >
   >* Statiska återgivningar visas i den övre halvan av rutan. Dynamiska återgivningar visas i den nedre halvan. Om du bara använder dynamiska återgivningar kan du använda URL-adressen för att visa bilden. The **[!UICONTROL URL]** visas bara om du väljer en dynamisk återgivning. The **[!UICONTROL RESS]** visas bara om du väljer en förinställning för responsiv bild.
   >
   >* Systemet visar flera renderingar när du väljer **[!UICONTROL Renditions]** i en tillgångs detaljvy. Du kan öka antalet förinställningar som visas. Se [Öka antalet bildförinställningar som visas](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Gör något av följande:

   * Om du vill förhandsgranska bildförinställningen väljer du en dynamisk återgivning.
   * Om du vill visa popup-fönstret väljer du **[!UICONTROL URL]**, **[!UICONTROL Embed]**, eller **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Om tillgången *och* bildförinställningen ännu inte publiceras, **[!UICONTROL URL]** (eller URL- och RESS-knapparna, om tillämpligt) är inte tillgängliga.
   >
   >Observera också att bildförinställningar automatiskt publiceras på en Dynamic Media S7-server.
