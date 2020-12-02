---
title: Lägg till användare och roller - vad som krävs
description: Lägg till användare och roller - vad som krävs
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 9%

---


# Lägg till användare och roller {#add-users-roles}


Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter för att kunna användas. Exempelvis kan bara vissa användare ange KPI:er (Key Performance Indicators) för ett program. Dessa behörigheter är logiskt grupperade i roller.

[!UICONTROL Cloud Manager] definierar för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!CAUTION]
>
>Om du vill använda [!UICONTROL Cloud Manager] måste du ha en Adobe ID och produktkontexten för Adobes hanterade tjänster.

## Rolldefinitioner {#role-definitions}

>[!NOTE]
>
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

I följande tabell sammanfattas rollerna:

| [!UICONTROL Cloud Manager] Roller | Beskrivning |
|--- |--- |
| Företagsägare | Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel. |
| Programhanteraren | Använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status och visa KPI:er. Kan godkänna viktiga fel i tre nivåer. |
| Distributionshanteraren | Hanterar distributionsåtgärder. Använder [!UICONTROL Cloud Manager] för att köra scen-/produktionsdistributioner. Kan redigera CI/CD-rör. Kan godkänna viktiga fel i tre nivåer. Kan få åtkomst till Git-databasen. |
| Utvecklare | Utvecklar och testar anpassad programkod. I används främst [!UICONTROL Cloud Manager] för att visa status. Kan få åtkomst till Git-databasen för kodimplementering. |
| Innehållsförfattare | I allmänhet interagerar inte med [!UICONTROL Cloud Manager]. Använd [!UICONTROL Cloud Manager] Programväljaren (när du har navigerat från [!UICONTROL Experience Cloud]) för att få åtkomst till AEM. |