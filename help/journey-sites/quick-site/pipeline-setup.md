---
title: Konfigurera din pipeline
description: Skapa en pipeline för frontend för att hantera anpassningen av webbplatsens tema.
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---

# Konfigurera din pipeline {#set-up-your-pipeline}

Skapa en pipeline för frontend för att hantera anpassningen av webbplatsens tema.

## Story hittills {#story-so-far}

I det föregående dokumentet från den AEM snabbwebbplatsgenereringsresan, [Skapa webbplats från mall](create-site.md), lärde du dig att använda en webbplatsmall för att snabbt skapa en AEM webbplats som kan anpassas ytterligare med hjälp av slutverktygen och nu bör du:

* Lär dig hur du hämtar AEM webbplatsmallar.
* Lär dig hur du skapar en plats med hjälp av en mall.
* Se hur du laddar ned mallen från din nya webbplats och kan ge den till frontutvecklaren.

Den här artikeln bygger på dessa grundläggande funktioner så att ni kan skapa en frontpipeline, som utvecklaren senare kommer att använda för att driftsätta gränssnittsanpassningar.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå rörledningar och hur du skapar en för att hantera distributionen av webbplatsens anpassade tema. När du har läst bör du:

* Förstå vad en rörledning är.
* Ta reda på hur man lägger upp en rörledning i Cloud Manager.

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller Cloud Manager-administratören.

## Krav {#requirements}

* Du måste ha tillgång till Cloud Manager.
* Du måste vara medlem i rollen **Distributionshanteraren** i Cloud Manager.
* En Git-repo för AEM måste konfigureras i Cloud Manager.
   * Detta är vanligtvis redan fallet för alla aktiva projekt. Om så inte är fallet läser du dokumentationen för Cloud Manager-databaser som finns under avsnittet [Ytterligare resurser](#additional-resources).

## Vad är en frontpipeline? {#front-end-pipeline}

Framtidsutveckling innebär anpassning av JavaScript-, CSS- och statiska resurser som definierar hur din AEM ska formateras. Utvecklaren kommer att arbeta i sina egna lokala miljöer för att göra dessa anpassningar. När de är klara implementeras ändringarna i databasen för AEM Git. Men de är bara kopplade till källkoden. De lever ännu inte.

I frontproduktionsflödet används dessa implementerade anpassningar och distribueras till en AEM miljö, vanligtvis i produktions- eller icke-produktionsmiljöer.

På så sätt kan front end-utveckling fungera separat från och parallellt med all backend-utveckling i full stack på AEM, som har sina egna driftsättningspipelines.

>[!NOTE]
>
>I frontledningarna kan du bara distribuera JavaScript-, CSS- och statiska resurser för att utforma din AEM. Webbplatsinnehåll som sidor eller resurser kan inte distribueras i en pipeline.

## Använd Cloud Manager {#login}

1. Logga in på Adobe Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Cloud Manager listar de olika program som är tillgängliga. Markera den du vill hantera. Om du just har börjat med AEM as a Cloud Service har du antagligen bara ett program tillgängligt.

   ![Välja ett program i Cloud Manager](assets/cloud-manager-select-program.png)

Nu visas en översikt över programmet. Sidan ser annorlunda ut men liknar det här exemplet.

![Cloud Manager - översikt](assets/cloud-manager-overview.png)

Observera namnet på programmet som du har öppnat eller kopierat URL:en. Du måste skicka detta till den som utvecklar gränssnittet senare.

## Skapa en frontpipeline {#create-front-end-pipeline}

Nu när du har kommit åt Cloud Manager kan du skapa en pipeline för driftsättning i gränssnittet.

1. Markera **Lägg till** i delen **Förgreningar** på Cloud Manager-sidan.

   ![Rörledningar](assets/pipelines-add.png)

1. På snabbmenyn som visas under knappen **Lägg till** väljer du **Lägg till icke-produktionspipeline** för den här resan.

1. På fliken **Konfiguration** i dialogrutan **Lägg till icke-produktionsförlopp** som öppnas:
   * Välj **Distributionspipeline**.
   * Ange ett namn för pipelinen i fältet **Namn på icke-produktionspipeline**.

   ![Lägg till pipeline-konfiguration](assets/add-pipeline-configuration.png)

1. Välj **Fortsätt**.

1. På fliken **Source Code**:
   * Välj **Front End Code** som den typ av kod som ska distribueras.
   * Kontrollera att rätt miljö är markerad under **Berättigade distributionsmiljöer**.
   * Välj rätt **databas**.
   * Ange vilken **Git-gren** som pipeline ska kopplas till.
   * Definiera **kodplatsen** om frontendutvecklingen finns under en viss sökväg i den valda databasen. Standardvärdet är databasens rot, men ofta är front end-utveckling och back end-objekt under olika sökvägar.

   ![Source-kodinformation för att lägga till pipeline](assets/add-pipeline-source-code.png)

1. Välj **Spara**.

Den nya pipelinen skapas och visas i avsnittet **Pipelines** i Cloud Manager-fönstret. Om du trycker på ellipsen efter pipelinenamnet visas alternativ för ytterligare redigering eller visning av detaljer efter behov.

![Alternativ för pipeline](assets/new-pipeline.png)

>[!TIP]
>
>Om du redan känner till pipelines i AEMaaCS och vill veta mer om skillnaderna mellan de olika typerna av pipelines, inklusive mer information om frontendpipeline, kan du läsa Konfigurera CI/CD-pipeline - Cloud Service som är länkade i avsnittet [Ytterligare resurser](#additional-resources) nedan.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM snabbwebbplats:

* Förstå vad en rörledning är.
* Ta reda på hur man lägger upp en rörledning i Cloud Manager.

Bygg vidare på den här kunskapen och fortsätt din resa med att skapa AEM genom att gå igenom dokumentet [Bevilja åtkomst till frontendutvecklaren](grant-access.md), där du kommer att introducera gränssnittsutvecklarna i Cloud Manager så att de har tillgång till din AEM platsdatabas och pipeline.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av snabbwebbplatsskapandeprocessen genom att granska dokumentet [Anpassa webbplatstemat](customize-theme.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=sv-SE) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.
* [Cloud Manager-databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - Om du vill ha mer information om hur du konfigurerar och hanterar Git-databaser för ditt AEMaaCS-projekt läser du det här dokumentet.
* [Konfigurera CI/CD-pipeline - Cloud Service](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Läs mer om hur du konfigurerar pipelines, både fullständig stack och frontend, i det här dokumentet.
