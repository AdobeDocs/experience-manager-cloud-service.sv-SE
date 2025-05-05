---
title: Skapa videoåtergivningar i Screens as a Cloud Service
description: På den här sidan beskrivs hur du skapar videoåtergivningar i Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Skapa videoåtergivningar i Screens as a Cloud Service {#creating-screens-video-renditions}

## Introduktion {#introduction}

I det här avsnittet beskrivs hur du skapar videoåtergivningar som används i Screens-spelare.

>[!IMPORTANT]
>Stegen som markeras i det här avsnittet måste konfigureras om du tänker använda videofilmer i Screens-kanaler.

## Steg för att skapa videoåtergivningar i Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Följ stegen nedan för att skapa videoåtergivningar i Screens as a Cloud Service från Screens Content Provider:

1. Navigera till kanalen i Screens Content Provider.

   >[!NOTE]
   >Mer information finns i [Använda Screens Content Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=sv-SE#screens-content-provider).

1. Klicka på Verktyg i det vänstra navigeringsfältet, klicka på **Assets** och sedan på **Bearbeta profiler**.

   ![Klicka på Bearbeta profiler](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Klicka på **Skapa** för att skapa en bearbetningsprofil.

   ![Klicka på Skapa](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Ange **Namn**, till exempel **ScreensProcessingProfile**.

   ![Dialogrutan Bearbetar profil med namnfältet markerat.](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navigera till fliken **Video** så att du kan lägga till en videokodning och klicka sedan på **Lägg till ny**.

   ![Dialogrutan Bearbetar profil med knappen Lägg till ny markerad.](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Ange **kodningsnamnet**, till exempel , **screens-fullhd** och **bithastighet** som **2500**.

   ![Dialogrutan Bearbetar profil med knappen Spara markerad.](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Använd kodningsnamnet som börjar med &quot;screens-&quot;. Endast dessa videoåtergivningar anses spela upp videoupplevelsen i Screens as a Cloud Service. Ange den bithastighet som fungerar för videoklipp (2 500 kbit/s för video med upplösningen 720 pixlar och 5 000 kbit/s för video med upplösningen 1 080 pixlar).

   >[!NOTE]
   >Du kan lägga till flera videoåtergivningar med olika bredd/höjd/bithastighet för att arbeta med videoklipp. Alla skärmar hämtas återgivningarna av Screens-enheterna, även om enheten bara spelar upp videoåtergivning.

1. Klicka på **Spara**.

1. Välj bearbetningsprofilen och klicka på **Använd profil för mappar**.

   ![Använd profil i mapp](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Markera de mappar där Screens-videofilmer sparas och klicka på **Använd**.

   ![Klicka på Använd](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* Du kan skapa flera Bearbeta-profiler och använda dem för motsvarande mappar, så att videofilmerna i dessa mappar får de specifika videoåtergivningarna.
   >* När du överför videoklipp till den mapp där en bearbetningsprofil används, bearbetas videoklipp. Konfigurerade återgivningar skapas, som används av Screens-enheter för att spela upp videofilmer.
