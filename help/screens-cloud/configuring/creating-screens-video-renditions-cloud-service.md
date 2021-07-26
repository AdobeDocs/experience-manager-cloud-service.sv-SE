---
title: Skapa videoåtergivningar för skärmar i skärmar som en Cloud Service
description: På den här sidan beskrivs hur du skapar skärmvideoåtergivningar i skärmar som en Cloud Service.
source-git-commit: b8691bb77079eeb7efd141ce89c44c5a312262b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Skapa videoåtergivningar för skärmar i skärmar som en Cloud Service {#creating-screens-video-renditions}

## Introduktion {#introduction}

I den här guiden beskrivs hur du skapar videoåtergivningar som används i skärmspelare.

>[!IMPORTANT]
>Stegen som markeras i det här avsnittet måste konfigureras om du tänker använda videoklipp i skärmkanaler.

## Steg för att skapa skärmar, videoåtergivningar i skärmar som en Cloud Service {#steps-creating-screens-video-renditions}

1. Navigera till kanaler i användargränssnittet i Skärmar Cloud.
1. Klicka på Adobe Experience Manager i det övre vänstra hörnet för att navigera till Skärminnehållsleverantören, d.v.s. AEM som en Cloud Service.
1. Klicka på Verktyg i huvudnavigeringen nu, klicka på Resurser och klicka sedan på Bearbeta profiler

1. Klicka på Skapa för att skapa en ny bearbetningsprofil
1. Ange ett namn som &quot;ScreensProcessingProfile&quot;
1. Navigera till fliken Video för att lägga till en videokodning och klicka på Lägg till ny


   >[!IMPORTANT]
   >Kontrollera att du använder kodningsnamnet som börjar med &quot;screens-&quot;, så att endast dessa videoåtergivningar anses spela upp videoupplevelsen i skärmar som en Cloud Service. Ange den bithastighet som passar dina videofilmer (2 500 kbit/s för 720 pixlar video och 5 000 kbit/s för 1 080 pixlar)

   >[!NOTE]
   >Flera videoåtergivningar kan läggas till med olika bredd/höjd/bithastighet för att passa dina behov, men kom ihåg att alla skärmåtergivningar laddas ned av skärmenheter, även om enheten bara spelar upp videoåtergivning.

1. Klicka på Spara

1. Markera bearbetningsprofilen och klicka på &quot;Använd profil för mapp(ar)&quot;

1. Markera mappen/mapparna där skärmar-videor finns och klicka på Använd

1. Du kan skapa flera Bearbetningsprofiler och använda dem för motsvarande mappar, så att videofilmerna i dessa mappar får de specifika videoåtergivningarna

1. När du överför videofilmer till den mapp där Bearbetningsprofilen används, kommer videofilmer att bearbetas och konfigurerade återgivningar att skapas, som kommer att användas av skärmenheter för att spela upp videofilmer.

