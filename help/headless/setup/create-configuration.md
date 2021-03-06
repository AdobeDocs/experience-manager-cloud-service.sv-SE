---
title: Skapa en konfiguration - Headless Setup
description: Skapa en konfiguration som ett första steg för att komma igång med headless på AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Skapa en konfiguration - Headless Setup {#creating-configuration}

Som ett första steg till att komma igång med headless på AEM as a Cloud Service måste du skapa en konfiguration.

## Vad är en konfiguration? {#what-is-a-configuration}

I Configuration Browser finns ett allmänt konfigurations-API, innehållsstruktur och lösningsmekanism för konfigurationer i AEM.

När det gäller headless content management i AEM kan du tänka på en konfiguration som en arbetsplats i AEM där du kan skapa dina innehållsmodeller, som definierar strukturen för ditt framtida innehåll och innehållsfragment. Du kan ha flera konfigurationer för att separera dessa modeller.

Om du känner till [sidmallar i en AEM-implementering,](/help/sites-cloud/authoring/features/templates.md) Användningen av konfigurationer för hantering av innehållsmodeller är likartad.

## Så här skapar du en konfiguration {#how-to-create-a-configuration}

En administratör behöver bara skapa en konfiguration en gång, eller mycket sällan, när det krävs en ny arbetsyta för att kunna ordna dina innehållsmodeller. I den här guiden behöver vi bara skapa en konfiguration.

1. Logga in AEM as a Cloud Service och välj **Verktyg -> Allmänt -> Konfigurationsläsaren**.
1. Ange en **Titel** och **Namn** för din konfiguration.
   * The **Titel** ska vara beskrivande.
   * The **Namn** blir nodnamnet i databasen.
      * Det genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/implementing/developing/introduction/naming-conventions.md)
      * Den kan vid behov justeras.
1. Markera följande alternativ:
   * **Modeller för innehållsfragment**
   * **GraphQL-beständiga frågor**

   ![Skapa konfiguration](../assets/create-configuration.png)

1. Tryck eller klicka **Skapa**

Du kan skapa flera konfigurationer om det behövs. Konfigurationer kan också kapslas.

>[!NOTE]
>
>Konfigurationsalternativ utöver **Modeller för innehållsfragment** och **GraphQL-beständiga frågor** kan vara nödvändigt beroende på implementeringskraven.

## Nästa steg {#next-steps}

Med den här konfigurationen kan du nu gå vidare till den andra delen av guiden Komma igång och [skapa modeller för innehållsfragment.](create-content-model.md)

>[!TIP]
>
>Fullständig information om Configuration Browser finns här: [finns i dokumentationen för Configuration Browser.](/help/implementing/developing/introduction/configurations.md)
