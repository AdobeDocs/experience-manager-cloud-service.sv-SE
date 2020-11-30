---
title: Rollbaserade behörigheter
description: Rollbaserade behörigheter
translation-type: tm+mt
source-git-commit: 3c56d94f9922cb65b91912dd96eb8aa60efc2b53
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 19%

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att definiera KPI:er (Key Performance Indicators) och godkänna distributioner.

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll. Den här tabellen visar vilka funktioner som är tillgängliga och vilka roller som kan utföra funktionen.

| Behörighet | Beskrivning | Business Owner | Deployment Manager | Program Manager | Developer |
|--- |--- |--- |--- |--- |--- |
| Lägg till program | Lägg till ett nytt program. | x |  |  |  |
| Skapa miljö | Skapa prod+stage-, dev- och Playground-miljöer. | x | x |  |  |
| Uppdateringsmiljö | Uppdatera Prod+Stage-, Dev- och Playground-miljöer. | x | x |  |  |
| Ta bort miljö | Ta bort miljöer som inte är produktiva, dev och Playground. | x | x |  |  |
| Ta bort miljö | Ta bort Prod+Stage Environment. |  |  |  |  |
| Programinställningar | Konfigurera program (inklusive KPI). | x |  |  |  |
| Programinställningar | Git implementera åtkomst. |  | x |  | x |
| Inställningar för pipeline | Konfigurera eller redigera pipeline. |  | x |  |  |
| Körning av pipeline | Starta rörledningen. | x | x |  |  |
| Körning av pipeline | Avvisa/godkänn viktiga 3-nivåfel. | x | x | x |  |
| Körning av pipeline | Godkänn GoLive. | x | x | x |  |
| Körning av pipeline | Schemalägg produktionsdistribution. | x | x | x |  |
| Körning av pipeline | Återuppta produktionsförlopp. |  |  |  |  |
| Ta bort pipeline | Tillåter borttagning av en pipeline. |  | x |  |  |
| Avbryt körning | Avbryt aktuell körning. |  | x |  |  |
| Hantera miljö | Lägg till segmentet Publish-Dispatcher från skärmen Manage Environment (Hantera miljö). | x | x |  |  |  |
| Push-uppdatering | Starta Push Update Pipeline. |  |  |  |  |
| Generera token för personlig åtkomst | Access Git. |  | x |  | x |

