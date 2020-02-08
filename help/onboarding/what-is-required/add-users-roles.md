---
title: Lägg till användare och roller - vad som krävs
description: Lägg till användare och roller - vad som krävs
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Lägg till användare och roller - vad som krävs {#add-users-roles}


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

## Skapa en profil med Admin Console {#using-admin-console-to-create-a-profile}

Roller hanteras för [!UICONTROL Cloud Manager] från Adobe Admin Console. Specifika rollmedlemskap erbjuds genom att användaren läggs till i en [!UICONTROL Cloud Manager] -produktprofil i Admin Console.

Du kan tilldela specifika rollmedlemskap genom att lägga till användaren i en [!UICONTROL Cloud Manager] - **produktprofil** i Adobe Admin Console, en central plats där du kan hantera dina Adobe-berättiganden i hela organisationen. Mer information om Adobe Admin Console finns i dokumentationen för [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

>[!NOTE]
>
>Öppna en webbläsare och gå till Admin Console och konfigurera ditt team (användare och roller) på [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise).

För att användare av [!UICONTROL Cloud Manager] ska kunna tillhandahålla rätt rollbaserade behörigheter måste en administratör i kundens **organisation** skapa nya produktprofiler under produktkontexten för [!UICONTROL AEM Managed Services] .

Om du vill ge [!UICONTROL Cloud Manager] -användare rätt rollbaserade behörigheter måste du som administratör skapa fyra nya produktprofiler under produktkontexten för [!UICONTROL AEM Managed Services] som motsvarar var och en av de fyra [!UICONTROL Cloud Manager] -rollerna:

* Företagsägare
* Distributionshanteraren
* Utvecklare
* Programhanteraren

Du kan skapa eller lägga till användare/grupper i dessa produktprofiler med [Admin Console](https://adminconsole.adobe.com/) för [!UICONTROL Cloud Manager], vilket visas i bilden nedan:

1. Logga in på Admin Console och klicka på **Ny profil** för att lägga till en ny profil.

1. Fyll i fälten för att konfigurera en ny roll för [!UICONTROL Cloud Manager].

   Ange **profilnamn**, **visningsnamn** för att skapa en ny profil. Dessutom kan du välja en **behörighetsgrupp** för profilen.

   Klicka på **Klar** för att slutföra steget när du skapar profilen.

   >[!NOTE]
   >
   >När du skapar de här produktprofilerna måste **visningsnamnet** vara det tekniska värde som definieras av [!UICONTROL Cloud Manager] (se tabellen nedan). Profilnamnet **kan vara vad som helst, men för att undvika missförstånd bör du använda värdena i kolumnen** Rekommenderat profilnamn ** nedan. När du skapar produktprofilen avmarkerar du **Samma som profilnamn** och anger motsvarande värde som **visningsnamn**.

   | **Roll** | **Visningsnamn (obligatoriskt)** | **Rekommenderat profilnamn** |
   |---|---|---|
   | Företagsägare | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - rollen som företagsägare |
   | Distributionshanteraren | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Distributionshanterarroll |
   | Utvecklare | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Utvecklarroll |
   | Programhanteraren | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - rollen programhanterare |

1. När du har skapat en produktprofil kan du lägga till användare (eller grupper) i produktprofiler.


