---
title: Namnkonventioner
description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Namnkonventioner{#naming-conventions}

Noderna i databasen omfattas av namnkonventioner i Java Content Repository. AEM lägger dock till ytterligare konventioner för sidnodernas namn.

## Namnkonventioner för sidor {#naming-conventions-for-pages}

Dessa namnkonventioner implementeras på olika nivåer:

* JcrUtil: den AEM implementeringen av [JCR-verktyg](#jcr-utilities).
* PageManager: [Sidhanteraren](#page-manager) innehåller metoder för åtgärder på sidnivå.
* I AEM {#ui-behavior}

### JCR-verktyg {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) är den AEM implementeringen av de gemensamma teknikverktygen. Det är särskilt intressant att validera namn om du kontrollerar teckenmappningar och följande valideringar:

* `isValidName`
   * Kontrollerar om namnet inte är tomt och bara innehåller giltiga tecken.
   * Kan användas för att kontrollera om ett föreslaget namn är giltigt.
* `createValidName`
   * Detta skapar en giltig etikett av en godtycklig sträng.
   * Den kan användas för att skapa ett namn från en titel.

### Sidhanteraren {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) innehåller metoder för sidnivååtgärder, baserade på [JCRUtil](#jcr-utilities).

### AEM gränssnittsbeteende {#ui-behavior}

När AEM hanterar innehåll:

* Validerar namnet enligt de begränsningar som PageManager har när något av följande inträffar:
   * en sidrubrik tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn har angetts
