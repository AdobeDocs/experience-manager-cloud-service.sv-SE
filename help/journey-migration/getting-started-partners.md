---
title: Migreringshandbok till Experience Manager as a Cloud Service for Partners
description: Migreringshandbok till Experience Manager as a Cloud Service for Partners
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 4%

---

# Migreringshandbok för Adobe Experience Manager as a Cloud Service for Partners {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrering till AEM som molntjänst"
>abstract="Här beskrivs det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager as a Cloud Service och hjälpa befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html" text="Vad är nytt och annorlunda?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html" text="Introduktion till AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service erbjuder en omgjord grund för Experience Manager, som bygger på en behållarbaserad infrastruktur, API-driven utveckling och en guidad DevOps-process, vilket gör att marknadsförare och utvecklare alltid kan ligga steget före när det gäller innovationer inom kundupplevelsehantering.

Cloud Service innehåller mängder av användningsklara funktioner och utbyggbarhet i Adobe Experience Manager tack vare den moderna molnbaserade arkitekturen som gör att varumärkena kan möta konsumenternas ständigt växande krav.

Den här enpersonsmodellen visar det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager as a Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Se diagrammet nedan för en allmän representation av migreringsresan.

![bild](/help/journey-migration/assets/migration-process.png)

## Komma igång med Adobe Experience Manager as a Cloud Service {#getting-started}

