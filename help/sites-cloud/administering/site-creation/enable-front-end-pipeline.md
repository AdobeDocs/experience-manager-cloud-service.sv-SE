---
title: Aktivera frontendspipelinen
description: Lär dig hur du kan aktivera frontend-flödet för befintliga webbplatser så att du kan använda webbplatsteman för att anpassa webbplatsen snabbare.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: a5661b6b75180dd77eb794eb5d215fd2e1d5eed0
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Aktivera frontendspipelinen {#enable-front-end-pipeline}

Lär dig hur du kan aktivera frontend-flödet för befintliga webbplatser så att du kan använda webbplatsteman för att anpassa webbplatsen snabbare.

## Ökning {#overview}

Framsidespipelinen är en mekanism som snabbt kan distribuera endast startkoden för dina webbplatser baserat på [webbplatsteman](site-themes.md) och [webbplatsmallar.](site-templates.md)

Detta tillvägagångssätt hanterar endast klientkod, vilket gör distributionsprocessen snabbare än distributioner i fullstackar. Det gör att gränssnittsutvecklare enkelt kan anpassa din webbplats utan att behöva känna till AEM.

Platser som är baserade på platsmallar kan som standard använda frontendspipelinen. I det här dokumentet beskrivs hur du kan anpassa dina befintliga webbplatser för att dra nytta av frontendriet.

>[!TIP]
>
>Om du inte känner till frontend-flödet och hur du snabbt distribuerar webbplatser med hjälp av det och webbplatsmallar kan du få en introduktion i [Skapa snabbwebbplats](/help/journey-sites/quick-site/overview.md).

AEM kan konfigurera din webbplats så att den läser in teman som har distribuerats med Front End Pipeline, även om din webbplats inte har skapats med webbplatsmallar och teman, genom att lägga dem ovanpå befintliga klientbibliotek.

## Teknisk information {#technical-details}

När du aktiverar frontend-flödet för en webbplats gör AEM följande ändringar i platsstrukturen.

* Alla sidor på webbplatsen innehåller ytterligare en CSS- och JS-fil, som kan ändras genom att distribuera uppdateringar via en dedikerad frontpipeline från Cloud Manager.
* De tillagda CSS- och JS-filerna är tomma från början. Du kan dock hämta en&quot;temakällmapp&quot; för att konfigurera den mappstruktur som behövs för att distribuera CSS- och JS-koduppdateringar via pipeline.
* Det är bara en utvecklare som kan ångra ändringen genom att ta bort noderna `SiteConfig` och `HtmlPageItemsConfig` som skapas under `/conf/<site-name>/sling:configs` med den här åtgärden.

>[!NOTE]
>
>Den här åtgärden konverterar inte automatiskt befintliga klientbibliotek på webbplatsen till att använda teckensnittsslutsflödet. Att flytta de här källorna från klientbiblioteksmappen till frontendmappen är en uppgift som kräver manuellt arbete av en frontendutvecklare.

## Krav {#requirements}

AEM kan automatiskt anpassa din befintliga webbplats så att den använder frontendriet. Om du vill kunna utföra det här arbetsflödet måste webbplatsen använda [v2 eller senare av Page Component i Core Components.](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/page)

## Aktivera frontendspipeline {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

Du aktiverar din plats från webbplatskonsolen med hjälp av [webbplatsspåret](site-rail.md).

1. Logga in AEM och navigera till din webbplats via **Global navigering** > **Webbplatser**.
1. Välj din plats i konsolen. Markera platsens rot och inte underordnade sidor.
1. När platsen är markerad öppnar du [spårväljaren](/help/sites-cloud/authoring/basic-handling.md#rail-selector) till vänster och väljer **Plats**.
1. Klicka på knappen **Aktivera frontpipeline** i **webbplatsens**-spår.

   ![Aktivera frontendpipeline](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM ber dig bekräfta med en översikt över ändringarna. Bekräfta att webbplatsen har anpassats.

Nu är webbplatsen redo att använda frontendriet. Om du vill veta mer om frontend-flödet och hur du hanterar ditt webbplatstema kan du läsa:

* [Använda webbplatsservern för att hantera ditt webbplatstema](site-rail.md)
* [Snabbresa för att skapa webbplats](/help/journey-sites/quick-site/overview.md) - Den här dokumentationsresan ger dig och en heltäckande översikt över processen att snabbt distribuera en webbplats med hjälp av frontendspipelinen och verktyget Skapa snabbwebbplats.
* [CI/CD-pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - Det här dokumentet beskriver frontendpipelinen i kontexten för hela stacken och på webbskiktet.

## Front-End Pipeline och anpassade domäner {#custom-domains}

Så som beskrivs i avsnittet [Teknisk information](#technical-details) skapar en `SiteConfig` - och `HtmlPageItemsConfig` -nod under `/conf/<site-name>/sling:configs` om du aktiverar funktionen för frontpipeline för en webbplats. 

Om du vill använda [Cloud Manager-funktionen för anpassade domäner](/help/implementing/cloud-manager/custom-domain-names/introduction.md) för din webbplats tillsammans med frontdelslinjen, måste ytterligare egenskaper läggas till i de här noderna.

1. Ange egenskapen `customFrontendPrefix` i `SiteConfig` för platsen.
1. Detta uppdaterar värdet `prefixPath` för `HtmlPageItemsConfig` med den anpassade domänen.

Sidorna för webbplatsen refererar sedan till temaartefakter från den uppdaterade URL:en.
