---
title: Hur lägger jag till hjälptext AEM adaptiva Forms-fält?
description: Med AEM Forms kan du lägga till sammanhangsberoende hjälp i anpassade formulärfält och paneler, som text eller multimedia, inklusive videor.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# Sammanhangsberoende hjälp för formulärfält{#authoring-in-context-help-for-form-fields}

## Introduktion {#introduction}

Det finns situationer när slutanvändare som fyller i ett formulär inte vet hur de ska fylla i information i ett visst formulärfält. För att åtgärda sådana problem har Adaptive Forms stöd för att lägga till text eller sammanhangsberoende hjälp i ett formulärfält. Det underlättar ifyllandet av formulär och undviker eventuella tvetydigheter för slutanvändarna.

I den här artikeln beskrivs hur formulärförfattare kan lägga till sammanhangsberoende hjälp när de skriver Adaptiv Forms.

## Lägg till sammanhangsberoende hjälp {#add-in-context-help}

Du kan ange sammanhangsberoende hjälp med följande alternativ i hjälpavsnittet på egenskapsfliken i sidofältet.

* [Kort beskrivning](authoring-in-field-help.md#p-short-description-p)
* [Lång beskrivning](authoring-in-field-help.md#p-long-description-p)

![Kontexthjälp för formulärfält](assets/descriptions.png)

>[!NOTE]
>
>Long description åsidosätter Short description. Om du har angett båda visas bara Lång beskrivning.

### Kort beskrivning {#short-description}

Fältet Kort beskrivning ger snabba och korta tips om hur du fyller i ett formulärfält. Texten som anges i fältet Kort beskrivning visas som ett verktygstips när du håller muspekaren över fältet.

![Kort beskrivning för att lägga till sammanhangsberoende hjälp för formulärfält](assets/tooltip.png)

>[!NOTE]
>
>Välj **Visa alltid kort beskrivning** för att permanent visa hjälptexten under fältet.

![Permanent kort sammanhangsberoende hjälp nedanför fältet](assets/short1.png)

### Lång beskrivning {#long-description}

Du kan använda fältet Lång beskrivning för att ange lång text eller bädda in multimedieinnehåll, inklusive videor, som sammanhangsberoende hjälp. I följande bild visas hur du kan bädda in en video som sammanhangsberoende hjälp.

![Lägga till multimedia som sammanhangsberoende hjälp för formulärfält](assets/long-descriptions.png)

Om du lägger till lång beskrivning visas en **?** -ikonen bredvid fältet. När du klickar på ikonen visas det innehåll som lagts till i avsnittet med lång beskrivning.

![Exempel på sammanhangsberoende multimediahjälp](assets/photoshop.png)

### Hjälp på panelnivå {#panel-level-help}

Utöver sammanhangsberoende hjälp för formulärfält kan du ange hjälp på panelnivå på fliken Hjälpinnehåll i dialogrutan Redigera i panelen.

![Lägga till sammanhangsberoende hjälp för en formulärpanel](assets/panel-level-help.png)

Om du lägger till hjälp för panelen visas en **?** -ikonen bredvid panelbeskrivningen. När du klickar på ikonen visas det innehåll som lagts till i hjälpdelen i dialogrutan Redigera i panelen.

![Exempel på sammanhangsberoende hjälp på formulärpanelsnivå](assets/photoshop-1.png)

>[!MORELIKETHIS]
>
>* [Lägga till platshållartext i formulärfält](/help/forms/placeholder-text-in-aem-forms.md)
>* [Lägg till fotnot i ett anpassat formulär för formaterad text](/help/forms/footnotes-richtextsupport.md)