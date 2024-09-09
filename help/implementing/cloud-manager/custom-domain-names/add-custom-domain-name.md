---
title: Lägg till ett anpassat domännamn
description: Lär dig hur du lägger till ett anpassat domännamn med Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---


# Lägg till ett anpassat domännamn {#adding-cdn}

Lär dig hur du lägger till ett anpassat domännamn med Cloud Manager.

## Krav {#requirements}

Uppfyll dessa krav innan du lägger till ett anpassat domännamn i Cloud Manager.

* Du måste ha lagt till ett SSL-domäncertifikat för domänen som du vill lägga till innan du lägger till ett anpassat domännamn enligt beskrivningen i dokumentet [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Du måste ha rollen **Affärsägare** eller **Distributionshanterare** för att lägga till ett anpassat domännamn i Cloud Manager.
* Använd det snabba nätverket för CDN.

## Var ska jag lägga till egna domännamn? {#where}

Du kan lägga till ett eget domännamn från två platser i Cloud Manager:

* [Från sidan Domäninställningar](#adding-cdn-settings)
* [Från sidan Miljöer](#adding-cdn-environments)

När du lägger till ett anpassat domännamn hanteras domänen med det mest specifika, giltiga certifikatet. Om flera certifikat har samma domän väljs den senast uppdaterade versionen. Adobe rekommenderar att du hanterar certifikat så att det inte finns några överlappande domäner.

Stegen som beskrivs i det här dokumentet är baserade på Fast. Om du har använt ett annat CDN konfigurerar du din domän med det CDN som du har valt att använda.

## Lägg till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

Följ de här stegen för att lägga till ett anpassat domännamn från sidan **Domäninställningar**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera till fliken **Domäninställningar** i den vänstra navigeringspanelen.

   ![Fönstret Domäninställningar](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på knappen **Lägg till domän** längst upp till höger för att öppna dialogrutan **Lägg till domännamn** .

   ![Dialogrutan Lägg till domän](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. På fliken **Domännamn** anger du det anpassade domännamnet i fältet **Domännamn**.

   >[!NOTE]
   >
   >Inkludera inte `http://`, `https://` eller mellanslag när du anger i din domän.

1. Välj den **miljö** vars tjänst är associerad med domännamnet.

1. Välj tjänsten **Publish** eller **Förhandsgranska**.

1. Välj **Domän-SSL-certifikatet** som är associerat med domännamnet i listrutan och välj **Fortsätt**.

1. Fliken **Verifiering** visas.

   ![Verifiering av domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * Fliken **Verifiering** beskriver nästa steg för att konfigurera ditt anpassade domännamn, som skapar en nödvändig TXT-post.
   * Du kan utföra det här steget direkt (innan du klickar på **Skapa** i dialogrutan) eller efter att du klickar på **Skapa** i dialogrutan.
   * Alternativen och nästa steg beskrivs nedan.

1. Klicka på **Skapa** för att spara det anpassade domännamnet i Cloud Manager.

När du väljer **Skapa** i guiden **Lägg till anpassad domän** utlöser Cloud Manager en TXT-verifiering. Skapa TXT-posten när du konfigurerar det anpassade domännamnet i Cloud Manager. Det här steget är dock inte nödvändigt. För efterföljande verifieringar måste du aktivt välja ikonen **Verifiera igen** bredvid statusen.

Namnet är inte aktivt förrän Cloud Manager har verifierat att TXT-posten har lagts till och verifierats. Statusen **Verifierad och distribuerad** indikerar en lyckad TXT-verifiering.

* Mer information om TXT-poster finns i [Lägg till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
* Mer information om hur Cloud Manager verifierar det anpassade domännamnet och dess TXT-post finns i [Kontrollera domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Nästa steg {#next-steps}

När du har skapat ditt anpassade domännamn i Cloud Manager lägger du till en TXT-post för att verifiera domänens ägarskap. Fortsätt till dokumentet [Lägger till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) om du vill fortsätta konfigurera ditt anpassade domännamn.

## Lägg till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

Stegen för att lägga till ett anpassat domännamn från sidan **Miljö** är desamma som när du [lägger till ett anpassat domännamn från sidan Domäninställningar](#adding-cdn-settings), men startpunkten skiljer sig åt. Följ de här stegen för att lägga till ett anpassat domännamn från sidan **Miljö**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till sidan **Miljöinformation** för att se om miljön är av intresse.

   ![Ange domännamn på sidan Miljöinformation](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Använd tabellen **Domännamn** för att skicka det anpassade domännamnet.

   1. Ange det anpassade domännamnet.
   1. Välj SSL-certifikatet som är associerat med det här namnet i listrutan.
   1. Klicka på **+Lägg till**.

   ![Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Dialogrutan **Lägg till domännamn** öppnas på fliken **Domännamn**. Fortsätt på samma sätt som du gör för [att lägga till ett anpassat domännamn från sidan Domäninställningar](#adding-cdn-settings).
