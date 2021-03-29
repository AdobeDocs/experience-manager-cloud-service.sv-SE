---
title: Headless Development for AEM Sites as a Cloud Service
description: Lär dig hur AEM som en Cloud Services kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att du kan hantera upplevelserna centralt och leverera dem i olika kanaler.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Headless Development for AEM Sites as a Cloud Service {#headless-development}

Lär dig hur AEM som en Cloud Services kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att du kan hantera upplevelserna centralt och leverera dem i olika kanaler.

## Översikt {#overview}

Headless-implementering blir allt viktigare för att ni ska kunna leverera upplevelser till er målgrupp, oavsett var de finns och kanal.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter på samma sätt som traditionella lösningar med kompletta stackar och hybridlösningar och fokuserar på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

![AEM implementeringsmodeller](assets/aem-implementation-models.png)

## Jämför Headful och Headless {#headful-headless}

Det här dokumentet fokuserar på den fullständiga headless-implementeringsmodellen för AEM. Men headful kontra headless behöver inte vara ett binärt val i AEM. Headless-funktioner kan användas för att hantera och leverera innehåll till olika slutpunkter och samtidigt göra det möjligt för innehållsförfattare att redigera single page-applikationer. Allt i AEM.

>[!TIP]
>
>Mer information finns i dokumentet [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md).

## AEM som en Cloud Service och Headless {#aem-headless}

AEM som Cloud Service är ett flexibelt verktyg för den headless-implementeringsmodellen genom att erbjuda tre kraftfulla tjänster:

1. Innehållsmodeller
   * Innehållsmodeller är strukturerade representationer av innehåll.
   * Dessa definieras av informationsarkitekter i AEM Content Fragment Model Editor.
   * Innehållsmodeller fungerar som bas för innehållsfragment.
1. Innehållsfragment
   * Innehållsfragment är instansieringar av innehållsmodeller.
   * Dessa skapas av innehållsförfattare med AEM Content Fragment Editor.
   * De lagras i AEM Assets och hanteras i gränssnittet Resurser Admin.
1. Innehålls-API för leverans
   * AEM GraphQL API har stöd för leverans av innehållsfragment.
   * AEM Assets REST API stöder CRUD-åtgärder för innehållsfragment.
   * Direktleverans av innehåll är också möjligt med JSON-exporten för komponenten [Content Fragment Core Component.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## Headless Getting Started Guides {#getting-started}

Med de Headless Getting Started Guides kan du enkelt skapa, hantera och leverera upplevelser med AEM som Cloud Service i fem steg. Varje guide bygger vidare på det föregående, så vi rekommenderar att du tittar noga igenom dem i ordning.

1. [Skapa en konfiguration](getting-started/create-configuration.md)
1. [Skapa en innehållsfragmentmodell](getting-started/create-content-model.md)
1. [Skapa en resursmapp](getting-started/create-assets-folder.md)
1. [Skapa ett innehållsfragment](getting-started/create-content-fragment.md)
1. [Åtkomst och leverans av innehållsfragment](getting-started/create-api-request.md)

## Målgrupp {#audience}

De åtgärder som beskrivs i [Headless Getting Started Guides](#getting-started) är nödvändiga för en grundläggande demonstration av AEM headless-funktioner. Alla som har administratörsåtkomst till en testinstans AEM kan följa dessa guider för att förstå headlessleverans i AEM, även om någon med utvecklarupplevelse är idealisk.

I en produktionssituation kommer uppgifterna dock att utföras av olika personer, olika många gånger. Till exempel:

* **Administratörer** måste konfigurera den inledande konfigurationen och mappstrukturen för innehållet, vanligtvis endast en gång eller sporadiskt.
* **Informationsarkitekturen** lägger i allmänhet till nya modeller i takt med att organisationens behov utvecklas.
* **Innehållsförfattare** skapar kontinuerligt nytt innehåll som innehållsfragment baserat på de modeller som definieras av arkitekterna.

Guiderna Komma igång utan rubriker visar vem som i allmänhet utför de beskrivna åtgärderna och hur ofta.

## Nästa steg {#next-step}

Vill du lära dig mer? Kom sedan igång genom att läsa den första delen av Headless Getting Started Guide: [Skapar en konfiguration.](getting-started/create-configuration.md)
