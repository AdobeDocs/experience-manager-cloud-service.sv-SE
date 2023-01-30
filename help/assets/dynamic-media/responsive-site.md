---
title: Leverera optimerade bilder för en responsiv webbplats
description: Lär dig hur du använder funktionen för responsiv kod för att leverera optimerade bilder från Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 11%

---

# Leverera optimerade bilder för en responsiv webbplats {#delivering-optimized-images-for-a-responsive-site}

Använd funktionen Responsiv kod när du vill dela koden för responsiv visning med webbutvecklaren. Du kopierar det responsiva (**[!UICONTROL RESS]**) till Urklipp så att du kan dela det med webbutvecklaren.

Den här funktionen är användbar om webbplatsen finns på en WCM-fil från tredje part. Om webbplatsen däremot finns på Adobe Experience Manager återger en extern bildserver bilden och skickar den till webbsidan.

Se även [Bädda in Video Viewer på en webbsida](embed-code.md).

Se även [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

**Så här levererar du optimerade bilder för en responsiv webbplats:**

1. Navigera till bilden som du vill ange responsiv kod för och välj i listrutan **[!UICONTROL Renditions]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Välj en responsiv bildförinställning. Knapparna **[!UICONTROL URL]** och **[!UICONTROL RESS]** visas.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >Den valda resursen *och* den valda bildförinställningen eller visningsförinställningen måste publiceras för att knappen **[!UICONTROL URL]** eller **[!UICONTROL RESS]** ska vara tillgänglig.
   >
   >Bildförinställningar publiceras automatiskt.

1. Välj **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. I **[!UICONTROL Embed Responsive Image]** markerar och kopierar den responsiva kodtexten och klistrar in den på din webbplats för att få tillgång till den responsiva resursen.
1. Redigera standardbrytpunkterna i den inbäddade koden så att de matchar det som finns på den responsiva webbplatsen, direkt i koden. Testa dessutom de olika bildupplösningarna som används vid olika sidbrytpunkter.

## Använda HTTP/2 för att leverera dina Dynamic Media-resurser {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Leverans av Dynamic Media-resurser stöds med HTTP/2 som ger bättre respons och laddningstider.

Se [HTTP2-leverans av innehåll](http2faq.md) om du vill ha fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.
