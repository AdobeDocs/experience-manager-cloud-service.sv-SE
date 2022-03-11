---
title: Arkitektur AEM Headless
description: Läs mer om Adobe Experience Manager högnivåarkitektur när det gäller headless-driftsättning. Förstå rollen för tjänsterna AEM Author, Preview och Publish och det rekommenderade distributionsmönstret för headless-program.
feature: Content Fragments,GraphQL API
exl-id: 5ba6921f-b06e-463d-b956-d1fb434090c9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Arkitektur AEM Headless

En typisk AEM består av en författartjänst, en publiceringstjänst och en förhandsgranskningstjänst (tillval).

* **Författartjänsten** är den plats där interna användare skapar, hanterar och förhandsgranskar innehåll.

* **Publiceringstjänsten** är&quot;Live&quot;-miljön och det är vanligtvis den slutanvändaren interagerar med. Innehåll som har redigerats och godkänts av författartjänsten distribueras till publiceringstjänsten. Det vanligaste distributionsmönstret med AEM headless-program är att ha produktionsversionen av programmet ansluten till en AEM Publish-tjänst.

* **Tjänsten Preview** är funktionellt detsamma som **Publiceringstjänst**. Den är dock bara tillgänglig för interna användare. Detta gör det idealiskt för godkännare att granska kommande innehållsändringar innan de görs tillgängliga för slutanvändare.

* **Dispatcher** är en statisk webbserver som utökas med AEM. Den har cachningsfunktioner och ett annat säkerhetsskikt. The **Dispatcher** visas framför **Publicera** och **Förhandsgranska** tjänster.

Inom ett AEM as a Cloud Service program kan du ha flera miljöer: Dev, Stage och Prod. Varje miljö skulle ha sin egen **Upphovsman**, **Publicera** och **Förhandsgranska** tjänster. Du kan lära dig mer om att hantera [miljöer](/help/implementing/cloud-manager/manage-environments.md)

## Skapa publiceringsmodell

Det vanligaste distributionsmönstret med AEM headless-program är att ha produktionsversionen av programmet ansluten till en AEM Publish-tjänst.

![Author Publish Architecture](assets/autho-publish-architecture-diagram.png)

Diagrammet ovan visar det här vanliga distributionsmönstret.

1. A **Innehållsförfattare** använder tjänsten AEM Author för att skapa, redigera och hantera innehåll.
1. The **Innehållsförfattare** och andra interna användare kan förhandsgranska innehållet direkt i författartjänsten. Du kan konfigurera en förhandsgranskningsversion av programmet som ansluter till författartjänsten.
1. När innehållet har godkänts kan det publiceras till AEM Publish-tjänsten.
1. The **Dispatcher** är ett lager framför **Publicera** som kan cachelagra vissa förfrågningar och tillhandahålla ett säkerhetslager.
1. Slutanvändarna interagerar med programmets produktionsversion. Produktionsprogrammet ansluter till publiceringstjänsten via Dispatcher och använder GraphQL-API:erna för att begära och använda innehåll.

## Publiceringsdistribution för förhandsgranskning av författare

Ett annat alternativ för headless-driftsättningar är att införliva en **AEM** service. Med den här metoden kan innehåll publiceras först i **Förhandsgranska** och en förhandsvisningsversion av det headless-program som kan anslutas till det. Fördelen med detta är att **Förhandsgranska** kan konfigureras med samma autentiseringskrav och behörigheter som **Publicera** och gör det enklare att simulera produktionsupplevelsen.

![Arkitektur för förhandsgranskning och publicering](assets/author-preview-publish-architecture-diagram.png)

1. A **Innehållsförfattare** använder tjänsten AEM Author för att skapa, redigera och hantera innehåll.
1. Innehållet publiceras först till AEM.
1. Du kan konfigurera en förhandsgranskningsversion av programmet som ansluter till förhandsgranskningstjänsten.
1. När innehållet har granskats och godkänts kan det publiceras till AEM Publish-tjänsten.
1. Slutanvändarna interagerar med programmets produktionsversion. Produktionsprogrammet ansluter till publiceringstjänsten via Dispatcher och använder GraphQL-API:erna för att begära och använda innehåll.
