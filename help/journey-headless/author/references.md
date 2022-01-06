---
title: Läs om hur du använder referenser i innehållsfragment
description: Lär dig hur du använder referenser i innehållsfragment, för innehåll, andra fragment och andra resurser (media). Lägg in behovet av och mekanismerna i kapslade fragment för Headless CMS Authoring.
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---

# Läs om hur du använder referenser i innehållsfragment {#author-headless-references}

## Story hittills {#story-so-far}

I början av [AEM Headless Content Author Journey](overview.md) den [Introduktion](introduction.md) har omfattat de grundläggande begrepp och termer som är relevanta för utvecklingen av headless.

Du har lärt dig grunderna i Headless CMS Authoring, med en introduktion till redigering med AEMaaCS och i synnerhet framtagning av Content Fragments.

Den här artikeln bygger vidare på dessa så att du förstår hur du använder referenser för att skapa ditt eget innehåll för ditt AEM headless-projekt.

## Syfte {#objective}

* **Målgrupp**: Avancerat
* **Syfte**: Introduktion till användning av referenser för Headless CMS Authoring. Vilka typer av referenser som finns tillgängliga, och vad är syftet med dem:

   * Innehållsreferenser
   * Resurs-/mediereferenser
   * Fragmentreferenser
   * Ad hoc-referenser inifrån ett textblock

## Vad är referenser? {#what-are-references}

Referenser är helt enkelt en mekanism för att koppla samman resurser, oavsett om det är annat innehåll, resurser (som i bilder) eller andra fragment. Även om de är mycket lika finns det vissa skillnader.

Vissa referenser har särskilda datatyper (till exempel Innehållsreferenser och Fragmentreferenser), medan andra bara läggs till som en referens i ett textblock (resursreferenser och ad hoc-referenser).

![Innehållsfragment - referenser](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Innehållsreferenser {#content-references}

Innehållsreferenser gör just det - de gör det möjligt att referera till annat innehåll. Då öppnas en webbläsare där du kan välja innehållsobjektet.

## Resurs-/mediereferenser {#assets-media-references}

Resurser (till exempel bilder eller media) kan refereras inom ett textblock med hjälp av **Infoga resurs** alternativ. Då öppnas en webbläsare där du kan välja resursen.

![Innehållsfragment - infoga resurs](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Fragmentreferenser {#fragment-references}

Fragmentreferenser gör det igen - de gör att du kan referera till ett annat fragment. Det här är viktigt och behöver en mer förklaring.

Du kan till exempel ha definierat följande modeller för innehållsfragment:

* Ort
* Företag
* Person
* Utmärkelser

Det verkar ganska okomplicerat, men ett företag har förstås både en koncernchef och anställda ....och dessa är alla människor, var och en definierade som en person.

Och en person kan ha en utmärkelse (eller kanske två).

* Mitt företag - Företag
   * VD - person
   * Medarbetare - person
      * Personliga utmärkelser - Utmärkelse

Och det är bara till att börja med. Beroende på komplexiteten kan en utmärkelse vara företagsspecifik eller ett företag ha sitt huvudkontor i en viss stad.

Att representera dessa inbördes relationer kan uppnås med Fragmentreferenser, så som de tolkas både av dig (författaren) och av rubrikfria program.

Som författare ansvarar du inte för att definiera dessa relationer (det gör innehållsarkitekten när du skapar innehållsfragmentmodellen), men du behöver veta hur du känner igen och redigerar referenserna.

<!--
![Content Modeling with Content Fragments](/help/journey-headless/developer/assets/headless-modeling-01.png "Content Modeling with Content Fragments")
-->

### Så här skapar du kapslade fragment {#author-nested-fragment}

Att skapa fragmentreferenser är ganska okomplicerat (men vanligtvis kommer fältet inte att märkas som **Fragmentreferens**). Du kan antingen skriva in referensen direkt eller (troligare) välja mappikonen för att öppna en webbläsare där du kan navigera och välja det fragment du behöver.

![Innehållsfragment - referenser](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

Definitionen av kontrollerna för innehållsfragmentmodellen:

* om du kan välja att lägga till flera referenser
* Modelltyper för innehållsfragment som du kan välja. I Content Fragment Model definieras de fragmentmodeller som tillåts för referensen, så AEM endast presenterar fragment som baseras på dessa modeller.

### Navigera i kapslade fragment {#navigate-nested-fragment}

Använda **Strukturträd** på fliken i redigeraren för innehållsfragment kan du navigera genom fragmenten som fragmentet refererar till och sedan genom eventuella referenser. Om du markerar en referens öppnas fragmentet för redigering.

>[!NOTE]
>
>Med hjälp av vägbeskrivningarna på huvudpanelen kan du gå tillbaka till startpunkten.

![Strukturträd för innehållsfragment](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Ad hoc-referenser {#adhoc-references}

Ad hoc-referenser kan läggas till som en enkel länk i ett textblock:

![Innehållsfragment - Ad hoc-referenser](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## What&#39;s Next {#whats-next}

Nu när du har lärt dig mer om referenser och struktur i innehållsfragment är nästa steg att [Läs mer om metadata och taggning](metadata-tagging.md). Då introduceras och diskuteras hur du kan definiera metadata och taggar för dina innehållsfragment.

## Ytterligare resurser {#additional-resources}

* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)

   * [Hantera innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md)

      * [Använd konfigurationen i resursmappen](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Skapa ett innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variationer - Skapa innehållsfragment](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)

      * [Modeller för innehållsfragment - datatyper](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modeller för innehållsfragment - egenskaper](/help/assets/content-fragments/content-fragments-models.md#properties)


* Komma igång-guider
   * [Skapa en startguide för en resursmapp utan rubrik](/help/implementing/developing/headless/getting-started/create-assets-folder.md)

* AEM Headless Content Architect Journey

* AEM Headless Translation Journey
