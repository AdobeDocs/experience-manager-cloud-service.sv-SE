---
title: Anpassa användargränssnittet
description: Lär dig mer om de olika tilläggspunkterna som gör att du kan anpassa gränssnittet i den universella redigeraren efter innehållsförfattarnas behov.
source-git-commit: 65893c0c0dee37bed8ecfbb06a12e7c093c4397c
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# Anpassa användargränssnittet {#customizing-ui}

Lär dig mer om de olika tilläggspunkterna som gör att du kan anpassa gränssnittet i den universella redigeraren efter innehållsförfattarnas behov.

## Inaktiverar publicering {#disable-publish}

Vissa redigeringsarbetsflöden kräver att innehållet granskas innan det publiceras. I sådana fall bör alternativet att publicera inte vara tillgängligt för någon författare.

The **Publicera** kan därför inaktiveras helt i en app genom att följande metadata läggs till.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
