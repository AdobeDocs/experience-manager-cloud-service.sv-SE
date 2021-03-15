---
title: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
description: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: ddee11fdfa8cadfcd63472fd3c94cd8af555c856
workflow-type: tm+mt
source-wordcount: '200'
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

## Tidigare CDN-konfigurationer för IP-Tillåtelselista {#pre-existing-cdn}

Kunder med miljöer som innehåller befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat eller anpassade domännamn ser följande meddelande på informationssidan för **IP Tillåtelselista** och **Miljö**.

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>För att kunna se och hantera befintliga konfigurationer måste de läggas till via användargränssnittet, vilket visas i bilden nedan.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)