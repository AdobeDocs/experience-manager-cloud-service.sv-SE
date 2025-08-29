---
title: Felsökning 502 Fel i anpassad överföringsåtgärd för adaptiv Forms
description: Lär dig hur du identifierar och åtgärdar 502 felsidor som inträffar när du använder anpassade skicka-åtgärder i Adaptive Forms (Core Components). I den här handboken förklaras vanliga orsaker, t.ex. ohanterade undantag, samt lösningssteg.
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Felsökning: Felsida 502 i anpassad överföringsåtgärd

När du arbetar med Adaptive Forms (Core Components) kan du stöta på en **502-felsida, HTML**, efter att du har skickat in ett formulär som använder en anpassad sändningsåtgärd.

## Problem

**Fel:** En felsida på 502 HTML visas när en anpassad sändningsåtgärdstjänst misslyckas.

**Orsak:** Detta händer om den anpassade åtgärden för att skicka genererar ett ohanterat fel, till exempel null-pekare, ogiltigt API-svar eller körningsfel.

## Upplösning

För att förhindra felsidan på 502 kapslar du in logiken med try-catch-block för att hantera fel på ett smidigt sätt.

Detaljerade steg finns i [Skapa en anpassad sändningsåtgärd för adaptiva Forms (kärnkomponenter)](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md).
