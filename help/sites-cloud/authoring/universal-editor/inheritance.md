---
title: Innehållsarv i den universella redigeraren
description: Läs om hur den universella redigeraren stöder innehållsarv för hantering av flera webbplatser och startar funktioner för återanvändning och lokalisering av innehåll.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 2a1b87c2-29b9-4689-9a15-e17942439160
source-git-commit: 2099a1aecd30eaa2ca3ca33a13729817a30b6c3f
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Innehållsarv i den universella redigeraren {#inheritance}

Läs om hur den universella redigeraren stöder innehållsarv för hantering av flera webbplatser och startar funktioner för återanvändning och lokalisering av innehåll.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för innehåll som lagras i AEM-databasen.

## Användningsfall {#use-case}

För många användare av AEM är det bara början att skapa en sida. För att innehållet ska kunna skalas effektivt är följande steg vanligtvis involverade efter att sidan har skapats:

1. **Översätt sidan** med språkkopior och översättningsarbetsflöden.
1. **Lokalisera sidan** genom att använda Multi Site Management (Hantering av flera webbplatser) för att rulla ut den översatta sidan till olika marknader.
1. **Skapa nya versioner** genom att använda Launches (Starta) för att förbereda framtida versioner av sidan och göra ändringarna tillgängliga.

Dessa steg kan snabba upp innehållets hastighet och säkerställa innehållets enhetlighet. Den universella redigeraren har stöd för innehållsarv, vilket är den mekanism som används för språkkopior, hantering av flera webbplatser och starter.

## Arv {#what-is-inheritance}

Arv är den mekanism där innehåll kan länkas så att om du ändrar det ena ändras det andra automatiskt.

MSM och Launches är kraftfulla verktyg som hjälper dig att återanvända ditt innehåll med hjälp av arv. Sidor kan kopieras från en central källa (utkast) så att författare kan göra ändringar som är specifika för kopiorna, medan resten av innehållet fortfarande ärvs från ritningen. Detta är mycket användbart när du lokaliserar webbplatser.

Om du vill ändra en del av innehållet i kopiorna bryter författarna arvet för de berörda komponenterna för att säkerställa att deras lokala ändringar inte skrivs över när kopiorna synkroniseras från planen.

## Innehållsarv och den universella redigeraren {#universal-editor}

När en sida är en del av ett flerlägesobjekt eller en Launch-sida och innehållet redigeras med den universella redigeraren, inaktiveras automatiskt arv för alla ändringar som görs av författare på den sidan, vilket säkerställer att det ändrade innehållet behålls när uppdateringarna synkroniseras från planen.

Författaren behöver inte klicka på en knapp eller på något annat sätt vidta några andra åtgärder för att inaktivera arv innan han eller hon gör lokala redigeringar. Så snart en ändring har gjorts avbryts arvet implicit. Det här arbetsflödet står i kontrast till [sidredigeraren](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components).

Arv kan återställas för hela sidan via:

* [Konsolen Live-kopia - översikt](/help/sites-cloud/administering/msm/live-copy-overview.md)
* [Startar konsolen](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* Använda knappen **Återställ** på fliken **Live-kopia** i fönstret [sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md).

Den universella redigeraren påverkar inte den underliggande arvsmekanismen. Mer information om hur arv fungerar finns i följande dokumentation.

* [Hantering av flera webbplatser (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Launches](/help/sites-cloud/authoring/launches/overview.md)

### AEM MSM-tillägg (Multi-Site Management) {#msm-extension}

Om det är installerat visar både **AEM Multi-Site-Management (MSM)-tillägget** den aktuella arvsstatusen för den markerade komponenten och gör att du kan bryta eller återställa arv på komponentnivå.

Mer information om hur du använder tillägget finns i [redigeringsdokumentationen.](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)

Information om hur du aktiverar det här tillägget finns i [Extension Manager-dokumentationen.](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## Begränsningar {#limitations}

* Om du vill återställa arv för enskilda komponenter måste **MSM-tillägget** (AEM Multi-Site-Management) vara aktiverat.
* Om du vill se vilken komponent som arv inaktiveras och som fortfarande har det bevarat, måste **MSM-tillägget** (AEM Multi-Site-Management) aktiveras.
