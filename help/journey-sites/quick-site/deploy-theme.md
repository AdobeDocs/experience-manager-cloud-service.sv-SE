---
title: Driftsätt ditt anpassade tema
description: Lär dig hur du distribuerar webbplatstemat med hjälp av pipeline.
exl-id: fe065972-39db-4074-a802-85895c701efd
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---


# Driftsätt ditt anpassade tema {#deploy-your-customized-theme}

{{traditional-aem}}

Lär dig hur du distribuerar webbplatstemat med hjälp av pipeline.

## Story hittills {#story-so-far}

I det tidigare dokumentet på AEM snabbwebbplats Skapa webbplats [Anpassa webbplatstemat](customize-theme.md) lärde du dig hur temat är skapat, hur du anpassar det och hur du testar det med AEM-innehåll, och du bör nu:

* Förstå webbplatsens grundläggande struktur och hur du redigerar den.
* Se hur du testar dina temaanpassningar med verkligt AEM-innehåll via en lokal proxy.
* Lär dig implementera ändringarna i AEM Git-databasen.

Du kan nu ta det sista steget och använda pipeline för att distribuera dem.

## Syfte {#objective}

I det här dokumentet förklaras hur du distribuerar temat med hjälp av pipeline. När du har läst bör du:

* Ta reda på hur ni kan utlösa en pipeline-distribution.
* Se hur du kontrollerar distributionsstatusen.

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller för den som utvecklar gränssnittet.

## Starta pipeline {#start-pipeline}

När du har implementerat ändringarna av temaanpassningen i AEM Git-databasen kan du köra [pipelinen som administratören skapade](pipeline-setup.md) för att distribuera ändringarna.

1. Logga in på Cloud Manager [ på samma sätt som du gjorde för att hämta Git-åtkomstinformation](retrieve-access.md) och få tillgång till ditt program. På fliken **Översikt** visas ett kort för **pipelines**.

   ![Cloud Manager - översikt](assets/cloud-manager-overview.png)

1. Markera ellipsen bredvid den pipeline du vill starta. Välj **Kör** i listrutan.

   ![Kör pipeline](assets/run-pipeline.png)

1. Välj **Ja** i bekräftelsedialogrutan för **Kör pipeline**.

   ![Bekräfta pipeline-körning](assets/pipeline-confirm.png)

1. Statuskolumnen i listan över pipelines anger att din pipeline nu körs.

   ![Körningsstatus för pipeline](assets/pipeline-running.png)

## Kontrollera pipeline-status {#pipeline-status}

Du kan när som helst kontrollera status för pipeline för att se hur långt förloppet har kommit.

1. Markera ellipsen bredvid din pipeline.

   ![Visa pipeline-information](assets/view-pipeline-details.png)

1. I informationsfönstret för pipeline visas en beskrivning av förloppet för pipeline.

   ![Information om pipeline](assets/pipeline-details.png)

