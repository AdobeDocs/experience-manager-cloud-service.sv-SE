---
title: Versionsinformation om Cloud Manager 2024.6.0 i Adobe Experience Manager as a Cloud Service
description: Det här är versionsinformationen för Cloud Manager 2024.6.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 6ca376bda8055d62e35e13053ff21f861c12b292
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2024.6.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

På den här sidan visas versionsinformation för Cloud Manager version 2024.6.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager version 2024.6.0 i AEM as a Cloud Service är 6 juni 2024. Nästa version planeras till den 18 juli 2024.

## Nyheter {#what-is-new}

* Du kan nu [använda dina egna GitHub-databaser](/help/implementing/cloud-manager/managing-code/private-repositories.md) som källor för både fullständigt stackade och frontend-pipelines.
   * Dessutom kan du dra nytta av GitHub-databaser med [git-undermoduler](/help/implementing/cloud-manager/managing-code/git-submodules.md) som ger dig bättre kontroll över de automatiskt genererade pipelines som används för pull-begärandevalidering och som gör att du kan definiera beteenden för viktiga mått under kodsökningsfasen.
   * [Du kan också välja ](/help/implementing/cloud-manager/managing-code/github-check-config.md) om du vill bevara rapporthistoriken på GitHub, namnge pipelinen och ange pipeline-variabler som passar dina behov.
* [Självbetjäning-innehållsåterställning](/help/operations/restore.md) ger säkerhetskopiering i upp till sju dagar och funktioner:
   * Säkerhetskopiering vid bestämda tidpunkter för de senaste 24 timmarna
   * Återställningar i upp till sju dagar
* [Nya OakPal-regler](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) har lagts till i Cloud Manager Code Quality scan.
   * Alla nya regler som läggs till från och med juni 2024 är en oföränderlig förändring.
   * Du uppmanas att åtgärda detta så snart som möjligt eftersom dessa nya regler kommer att få rörledningar att misslyckas från och med Cloud Manager augusti 2024.

## Tidig användning {#early-adoption}

Om du vill testa några av de kommande funktionerna kan du vara en del av programmet Adobe tidiga införande.

### Stöd för Edge Delivery Services i Cloud Manager {#edge-delivery-services}

Om du har licensierat Edge Delivery Services som en del av Adobe Experience Manager Sites kan [du nu publicera din webbplats med Edge Delivery Services direkt i Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) och använda en guidad självbetjäning.

Detta ger en enhetlig upplevelse av alla dina AEM egenskaper och säkerställer konsekvens med alla kritiska arbetsflöden, inklusive domännamnshantering, SSL-certifikathantering och CDN-mappningar.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-cmedgedelsvs-program-adopter@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

### DV-certifikat (Domain Validated)

Nu kan du [skapa och hantera domänvaliderade (DV) SSL-certifikat med hjälp av Cloud Manager.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Detta ger dig den snabbaste, enklaste och mest kostnadseffektiva lösningen för att skapa en säker webbplats för din onlineverksamhet.

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-aemcs-dv-dert-adopter@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

<!-- RICK: REMOVED THIS SECTION AS PER EMAIL REQUEST TO DL-AEM-DOCS FROM SHWETA DUA, WEDNESDAY, JUNE 12, 2024 ### Client-Side Collection via Real Use Monitoring (RUM) {#rum}

You can leverage the [Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) to enable client-side collection for AEM as a Cloud Service.

Real Use Monitoring (RUM) Data Service offers a more precise reflection of user interactions, ensuring a reliable measure of website engagement. It is a great opportunity to gain advanced insights into your page performance. This is beneficial for customers who use either Adobe-managed CDN or non-Adobe managed CDN. For customers using a non-Adobe managed CDN, automated traffic reporting can now be enabled for them, thus removing the need to share any traffic report with Adobe.

If you are interested in testing this new feature and sharing your feedback, please send an email to `aemcs-rum-adopter@adobe.com` from the email address associated with your Adobe ID. Please include the domain name for production, stage, and dev environments in your email.  Availability of the early adopter program of this feature is limited.-->

### Kontrollpanelen för Experience Audit {#experience-audit-dashboard}

[Kontrollpanelen för Cloud Manager Experience Audit](/help/implementing/cloud-manager/experience-audit-dashboard.md) innehåller en trendvy över dina sidresultatspoäng tillsammans med insikter och rekommendationer som hjälper dig att förbättra dem. Experience Audit ingår som ett steg i Cloud Manager produktionsflöde.

Kontrollpanelen använder Google Lightroom, ett automatiserat verktyg med öppen källkod som förbättrar kvaliteten på dina webbprogram. Du kan köra det mot alla webbsidor, offentliga webbplatser eller autentiseringar. Den har granskningar av prestanda, tillgänglighet, progressiva webbprogram, SEO med mera.

Är du intresserad av att testa den nya instrumentpanelen? Om du vill komma igång skickar du ett e-postmeddelande till `aem-lighthouse-pilot@adobe.com` från ditt e-postmeddelande som är kopplat till din Adobe ID.
