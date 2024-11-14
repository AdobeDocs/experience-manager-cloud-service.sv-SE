---
title: Konfigurera push-validering för en Edge Delivery-webbplats
description: Upptäck hur du konfigurerar push-ogiltigförklaring för en Edge Delivery-webbplats för att säkerställa effektiv innehållsuppdatering och cachningskontroll.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: 1a391837ded0af0c5bb436c34a5818f418436308
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Ange push-ogiltigförklaring

Push-ogiltigförklaring säkerställer att innehållsuppdateringar som författare gjort automatiskt tas bort från det hanterade CDN-nätverket (Content Delivery Network) när de publiceras. På så sätt säkerställs att endast det senaste innehållet levereras.

Systemet rensar innehållet baserat på specifika URL:er och cachetaggar eller nycklar, vilket säkerställer att inaktuella versioner rensas.

Om du vill aktivera push-ogiltigförklaring måste specifika egenskaper läggas till i projektets konfigurationsfil. Exempel: en Microsoft Excel-arbetsbok med namnet `.helix/config.xlsx` i SharePoint, eller ett Google-bladnamn `.helix/config` i Google Drive.

Följande konfigurationsegenskaper definierar namnet på produktionsvärden och typen av CDN-hantering:

| key | value | kommentar |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Produktionsplatsens värdnamn. Exempel: `www.example.com`. |
| `cdn.prod.type` | hanterad |   |

När ändringar har gjorts i konfigurationsbladet måste användarna förhandsgranska och aktivera dem med verktyget [Sidekick](/help/edge/docs/sidekick.md) för att kunna använda uppdateringarna.

Se även [Om att göra-listan för Edge Delivery i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
