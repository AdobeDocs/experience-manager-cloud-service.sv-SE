---
title: Skapa videoåtergivningar på skärmar as a Cloud Service
description: På den här sidan beskrivs hur du skapar videoåtergivningar på skärmar as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Skapa videoåtergivningar på skärmar as a Cloud Service {#creating-screens-video-renditions}

## Introduktion {#introduction}

I det här avsnittet beskrivs hur du skapar videoåtergivningar som används i skärmspelare.

>[!IMPORTANT]
>Stegen som markeras i det här avsnittet måste konfigureras om du tänker använda videoklipp i skärmkanaler.

## Steg för att skapa videoåtergivningar på skärmar as a Cloud Service {#steps-creating-screens-video-renditions}

Följ stegen nedan för att skapa videoåtergivningar på skärmar som är as a Cloud Service från leverantörer av skärminnehåll:

1. Navigera till kanalen i Screens Content Provider.

   >[!NOTE]
   >Se [Använda leverantör av skärminnehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider) för mer information.

1. Klicka på avsnittet Verktyg i det vänstra navigeringsfältet och klicka på **Resurser** och sedan klicka **Bearbetar profiler**.

   ![Klicka på Bearbeta profiler](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Klicka **Skapa** för att skapa en bearbetningsprofil.

   ![Klicka på Skapa](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Ange **Namn**, till exempel **SkärmarBearbetningsprofil**.

   ![Dialogrutan Bearbetar profil med fältet Namn markerat.](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navigera till **Video** så att du kan lägga till en videokodning och sedan klicka på **Lägg till ny**.

   ![Dialogrutan Bearbetar profil med knappen Lägg till ny markerad.](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Ange **Kodningsnamn** till exempel **screens-fullhd** och **Bithastighet** as **2500**.

   ![Bearbetar profildialogrutan med knappen Spara markerad.](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Använd kodningsnamnet som börjar med &quot;screens-&quot;. Endast dessa videoåtergivningar anses spela upp videoupplevelsen på skärmar as a Cloud Service. Ange den bithastighet som fungerar för videoklipp (2 500 kbit/s för video med upplösningen 720 pixlar och 5 000 kbit/s för video med upplösningen 1 080 pixlar).

   >[!NOTE]
   >Du kan lägga till flera videoåtergivningar med olika bredd/höjd/bithastighet för att arbeta med videoklipp. Alla skärmar hämtas återgivningarna av skärmenheterna, även om enheten bara spelar upp videoåtergivning.

1. Klicka **Spara**.

1. Markera bearbetningsprofilen och klicka på **Använd profil för mappar**.

   ![Använd profil i mapp](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Markera de mappar där skärmar-videor finns och klicka på **Använd**.

   ![Klicka på Använd](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* Du kan skapa flera Bearbeta-profiler och använda dem för motsvarande mappar, så att videofilmerna i dessa mappar får de specifika videoåtergivningarna.
   >* När du överför videoklipp till den mapp där en bearbetningsprofil används, bearbetas videoklipp. Konfigurerade återgivningar skapas, som används av skärmenheter för att spela upp videoklipp.
