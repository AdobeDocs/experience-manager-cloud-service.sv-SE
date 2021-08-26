---
title: Miniatyrbildsstöd för video på skärmar som Cloud Service
description: På den här sidan beskrivs hur du lägger till stöd för miniatyrbilder för videoklipp på skärmar som en Cloud Service.
hide: true
index: false
source-git-commit: ea96e811c0164e3cc7d323e734c1617d3c0e9308
workflow-type: tm+mt
source-wordcount: '416'
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

1. Redigera videokomponentens egenskaper.

1. Dra en bild från resursväljaren till släppzonen Miniatyrbilder.

1. Förhandsgranska kanalen.

1. Om en video är inställd på komponenten spelas videon upp. Om inte, och miniatyrbilden är inställd, spelas miniatyrbilden upp. Annars betraktas komponenten som inte konfigurerad och hoppas över

## Användningsexempel som stöds vid användning av miniatyrbilder i videoklipp {#understand-use-case}

Se följande exempel när du använder miniatyrbilder i videor.

En videokomponent med:

* *ingen* inställning kommer att hoppas över

* *bara miniatyrbildsinställningen* spelar upp miniatyrbilden

* *både video- och miniatyrbildsvisning* spelar upp videon

* *videouppsättningen* spelar upp miniatyrbilden om det finns ett uppspelningsfel, eller hoppa till nästa objekt om miniatyrbilden inte är konfigurerad
