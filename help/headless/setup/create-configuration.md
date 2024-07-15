---
title: Skapa en konfiguration - Headless-installation
description: Skapa en konfiguration som ett första steg i arbetet med headless i AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Skapa en konfiguration - Headless-installation {#creating-configuration}

Som ett första steg mot headless i AEM as a Cloud Service måste du skapa en konfiguration.

## Vad är en konfiguration? {#what-is-a-configuration}

I Configuration Browser finns ett allmänt konfigurations-API, innehållsstruktur och lösningsmekanism för konfigurationer i AEM.

När det gäller headless content management i AEM kan du tänka på en konfiguration som en arbetsplats i AEM där du kan skapa dina innehållsmodeller, som definierar strukturen för ditt framtida innehåll och innehållsfragment. Du kan ha flera konfigurationer för att separera dessa modeller.

Om du är bekant med [sidmallar i en AEM-implementering i en hel hög ](/help/sites-cloud/authoring/sites-console/templates.md) är användningen av konfigurationer för hantering av innehållsmodeller likartad.

## Så här skapar du en konfiguration {#how-to-create-a-configuration}

En administratör behöver bara skapa en konfiguration en gång, eller mycket sällan, när det krävs en ny arbetsyta för att kunna ordna dina innehållsmodeller. I den här guiden behöver vi bara skapa en konfiguration.

1. Logga in på AEM as a Cloud Service och välj **Verktyg > Allmänt > Konfigurationsläsaren** på huvudmenyn.
1. Ange en **titel** och ett **namn** för din konfiguration.
   * **Rubriken** ska vara beskrivande.
   * **Namn** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md).
      * Den kan vid behov justeras.
1. Markera följande alternativ:
   * **Modeller för innehållsfragment**
   * **GraphQL beständiga frågor**

   ![Skapa konfiguration](../assets/create-configuration.png)

1. Välj **Skapa**

Du kan skapa flera konfigurationer om det behövs. Konfigurationer kan också kapslas.

>[!NOTE]
>
>Konfigurationsalternativ utöver **modeller för innehållsfragment** och **GraphQL beständiga frågor** kan vara nödvändiga beroende på implementeringskraven.

## Nästa steg {#next-steps}

Med den här konfigurationen kan du nu gå vidare till den andra delen av guiden Komma igång och [skapa modeller för innehållsfragment.](create-content-model.md)

>[!TIP]
>
>Fullständig information om Configuration Browser finns i [dokumentationen för Configuration Browser](/help/implementing/developing/introduction/configurations.md).
