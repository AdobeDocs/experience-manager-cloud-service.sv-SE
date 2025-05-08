---
title: Autentisering av universell redigerare
description: Läs om hur den universella redigeraren använder Adobe Identity Management System (IMS) för autentisering.
exl-id: fb86c510-3c41-4511-81b7-1bdf2f5e7dd3
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c4dcb1cecb756f746ecb856fcfd65d73833a5ee0
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Autentisering av universell redigerare {#authentication}

Lär dig hur den universella redigeraren autentiseras.

## Alternativ {#options}

Universal Editor använder Adobe Identity Management System-autentisering (IMS), som tillhandahålls via det enhetliga skalet.

Alla program/fjärrsidor ansvarar för autentisering till de backend-system som krävs. Tjänsten Universal Editor behöver denna autentisering för backend-system för att kunna utföra CRUD-åtgärder som fristående tjänster.

## Standardflöde {#standard-flow}

Det här är lösningen för AEM as a Cloud Service och AMS som använder IMS för att använda Universal Editor.

Om du vill använda den universella redigeraren måste användaren vara inloggad i det enhetliga gränssnitt som autentiserar mot IMS. Den angivna IMS-token lagras i användarens sessionsarkiv.

När en användare utför en CRUD-åtgärd skickas ett anrop till Universal Editor-tjänsten med IMS-bearer-token i HTTP-huvudet. Tjänsten Universal Editor använder sedan bearer-token för att autentisera begäran mot AEM serverdelssystem för att köra åtgärder i användarens namn.

![Standardautentiseringsflöde](assets/standard-flow.png)

I det här diagrammet och den här artikeln beskrivs den interna autentiseringen av den universella redigeraren.

{{ue-headless-auth}}
