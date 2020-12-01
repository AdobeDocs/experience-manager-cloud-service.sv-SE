---
title: Content Fragments - Configuration Browser
description: Lär dig hur du aktiverar vissa funktioner för innehållsfragment i konfigurationsläsaren.
translation-type: tm+mt
source-git-commit: ae918d074d4bacfc207d4dca2c67f41a3118aff4
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 20%

---


# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

>[!CAUTION]
>
>AEM GraphQL API, för Content Fragment Delivery, släpps i början av 2021.
>
>Den relaterade dokumentationen är redan tillgänglig för förhandsgranskning.

## Aktivera funktionen för innehållsfragment för din instans {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment måste du använda **Configuration Browser** för att aktivera:

* **Modeller**  för innehållsfragment - obligatoriskt
* **GraphQL Beständiga frågor**  - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **Content Fragment Models** kommer alternativet **Create** inte att vara tillgängligt för att skapa nya modeller.

Om du vill aktivera funktioner för innehållsfragment måste du:

* Aktivera användning av innehållets fragmentfunktioner via konfigurationsläsaren
* Använda konfigurationen i resursmappen

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Om du vill [använda vissa funktioner för innehållsfragment](#creating-a-content-fragment-model) måste du **först aktivera dem via** **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns även i [Konfigurationsläsaren:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.
2. Välj lämplig plats för webbplatsen.
3. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **titel**.
   2. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **Beständiga GraphQL-frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)


4. Välj **Skapa** om du vill spara definitionen.

### Använd konfigurationen i resursmappen {#apply-the-configuration-to-your-assets-folder}

När konfigurationen **global** är aktiverad för innehållets fragmentfunktion, gäller den alla resursmappar.

Om du vill använda andra konfigurationer (dvs. exkludera globala) med en jämförbar Assets-mapp måste du definiera kopplingen. Detta gör du genom att välja lämplig **konfiguration** på fliken **Cloud Services** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)