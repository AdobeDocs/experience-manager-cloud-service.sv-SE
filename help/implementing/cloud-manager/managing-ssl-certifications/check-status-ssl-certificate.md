---
title: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
description: Kontrollerar status för ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Kontrollerar status för ett SSL-certifikat {#checking-status-an-ssl-certificate}

Statusen för dina SSL-certifikat kan snabbt förstås från SSL-certifikatsidan eller från sidan med miljöinformation.

Du kan identifiera statusen för ett SSL-certifikat från följande färgscheman:

* ****
GreenAnger att ditt certifikat är giltigt i minst 60 dagar framåt.

* **Orange**
Anger att ditt certifikat upphör att gälla om mindre än 60 dagar. Det är dags att se till att du har en plan för att förnya ditt certifikat och ersätta det via användargränssnittet i Cloud Manager för att undvika eventuell webbplatsåtkomst eller avbrott. Cloud Manager skickar regelbundna meddelanden i användargränssnittet för att informera dig om att certifikatet snart upphör att gälla.

* ****
RedAnger att ditt SSL-certifikat har upphört att gälla trots flera meddelanden.