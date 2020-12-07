---
title: Lägga till ett anpassat domännamn
description: Lägga till ett anpassat domännamn
translation-type: tm+mt
source-git-commit: 6571c11cedbc0d81fbdfd8072a39b1327bdba10b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Lägga till ett anpassat domännamn {#adding-cdn}

En användare måste vara en Business Owner eller Deployment Manager för att kunna lägga till ett anpassat domännamn i Cloud Manager.

>[!NOTE]
>Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet installeras i ditt program. Mer information finns i Installera ett SSL-certifikat.

Det går bara att lägga till ett domännamn åt gången. Användare kan dock lägga till jokertecken, till exempel `*.wknd.com` som ett domännamn, vilket gör att flera underdomäner kan lagras med en enda TXT-post.
Varje Cloud Manager-miljö har plats för upp till 50 anpassade domäner per miljö.
Samma domännamn kan inte användas i mer än en miljö.

## Lägga till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

Följ stegen nedan för att lägga till ett anpassat domännamn från sidan Domäninställningar:

1. Navigera till sidan Domäninställningar från **miljösidan**

1. Välj **Lägg till anpassat domännamn** för att starta guiden Lägg till anpassat domännamn.

1. Ange det anpassade domännamnet.

   >[!NOTE]
   >Du bör inte inkludera `http://`, `https://` eller mellanslag när du anger i domänen.

1. Välj den miljö vars publiceringstjänst ska kopplas till domännamnet.

1. Välj SSL-certifikatet i listrutan och välj Fortsätt.

1. Du kommer nu till Verifiering av domännamn för miljöskärmen. Mer information finns i Lägga till en TXT-post.

   >[!NOTE]
   >Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö.

1. Välj Fortsätt.
1. CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges med statusen **Verifierad och distribuerad**.
1. Navigera till Kontrollera status för anpassat domännamn om du vill veta mer om olika statusar och hur du ska adressera.

   >[!NOTE]
   >Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i Kontrollera domännamnsstatus.

## Lägga till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

1. Navigera till sidan Miljöinformation om den aktuella miljön.
1. Använd indatafälten högst upp i tabellen Domännamn för att skicka det anpassade domännamnet, SSL-certifikatet. Välj sedan Lägg till.
1. Detta startar guiden Lägg till anpassat domännamn med miljönamnet förifyllt.
1. Ange det anpassade domännamnet. Obs! Ta inte med `http://`, `https://` eller blanksteg när du anger i domänen. Välj Fortsätt.
1. Du kommer nu till Verifiering av domännamn för miljöskärmen. Mer information finns i Domänverifiering (Lägg till TXT-post).

   >[!NOTE]
   >Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö.

1. Välj Fortsätt.
1. CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges med statusen **Verifierad och distribuerad**.

Nu är ditt anpassade domännamn klart för testning och en `CNAME` som pekar på det. Mer information om olika statusar och hur du åtgärdar dem finns i Domännamnsstatus.

>[!NOTE]
>Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i Kontrollera domännamnsstatus.
