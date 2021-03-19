---
title: Leverera optimerade bilder för en responsiv webbplats
description: Lär dig hur du använder funktionen för responsiv kod för att leverera optimerade bilder från Dynamic Media.
feature: Resurshantering
topic: Yrkesverksamma inom affärsverksamhet
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 13%

---


# Leverera optimerade bilder för en responsiv webbplats {#delivering-optimized-images-for-a-responsive-site}

Använd funktionen Responsiv kod när du vill dela koden för responsiv visning med webbutvecklaren. Du kopierar den responsiva (**[!UICONTROL RESS]**) koden till Urklipp så att du kan dela den med webbutvecklaren.

Den här funktionen är användbar om webbplatsen finns på en WCM-fil från tredje part. Om webbplatsen däremot finns på AEM återger en extern bildserver bilden och skickar den till webbsidan.

Se även [Bädda in Video Viewer på en webbsida.](embed-code.md)

Se även [Länka URL:er till ditt webbprogram.](linking-urls-to-yourwebapplication.md)

**Så här levererar du optimerade bilder för en responsiv webbplats**:

1. Navigera till bilden som du vill ange responsiv kod för och tryck på **[!UICONTROL Renditions]** i listrutan.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Välj en responsiv bildförinställning. Knapparna **[!UICONTROL URL]** och **[!UICONTROL RESS]** visas.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >Den valda resursen *och* den valda bildförinställningen eller visningsförinställningen måste publiceras för att knappen **[!UICONTROL URL]** eller **[!UICONTROL RESS]** ska vara tillgänglig.
   >
   >Bildförinställningar publiceras automatiskt.

1. Tryck på **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. I dialogrutan **[!UICONTROL Embed Responsive Image]** markerar och kopierar du den responsiva kodtexten och klistrar in den på din webbplats för att komma åt den responsiva resursen.
1. Redigera standardbrytpunkterna i inbäddningskoden så att de matchar dem för den responsiva webbplatsen direkt i koden. Testa dessutom de olika bildupplösningarna som används vid olika sidbrytpunkter.

## Använda HTTP/2 för att leverera dina Dynamic Media-resurser {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Leverans av Dynamic Media-resurser stöds med HTTP/2 som ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](http2faq.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.
