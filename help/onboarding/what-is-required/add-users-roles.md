---
title: Lägg till användare och roller - vad som krävs
description: Lägg till användare och roller - vad som krävs
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Lägg till användare och roller {#add-users-roles}


Många funktioner i [!UICONTROL Cloud Manager] kräver specifika behörigheter för att kunna användas.

[!UICONTROL Cloud Manager] definierar för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!CAUTION]
>
>Om du vill använda [!UICONTROL Cloud Manager] måste du ha en Adobe ID och Adobe Experience Manager som produktkontext för Cloud Service.

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

## Integreringsproduktprofilen {#integration-product-profile}

Utöver ovanstående skapar Cloud Manager automatiskt en produktprofil med namnet&quot;Integrationer - Cloud Service&quot;. Den här produktprofilen används för integreringar mellan Adobe Experience Manager och andra Adobe-produkter. Den här produktprofilen **måste** inte tas bort. Om du tar bort den här profilen av misstag måste den återskapas manuellt. Visningsnamnet för den här profilen **måste** vara `CM_CS_DEFAULT`.
