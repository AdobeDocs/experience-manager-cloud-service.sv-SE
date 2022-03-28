---
title: Gör cacheminnet för leveransnätverket ogiltigt via Dynamic Media Classic
description: Lär dig hur du ogiltigförklarar det cachelagrade innehållet i CDN (Content Delivery Network) så att du snabbt kan uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: cf7d844acb0158b543d575368e35cd1c2fc72fba
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 13%

---

# Invalidera CDN-cachen med Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Dynamic Media resurser cachas av CDN (Content Delivery Network) för snabb leverans. När du uppdaterar en resurs vill du dock att ändringarna ska börja gälla omedelbart. Om du validerar ditt CDN-cachelagrade innehåll kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Eventuellt annat anpassat CDN stöds inte med den här funktionen.

>[!IMPORTANT]
>
>Dessa steg gäller endast Dynamic Media i Adobe Experience Manager 6.5, Service Pack 5 eller tidigare. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Så här gör du CDN-cachen ogiltig via Dynamic Media Classic:**

1. Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Kontakta kundsupport om du inte har den här informationen.

1. Gå till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]**.
1. På sidan Allmänna inställningar för programmet, under grupprubriken Servrar, hittar du **[!UICONTROL CDN Invalidation Template]** textruta.

1. Ange den mall som används för att ogiltigförklara CDN-cachen (Content Delivery Network).

   Anta att du anger en bild-URL (inklusive bildförinställningar eller modifierare) som refererar till `<ID>`i stället för ett specifikt bild-ID, som i följande exempel:

   `https://server.com/is/image/Company/<ID>?$product$`

   Om mallen bara innehåller `<ID>`fylls sedan Dynamic Media i `https://<server>/is/image` där `<server>` är namnet på den publiceringsserver som definieras i Allmänna inställningar och &lt;id> är de tillgångar som har valts för att ogiltigförklaras.

1. Välj **[!UICONTROL Close]**.
1. I användargränssnittet för Dynamic Media Classic (Scene7) väljer du en eller flera resurser och går sedan till **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**. Du ser en lista över en eller flera URL-adresser som genererats från mallen som du skapade och de resurser som du markerade. Den använder den server-URL som anges under &quot;Publicerat servernamn&quot; under Allmänna inställningar för programmet.

   Anta till exempel att du har valt en enda bild med namnet &quot;Invalidering av CDN&quot; i föregående steg `Backpack_B`. När du går till **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]** resulterar det i följande genererade URL i CDN-valideringsgränssnittet:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. I listrutan URL väljer du **[!UICONTROL Continue]** för att rensa cacheminnet för varje specifik URL. Du kan redigera en URL-adress eller lägga till en URL-adress genom att skriva eller klistra in den i URL-listrutan; Du behöver inte ställa in CDN Invalidate Template i förväg.

   När du har valt **[!UICONTROL Continue]** visas en indikator som ger dig en uppskattning av hur lång tid det tar att rensa cachen.

   Om du har valt flera resurser går du till **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**, refereras varje resurs i den sparade **[!UICONTROL Template URL]**. Därför kan du definiera en **[!UICONTROL CDN Invalidate Template]** referera till varje URL-bildförinställning som refereras på webbplatsen, t.ex. produktinformation och sökresultat. När du sedan väljer en eller flera bilder som ska ogiltigförklaras från cachen fylls gränssnittet automatiskt i med URL:erna.

   >[!NOTE]
   >
   >När du väljer resurser går du till **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]** använder Dynamic Media en ogiltig CDN-mall för att automatiskt skapa URL:er som blir ogiltiga från CDN. Om det inte finns något i textrutan **[!UICONTROL CDN Invalidate Template]** visas en tom URL-lista. Cachelagring i leveransnätverket (CDN) är inte resursbaserad utan URL-baserad. Därför är det nödvändigt att känna till de fullständiga URL:erna på webbplatsen. När du har definierat dessa URL:er kan du lägga till dem i textrutan **[!UICONTROL Invalidate CDN Template]** tidigare i stegen. Sedan kan du markera dessa resurser och göra URL:erna ogiltiga i ett enda steg.
   >
   >Ett annat alternativ är att lägga till fullständiga URL:er i **[!UICONTROL Invalidate CDN]** lista. Om du väljer det här sättet behöver du inte markera resurser i Dynamic Media Classic innan du går till **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]** alternativ.
