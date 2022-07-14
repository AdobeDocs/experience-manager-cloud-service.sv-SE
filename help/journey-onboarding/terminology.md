---
title: AEM as a Cloud Service terminologi
description: Innan du loggar in på AEMaaCS är det praktiskt att förstå en del av terminologin i systemet och dess grundläggande struktur.
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# AEM as a Cloud Service terminologi {#terminology}

I den här delen av [startresan,](overview.md) kommer du att lära dig en del av terminologin AEM as a Cloud Service och dess grundläggande struktur.

## Syfte {#objective}

Nu när du förstår vad som har lett till introduktionsprocessen genom att läsa dokumentet [Förberedelser för introduktion,](preparation.md) det är till hjälp att förstå vissa termer i systemet och dess grundläggande struktur innan du loggar in.

AEM as a Cloud Service är ett kraftfullt och flexibelt verktyg och för att kunna använda vilket verktyg som helst måste du känna till hur det är organiserat och vilka termer och språk som används för att beskriva det. I det här dokumentet sammanfattas några viktiga termer som du behöver förstå innan du börjar använda systemet.

När du har läst det här dokumentet kommer du att förstå:

* De olika lager som utgör AEMaaCS.
* Grunderna i vad varje lager gör.

## AEMaaCS-struktur {#structure}

För denna introduktionsresa behövs ingen fullständig förståelse av den AEM as a Cloud Service strukturen. Men om du är bekant med följande koncept blir det enklare att följa med senare under resan.

![Cloud Manager-struktur](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **TENANT** - Alla kunder tillhandahålls med en klient. En hyresgäst kallas även IMS-organisation (mer på IMS senare under denna resa)
* **PROGRAM** - Varje innehavare har ett eller flera program som ofta återspeglar kundens licensierade lösningar.
* **MILJÖ** - Varje program har flera miljöer, t.ex. produktion för direktinnehåll, en för mellanlagring och en för utvecklingsändamål.
* **DATABAS** - Miljöerna har en eller flera Git-databaser där program- och front end-kod bevaras.
* **VERKTYG OCH ARBETSFLÖDEN** - Pipelines hanterar distributionen av kod från databaserna till miljöerna.

Ett exempel är ofta användbart när hierarkin ska sammanställas.

* WKND Travel and Adventure Enterprises kan vara en **tenant** som fokuserar på reserelaterade medier.
* Innehavare av WKND Travel och Adventure Enterprises kan ha två **program**:
   * One Sites Program for its WKND Magazine division
   * Ett Assets-program för WKND Media Division
* Programmen WKND Magazine och WKND Media skulle ha både utveckling, staging och produktion **miljöer**.
* **Databaser** används för att underhålla anpassad kod och program för WKND Magazine och WKND Media.
* Olika **verktyg och arbetsflöden** arbeta i alla rapporter för att driftsätta kod med CI/CD-pipelines, åtkomstloggar, AEM etc.

## What’s Next {#what-is-next}

Nu när du har slutfört den här delen av AEM introduktionsresa bör du förstå:

* De olika lager som utgör AEMaaCS.
* Grunderna i vad varje lager gör.

Bygg vidare på denna kunskap och fortsätt din AEM introduktionsresa genom att läsa dokumentet nästa gång [Åtkomst till Admin Console](admin-console.md), där du får lära dig hur du kommer åt konsolen och verifierar din status som systemadministratör.
