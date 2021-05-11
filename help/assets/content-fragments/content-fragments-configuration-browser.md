---
title: Content Fragments - Configuration Browser
description: Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser för att utnyttja AEM kraftfulla headless-leveransfunktioner.
feature: Innehållsfragment
role: Business Practitioner
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
translation-type: tm+mt
source-git-commit: 0c7b66e636e36a8036a590e949aea42e33a4e289
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 18%

---

# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser för att utnyttja AEM kraftfulla headless-leveransfunktioner.

## Aktivera funktionen för innehållsfragment för din instans {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment måste du använda **Configuration Browser** för att aktivera:

* **Modeller**  för innehållsfragment - obligatoriskt
* **GraphQL Beständiga frågor**  - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **Content Fragment Models**:
>
>* **Alternativet Skapa** är inte tillgängligt för att skapa nya modeller.
>* du inte kan [välja platskonfigurationen för att skapa den relaterade slutpunkten](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


Om du vill aktivera funktioner för innehållsfragment måste du:

* Aktivera användning av innehållets fragmentfunktioner via konfigurationsläsaren
* Använda konfigurationen i resursmappen

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Om du vill [använda vissa funktioner för innehållsfragment](#creating-a-content-fragment-model) måste du **först aktivera dem via** **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns även i [Konfigurationsläsaren:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Delkonfigurationer (en konfiguration som är kapslad i en konfiguration) stöds inte för användning med innehållsfragment.

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **titel**.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **Beständiga GraphQL-frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)


1. Välj **Skapa** om du vill spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen i resursmappen {#apply-the-configuration-to-your-assets-folder}

När konfigurationen **global** är aktiverad för innehållets fragmentfunktion, gäller den alla resursmappar.

Om du vill använda andra konfigurationer (dvs. exkludera globala) med en jämförbar Assets-mapp måste du definiera kopplingen. Detta gör du genom att välja lämplig **konfiguration** på fliken **Cloud Services** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)
