---
title: Inställning av push-validering
description: Lär dig hur du konfigurerar push-ogiltigförklaring för att skapa en egen produktion för CDN.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
source-git-commit: 3941b7f97d434946a3cb796633f306b89e68c0a4
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Ange push-ogiltigförklaring

Push-ogiltigförklaring säkerställer att innehållsuppdateringar som författarna gjort automatiskt tas bort från CDN (Managed Content Delivery Network) när de publiceras, så att endast det senaste innehållet levereras.

Systemet rensar innehållet baserat på specifika URL:er och cachetaggar eller nycklar, vilket säkerställer att inaktuella versioner rensas.

Om du vill aktivera push-ogiltigförklaring måste specifika egenskaper läggas till i projektets konfigurationsfil. Exempel: en Microsoft Excel-arbetsbok med namnet `.helix/config.xlsx` i SharePoint, eller ett Google-bladnamn `.helix/config` i Google Drive.

Följande konfigurationsegenskaper definierar namnet på produktionsvärden och typen av CDN-hantering:

| key | value | kommentar |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Produktionsplatsens värdnamn. Exempel: `www.example.com`. |
| `cdn.prod.type` | hanterad |   |

När ändringar har gjorts i konfigurationsbladet måste användarna förhandsgranska och aktivera dem med verktyget [Sidekick](/help/edge/docs/sidekick.md) för att kunna använda uppdateringarna.
