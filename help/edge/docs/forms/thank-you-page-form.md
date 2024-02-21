---
title: Konfigurera tacksida för EDS Forms
description: Konfigurera tacksida för EDS Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 1%

---


# Konfigurera omdirigeringar av formulärblock

Du kan konfigurera formulärblocket så att det dirigeras om till en annan sida på webbplatsen i stället för till standardsidan&quot;Tack&quot;. Konfigurera en annan sida som omdirigeringsmål

1. Öppna `[EDS Project]/blocks/form/form.js` fil för redigering.

   ![kod för tacknod](/help/edge/assets/change-thankyou-node.png)

1. Ändra `thankyou` noden på följande rad till valfri nod:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Exempel:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > Se till att en dokumentsida med samma namn skapas i projektmappen Edge Delivery Service på Microsoft SharePoint eller Google Sheets, om den inte redan har skapats.


1. Gå till incheckningen av den uppdaterade mappen form.js och dess underliggande filer i Edge Delivery Service-projektet på GitHub. Uppdateringen ser till att formuläret nu dirigeras om till den uppdaterade noden som angetts.
