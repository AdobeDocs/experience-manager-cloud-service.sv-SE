---
title: Sidskillnader
description: Med funktionen för sidskillnader kan du enkelt jämföra två sidor sida vid sida med skillnaderna markerade.
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: ae1dedc3d0533205decc08d396c5a844c4525ba2
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Sidskillnader {#page-diff}

## Introduktion {#introduction}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill enkelt kunna jämföra den aktuella sidan sida vid sida med en annan version.

Med funktionen för sidskillnader kan du enkelt jämföra två sidor sida vid sida med skillnaderna markerade.

>[!NOTE]
>
>Användaren måste ha behörigheten **Ändra/skapa/ta bort** på noden `/content/versionhistory` för att kunna använda funktionen.
>
>Mer teknisk information om den här funktionen finns i [Developing and Page Diff](/help/implementing/developing/introduction/page-diff.md#operation-details).

## Använd {#use}

Diff:en sida vid sida kan jämföra:

* [Versioner](/help/sites-cloud/authoring/sites-console/page-versions.md#comparing-a-version-with-current-page) - Tidigare version av en sida med det aktuella läget
* [Live-kopior](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live-kopia med utkast
* [Startar](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) - Starta med Source
* [Språkkopior](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) - En sida före och efter (re-)översättning

Läs respektive avsnitt om hur du påbörjar skillnaderna i dessa sammanhang.

### Presentation av skillnader {#presentation-of-differences}

Oberoende av vilket innehåll som jämförs, förblir presentationen av skillnaderna densamma.

* Det innehåll som valdes när du startade differensen visas till vänster (diff-startpunkten).
* Jämförelseinnehållet visas till höger (vad det markerade innehållet jämförs med).

Om du till exempel jämför versioner visas den aktuella versionen till vänster och den föregående versionen till höger.

Källan för båda sidorna visas tydligt i sidhuvudsfältet högst upp i webbläsarfönstret.

![Versioner sida vid sida ](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

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

### Helskärm och avslutande {#fullscreen-and-exiting}

Om du vill fokusera på ett visst innehåll kan du klicka på helskärmsikonen för någon av sidorna i den sida som skiljer sig åt för att förstora den till hela webbläsarfönstret.

![Helskärmsknapp](/help/sites-cloud/authoring/assets/versions-full-screen.png)

Den markerade sidan fyller hela fönstret, men fältet förblir överst så att du kan växla mellan de två sidorna.

![Helskärmsläge](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Om webbläsarbredden inte kan hantera båda sidnamnen i helskärmsläge visas bara namnet på sidan som visas och den andra är tillgänglig bakom ellipsen.

Du kan också stänga helskärmsläget genom att klicka på ikonen för att avsluta helskärmsläget.

![Avsluta helskärmsläge](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

Du kan när som helst stänga diff sida vid sida genom att klicka på stängningsknappen i sidhuvudet.

## Begränsningar {#limitations}

I vissa situationer kan det hända att sidskillnader inte identifierar någon skillnad som förväntat.

* När olika sidor skapas för användning med [Edge Delivery Services](/help/edge/overview.md) visas sidorna sida vid sida för att underlätta jämförelsen, men skillnaderna markeras inte.
* När olika versioner och starter används inte dynamiska komponenter som vägbeskrivningar, menyer, produktlistor eller logotyper (komponenter som är beroende av webbplatsstrukturen för att återge sitt innehåll).
* För versioner återskapar inte diff åtkomstkontrollprincipen och Live copy-relationen.
* Om en sida flyttas kan du inte längre göra några skillnader med versioner som gjorts före flyttningen.
   * Om du får problem med en skillnad kontrollerar du [tidslinjen](/help/sites-cloud/authoring/basic-handling.md#timeline) för sidan för att se om sidan har flyttats.

>[!NOTE]
>
>Versioner kan inte jämföras med varandra. Endast den aktuella versionen kan jämföras med andra versioner av sidan. Den aktuella versionen är alltid den version som markeras med ändringar.

>[!NOTE]
>
>Mer information om funktionen för sidskillnader och begränsningar som kan påverka sidskillnader finns i [utvecklardokumentationen](/help/implementing/developing/introduction/page-diff.md) för den här funktionen.
