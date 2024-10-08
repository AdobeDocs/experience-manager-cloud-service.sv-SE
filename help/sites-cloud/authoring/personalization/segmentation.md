---
title: Förstå segmentering
description: Segmentering är en viktig faktor när man skapar en kampanj
exl-id: 36a9623a-bb19-498a-a0e9-ef80582b1fcf
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Förstå segmentering {#understanding-segmentation}

Segmentering är en viktig faktor när man skapar en kampanj. I de flesta fall måste du ha definierat segment innan du kan starta kampanjen.

Besökare har olika intressen och mål när de besöker en webbplats. Att förstå dessa mål och uppfylla förväntningarna är en viktig framgångsrik faktor för onlinemarknadsföring.

Segmentering hjälper till att uppnå detta genom att analysera och karakterisera besökarens:

* Aktivitet på webbplatsen
* Profil
* Aktivitet på andra webbplatser

Innehållet kan sedan anpassas specifikt efter besökarens behov och intressen beroende på vilket segment de matchar.

## Använda segmentering {#using-segmentation}

Segment definieras i Konfigurera segmentering. De används för att styra det faktiska innehåll som ses av en specifik målpublik.<!--Segments are defined in [Configuring Segmentation](/help/sites-administering/campaign-segmentation.md). They are used to steer the actual content seen by a specific target audience.-->

## Segmenteringsterminologi {#segmentation-terminology}

Vid diskussion av segmentering används följande terminologi:

* **Besökare** - En besökare är en person som besöker en webbplats. Personens besök börjar oftast från en hänvisande sida och går sedan vidare till en eller flera sidvisningar på din egen webbplats. En beteendeprofil kan skapas utifrån detaljerna från den personens besök.
* **Användare** - En användare är en besökare som registrerar sig hos webbplatsen för att ta emot en kontoprofil. För att generera en profil kan de tillhandahålla ytterligare identifiering, till exempel en e-postadress och ett kön, bland annat. Ytterligare information kan också samlas in, bland annat om communityaktiviteter och köpmönster. Baserat på informationen i profilen kan en demografisk profil skapas.
* **Trait** - En trait är en egenskap eller egenskap hos en besökare som kan användas för att bestämma medlemskap i ett visst segment.
* **Segment** - Ett segment är en samling besökare som delar vissa egenskaper. Segmenten bör vara distinkta, med ett minimum av överlappning med andra segment.
* **Beteenden** - Beteenden är sådana som relaterar till en besökares beteende på webbplatsen. Bland dessa finns:
   * Intresset hos er webbplats, inklusive besökta sidor och köpta produkter
   * Intressen på den refererande webbplatsen, inklusive söktermer som används eller annonser som klickats på
   * Intressen av andra webbplatser; fastställs med verktyg som Spyjax
   * Besökarens lojalitet, besökets varaktighet, besöksfrekvens
* **Demografiska egenskaper** - Dessa är valda populationsegenskaper, bland annat:
   * Ålder
   * Intäkter
   * Familjestorlek
   * Civilstånd
   * Kön
   * Plats
* **Härledda egenskaper** - Vissa demografiska egenskaper är svåra att fastställa utan registrering, men kan härledas genom en kombination av beteenden och demografiska egenskaper.
   * Om du t.ex. kombinerar den refererande URL:en (som en beteendeegenskap) med demografiska data (som hämtats från verktyg som [Google Ad Planner](https://www.google.com/adplanner/)) kan webbplatsägare härleda demografiska egenskaper hos sina besökare.
* **Delsegment** - Ett segment kan delas upp i flera delsegment. Detta görs genom att definiera ytterligare egenskaper.
* **Teaser Page** - en teaser-sida är riktad mot en viss målgrupp. Den innehåller återanvändbart innehåll som kan användas i det underordnade stycket.
* **Kampanj** - En kampanj är en samling med interaktiva sidor och e-postmarknadsföringssidor, som nyhetsbrev och inbjudningar. En kampanj körs vanligtvis under en begränsad period och ersätts av en annan kampanj.
* **Teaser Paragraph** - Det här är ett stycke som hämtar innehåll från en annan sida beroende på en markeringsstrategi. Denna urvalsstrategi kan ta segment och kampanjer i beaktande.
* **Lista** - En lista extraheras från ett segment med registrerade användare. Den plats som t.ex. används för att styra innehållet i det traderande stycket.
