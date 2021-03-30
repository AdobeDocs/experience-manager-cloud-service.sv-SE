---
title: 'Lägga till användare och tilldela molnhanterarroller '
description: Följ den här sidan om du vill lära dig hur du lägger till användare och tilldelar dem till Cloud Manager-roller
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 5%

---


# Lägga till användare och tilldela roller för Cloud Manager {#add-users-assign}

Adobe skapar en **Organization**-identifierare för ditt företag i Adobe Identity Management System (IMS), där alla användare och deras behörigheter kan hanteras. Varje användare, som måste vara medlem i den här organisationen och ska få åtkomst till någon av [!UICONTROL Experience Cloud]-tjänsterna, måste ha sin egen **Adobe ID**.

## Förstå användarroller {#user-roles}

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

## Lägga till användare {#add-users}

>[!NOTE]
>Du måste vara systemadministratör för att kunna lägga till en användare.

1. Om du är systemadministratör går du till [Admin Console](https://adminconsole.adobe.com). Du kan också navigera till Cloud Manager där du kan se knappen **Hantera åtkomst** enligt beskrivningen nedan.

1. Klicka på **Hantera åtkomst**-knappen, som finns högst upp till höger på Cloud Managers startsida, för att öppna Admin Console på en ny flik.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   Från **Admin Console** kan du lägga till användare i Cloud Manager och tilldela dem till roller, som kallas produktprofiler i Admin Console.

1. Välj **Adobe Experience Manager som Cloud Service** på **kort för produkter och tjänster** enligt nedan.

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. Välj fliken **Användare** i åtgärdsfältet och välj sedan **Lägg till användare**.

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. Välj användare och tilldela lämplig molnhanterarroll(er) eller produktprofil(er) till användaren enligt nedan.

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >Se föregående avsnitt, [Användarroller och behörigheter](#user-roles) och [Behörigheter som är associerade med rolldefinitioner](#permissions), för att säkerställa att rätt användare tilldelas rätt roll(er) i **Admin Console**.

   Nu har du lagt till användare i Adobe Experience Manager som produktkontext för Cloud Service och konfigureras med rätt roller eller produktprofiler.

   Om du till exempel har rollen som

   * ***Business Owner***, du har behörighet att lägga till ett nytt program eller redigera ett program, lägga till eller uppdatera en miljö, lägga till/redigera/ta bort pipelinen och köra valfri pipeline samt distribuera kod AEM miljö eller kodkvalitet.

   * ***Distributionshanteraren*** har behörighet att lägga till eller uppdatera en miljö, köra valfri pipeline och distribuera kod AEM miljön eller kodkvaliteten.

   * ***Utvecklare***: du har behörighet att skapa en personlig åtkomsttoken för åtkomst till Git.

      >[!NOTE]
      > En användare kan tilldelas flera roller. Om du till exempel tilldelar både Business Owner- och Deployment Manager-roller till en användare får användaren en kombination av eller summan av dessa behörigheter.
