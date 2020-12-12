---
title: Lägga till ett anpassat domännamn
description: Lägga till ett anpassat domännamn
translation-type: tm+mt
source-git-commit: 3d60af3da62a8a5c8cb62a4e79452bc7675b1878
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---


# Lägga till ett anpassat domännamn {#adding-cdn}

En användare måste vara en Business Owner eller Deployment Manager för att kunna lägga till ett anpassat domännamn i Cloud Manager.

## Viktiga överväganden {#important-considerations}

* Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet installeras i ditt program. Mer information finns i [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

* Det går bara att lägga till ett domännamn åt gången. Domäner kan dock inte innehålla jokertecken. Anpassade domäner på författarsidan stöds inte.

* Varje Cloud Manager-miljö har plats för upp till 100 anpassade domäner per miljö.

* Samma domännamn kan inte användas i mer än en miljö.

## Lägga till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

Följ stegen nedan för att lägga till ett anpassat domännamn från sidan Domäninställningar:

1. Navigera till **Miljöer** från sidan **Översikt**.

1. Klicka på **Domäninställningar** på den vänstra navigeringsmenyn.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på knappen **Lägg till domän** för att öppna dialogrutan **Lägg till domännamn**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. Ange det anpassade domännamnet i **Domännamn**.

   >[!NOTE]
   >Du bör inte inkludera `http://`, `https://` eller mellanslag när du anger i domänen.

1. Välj den **miljö** vars publiceringstjänst ska kopplas till domännamnet.

1. Välj **Domän-SSL-certifikat** i listrutan och välj **Fortsätt**.

1. **Dialogrutan Lägg till** domännamn visas. Du kommer nu till Verifiering av domännamn för miljöskärmen. Mer information finns i [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö.

1. Klicka på **Skapa**.
1. CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges med statusen **Verifierad och distribuerad**.
Navigera till [Kontrollera status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill veta mer om olika statusar och hur du adresserar.

   >[!NOTE]
   >Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i Kontrollera domännamnsstatus.

## Lägga till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

1. Navigera till miljöinformationssidan för att se om miljön är av intresse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Använd indatafälten högst upp i tabellen Domännamn för att skicka det anpassade domännamnet och välj SSL-certifikatet i listrutan. Klicka på **+ Lägg till**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Markera fälten i dialogrutan **Lägg till domännamn** och klicka på **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Ta inte med `http://`, `https://` eller blanksteg när du anger i domänen.

1. Domännamnsverifiering för din miljöskärm visas.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Mer information finns i [Domänverifiering](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md). Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö.

1. Klicka på **Skapa**.

1. Distributionen av det anpassade domännamnet kräver ett giltigt SSL-certifikat och en lyckad TXT-verifiering. Detta anges med statusen **Verifierad och distribuerad**.

Nu är ditt anpassade domännamn klart för testning och en `CNAME` som pekar på det. Läs [Domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill veta mer om olika statusar och hur du åtgärdar dem.

>[!NOTE]
>Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i Kontrollera domännamnsstatus.
