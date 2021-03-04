---
title: Ansluter till Microsoft Translator
description: Lär dig hur du ansluter AEM till Microsoft Translator körklart för att automatisera ditt arbetsflöde för översättning.
translation-type: tm+mt
source-git-commit: 5902e026c47aac0c1ea62a2b74be6109b216fb74
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Ansluter till Microsoft Translator {#connecting-to-microsoft-translator}

Skapa en konfiguration för molntjänsten [Microsoft Translator](https://hub.microsofttranslator.com) om du vill använda ditt Microsoft Translation-konto för översättning AEM sidinnehåll eller resurser.

>[!NOTE]
>
>AEM har ett Microsoft Translation-konto som du kan använda för högst 2 000 000 kostnadsfria översatta tecken per månad. Mer information om hur du får en kontoprenumeration som är lämplig för produktionssystem finns i [Uppgradera Microsoft Translator Trial License Configuration](#upgrading-the-microsoft-translator-trial-license-configuration).

| Egenskap | Beskrivning |
|---|---|
| Översättningsetikett | Översättningstjänstens visningsnamn |
| Översättningsattribut | (Valfritt) För användargenererat innehåll visas attribueringen bredvid översatt text, till exempel `Translations by Microsoft` |
| ID för arbetsyta | (Valfritt) ID:t för den anpassade Microsoft Translator-motorn som ska användas |
| Prenumerationsnyckel | Din Microsoft-prenumerationsnyckel för Microsoft Translator |

När du har skapat konfigurationen måste du [aktivera den](#activating-the-translator-service-configurations).

Följande procedur skapar en Microsoft Translator-konfiguration.

1. I [navigeringspanelen](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) klickar eller trycker du på **Verktyg** -> **Cloud Services** -> **Cloud Services för översättning**.
1. Navigera till den plats där du vill skapa konfigurationen. Normalt finns det i platsroten eller så kan det vara en global standardkonfiguration.
1. Tryck eller klicka på knappen **Skapa**.
1. Definiera konfigurationen.
   1. Välj **Microsoft Translator** i listrutan.
   1. Ange en rubrik för konfigurationen. Titeln identifierar konfigurationen i konsolen Cloud Services samt i listrutor för sidegenskaper.
   1. Du kan också ange ett namn som ska användas för databasnoden som lagrar konfigurationen.

   ![Skapa översättningskonfiguration](../assets/create-translation-config.png)

1. Klicka på **Skapa**.
1. I fönstret **Redigera konfiguration** anger du värdena för översättningstjänsten som beskrivs i föregående tabell.

   ![Redigera översättningskonfiguration](../assets/edit-translation-config.png)

1. Tryck eller klicka på **Anslut** för att verifiera anslutningen.
1. Tryck eller klicka på **Spara och stäng**.

## Uppgraderar Microsoft Translator Trial License Configuration {#upgrading-the-microsoft-translator-trial-license-configuration}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsofts webbplats för att få en kontoprenumeration som passar för produktionssystem.

1. Tryck eller klicka på **Verktyg** -> **Cloud Services** -> **Cloud Services** på [navigeringspanelen.](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)
1. Tryck eller klicka på din befintliga Microsoft Translator-konfiguration.
1. Tryck eller klicka på **Redigera**.
1. I fönstret **Redigera konfiguration** trycker eller klickar du på **Uppgradera prenumeration**. En Microsoft-webbsida med mer information om tjänsten öppnas.

## Anpassa Microsoft Translator Engine {#customizing-your-microsoft-translator-engine}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsofts webbplats där du kan anpassa Microsoft Translator-motorn.

1. Tryck eller klicka på **Verktyg** -> **Cloud Services** -> **Cloud Services** på [navigeringspanelen.](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)
1. Tryck eller klicka på din befintliga Microsoft Translator-konfiguration.
1. Tryck eller klicka på **Redigera**.
1. I fönstret **Redigera konfiguration** trycker eller klickar du på **Anpassa översättare**. Använd Microsofts webbsida som öppnas för att anpassa tjänsten.

## Aktivera översättartjänstens konfigurationer {#activating-the-translator-service-configurations}

Du måste aktivera dina molntjänstkonfigurationer för att stödja översatt innehåll som replikeras till publiceringsinstansen. Använd metoden [publicera ett träd](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) för att aktivera databasnoderna som lagrar Microsoft Translator-konfigurationerna. Noderna finns under följande överordnade noder:

* `/libs/settings/cloudconfigs/translation/msft-translation`
