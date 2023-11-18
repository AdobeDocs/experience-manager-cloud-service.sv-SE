---
title: Aktivera frontendspipelinen
description: Lär dig hur du kan aktivera frontend-flödet för befintliga webbplatser så att du kan använda webbplatsteman för att anpassa webbplatsen snabbare.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Aktivera frontendspipelinen {#enable-front-end-pipeline}

Lär dig hur du kan aktivera frontend-flödet för befintliga webbplatser så att du kan använda webbplatsteman för att anpassa webbplatsen snabbare.

## Översikt {#overview}

Det är en mekanism som snabbt kan driftsätta endast koden på era webbplatser baserat på [webbplatsteman](site-themes.md) och [webbplatsmallar.](site-templates.md)

I stället för att använda den fullständiga stacken hanteras bara den färdiga koden av den här pipeline som gör processen snabbare och gör det även möjligt för gränssnittsutvecklare att enkelt och snabbt anpassa din webbplats utan att känna till AEM.

Platser som är baserade på platsmallar kan som standard använda frontendspipelinen. I det här dokumentet beskrivs hur du kan anpassa dina befintliga webbplatser för att dra nytta av frontendriet.

>[!TIP]
>
>Om du inte känner till produktionsflödet och hur du snabbt distribuerar webbplatser med hjälp av det och webbplatsmallar kan du läsa [Snabbskapande av webbplats - resa](/help/journey-sites/quick-site/overview.md) för en introduktion.

Om du inte har skapat din befintliga webbplats baserat på webbplatsmallar och teman, kan AEM konfigurera din webbplats så att den läser in de teman som distribueras med Front End Pipeline ovanpå befintliga klientbibliotek.

## Teknisk information {#technical-details}

När du aktiverar frontend-flödet för en webbplats gör AEM följande ändringar i platsstrukturen.

* Alla sidor på webbplatsen kommer att innehålla ytterligare en CSS- och JS-fil, som kan ändras genom att distribuera uppdateringar via en dedikerad molnhanterare.
* De tillagda CSS- och JS-filerna kommer från början att vara tomma, men en temakällsmapp kan laddas ned för att starta mappstrukturen som gör det möjligt att distribuera CSS- och JS-koduppdateringar via den pipeline som läggs till.
* Den här ändringen kan bara ångras av en utvecklare genom att ta bort `SiteConfig` och `HtmlPageItemsConfig` noder som skapas under den här åtgärden `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Den här åtgärden konverterar inte automatiskt befintliga klientbibliotek på webbplatsen till att använda teckensnittsslutsflödet. Att flytta de här källorna från klientbiblioteksmappen till frontendmappen är en uppgift som kräver manuellt arbete av en frontendutvecklare.

## Krav {#requirements}

AEM kan automatiskt anpassa din befintliga webbplats så att den använder frontendriet. För att kunna göra detta måste webbplatsen använda [v2 eller senare av Page Component of the Core Components.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Aktivera frontendspipeline {#enabling}

Du aktiverar din plats från webbplatskonsolen med hjälp av [Platsjärnvägar.](site-rail.md)

1. Logga in AEM och navigera till webbplatsen via **Global navigering** > **Webbplatser**.
1. Välj din plats i konsolen. Markera platsens rot och inte underordnade sidor.
1. När webbplatsen är markerad öppnar du [järnvägsväljare](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) till vänster och välj **Plats**.
1. I **Plats** klicka på knappen **Aktivera frontdelspipeline**.

   ![Aktivera frontendpipeline](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM ber dig bekräfta med en översikt över de ändringar som kommer att göras. Bekräfta att webbplatsen har anpassats.

Nu är webbplatsen redo att använda frontendriet. Om du vill veta mer om frontend-flödet och hur du hanterar ditt webbplatstema kan du läsa:

* [Använda webbplatsservern för att hantera ditt webbplatstema](site-rail.md)
* [Skapa snabbt webbplatser](/help/journey-sites/quick-site/overview.md) - Den här dokumentationsresan ger dig och en heltäckande översikt över processen att snabbt distribuera en webbplats med hjälp av pipeline i gränssnittet och verktyget för att skapa snabbwebbplatser.
* [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - I det här dokumentet beskrivs frontendjörledningen i samband med rörledningar i full hög och på webbnivå.
