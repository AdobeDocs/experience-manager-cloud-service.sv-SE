---
title: Introduktion till AEM Headless
description: Lär dig mer om Adobe Experience Manager (AEM) som headless CMS med en kombination av detaljerad dokumentation och resor utan huvud. Lär dig hur funktioner som innehållsmodeller, innehållsfragment och ett GraphQL API används för att skapa headless-upplevelser.
landing-page-description: Lär dig hur du använder och administrerar Experience Manager Headless as a Cloud Service.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 4e64683598ced4b9811e957082932971f0ec0bb1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Introduktion till Adobe Experience Manager som headless CMS {#introduction-aem-headless}

Lär dig hur du använder Adobe Experience Manager (AEM) som ett headless CMS med funktioner som innehållsmodeller, innehållsfragment och ett GraphQL-API som ger en kraftfull, skalbar upplevelse.

Du kan läsa detaljerad dokumentation om de olika funktionerna och/eller följa valet av [Headless Journeys för att få en översikt över de första stegen](#first-steps).

>[!NOTE]
>
>Se även [Vad är Headless?](/help/headless/what-is-headless.md) för en introduktion till Headless-koncept och -terminologi.

## Översikt {#overview}

AEM Headless är en CMS-lösning från Experience Manager som gör att strukturerat innehåll (innehållsfragment) i AEM kan användas av alla appar via HTTP med GraphQL. Headless-implementationer gör det möjligt att leverera upplevelser för olika plattformar och kanaler i stor skala.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter på samma sätt som traditionella lösningar med kompletta stackar och hybridlösningar och fokuserar på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

![AEM implementeringsmodeller](assets/aem-implementation-models.png)

## Funktioner för AEM Headless {#aem-headless-features}

AEM as a Cloud Service är ett flexibelt verktyg för den headless-implementeringsmodellen med tre kraftfulla funktioner:

1. **Innehållsmodeller**
   * Innehållsmodeller är strukturerade representationer av innehåll.
   * Innehållsmodeller definieras av informationsarkitekter i AEM Content Fragment Model Editor.
   * Innehållsmodeller fungerar som bas för innehållsfragment.
1. **Innehållsfragment**
   * Innehållsfragment skapas baserat på en innehållsmodell.
   * Skapas av innehållsförfattare med AEM Content Fragment editor.
   * Innehållsfragment lagras i AEM Assets och hanteras i gränssnittet Resurser Admin.
1. **Innehålls-API för leverans**
   * AEM GraphQL API har stöd för leverans av innehållsfragment.
   * AEM Assets REST API stöder CRUD-åtgärder för innehållsfragment.
   * Direktleverans av innehåll är också möjligt med [JSON-export av kärnkomponenten för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## Dina första steg med AEM headless {#first-steps}

Det finns flera tillgängliga resurser för att komma igång med AEM headless-funktioner. Varje guide är skräddarsydd för olika användningsområden och målgrupper.

| Resurs | Beskrivning | Typ | Målgrupp | Beräkna. Time |
|---|---|---|---|---|
| [Headless Developer Journey](/help/journey-headless/developer/overview.md) | **För utvecklare som inte är AEM och utan headless** börjar du här för att få en omfattande introduktion till AEM och dess headless-funktioner från teorin om headless genom att publicera ditt första headless-projekt. | Guide | Utvecklare **nya i AEM och utan huvud** | 1 timme |
| [Headless Setup](/help/headless/setup/introduction.md) | **För erfarna AEM** som behöver en kort sammanfattning av de viktigaste AEM rubrikfria funktionerna, se den här snabbstartsöversikten. | Referensinställningar | Utvecklare, administratörer **med AEM** | 20 minuter |
| [Självstudiekurs utan hörn](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Om du föredrar en praktisk lösning och är bekant med AEM** den här självstudiekursen lär sig att implementera en enkel headless-app. | Självstudiekurs | Utvecklare | 2 timmar |
| [Headless Architect Journey](/help/journey-headless/architect/overview.md) | **För arkitekter som är nya för AEM och utan huvud** börjar du här för att få en introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager as a Cloud Service och för hur du modellerar innehåll för ditt projekt. | Guide | Arkitekter | 1 timme |
| [Headless Authoring Journey](/help/journey-headless/author/overview.md) | **För företagsanvändare som inte är AEM och utan headless** börjar du här för att få en introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager as a Cloud Service och för hur du modellerar innehåll för ditt projekt. | Guide | Innehållsskapare | 1 timme |
| [Headless Translation Journey](/help/journey-headless/translation/overview.md) | För dessa **intresserad av AEM översättningsstrategi för headless**. Lär dig mer om headless-teknik och hur du skapar och uppdaterar översättningsprojekt i AEM från A till Z. | Guide | Översättningsspecialister | 1 timme |

## Jämför Headful och Headless {#headful-headless}

Den här guiden fokuserar på den fullständiga headless-implementeringsmodellen för AEM. Men headful kontra headless behöver inte vara ett binärt val i AEM. Headless-funktioner kan användas för att hantera och leverera innehåll till flera kontaktpunkter, samtidigt som innehållsförfattare kan redigera single page-applikationer. Allt i AEM.

>[!TIP]
>
>Se dokumentet [Headless and Headless in AEM](/help/implementing/developing/headful-headless.md) för mer information.