---
title: Versionsinformation om Cloud Manager 2024.6.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2024.6.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 958d8fb3526bafeb5a3be9828bddfa3330c05fec
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2024.6.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2024.6.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager version 2024.6.0 i AEM as a Cloud Service är 6 juni 2024. Nästa version planeras till den 11 juli 2024.

## Nyheter {#what-is-new}

* Nu kan du [använda dina egna GitHub-databaser](/help/implementing/cloud-manager/managing-code/private-repositories.md) som källor för både rörledningar med full stapel och frontledning.
   * Dessutom kan du utnyttja GitHub-databaser med [Git-undermoduler,](/help/implementing/cloud-manager/managing-code/git-submodules.md) ger dig bättre kontroll över de automatiskt genererade rörledningarna som används för pull-begärandevalidering och som gör det möjligt att definiera beteenden för viktiga mätvärden under kodsökningsfasen.
   * [Du kan också välja](/help/implementing/cloud-manager/managing-code/github-check-config.md) om du vill bevara rapporthistoriken på GitHub, namnge pipelinen och ange pipelinevariabler som passar dina behov.
* [Självbetjäning för innehållsåterställning](/help/operations/restore.md) har funktioner för återställning av säkerhetskopior i upp till sju dagar:
   * Säkerhetskopiering vid bestämda tidpunkter för de senaste 24 timmarna
   * Återställningar i upp till sju dagar
* [Nya OakPal-regler](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) lades till i Cloud Manager Code Quality scan.
   * Alla nya regler som läggs till från och med juni 2024 är en oföränderlig förändring.
   * Du uppmanas att åtgärda dessa så snart som möjligt eftersom dessa nya regler kommer att få rörledningar att misslyckas från och med Cloud Manager-versionen från augusti 2024.

## Tidig användning {#early-adoption}

Om du vill testa några av de kommande funktionerna kan du vara en del av programmet Adobe tidiga införande.

### Stöd för Edge Delivery Services i Cloud Manager {#edge-delivery-services}

Om du har licensierat Edge Delivery Services som en del av Adobe Experience Manager Sites [du kan nu lägga upp din webbplats med Edge Delivery Services direkt i Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) och publicera med hjälp av en guidad självbetjäningsupplevelse.

Detta ger en enhetlig upplevelse av alla dina AEM egenskaper och säkerställer konsekvens med alla kritiska arbetsflöden, inklusive domännamnshantering, SSL-certifikathantering och CDN-mappningar.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-cmedgedelsvs-program-adopter@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

### DV-certifikat (Domain Validated)

Med Cloud Manager kan du nu [självbetjäningsgenerering och hantering av DV-SSL-certifikat (Domain Valided).](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Detta ger er den snabbaste, enklaste och mest kostnadseffektiva lösningen för att skapa en säker webbplats för ert onlineföretag.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-aemcs-dv-dert-adopter@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

<!-- RICK: REMOVED THIS SECTION AS PER EMAIL REQUEST TO DL-AEM-DOCS FROM SHWETA DUA, WEDNESDAY, JUNE 12, 2024 ### Client-Side Collection via Real Use Monitoring (RUM) {#rum}

You can leverage the [Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) to enable client-side collection for AEM as a Cloud Service.

Real Use Monitoring (RUM) Data Service offers a more precise reflection of user interactions, ensuring a reliable measure of website engagement. It is a great opportunity to gain advanced insights into your page performance. This is beneficial for customers who use either Adobe-managed CDN or non-Adobe managed CDN. For customers using a non-Adobe managed CDN, automated traffic reporting can now be enabled for them, thus removing the need to share any traffic report with Adobe.

If you are interested in testing this new feature and sharing your feedback, please send an email to `aemcs-rum-adopter@adobe.com` from the email address associated with your Adobe ID. Please include the domain name for production, stage, and dev environments in your email.  Availability of the early adopter program of this feature is limited. -->

### Kontrollpanelen för Experience Audit {#experience-audit-dashboard}

[Kontrollpanelen för Experience Audit i Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) innehåller en trendvy över dina sidresultatspoäng tillsammans med insikter och rekommendationer som hjälper dig att förbättra dem. Experience Audit ingår som ett steg i Cloud Managers produktionsflöde.

Kontrollpanelen använder Google Lightroom, ett automatiserat verktyg med öppen källkod som förbättrar kvaliteten på dina webbprogram. Du kan köra det mot alla webbsidor, offentliga webbplatser eller autentiseringar. Den har granskningar av prestanda, tillgänglighet, progressiva webbprogram, SEO med mera.

Är du intresserad av att testa den nya instrumentpanelen? Skicka ett e-postmeddelande till `aem-lighthouse-pilot@adobe.com` via e-post som är kopplad till din Adobe ID.
