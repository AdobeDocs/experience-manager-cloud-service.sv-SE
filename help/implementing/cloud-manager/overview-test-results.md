---
title: Översikt över testning av Cloud Manager
description: Få en översikt över de tre typer av tester som Cloud Manager automatiskt kör för att säkerställa kvaliteten på din anpassade kod.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Översikt över testning av Cloud Manager {#overview}

Det finns tre testkategorier som stöds av Cloud Manager för rörledningar för Cloud Service.

1. [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md)

   * Kodkvalitetstestningen utvärderar kvaliteten på programkoden.
   * Kodkvalitetspipelinen utförs omedelbart efter byggsteget i alla icke-produktions- och produktionspipelinjer.
   * The [regler för anpassad kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md) som körs av Cloud Manager skapas baserat på bästa praxis från AEM Engineering.

1. [Funktionstestning](/help/implementing/cloud-manager/functional-testing.md)

   * Funktionstestning är en del av testfasen i ett [produktionsflöde](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) och eventuellt en del av testfasen i [rörledning för icke-produktion](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

1. [Testning av Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md)

   * Experience Audit-testning är aktiverat i alla produktionspipelines i Cloud Manager och kan inte hoppas över.

Dessa tester kan vara:

* Kundskriven
* Adobe-skriven
* Skapat med verktyg med öppen källkod

>[!NOTE]
>
> Både kundskrivna tester och Adobe-skrivna tester körs i en containerinfrastruktur som är utformad för att köra sådana tester.
