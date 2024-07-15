---
title: AEM as a Cloud Service Terminologi
description: Innan du loggar in på AEMaaCS är det praktiskt att förstå en del av terminologin i systemet och dess grundläggande struktur.
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# AEM as a Cloud Service Terminologi {#terminology}

I den här delen av [introduktionsresan ](overview.md) lär du dig en del av terminologin i AEM as a Cloud Service och dess grundläggande struktur.

## Syfte {#objective}

Nu när du förstår vad som har lett till introduktionsprocessen genom att läsa dokumentet [Förberedelse för introduktion](preparation.md) kan det vara bra att förstå en del av terminologin i systemet och dess grundläggande struktur innan du loggar in.

AEM as a Cloud Service är ett kraftfullt och flexibelt verktyg och för att kunna använda det bör du känna till hur det är organiserat och vilka termer och språk som används i det. I det här dokumentet sammanfattas några viktiga termer som du behöver förstå innan du börjar använda systemet.

När du har läst det här dokumentet bör du förstå

* De olika lager som utgör AEMaaCS.
* Grunderna i vad varje lager gör.

## AEMaaCS-struktur {#structure}

För denna introduktionsresa behövs ingen fullständig förståelse för AEM as a Cloud Service struktur. Men om du är bekant med följande koncept blir det enklare att följa med senare under resan.

![Cloud Manager-struktur](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **TENANT** - Alla kunder etableras med en klientorganisation. En hyresgäst kallas även IMS-organisation (mer på IMS senare under denna resa)
* **PROGRAM** - Varje klientorganisation har ett eller flera program som ofta återspeglar kundens licensierade lösningar.
* **MILJÖER** - Varje program har flera miljöer, till exempel produktion för direktinnehåll, en för mellanlagring och en för utvecklingsändamål.
* **REPOSITORY** - Miljöerna har en eller flera Git-databaser där program- och front end-kod bevaras.
* **VERKTYG OCH ARBETSFLÖDEN** - Pipelines hanterar distributionen av kod från databaserna till miljöerna.

Ett exempel är ofta användbart när hierarkin ska sammanställas.

* WKND Travel and Adventure Enterprises kan vara en **tenant** som fokuserar på reserelaterade medier.
* WKND Travel and Adventure Enterprises-klienten kan ha två **program**:
   * One Sites Program for its WKND Magazine division
   * Ett Assets-program för WKND Media Division
* Programmen WKND Magazine och WKND Media skulle båda ha **miljöerna för utveckling, staging och produktion**.
* **Databaser** används för att underhålla anpassad kod och program för WKND Magazine och WKND Media.
* Olika **verktyg och arbetsflöden** fungerar i alla rapporter för att distribuera kod med CI/CD-pipelines, åtkomstloggar, AEM och så vidare.

## What&#39;s Next {#what-is-next}

Nu när du har slutfört den här delen av AEM introduktionsresa bör du förstå:

* De olika lager som utgör AEMaaCS.
* Grunderna i vad varje lager gör.

Bygg vidare på den här kunskapen och fortsätt din AEM introduktionsresa genom att nästa läsning av dokumentet [Åtkomst till Admin Console](admin-console.md), där du får lära dig hur du kommer åt konsolen och verifierar din status som systemadministratör.
