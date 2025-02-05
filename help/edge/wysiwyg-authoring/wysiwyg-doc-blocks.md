---
title: Block för WYSIWYG och dokumentbaserad redigering
description: Lär dig hur du kan skapa block som kan användas både för WYSIWYG-redigering och dokumentbaserad redigering.
feature: Edge Delivery Services
role: User
exl-id: f039c70a-e1a0-4fcc-8f42-dfa0f8bb3764
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Block för WYSIWYG och dokumentbaserad redigering {#wysiwyg-and-doc-blocks}

Lär dig hur du kan skapa block som kan användas både för WYSIWYG-redigering och dokumentbaserad redigering.

## Ökning {#overview}

I vissa projekt kanske du vill ha stöd för både [WYSIWYG-redigering med den universella redigeraren](/help/edge/wysiwyg-authoring/authoring.md) och [dokumentbaserad redigering](/help/edge/docs/authoring.md). För att minimera utvecklingstiden och säkerställa samma webbplatsupplevelse kan du skapa en uppsättning block som har stöd för båda användningsfallen.

För att göra detta måste du använda samma innehållsmodelleringsmetod för både WYSIWYG-redigeringsprogrammet och dokumentbaserade redigeringsprogram.

## Metod {#approach}

I WYSIWYG-redigering i AEM [deklarerar du en modell](/help/edge/wysiwyg-authoring/content-modeling.md) och anger namnkonventioner. Data återges sedan i tabellliknande blockstrukturer med Edge Delivery på samma sätt som om tabellen skulle ha skapats manuellt med dokumentbaserad redigering.

För att uppnå detta görs vissa antaganden, t.ex. för ett enkelt block som ett teaser, om att alla egenskaper och grupper av egenskaper återges i 1.n rader med en enda kolumn var. För block som har 1..I objekt (till exempel karusell och kort) läggs objekten till efter dessa rader med en rad vardera och en kolumn för varje egenskap/grupp med egenskaper.

Om du använder samma sätt för dokumentbaserad redigering kan du återanvända dina WYSIWYG-block.
