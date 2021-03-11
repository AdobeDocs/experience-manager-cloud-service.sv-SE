---
title: Program- och programtyper
description: Program- och programtyper - Cloud Services
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# Förstå program och programtyper {#understanding-programs}

I Cloud Manager har du klientorganisationen högst upp som kan ha flera program inuti. Varje program får inte innehålla mer än en produktionsmiljö och flera icke-produktionsmiljöer.

I följande diagram visas hierarkin för enheter i Cloud Manager.

![bild](assets/program-types1.png)

## Programtyper {#program-types}

En användare kan skapa en **sandlåda** eller ett **Production**-program.

* Ett *produktionsprogram* skapas för att aktivera livstrafik vid rätt tidpunkt i framtiden.
Mer information finns i [Introduktion till produktionsprogram](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md).


* Ett *sandlådeprogram* skapas vanligtvis för att användas i utbildningssyfte, köra demo, aktivering, POC eller dokumentation. Den är inte avsedd att transportera livstrafik och kommer att ha begränsningar som ett produktionsprogram inte kommer att ha. Den kommer att innehålla Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en Dev-miljö och en icke-produktionsprocess.
Mer information finns i [Introduktion till sandlådeprogram](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).

