---
title: Versionsinformation om Cloud Manager 2023.12.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.12.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b3a338f469ea04d2c31204149d619931a55f2b24
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.12.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.12.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.12.0 i AEM as a Cloud Service är 14 december 2023. Nästa version planeras till den 18 januari 2024.

## Nyheter {#what-is-new}

* [Anpassade behörigheter för Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) gör att du kan skapa anpassade behörighetsprofiler med konfigurerbara behörigheter för att begränsa åtkomst till program, rörledningar och miljöer för användare av Cloud Manager.
   * Den här funktionen kommer att introduceras stegvis och förväntas bli klar i februari 2024 års utgåva av Cloud Manager.
   * Skicka e-post till `Grp-CloudManager-custom-permissions@adobe.com` från den e-postadress som är kopplad till din Adobe ID, om du vill aktiveras tidigare.
* Build containers now support Node.js version 18 for [frontrörledningar.](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
* För nyligen skapade Cloud Manager-program [tillhörande New Relic-underkonto](/help/implementing/cloud-manager/user-access-new-relic.md) är inte aktiverat som standard.
   * För befintliga program där New Relic-underkonto inte har öppnats på mer än 90 dagar inaktiveras det.
   * Om du vill använda New Relic underkonto måste du anmäla dig via Cloud Manager.
* Delversionerna för java 8 och 11 och uppdaterar till maven [lanserades och startades i oktober-versionen av Cloud Manager](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) har slutförts.
   * Stöd för Node 18 lades till för rörledningar i fronthög och fullständig stack.
   * Java 8 minor version har uppdaterats till `jdk1.8.0_371`.
   * Java 11 minor version har uppdaterats till `jdk-11.0.20`.
   * Maven uppdaterades till version 3.8.8
   * Bas-bilden för byggbehållaren uppdaterades till Ubuntu 22.04.

## Tidig användning {#early-adoption}

Om du vill testa några av de kommande funktionerna kan du vara en del av programmet Adobe tidiga införande.

### Klientsamling via Real User Monitoring (RUM) {#rum}

Du kan använda [Real User Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) för att aktivera klientsidessamling för AEM as a Cloud Service.

Real User Monitoring (RUM) Data Service ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det är en utmärkt möjlighet att få avancerade insikter om hur sidan fungerar. Detta är fördelaktigt för kunder som använder antingen CDN som hanteras av Adobe eller CDN som inte hanteras av Adobe. För kunder som använder ett icke-Adobe-hanterat CDN kan automatiserad trafikrapportering nu aktiveras för dem, vilket eliminerar behovet av att dela trafikrapporter med Adobe.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-rum-adopter@adobe.com` från den e-postadress som är kopplad till din Adobe ID. Ange domännamnet för produktions-, scen- och utvecklingsmiljöer i ditt e-postmeddelande.  Tillgången till programmet för tidig användning av den här funktionen är begränsad.

### Hämta din egen GitHub {#byo-github}

Om du använder GitHub för att hantera dina databaser, [du kan nu validera kod direkt i dina GitHub-databaser via Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Integreringen eliminerar behovet av att konsekvent synkronisera kod med Adobe-databasen och gör att du kan verifiera pull-begäranden innan du sammanfogar dem i huvudgrenarna.

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
