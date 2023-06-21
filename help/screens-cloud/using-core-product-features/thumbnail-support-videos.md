---
title: Stöd för miniatyrbilder för videoklipp på skärmar as a Cloud Service
description: På den här sidan beskrivs hur du lägger till stöd för miniatyrbilder för videoklipp på skärmar as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: cf1e2717342ca4e00780428d6ccf264bd8eca371
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Stöd för miniatyrbilder för videoklipp {#thumbnail-support-videos}

## Introduktion {#introduction}

Innehållsförfattare kan definiera en miniatyrbild för videoklipp så att bilden kan användas som platshållare och testa uppspelning och målgruppsanpassning av innehållet medan videon färdigställs av rätt team. Bilden kan också användas om videouppspelningen misslyckas.

Genom att lägga till stöd för en miniatyrbild i videokomponenten kan kunden lägga till en giltig komponent i kanalen, med faktiskt innehåll, och utföra eventuella målinriktningskonfigurationer innan videon levereras.

>[!NOTE]
>Miniatyrbilden spelas upp om videomponenten är inställd om videouppspelningen misslyckas i spelaren. På så sätt kan du leverera önskat meddelande till målgruppen (genom att spela upp innehåll) i stället för att helt hoppa över det.

Med stöd för miniatyrbilder kan du:

* Förbered en kanalupplevelse när videoklippen inte är klara än, eller när du inte nödvändigtvis vill testa en stor resurshämtning på spelarna

* Ange en reservmekanism om det skulle uppstå uppspelningsproblem på enheten.

## Använda miniatyrer i videoklipp {#using-thumbnails}

>[!IMPORTANT]
>**Förutsättningar**
>Innan du lär dig hur du använder miniatyrbilder för videofilmer bör du lära dig hur du skapar videoåtergivningar för kanaler i as a Cloud Service projekt för skärmar. Se [här](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) för mer information.

Följ stegen nedan för att använda miniatyrbilden i videoklipp:

1. Navigera till en befintlig skärmkanal eller skapa en ny kanal.

   >[!NOTE]
   >Mer information om hur du skapar en kanal och lägger till innehåll i en kanal finns i [Skapa och hantera en kanal på skärmar as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Markera kanalen och klicka på **Redigera** i åtgärdsfältet för att öppna redigeraren.

   ![Öppna redigeraren](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. Lägg till eller redigera en befintlig videokomponent enligt bilden nedan.

   ![Redigera komponenten](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. Markera videon och klicka på *wrench* -ikonen för att öppna videoegenskaperna.

   ![Klicka på växeln](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. The **Video** öppnas där du kan se **Miniatyrbild** släppzon.

   ![Visa miniatyrbilden](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. Dra och släpp en bild från resursväljaren till **Miniatyrbild** släppa zon och klicka på **Klar**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. Klicka på **Förhandsgranska**.

1. Om en video är inställd på komponenten spelas videon upp. Om inte, och miniatyrbilden är inställd, spelas miniatyrbilden upp. Annars betraktas komponenten som inte konfigurerad och hoppas över.

## Användningsexempel som stöds vid användning av miniatyrbilder i videoklipp {#understand-use-case}

Miniatyrbilder i videoklipp har stöd för följande användningsområden:

* En videokomponent som inte har konfigurerats hoppas över.

* En videokomponent som bara innehåller en miniatyrbilduppsättning spelar upp miniatyrbilden.

* En videokomponent med både videon (om videon har rätt återgivning) och en miniatyrbildsuppsättning spelar upp videon.

* En videokomponent med videouppsättningen spelar upp miniatyrbilden om det uppstår ett uppspelningsfel, eller hoppar bara till nästa objekt om miniatyrbilden inte är konfigurerad.
