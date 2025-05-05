---
title: Stöd för miniatyrbilder för videoklipp i Screens as a Cloud Service
description: På den här sidan beskrivs hur du lägger till stöd för miniatyrbilder för videoklipp i Screens as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Stöd för miniatyrbilder för videor {#thumbnail-support-videos}

## Introduktion {#introduction}

Innehållsförfattaren kan definiera en miniatyrbild för videoklipp så att bilden används som platshållare och testar uppspelning och målgruppsanpassning av innehållet medan videon färdigställs av rätt team. Bilden kan också användas om videouppspelningen misslyckas.

Genom att lägga till stöd för en miniatyrbild i videokomponenten kan kunden lägga till en giltig komponent i kanalen, med faktiskt innehåll, och utföra eventuella målinriktningskonfigurationer innan videon levereras.

>[!NOTE]
>Miniatyrbilden spelas upp om den har angetts för videokomponenten om det inte går att spela upp videon i spelaren. Med det här arbetsflödet kan du leverera önskat meddelande till målgruppen (genom att spela upp innehåll) i stället för att helt hoppa över det.

Med stöd för miniatyrbilder kan du göra följande:

* Förbered en kanalupplevelse när videoklippen inte är klara än, eller när du inte nödvändigtvis vill testa en stor resurshämtning på spelarna

* Ange en reservmekanism om det skulle uppstå uppspelningsproblem på enheten.

## Använda miniatyrer i videoklipp {#using-thumbnails}

>[!IMPORTANT]
>**Förutsättningar**
>Innan du lär dig hur du använder miniatyrer för videofilmer bör du kontrollera att du har lärt dig hur du skapar videoåtergivningar för kanaler i Screens as a Cloud Service-projekt. Se [Skapa videoåtergivningar i Screens as a Cloud Service](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md).

Följ stegen nedan för att använda miniatyrbilden i videoklipp:

1. Navigera till en befintlig Screens-kanal eller skapa en kanal.

   >[!NOTE]
   >Mer information om hur du skapar en kanal och lägger till innehåll i en kanal finns i [Skapa och hantera en kanal i Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=sv-SE).

1. Markera kanalen. Klicka på **Redigera** i åtgärdsfältet för att öppna redigeraren.


   ![Redigera-knappen i åtgärdsfältet](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png).

1. Lägg till eller redigera en befintlig videokomponent enligt bilden nedan.

   ![Markerad bild av en videoresurs](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png).

1. Lägg till eller redigera en befintlig videokomponent enligt bilden nedan.

1. Markera videon och klicka på ikonen Konfigurera (*skiftnyckel*) för att öppna videoegenskaperna.

   ![Markerad videoresursbild med en pil som pekar på ikonen Konfigurera, som visas som en skiftnyckel. i verktygsfältet ](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png).

1. Dialogrutan **Video** öppnas där du kan visa släppzonen **Miniatyrbild**.

   ![Dialogrutan Video visar en bild av videomaterialet och miniatyrrutan](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png).

1. Dra och släpp en bild från resursväljaren till släppzonen **Miniatyrbild** och klicka på **Klar**.

   ![Resursbildväljaren visas bakom dialogrutan Video och bildresursen visas i miniatyrrutan](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png).

1. Klicka på **Förhandsgranska**.

1. Om en video är inställd på komponenten spelas videon upp. Om inte, och miniatyrbilden är inställd, spelas miniatyrbilden upp. Annars betraktas komponenten som inte konfigurerad och hoppas över.

## Användningsexempel som stöds vid användning av miniatyrbilder i videoklipp {#understand-use-case}

Miniatyrbilder i videoklipp har stöd för följande användningsområden:

* En videokomponent utan några inställningar hoppas över.

* En videokomponent med bara miniatyrbildsuppsättningen spelar upp miniatyrbilden.

* En videokomponent med både videon (om videon har rätt återgivning) och miniatyruppsättningen spelar upp videon.

* En videokomponent med videouppsättningen spelar upp miniatyrbilden, om det finns ett uppspelningsfel, eller hoppar till nästa objekt om miniatyrbilden inte är konfigurerad.
