---
title: Miniatyrbildsstöd för video på skärmar som Cloud Service
description: På den här sidan beskrivs hur du lägger till stöd för miniatyrbilder för videoklipp på skärmar som en Cloud Service.
index: true
source-git-commit: cd06e409ec085fcc77fc7bb466169de3a14dba40
workflow-type: tm+mt
source-wordcount: '455'
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

Följ stegen nedan för att använda miniatyrbilden i videoklipp:

1. Navigera till en befintlig skärmkanal eller skapa en ny kanal.

   >[!NOTE]
   >Mer information om hur du skapar en kanal och lägger till innehåll i en kanal finns i [Skapa och hantera en kanal på skärmar som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Markera kanalen och klicka på **Redigera** i åtgärdsfältet för att öppna redigeraren.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. Lägg till eller redigera en befintlig videokomponent enligt bilden nedan.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. Markera videon och klicka på ikonen *skiftnyckel* för att öppna videoegenskaperna.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. Dialogrutan **Video** öppnas där du kan visa släppzonen **Miniatyrbild**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. Dra och släpp en bild från resursväljaren till släppzonen **Miniatyrbild** och klicka på **Klar**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. Klicka på **Förhandsgranska**.

1. Om en video är inställd på komponenten spelas videon upp. Om inte, och miniatyrbilden är inställd, spelas miniatyrbilden upp. Annars betraktas komponenten som inte konfigurerad och kommer att hoppas över.

## Användningsexempel som stöds vid användning av miniatyrbilder i videoklipp {#understand-use-case}

Miniatyrbilder i videoklipp har stöd för följande användningsområden:

* En videokomponent utan inställningar hoppas över.

* En videokomponent som bara innehåller en miniatyrbilduppsättning spelar upp miniatyrbilden.

* En videokomponent med både videon och miniatyrbilderna inställda spelas upp.

* En videokomponent med videouppsättningen spelar upp miniatyrbilden om det uppstår ett uppspelningsfel, eller hoppar bara till nästa objekt om miniatyrbilden inte är konfigurerad.
