---
title: Skapa videoåtergivningar för skärmar i skärmar som en Cloud Service
description: På den här sidan beskrivs hur du skapar skärmvideoåtergivningar i skärmar som en Cloud Service.
source-git-commit: 0badd4209b35b4c8cdfa765a08b5d9db749f52b5
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Skapa videoåtergivningar för skärmar i skärmar som en Cloud Service {#creating-screens-video-renditions}

## Introduktion {#introduction}

I den här guiden beskrivs hur du skapar videoåtergivningar som används i skärmspelare.

>[!IMPORTANT]
>Stegen som markeras i det här avsnittet måste konfigureras om du tänker använda videoklipp i skärmkanaler.

## Steg för att skapa skärmar, videoåtergivningar i skärmar som en Cloud Service {#steps-creating-screens-video-renditions}

1. Navigera till kanalen i Screens Content Provider.

   >[!NOTE]
   >Mer information finns i [Använda rasterinnehållsleverantör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider).

1. Klicka på Verktyg i det vänstra navigeringsfältet, klicka på **Resurser** och klicka sedan på **Bearbeta profiler**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Klicka på **Skapa** för att skapa en ny bearbetningsprofil.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Ange **namnet**, till exempel **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navigera till fliken **Video** för att lägga till en videokodning och klicka på **Lägg till ny**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Ange **kodningsnamnet** till exempel , **screens-fullhd** och **bithastigheten** till **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Se till att du använder kodningsnamnet som börjar med &quot;screens-&quot;, så att bara dessa videoåtergivningar räknas som Cloud Service när videoupplevelsen spelas upp på skärmar. Ange den bithastighet som fungerar för videoklipp (2 500 kbit/s för 720 pixlar video och 5 000 kbit/s för 1 080 pixlar).

   >[!NOTE]
   >Du kan lägga till flera videoåtergivningar med olika bredd/höjd/bithastighet för att arbeta med videoklipp. Kom ihåg att alla skärmåtergivningar hämtas av skärmenheterna, även om enheten bara spelar upp videoåtergivning.

1. Klicka på **Spara**.

1. Välj Bearbetningsprofilen och klicka på **Använd profil för mapp(ar)**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Markera mappen/mapparna där skärmar-videor finns och klicka på **Använd**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Du kan skapa flera Bearbeta-profiler och använda dem för motsvarande mappar, så att videofilmerna i dessa mappar får de specifika videoåtergivningarna.
   >* När du överför videofilmer till den mapp där Bearbeta profil används, bearbetas videofilmer och konfigureras återgivningar som sedan används av skärmenheter för att spela upp videofilmerna.


