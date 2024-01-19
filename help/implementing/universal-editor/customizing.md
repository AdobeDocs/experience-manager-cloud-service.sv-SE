---
title: Anpassa användargränssnittet
description: Lär dig mer om de olika tilläggspunkterna som gör att du kan anpassa gränssnittet i den universella redigeraren efter innehållsförfattarnas behov.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
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
