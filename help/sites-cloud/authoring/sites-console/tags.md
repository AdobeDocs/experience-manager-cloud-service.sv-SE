---
title: Använda taggar
description: Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats
exl-id: d2a9f578-fe0a-48ea-851c-2c84463661e0
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 6%

---

# Använda taggar {#using-tags}

Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats. Taggar kan ses som nyckelord eller etiketter som kan bifogas till en sida, en resurs eller annat innehåll för att göra det möjligt att söka efter innehållet och relaterat innehåll.

* Mer information om hur du skapar och hanterar taggar och till vilka innehållstaggar har tillämpats finns i [Administrera taggar](/help/sites-cloud/administering/tags.md) .
* Mer information om taggningsramverket och hur du inkluderar och utökar taggar i anpassade program finns i [Tagga för utvecklare](/help/implementing/developing/introduction/tagging-framework.md).

## Tio skäl att använda märkord {#ten-reasons-to-use-tagging}

1. **Ordna innehåll** - Med taggning blir livet enklare för författare eftersom de snabbt kan ordna innehåll utan ansträngning.
1. **Ordna taggar** - Medan taggar organiserar innehåll organiserar hierarkiska taxonomier/namnutrymmen taggar.
1. **Djupt organiserade taggar** - Med möjlighet att skapa taggar och undertaggar blir det möjligt att uttrycka hela taxonomiska system, som omfattar termer, undertermer och deras relationer. Detta gör att en andra (eller tredje) innehållshierarki kan skapas parallellt med den officiella.
1. **Kontrollerad taggning** - Du kan styra taggningen genom att tillämpa behörigheter på taggar och/eller namnutrymmen för att styra hur taggar skapas och används.
1. **Flexibel taggning** - Taggar har många namn och ansikten: taggar, taxonomitermer, kategorier, etiketter och mycket annat. De är flexibla i sin innehållsmodell och i hur de kan användas, t.ex. när måldemografi kontureras, kategoriseras och klassificeras innehåll eller när en sekundär innehållshierarki skapas.
1. **Förbättrad sökning** - Standardsökkomponenten i AEM innehåller i stort sett skapade taggar och tillämpade taggar som kan användas för att begränsa resultaten till de som är relevanta.
1. **SEO-aktivering** - Taggar som används som sidegenskaper visas automatiskt i de metataggar på sidan som gör den synlig för sökmotorer.
1. **Enkel sofistikering** - Du kan skapa taggar från ett ord och trycka på en knapp. Därefter kan en titel, beskrivning och ett obegränsat antal etiketter läggas till för att ge taggen mer semantik.
1. **Kärnkonsekvens** - Taggsystemet är en huvudkomponent i AEM och används av alla AEM funktioner för att kategorisera innehåll. Programmeringsgränssnittet för taggning är även tillgängligt för utvecklare som skapar taggningsaktiverade program med tillgång till samma taxonomier.
1. **Kombinerar struktur och flexibilitet** - AEM är idealiskt för arbete med strukturerad information på grund av inkapsling av sidor och sökvägar. Det är lika kraftfullt när du arbetar med ostrukturerad information på grund av den inbyggda textsökningen. Taggning kombinerar styrkan hos både strukturen och flexibiliteten.

När du utformar innehållsstrukturen för en plats och metadatarammet för resurser bör du tänka på att taggningen är enkel och tillgänglig.

## Tillämpar taggar {#applying-tags}

I redigeringsmiljön kan författare lägga till taggar genom att gå till sidegenskaperna och ange en eller flera taggar i fältet **Taggar/nyckelord**.

Om du vill använda fördefinierade taggar använder du fältet **Taggar** och fönstret **Markera taggar** i fönstret **Sidegenskaper**. Fliken **Standardtaggar** är standardnamnutrymmet, vilket innebär att taxonomin inte har prefixet `namespace-string:`. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![Markera flera taggar](/help/sites-cloud/authoring/assets/tags-select.png)

## Publiceringstaggar {#publishing-tags}

På samma sätt som du kan publicera och avpublicera sidor kan du göra följande med taggar och namnutrymmen:

### Aktivera {#activate}

* Aktivera enskilda taggar.

  Precis som med sidor måste skapade taggar aktiveras innan de blir tillgängliga i publiceringsmiljön.

>[!NOTE]
>
>När du aktiverar en sida öppnas en dialogruta automatiskt där du kan aktivera oaktiverade taggar som tillhör sidan.

### Inaktivera {#deactivate}

* Inaktivera de markerade taggarna.