>[!TIP]
>
>I informationsfönstret för pipeline kan du välja **Hämta logg** för valfritt steg i pipeline för felsökningssyften om något steg skulle misslyckas. Felsökning av pipeline ligger utanför den här kundresan. Se de tekniska dokumenten för Cloud Manager i avsnittet [Ytterligare resurser](#additional-resources) på den här sidan.

## Validera distribuerade anpassningar {#view-customizations}

När pipelinen är klar kan du informera administratören om att validera ändringarna. Administratören kommer då att

1. Öppna AEM redigeringsmiljö.
1. Navigera till [platsen som administratören skapade](create-site.md) tidigare.
1. Redigera en av innehållssidorna.
1. Se ändringarna.

![Ändringarna tillämpas](assets/changes-applied.png)

## Slut på resan? {#end-of-journey}

Grattis! Du har nu slutfört AEM snabbwebbplats! Nu bör du:

* Förstå hur Cloud Manager och den integrerade pipeline fungerar för att hantera och driftsätta gränssnittsanpassningar.
* Lär dig hur du skapar en AEM-webbplats baserat på en mall och hur du hämtar webbplatstemat.
* Anlita en frontutvecklare så att de kan komma åt AEM Git-databasen.
* Hur man anpassar och testar ett tema med hjälp av proxiderat AEM-innehåll och implementerar dessa ändringar i AEM Git.
* Så här distribuerar du gränssnittsanpassning med hjälp av pipeline.

Nu kan du anpassa temana för din egen AEM-webbplats. Innan du börjar skapa olika arbetsflöden med flera frontendpipelines bör du dock granska dokumentet [Utveckla platser med frontendspipelinen](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md). Det kan hjälpa er att få ut så mycket som möjligt av er frontendutveckling genom att:

* Bevara en enda sanningskälla.
* Upprätthålla ett åtskilt engagemang.

AEM är ett kraftfullt verktyg och det finns många andra alternativ. Ta en titt på några av de ytterligare resurser som är tillgängliga i avsnittet [Ytterligare resurser](#additional-resources) om du vill veta mer om de funktioner du såg under den här resan.

## Ytterligare resurser {#additional-resources}

Nedan följer ytterligare resurser som ger en djupdykning i några koncept som nämns i det här dokumentet.

* [Använda webbplatsregistret för att hantera webbplatstemat](/help/sites-cloud/administering/site-creation/site-rail.md) - Lär dig de kraftfulla funktionerna i webbplatsspåret för att enkelt anpassa och hantera webbplatstemat, inklusive hämtning av temakällor och hantering av temaversioner.
* [AEM as a Cloud Service tekniska dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - Om du redan har en god förståelse för AEM kan det vara bra att läsa de detaljerade tekniska dokumenten direkt.
* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.
* [Rollbaserade behörigheter](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager har förkonfigurerade roller med lämpliga behörigheter. I det här dokumentet finns mer information om de här rollerna och hur du administrerar dem.
* [Cloud Manager-databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - Om du vill ha mer information om hur du konfigurerar och hanterar Git-databaser för ditt AEMaaCS-projekt läser du det här dokumentet.
* [Konfigurera CI/CD-pipeline - molntjänster](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Läs mer om hur du konfigurerar pipelines, både fullständig stack och frontend, i det här dokumentet.
* [AEM standardwebbplatsmall](https://github.com/adobe/aem-site-template-standard) - Detta är GitHub-databasen för AEM standardwebbplatsmall.
* [AEM Site Theme](https://github.com/adobe/aem-site-template-standard-theme-e2e) - Detta är GitHub-databasen för AEM Site Theme.
* [npm](https://www.npmjs.com) - AEM-teman som används för att snabbt skapa webbplatser baseras på npm.
* [webpack](https://webpack.js.org) - AEM-teman som används för att snabbt skapa webbplatser är beroende av webbpaket.
* [Organisera sidor](/help/sites-cloud/authoring/sites-console/organizing-pages.md) - Den här guiden beskriver hur du organiserar sidor på din AEM-webbplats.
* [Skapar sidor](/help/sites-cloud/authoring/sites-console/creating-pages.md) - Den här guiden beskriver hur du lägger till nya sidor på webbplatsen.
* [Hantera sidor](/help/sites-cloud/authoring/sites-console/managing-pages.md) - Den här guiden beskriver hur du hanterar sidorna på din webbplats, inklusive flyttning, kopiering och borttagning.
* [Så här arbetar du med paket](/help/implementing/developing/tools/package-manager.md) - Med paket kan du importera och exportera databasinnehåll. I det här dokumentet beskrivs hur du arbetar med paket i AEM 6.5, som även gäller för AEMaaCS.
* [Onboarding Journey](/help/journey-onboarding/overview.md) - Den här guiden fungerar som en startpunkt för att säkerställa att dina team har konfigurerats och tillgång till AEM as a Cloud Service.
* [Adobe Experience Manager Cloud Manager Documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) - Utforska Cloud Manager-dokumentationen och få fullständig information om dess funktioner.
* [Dokumentation för webbplatsadministration](/help/sites-cloud/administering/site-creation/create-site.md) - Mer information om funktionerna i verktyget Skapa snabbwebbplats finns i de tekniska dokumenten för att skapa webbplatser.
* [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) - I det här dokumentet beskrivs några överväganden som du bör vara medveten om så att du kan få ut mesta möjliga av utvecklingsprocessen med hjälp av frontendpipeline.
