---
title: Headless Development for AEM Sites as a Cloud Service
description: Lär dig hur AEM som en Cloud Services kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att du kan hantera upplevelserna centralt och leverera dem i olika kanaler.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 469579cfe10227ab22bbe055d4c503d8ea978150
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

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

## Dina första steg med AEM Headless {#first-steps}

Det finns ett antal resurser som du kan använda för att komma igång med AEM headless-funktioner. De är avsedda för olika användningsområden, men ger alla en bra översikt över AEM rubrikfria funktioner.

| Resurs | Beskrivning | Typ | Målgrupp | Beräkna. Time |
|---|---|---|---|---|
| [Headless Developer Journey](/help/implementing/developing/headless-journey/overview.md) | Börja här om du vill få en heltäckande översikt över AEM headless-funktioner från teorin om headless genom att gå live med ditt första headless-projekt. | Guide | Utvecklare | 1 timme |
| [Starthandbok för Headless](/help/implementing/developing/headless/getting-started/introduction.md) | En kort sammanfattning av de viktigaste AEM rubrikfria funktionerna finns i den här snabbstartsöversikten. | Snabbstart | Utvecklare, administratörer | 20 minuter |
| [Komma igång med AEM självstudiekurs utan hörn](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | Om du föredrar en praktisk strategi går den här självstudiekursen direkt in i ett enkelt headless-projekt. | Självstudiekurs | Utvecklare | 2 timmar |
