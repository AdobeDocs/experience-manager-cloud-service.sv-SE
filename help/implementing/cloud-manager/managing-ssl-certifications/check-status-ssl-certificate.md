---
title: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
description: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Kontrollerar status för ett SSL-certifikat {#checking-status-an-ssl-certificate}

Statusen för dina SSL-certifikat kan snabbt förstås från SSL-certifikatsidan.

Du kan identifiera statusen för ett SSL-certifikat från följande färgscheman:

* **Grön**
Anger att ditt certifikat är giltigt i minst 60 dagar framåt.

* **Orange**
Anger att ditt certifikat upphör att gälla om mindre än 60 dagar. Det är dags att se till att du har en plan för att förnya ditt certifikat och ersätta det via användargränssnittet i Cloud Manager för att undvika eventuell webbplatsåtkomst eller avbrott. Cloud Manager skickar regelbundna meddelanden i användargränssnittet för att informera dig om att certifikatet snart upphör att gälla.

* **Röd**
Anger att ditt SSL-certifikat har upphört att gälla trots flera meddelanden.

## Tidigare CDN-konfigurationer {#pre-existing-cdn}

Kunder som har miljöer med befintliga CDN-konfigurationer för IP-Tillåtelselista, SSL-certifikat eller anpassade domännamn kommer att se följande meddelande i **IP Tillåtelselista** och **Miljö** informationssida. Meddelandet som visas i användargränssnittet försvinner när kunden har migrerat alla befintliga miljökonfigurationer via användargränssnittet och det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

>[!NOTE]
>För att kunna se och hantera befintliga konfigurationer måste de läggas till via användargränssnittet. Se [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) för mer information.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
