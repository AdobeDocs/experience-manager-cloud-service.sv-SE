---
title: Rollbaserade behörigheter
description: Rollbaserade behörigheter
translation-type: tm+mt
source-git-commit: 6cae9b2b719dab687f601a0596d37f99afded9ab

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att definiera KPI:er (Key Performance Indicators) och godkänna distributioner.

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll. Den här tabellen visar vilka funktioner som är tillgängliga och vilka roller som kan utföra funktionen.

| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare |
|--- |--- |--- |--- |--- |--- |
| Skapa klientorganisation | Skapa en ny klientorganisation. |  |  |  |  |
| Uppdatera klientorganisation | Uppdatera klientorganisation. |  |  |  |  |
| Lägg till program | Lägg till ett nytt program. | x |  |  |  |
| Skapa miljö | Skapa prod+stage-, dev- och Playground-miljöer. | x | x |  |  |
| Konfigurera miljövariabler | Konfigurera miljövariabler och hemligheter. |  | x |  | x |
| Lägg till eller ta bort anpassat domännamn, överför eller uppdatera SSL-certifikat | Lägg till/ta bort eget domännamn, Överför/Uppdatera SSL-certifikat. | x | x |  |  |
| Uppdateringsmiljö | Uppdatera Prod+Stage-, Dev- och Playground-miljöer. | x | x |  |  |
| Ta bort miljö | Ta bort miljöer som inte är produktiva, dev och Playground. | x | x |  |  |
| Ta bort miljö | Ta bort Prod+Stage Environment. |  |  |  |  |
| Vilolägesmiljö | Hibernate Non-prod, Dev, Playground environment. | x | x |  |  |
| Programinställningar | Konfigurera program (inklusive KPI). | x |  |  |  |
| Programinställningar | Konfigurera skalningsprinciper (allmänt: konfigurera högsta antal nivåer och horisontell skalning vid behov: Anmäl dig). | x |  |  |  |
| Programinställningar | Git implementera åtkomst. |  | x |  | x |
| Inställningar för pipeline | Konfigurera eller redigera pipeline. |  | x |  |  |
| Körning av pipeline | Starta rörledningen. | x | x |  |  |
| Körning av pipeline | Avvisa/godkänn viktiga 3-nivåfel. | x | x | x |  |
| Körning av pipeline | Godkänn Adobe GoLive. | x | x | x |  |
| Körning av pipeline | Schemalägg produktionsdistribution. | x | x | x |  |
| Körning av pipeline | Återuppta produktionsförlopp. |  |  |  |  |
| Anmäl dig till provisionering (eller inte) | Anmäl dig till Vågrät provisionering på begäran från skärmen Programinställningar. Konfigurera de högsta tillåtna P-D-segmenten som kan skalas ut vågrätt i PROD- och icke-PROD-miljöer. | x |  |  |  |
| Hantera miljö | Lägg till segmentet Publish-Dispatcher från skärmen Manage Environment (Hantera miljö). | x | x |  |  |  |
| Produktuppdatering | AEM Update Card är synligt och tar användaren till uppdateringsguiden. | x | x | x | x |
| Produktuppdatering | Produktuppdateringsguiden kan aktiveras. | x | x |  |  |
| Push-uppdatering | Starta Push Update Pipeline. |  |  |  |  |
| Generera token för personlig åtkomst | Generera personlig åtkomsttoken. |  | x |  | x |

