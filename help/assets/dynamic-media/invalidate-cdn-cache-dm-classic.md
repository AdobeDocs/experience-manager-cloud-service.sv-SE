---
title: Invalidera CDN-cachen med hjälp av Dynamic Media Classic
description: Genom att du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska förfalla.
translation-type: tm+mt
source-git-commit: 8f555f2cf97aaeabfae24919ad5861a2512b0903
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 25%

---


# CDN-cachen har inte verifierats med hjälp av Dynamic Media Classic {#invalidating-your-cdn-cached-content}

CDN cachelagrar medieresurser för snabb leverans. När du uppdaterar en resurs kanske du vill att ändringarna ska börja gälla omedelbart. Genom att du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska förfalla.

>[!IMPORTANT]
>
>Dessa steg gäller endast för Dynamic Media i AEM 6.5, Service Pack 5 eller tidigare. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

Se även [Cacheöversikt i Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Så här gör du CDN-cachen ogiltig med hjälp av Dynamic Media Classic:**

1. Gör något av följande:

   * Logga in på ditt Dynamic Media Classic-konto i webbläsaren:

      [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

      Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

   * Öppna programmet Dynamic Media Classic och logga sedan in på ditt konto.

1. Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**.
1. Gå till textrutan **[!UICONTROL CDN Invalidation Template]** under grupprubriken Servrar på sidan Allmänna inställningar för program.

1. Ange den mall som används för att ogiltigförklara CDN-cachen (Content Delivery Network).

   Anta till exempel att du anger en bild-URL (inklusive bildförinställningar eller modifierare) som refererar till `<ID>`, i stället för ett specifikt bild-ID som i följande exempel:

   `https://server.com/is/image/Company/<ID>?$product$`

   Om mallen bara innehåller `<ID>` fylls Dynamic Media i `https://<server>/is/image` där `<server>` är det publiceringsservernamn som definieras i Allmänna inställningar och &lt;ID> är de resurser som markerats som ogiltiga.

1. I sidans nedre högra hörn klickar du på **[!UICONTROL Close]**.
1. I gränssnittet för Dynamic Media Classic (Scene7) väljer du en eller flera resurser och klickar sedan på **[!UICONTROL File > Invalidate CDN]**. Du ser en lista över en eller flera URL-adresser som genererats från mallen som du skapade och de resurser som du markerade. Den använder den server-URL som anges under &quot;Publicerat servernamn&quot; under Allmänna inställningar för programmet.

   Anta till exempel att du har valt en enda bild med namnet `Backpack_B` när du har angett en mall för CDN-validering i föregående steg. När du klickar på **[!UICONTROL File > Invalidate CDN]** resulterar det i följande genererade URL i användargränssnittet för CDN-validering:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Klicka på **[!UICONTROL Continue]** i listrutan URL för att rensa cachen för varje URL. Observera att du kan redigera en URL-adress eller lägga till en URL-adress genom att skriva eller klistra in den i URL-listrutan. Du behöver inte ställa in CDN Invalidate Template i förväg.

   När du har klickat på **[!UICONTROL Continue]** visas en indikator som ger dig en uppskattning av hur lång tid det tar att rensa cachen.

   Om du har markerat flera resurser och sedan klickar på **[!UICONTROL File > Invalidate CDN]** refererar den sparade **[!UICONTROL Template URL]** till alla dessa resurser. Därför kan du definiera en **[!UICONTROL CDN Invalidate Template]** som refererar till alla URL-bildförinställningar som webbplatsen refererar till (exempelvis produktinformation och sökresultat). När du sedan väljer en eller flera bilder som ska ogiltigförklaras från cachen fylls gränssnittet automatiskt i med URL:erna.

   >[!NOTE]
   >
   >När du markerar resurser och sedan klickar på **[!UICONTROL File > Invalidate CDN]** använder Dynamic Media en mall för att automatiskt skapa URL:er som ska ogiltigförklaras i leveransnätverket (CDN, Content Delivery Network). Om det inte finns något i textrutan **[!UICONTROL CDN Invalidate Template]** visas en tom URL-lista. Cachelagring i leveransnätverket (CDN) är inte resursbaserad utan URL-baserad. Därför är det nödvändigt att känna till de fullständiga URL:erna på webbplatsen. När du har definierat dessa URL:er kan du lägga till dem i textrutan **[!UICONTROL Invalidate CDN Template]** tidigare i stegen. Sedan kan du markera dessa resurser och göra URL:erna ogiltiga i ett enda steg.
   >
   >Ett annat alternativ är att lägga till fullständiga URL:er i **[!UICONTROL Invalidate CDN]**-listan. Om du väljer det här sättet behöver du inte markera resurser i Dynamic Media Classic innan du går till alternativet **[!UICONTROL File > Invalidate CDN]**.

