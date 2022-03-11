---
title: Migreringshandbok till Experience Manager as a Cloud Service for Partners
description: Migreringshandbok till Experience Manager as a Cloud Service for Partners
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 7%

---

# Migreringshandbok för Adobe Experience Manager as a Cloud Service for Partners {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrering till AEM som molntjänst"
>abstract="Här beskrivs det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager as a Cloud Service och hjälpa befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="Vad är nytt och annorlunda?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="Introduktion till AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service erbjuder en omgjord grund för Experience Manager, som bygger på en behållarbaserad infrastruktur, API-driven utveckling och en guidad DevOps-process, vilket gör att marknadsförare och utvecklare alltid kan ligga steget före när det gäller innovationer inom kundupplevelsehantering.

Cloud Service innehåller mängder av användningsklara funktioner och utbyggbarhet i Adobe Experience Manager tack vare den moderna molnbaserade arkitekturen som gör att varumärkena kan möta konsumenternas ständigt växande krav.

Den här enpersonsmodellen visar det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager as a Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Komma igång med Adobe Experience Manager as a Cloud Service {#getting-started}

| Vad är det för skillnad? | Arkitektur - översikt |
|--------------------------|--------------------------|
| <ul><li>[Modern arkitektur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/architecture.html)</li><li>[Automatiska uppdateringar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Asset Microservices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[Binärfiler för direktåtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[Separation av kod och innehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Replikering som en tjänst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[Admin console, Group/User Membership and ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[Introduktion till AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Miljöhög](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/architecture.html)</li><li>[Författarnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Publiceringsnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[Tjänsten Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service – körningsarkitektur](/help/overview/assets/concepts-03.png "AEM as a Cloud Service – körningsarkitektur")

<br>

## Developer Journey i Adobe Experience Manager as a Cloud Service {#developer-journey}

### Utveckling

De grundläggande funktionerna för kodutveckling liknar dem i Adobe Experience Manager as a Cloud Service jämfört med Adobe Experience Manager On Premise och Managed Services.

Utvecklarna skriver kod och testar den lokalt, som sedan skickas till Adobe Experience Manager as a Cloud Service fjärrmiljöer.

Se självhjälpsresurser om implementering för Experience Manager as a Cloud Service om du vill veta hur du kan anpassa Experience Manager as a Cloud Service driftsättning.

| Lokal utveckling | Saker att veta innan du börjar |
|-----------|------------|
| <ol><li>Granska [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing) dokumentation som lär dig mer.</li><li>Titta [Installera Dispatcher SDK](https://video.tv.adobe.com/v/30601) för att förstå hur du installerar Dispatcher SDK</li><li>Titta [Konfigurera Dispatcher SDK](https://video.tv.adobe.com/v/30602) för att förstå hur du konfigurerar Dispatcher SDK</li><li>Granska [Lokal utveckling](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) dokumentation som lär dig mer</li><li>Konfigurera åtkomst till Experience Manager [genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Grundläggande om utveckling](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Utvecklingsriktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[Om projektstrukturen Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Formatsystem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[Övertäckningar](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manager as a Cloud Service API-referens](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Se självstudiekursen om hur du [Utveckla och distribuera WKND på lokal Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### Distribuerar

Utvecklare skriver kod och testar den lokalt, som sedan skickas till AEM as a Cloud Service miljöer.

Cloud Manager, som var ett valfritt verktyg för innehållsleverans för Managed Services, krävs. Detta är nu den enda mekanismen för att distribuera kod till AEM as a Cloud Service miljöer.

Se självhjälpsresurser om hur du konfigurerar och distribuerar till AEM as a Cloud Service miljöer.

1. [Konfigurera CM-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * Produktionspipeline
   * Icke-produktion och endast kodkvalitet, rörledningar
2. [Distribuera kod](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [Förstå testresultaten](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **Åtkomst till loggar**
   * [via CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [via Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Drift och underhåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [Konfigurerar OSGI-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [Säkerhetskopiering och återställning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> Se självstudiekursen om hur du [Distribuera WKND till Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### Hjälp och resurser

1. [Tips och tricks för felsökning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (Endast tillgängligt i lokala SDK- och Experience Manager Cloud Dev-miljöer)
4. [Loggar och loggning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM-loggar](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) (build-unit-testing, code-scanning, build-image, deploy)
   * [Experience Manager Cloud Service Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Lokala SDK-loggar (under värd:port/crx-quickstart/logs)

>[!NOTE]
> Om du behöver mer hjälp kan du:
>1. [Kontakta Experience Manager Support-teamet](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Flyttar till Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Flyttar till Adobe Experience Manager as a Cloud Service"
>abstract="Den här enpersonsmodellen visar det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager as a Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering."

**Experience Manager as a Cloud Service utgör en skalbar, säker och flexibel teknikgrund för Experience Manager Sites och Assets som gör att marknadsförare och IT kan fokusera på att leverera slagkraftiga upplevelser i stor skala.**

Med Experience Manager as a Cloud Service kan era team fokusera på innovationer istället för att planera för produktuppgraderingar. De nya funktionerna testas grundligt och levereras till era team utan avbrott så att de alltid har tillgång till den senaste programvaran.

Övergången till Cloud Service omfattar tre faser – Planering, Körning och Efter publicering.
För en lyckad och smidig övergång bör du säkerställa korrekt planering och följa bästa praxis som beskrivs i den här handboken.

Bilden nedan visar en illustrativ representation av den rekommenderade övergångsprocessen till Cloud Service.

![bild](/help/journey-migration/assets/home-img1.png)

<br>

### Planering

Innan du påbörjar en övergångsresa till Cloud Service bör du bekanta dig med Experience Manager as a Cloud Service och granska de märkbara ändringar som har gjorts i den samt även se vilka funktioner som har ersatts eller ersatts.

<table>
<tr>
<td>Projektidentifiering och utvärdering</td>
<td><ul><li>Se <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Betydande ändringar av Experience Manager as a Cloud Service</a> för att förstå de viktiga skillnaderna mellan Adobe Experience Manager as a Cloud Service och Experience Manager 6.x.</li><li>Se <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">Föråldrade funktioner</a> om du vill veta mer om funktioner som har markerats som föråldrade.</li><li>[Endast för Cloud Service-migreringar] Utvärderar Cloud Servicens beredskap: Kör <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">Best Practices Analyzer (BPA)</a> i källmiljö </li><li>Gör en bedömning mot märkbara förändringar och borttagna funktioner i Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Granska</td>
<td><ul><li>Utför ansträngningsberäkning och resursövningar baserat på upptäckt</li></ul></td>
</tr>
<tr>
<td>Mät</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Upprätta nyckeltal för projekt</a>, resultatkriterier och projekttidslinjer</li></ul></td>
</tr>
</table>

>[!NOTE]
>Rapporten Best Practices Analyzer snabbar upp processen att beräkna den tid och kostnad som krävs för att gå över till AEM as a Cloud Service genom att tillhandahålla information som annars skulle behöva samlas in och utvärderas manuellt.


<br>

### Körning 

Innan du påbörjar körningsfasen av ett projekt bör du vara ombord på Cloud Servicen. Du måste också bekanta dig med Cloud Manager. Detta är den mekanism som används för att distribuera projektkod till en Experience Manager Cloud Service-instans.

Med Cloud Manager kan organisationer självhantera Experience Manager i molnet. Den har en kontinuerlig integrering och kontinuerlig leverans ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview)) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

#### Innehållsmigrering

1. [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) : används för att flytta befintligt innehåll från en AEM (lokal eller AMS) till AEM Cloud Service-målinstansen.
2. [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) : används för att importera och exportera muterbart innehåll i databasen.


#### Baktor/optimera

| Komma igång | Granska och reaktorkod | Dispatcher Review |
|---|---|---|
| <ul><li>[Konfiguration av lokal Dev](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Local Dispatcher Setup](https://video.tv.adobe.com/v/30602/)</li><li>[Kompilera koden med SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Granska AEM Dev Guidelines](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>Bakgrundsuppgifter och tidskrävande jobb</li><li>Sling Scheduler</li><li>Användning av indataström med mera</li></ul></li></ul> | <ul><li>Kör [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) i källmiljön.[**Endast migrering**]<ul><li>Om projektstruktur (baserat på [Cloud Archetype](https://github.com/adobe/aem-project-archetype))<ul><li>Separation av kod och innehåll (mutable vs Immutable)</li><li>[Anpassade indexdefinitioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[Anpassade körningslägen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>Granska och utför nödvändiga ändringar</li><li>[Distribuera](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) på lokal SDK</li><li>Utför röktestning via AEM SDK</li></ul> | <ul><li>Granska [Dispatcher-konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration) för refactoring</li><li>Utnyttja [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher) verktyg där så är lämpligt. [**Endast migrering**]</li><li>Testning kan utföras med [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Resurskunder: Arbetsflöden för granskning och reaktorresurser med [Migrering av molnresurser](https://github.com/adobe/aem-cloud-migration) verktyg


#### Driftsättning/GoLive

1. [Distribuera till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) git
2. Kör kundkod via [Kvalitetspipeline för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)
3. [Distribuera till utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Endast migrering**] Innehållsöverföring med paket eller [Verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Utför rekommenderade testcykler (rök, kvalitetskontroll med mera)
6. Befordra till Cloud Manager Production Pipeline
7. Validering av röktest
8. GoLive

<br>

### Post GoLive

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar. 

>[!TIP]
> Verktyg finns för att felsöka AEM as a Cloud Service miljöer
>1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [Hantera loggar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### Verktyg och resurser

| Bedömning | Refactoring | Modernisering av Experience Manager | Innehållsmigrering |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[Statiska mallar till redigerbara mallar](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[Designkonfigurationer till policyer](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[Foundation-komponenter till Core-komponenter](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[Klassiskt användargränssnitt till pekaktiverat användargränssnitt ](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> Om du behöver mer hjälp kan du:
>1. [Kontakta Experience Manager Support-teamet](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

