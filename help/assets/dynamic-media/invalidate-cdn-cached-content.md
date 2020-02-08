---
title: Invaliderar CDN-cachelagrat innehåll
description: Genom att du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Invaliderar CDN-cachelagrat innehåll {#invalidating-your-cdn-cached-content}

CDN cachelagrar medieresurser för snabb leverans. När du uppdaterar en resurs kanske du vill att ändringarna ska börja gälla omedelbart. Genom att du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.

Se även Översikt över [cache i Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Så här gör du ditt CDN-cachelagrade innehåll ogiltigt:**

1. Logga in på ditt konto för Dynamic Media Classic (Scene7):

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Klicka på **[!UICONTROL Inställningar > Programinställningar > Allmänna inställningar]**.
1. Gå till textrutan **[!UICONTROL CDN-valideringsmall]** på sidan Allmänna inställningar i gruppen Servrar.

1. Ange den mall som används för att ogiltigförklara CDN-cachen (Content Delivery Network).

   Anta till exempel att du anger en bild-URL (inklusive bildförinställningar eller modifierare) som refererar `<ID>`i stället för ett specifikt bild-ID, som i följande exempel:

   `https://server.com/is/image/Company/<ID>?$product$`

   Om mallen bara innehåller `<ID>`fylls Dynamic Media i `https://<server>/is/image` där `<server>` är namnet på publiceringsservern som definieras i Allmänna inställningar och &lt;ID> är den eller de mediefiler som markerats för att ogiltigförklaras.

1. Klicka på **[!UICONTROL Stäng]** i sidans nedre högra hörn.
1. I gränssnittet för Dynamic Media Classic (Scene7) markerar du en eller flera resurser och klickar sedan på **[!UICONTROL Arkiv > Invalidera CDN]**. Du ser en lista över en eller flera URL-adresser som genererats från mallen som du skapade och de resurser som du markerade. Den använder den server-URL som anges under &quot;Publicerat servernamn&quot; under Allmänna inställningar för programmet.

   Anta att du har valt en enda bild med namnet `Backpack_B`för bildresursen när du har angett en mall för CDN-validering i föregående steg. När du klickar på **[!UICONTROL Arkiv > Gör CDN]** ogiltig resulterar det i följande genererade URL i användargränssnittet för CDN-validering:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. I listrutan URL klickar du på **[!UICONTROL Fortsätt]** för att rensa cachen för varje URL. Observera att du kan redigera en URL-adress eller lägga till en URL-adress genom att skriva eller klistra in den i URL-listrutan. Du behöver inte ställa in CDN Invalidate Template i förväg.

   När du klickar på **[!UICONTROL Fortsätt]** visas en indikator som ger dig en uppskattning av hur lång tid det tar att rensa cachen.

   Om du har valt flera resurser och sedan klickat på **[!UICONTROL Arkiv > Invalidera CDN]**, refereras varje resurs till i den sparade **[!UICONTROL mallens URL]**. Därför kan du definiera en **[!UICONTROL CDN-mall]** för invalidering som refererar till varje URL-bildförinställning som finns på webbplatsen (t.ex. produktinformation, sökresultat). När du sedan väljer en eller flera bilder som ska ogiltigförklaras från cachen fyller URL-adresserna automatiskt i gränssnittet.

   >[!NOTE]
   >
   >När du markerar resurser och sedan klickar på **[!UICONTROL Arkiv > Invalidera CDN]**, använder Dynamic Media en ogiltig CDN-mall för att automatiskt skapa URL:er som blir ogiltiga i CDN (Content Delivery Network). Om det inte finns något i textrutan **[!UICONTROL CN-mall]** för att validera mall visas en tom URL-lista. Cachelagring vid CDN är inte tillgångsbaserad. det är URL-baserat. Därför är det nödvändigt att du är medveten om de fullständiga URL:er som finns på webbplatsen. När du har identifierat dessa URL:er kan du lägga till dem i textrutan **[!UICONTROL Invalidera CDN-mall]** tidigare i stegen. Sedan kan du markera dessa resurser och göra URL-adresserna ogiltiga i ett enda steg.
   >
   >Ett annat alternativ är att lägga till fullständiga URL:er i listan **[!UICONTROL Ovalidera CDN]** . Om du väljer det här sättet behöver du inte markera resurser i Dynamic Media Classic innan du går till alternativet **[!UICONTROL Arkiv > Invalidera CDN]** .

