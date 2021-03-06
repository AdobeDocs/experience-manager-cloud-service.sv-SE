---
title: Hantera GraphQL-slutpunkter i AEM
description: Lär dig hur du hanterar GraphQL-slutpunkter i Adobe Experience Manager as a Cloud Service för leverans av headless-innehåll.
feature: Content Fragments,GraphQL API
exl-id: f7164ae3-4074-4db7-8c43-a79cc2ef00b1
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Hantera GraphQL-slutpunkter i AEM {#graphql-aem-endpoint}

Slutpunkten är den bana som används för att komma åt GraphQL för AEM. Med den här sökvägen kan du (eller din app):

* få tillgång till GraphQL-schemat,
* skicka GraphQL-frågor,
* ta emot svar (på GraphQL-frågor).

Det finns två typer av slutpunkter i AEM:

* Global
   * Tillgängligt för alla webbplatser.
   * Den här slutpunkten kan använda alla modeller för innehållsfragment från alla platskonfigurationer (definieras i [Konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Om det finns några modeller för innehållsfragment som ska delas mellan platskonfigurationer, ska dessa skapas under de globala platskonfigurationerna.
* Platskonfigurationer:
   * Motsvarar en platskonfiguration, enligt definitionen i [Konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Specifikt för en angiven plats/ett angivet projekt.
   * En platskonfigurationsspecifik slutpunkt använder innehållsfragmentmodellerna från den specifika platskonfigurationen tillsammans med de från den globala platskonfigurationen.

>[!CAUTION]
>
>Innehållsfragmentsredigeraren kan tillåta att ett innehållsfragment av en platskonfiguration refererar till ett innehållsfragment av en annan platskonfiguration (via principer).
>
>I så fall går det inte att hämta allt innehåll med en platskonfigurationsspecifik slutpunkt.
>
>Innehållsförfattaren bör kontrollera detta scenario; Det kan till exempel vara bra att överväga att placera delade modeller för innehållsfragment under konfigurationen för globala platser.

Databassökvägen för GraphQL för AEM globala slutpunkten är:

`/content/cq:graphql/global/endpoint`

För vilken ditt program kan använda följande sökväg i URL:en för begäran:

`/content/_cq_graphql/global/endpoint.json`

Om du vill aktivera en slutpunkt för GraphQL för AEM måste du:

* [Aktivera GraphQL-slutpunkten](#enabling-graphql-endpoint)
* [Publicera din GraphQL-slutpunkt](#publishing-graphql-endpoint)

## Aktivera GraphQL-slutpunkten {#enabling-graphql-endpoint}

Om du vill aktivera en GraphQL-slutpunkt måste du först ha en lämplig konfiguration. Se [Content Fragments - Configuration Browser](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Om [användning av innehållsfragmentmodeller inte har aktiverats](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md), **Skapa** kommer inte att vara tillgängligt.

Så här aktiverar du motsvarande slutpunkt:

1. Navigera till **verktyg**, **Allmänt** väljer **GraphQL**.
1. Välj **Skapa**.
1. The **Skapa ny GraphQL-slutpunkt** öppnas. Här kan du ange:
   * **Namn**: Slutpunktens namn. du kan skriva vilken text som helst.
   * **Använd GraphQL-schema från**: Använd listrutan för att välja önskad plats/önskat projekt.

   >[!NOTE]
   >
   >Följande varning visas i dialogrutan:
   >
   >* *GraphQL-slutpunkter kan medföra problem med datasäkerhet och prestanda om de inte hanteras varsamt. Kontrollera att du har angett rätt behörigheter när du har skapat en slutpunkt.*


1. Bekräfta med **Skapa**.
1. The **Nästa steg** kommer att innehålla en direktlänk till säkerhetskonsolen så att du kan se till att den nyskapade slutpunkten har rätt behörigheter.

   >[!CAUTION]
   >
   >Slutpunkten är tillgänglig för alla. Detta kan - särskilt när det gäller publiceringsinstanser - utgöra ett säkerhetsproblem, eftersom GraphQL-frågor kan medföra en stor belastning på servern.
   >
   >Du kan ställa in åtkomstkontrollistor, som passar ditt användningsfall, på slutpunkten.

## Publicera GraphQL-slutpunkten {#publishing-graphql-endpoint}

Markera den nya slutpunkten och **Publicera** för att göra den helt tillgänglig i alla miljöer.

>[!CAUTION]
>
>Slutpunkten är tillgänglig för alla.
>
>På publiceringsinstanser kan detta utgöra ett säkerhetsproblem, eftersom GraphQL-frågor kan medföra en stor belastning på servern.
>
>Du måste konfigurera [Behörighetslistor som passar ditt användningsfall](/help/headless/security/permissions.md) på slutpunkten.
