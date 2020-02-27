---
title: Lägg till användare och roller - vad som krävs
description: Lägg till användare och roller - vad som krävs
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f

---


# Lägg till användare och roller {#add-users-roles}


Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter för att fungera. Exempelvis kan bara vissa användare ange KPI:er (Key Performance Indicators) för ett program. Dessa behörigheter är logiskt grupperade i roller.

[!UICONTROL I Cloud Manager] definieras för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Företagsägare
* Programhanteraren
* Distributionshanteraren
* Utvecklare

>[!CAUTION]
>
>Om du vill använda [!UICONTROL Cloud Manager]måste du ha ett Adobe ID och produktkontexten för Adobe Managed Services.

## Rolldefinitioner {#role-definitions}

>[!NOTE]
>
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

I följande tabell sammanfattas rollerna:

| [!UICONTROL Roller för Cloud Manager] | Beskrivning |
|--- |--- |
| Företagsägare | Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel. |
| Programhanteraren | Använder [!UICONTROL Cloud Manager] för att utföra teamkonfiguration, granska status och visa KPI:er. Kan godkänna viktiga fel i tre nivåer. |
| Distributionshanteraren | Hanterar distributionsåtgärder. Använder [!UICONTROL Cloud Manager] för att köra scen-/produktionsdistributioner. Kan redigera CI/CD-rör. Kan godkänna viktiga fel i tre nivåer. Kan få åtkomst till Git-databasen. |
| Utvecklare | Utvecklar och testar anpassad programkod. I [!UICONTROL molnhanteraren] används främst för att visa status. Kan få åtkomst till Git-databasen för kodimplementering. |
| Innehållsförfattare | I allmänhet interagerar inte med [!UICONTROL Cloud Manager]. Använd [!UICONTROL Cloud Manager] Program Switcher (efter att ha navigerat från [!UICONTROL Experience Cloud]) för att få tillgång till AEM. |