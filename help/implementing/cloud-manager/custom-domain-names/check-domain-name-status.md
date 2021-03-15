---
title: Kontrollerar domännamnsstatus
description: Kontrollerar domännamnsstatus
translation-type: tm+mt
source-git-commit: ddee11fdfa8cadfcd63472fd3c94cd8af555c856
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Du kan ta reda på om ditt domännamn har verifierats genom att klicka på statusikonen för domännamnet i tabellen i Miljöer på sidan Domäninställningar.

>[!NOTE]
>Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer Spara i verifieringssteget i guiden Lägg till anpassad domän. För efterföljande verifieringar måste du aktivt välja ikonen **verifiera igen** bredvid statusen.

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden:

* **Domänverifieringen**
FailedTXT-värdet saknas eller har identifierats med fel. Följ instruktionerna och försök igen. När du är klar måste du välja 
*verifiera* againicon bredvid statusen.

* **Domänverifiering**
pågårVerifiering pågår. Den här statusen visas vanligtvis när du har valt 
*verifiera* againicon bredvid statusen.

* **Verifierad, Distributionen**
FailedTXT-verifieringen lyckades. CDN-distributionen misslyckades dock. En Adobe-representant meddelas automatiskt.

* **Domän verifierad och**
distribueradDen här statusen anger att ditt anpassade domännamn är klart att användas.
   >[!NOTE]
   >Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn. Mer information finns i [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md).

* **Borttagning**
av anpassat domännamn pågår.

* **Borttagningen**
misslyckades. Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen. Mer information finns i [Ta bort ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md).


## Tidigare CDN-konfigurationer för IP-Tillåtelselista {#pre-existing-cdn}

Kunder med miljöer som innehåller befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat eller anpassade domännamn ser följande meddelande på informationssidan för **IP Tillåtelselista** och **Miljö**.

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>För att kunna se och hantera befintliga konfigurationer måste de läggas till via användargränssnittet, vilket visas i bilden nedan.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)
