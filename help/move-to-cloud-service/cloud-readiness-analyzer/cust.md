---
title: Anpassning identifierad
description: Anpassning identifierad
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---


# Anpassning identifierad {#cust-pattern}

Den här sidan beskriver koden för mönstret Anpassning upptäckt.

## Bakgrund {#background}

Den här mönsterkoden används för att identifiera anpassningar som har gjorts i AEM-instansen. Eftersom det är vanligt att anpassa AEM betyder mönstret inte nödvändigtvis att det finns ett problem. Här anges en förteckning över anpassningar så att de kan utvärderas med avseende på deras inverkan på uppgraderingsplaner.

Några av de anpassningar som identifieras:

* Kundkod (paket) och konfigurationer
* Tredjepartspaket
* Integrering med tredjepartstjänster
* Icke-standardiserade ekindexvärden

## Mönsterdata {#pattern-data}

Följande objekt ingår i JSON-representationen av mönstret:

* **item.message**: refererar till mönstrets meddelande.
* **item.context**: hänvisar till ytterligare information om översiktsinformationen:
   * *typ*: customization.discover.
   * *data*: Ett JSON-objekt som innehåller data som beskriver anpassningen

### Möjliga konsekvenser och risker {#possible-implications}

Ej relevant.

### Möjliga lösningar  {#possible-solutions}

Ej relevant.
