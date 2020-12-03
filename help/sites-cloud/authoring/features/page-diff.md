---
title: Sidskillnader
description: Med funktionen för sidskillnader kan du enkelt jämföra två sidor sida vid sida med skillnaderna markerade.
translation-type: tm+mt
source-git-commit: b405e49cd883df1e2e9768bb9e4d6908afc443e2
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---


# Sidskillnader {#page-diff}

## Introduktion {#introduction}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill enkelt kunna jämföra den aktuella sidan sida vid sida med en annan version.

Med funktionen för sidskillnader kan du enkelt jämföra två sidor sida vid sida med skillnaderna markerade.

>[!NOTE]
>
>Användaren måste ha behörigheten **Modify/Create/Delete** på noden `/content/versionhistory` för att kunna använda funktionen.
>
>Mer teknisk information om den här funktionen finns i [Developing and Page Diff](/help/implementing/developing/introduction/page-diff.md#operation-details).

## Använd {#use}

Diff:en sida vid sida kan jämföra:

* [Versioner](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page)  - Tidigare version av en sida med det aktuella läget
* Live-kopior - Live-kopia med utkast <!-- [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy with its Blueprint-->
* [Startar](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page)  - Starta med dess källa
* Språkkopior - En sida före och efter (re-)translation <!-- [Language Copies](/help/sites-administering/tc-manage.md#comparing-language-copies) - A page before and after (re-)translation-->

Läs respektive avsnitt om hur du påbörjar skillnaderna i dessa sammanhang.

### Presentation av skillnader {#presentation-of-differences}

Oberoende av vilket innehåll som jämförs, förblir presentationen av skillnaderna densamma.

* Det innehåll som valdes när du startade differensen visas till vänster (diff-startpunkten).
* Jämförelseinnehållet visas till höger (vad det markerade innehållet jämförs med).

Om du till exempel jämför versioner visas den aktuella versionen till vänster och den föregående versionen till höger.

Källan för båda sidorna visas tydligt i sidhuvudsfältet högst upp i webbläsarfönstret.

![Versioner sida vid sida](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

Skillnaden identifierar ändringar på komponentnivå och HTML-nivå. Objekt som har ändrats markeras med olika färger.

**Komponentändringar**

* Ljusgrön - komponent tillagd
* Rosa - komponent borttagen

**HTML-ändringar**

* Mörkgrön - HTML tillagd
* Röd - HTML borttagen

>[!NOTE]
>
>När du jämför språkkopior inaktiveras markering, eftersom i en översättning ändras allt och markering inte har någon fördel.

### Helskärm och Avslutar {#fullscreen-and-exiting}

Om du vill fokusera på ett visst innehåll kan du klicka på helskärmsikonen för endera&quot;sidan&quot; av diff:n för att förstora den till hela webbläsarfönstret.

![Helskärmsknapp](/help/sites-cloud/authoring/assets/versions-full-screen.png)

Den markerade sidan fyller hela fönstret, men fältet förblir överst så att du kan växla mellan de två sidorna.

![Helskärmsläge](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Om webbläsarbredden inte kan hantera båda sidnamnen i helskärmsläge visas bara namnet på sidan som visas och den andra visas bakom ellipsen.

Du kan också stänga helskärmsläget genom att klicka på ikonen för att avsluta helskärmsläget.

![Avsluta helskärmsläge](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

Du kan när som helst stänga diff sida vid sida genom att klicka på stängningsknappen i sidhuvudet.

## Begränsningar {#limitations}

I vissa situationer kan det hända att sidskillnader inte identifierar någon skillnad som förväntat.

* När olika versioner och starter används inte dynamiska komponenter som vägbeskrivningar, menyer, produktlistor eller logotyper (komponenter som är beroende av webbplatsstrukturen för att återge sitt innehåll).
* För versioner återskapar inte diff åtkomstkontrollprincipen och Live copy-relationen.
* Om en sida flyttas kan du inte längre göra några skillnader med versioner som gjorts före flyttningen.
   * Om du får problem med en skillnad kontrollerar du [tidslinjen](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) för sidan för att se om sidan har flyttats.

>[!NOTE]
>
>Versioner kan inte jämföras med varandra. Endast den aktuella versionen kan jämföras med andra versioner av sidan. Den aktuella versionen är alltid den version som markeras med ändringar.

>[!NOTE]
>
>Mer information om hur sidskillnader fungerar och om begränsningar som kan påverka sidskillnader finns i [utvecklardokumentationen](/help/implementing/developing/introduction/page-diff.md) för den här funktionen.
