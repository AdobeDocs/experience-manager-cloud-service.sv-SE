---
title: Ansluta till Microsoft Translator
description: Lär dig hur du kan koppla AEM till Microsoft Translator körklart för att automatisera ditt arbetsflöde för översättning.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
solution: Experience Manager Sites
source-git-commit: 2314ad30ea31b49d832ce0fdf729420e0ee70e0c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Ansluta till Microsoft Translator {#connecting-to-microsoft-translator}

AEM tillhandahåller en inbyggd koppling för [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/) för översättning av sidinnehåll eller resurser. När du har fått en licens från Microsoft att använda Microsoft Translator konfigurerar du anslutningsprogrammet enligt instruktionerna på den här sidan.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md), som är en guidad väg genom att översätta ditt AEM Sites-innehåll med hjälp av AEM kraftfulla översättningsverktyg, som är idealisk för dem som saknar AEM eller översättningsupplevelse.

| Egenskap | Beskrivning |
|---|---|
| Översättningsetikett | Översättningstjänstens visningsnamn |
| Översättningsattribut | (Valfritt) För användargenererat innehåll visas attribueringen bredvid översatt text, till exempel `Translations by Microsoft` |
| WORKSPACE ID | (Valfritt) ID:t för den anpassade Microsoft Translator-motorn som ska användas |
| Prenumerationsnyckel | Din Microsoft-prenumerationsnyckel för Microsoft Translator |

Följande procedur skapar en Microsoft Translator-konfiguration.

1. I [navigeringspanelen](/help/sites-cloud/authoring/basic-handling.md#first-steps) väljer du **Verktyg** > **Cloud Service** > **ÖversättningsCloud Service**.
1. Navigera till den plats där du vill skapa konfigurationen. Normalt finns det i platsroten eller så kan det vara en global standardkonfiguration.
1. Klicka på knappen **Skapa**.
1. Definiera konfigurationen.
   1. Välj **Microsoft Translator** i listrutan.
   1. Ange en rubrik för konfigurationen. Titeln identifierar konfigurationen i konsolen Cloud Service och i listrutor för sidegenskaper.
   1. Du kan också ange ett namn som ska användas för databasnoden som lagrar konfigurationen.

   ![Skapa översättningskonfiguration](../assets/create-translation-config.png)

1. Klicka på **Skapa**.
1. I fönstret **Redigera konfiguration** anger du värdena för översättningstjänsten som beskrivs i föregående tabell.

   ![Redigera översättningskonfiguration](../assets/msft-config-ui.png)

1. Välj **Anslut** för att verifiera anslutningen.
1. Välj **Spara och stäng**.

## Publicera översättartjänstkonfigurationer {#publishing-the-translator-service-configurations}

Som ett sista steg publicerar du dina Microsoft Translator-konfigurationer med stöd för publicerat översatt innehåll med åtgärden [publicera ett träd](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-and-unpublishing-a-tree).
