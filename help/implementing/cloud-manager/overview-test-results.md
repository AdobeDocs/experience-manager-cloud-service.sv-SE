---
title: Cloud Manager Tests - översikt
description: Få en översikt över de tre typer av tester som Cloud Manager automatiskt kör för att säkerställa kvaliteten på din anpassade kod.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Cloud Manager Tests - översikt {#overview}

Det finns tre testkategorier som stöds av pipelines i Cloud Manager för molntjänster.

1. [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md)

   * Kodkvalitetstestningen utvärderar kvaliteten på programkoden.
   * Kodkvalitetspipelinen utförs omedelbart efter byggsteget i alla icke-produktions- och produktionspipelinjer.
   * De [anpassade reglerna för kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md) som körs av Cloud Manager skapas baserat på bästa praxis från AEM Engineering.

1. [Funktionstestning](/help/implementing/cloud-manager/functional-testing.md)

   * Funktionstestning körs under testfasen i en [produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md). Den kan också köras under testfasen av en [icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) som inte är i produktion.

1. [Testning av Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   * Granskningstestning är aktiverat i alla Cloud Manager-produktionspipelines och kan inte hoppas över.

Dessa tester kan vara:

* Kundskriven
* Adobe-skriven
* Skapat med verktyg med öppen källkod

>[!NOTE]
>
> Både kundskrivna tester och Adobe-skrivna tester körs i en innesluten infrastruktur som är utformad för att köra sådana tester.
