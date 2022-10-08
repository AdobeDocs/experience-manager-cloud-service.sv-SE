---
title: Förbereder innehåll för översättning
description: Lär dig hur du förbereder innehåll för översättning.
feature: Language Copy
role: Admin
exl-id: afc577a2-2791-481a-ac77-468011e4302e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# Förbereder innehåll för översättning {#preparing-content-for-translation}

Flerspråkiga webbplatser har i allmänhet en viss mängd innehåll på flera språk. Webbplatsen är skriven på ett språk och sedan översatt till andra språk. Vanligtvis består flerspråkiga webbplatser av sidgrenar, där varje gren innehåller webbplatsens sidor på ett annat språk.

>[!TIP]
>
>Om du är nybörjare på att översätta innehåll kan du läsa [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

The [WKND självstudiewebbplats](/help/implementing/developing/introduction/develop-wknd-tutorial.md) innehåller flera språkgrenar och använder följande struktur:

```text
/content
    |- wknd
        |- language-masters
            |- en
            |- de
            |- es
            |- fr
            |- it
        |- us
            |- en
            |- es
        |- ca
            |- en
            |- fr
        |- ch
            |- de
            |- fr
            |- it
        |- de
            |- de
        |- fr
            |- fr
        |- es
            |- es
        |- it
            |- it
```

Den språkkopia som du ursprungligen skapade webbplatsinnehållet för är överordnad. Överordnad språk är källan som översätts till andra språk.

Varje språkgren på en webbplats kallas för en språkkopia. Rotsidan för en språkkopia, som kallas språkroten, identifierar språket för innehållet i språkkopian. Till exempel: `/content/wknd/fr` är språkroten för den franska språkkopian. Språkkopior måste använda [korrekt konfigurerad språkrot](preparation.md#creating-a-language-root) så att rätt språk används när översättningar av en källplats utförs.

Gör så här för att förbereda webbplatsen för översättning:

1. Skapa språkroten för din överordnad. Exempelvis är språkroten för den engelska demowebbplatsen WKND `/content/wknd/language-masters/en`. Kontrollera att språkroten är korrekt konfigurerad enligt informationen i [Skapa en språkrot](preparation.md#creating-a-language-root).
1. Skriv innehåll på ditt språk överordnad.
1. Skapa språkroten för varje språkkopia för webbplatsen. Exempelwebbplatsen för WKND innehåller t.ex. en fransk språkkopia `/content/wknd/language-masters/fr`.

När du har förberett innehållet för översättning kan du automatiskt skapa saknade sidor i dina språkkopior och tillhörande översättningsprojekt. (Se [Skapa ett översättningsprojekt](managing-projects.md).) En översikt över innehållsöversättningsprocessen i AEM finns i [Översätta innehåll för flerspråkiga webbplatser](overview.md).

## Skapa en språkrot {#creating-a-language-root}

Skapa en språkrot som rotsida för en språkkopia som identifierar språket i innehållet. När du har skapat språkroten kan du skapa översättningsprojekt som innehåller språkkopian.

Om du vill skapa språkroten skapar du en sida och använder en ISO-språkkod som värde för **Namn** -egenskap. Språkkoden måste ha något av följande format:

* `<language-code>` - Den språkkod som stöds är en kod med två bokstäver som definieras av ISO-639-1, till exempel `en`.
* `<language-code>_<country-code>` eller `<language-code>-<country-code>` - Den landskod som stöds är en kod med två bokstäver i gemener eller versaler enligt ISO 3166, till exempel `en_US`, `en_us`, `en_GB`, `en-gb`.

Du kan använda båda formaten enligt den struktur som du har valt för den globala platsen. Rotsidan för den franska språkkopian av WKND-webbplatsen har `fr` som **Namn** -egenskap. Observera att **Namn** används som namn på sidnoden i databasen och därför bestäms sidans sökväg (`http://<host>:<4502>/content/wknd/language-masters/fr.html`).

1. Navigera till webbplatser.
1. Klicka på eller tryck på den webbplats där du vill skapa en språkkopia.
1. Klicka eller tryck **Skapa** och sedan klicka eller trycka **Sida**.

   ![Skapa sida](../assets/create-page.png)

1. Välj sidmallen och klicka eller tryck sedan på **Nästa**.
1. I **Namn** fälttyp landskoden i formatet `<language-code>` eller `<language-code>_<country-code>`, till exempel `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Skriv en rubrik för sidan.

   ![Skapa språkets rotsida](../assets/create-language-root.png)

1. Klicka eller tryck **Skapa**. I bekräftelsedialogrutan klickar du på eller trycker på **Klar** för att gå tillbaka till Sites-konsolen, eller **Öppna** för att öppna språkkopian.

## Se status för språkrötter {#seeing-the-status-of-language-roots}

AEM tillhandahåller en **Referenser** som visar en lista med språkrötter som har skapats.

![Språkrötter](../assets/language-roots.png)

Använd följande procedur för att visa språkkopiorna för en sida med [järnvägsväljare.](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

1. Välj en sida på webbplatsen i webbplatskonsolen och klicka eller tryck sedan på **Referenser**.

   ![Räler för öppna referenser](../assets/opening-references-rail.png)

1. Klicka eller tryck på referenslisten **Språkkopior**. Rälsen visar webbplatsens språkkopior.

## Språkkopior på flera nivåer {#multiple-levels}

Språkrötter kan också grupperas under noder, till exempel efter region, samtidigt som de fortfarande identifieras som rötter i språkkopior.

```text
/content
    |- wknd
        |- language-masters
            |- europe
                |- de
                |- fr
                |- it
                |- es
                ]- pt
            |- americas
                |- en
                |- es
                |- fr
                |- pt
            |- asia
                |- ...
            |- africa
                |- ...
            |- oceania
                |- ...
        |- europe
        |- americas
        |- asia
        |- africa
        |- oceania            
```

>[!NOTE]
>
>Endast en nivå tillåts. Följande tillåter till exempel inte `es` sida som ska tolkas som en språkkopia:
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`
>
> Detta `es` språkversionen identifieras inte eftersom den är 2 nivåer (`americas/central-america`) bort från `en` nod.

>[!TIP]
>
>I sådana fall kan språkrörelser ha vilket sidnamn som helst, i stället för bara språkets ISO-kod. AEM kontrollerar alltid sökvägen och namnet först, men om sidnamnet inte identifierar något språk AEM kontrollerar `cq:language` sidegenskapen för språkidentifieringen.
