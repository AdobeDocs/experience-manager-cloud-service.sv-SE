---
title: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
description: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: 0b04d43c8b5bb28286e616f0bd902c05ec56ec05
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Kontrollerar status för ett SSL-certifikat {#checking-status-an-ssl-certificate}

Statusen för dina SSL-certifikat kan snabbt förstås från SSL-certifikatsidan.

Du kan identifiera statusen för ett SSL-certifikat från följande färgscheman:

* ****
GreenAnger att ditt certifikat är giltigt i minst 60 dagar framåt.

* **Orange**
Anger att ditt certifikat upphör att gälla om mindre än 60 dagar. Det är dags att se till att du har en plan för att förnya ditt certifikat och ersätta det via användargränssnittet i Cloud Manager för att undvika eventuell webbplatsåtkomst eller avbrott. Cloud Manager skickar regelbundna meddelanden i användargränssnittet för att informera dig om att certifikatet snart upphör att gälla.

* ****
RedAnger att ditt SSL-certifikat har upphört att gälla trots flera meddelanden.

## Redan befintliga CDN-konfigurationer för IP-Tillåtelselista {#pre-existing-cdn}

Kunder med miljöer som innehåller befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat eller anpassade domännamn ser följande meddelande på informationssidan för **IP Tillåtelselista** och **Miljö**. Meddelandet som visas i användargränssnittet försvinner när kunden har migrerat alla befintliga miljökonfigurationer via användargränssnittet och det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>För att kunna se och hantera befintliga konfigurationer måste de läggas till via användargränssnittet, vilket visas i bilden nedan.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)