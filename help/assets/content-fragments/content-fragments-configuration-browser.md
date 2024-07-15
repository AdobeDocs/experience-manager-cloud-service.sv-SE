---
title: Content Fragments - Configuration Browser (Assets - Content Fragments)
description: Lär dig hur du aktiverar funktionen för innehållsfragment i konfigurationsläsaren.
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
feature: Content Fragments
role: User, Admin, Developer
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 3%

---

# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser för att använda AEM kraftfulla headless-leveransfunktioner.

## Aktivera funktionen för innehållsfragment för instansen {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment måste du använda **Konfigurationsläsaren** för att aktivera:

* **Modeller för innehållsfragment** - obligatoriskt
* **GraphQL Persisted Queries** - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **modeller för innehållsfragment**:
>
>* alternativet **Skapa** är inte tillgängligt för att skapa modeller.
>* Du kan inte [välja platskonfigurationen för att skapa den relaterade slutpunkten](/help/headless/graphql-api/graphql-endpoint.md).

Om du vill aktivera funktionen för innehållsfragment måste du göra följande:

* Aktivera användning av innehållsfragmentsfunktioner via konfigurationsläsaren
* Använd konfigurationen i din Assets-mapp

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Om du vill använda vissa [funktioner för innehållsfragment](#creating-a-content-fragment-model) måste **du** först aktivera dem via **konfigurationsläsaren**:

>[!NOTE]
>
>Se [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Delkonfigurationer](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (en konfiguration som är kapslad i en annan konfiguration) stöds fullt ut för användning med innehållsfragment, innehållsfragmentmodeller och GraphQL-frågor.
>
>Observera följande:
>
>
>* När du har skapat modeller i en delkonfiguration går det INTE att flytta eller kopiera modellen till en annan underkonfiguration.
>
>* En GraphQL-slutpunkt är (fortfarande) baserad på en överordnad (rot) konfiguration.
>
>* Beständiga frågor sparas (fortfarande) som är relevanta för den överordnade konfigurationen (roten).


1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **titel**.
   1. **Namn** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md).
      * Du kan justera den om det behövs.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **GraphQL beständiga frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)

1. Välj **Skapa** om du vill spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen i din Assets-mapp {#apply-the-configuration-to-your-assets-folder}

När konfigurationen **global** är aktiverad för innehållsfragmentfunktioner gäller detta alla Assets-mappar.

Om du vill använda andra konfigurationer (d.v.s. inte globala) med en jämförbar Assets-mapp måste du definiera anslutningen. Den här anslutningen görs genom att du väljer lämplig **konfiguration** på fliken **Cloud Service** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)
