---
title: Tjänsten Skärmmeddelanden på as a Cloud Service
description: På den här sidan beskrivs hur du konfigurerar meddelandetjänsten på skärmar as a Cloud Service.
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 69798b1ac3758d37c4e2f480ccc23bae24d6a814
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Tjänsten Skärmmeddelanden {#notification-service}

## Introduktion {#introduction}

### Ökning

Med AEM Screens Notifications Service kan administratörer få en rapport med en lista över alla AEM Screens-spelare som inte pingade för en konfigurerbar tidsperiod i ett e-postmeddelande.

### Konfigurera

På AEM Screens Cloud kan kunder begära en rapport om status för enhetsinaktivitet genom att skapa en supportanmälan med följande information:

* Kundnamn
* IMS OrgID
* Schemaläggningsfrekvens: Ange en tid eller frekvens i timmar (till exempel 1) som den här övervakaren ska skicka e-post med.
* Ping-timeout: Anger intervallet i minuter efter vilket en enhet inte kan nås.
* E-post-ID: E-post-ID dit rapporten ska skickas

>[!NOTE]
>I e-postmeddelanden rapporteras spelaren endast om enheten som inte har pingat för den angivna pingtidsgränsen när e-postmeddelandet genereras.

### Exempel på användningsfall

Om du anger rapporttiden som 5 och pingtidsgränsen som 1 timme, kommer du att få ett e-postmeddelande som bekräftar inaktivitet för enheten om skärmenheten inte växlar mellan 04.00 och 07.00.
