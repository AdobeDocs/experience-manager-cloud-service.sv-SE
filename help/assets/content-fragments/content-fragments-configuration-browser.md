---
title: Content Fragments - Configuration Browser
description: Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser för att utnyttja AEM kraftfulla headless-leveransfunktioner.
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 2e6f59fe663a3c93fc612b888f151d75dc5821f6
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 17%

---

# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser för att utnyttja AEM kraftfulla headless-leveransfunktioner.

## Aktivera funktionen för innehållsfragment för instansen {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment måste du använda **Konfigurationsläsaren** för att aktivera:

* **Modeller för innehållsfragment** - obligatoriskt
* **Beständiga GraphQL-frågor** - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **Modeller för innehållsfragment**:
>
>* den **Skapa** kan inte användas för att skapa nya modeller.
>* kommer du inte att kunna [välj platskonfigurationen för att skapa den relaterade slutpunkten](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


Om du vill aktivera funktioner för innehållsfragment måste du:

* Aktivera användning av innehållets fragmentfunktioner via konfigurationsläsaren
* Använda konfigurationen i resursmappen

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Till [använda vissa funktioner för innehållsfragment](#creating-a-content-fragment-model) dig **måste** först aktivera dem via **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns i [Konfigurationsläsaren:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Delkonfigurationer (en konfiguration som är kapslad i en konfiguration) stöds för användning med innehållsfragment, men kan inte användas för GraphQL-frågor.

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **Titel**.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **Beständiga GraphQL-frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)


1. Välj **Skapa** för att spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen i resursmappen {#apply-the-configuration-to-your-assets-folder}

När konfigurationen **global** är aktiverat för innehållets fragmentfunktion och gäller sedan för alla resursmappar.

Om du vill använda andra konfigurationer (dvs. exkludera globala) med en jämförbar Assets-mapp måste du definiera kopplingen. Detta gör du genom att välja lämplig **konfiguration** på fliken **Cloud Services** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)
