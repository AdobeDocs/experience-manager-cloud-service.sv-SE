---
title: Aktivera frontpipeline
description: Lär dig hur du kan aktivera frontend-flödet för befintliga webbplatser för att utnyttja webbplatsteman för att snabbare anpassa din webbplats.
feature: Administering
role: Admin
source-git-commit: dc7e89c601bb02c78f65ca58eff34c15092b5561
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Aktivera frontpipeline {#enable-front-end-pipeline}

Lär dig hur du kan aktivera frontend-flödet för befintliga webbplatser för att utnyttja webbplatsteman för att snabbare anpassa din webbplats.

## Översikt {#overview}

Det är en mekanism som snabbt kan driftsätta endast koden på era webbplatser baserat på [webbplatsteman](site-themes.md) och [webbplatsmallar.](site-templates.md)

I stället för att använda den fullständiga stacken hanteras bara den färdiga koden av den här pipeline som gör processen snabbare och gör det även möjligt för gränssnittsutvecklare att enkelt och snabbt anpassa din webbplats utan att känna till AEM.

Webbplatser som är baserade på webbplatsmallar kan utnyttja frontendspipelinen som standard. I det här dokumentet beskrivs hur du kan anpassa dina befintliga webbplatser för att dra nytta av frontendriet.

>[!TIP]
>
>Om du inte känner till produktionsflödet och hur du snabbt distribuerar webbplatser med hjälp av det och webbplatsmallar kan du läsa [Snabbskapande av webbplats - resa](/help/journey-sites/quick-site/overview.md) för en introduktion.

Om du inte har skapat din befintliga webbplats baserat på webbplatsmallar och teman, kan AEM konfigurera din webbplats så att den läser in de teman som distribueras med Front End Pipeline ovanpå befintliga klientbibliotek.

## Krav {#requirements}

AEM kan automatiskt anpassa din befintliga webbplats så att den använder frontendriet. För att kunna göra detta måste webbplatsen använda [v2 eller senare av Page Component of the Core Components.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Aktivera frontendspipeline {#enabling}

Du aktiverar din plats via webbplatskonsolen.

1. Logga in AEM och navigera till webbplatsen via **Global navigering** > **Webbplatser**.
1. Välj din plats i konsolen. Du måste markera platsens rot och inte underordnade sidor.
1. När webbplatsen är markerad öppnar du [järnvägsväljare](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) till vänster och välj **Plats**.
1. I **Plats** klicka på knappen **Aktivera frontdelspipeline**.

   ![Aktivera frontendpipeline](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM ber dig bekräfta med en översikt över de ändringar som kommer att göras. Bekräfta att webbplatsen har anpassats.

Nu är webbplatsen redo att använda frontendriet. Mer information om frontendriet finns i:

* [Skapa snabbt webbplatser](/help/journey-sites/quick-site/overview.md) - Den här dokumentationsresan ger dig och en heltäckande översikt över processen att snabbt distribuera en webbplats med hjälp av pipeline i gränssnittet och verktyget för att skapa snabbwebbplatser.
* [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - I det här dokumentet beskrivs frontendjörledningen i samband med rörledningar i full hög och på webbnivå.
