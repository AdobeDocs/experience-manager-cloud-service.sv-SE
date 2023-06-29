---
title: Content Fragments - Configuration Browser
description: Lär dig hur du aktiverar funktionerna Content Fragment och GraphQL i Configuration Browser för att använda AEM headless delivery features.
feature: Content Fragments
role: User
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

Lär dig hur du aktiverar vissa funktioner för innehållsfragment i konfigurationsläsaren.

## Aktivera funktionen för innehållsfragment för instansen {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment måste du använda **Konfigurationsläsaren** för att aktivera:

* **Modeller för innehållsfragment** - obligatoriskt
* **GraphQL Beständiga frågor** - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **Modeller för innehållsfragment**:
>
>* den **Skapa** kan inte användas för att skapa modeller.
>* du inte kan [välj platskonfigurationen för att skapa den relaterade slutpunkten](/help/headless/graphql-api/graphql-endpoint.md).

Om du vill aktivera funktionen för innehållsfragment måste du göra följande:

* Aktivera användning av innehållets fragmentfunktioner via konfigurationsläsaren
* Använda konfigurationen i resursmappen

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Använda vissa [Funktion för innehållsfragment](#creating-a-content-fragment-model), **måste** först aktivera dem via **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns i [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Delkonfigurationer](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (en konfiguration som är kapslad i en annan konfiguration) stöds fullt ut för användning med Content Fragments, Content Fragment Models och GraphQL queries.
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

   1. Ange en **Titel**.
   1. The **Namn** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md).
      * Du kan justera den om det behövs.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **GraphQL Beständiga frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)

1. Välj **Skapa** för att spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen för din mapp {#apply-the-configuration-to-your-folder}

När konfigurationen **global** är aktiverat för innehållets fragmentfunktion, gäller för alla resursmappar som är tillgängliga via **Resurser** konsol.

Om du vill använda andra konfigurationer (d.v.s. exkludera globala) med en jämförbar resursmapp måste du definiera anslutningen. Den här anslutningen görs genom att välja lämplig **Konfiguration** i **Cloud Services** -fliken i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)
