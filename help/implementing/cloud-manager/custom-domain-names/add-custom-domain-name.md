---
title: Lägga till ett anpassat domännamn
description: Lägga till ett anpassat domännamn
translation-type: tm+mt
source-git-commit: b6b1ef8f97413dc8bf9b1fa7f355a02bdaeebfd8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Lägga till ett anpassat domännamn {#adding-cdn}

En användare måste vara en Business Owner eller Deployment Manager för att kunna lägga till ett anpassat domännamn i Cloud Manager.

>[!NOTE]
>Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet installeras i ditt program. Mer information finns i Installera ett SSL-certifikat (INSERT LINK).

Det går bara att lägga till ett domännamn åt gången. Användare kan dock lägga till jokertecken, till exempel `*.wknd.com` som ett domännamn, och på så sätt tillåta att flera underdomäner lagras med en enda TXT-post.
Varje Cloud Manager-miljö har plats för upp till 50 anpassade domäner per miljö.
Samma domännamn kan inte användas i mer än en miljö.

## Lägga till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

Följ stegen nedan för att lägga till ett anpassat domännamn från sidan Domäninställningar:

1. Navigera från miljösidan till sidan Domäninställningar.

1. Välj Lägg till eget domännamnDetta startar guiden Lägg till eget domännamn INSERT IMAGE

1. Ange det anpassade domännamnet. Obs! Ta inte med http://&#39;, https://&#39; eller mellanslag när du anger i din domän.

1. Välj den miljö vars publiceringstjänst ska kopplas till domännamnet.

1. Välj SSL-certifikatet i listrutan och välj Fortsätt.

1. Du kommer nu till Verifiering av domännamn för miljöskärmen. Gå till Lägg till TXT-post om du vill veta mer. INFOGA BILD

Följ instruktionerna för att bevisa domänägarskap för din miljö:

1. Välj Fortsätt.
1. CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges med statusen &quot;Verifierad och distribuerad&quot;.  INFOGA BILD
1. Gå till Kontrollera status för anpassat domännamn INSERT LINK om du vill veta mer om olika statusar och hur du adresserar.

>[!NOTE]
>Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Gå till Kontrollera domännamnsstatus INSERT LINK om du vill veta mer.

## Lägga till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

1. Navigera till sidan Miljöinformation om den aktuella miljön.
1. Använd indatafälten högst upp i tabellen Domännamn för att skicka det anpassade domännamnet, SSL-certifikatet. Välj sedan Lägg till.
1. Detta startar guiden Lägg till anpassat domännamn med miljönamnet förifyllt.
1. Ange det anpassade domännamnet. Obs! Ta inte med `http://`, `https://`eller blanksteg i domänen. Välj Fortsätt.
1. Du kommer nu till Verifiering av domännamn för miljöskärmen. Gå till domänverifiering (lägg till TXT-post) om du vill veta mer. INFOGA BILD

Följ instruktionerna för att bevisa domänägarskap för din miljö:

1. Välj Fortsätt.
1. CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges med statusen &quot;Verifierad och distribuerad&quot;.

Nu kan du testa och peka på det anpassade domännamnet. `CNAME` Gå till Domännamnsstatus om du vill veta mer om olika statusar och hur du adresserar.

>[!NOTE]
>Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Gå till Kontrollera domännamnsstatus INSERT LINK om du vill veta mer.
