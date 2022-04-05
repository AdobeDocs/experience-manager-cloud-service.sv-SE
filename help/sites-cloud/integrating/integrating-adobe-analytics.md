---
title: Integrera med Adobe Analytics
description: 'Integrera med Adobe Analytics '
feature: Administering
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
source-git-commit: acd44bd7ff211466acc425148cab18dc7ae6d44c
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 2%

---

# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

Genom att integrera Adobe Analytics och AEM as a Cloud Service kan du spåra webbsidans aktivitet. Integreringen kräver:

* med Touch-gränssnittet för att skapa en Analytics-konfiguration på AEM as a Cloud Service.
* lägga till och konfigurera Adobe Analytics som ett tillägg i [Adobe Launch](#analytics-launch). Mer information om Adobe Launch finns på [den här sidan](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html).

Jämfört med tidigare versioner av AEM finns ramverksstöd inte i Analytics Configuration i AEM as a Cloud Service. I stället görs det nu via Adobe Launch, som är det defacto-verktyg för att skapa en AEM webbplats med analysfunktioner (JS-bibliotek). I Adobe Launch skapas en egenskap där Adobe Analytics-tillägget kan konfigureras och regler skapas för att skicka data till Adobe Analytics. Adobe Launch har ersatt uppgiften med analys från sitecatalyst.

>[!NOTE]
>Tillagd i prerelease-kanalen är kravet på IMS-autentisering för att integrera Adobe Analytics med AEM as a Cloud Service. Se [Konfigurera Adobe Analytics med IMS-autentisering (prerelease channel)](#configuration-parameters-ims) för mer information. Se betaversionskanalen [dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) om du vill ha information om hur du aktiverar den här inställningen för din miljö.

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service-kunder som inte har något befintligt Analytics-konto kan begära åtkomst till Analytics Foundation Pack för Experience Cloud. Detta Foundation Pack ger volymbegränsad användning av Analytics.

## Skapa Adobe Analytics-konfigurationen {#analytics-configuration}

1. Navigera till **verktyg** → **Cloud Services**.
2. Välj **Adobe Analytics**.
   ![Adobe Analytics Window](assets/analytics_screen2.png "Adobe Analytics Window")
3. Välj **Skapa** -knappen.
4. Fyll i informationen (se nedan) och klicka på **Anslut**.

### Konfigurationsparametrar {#configuration-parameters}

Konfigurationsfälten som finns i konfigurationsfönstret i Adobe Analytics är:

![Konfigurationsparametrar](assets/properties_field1.png "Konfigurationsparametrar")

| Egenskap | Beskrivning |
|---|---|
| Företag | Adobe Analytics Login Company |
| Användarnamn | Adobe Analytics API-användare |
| Lösenord | Adobe Analytics-lösenord för autentisering |
| Datacenter | Adobe Analytics datacenter som ditt konto är kopplat till (server, till exempel San Jose, London) |
| Segment | Möjlighet att använda ett analyssegment som definieras i den aktuella rapporteringssviten. Analysrapporterna filtreras baserat på segmentet. Se [den här sidan](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) om du vill ha mer information. |
| Rapportsviter | En databas där du skickar data och hämtar rapporter. En rapportsvit definierar den fullständiga, oberoende rapporteringen på en vald webbplats, en uppsättning webbplatser eller en delmängd av webbplatssidor. Du kan visa rapporter som hämtats från en enda rapportserie och kan redigera det här fältet i en konfiguration när som helst enligt dina önskemål. |

### Konfigurera Adobe Analytics med IMS-autentisering (prerelease channel) {#configuration-parameters-ims}

Tillagd i prerelease-kanalen är kravet på IMS-autentisering för att integrera Adobe Analytics med AEM as a Cloud Service. Se betaversionskanalen [dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) om du vill ha information om hur du aktiverar den här inställningen för din miljö. Det innebär att det krävs en IMS-konfiguration för både Launch och Analytics för att Analytics ska kunna integreras korrekt med AEM och Launch. IMS-konfigurationen för Launch är förkonfigurerad i AEM as a Cloud Service, men IMS-konfigurationen för Analytics måste skapas.

Se detta [page](/help/sites-cloud/integrating/integration-adobe-analytics-ims.md) om du vill lära dig hur du skapar IMS-konfigurationen för Analytics.

När du utfört stegen i [Skapa Adobe Analytics-konfigurationen](#configuration-parameters) är fälten i konfigurationsfönstret följande:

![Konfigurationsparametrar](assets/properties_field2.png "Konfigurationsparametrar")

| Egenskap | Beskrivning |
|---|---|
| Titel | Konfigurationsnamnet |
| IMS-konfiguration | Välj IMS-konfigurationen (se beskrivningen ovan) |
| Segment | Möjlighet att använda ett analyssegment som definieras i den aktuella rapporteringssviten. Analysrapporterna filtreras baserat på segmentet. Se [den här sidan](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) om du vill ha mer information. |
| Rapportsviter | En databas där du skickar data och hämtar rapporter. En rapportsvit definierar den fullständiga, oberoende rapporteringen på en vald webbplats, en uppsättning webbplatser eller en delmängd av webbplatssidor. Du kan visa rapporter som hämtats från en enda rapportserie och kan redigera det här fältet i en konfiguration när som helst enligt dina önskemål. |

### Lägga till en konfiguration till en plats {#add-configuration}

Om du vill använda en Touch UI-konfiguration på en webbplats går du till: **Webbplatser** → **Välj en webbplatssida** → **Egenskaper** → **Avancerat** → **Konfiguration** → välj konfigurationspersonen.

## Integrera Adobe Analytics på AEM sajter med Adobe Launch {#analytics-launch}

Adobe Analytics kan läggas till som ett tillägg i startegenskapen. Regler kan definieras för mappning och postanrop till Adobe Analytics:

* Titta [den här videon](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) om du vill lära dig hur du konfigurerar Analytics-tillägget i Launch för en grundläggande webbplats.

* Se [den här sidan](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) om du vill ha mer information om hur du skapar regler och skickar data till Adobe Analytics.

>[!NOTE]
>
>Befintliga (äldre) ramverk fungerar fortfarande, men de kan inte konfigureras i Touch-gränssnittet. Du bör återskapa variabelmappningskonfigurationerna i Launch.

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch är förkonfigurerad i AEM as a Cloud Service. Användare behöver inte skapa den här konfigurationen.
