---
title: Migreringshandbok för Experience Manager as a Cloud Service for Partners
description: Migreringshandbok för Experience Manager as a Cloud Service for Partners
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 4%

---

# Migreringshandbok för Adobe Experience Manager as a Cloud Service for Partners {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrering till AEM som molntjänst"
>abstract="Här beskrivs det rekommenderade stegvisa tillvägagångssättet för att gå över från olika Experience Manager-installationer till Experience Manager as a Cloud Service och hjälpa befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=sv-SE" text="Vad är nytt och annorlunda?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=sv-SE" text="Introduktion till AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service har en uppdaterad arkitektur för Experience Manager. Denna grund bygger på en behållarbaserad infrastruktur, API-driven utveckling och guidad DevOps-process. Detta gör att marknadsförare och utvecklare kan ligga steget före när det gäller innovationer inom kundupplevelsehantering.

Cloud Service innehåller mängder av användningsklara funktioner och utbyggbarhet i Adobe Experience Manager tack vare den moderna molnbaserade arkitekturen, som gör att varumärkena kan möta konsumenternas ständigt föränderliga krav.

På den här sidan beskrivs den stegvisa metod som rekommenderas för att övergå från tidigare Experience Manager-distributioner till Experience Manager as a Cloud Service. Den nya, specialbyggda plattformen hjälper er att leverera sammankopplade, kontinuerliga upplevelser.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Se diagrammet nedan för en allmän representation av migreringsresan.

![Allmän representation av migreringsresan](/help/journey-migration/assets/migration-process.png)

## Komma igång med Adobe Experience Manager as a Cloud Service {#getting-started}

