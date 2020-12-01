---
title: Skapa en guide till Headless-konfiguration
description: Som ett första steg till att komma igång med headless AEM som Cloud Service måste du skapa en konfiguration.
translation-type: tm+mt
source-git-commit: 7ed96dc0da879800d731983a0399b4f4fb3d7d41
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Skapa en snabbstartsguide för Headless Configuration{#creating-configuration}

Som ett första steg till att komma igång med headless AEM som Cloud Service måste du skapa en konfiguration.

## Vad är en konfiguration? {#what-is-a-configuration}

I Configuration Browser finns ett allmänt konfigurations-API, innehållsstruktur och lösningsmekanism för konfigurationer i AEM.

När det gäller headless content management i AEM kan du tänka på en konfiguration som en arbetsplats i AEM där du kan skapa dina innehållsmodeller, som definierar strukturen för ditt framtida innehåll och innehållsfragment. Du kan ha flera konfigurationer för att separera dessa modeller.

Om du är bekant med [sidmallar i en implementering av en fullhög AEM](/help/sites-cloud/authoring/features/templates.md) är användningen av konfigurationer för hantering av innehållsmodeller likartad.

## Så här skapar du en konfiguration {#how-to-create-a-configuration}

En administratör behöver bara skapa en konfiguration en gång, eller mycket sällan, när det krävs en ny arbetsyta för att kunna ordna dina innehållsmodeller. I den här guiden behöver vi bara skapa en konfiguration.

1. Logga in AEM som Cloud Service och välj **Verktyg -> Allmänt -> Konfigurationsläsaren** på huvudmenyn.
1. Ange en **titel** och ett **namn** för din konfiguration.
   * **Titeln** ska vara beskrivande.
   * **Namnet** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/implementing/developing/introduction/naming-conventions.md)
      * Den kan vid behov justeras.
1. Markera följande alternativ:
   * **Modeller för innehållsfragment**
   * **Beständiga GraphQL-frågor**

   ![Skapa konfiguration](../assets/create-configuration.png)

1. Tryck eller klicka på **Skapa**

Du kan skapa flera konfigurationer om det behövs. Konfigurationer kan också kapslas.

>!![NOTE]
Konfigurationsalternativ utöver **Content Fragment Models** och **GraphQL Persistent Queries** kan behövas beroende på implementeringskraven.

## Nästa steg {#next-steps}

Med den här konfigurationen kan du nu gå vidare till den andra delen av guiden Komma igång och [skapa modeller för innehållsfragment.](create-content-model.md)

>!![TIP]
Fullständig information om Configuration Browser finns i [dokumentationen till Configuration Browser.](/help/implementing/developing/introduction/configurations.md)
