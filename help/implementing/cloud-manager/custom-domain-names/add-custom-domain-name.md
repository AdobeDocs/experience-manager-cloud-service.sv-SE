---
title: Lägga till ett anpassat domännamn
description: Lär dig hur du lägger till ett anpassat domännamn med Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Lägga till ett anpassat domännamn {#adding-cdn}

Du kan lägga till ett eget domännamn från två platser i Cloud Manager:

* [Från sidan Domäninställningar](#adding-cdn-settings)
* [Från sidan Miljöer](#adding-cdn-environments)

>[!NOTE]
>
>En användare måste ha rollen **Affärsägare** eller **Distributionshanterare** för att kunna lägga till ett anpassat domännamn i Cloud Manager, och du måste använda Snabbt CDN.

## Lägga till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

När du lägger till ett anpassat domännamn hanteras domänen med det mest specifika, giltiga certifikatet. Om flera certifikat har samma domän väljs den senast uppdaterade versionen. Adobe rekommenderar att du hanterar certifikat så att det inte finns några överlappande domäner.

Följ de här stegen för att lägga till ett anpassat domännamn från sidan **Domäninställningar**. De här stegen baseras på Snabb. Om du använder ett annat CDN måste du konfigurera din domän med det CDN som du har valt att använda.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera till fliken **Domäninställningar** i den vänstra navigeringspanelen.

   ![Fönstret Domäninställningar](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på knappen **Lägg till domän** längst upp till höger för att öppna dialogrutan **Lägg till domännamn** .

   ![Dialogrutan Lägg till domän](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Ange det anpassade domännamnet i fältet **Domännamn**.

   >[!NOTE]
   >
   >Inkludera inte `http://`, `https://` eller mellanslag när du anger i din domän.

1. Välj den **miljö** vars tjänst är associerad med domännamnet.

1. Välj tjänsten **Publish** eller **Förhandsgranska**.

1. Välj **Domän-SSL-certifikatet** som är associerat med domännamnet i listrutan och välj **Fortsätt**.

1. Dialogrutan **Lägg till domännamn** visas och kommer att ta dig till verifieringsprocessen för domännamn. Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö. Klicka på **Skapa**.

   ![Verifiering av domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta indikeras av statusen **Verifierad och distribuerad**.

Mer information om olika statusar och hur du åtgärdar potentiella problem finns i [Kontrollera status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!TIP]
>
>Granska följande artikel om behovet av att [lägga till en CNAME eller en post nästa](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) för att undvika dubbelarbete när du lägger till DNS-poster i din anpassade domän. TXT-posten och CNAME- eller A-posten kan anges samtidigt på den styrande DNS-servern.

>[!TIP]
>
>Mer information om TXT-poster finns i [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).

>[!NOTE]
>
>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.
>
>Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i [Kontrollera status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Lägga till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

Följ de här stegen för att lägga till ett anpassat domännamn från sidan **Miljö**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till sidan **Miljöinformation** för att se om miljön är av intresse.

   ![Ange domännamn på sidan Miljöinformation](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Använd tabellen **Domännamn** för att skicka det anpassade domännamnet.

   1. Ange det anpassade domännamnet.
   1. Välj SSL-certifikatet som är associerat med det här namnet i listrutan.
   1. Klicka på **+Lägg till**.

   ![Lägg till anpassat domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Kontrollera de värden som har valts i dialogrutan **Lägg till domännamn** och klicka på **Fortsätt**.

   ![Fönstret Domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Inkludera inte `http://`, `https://` eller mellanslag när du anger i domännamnet.

1. Dialogrutan **Lägg till domännamn** visas och kommer att ta dig till verifieringsprocessen för domännamn. Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö. Klicka på **Skapa**.

   ![Verifiering av domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta indikeras av statusen **Verifierad och distribuerad**.

Mer information om olika statusar och hur du åtgärdar potentiella problem finns i [Kontrollera status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!NOTE]
>
>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.
>
>Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i [Kontrollera status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!TIP]
>
>Mer information om TXT-poster finns i [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
