---
title: Användarroller och behörigheter
description: Den här sidan beskriver användarroller och behörigheter. Följ den här sidan om du vill lära dig hur du lägger till användare och tilldelar dem till roller i molnhanteraren.
translation-type: tm+mt
source-git-commit: f09b688db23024d59f39b53766060b6f3b14e564
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 9%

---


# Användarroller och behörigheter {#user-roles-permissions}

Adobe skapar en **Organization**-identifierare för ditt företag i Adobe Identity Management System (IMS), där alla användare och deras behörigheter kan hanteras. Varje användare, som måste vara medlem i den här organisationen och ska få åtkomst till någon av [!UICONTROL Experience Cloud]-tjänsterna, måste ha sin egen **Adobe ID**.

## Användarroller {#user-roles}

Många funktioner i Cloud Manager kräver specifika behörigheter för att fungera.

I Cloud Manager definieras för närvarande fyra roller för användare som styr tillgängligheten av specifika funktioner:

* Business Owner
* Deployment Manager
* Program Manager
* Developer

>[!NOTE]
>Utvecklarrollen i Admin Console är inte relaterad till utvecklarrollen i [!UICONTROL Cloud Manager].

I följande tabell sammanfattas rollerna:

| [!UICONTROL Cloud Manager] Roller | Beskrivning |
|--- |--- |
| Företagsägare | Ansvarig för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-skiktsfel. |
| Programhanteraren | Använder [!UICONTROL Cloud Manager] för att utföra gruppkonfiguration, granska status och visa KPI:er. Kan godkänna viktiga fel i tre nivåer. |
| Distributionshanteraren | Hanterar distributionsåtgärder. Använder [!UICONTROL Cloud Manager] för att köra scen-/produktionsdistributioner. Kan redigera CI/CD-rör. Kan godkänna viktiga fel i tre nivåer. Kan få åtkomst till Git-databasen. |
| Utvecklare | Utvecklar och testar anpassad programkod. I används främst [!UICONTROL Cloud Manager] för att visa status. Kan få åtkomst till Git-databasen för kodimplementering. |
| Innehållsförfattare | I allmänhet interagerar inte med [!UICONTROL Cloud Manager]. Använd [!UICONTROL Cloud Manager] Programväljaren (när du har navigerat från [!UICONTROL Experience Cloud]) för att få åtkomst till AEM. |

### Integreringsproduktprofilen {#integration-product-profile}

Utöver ovanstående skapar Cloud Manager automatiskt en produktprofil med namnet&quot;Integrationer - Cloud Service&quot;. Den här produktprofilen används för integreringar mellan Adobe Experience Manager och andra Adobe-produkter. Den här produktprofilen **måste** inte tas bort. Om du tar bort den här profilen av misstag måste den återskapas manuellt. Visningsnamnet för den här profilen **måste** vara `CM_CS_DEFAULT`.


## Behörigheter associerade med rolldefinitioner {#permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att definiera KPI:er (Key Performance Indicators) och godkänna distributioner.


Var och en av rollerna har specifika behörigheter som är kopplade till varje roll. I följande tabell sammanfattas rollerna, de funktioner som är tillgängliga och de roller som kan utföra funktionen.

| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare |
|--- |--- |--- |--- |--- |--- |
| Lägg till program | Lägg till ett nytt program. | x |  |  |  |
| Skapa miljö | Skapa prod+stage, dev, environment. | x | x |  |  |
| Uppdateringsmiljö | Uppdatera Prod+Stage, Dev, Environmental. | x | x |  |  |
| Ta bort miljö | Ta bort miljöer som inte är produktiva, dev. | x | x |  |  |
| Inställningar för pipeline | Konfigurera eller redigera pipeline. |  | x |  |  |
| Körning av pipeline | Starta rörledningen. | x | x |  |  |
| Körning av pipeline | Avvisa/godkänn viktiga 3-nivåfel. | x | x | x |  |
| Körning av pipeline | Godkänn GoLive. | x | x | x |  |
| Körning av pipeline | Schemalägg produktionsdistribution. | x | x | x |  |
| Ta bort pipeline | Tillåter borttagning av en pipeline. |  | x |  |  |
| Avbryt körning | Avbryt aktuell körning. |  | x |  |  |
| Generera token för personlig åtkomst | Access Git. |  | x |  | x |