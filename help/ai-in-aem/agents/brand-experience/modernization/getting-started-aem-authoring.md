---
title: Komma igång med Experience Modernization Agent for AEM Authoring Projects
description: Lär dig de specifika konfigurationssteg som krävs för att skapa AEM-projekt när du börjar med Experience Modernization Agent med Experience Modernization Console.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: a1b2c3d4-e5f6-4789-a012-3456789abcde
source-git-commit: df23c3a4c497943135f8719425225526ae14aa92
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Komma igång med Experience Modernization Agent for AEM Authoring Projects {#getting-started-aem-authoring}

För AEM-projekt som använder Universal Editor skiljer sig beredningen av Experience Modernization Agent från Edge Delivery standardflöde. Det här dokumentet täcker de inställningsskillnader som finns. När stegen nedan är klara följer du huvudguiden för [Komma igång med Experience Modernization Agent](getting-started.md).

## Skapa en Edge Delivery Services Project Repo {#create-repo}

1. Använd databasen [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) som mall (inte standardmallen för Edge Delivery Services).
1. Följ självstudiekursen [Universal Editor](https://www.aem.live/developer/ue-tutorial) för att konfigurera ditt svar.
   * Stoppa när du uppmanas att skapa en webbplats i AEM.
1. Ta bort `paths.json` och verkställ den här ändringen i `main`.
1. Lägg till appen [AEM Code Connector](https://github.com/apps/aem-code-connector/installations/select_target) i ditt svar.
   * Detta gör att konsolen kan inspektera koden.

## Skapa en ny webbplats i AEM {#create-site}

1. I AEM Sites-konsolen väljer du **Skapa** > **Plats från mall**.
1. Markera **AEM-webbplatsen med Edge Delivery Services-mallen**.
   * Ser du den inte? [Installera mallen.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)
1. Behåll webbplatsens **namn** (inte titeln) enligt informationen.
   * Webbplatsnamnet används som unik identifierare.
   * Titeln kan ändras för visning.
1. Klicka på **Skapa**.
   * Du omdirigeras till sidan Platser.
   * Uppdatera sidan om den nya platsen inte visas omedelbart.
1. Om du inte redan har gjort det när du [konfigurerar ditt svar &#x200B;](#create-repo) uppdaterar `fstab.yaml` så att det pekar på din AEM-värd, Git-ägare och Git-repo och verkställer ändringarna i `main`.
   * Mer information finns i [Konfigurera innehållskällan](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md).

## Fortsätt med standardstegen Komma igång {#continue}

När ovanstående steg är klara kan du fortsätta med den vanliga guiden Komma igång för att börja migrera ditt innehåll.

![Innehållsimport](assets/content-import.png)

Följ de här stegen från standardguiden.

1. [Förbered en Edge Delivery GitHub-databas](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#prepare-repo)
1. [Öppna Experience Modernization Console](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#open-console)
1. [Anslut din GitHub-databas](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#connect-repo)
1. [Starta fråga](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#start-prompting)

![Innehåll importerat](assets/content-imported-aem-authoring.png)

När du är klar med de här stegen för att migrera innehållet fortsätter du med följande steg.

## Validera innehåll {#validate-content}

Validera innehållet på den markerade sidan på förhandsgranskningspanelen. Eventuella fel visas om du klickar på knappen **Fel** .
Fortsätt chatten med agenten för att åtgärda felen. Använd funktionen **Lägg till i chatt** för att åtgärda specifika element på sidan, tolkningsfiler eller transformeringsfiler.

![Kontextuell chatt](assets/contextual-chat.png)

## Överför innehåll {#upload-content}

Så här överför du innehåll till AEM:

1. Se till att du är i vyn **Innehåll** och klicka på knappen **Överför innehåll** överst till höger.
1. I dialogrutan **Skapa innehållspaket** väljer du vilka sidor som ska inkluderas i paketet.
   * Du kan också ange ett **paketnamn** (standardvärdet är platsnamnet om inget anges).
   * Använd **Markera alla**, **Rensa markering**, **Expandera alla** eller **Komprimera alla** för att hantera listan.
1. Klicka på **Skapa paket**.

   ![Skapa innehållspaket - välj sidor och skapa](assets/content-package.png)

1. När paketet har skapats visar dialogrutan **Överför innehållspaket** att paketet är klart.
   1. Du kan **hämta paketet** om du vill spara det lokalt eller fortsätta med överföringen.
   1. Under **Överför till AEM** bekräftar du **AEM-webbplatsen** och **AEM-värden** (ifylld i förväg från dina projektinställningar).
      * Låt **Överför bilder** vara markerat om du vill inkludera bilder.
   1. Klicka på **Överför till AEM**.

   ![Paketet är klart för överföring till AEM eller hämtning](assets/upload-package-start.png)

1. I dialogrutan visas överföringsförloppet när sidor och resurser skickas till AEM. När överföringen är klar visas ett meddelande om att överföringen lyckades och överföringsloggen. Klicka på **Stäng** för att stänga dialogrutan.

   ![Överföringsförlopp och slutförande i AEM](assets/upload-package-complete.png)

Ditt importerade innehåll finns nu i AEM. Fortsätt med [Push Code Changes](getting-started.md#push-code-changes) i den huvudsakliga Komma igång-guiden.

## Ytterligare resurser {#additional-resources}

* [Komma igång med Experience Modernization Agent](getting-started.md) - ett fullständigt arbetsflöde, inklusive konsol, prompter, överföring och förhandsgranskning
* [Experience Modernization Console](console.md) - konsolreferens
* [Universal Editor, genomgång](https://www.aem.live/developer/ue-tutorial) - Konfigurera ett AEM-redigeringsprojekt och ett Universal Editor-projekt
* [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) - Mallarkiv för projekt för AEM-redigering och Universal Editor
