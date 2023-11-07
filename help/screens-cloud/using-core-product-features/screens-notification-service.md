---
title: Tjänsten Skärmmeddelanden på as a Cloud Service
description: På den här sidan beskrivs hur du konfigurerar meddelandetjänsten på skärmar as a Cloud Service.
index: true
source-git-commit: 81ce7954479366e40b47325577e1450f3d7a4c29
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Tjänsten Skärmmeddelanden {#notification-service}

## Introduktion {#introduction}

### Översikt

Med AEM Screens Notifications Service kan administratörer få ett e-postmeddelande om en AEM inte pingar under en konfigurerbar tidsperiod.

### Konfigurera

På AEM Screens Cloud kan kunder begära aviseringar om status för enhetsinaktivitet genom att skapa en supportanmälan med följande information:

* Kundnamn
* IMS OrgID
* Schemaläggningsfrekvens: Ange en tid eller frekvens i timmar (t.ex. 1) som den här övervakaren ska skicka e-post med.
* Ping-timeout: Anger intervallet i minuter efter vilket en enhet inte kan nås.
* E-post-ID: E-post-ID dit rapporten ska skickas