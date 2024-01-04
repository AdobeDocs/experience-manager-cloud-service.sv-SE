---
title: Content Fragments - Setup
description: Lär dig hur du aktiverar Content Fragment- och GraphQL-funktioner som kan användas med AEM headless-funktioner och sidredigering.
feature: Content Fragments
role: Developer, Architect
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
source-git-commit: 19685cb952a890731bd7d75a2adf3cfd841a465f
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 3%

---

# Content Fragments - Setup {#content-fragments-setup}

Med innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service kan du förbereda innehåll som ska användas på flera platser och i flera kanaler. Detta är idealiskt för headlessleverans och sidredigering.

Så här aktiverar du instansen för funktionen för innehållsfragment:

* **Modeller för innehållsfragment** - obligatoriskt

  >[!CAUTION]
  >
  >Om du inte aktiverar **Modeller för innehållsfragment**:
  >
  >* den **Skapa** kan inte användas för att skapa modeller.
  >* kommer du inte att kunna [välj platskonfigurationen för att skapa den relaterade slutpunkten](/help/headless/graphql-api/graphql-endpoint.md).

* **GraphQL Beständiga frågor** - valfritt

Instansen har konfigurerats:

* av [aktivera funktioner i Configuration Browser](#enable-content-fragment-functionality-configuration-browser)
* sedan [tillämpa konfigurationen på dina enskilda resursmappar](#apply-the-configuration-to-your-folder)

## Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-configuration-browser}

Om du vill använda funktionen för innehållsfragment, för modeller för innehållsfragment och GraphQL beständiga frågor, ska du **måste** först aktivera dem via **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns i [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Delkonfigurationer](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (en konfiguration som är kapslad i en annan konfiguration) stöds fullt ut för användning med Content Fragments, Content Fragment Models och GraphQL queries.
>
>Observera följande:
>
>* När du har skapat modeller i en delkonfiguration går det INTE att flytta eller kopiera modellen till en annan underkonfiguration.
>
>* En GraphQL-slutpunkt kommer (fortfarande) att baseras på en överordnad (rot) konfiguration.
>
>* Beständiga frågor sparas (fortfarande) som är relevanta för den överordnade konfigurationen (roten).

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **Titel**.
   1. När du skapar **Namn** blir nodnamnet i databasen.
Du kan ange ett namn. Om du lämnar fältet tomt genereras det automatiskt baserat på titeln och justeras sedan enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md); du kan justera resultatet om det behövs.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **GraphQL Beständiga frågor**

      ![Definiera konfiguration](assets/cf-setup-create-conf.png)

1. Välj **Skapa** för att spara definitionen.

## Använd konfigurationen för din mapp {#apply-the-configuration-to-your-folder}

När konfigurationen **global** är aktiverat för funktionen för innehållsfragment och gäller sedan för alla Resursmappar som är tillgängliga via **Resurser** konsol.

Om du vill använda andra konfigurationer (och därmed utesluta globala) med en jämförbar resursmapp måste du definiera anslutningen. Gör detta genom att välja lämplig **Konfiguration** i **Cloud Service** -fliken i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cf-setup-apply-conf.png)
