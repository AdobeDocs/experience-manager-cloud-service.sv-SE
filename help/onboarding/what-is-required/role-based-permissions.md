---
title: Rollbaserade behörigheter
description: Rollbaserade behörigheter
translation-type: tm+mt
source-git-commit: e59fe55c255d5239a561a9fb878faa81d17b4b48

---


# Rollbaserade behörigheter {#role-based-permissions}

[!UICONTROL Cloud Manager] har förkonfigurerade roller med lämplig behörighet. En utvecklare utvecklar till exempel kod och har behörighet att skicka koden till **Git-databasen**. En företagsägare har också olika behörigheter för att definiera KPI:er (Key Performance Indicators) och godkänna distributioner.

## Användarbehörigheter {#user-permissions}

Var och en av rollerna har specifika behörigheter, förkonfigurerade uppgifter eller behörigheter som är kopplade till varje roll. Den här tabellen visar vilka funktioner som är tillgängliga och vilka roller som kan utföra funktionen.

| Behörighet | Beskrivning | Företagsägare | Distributionshanteraren | Programhanteraren | Utvecklare |
|--- |--- |--- |--- |--- |--- |
| Lägg till program | Lägg till nytt program. | x | x | x | x |
| Läsprogram | Läs Program-KPI:er. | x | x | x | x |
| Skriv program | Programinstallation eller redigering. | x |  |  |  |  |
| Läs miljö | Se Miljöinformation. | x | x | x | x |
| Skapa körning | Starta pipeline. | x | x | x |  |
| Läskörning | Se körningsstatus. | x | x | x | x |
| Återuppta körning | Kan återuppta körning när den är pausad. | x | x | x |  | x |
| Kör Godkänn distribution till produktion | Godkänn Adobe GoLive. | x | x | x |  |  |
| Distribuera körningsschema till produktion | Schemalägg produktionsdistribution. | x | x | x |
| Avbryt körning | Avbryt aktuell körning. | x | x | x |  |
| Fel vid kvalitetshastighet för körning | Godkänn viktiga fel i Quality Gate. | x | x | x |  |
| Skapa pipeline | Konfigurera/redigera pipeline. |  | x |  |  |
| Pipeline-läsning | Se Information om pipeline. | x | x | x | x |
| Pipeline Write | Konfigurera/redigera pipeline. |  | x |  |  |
| Ändra godkännande av pipeline | Tillåter redigering av alternativet Affärsägare. |  | x |  |  |
| Läs steg | Se resultaten av mätvärdena för stegkvalitet. | x | x | x | x |
