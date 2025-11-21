---
title: Introduktion till Headless för AEM
description: Läs mer om Headless i Adobe Experience Manager (AEM) med en kombination av detaljerad dokumentation och headless-resor. Lär dig hur funktioner som modeller för innehållsfragment, innehållsfragment och ett GraphQL-API används för att driva Headless-upplevelser.
landing-page-description: Lär dig hur du använder och administrerar Headless i Adobe Experience Manager as a Cloud Service.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
feature: Headless
role: Admin, Developer
source-git-commit: 920045ab4e79dc223706219bf64347649af14125
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 8%

---


# Introduktion till Adobe Experience Manager som Headless CMS {#introduction-aem-headless}

Lär dig hur du använder Adobe Experience Manager (AEM) som ett Headless CMS (Content Management System) med funktioner som Content Fragment Models, Content Fragments och ett GraphQL-API som tillsammans ger dig en kraftfull, skalbar upplevelse.

Du kan läsa detaljerad dokumentation om de olika funktionerna och/eller följa urvalet av [Headless Journeys för att få en översikt över de första stegen](#first-steps).

>[!NOTE]
>
>Se även [Vad är Headless?](/help/headless/what-is-headless.md) om du vill ha en introduktion till Headless-koncept och -terminologi.

## Ökning {#overview}

AEM Headless är en CMS-lösning från Experience Manager som gör att strukturerat innehåll (innehållsfragment) i AEM kan användas av alla appar via HTTP med GraphQL. Headless-implementationer gör det möjligt att leverera upplevelser för olika plattformar och kanaler i stor skala.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter, vilket är vanligt i kompletta stacklösningar och hybridlösningar. I stället fokuserar det på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

![AEM implementeringsmodeller](assets/aem-implementation-models.png)

## Funktioner {#aem-headless-features}

AEM as a Cloud Service är ett flexibelt verktyg för en headless-implementeringsmodell med tre kraftfulla funktioner:

1. **Modeller för innehållsfragment**
   * Content Fragment Models är strukturerade representationer av innehåll.
   * Content Fragment Models definieras av informationsarkitekter i AEM Content Fragment Model Editor.
   * Content Fragment Models fungerar som bas för Content Fragments.
1. **Innehållsfragment**
   * Ett innehållsfragment skapas baserat på en innehållsfragmentmodell.
   * Innehållsfragment skapas av innehållsförfattare med AEM Content Fragment Editor.
   * Innehållsfragment lagras som AEM Assets, men kan hanteras via Assets Console eller [konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).
1. **Innehålls-API för leverans**
   * Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de koncept som ingår.

   * Direktleverans av innehåll är också möjligt med [JSON-exporten av kärnkomponenten för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## Dina första steg {#first-steps}

Det finns flera tillgängliga resurser för att komma igång med AEM headless-funktioner. Varje guide är anpassad för olika användningsområden och målgrupper.

| Resurs | Beskrivning | Typ | Målgrupp | Beräkna. Tid |
|---|---|---|---|---|
| [Headless Developer Journey](/help/journey-headless/developer/overview.md) | **För utvecklare som är nya för AEM och headless**-tekniker kan du börja här för att få en omfattande introduktion till AEM och dess headless-funktioner, från teorin om headless till att börja med ditt första headless-projekt. | Guide | Utvecklare **nybörjare i AEM och headless** | 1 timme |
| [Headless-inställningar](/help/headless/setup/introduction.md) | **För erfarna AEM-användare** som behöver en kort sammanfattning av de viktigaste rubrikfria funktionerna i AEM kan du ta en titt på den här snabbstartsöversikten. | Referensinställningar | Utvecklare, administratörer **med AEM** | 20 minuter |
| [Självstudiekurs utan hörn](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Om du föredrar en praktisk lösning och är bekant med AEM** är det här självstudiekursen som handlar om att implementera en enkel headless-app. | Självstudiekurs | Utvecklare | 2 timmar |
| [Headless Architect Journey](/help/journey-headless/architect/overview.md) | **För arkitekter som är nya för AEM och headless**-tekniker kan du börja här för att få en introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager as a Cloud Service och hur du modellerar innehåll för ditt projekt. | Guide | Arkitekter | 1 timme |
| [Headless Authoring Journey](/help/journey-headless/author/overview.md) | **För företagsanvändare som inte har använt AEM eller headless** kan du börja här för att få en introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager as a Cloud Service och hur du modellerar innehåll för ditt projekt. | Guide | Innehållsskapare | 1 timme |
| [Headless Translation Journey](/help/journey-headless/translation/overview.md) | För de **som är intresserade av AEM översättningsmetod för headless**. Lär dig mer om headless-teknik och hur du skapar och uppdaterar översättningsprojekt i AEM från A till Z. | Guide | Översättningsspecialister | 1 timme |

## Jämför Headful och Headless {#headful-headless}

Den här guiden fokuserar på AEM fullständiga headless-implementeringsmodell. Du behöver dock inte vara binärt i AEM för att vara både headful och headless. Headless-funktioner kan användas för att hantera och leverera innehåll till flera kontaktpunkter, samtidigt som innehållsförfattare kan redigera single page-applikationer. Allt i AEM.

>[!TIP]
>
>Mer information finns i dokumentet [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md).
