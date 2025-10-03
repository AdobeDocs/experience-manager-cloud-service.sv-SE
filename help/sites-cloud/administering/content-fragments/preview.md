---
title: Förhandsgranska innehållsfragment
description: Lär dig hur du förhandsgranskar innehållsfragment på flera olika sätt.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 42dbf6138920c4f733d7dc74dfc81504dee1e0ae
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---

# Förhandsgranska innehållsfragment {#previewing-content-fragments}

Innehållsfragment kan användas för både rubrikfri leverans och sidredigering. Eftersom fragmenten bara är innehåll, utan formatering, kan det vara en större utmaning att granska dem. Det finns alltså flera metoder för att förhandsgranska fragmenten, i en rad olika scenarier.

Det finns flera metoder för innehållsfragment som du kan nå från konsolfragmentskonsolen och redigeraren. Konsolen och redigeraren som beskrivs i det här avsnittet har utvecklats för headless-innehållsleverans (men de kan användas för alla scenarier).

Du kan förhandsgranska fragmentet:

* med URL-mönstret [Förhandsgranska](#preview-url-pattern)

* genom att publicera till och avpublicera från [förhandsgranskningsinstansen](#preview-instance)

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

>[!IMPORTANT]
>
>Du kan komma åt innehållsfragment från två konsoler: **Innehållsfragment** och **Assets**.
>
>Det finns också två redigerare för att skapa innehållsfragment. Även om de grundläggande funktionerna är desamma finns det vissa skillnader. Båda redigerarna är tillgängliga från båda konsolerna.
>
>I det här avsnittet behandlas konsolen **Innehållsfragment** och den *nya* innehållsfragmentsredigeraren. Dessa har utvecklats för leverans av headless-innehåll (även om de kan användas för alla scenarier)
>
>Mer information finns i:
>
>* användning av **Assets**-konsolen för [hantering av innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md)
>* användning av den [*ursprungliga* innehållsfragmentsredigeraren](/help/assets/content-fragments/content-fragments-variations.md),
>* använder [Innehållsfragment för sidredigering](/help/sites-cloud/authoring/fragments/content-fragments.md).

## Förhandsgranska URL-mönster {#preview-url-pattern}

Med redigeraren för innehållsfragment kan författare förhandsgranska sina redigeringar i ett externt klientprogram.

Om du vill använda den här funktionen måste du först:

* Samarbeta med IT-avdelningen och skapa ett externt klientprogram som återger innehållsfragmentet genom att använda JSON-utdata.

* När det externa klientprogrammet har konfigurerats måste URL-mönstret **Standardförhandsgranskning** definieras som en [egenskap för rätt innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties).

URL:en för förhandsgranskning bör följa detta mönster:

    `https://<preview_url>?param=${expression}`

Tillgängliga uttryck är:

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

När URL:en har definierats är knappen **[Förhandsgranska](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)** aktiv i det övre verktygsfältet i redigeraren. Du kan välja den här knappen om du vill starta det externa programmet (på en separat flik) för att återge innehållsfragmentet.

## Förhandsgranska instans {#preview-instance}

Du kan **publicera**, och **avpublicera**, ditt fragment till din Preview-instans (samt till din Publish-instans).

Du kan publicera fragmentet antingen från redigeraren eller konsolen.

Se:

* [Publicera och förhandsgranska ett fragment](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) för fullständig information.

* [Avpublicerar ett fragment](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) för fullständig information.

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
