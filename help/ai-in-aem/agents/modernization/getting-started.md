---
title: Komma igång med agenten för upplevelsemodernisering
description: Lär dig de första stegen för att snabbt bli produktiv med Experience Modernization Agent med Experience Modernization Console.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 612c211e-43bf-47dc-89a8-9995a960e4d7
source-git-commit: 76c0f41acb5c2e4e0f0a292f8205b0b9de5cda81
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---


# Komma igång med agenten för upplevelsemodernisering {#getting-started}

Lär dig de första stegen för att snabbt bli produktiv med Experience Modernization Agent med Experience Modernization Console.

>[!NOTE]
>
>Om du är intresserad av att använda Experience Modernization Console kan du begära åtkomst för att få en smidig introduktionsupplevelse.

## Förbered en Edge Delivery GitHub-databas {#prepare-repo}

1. Välj en [Edge Delivery Services](/help/edge/overview.md)-databas som ska användas med Experience Modernization Console.
   * Detta kan vara ett befintligt Edge Delivery Services-projekt eller så kan du skapa ett nytt efter [utvecklarsjälvstudiekursen](https://www.aem.live/developer/tutorial) med hjälp av [standarddatabasen.](https://github.com/adobe/aem-boilerplate)
1. Kontrollera att [AEM Code Connector](https://github.com/apps/aem-code-connector) är installerad i databasen.
   * Detta gör att konsolen kan inspektera koden.
1. Kontrollera att [AEM Code Sync GitHub-appen](https://github.com/apps/aem-code-sync) är installerad i databasen.
   * Detta gör att Edge Delivery Services kan synkronisera din kod.
   * Om ditt svar baseras på självstudiekursen är det här steget redan klart.

## Öppna Experience Modernization Console {#open-console}

1. Navigera till [`aemcoder.adobe.io`.](https://aemcoder.adobe.io)
1. Logga in med din Adobe ID.

## Anslut din GitHub-databas {#connect-repo}

Konsolen frågar efter en databas när du loggar in första gången.

![Konsolens första inloggningsskärm](assets/first-sign-on.png)

1. Klicka på **Anslut databas**.
1. Då öppnas appen AEM Code Connector på en ny webbläsarflik. Klicka på **Auktorisera AEM Code Connector**.
1. Gå tillbaka till konsolen, välj **Ägare**, **Databas** och **Grenval** och klicka på **Checka ut till arbetsyta**.
   ![Ansluter till GitHub-projekt](assets/connect-to-github-project.png)
1. När du uppmanas att **Ersätt befintlig arbetsyta** klickar du på **Ersätt arbetsyta**.
   ![Ersätt befintlig arbetsyta](assets/replace-existing-workspace.png)

Ditt GitHub-projekt är nu anslutet till konsolen och du är på startskärmen.

![Startsida för konsolen](assets/console-home.png)

## Starta fråga {#start-prompting}

Nu när konsolen har åtkomst till koden kan du börja fråga.

1. För att komma igång kan du importera innehållet på en webbplats:
   * &quot;Migrera sidan `https://wknd-trendsetters.site`.&quot;
1. Detta importerar platsens innehåll.
   * Konsolen observerar olika problemområden och hanterar innehåll och presentation separat.
   * Den inledande importen av en webbplats innehåll kan ta flera minuter.
   * Konsolen ger dig kontinuerlig feedback när arbetet börjar, inklusive en översikt över de planerade stegen.
     ![Innehållsimport](assets/content-import.png)
1. När webbplatsen har importerats visas sidorna på panelen **Workspace**. Markera en sida om du vill förhandsgranska den på den högra panelen.
   ![Innehåll importerat](assets/content-imported.png)
1. Nu när du har innehåll kan du be om att importera formaten från samma källa.
   * &quot;Importera allmänna format från `https://wknd-trendsetters.site`.&quot;
1. Precis som med den ursprungliga innehållsimporten kan importen ta flera minuter och konsolen ger feedback när din begäran behandlas och formaten importeras. När aktiviteten är klar klickar du på **Uppdatera förhandsvisning** på den högra panelen för att visa det formaterade innehållet.
   ![Format importerade](assets/styles-imported.png)

Nu har du importerat både innehåll och format till konsolen.

## Överför innehåll {#upload-content}

Så här överför du ditt innehåll till [Dokumentredigering](https://da.live):

1. Kontrollera att du är i vyn **Innehåll** och klicka sedan på knappen **Överför innehåll** överst till höger.
   * Som standard är du i vyn **Innehåll** när du öppnar konsolen.
   * Din vy indikeras av den markerade ikonen i sidlisten på vänster sida av konsolen.
1. Dialogrutan **Överför innehåll** öppnas med målorganisationen och repo är ifylld från din `fstab.yaml`.
   * Om `fstab.yaml` inte finns i din anslutna databas måste du ange din **organisation** och **databas** manuellt.
   * Om du använde mallsidan anges `fstab.yaml`.
1. Markera de filer som du vill överföra och klicka på **Överför**.
   ![Dialogrutan Överför innehåll](assets/upload-content.png)
1. Konsolen anger överföringsprocessen genom att gråta knappen **Överför**.
   ![Överför](assets/uploading.png)
1. När det är klart visas ett meddelande längst ned på konsolen.
   ![Visa i AEM](assets/view-in-aem.png)

Om du vill komma åt det överförda innehållet i dokumentredigering kan du klicka på **Visa i AEM** i meddelandet när överföringen är klar, eller navigera till `https://da.live/#/{organization}/{repository}`.

![Innehåll i dokumentredigering](assets/content-in-document-authoring.png)

Ditt importerade innehåll är nu i dokumentredigering.

## Push-kodändringar {#push-code-changes}

När du är nöjd med de ändringar du har gjort i koden kan du överföra dem till din GitHub-databas.

1. Växla till vyn **Kod** (`</>` ikon i det vänstra sidfältet) och sedan fliken **Git Changes** (fililikon längst upp till höger).
   ![Kodvyn](assets/code-view-git-changes.png)
1. Om vissa filer visas som ej spårade i listan över ändrade filer klickar du på knappen `+` för att mellanlagra dem.
1. Klicka på knappen **GitHub-åtgärder** längst upp till höger och välj sedan **Push** i listrutan.
1. I dialogrutan **Push changes** väljer du att överföra ändringar till en ny PR (standard) eller den aktuella grenen och klickar sedan på **Confirm** för att skicka ändringarna.
   * Om du är osäker kan du flytta till den aktuella grenen för att göra det enkelt.
1. När det är klart visas ett meddelande längst ned på konsolen.
   ![Visa PR](assets/view-pr.png)

Om du vill ha direktåtkomst till de push-ändringar som gjorts i GitHub klickar du på **Visa PR** i meddelandet när push-åtgärden har slutförts.

![Kod i GitHub](assets/code-in-github.png)

Din kod finns nu i GitHub.

## Förhandsgranska webbplats {#preview-site}

Så här visar du ändringarna i förhandsvisningsmiljön:

1. Gå tillbaka till Dokumentredigering.
   * Det kan fortfarande vara öppet på en webbläsarflik som du har öppnat efter att du klickat på **Visa i AEM** när du har överfört innehållet.
   * Eller navigera till `https://da.live/#/{organization}/{repository}`
1. Öppna en av sidorna som du tidigare överförde till AEM.
1. Klicka på pappersplansikonen (överst till höger) och välj **Förhandsgranska**.
   ![Publicera för förhandsgranskning](assets/publish-to-preview.png)

Grattis! Ditt migrerade innehåll och format finns nu i AEM förhandsvisningsmiljö.

![Publicerat förhandsgranskningsinnehåll](assets/published-preview.png)

Om du har överfört koden till en annan gren än `main` visas inte formaten i den förhandsgranskning som har öppnats från Dokumentredigering. Ändra till grenen genom att uppdatera URL:en för förhandsgranskningen så att du kan se dina format.

## Ytterligare resurser {#additional-resources}

Följande dokument kan vara användbara när du fortsätter att utforska Experience Modernization Agent och dess konsol.

* [Experience Modernization Console](/help/ai-in-aem/agents/modernization/console.md) - information om konsolen, dess vyer, alternativ och funktioner
* [Edge Delivery Services utvecklarsjälvstudiekurs](https://www.aem.live/developer/tutorial) - Praktiskt om du inte har använt AEM- eller Edge Delivery Services-projekt tidigare
* [Dokumentredigering](https://da.live) - Praktiskt om du inte har använt dokumentredigering tidigare för innehållshantering
