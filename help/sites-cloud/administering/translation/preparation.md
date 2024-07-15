---
title: Förbereder innehåll för översättning
description: Lär dig hur du förbereder innehåll för översättning när du utvecklar flerspråkiga webbplatser.
feature: Language Copy
role: Admin
exl-id: afc577a2-2791-481a-ac77-468011e4302e
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Förbereder innehåll för översättning {#preparing-content-for-translation}

Flerspråkiga webbplatser har i allmänhet en viss mängd innehåll på flera språk. Webbplatsen är skriven på ett språk och sedan översatt till andra språk. Vanligtvis består flerspråkiga webbplatser av sidgrenar, där varje gren innehåller webbplatsens sidor på ett annat språk.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md), som är en guidad väg genom att översätta ditt AEM Sites-innehåll med hjälp av AEM kraftfulla översättningsverktyg, som är idealisk för dem som saknar AEM eller översättningsupplevelse.

Självstudiewebbplatsen [WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) innehåller flera språkgrenar och använder följande struktur:

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

Den språkkopia som du ursprungligen skapade webbplatsinnehållet för är språkinställningen. Språkmallsidan är källan som översätts till andra språk.

Varje språkgren på en webbplats kallas för en språkkopia. Rotsidan för en språkkopia, som kallas språkroten, identifierar språket för innehållet i språkkopian. `/content/wknd/fr` är till exempel språkroten för den franska språkkopian. Språkkopior måste använda en [korrekt konfigurerad språkrot](preparation.md#creating-a-language-root) så att rätt språk används när översättningar av en källplats utförs.

Gör så här för att förbereda webbplatsen för översättning:

1. Skapa språkroten för din språkinställning. Språkroten för den engelska WKND-demowebbplatsen är till exempel `/content/wknd/language-masters/en`. Kontrollera att språkroten är korrekt konfigurerad enligt informationen i [Skapa en språkrot](preparation.md#creating-a-language-root).
1. Skriv innehållet i din språkmaster.
1. Skapa språkroten för varje språkkopia för webbplatsen. Den franska språkkopian av WKND-exempelwebbplatsen är till exempel `/content/wknd/language-masters/fr`.

När du har förberett innehållet för översättning kan du automatiskt skapa saknade sidor i dina språkkopior och tillhörande översättningsprojekt. (Se [Skapa ett översättningsprojekt](managing-projects.md).) En översikt över innehållsöversättningsprocessen i AEM finns i [Översätta innehåll för flerspråkiga webbplatser](overview.md).

## Skapa en språkrot {#creating-a-language-root}

Skapa en språkrot som rotsida för en språkkopia som identifierar språket i innehållet. När du har skapat språkroten kan du skapa översättningsprojekt som innehåller språkkopian.

Om du vill skapa språkroten skapar du en sida och använder en ISO-språkkod som värde för egenskapen **Name**. Språkkoden måste ha något av följande format:

* `<language-code>` - Den språkkod som stöds är en kod med två bokstäver som definieras av ISO-639-1, till exempel `en`.
* `<language-code>_<country-code>` eller `<language-code>-<country-code>` - Den landskod som stöds är en kod med två bokstäver i gemener eller versaler enligt ISO 3166, till exempel `en_US`, `en_us`, `en_GB`, `en-gb`.

Du kan använda båda formaten enligt den struktur som du har valt för den globala platsen. Rotsidan för den franska språkkopian av WKND-webbplatsen har till exempel `fr` som **Name**-egenskap. Egenskapen **Name** används som namn på sidnoden i databasen och avgör därför sidans sökväg (`http://<host>:<4502>/content/wknd/language-masters/fr.html`).

1. Navigera till webbplatser.
1. Välj den webbplats som du vill skapa en språkkopia för.
1. Välj **Skapa** och välj sedan **Sida**.

   ![Skapa sida](../assets/create-page.png)

1. Markera sidmallen och välj sedan **Nästa**.
1. I fältet **Namn** skriver du landskoden i formatet `<language-code>` eller `<language-code>_<country-code>`, till exempel `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Skriv en rubrik för sidan.

   ![Skapa språkets rotsida](../assets/create-language-root.png)

1. Välj **Skapa**. I bekräftelsedialogrutan väljer du antingen **Klar** för att återgå till webbplatskonsolen eller **Öppna** för att öppna språkkopian.

## Se status för språkrötter {#seeing-the-status-of-language-roots}

AEM tillhandahåller en **Reference**-räl som visar en lista över språkrötter som har skapats.

![Språkrötter](../assets/language-roots.png)

Använd följande procedur för att visa språkkopiorna för en sida med hjälp av [spårväljaren](/help/sites-cloud/authoring/basic-handling.md#rail-selector).

1. På webbplatskonsolen markerar du en sida på webbplatsen och väljer sedan **Referenser**.

   ![Öppna referensfältet](../assets/opening-references-rail.png)

1. Välj **Språkkopior** i referensfältet. Rälsen visar webbplatsens språkkopior.

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
>Endast en nivå tillåts. Följande tillåter till exempel inte att sidan `es` tolkas som en språkkopia:
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`
>
> Denna `es`-språkkopia kommer inte att identifieras eftersom den ligger två nivåer (`americas/central-america`) utanför noden `en`.

>[!TIP]
>
>I sådana fall kan språkrörelser ha vilket sidnamn som helst, i stället för bara språkets ISO-kod. AEM kontrollerar alltid sökvägen och namnet först, men om sidnamnet inte identifierar något språk AEM egenskapen `cq:language` för sidan för att se om det finns en språkidentifiering.
