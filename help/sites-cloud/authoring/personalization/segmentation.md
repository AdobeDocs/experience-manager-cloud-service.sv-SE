---
title: Förstå segmentering
description: Segmentering är en viktig faktor när man skapar en kampanj
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# Förstå segmentering {#understanding-segmentation}

Segmentering är en viktig faktor när man skapar en kampanj. I de flesta fall måste ni ha definierade segment innan ni kan påbörja kampanjen.

Besökare har olika intressen och mål när de besöker en webbplats. Att förstå dessa mål och uppfylla förväntningarna är en viktig framgångsrik faktor för onlinemarknadsföring.

Segmentering hjälper till att uppnå detta genom att analysera och karakterisera besökarens:

* Aktivitet på webbplatsen
* Profil
* Aktivitet på andra webbplatser

Innehållet kan sedan anpassas specifikt efter besökarens behov och intressen beroende på vilket segment de matchar.

## Använda segmentering {#using-segmentation}

Segment definieras i Konfigurera segmentering. De används för att styra det faktiska innehåll som ses av en viss målgrupp.<!--Segments are defined in [Configuring Segmentation](/help/sites-administering/campaign-segmentation.md). They are used to steer the actual content seen by a specific target audience.-->

## Segmenteringsterminologi {#segmentation-terminology}

Vid diskussion av segmentering används följande terminologi:

* **Besökare**  - En besökare är en person som besöker en webbplats. Personens besök börjar oftast från en hänvisande sida och går sedan vidare till en eller flera sidvisningar på din egen webbplats. En beteendeprofil kan skapas utifrån detaljerna från den personens besök.
* **Användare**  - En användare är en besökare som registrerar sig hos webbplatsen för att få en kontoprofil. För att generera en profil kan de tillhandahålla ytterligare identifiering, till exempel en e-postadress och ett kön, bland annat. Ytterligare information kan också samlas in, bland annat om communityaktiviteter och köpmönster. Baserat på informationen i profilen kan en demografisk profil skapas.
* **Trait**  - En egenskap eller egenskap hos en besökare som kan användas för att bestämma medlemskap i ett visst segment.
* **Segment**  - Ett segment är en samling besökare som delar vissa egenskaper. Segmenten bör vara distinkta, med ett minimum av överlappning med andra segment.
* **Beteenden**  - Beteenden är sådana som relaterar till besökarens beteende på webbplatsen. Bland dessa finns:
   * Intresset på er webbplats; inklusive besökta sidor och köpta produkter
   * Intresse för den webbplats som refererar. inklusive söktermer som används eller annonser som klickats på
   * Intresse av andra anläggningar. med verktyg som Spyjax
   * Besökarlojalitet; besökets längd, besöksfrekvens
* **Demografiska egenskaper**  - Dessa är utvalda populationsegenskaper, inklusive:
   * Ålder
   * Inkomst
   * Familjestorlek
   * Civilstånd
   * Kön
   * Plats
* **Härledda egenskaper**  - Vissa demografiska egenskaper är svåra att fastställa utan registrering, men kan härledas genom en kombination av beteendemässiga och demografiska egenskaper.
   * Om du t.ex. kombinerar den refererande URL:en (som en beteendeegenskap) med demografiska data (som hämtats från verktyg som [Google Ad Planner](https://www.google.com/adplanner/)) kan webbplatsägarna få demografiska egenskaper för sina besökare.
* **Delsegment**  - Ett segment kan delas upp i flera delsegment. Detta görs genom att definiera ytterligare egenskaper.
* **Teaser Page**  - En teaser page är riktad mot en viss målgrupp. Den innehåller återanvändbart innehåll som kan användas i det underordnade stycket.
* **Campaign**  - En kampanj är en samling med interaktiva sidor och e-postmarknadsföringssidor, som nyhetsbrev och inbjudningar. En kampanj körs vanligtvis under en begränsad period och ersätts av en annan kampanj.
* **Teaser Paragraph**  - Det här är ett stycke som hämtar innehåll från en annan sida beroende på en markeringsstrategi. Denna urvalsstrategi kan ta segment och kampanjer i beaktande.
* **Lista**  - En lista extraheras från ett segment med registrerade användare. Den plats som t.ex. används för att styra innehållet i det traderande stycket.
