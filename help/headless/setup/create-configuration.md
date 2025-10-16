---
title: Skapa en konfiguration - Headless Setup
description: Skapa en konfiguration som ett första steg i arbetet med headless i AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Skapa en konfiguration - Headless Setup {#create-configuration}

Som ett första steg mot headless i AEM as a Cloud Service måste du skapa en konfiguration.

## Vad är en konfiguration? {#what-is-a-configuration}

I Configuration Browser finns ett allmänt konfigurations-API, innehållsstruktur och lösningsmekanism för konfigurationer i AEM.

När det gäller headless content management i AEM kan du tänka dig en konfiguration som en arbetsplats i AEM där du kan skapa dina innehållsmodeller, som definierar strukturen för ditt framtida innehåll och dina framtida innehållsfragment. Du kan ha flera konfigurationer för att separera dessa modeller.

Om du är bekant med [sidmallar i en AEM-implementering i full hög](/help/sites-cloud/authoring/page-editor/templates.md), är användningen av konfigurationer för hantering av innehållsmodeller likartad.

## Så här skapar du en konfiguration {#how-to-create-a-configuration}

En administratör behöver bara skapa en konfiguration en gång, eller mycket sällan, när det krävs en ny arbetsyta för att kunna ordna dina innehållsmodeller. I den här guiden behöver vi bara skapa en konfiguration.

Stegvisa detaljer finns i [Aktivera funktioner för innehållsfragment i konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).

>[!NOTE]
>
>Konfigurationsalternativ utöver **modeller för innehållsfragment** och **GraphQL beständiga frågor** kan vara nödvändiga beroende på implementeringskraven.

## Nästa steg {#next-steps}

Med den här konfigurationen kan du nu gå vidare till den andra delen av guiden Komma igång och [skapa modeller för innehållsfragment](create-content-model.md).

>[!TIP]
>
>Fullständig information om Configuration Browser finns i [dokumentationen för Configuration Browser](/help/implementing/developing/introduction/configurations.md).
