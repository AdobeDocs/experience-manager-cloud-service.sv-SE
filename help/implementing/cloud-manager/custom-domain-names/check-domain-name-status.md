---
title: Kontrollerar domännamnsstatus
description: Kontrollerar domännamnsstatus
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Kontrollerar domännamnsstatus {#check-status}

Du kan ta reda på om ditt domännamn har verifierats genom att klicka på statusikonen för domännamnet i tabellen i Miljöer på sidan Domäninställningar.

>[!NOTE]
>Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer Spara i verifieringssteget i guiden Lägg till anpassad domän. För efterföljande verifieringar måste du aktivt välja **verifiera igen** -ikonen bredvid statusen.

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden:

* **Domänverifieringen misslyckades**
TXT-värdet saknas eller identifieras med fel. Följ instruktionerna och försök igen. När du är klar måste du välja 
*verifiera igen* -ikonen bredvid statusen.

* **Domänverifiering pågår**
Verifiering pågår. Den här statusen visas vanligtvis när du har valt 
*verifiera igen* -ikonen bredvid statusen.

* **Verifierad, distributionen misslyckades**
TXT-verifieringen lyckades. CDN-distributionen misslyckades dock. Kontakta din Adobe-representant.

* **Domänen har verifierats och distribuerats**
Den här statusen anger att ditt anpassade domännamn är klart att användas.
   >[!NOTE]
   >Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn. Se [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) om du vill veta mer.

* **Tar bort**
Det anpassade domännamnet tas bort.

* **Borttagningen misslyckades**
Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen. Se [Ta bort ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) om du vill veta mer.


## Tidigare CDN-konfigurationer för anpassade domännamn {#pre-existing-cdn}

Kunder som har miljöer med befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat eller anpassade domännamn kommer att se följande meddelande i **IP Tillåtelselista** och **Miljö** informationssida. Meddelandet som visas i användargränssnittet försvinner när kunden har migrerat alla befintliga miljökonfigurationer via användargränssnittet och det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

>[!NOTE]
>För att kunna se och hantera befintliga konfigurationer måste de läggas till via användargränssnittet. Se [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) för mer information.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
