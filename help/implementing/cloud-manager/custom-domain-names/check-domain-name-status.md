---
title: Kontrollerar domännamnsstatus
description: Kontrollerar domännamnsstatus
translation-type: tm+mt
source-git-commit: f3df4b23dc4542e7a194c979a7894bda1b728572
workflow-type: tm+mt
source-wordcount: '343'
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


## Redan befintliga CDN-konfigurationer för IP-Tillåtelselista {#pre-existing-cdn}

Kunder med miljöer som innehåller befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat eller anpassade domännamn ser följande meddelande på informationssidan för **IP Tillåtelselista** och **Miljö**. Meddelandet som visas i användargränssnittet försvinner när kunden har migrerat alla befintliga miljökonfigurationer via användargränssnittet och det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

>[!NOTE]
>För att kunna se och hantera befintliga konfigurationer måste de läggas till via användargränssnittet. Mer information finns i [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)
