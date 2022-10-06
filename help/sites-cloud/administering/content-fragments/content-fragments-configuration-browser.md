---
title: Content Fragments - Configuration Browser
description: Lär dig hur du aktiverar funktionerna för innehållsfragment och GraphQL i Configuration Browser för att utnyttja AEM headless-leveransfunktioner.
feature: Content Fragments
role: User
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 944665bc7cac1f00811187a508a18800c3d73f2a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 14%

---

# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

Lär dig hur du aktiverar vissa funktioner för innehållsfragment i konfigurationsläsaren.

## Aktivera funktionen för innehållsfragment för instansen {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment måste du använda **Konfigurationsläsaren** för att aktivera:

* **Modeller för innehållsfragment** - obligatoriskt
* **GraphQL-beständiga frågor** - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **Modeller för innehållsfragment**:
>
>* den **Skapa** kan inte användas för att skapa nya modeller.
>* kommer du inte att kunna [välj platskonfigurationen för att skapa den relaterade slutpunkten](/help/headless/graphql-api/graphql-endpoint.md).


Om du vill aktivera funktioner för innehållsfragment måste du:

* Aktivera användning av innehållets fragmentfunktioner via konfigurationsläsaren
* Använda konfigurationen i resursmappen

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Till [använda vissa funktioner för innehållsfragment](#creating-a-content-fragment-model) dig **måste** först aktivera dem via **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns i [Konfigurationsläsaren:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Delkonfigurationer](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (en konfiguration som är kapslad i en annan konfiguration) stöds fullt ut för användning med Content Fragments, Content Fragment Models och GraphQL queries.
>
>Observera följande:
>
>
>* När du har skapat modeller i en underkonfiguration är det INTE möjligt att flytta eller kopiera modellen till en annan underkonfiguration.
>
>* En GraphQL-slutpunkt kommer (fortfarande) att baseras på en överordnad (rot) konfiguration.
>
>* Beständiga frågor sparas (fortfarande) som är relevanta för den överordnade konfigurationen (roten).



1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **Titel**.
   1. The **Namn** blir nodnamnet i databasen.
      * Det genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/implementing/developing/introduction/naming-conventions.md)
      * Du kan justera den om det behövs.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **GraphQL-beständiga frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)


1. Välj **Skapa** för att spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen för din mapp {#apply-the-configuration-to-your-folder}

När konfigurationen **global** är aktiverat för innehållets fragmentfunktion, vilket sedan gäller för alla resursmappar som är tillgängliga via **Resurser** konsol.

Om du vill använda andra konfigurationer (dvs. exkludera globala) med en jämförbar Assets-mapp måste du definiera kopplingen. Detta gör du genom att välja lämplig **konfiguration** på fliken **Cloud Services** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)
