---
title: Integrera med Adobe Analytics
description: 'Integrera med Adobe Analytics '
translation-type: tm+mt
source-git-commit: 96e1d775a98584f12e4571c708955a9ded57e3c4
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 2%

---


# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

Genom att integrera Adobe Analytics och AEM som en Cloud Service kan du spåra webbsidans aktivitet. Integreringen kräver:

* med Touch-gränssnittet för att skapa en Analytics-konfiguration i AEM som en Cloud Service.
* lägga till och konfigurera Adobe Analytics som ett tillägg i [Adobe Launch](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html).

Jämfört med tidigare versioner av AEM finns inte ramverksstöd i Analytics Configuration in AEM som Cloud Service. I stället görs det nu via Adobe Launch, som är det defaceverktyg som används för att skapa en AEM sajt med Analytics-funktioner (JS-bibliotek). I Adobe Launch skapas en egenskap där Adobe Analytics-tillägget kan konfigureras och regler skapas för att skicka data till Adobe Analytics. Adobe Launch har ersatt uppgiften med analys från sitecatalyst.

>[!NOTE]
>
>Adobe Experience Manager som Cloud Service som inte har något Analytics-konto kan begära åtkomst till Analytics Foundation Pack för Experience Cloud. Detta Foundation Pack ger begränsad användning av Analytics i volymprocent.

## Skapa Adobe Analytics-konfigurationen {#analytics-configuration}

1. Navigera till **Verktyg** → **Cloud Service**.
2. Välj **Adobe Analytics**.
   ![Adobe Analytics](assets/analytics_screen2.png "WindowAdobe Analytics Window")
3. Klicka på **Skapa** .
4. Fyll i informationen (se nedan) och klicka på **Anslut**.

### Konfigurationsparametrar {#configuration-parameters}

Konfigurationsfälten som finns i konfigurationsfönstret i Adobe Analytics är:

![Configuration](assets/properties_field1.png "ParametersConfiguration Parameters")

| Egenskap | Beskrivning |
|---|---|
| Företag | Adobe Analytics Login Company |
| Användarnamn | Adobe Analytics API-användare |
| Lösenord | Adobe Analytics-lösenord för autentisering |
| Datacenter | Adobe Analytics datacenter som ditt konto är kopplat till (server, till exempel San Jose, London) |
| Segment | Möjlighet att använda ett Analytics-segment som definieras i den aktuella rapporteringssviten. Analytics-rapporterna filtreras baserat på segmentet. Mer information finns på [den här sidan](https://docs.adobe.com/content/help/en/analytics/components/segmentation/seg-overview.html) . |
| Rapportsviter | En databas där du skickar data och hämtar rapporter. En rapportsvit definierar den fullständiga, oberoende rapporteringen på en vald webbplats, en uppsättning webbplatser eller en delmängd av webbplatssidor. Du kan visa rapporter som hämtats från en enda rapportserie och kan redigera det här fältet i en konfiguration när som helst enligt dina önskemål. |

### Lägga till en konfiguration till en plats {#add-configuration}

Om du vill använda en Touch UI-konfiguration på en webbplats går du till: **Webbplatser** → **Välj en webbsida** → **Egenskaper** → **Avancerad** → **Konfiguration** → Välj konfigurationtenant.

## Integrera Adobe Analytics på AEM sajter med Adobe Launch

Adobe Analytics kan läggas till som ett tillägg i startegenskapen. Regler kan definieras för mappning och postanrop till Adobe Analytics:

* I [den här videon](https://docs.adobe.com/content/help/en/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) får du lära dig hur du konfigurerar Analytics-tillägget i Launch för en grundläggande webbplats.

* På [den här sidan](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) finns mer information om hur du skapar regler och skickar data till Adobe Analytics.

>[!NOTE]
>
>Befintliga (äldre) ramverk fungerar fortfarande, men de kan inte konfigureras i Touch-gränssnittet. Du bör återskapa variabelmappningskonfigurationerna i Launch.

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch är förkonfigurerad i AEM som en Cloud Service. Användare behöver inte skapa den här konfigurationen.
