---
title: Versionsinformation om Cloud Manager 2024.3.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2024.3.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4bae300f653ae6b84cf798f4fe9e8c9326963718
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2024.3.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2024.3.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2024.3.0 i AEM as a Cloud Service är 14 mars 2024. Nästa version är planerad till den 11 april 2024.

## Nyheter {#what-is-new}

* [Nu kan du skapa avancerad nätverksinfrastruktur](/help/security/configuring-advanced-networking.md) i ditt Cloud Manager-program och konfigurera dina miljöer på ett självbetjäningssätt med hjälp av användargränssnittet i Cloud Manager.
* [Information om stegen för pipeline-körning](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) innehåller det aktuella distributionssteget och vad som förväntas komma efter det.

## Tidig användning {#early-adoption}

Om du vill testa några av de kommande funktionerna kan du vara en del av programmet Adobe tidiga införande.

### Klientsamling via Real User Monitoring (RUM) {#rum}

Du kan använda [Real User Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) för att aktivera klientsidessamling för AEM as a Cloud Service.

Real User Monitoring (RUM) Data Service ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det är en utmärkt möjlighet att få avancerade insikter om hur sidan fungerar. Detta är fördelaktigt för kunder som använder antingen CDN som hanteras av Adobe eller CDN som inte hanteras av Adobe. För kunder som använder ett icke-Adobe-hanterat CDN kan automatiserad trafikrapportering nu aktiveras för dem, vilket eliminerar behovet av att dela trafikrapporter med Adobe.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-rum-adopter@adobe.com` från den e-postadress som är kopplad till din Adobe ID. Ange domännamnet för produktions-, scen- och utvecklingsmiljöer i ditt e-postmeddelande.  Tillgången till programmet för tidig användning av den här funktionen är begränsad.

### Hämta din egen GitHub {#byo-github}

Om du använder GitHub för att hantera dina databaser, [du kan nu validera kod direkt i dina GitHub-databaser via Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Integreringen eliminerar behovet av att konsekvent synkronisera kod med Adobe-databasen och gör att du kan verifiera pull-begäranden innan du sammanfogar dem i huvudgrenarna. Den här funktionen är exklusiv för public GitHub. Det finns inget stöd för GitHub som är självvärd.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-CloudManager_BYOG@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

### Självbetjäning för återställning av innehåll {#content-restore}

[En ny självbetjäningsfunktion för innehållsåterställning](/help/operations/restore.md) erbjuder nu säkerhetskopiering för återställning i upp till sju dagar och är tillgänglig för tidiga användare i utvärderingssyfte som omfattar:

* Säkerhetskopiering vid bestämda tidpunkter för de senaste 24 timmarna
* Återställningar i upp till sju dagar

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-restorefrombackup-adopter@adobe.com` via e-post som är kopplad till din Adobe ID.

* Det tidiga adopterprogrammet är begränsat till utvecklingsmiljöer.
* Tillgången till programmet för tidig användning av den här funktionen är begränsad.
* Den här funktionen används för att återställa innehåll som har tagits bort av misstag och är inte avsedd för katastrofåterställning.

### Kontrollpanelen för Experience Audit {#experience-audit-dashboard}

[Kontrollpanelen för Experience Audit i Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) innehåller en trendvy över dina sidresultatspoäng tillsammans med insikter och rekommendationer som hjälper dig att förbättra dem. Experience Audit ingår som ett steg i Cloud Managers produktionsflöde.

Kontrollpanelen använder Google Lightroom, ett automatiserat verktyg med öppen källkod som förbättrar kvaliteten på dina webbprogram. Du kan köra det mot alla webbsidor, offentliga webbplatser eller autentiseringar. Den har granskningar av prestanda, tillgänglighet, progressiva webbprogram, SEO med mera.

Är du intresserad av att testa den nya instrumentpanelen? Skicka ett e-postmeddelande till `aem-lighthouse-pilot@adobe.com` via e-post som är kopplad till din Adobe ID.

## Felkorrigeringar {#bug-fixes}

* Ett fel har korrigerats när en användare definierar `COMMERCE_ENDPOINT` variabel med ett avslutande blanksteg, kommer dispatchern inte att läsas in.
