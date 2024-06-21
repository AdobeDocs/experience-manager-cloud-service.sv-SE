---
title: Arkitektur AEM Headless
description: Läs mer om Adobe Experience Manager högnivåarkitektur när det gäller headless-driftsättning. Förstå rollen för AEM Author, Preview och Publish och det rekommenderade distributionsmönstret för headless-program.
feature: Headless, Content Fragments,GraphQL API
exl-id: 5ba6921f-b06e-463d-b956-d1fb434090c9
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Arkitektur AEM Headless

En typisk AEM består av en författartjänst, en Publish-tjänst och en förhandsgranskningstjänst (tillval).

* **Författartjänsten** är den plats där interna användare skapar, hanterar och förhandsgranskar innehåll.

* **Publiceringstjänsten** är&quot;Live&quot;-miljön och det är vanligtvis den slutanvändaren interagerar med. Innehåll som har redigerats och godkänts av författartjänsten distribueras till publiceringstjänsten. Det vanligaste distributionsmönstret med AEM headless-program är att få produktionsversionen av programmet att ansluta till en AEM Publish-tjänst.

* **Förhandsgranskningstjänsten** är funktionellt detsamma som **Publish Service**. Den är dock bara tillgänglig för interna användare. Detta gör det idealiskt för godkännare att granska kommande innehållsändringar innan de görs tillgängliga för slutanvändare.

* **Dispatcher** är en statisk webbserver som utökas med AEM. Den har cachningsfunktioner och ett annat säkerhetsskikt. The **Dispatcher** visas framför **Publicera** och **Förhandsgranska** tjänster.

Inom ett AEM as a Cloud Service program kan du ha flera miljöer: Dev, Stage och Prod. Varje miljö skulle ha sin egen **Upphovsman**, **Publicera** och **Förhandsgranska** tjänster. Du kan lära dig mer om att hantera [miljöer](/help/implementing/cloud-manager/manage-environments.md)

## Skapa Publish-modell

Det vanligaste distributionsmönstret med AEM headless-program är att få produktionsversionen av programmet att ansluta till en AEM Publish-tjänst.

![Skapa Publish-arkitektur](assets/autho-publish-architecture-diagram.png)

Diagrammet ovan visar detta vanliga distributionsmönster.

1. A **Innehållsförfattare** använder tjänsten AEM författare för att skapa, redigera och hantera innehåll.
1. The **Innehållsförfattare** och andra interna användare kan förhandsgranska innehållet direkt i författartjänsten. Du kan konfigurera en förhandsgranskningsversion av programmet som ansluter till författartjänsten.
1. När innehållet har godkänts kan det publiceras till den AEM Publish-tjänsten.
1. The **Dispatcher** är ett lager framför **Publicera** som kan cachelagra vissa förfrågningar och tillhandahålla ett säkerhetslager.
1. Slutanvändarna interagerar med programmets produktionsversion. Produktionsprogrammet ansluter till Publish-tjänsten via Dispatcher och använder GraphQL API:er för att begära och använda innehåll.

## Förhandsgranska Publish-distribution för författare

Ett annat alternativ för headless-driftsättningar är att införliva en **AEM** service. Med den här metoden kan innehåll publiceras först i **Förhandsgranska** och en förhandsvisningsversion av det headless-program som kan anslutas till det. Fördelen med detta är att **Förhandsgranska** kan konfigureras med samma autentiseringskrav och behörigheter som **Publicera** och gör det enklare att simulera produktionsupplevelsen.

![Skapa förhandsgranskning och Publish-arkitektur](assets/author-preview-publish-architecture-diagram.png)

1. A **Innehållsförfattare** använder tjänsten AEM författare för att skapa, redigera och hantera innehåll.
1. Innehållet publiceras först till AEM.
1. Du kan konfigurera en förhandsgranskningsversion av programmet som ansluter till förhandsgranskningstjänsten.
1. När innehållet har granskats och godkänts kan det publiceras till AEM Publish-tjänst.
1. Slutanvändarna interagerar med programmets produktionsversion. Produktionsprogrammet ansluter till Publish-tjänsten via Dispatcher och använder GraphQL API:er för att begära och använda innehåll.
