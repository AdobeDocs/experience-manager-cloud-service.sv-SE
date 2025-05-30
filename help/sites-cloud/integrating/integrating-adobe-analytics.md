---
title: Integrera med Adobe Analytics
description: Lär dig hur du integrerar Adobe Analytics med AEM as a Cloud Service med Touch-gränssnittet och Adobe Launch.
feature: Integration
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
solution: Experience Manager Sites
source-git-commit: 1289da67452be7fc0fa7f3126d2a3dbf051aa9b5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

Genom att integrera Adobe Analytics och AEM as a Cloud Service kan du spåra webbsidesaktiviteten. Integreringen kräver:

* med Touch-gränssnittet för att skapa en Analytics-konfiguration i AEM as a Cloud Service. IMS-autentisering krävs för att integrera Adobe Analytics med AEM as a Cloud Service.
* lägger till och konfigurerar Adobe Analytics som ett tillägg i [Adobe Launch](#analytics-launch). Om du vill ha mer information om Adobe Launch kan du börja med [snabbstartsguiden](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=sv-SE).

Jämfört med tidigare versioner av AEM finns ramverksstöd inte i Analytics Configuration i AEM as a Cloud Service. I stället görs det nu via Adobe Launch, som är det defacto-verktyg för att skapa en AEM webbplats med analysfunktioner (JS-bibliotek). I Adobe Launch skapas en egenskap där Adobe Analytics-tillägget kan konfigureras och regler skapas för att skicka data till Adobe Analytics. Adobe Launch har ersatt uppgiften med analys från sitecatalyst.

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service-kunder som inte har något befintligt Analytics-konto kan begära åtkomst till Analytics Foundation Pack för Experience Cloud. Detta Foundation Pack ger volymbegränsad användning av Analytics.

## Skapa Adobe Analytics-konfigurationen {#analytics-configuration}

1. Navigera till **Verktyg** → **Cloud Service**.
2. Välj **Adobe Analytics**.
   ![Adobe Analytics Window](assets/analytics_screen2.png "Adobe Analytics Window")
3. Klicka på knappen **Skapa**.
4. Fyll i informationen (se nedan) och klicka på **Anslut**.

### Konfigurationsparametrar {#configuration-parameters}

Fälten i konfigurationsfönstret är följande:

![Konfigurationsparametrar](assets/properties_field2.png "Konfigurationsparametrar")

| Egenskap | Beskrivning |
|---|---|
| Titel | Konfigurationsnamnet |
| IMS-konfiguration | Välj IMS-konfigurationen (se kapitlet nedan) |
| Segment | Möjlighet att använda ett analyssegment som definieras i den aktuella rapporteringssviten. Analysrapporterna filtreras baserat på segmentet. Mer information finns i [Om segment](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=sv-SE). |
| Rapportsviter | En databas där du skickar data och hämtar rapporter. En rapportsvit definierar den fullständiga, oberoende rapporteringen på en vald webbplats, en uppsättning webbplatser eller en delmängd av webbplatssidor. Du kan visa rapporter som hämtats från en enda rapportserie och kan redigera det här fältet i en konfiguration när som helst enligt dina önskemål. |

### Adobe Analytics med IMS-autentisering {#configuration-parameters-ims}

Integrationen av Adobe Experience Manager as a Cloud Service (AEMaaCS) med Adobe Analytics via API:t för Analytics Standard kräver att du konfigurerar Adobe IMS (Identity Management System).

Mer information om hur du skapar IMS-konfigurationen finns i [Konfigurera IMS-integreringar för AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md).

>[!NOTE]
>
>[IMS-integreringar har nu konfigurerats med S2S OAuth](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md).
>
>Tidigare konfigurationer gjordes med [JWT-autentiseringsuppgifter som nu är borttagna i Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md).

### Lägga till en konfiguration till en plats {#add-configuration}

Om du vill använda en Touch UI-konfiguration för en plats går du till **Webbplatser** → **Välj en webbplatssida** → **Egenskaper** → **Avancerat** → **Konfiguration** → Välj konfigurationtenanten.

## Integrera Adobe Analytics på AEM sajter med Adobe Launch {#analytics-launch}

Adobe Analytics kan läggas till som ett tillägg i startegenskapen. Regler kan definieras för mappning och postanrop till Adobe Analytics:

* Titta på [den här videon](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html?lang=sv-SE) om du vill lära dig hur du konfigurerar Analytics-tillägget i Launch för en grundläggande webbplats.

* Mer information om hur du skapar regler och skickar data till Adobe Analytics finns i [Lägg till Adobe Analytics](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=sv-SE).

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch är förkonfigurerad i AEM as a Cloud Service. Du behöver inte skapa den här konfigurationen.

>[!NOTE]
>
>Befintliga (äldre) ramverk fungerar fortfarande, men de kan inte konfigureras i Touch-gränssnittet. Du bör återskapa variabelmappningskonfigurationerna i Launch.
