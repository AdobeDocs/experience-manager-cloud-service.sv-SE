---
title: Översikt över testresultat - Cloud Services
description: Översikt över testresultat - Cloud Services
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Översikt {#overview}

Det finns tre olika testkategorier som stöds av Cloud Manager för Cloud Services i pipeline:

1. [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md)

   Kodkvalitetstestningen utvärderar kvaliteten på programkoden. Ledningen Code-Quality utförs omedelbart efter byggsteget i alla icke-produktions- och produktionspipelinjer.

   De regler [för](/help/implementing/cloud-manager/custom-code-quality-rules.md) anpassad kodkvalitet som körs av Cloud Manager skapas baserat på bästa praxis från AEM.

1. [Funktionstestning](/help/implementing/cloud-manager/functional-testing.md)

   Funktionstestningen är en del av scentestningsfasen i en produktionspipeline.

1. [Testning av innehållsgranskning](/help/implementing/cloud-manager/content-audit-testing.md)

   Testning av innehållsgranskning är aktiverat i alla produktionsförlopp för Cloud Manager och kan inte hoppas över.

Dessa tester kan vara:

* Kundskriven
* Adobe-skriven
* Verktyget Open Source

   >[!NOTE]
   > Både kundskrivna tester och Adobe-skrivna tester körs i en containerinfrastruktur som är utformad för att köra dessa typer av tester.

