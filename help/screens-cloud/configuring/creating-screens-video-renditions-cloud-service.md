---
title: Skapa videoåtergivningar på skärmar as a Cloud Service
description: På den här sidan beskrivs hur du skapar videoåtergivningar på skärmar as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '341'
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
   >Se [Använda leverantör av skärminnehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) för mer information.

1. Klicka på verktygsavsnittet i det vänstra navigeringsfältet och klicka på **Resurser** och klicka sedan på **Bearbetar profiler**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Klicka på **Skapa** för att skapa en ny bearbetningsprofil.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Ange **Namn**, till exempel **SkärmarBearbetningsprofil**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navigera till **Video** för att lägga till videokodning och klicka på **Lägg till ny**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Ange **Kodningsnamn** som **screens-fullhd** och **Bithastighet** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Kontrollera att du använder kodningsnamnet som börjar med &quot;screens-&quot;, så att bara dessa videoåtergivningar anses spela upp videoupplevelsen på skärmar as a Cloud Service. Ange den bithastighet som fungerar för videoklipp (2 500 kbit/s för 720 pixlar video och 5 000 kbit/s för 1 080 pixlar).

   >[!NOTE]
   >Du kan lägga till flera videoåtergivningar med olika bredd/höjd/bithastighet för att arbeta med videoklipp. Alla skärmar hämtas återgivningarna av skärmenheterna, även om enheten bara spelar upp videoåtergivning.

1. Klicka på **Spara**.

1. Välj Bearbetningsprofil och klicka på **Använd profil för mapp(ar)**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Markera mappen/mapparna där skärmar-videor finns och klicka på **Använd**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Du kan skapa flera Bearbeta-profiler och använda dem för motsvarande mappar, så att videofilmerna i dessa mappar får de specifika videoåtergivningarna.
   >* När du överför videofilmer till den mapp där Bearbeta profil används, bearbetas videofilmer och konfigureras återgivningar som sedan används av skärmenheter för att spela upp videofilmerna.
