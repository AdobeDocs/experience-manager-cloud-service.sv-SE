---
title: Program- och programtyper
description: Program- och programtyper - molntjänster
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# Förstå program och programtyper {#understanding-programs}

I Cloud Manager har du klientorganisationen högst upp som kan ha flera program inuti.  Varje program får inte innehålla mer än en produktionsmiljö och flera icke-produktionsmiljöer.

I följande diagram visas hierarkin för enheter i Cloud Manager.

![image](assets/program-types1.png)

## Programtyper {#program-types}

En användare kan skapa en **sandlåda** eller ett **vanligt** program.

En *sandlåda* skapas vanligtvis för utbildning, körning av demo, aktivering, POC eller dokumentation. Den är inte avsedd att transportera livstrafik och kommer att ha begränsningar som ett reguljärt program inte kommer att ha. Den kommer att innehålla Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en Dev-miljö och en icke-produktionsprocess.

Ett *Regelbundet program* skapas för att möjliggöra livstrafik vid rätt tidpunkt i framtiden.