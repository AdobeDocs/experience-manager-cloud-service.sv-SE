---
title: Tjänsten Skärmmeddelanden på as a Cloud Service
description: På den här sidan beskrivs hur du konfigurerar meddelandetjänsten på skärmar as a Cloud Service.
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 237b4a8e01af74dbaac0ba1715b5fa95c931be7c
workflow-type: tm+mt
source-wordcount: '125'
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
* Schemaläggningsfrekvens: Ange en tid eller frekvens i timmar (till exempel 1) som den här övervakaren ska skicka e-post med.
* Ping-timeout: Anger intervallet i minuter efter vilket en enhet inte kan nås.
* E-post-ID: E-post-ID dit rapporten ska skickas
