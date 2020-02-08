---
title: Använda taggar
description: Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Använda taggar {#using-tags}

Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats. Taggar kan ses som nyckelord eller etiketter som kan bifogas till en sida, en resurs eller annat innehåll för att göra det möjligt att söka efter innehållet och relaterat innehåll.

* Mer information om hur du skapar och hanterar taggar samt vilka innehållstaggar som har tillämpats finns i Administrera taggar. <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.-->
* Mer information om taggningsramverket samt om hur du inkluderar och utökar taggar i anpassade program finns i Tagga för utvecklare. <!-- See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.-->

## Tio skäl att använda märkord {#ten-reasons-to-use-tagging}

1. **Ordna innehåll** - Taggning gör livet enklare för författare eftersom de snabbt kan ordna innehåll utan ansträngning.
1. **Ordna taggar** - När taggar organiserar innehåll organiserar hierarkiska taxonomier/namnutrymmen taggar.
1. **Djupt organiserade taggar** - Med möjlighet att skapa taggar och undertaggar blir det möjligt att uttrycka hela taxonomiska system, som omfattar termer, undertermer och deras relationer. Detta gör att en andra (eller tredje) innehållshierarki kan skapas parallellt med den officiella.
1. **Kontrollerad taggning** - Du kan styra taggningen genom att lägga till behörigheter till taggar och/eller namnutrymmen för att styra hur taggar skapas och används.
1. **Flexibel taggning** - Taggar har många namn och ansikten: taggar, taxonomitermer, kategorier, etiketter och mycket annat. De är flexibla i sin innehållsmodell och i hur de kan användas. om du t.ex. anger målgrafik, kategoriserar och klassificerar innehåll eller skapar en sekundär innehållshierarki.
1. **Förbättrad sökning** - I standardsökkomponenten i AEM ingår i stort sett skapade taggar och tillämpade taggar som du kan använda filter på för att begränsa resultaten till de som är relevanta.
1. **SEO-aktivering** - Taggar som används som sidegenskaper visas automatiskt i de metataggar på sidan som gör den synlig för sökmotorer.
1. **Enkel sofistikering** - Du kan helt enkelt skapa taggar från ett ord med en knapptryckning. Därefter kan en titel, beskrivning och ett obegränsat antal etiketter läggas till för att ge taggen mer semantik.
1. **Core Consistency** - Taggningssystemet är en huvudkomponent i AEM och används av alla AEM-funktioner för att kategorisera innehåll. Programmeringsgränssnittet för taggning är även tillgängligt för utvecklare som skapar taggningsaktiverade program med tillgång till samma taxonomier.
1. **Kombinerar struktur och flexibilitet** - AEM är idealiskt för att arbeta med strukturerad information på grund av inkapsling av sidor och banor. Det är lika kraftfullt när du arbetar med ostrukturerad information på grund av den inbyggda textsökningen. Taggning kombinerar styrkan hos både strukturen och flexibiliteten.

När du utformar innehållsstrukturen för en plats och metadatarammet för resurser bör du tänka på att taggningen är enkel och tillgänglig.

## Tillämpar taggar {#applying-tags}

I redigeringsmiljön kan författare lägga till taggar genom att gå till sidegenskaperna och ange en eller flera taggar i fältet **Taggar/nyckelord** .

Om du vill använda fördefinierade taggar använder du fältet **Taggar** och fönstret **Markera taggar** i fönstret **Sidegenskaper** . Fliken **Standardtaggar** är standardnamnutrymmet, vilket innebär att det inte finns något `namespace-string:` prefix till taxonomin. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![Markera flera taggar](/help/sites-cloud/authoring/assets/tags-select.png)

## Publiceringstaggar {#publishing-tags}

På samma sätt som du kan publicera och avpublicera sidor kan du göra följande med taggar och namnutrymmen:

### Aktivera {#activate}

* Aktivera enskilda taggar.

   Precis som för sidor måste nyligen skapade taggar aktiveras innan de blir tillgängliga i publiceringsmiljön.

>[!NOTE]
>
>När du aktiverar en sida öppnas en dialogruta automatiskt där du kan aktivera oaktiverade taggar som tillhör sidan.

### Inaktivera {#deactivate}

* Inaktivera de markerade taggarna.
