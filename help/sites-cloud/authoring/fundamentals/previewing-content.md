---
title: Förhandsgranska innehåll
description: Lär dig hur du använder AEM Preview Service för att förhandsgranska innehåll innan du publicerar.
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Förhandsgranska innehåll {#previewing-content}

>[!NOTE]
>
>Förhandsgranskningsfunktionen ingår i version 2021.5.0 och kommer att lanseras gradvis under de kommande veckorna.

AEM har en Site Preview Service som är avsedd att låta utvecklare och skribenter förhandsgranska en webbplats innan den når publiceringsmiljön och är tillgänglig för allmänheten.

Det underlättar förhandsgranskning av sidupplevelser som annars inte skulle vara synliga i redigeringsmiljön, som sidövergångar och annat innehåll på publiceringssidan.

## Publicerar innehåll för förhandsgranskning {#publishing-content-to-preview}

Du kan publicera innehåll till förhandsgranskningstjänsten med hjälp av gränssnittet för hanterade publikationer på följande sätt:

1. Markera den eller de sidor du vill skicka för förhandsgranskning i webbplatskonsolen och klicka på knappen **Hantera publikation**
1. I följande guide väljer du **Förhandsgranska** som mål

   ![hanterad publikation](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Klicka på **Nästa** och **Publicera** för att bekräfta.

Förhandsgranskningsinnehållet visas. Lägg till **förhandsgranskning** i publicerings-URL:en för produktionsinstansen. URL:en ska utformas så här:

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

Mer information om hur du hämtar URL:er för dina miljöer finns i [Hantera dina miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en).

