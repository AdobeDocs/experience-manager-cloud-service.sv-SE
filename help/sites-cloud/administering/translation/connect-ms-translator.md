---
title: Ansluta till Microsoft Translator
description: Lär dig hur du kan koppla AEM till Microsoft Translator körklart för att automatisera ditt arbetsflöde för översättning.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Ansluta till Microsoft Translator {#connecting-to-microsoft-translator}

Skapa en konfiguration för [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/) molntjänst för att använda ditt Microsoft Translation-konto för översättning AEM sidinnehåll eller resurser.

>[!TIP]
>
>Om du är nybörjare på att översätta innehåll kan du läsa [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

>[!NOTE]
>
>AEM har ett provkonto för Microsoft Translation som tillåter högst 2 000 000 kostnadsfria översatta tecken per månad. Information om hur du får en kontoprenumeration som är lämplig för produktionssystem finns i [Uppgraderar Microsoft Translator Trial License Configuration](#upgrading-the-microsoft-translator-trial-license-configuration).

| Egenskap | Beskrivning |
|---|---|
| Översättningsetikett | Översättningstjänstens visningsnamn |
| Översättningsattribut | (Valfritt) För användargenererat innehåll visas den attribuering som visas bredvid översatt text, till exempel `Translations by Microsoft` |
| ID för arbetsyta | (Valfritt) ID:t för den anpassade Microsoft Translator-motorn som ska användas |
| Prenumerationsnyckel | Din Microsoft-prenumerationsnyckel för Microsoft Translator |

När du har skapat konfigurationen måste du [aktivera den](#activating-the-translator-service-configurations).

Följande procedur skapar en Microsoft Translator-konfiguration.

1. I [navigeringspanelen,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) klicka eller trycka **verktyg** -> **Cloud Services** -> **Cloud Services för översättning**.
1. Navigera till den plats där du vill skapa konfigurationen. Normalt finns det i platsroten eller så kan det vara en global standardkonfiguration.
1. Tryck eller klicka på **Skapa** -knappen.
1. Definiera konfigurationen.
   1. Välj **Microsoft Translator** i listrutan.
   1. Ange en rubrik för konfigurationen. Titeln identifierar konfigurationen i konsolen Cloud Services samt i listrutor för sidegenskaper.
   1. Du kan också ange ett namn som ska användas för databasnoden som lagrar konfigurationen.

   ![Skapa översättningskonfiguration](../assets/create-translation-config.png)

1. Klicka **Skapa**.
1. I **Redigera konfiguration** anger du värdena för översättningstjänsten som beskrivs i föregående tabell.

   ![Redigera översättningskonfiguration](../assets/edit-translation-config.png)

1. Tryck eller klicka **Anslut** för att verifiera anslutningen.
1. Tryck eller klicka **Spara och stäng**.

## Uppgraderar Microsoft Translator Trial License Configuration {#upgrading-the-microsoft-translator-trial-license-configuration}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsoft webbplats där man kan få en kontoprenumeration som passar för produktionssystem.

1. I [navigeringspanelen,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) tryck eller klicka **verktyg** -> **Cloud Services** -> **Cloud Services för översättning**.
1. Tryck eller klicka på den befintliga Microsoft Translator-konfigurationen.
1. Tryck eller klicka **Redigera**.
1. I **Redigera konfiguration** fönster, trycka eller klicka **Uppgradera prenumeration**. En Microsoft-webbsida med mer information om tjänsten öppnas.

## Anpassa Microsoft Translator Engine {#customizing-your-microsoft-translator-engine}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsoft webbplats där du kan anpassa Microsoft Translator-motorn.

1. I [navigeringspanelen,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) tryck eller klicka **verktyg** -> **Cloud Services** -> **Cloud Services för översättning**.
1. Tryck eller klicka på den befintliga Microsoft Translator-konfigurationen.
1. Tryck eller klicka **Redigera**.
1. I **Redigera konfiguration** fönster, trycka eller klicka **Anpassa översättare**. Använd Microsoft webbsida som öppnas för att anpassa tjänsten.

## Aktivera tjänstkonfigurationer för översättare {#activating-the-translator-service-configurations}

Du måste aktivera dina molntjänstkonfigurationer för att stödja översatt innehåll som replikeras till publiceringsinstansen. Använd metoden [publicera ett träd](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) för att aktivera databasnoder som lagrar Microsoft Translator-konfigurationer. Noderna finns under följande överordnade noder:

* `/libs/settings/cloudconfigs/translation/msft-translation`