| Vad är det för skillnad? | Arkitektur - översikt |
|--------------------------|--------------------------|
| <ul><li>[Modern arkitektur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Automatiska uppdateringar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[Asset Microservices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Binärfiler för direktåtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Separation av kod och innehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)</li><li>[Replikering som en tjänst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html)</li><li>[Admin console, Group/User Membership and ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[Introduktion till AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html#underlying-technology)</li><li>[Miljöhög](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Författarnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html#underlying-technology)</li><li>[Publiceringsnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[Tjänsten Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service – körningsarkitektur](/help/overview/assets/concepts-03.png "AEM as a Cloud Service – körningsarkitektur")

<br>

## Developer Journey i Adobe Experience Manager as a Cloud Service {#developer-journey}

### Utvecklar

De grundläggande funktionerna för kodutveckling liknar dem i Adobe Experience Manager as a Cloud Service jämfört med Adobe Experience Manager On Premise och Managed Services.

Utvecklarna skriver kod och testar den lokalt, som sedan skickas till Adobe Experience Manager as a Cloud Service fjärrmiljöer.

Se självhjälpsresurser om implementering för Experience Manager as a Cloud Service om du vill veta hur du kan anpassa Experience Manager as a Cloud Service driftsättning.

| Lokal utveckling | Saker att veta innan du börjar |
|-----------|------------|
| <ol><li>Granska [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html) dokumentation som lär dig mer.</li><li>Titta [Installera Dispatcher SDK](https://video.tv.adobe.com/v/30601) för att förstå hur Dispatcher SDK installeras</li><li>Titta [Konfigurera Dispatcher SDK](https://video.tv.adobe.com/v/30602) för att förstå hur du konfigurerar Dispatcher SDK</li><li>Granska [Lokal utveckling](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html#local-development-environment-set-up) dokumentation som lär dig mer</li><li>Konfigurera åtkomst till Experience Manager [genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html#accessing)</li></ol> | <ol><li>[Grundläggande om utveckling](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)</li><li>[Utvecklingsriktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)</li><li>[Om projektstrukturen Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)</li><li>[Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Formatsystem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html)</li><li>[Övertäckningar](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manager as a Cloud Service API-referens](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Se självstudiekursen om hur du [Utveckla och distribuera WKND på lokal Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### Distribuerar

Utvecklare skriver kod och testar den lokalt, som sedan skickas till AEM as a Cloud Service miljöer.

Cloud Manager, som var ett valfritt verktyg för innehållsleverans för Managed Services, krävs. Detta är nu den enda mekanismen för att distribuera kod till AEM as a Cloud Service miljöer.

Se självhjälpsresurser om hur du konfigurerar och distribuerar till AEM as a Cloud Service miljöer.

1. [Konfigurera CM-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html)
   * Produktionspipeline
   * Icke-produktion och endast kodkvalitet, rörledningar
2. [Distribuera kod](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)
3. [Förstå testresultaten](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html)
4. **Åtkomst till loggar**
   * [via CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html)
   * [via Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html#debugging)
5. [Drift och underhåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html)
   * [Konfigurerar OSGI-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html)
   * [Säkerhetskopiering och återställning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html)

>[!TIP]
> Se självstudiekursen om hur du [Distribuera WKND till Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### Hjälp och resurser

1. [Tips och tricks för felsökning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html#debugging-aem-as-a-cloud-service)
2. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) (Endast tillgängligt i lokala SDK- och Experience Manager Cloud Dev-miljöer)
4. [Loggar och loggning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html#debugging)
   * [CM-loggar](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html#debugging) (build-unit-testing, code-scanning, build-image, deploy)
   * [Experience Manager Cloud Service Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Lokala SDK-loggar (under värd:port/crx-quickstart/logs)

>[!NOTE]
> Om du behöver mer hjälp kan du:
>1. [Kontakta Experience Manager Support-teamet](https://experienceleague.adobe.com/docs/customer-one/using/home.html)
>2. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

<br>

## Flyttar till Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Flyttar till Adobe Experience Manager as a Cloud Service"
>abstract="Den här enpersonsmodellen visar det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager as a Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering."

**Experience Manager as a Cloud Service utgör en skalbar, säker och flexibel teknikgrund för Experience Manager Sites och Assets som gör att marknadsförare och IT kan fokusera på att leverera slagkraftiga upplevelser i stor skala.**

Med Experience Manager as a Cloud Service kan era team fokusera på innovationer istället för att planera för produktuppgraderingar. De nya funktionerna testas grundligt och levereras till era team utan avbrott så att de alltid har tillgång till den senaste programvaran.

Övergången till Cloud Service omfattar tre faser - Planering, Körning och Post Go-live.
För en lyckad och smidig övergång bör du säkerställa korrekt planering och följa bästa praxis som beskrivs i den här handboken.

I bilden nedan visas en högnivårepresentation av den rekommenderade övergången till Cloud Service.

![bild](/help/journey-migration/assets/home-img1.png)

<br>

### Planering

Innan du påbörjar en övergångsresa till Cloud Service bör du bekanta dig med Experience Manager as a Cloud Service och granska de märkbara ändringar som har gjorts i den samt även se vilka funktioner som har ersatts eller ersatts.

<table>
<tr>
<td>Projektidentifiering och utvärdering</td>
<td><ul><li>Se <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=en">Betydande ändringar av Experience Manager as a Cloud Service</a> för att förstå de viktiga skillnaderna mellan Adobe Experience Manager as a Cloud Service och Experience Manager 6.x.</li><li>Se <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">Föråldrade funktioner</a> om du vill veta mer om funktioner som har markerats som föråldrade.</li><li>[Endast för Cloud Service-migreringar] Utvärderar Cloud Servicens beredskap: Kör <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Best Practices Analyzer (BPA)</a> i källmiljö </li><li>Gör en bedömning mot märkbara förändringar och borttagna funktioner i Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Granska</td>
<td><ul><li>Utför ansträngningsberäkning och resursövningar baserat på upptäckt</li></ul></td>
</tr>
<tr>
<td>Mät</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Upprätta KPI:er för projekt</a>, resultatkriterier och projekttidslinjer</li></ul></td>
</tr>
</table>

>[!NOTE]
>Rapporten Best Practices Analyzer snabbar upp processen att beräkna den tid och kostnad som krävs för att gå över till AEM as a Cloud Service genom att tillhandahålla information som annars skulle behöva samlas in och utvärderas manuellt.


<br>

### Körning

Innan du påbörjar körningsfasen av ett projekt bör du vara ombord på Cloud Servicen. Du måste också bekanta dig med Cloud Manager. Detta är den mekanism som används för att distribuera projektkod till en Experience Manager Cloud Service-instans.

Med Cloud Manager kan organisationer självhantera Experience Manager i molnet. Den har en kontinuerlig integrering och kontinuerlig leverans ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html)) som gör det möjligt för IT-team och implementeringspartners att snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

#### Innehållsmigrering

1. [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration) : används för att flytta befintligt innehåll från en AEM (lokal eller AMS) till AEM Cloud Service-målinstansen.
2. [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html#package-manager) : används för import och export av ändringsbart innehåll i databasen.


#### Baktor/optimera

| Komma igång | Granska och reaktorkod | Dispatcher Review |
|---|---|---|
| <ul><li>[Konfiguration av lokal Dev](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html#local-development-environment-set-up)</li><li>[Local Dispatcher Setup](https://video.tv.adobe.com/v/30602/)</li><li>[Kompilera koden med SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)</li><li>[Granska AEM Dev Guidelines](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)<ul><li>Bakgrundsuppgifter och tidskrävande jobb</li><li>Sling Scheduler</li><li>Användning av indataström med mera</li></ul></li></ul> | <ul><li>Kör [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html) i källmiljön.[**Endast migrering**]<ul><li>Om projektstruktur (baserat på [Cloud Archetype](https://github.com/adobe/aem-project-archetype))<ul><li>Separation av kod och innehåll (mutable vs Immutable)</li><li>[Anpassade indexdefinitioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)</li><li>[Anpassade körningslägen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)</li></ul></li></ul></li><li>Granska och utför nödvändiga ändringar</li><li>[Distribuera](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) på lokal SDK</li><li>Utför röktestning via AEM SDK</li></ul> | <ul><li>Granska [Dispatcher-konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) för refactoring</li><li>Använd [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html) verktyg där så är lämpligt. [**Endast migrering**]</li><li>Testning kan utföras med [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)</li></ul> |

>[!TIP]
> Resurskunder: Granska och uppdatera resurser med [Migrering av molnresurser](https://github.com/adobe/aem-cloud-migration) verktyg


#### Driftsättning/GoLive

1. [Distribuera till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html) git
2. Kör kundkod via [Kvalitetspipeline för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html)
3. [Distribuera till utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html#debugging)
4. [**Endast migrering**] Innehållsöverföring med paket eller [Verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Utför rekommenderade testcykler (rök, kvalitetskontroll med mera)
6. Befordra till Cloud Manager Production Pipeline
7. Validering av röktest
8. GoLive

<br>

### Post GoLive

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar. 

>[!TIP]
> Verktyg finns för att felsöka AEM as a Cloud Service miljö
>1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html)
>3. [Hantera loggar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html)

<br>

### Verktyg och resurser

| Utvärdering | Refactoring | Modernisering av Experience Manager | Innehållsmigrering |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html)</li></ul> | <ul><li>[Statiska mallar till redigerbara mallar](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Utforma konfigurationer enligt policyer](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Grundkomponenter till kärnkomponenter](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[Klassiskt användargränssnitt till pekaktiverat användargränssnitt](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html)</li><li>[Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html#contentmanagement)</li></ul> |

>[!NOTE]
> Om du behöver mer hjälp kan du:
>1. [Kontakta Experience Manager Support-teamet](https://experienceleague.adobe.com/docs/customer-one/using/home.html)
>2. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)
