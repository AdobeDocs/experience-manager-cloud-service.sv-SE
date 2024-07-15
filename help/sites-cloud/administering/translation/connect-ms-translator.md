---
title: Ansluta till Microsoft Translator
description: Lär dig hur du kan koppla AEM till Microsoft Translator körklart för att automatisera ditt arbetsflöde för översättning.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Ansluta till Microsoft Translator {#connecting-to-microsoft-translator}

Skapa en konfiguration för molntjänsten [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/) om du vill använda ditt Microsoft Translation-konto för översättning AEM sidinnehåll eller resurser.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md), som är en guidad väg genom att översätta ditt AEM Sites-innehåll med hjälp av AEM kraftfulla översättningsverktyg, som är idealisk för dem som saknar AEM eller översättningsupplevelse.

>[!NOTE]
>
>AEM har ett provkonto för Microsoft Translation som tillåter högst 2 000 000 kostnadsfria översatta tecken per månad. Mer information om hur du får en kontoprenumeration som är lämplig för produktionssystem finns i [Uppgradera provlicenskonfigurationen för Microsoft Translator](#upgrading-the-microsoft-translator-trial-license-configuration).

| Egenskap | Beskrivning |
|---|---|
| Översättningsetikett | Översättningstjänstens visningsnamn |
| Översättningsattribut | (Valfritt) För användargenererat innehåll visas attribueringen bredvid översatt text, till exempel `Translations by Microsoft` |
| WORKSPACE ID | (Valfritt) ID:t för den anpassade Microsoft Translator-motorn som ska användas |
| Prenumerationsnyckel | Din Microsoft-prenumerationsnyckel för Microsoft Translator |

När du har skapat konfigurationen måste du [aktivera den](#activating-the-translator-service-configurations).

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

   ![Redigera översättningskonfiguration](../assets/edit-translation-config.png)

1. Välj **Anslut** för att verifiera anslutningen.
1. Välj **Spara och stäng**.

## Uppgraderar Microsoft Translator Trial License Configuration {#upgrading-the-microsoft-translator-trial-license-configuration}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsoft webbplats där man kan få en kontoprenumeration som passar för produktionssystem.

1. I [navigeringspanelen](/help/sites-cloud/authoring/basic-handling.md#first-steps) väljer du **Verktyg** > **Cloud Service** > **ÖversättningsCloud Service**.
1. Välj en befintlig Microsoft Translator-konfiguration.
1. Välj **Redigera**.
1. I fönstret **Redigera konfiguration** väljer du **Uppgradera prenumeration**. En Microsoft-webbsida med mer information om tjänsten öppnas.

## Anpassa Microsoft Translator Engine {#customizing-your-microsoft-translator-engine}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsoft webbplats där du kan anpassa Microsoft Translator-motorn.

1. I [navigeringspanelen](/help/sites-cloud/authoring/basic-handling.md#first-steps) väljer du **Verktyg** > **Cloud Service** > **ÖversättningsCloud Service**.
1. Välj en befintlig Microsoft Translator-konfiguration.
1. Välj **Redigera**.
1. I fönstret **Redigera konfiguration** väljer du **Anpassa översättare**. Använd Microsoft webbsida som öppnas för att anpassa tjänsten.

## Aktivera tjänstkonfigurationer för översättare {#activating-the-translator-service-configurations}

Du måste aktivera dina molntjänstkonfigurationer för att stödja översatt innehåll som replikeras till publiceringsinstansen. Använd metoden för att [publicera ett träd](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-and-unpublishing-a-tree) för att aktivera databasnoderna som lagrar Microsoft Translator-konfigurationerna. Noderna finns under följande överordnade noder:

* `/libs/settings/cloudconfigs/translation/msft-translation`
