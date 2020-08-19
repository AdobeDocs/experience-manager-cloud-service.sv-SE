---
title: Översikt över testresultat - Cloud Services
description: Översikt över testresultat - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 16%

---


# Översikt {#overview}

Körningar av pipeline för Cloud Manager för Cloud Services stöder körning av tester som körs mot mellanlagringsmiljön. Detta är i motsats till tester som körs under steget Skapa och Enhetstestning som körs offline, utan åtkomst till någon AEM miljö som körs.

Det finns tre olika testkategorier som stöds av Cloud Manager för Cloud Services i pipeline:

1. [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md)
1. [Funktionstestning](/help/implementing/cloud-manager/functional-testing.md)
1. [Testning av innehållsgranskning](/help/implementing/cloud-manager/content-audit-testing.md)

Dessa tester kan vara:

* Kundskriven
* Adobe-skriven
* Verktyg med öppen källkod (från Google)

   >[!NOTE]
   > Både kundskrivna tester och Adobe-skrivna tester körs i en containerinfrastruktur som är utformad för att köra dessa typer av tester.

