---
title: Namnkonventioner
description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Namnkonventioner{#naming-conventions}

Noderna i databasen omfattas av namnkonventioner i Java Content Repository. AEM lägger dock till ytterligare konventioner för sidnodernas namn.

## Namnkonventioner för sidor {#naming-conventions-for-pages}

Dessa namnkonventioner implementeras på olika nivåer:

* JcrUtil: aem av [JCR-verktygen](#jcr-utilities).
* PageManager: I [sidhanteraren](#page-manager) finns metoder för sidnivååtgärder.
* I AEM {#ui-behavior}

### JCR-verktyg {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) är den AEM implementeringen av JCR-verktygen. Det är särskilt intressant att validera namn om du kontrollerar teckenmappningar och följande valideringar:

* `isValidName`
   * Kontrollerar om namnet inte är tomt och bara innehåller giltiga tecken.
   * Kan användas för att kontrollera om ett föreslaget namn är giltigt.
* `createValidName`
   * Detta skapar en giltig etikett av en godtycklig sträng.
   * Den kan användas för att skapa ett namn från en titel.

### Page Manager {#page-manager}

[I PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) finns metoder för åtgärder på sidnivå som baseras på [JCRUtil](#jcr-utilities).

### AEM gränssnittsbeteende {#ui-behavior}

När AEM hanterar innehåll:

* Validerar namnet enligt de begränsningar som PageManager har när något av följande inträffar:
   * en sidrubrik tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn anges