| Vad är det för skillnad? | Arkitektur - översikt |
|--------------------------|--------------------------|
| <ul><li>[Modern arkitektur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=sv-SE)</li><li>[Automatiska uppdateringar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=sv-SE)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=sv-SE)</li><li>[Resursmikrotjänster](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=sv-SE)</li><li>[Binärfiler för direktåtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=sv-SE)</li><li>[Separation av kod och innehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=sv-SE)</li><li>[Replikering som en tjänst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=sv-SE)</li><li>[Admin console, Group/User Membership and ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=sv-SE)</li></ul> | <ul><li>[Introduktion till AEM-arkitektur](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=sv-SE#underlying-technology)</li><li>[Miljöhög](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=sv-SE)</li><li>[Författarnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=sv-SE#underlying-technology)</li><li>[Publiceringsnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=sv-SE#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=sv-SE)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=sv-SE) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=sv-SE) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=sv-SE) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=sv-SE)</li><li>[Asset Compute-tjänst](https://experienceleague.adobe.com/docs/asset-compute/using/home.html?lang=sv-SE)</li></ul> |

![AEM as a Cloud Service – körningsarkitektur](/help/overview/assets/concepts-03.png "AEM as a Cloud Service – körningsarkitektur")

<br>

## Developer Journey i Adobe Experience Manager as a Cloud Service {#developer-journey}

### Utvecklar

De grundläggande funktionerna för kodutveckling i Adobe Experience Manager as a Cloud Service liknar dem i Adobe Experience Manager On Premise och Managed Services.

Utvecklare skriver kod och testar den lokalt och skickar den sedan till Adobe Experience Manager as a Cloud Service fjärrmiljöer.

Se självhjälpsresurser om implementering av Experience Manager as a Cloud Service och lär dig hur du anpassar driftsättningen av Experience Manager as a Cloud Service.

| Lokal utveckling | Saker att veta innan du börjar |
|-----------|------------|
| <ol><li>Läs [dokumentationen för Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=sv-SE) om du vill veta mer.</li><li>Titta på [Installera Dispatcher SDK](https://video.tv.adobe.com/v/30601) om du vill veta hur du installerar Dispatcher SDK</li><li>Titta på [Konfigurera Dispatcher SDK](https://video.tv.adobe.com/v/30602) om du vill veta hur du konfigurerar Dispatcher SDK</li><li>Läs dokumentationen för [Local Development Setup](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=sv-SE#local-development-environment-set-up) om du vill veta mer</li><li>Konfigurerar åtkomst till Experience Manager [genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=sv-SE#accessing)</li></ol> | <ol><li>[Grundläggande om utveckling](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=sv-SE)</li><li>[Utvecklingsriktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=sv-SE)</li><li>[Om Experience Manager projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=sv-SE)</li><li>[Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=sv-SE)</li><li>[Digital Foundation-utkast](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Formatsystem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=sv-SE)</li><li>[Övertäckningar](/help/implementing/developing/introduction/overlays.md)</li><li>[API-referens för Experience Manager as a Cloud Service](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Se självstudiekurs om hur du [utvecklar och distribuerar WKND på lokal Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=sv-SE)

### Distribuerar

Utvecklare skriver kod och testar den lokalt och skickar den sedan till AEM as a Cloud Service fjärrmiljöer.

Cloud Manager, som var ett valfritt innehållsleveransverktyg för Managed Services, behövs nu. Det är den enda mekanismen för att distribuera kod till AEM as a Cloud Service-miljöer.

Se självhjälpsresurser om hur du konfigurerar och distribuerar till AEM as a Cloud Service-miljöer.

1. [Konfigurera CM-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=sv-SE)

   * Produktionspipeline
   * Icke-produktion och endast kodkvalitet, rörledningar

1. [Distribuera kod](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE)
1. [Förstå testresultaten](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=sv-SE)
1. **Åtkomst till loggar**

   * [via CM-gränssnitt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=sv-SE)
   * [via Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=sv-SE#debugging)

1. [Drift och underhåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=sv-SE)

   * [Konfigurerar OSGI-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=sv-SE)
   * [Säkerhetskopiering och återställning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=sv-SE)

>[!TIP]
> Se självstudiekurs om hur du [distribuerar WKND till Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=sv-SE)

### Hjälp och resurser

1. [Felsökningstips och tricks](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=sv-SE#debugging-aem-as-a-cloud-service)
1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=sv-SE#debugging)
1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=sv-SE) (endast tillgängligt i lokala SDK- och Experience Manager Cloud Dev-miljöer)
1. [Loggar och loggning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=sv-SE#debugging)

   * [CM-loggar](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=sv-SE#debugging) (build-unit-testing, code-scanning, build-image, deploy)
   * [Experience Manager Cloud Service-loggar](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=sv-SE#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Lokala SDK-loggar (under värd:port/crx-quickstart/logs)

>[!NOTE]
>
> Om du behöver mer hjälp kan du:
>
>1. [Kontakta Experience Manager Support Team](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=sv-SE)
>1. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

<br>

## Flyttar till Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Flyttar till Adobe Experience Manager as a Cloud Service"
>abstract="Den här enpersonsversionen visar det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-installationer till Experience Manager as a Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering."

**Experience Manager as a Cloud Service är en skalbar, säker och flexibel teknikgrund för Experience Manager Sites och Assets som gör att marknadsförare och IT kan fokusera på att leverera slagkraftiga upplevelser i stor skala.**

Med Experience Manager as a Cloud Service kan era team fokusera på innovationer istället för att planera för produktuppgraderingar. De nya funktionerna testas grundligt och levereras till era team utan avbrott så att de alltid har tillgång till den senaste programvaran.

Övergången till Cloud Service omfattar tre faser - Planering, Körning och Post Go-live.
För en lyckad och smidig övergång bör du säkerställa korrekt planering och följa bästa praxis som beskrivs i den här handboken.

I bilden nedan visas en högnivårepresentation av den rekommenderade övergångsresan till Cloud Service.

![Högnivårepresentation av den rekommenderade övergångsresan till Cloud Service](/help/journey-migration/assets/home-img1.png)

<br>

### Planering

Innan du börjar din övergångsresa till Cloud Service bör du:

* bekanta dig med Experience Manager as a Cloud Service
* Granska de ändringar som har gjorts i den
* Granska de funktioner som har ersatts eller tagits bort

<table>
<tr>
<td>Projektidentifiering och utvärdering</td>
<td><ul><li>Se <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=sv-SE">Observera ändringar i Experience Manager as a Cloud Service</a> om du vill veta mer om de viktiga skillnaderna mellan Adobe Experience Manager as a Cloud Service och Experience Manager 6.x.</li><li>Mer information om funktioner som har markerats som inaktuella finns i <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=sv-SE">Inaktuella funktioner</a>.</li><li>[Endast för Cloud Service-migreringar] Utvärderar Cloud Service beredskap: Kör <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=sv-SE">BPA </a> (Best Practices Analyzer)i källmiljön </li><li>Gör en bedömning mot märkbara förändringar och borttagna funktioner i Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Granska</td>
<td><ul><li>Utför ansträngningsberäkning och resursövningar baserat på upptäckt</li></ul></td>
</tr>
<tr>
<td>Mät</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Upprätta KPI:er för projekt</a>, kriterier för lyckade projekt och tidslinjer för projekt</li></ul></td>
</tr>
</table>

>[!NOTE]
>Rapporten Best Practices Analyzer snabbar upp processen att beräkna den tid och kostnad som krävs för övergången till AEM as a Cloud Service genom att tillhandahålla information som annars skulle behöva samlas in och utvärderas manuellt.


<br>

### Körning

Innan du påbörjar körningsfasen av ett projekt bör du vara ombord på Cloud Service. Du måste också bekanta dig med Cloud Manager. Detta är den mekanism som används för att distribuera projektkod till en Experience Manager Cloud Service-instans.

Med Cloud Manager kan organisationer själva hantera Experience Manager i molnet. Det innehåller en kontinuerlig integrering och ett kontinuerligt leveransramverk ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=sv-SE)) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

#### Innehållsmigrering

1. [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=sv-SE#migration) : används för att flytta befintligt innehåll från en AEM-källinstans (lokal eller AMS) till AEM Cloud-måltjänstinstansen.
1. [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=sv-SE#package-manager) : används för import och export av muterbart innehåll i databasen.


#### Baktor/optimera

| Komma igång | Granska och reaktorkod | Dispatcher Review |
|---|---|---|
| <ul><li>[Lokal utvecklarkonfiguration](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=sv-SE#local-development-environment-set-up)</li><li>[Lokala Dispatcher-inställningar](https://video.tv.adobe.com/v/30602/)</li><li>[Kompilera koden med SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=sv-SE)</li><li>[Granska riktlinjerna för AEM Dev](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=sv-SE)<ul><li>Bakgrundsuppgifter och tidskrävande jobb</li><li>Sling Scheduler</li><li>Användning av indataström med mera</li></ul></li></ul> | <ul><li>Kör [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=sv-SE) i källmiljön.[**Endast migrering**]<ul><li>Om projektstrukturering (baserat på [molnarkityp](https://github.com/adobe/aem-project-archetype))<ul><li>Separation av kod och innehåll (mutable vs Immutable)</li><li>[Anpassade indexdefinitioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=sv-SE)</li><li>[Anpassade runmodes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=sv-SE)</li></ul></li></ul></li><li>Granska och utför nödvändiga ändringar</li><li>[Distribuera](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=sv-SE) på lokal SDK</li><li>Utför röktestning via AEM SDK</li></ul> | <ul><li>Granska [Dispatcher-konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=sv-SE) för omfaktorisering</li><li>Använd verktyget [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=sv-SE) där det är lämpligt. [**Endast migrering**]</li><li>Testning kan utföras med [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=sv-SE#prerequisites)</li></ul> |

>[!TIP]
> Assets-kunder: Granska och uppdatera Assets-arbetsflöden med verktyget för [resursmigrering](https://github.com/adobe/aem-cloud-migration)


#### Driftsättning/GoLive

1. [Distribuera till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=sv-SE) Git
2. Kör kundkod via [Cloud Manager kvalitetspipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=sv-SE)
3. [Distribuera till utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=sv-SE#debugging)
4. **Endast migrering** Innehållsöverföring med paket eller [Innehållsöverföringsverktyg](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Utför rekommenderade testcykler (rök, kvalitetskontroll med mera)
6. Uppgradera till Cloud Manager Production Pipeline
7. Validering av röktest
8. GoLive

<br>

### Post GoLive

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar. 

>[!TIP]
>
> Det finns verktyg för att felsöka AEM as a Cloud Service-miljön
>
>1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=sv-SE)
>1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=sv-SE)
>1. [Hantera loggar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=sv-SE)

<br>

### Verktyg och resurser

| Utvärdering | Refactoring | Experience Manager modernisering | Innehållsmigrering |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=sv-SE)</li></li> | <ul><li>[Plugin-programmet för enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=sv-SE)</li></ul> | <ul><li>[Statiska mallar till redigerbara mallar](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Utforma konfigurationer för profiler](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Foundation Components to Core Components](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[Klassiskt användargränssnitt för pekaktiverat användargränssnitt](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=sv-SE)</li><li>[Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=sv-SE#contentmanagement)</li></ul> |

>[!NOTE]
>
> Om du behöver mer hjälp kan du:
>
>1. [Kontakta Experience Manager Support Team](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=sv-SE)
>1. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)
