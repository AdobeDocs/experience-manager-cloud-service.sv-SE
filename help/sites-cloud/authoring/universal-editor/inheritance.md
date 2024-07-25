---
title: Innehållsarv i den universella redigeraren
description: Läs om hur den universella redigeraren stöder innehållsarv för hantering av flera webbplatser och startar funktioner för återanvändning och lokalisering av innehåll.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 58c58243dc98a21161afe0976da4dcdc235da0d3
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Innehållsarv i den universella redigeraren {#inheritance}

Läs om hur den universella redigeraren stöder innehållsarv för hantering av flera webbplatser och startar funktioner för återanvändning och lokalisering av innehåll.

## Användningsfall {#use-case}

För många användare av AEM är det bara början att skapa en sida. För att innehållet ska kunna skalas effektivt är följande steg vanligtvis involverade efter att sidan har skapats:

1. **Översätt sidan** med språkkopior och översättningsarbetsflöden.
1. **Lokalisera sidan** genom att använda Multi Site Management (Hantering av flera webbplatser) för att rulla ut den översatta sidan till olika marknader.
1. **Skapa nya versioner** genom att använda Launches (Starta) för att förbereda framtida versioner av sidan och göra ändringarna tillgängliga.

Dessa steg kan snabba upp innehållets hastighet och säkerställa innehållets enhetlighet. Den universella redigeraren stöder innehållsarv, vilket är den mekanism som dessa steg är beroende av.

## Arv {#what-is-inheritance}

Arv är den mekanism där innehåll kan länkas så att om du ändrar det ena ändras det andra automatiskt. Ärvda komponenter kan vara produkten av olika scenarier, bland annat:

* [Hantering av flera webbplatser (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Startar](/help/sites-cloud/authoring/launches/overview.md)

MSM och Launches är kraftfulla verktyg som hjälper dig att återanvända innehållet. Sidor kan kopieras från en central källa (utkast) så att författare kan göra ändringar som är specifika för kopiorna, medan resten av innehållet fortfarande ärvs från ritningen. Detta är mycket användbart när du lokaliserar webbplatser.

Om du vill ändra en del av innehållet i kopiorna bryter författarna arvet för de berörda komponenterna för att säkerställa att deras lokala ändringar inte skrivs över när kopiorna synkroniseras från planen.

## Innehållsarv och den universella redigeraren {#universal-editor}

När en sida är en del av ett flerlägesobjekt eller en Launch-sida och innehållet redigeras med den universella redigeraren, inaktiveras automatiskt arv för alla ändringar som görs av författare på den sidan, vilket säkerställer att det ändrade innehållet behålls när uppdateringarna synkroniseras från planen.

Författaren behöver inte klicka på en knapp eller på något annat sätt vidta några andra åtgärder för att inaktivera arv innan han eller hon gör lokala redigeringar. Så snart en ändring har gjorts avbryts arvet implicit. Detta står i kontrast till [sidredigeraren.](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)

## Begränsningar {#limitations}

* Författare kan inte återställa arv för enskilda komponenter.
   * Arv kan bara återställas för hela sidan via [Live Copy Overview Console](/help/sites-cloud/administering/msm/live-copy-overview.md) eller [Launches Console.](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* Författare har ingen visuell feedback för att se vilka komponenter som har sitt arv inaktiverat och vilka som fortfarande har det bevarat.
* Dessa funktioner är för närvarande begränsade till komponenter på sidor och gäller ännu inte för [innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md), trots att de också har MSM- och Launch-funktioner.
