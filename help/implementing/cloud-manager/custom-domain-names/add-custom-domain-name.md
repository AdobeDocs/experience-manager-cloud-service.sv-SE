---
title: Lägga till ett anpassat domännamn
description: Lär dig hur du lägger till ett anpassat domännamn med hjälp av Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Lägga till ett anpassat domännamn {#adding-cdn}

Du kan lägga till ett eget domännamn från två platser i Cloud Manager:

* [Från sidan Domäninställningar](#adding-cdn-settings)
* [Från sidan Miljöer](#adding-cdn-environments)

>[!NOTE]
>
>En användare måste ha **Företagsägare** eller **Distributionshanteraren** roll för att lägga till ett anpassat domännamn i Cloud Manager

## Lägga till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

Följ de här stegen för att lägga till ett eget domännamn från **Domäninställningar** sida.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

   ![Fönstret Domäninställningar](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på **Lägg till domän** längst upp till höger för att öppna **Lägg till domännamn** -dialogrutan.

   ![Dialogrutan Lägg till domän](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Ange det anpassade domännamnet i dialogrutan **Domännamn** fält.

   >[!NOTE]
   >
   >Inkludera inte `http://`, `https://`eller blanksteg när du anger i domänen.

1. Välj **Miljö** vars tjänst är associerad med domännamnet.

1. Välj antingen **Publicera** eller **Förhandsgranska** service.

1. Välj **Domän-SSL-certifikat** som är associerat med domännamnet i listrutan och väljer **Fortsätt**.

1. The **Lägg till domännamn** öppnas och du kommer att gå vidare till verifieringsprocessen för domännamnet. Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö. Klicka på **Skapa**.

   ![Verifiering av domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges av statusen **Verifierat och distribuerat**.

Se dokumentet [Kontrollerar status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill veta mer om olika statusar och hur du åtgärdar potentiella problem.

>[!NOTE]
>
>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.
>
>Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Se dokumentet [Kontrollerar status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) för mer information.

>[!TIP]
>
>Se [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) om du vill veta mer om TXT-poster.

## Lägga till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

Följ de här stegen för att lägga till ett eget domännamn från **Miljö** sida.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljödetaljer** sida för den intressanta miljön.

   ![Ange domännamn på sidan Miljöinformation](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Använd **Domännamn** tabell för att skicka det anpassade domännamnet.

   1. Ange det anpassade domännamnet.
   1. Välj SSL-certifikatet som är associerat med det här namnet i listrutan.
   1. Klicka på **+Lägg till**.

   ![Lägg till anpassat domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Kontrollera de värden som är markerade i dialogrutan **Lägg till domännamn** och klicka **Fortsätt**.

   ![Domännamnsfönster](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Inkludera inte `http://`, `https://`eller blanksteg när du anger domännamnet.

1. The **Lägg till domännamn** öppnas och du kommer att gå vidare till verifieringsprocessen för domännamnet. Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö. Klicka på **Skapa**.

   ![Verifiering av domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges av statusen **Verifierat och distribuerat**.

Se dokumentet [Kontrollerar status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill veta mer om olika statusar och hur du åtgärdar potentiella problem.

>[!NOTE]
>
>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.
>
>Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Se dokumentet [Kontrollerar status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) för mer information.

>[!TIP]
>
>Se [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) om du vill veta mer om TXT-poster.
