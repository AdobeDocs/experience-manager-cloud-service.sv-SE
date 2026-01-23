---
title: Content Fragments - Setup
description: Lär dig hur du aktiverar Content Fragment- och GraphQL-funktioner som kan användas med AEM headless-funktioner för leverans och sidredigering.
feature: Content Fragments
role: Developer
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
solution: Experience Manager Sites
source-git-commit: b3e1d3a3770531728d696be125f074881f179573
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 2%

---

# Content Fragments - Setup {#content-fragments-setup}

Med innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service kan du förbereda innehåll som ska användas på flera platser och i flera kanaler. Detta är idealiskt för headlessleverans och sidredigering.

Så här aktiverar du instansen för funktionen för innehållsfragment:

* **Modeller för innehållsfragment** - obligatoriskt

  >[!CAUTION]
  >
  >Om du inte aktiverar **modeller för innehållsfragment**:
  >
  >* alternativet **Skapa** är inte tillgängligt för att skapa modeller.
  >* Du kan inte [välja platskonfigurationen för att skapa den relaterade slutpunkten](/help/headless/graphql-api/graphql-endpoint.md).

* **GraphQL Persisted Queries** - valfritt

Instansen har konfigurerats:

* av [aktivera funktioner i konfigurationsläsaren](#enable-content-fragment-functionality-configuration-browser)
* [tillämpar sedan konfigurationen på dina enskilda Assets-mappar](#apply-the-configuration-to-your-folder)

>[!TIP]
>
>Innehållsfragment kan [publiceras till Edge Delivery Services.](https://www.aem.live/developer/content-fragment-overlay)

## Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-configuration-browser}

Om du vill använda funktionen för innehållsfragment, för modeller för innehållsfragment och GraphQL beständiga frågor, måste **du** först aktivera dem via **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns i [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Delkonfigurationer](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (en konfiguration som är kapslad i en annan konfiguration) stöds fullt ut för användning med innehållsfragment, innehållsfragmentmodeller och GraphQL-frågor.
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

   1. Ange en **titel**.
   1. När **Name** skapas blir det nodnamnet i databasen.
Du kan ange ett namn. Om du lämnar fältet tomt genereras det automatiskt baserat på titeln och justeras sedan enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md). Du kan justera resultatet om det behövs.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **GraphQL beständiga frågor**

      ![Definiera konfiguration](assets/cf-setup-create-conf.png)

1. Välj **Skapa** om du vill spara definitionen.

## Använd konfigurationen för din mapp {#apply-the-configuration-to-your-folder}

När konfigurationen **global** är aktiverad för funktionen Innehållsfragment gäller den alla Assets-mappar som är tillgängliga via **Assets**-konsolen.

Om du vill använda andra konfigurationer (alltså inte globala) med en jämförbar Assets-mapp måste du definiera anslutningen. Det gör du genom att välja lämplig **konfiguration** på fliken **Cloud-tjänster** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cf-setup-apply-conf.png)
