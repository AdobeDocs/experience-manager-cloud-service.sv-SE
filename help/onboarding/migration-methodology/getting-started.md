---
title: Migrering till Experience Manager som Cloud Service
description: Migrering till Experience Manager som Cloud Service
exl-id: 4d1addcf-b22d-41a3-ba5c-e5c42244e5cd
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 7%

---

# Migrering till Adobe Experience Manager som Cloud Service {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrering till AEM som molntjänst"
>abstract="Här beskrivs det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-distributioner till Experience Manager som en Cloud Service och hjälpa befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="Vad är nytt och annorlunda?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="Introduktion till AEM as a Cloud Service."

Adobe Experience Manager (AEM) som Cloud Service erbjuder en omgjord grund för Experience Manager, som bygger på en behållarbaserad infrastruktur, API-styrd utveckling och guidad DevOps-process, vilket gör att marknadsförare och utvecklare alltid kan ligga steget före i utvecklingen av kundupplevelsehanteringsinnovationer.

Cloud Service innehåller mängder av användningsklara funktioner och utbyggbarhet i Adobe Experience Manager tack vare den moderna molnbaserade arkitekturen som gör att varumärkena kan möta konsumenternas ständigt växande krav.

Den här enpersonsmodellen beskriver det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager som en Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Komma igång med Adobe Experience Manager som Cloud Service {#getting-started}

| Vad är det för skillnad? | Arkitektur - översikt |
|--------------------------|--------------------------|
| <ul><li>[Modern arkitektur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Automatiska uppdateringar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Asset Microservices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[Binärfiler för direktåtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[Separation av kod och innehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Replikering som en tjänst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[Admin console, Group/User Membership and ACLs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[Introduktion till AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Miljöhög](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Författarnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Publiceringsnivå](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)  (CI/CD)</li><li>[Identitetshantering ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) via  [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[Tjänsten Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service – körningsarkitektur](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service – körningsarkitektur")

<br>

## Developer Journey i Adobe Experience Manager som Cloud Service {#developer-journey}

### Utveckling

De grundläggande funktionerna för kodutveckling liknar i Adobe Experience Manager som en Cloud Service jämfört med Adobe Experience Manager On Premise och Managed Services.

Utvecklare skriver kod och testar den lokalt, som sedan skickas till Adobe Experience Manager på distans som en Cloud Service-miljö.

Se självhjälpsresurser om implementering för Experience Manager som Cloud Service för att lära dig hur du anpassar Experience Manager som Cloud Service.

| Lokal utveckling | Saker att veta innan du börjar |
|-----------|------------|
| <ol><li>Läs [dokumentationen för Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing) om du vill veta mer.</li><li>Titta på [Installera Dispatcher SDK](https://video.tv.adobe.com/v/30601) om du vill veta hur du installerar Dispatcher SDK</li><li>Titta på [Konfigurera Dispatcher SDK](https://video.tv.adobe.com/v/30602) för att förstå hur du konfigurerar Dispatcher SDK</li><li>Läs [dokumentationen till den lokala utvecklingsmiljön](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) om du vill veta mer</li><li>Konfigurerar åtkomst till Experience Manager [genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Grundläggande om utveckling](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Utvecklingsriktlinjer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[Om projektstrukturen Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Formatsystem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[Övertäckningar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Experience Manager som Cloud Service-API-referens](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> Se självstudiekurs om hur du [utvecklar och distribuerar WKND på lokal Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

### Distribuerar

Utvecklare skriver kod och testar den lokalt, som sedan skickas till AEM som en Cloud Service-miljö.

Cloud Manager, som var ett valfritt verktyg för innehållsleverans för Managed Services, krävs. Detta är nu den enda mekanismen för att distribuera kod till AEM som en Cloud Service-miljö.

Se självhjälpsresurser om hur du konfigurerar och distribuerar till AEM som en Cloud Service-miljö.

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
> Se självstudiekurs om hur du [distribuerar WKND till Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### Hjälp och resurser

1. [Tips och tricks för felsökning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (Endast tillgängligt i lokala SDK- och Experience Manager Cloud Dev-miljöer)
4. [Loggar och loggning](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM-loggar](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)  (build-unit-testing, code-scanning, build-image, deploy)
   * [Experience Manager Cloud Service Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Lokala SDK-loggar (under värd:port/crx-quickstart/logs)

>[!NOTE]
> Om du behöver mer hjälp kan du:
>1. [Kontakta Experience Manager Support-teamet](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Utforska [Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Flyttar till Adobe Experience Manager som Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Gå till Adobe Experience Manager som Cloud Service"
>abstract="Den här enpersonsmodellen beskriver det rekommenderade stegvisa tillvägagångssättet för att övergå från olika Experience Manager-driftsättningar till Experience Manager som en Cloud Service och hjälper befintliga kunder att leverera sammankopplade, kontinuerliga upplevelser på den här moderna, specialbyggda plattformen för upplevelsehantering."

**Experience Manager som Cloud Service är en skalbar, säker och flexibel teknikgrund för Experience Manager Sites and Assets som gör att marknadsförare och IT kan fokusera på att leverera slagkraftiga upplevelser i stor skala.**

Med Experience Manager som Cloud Service kan era team fokusera på innovationer istället för att planera för produktuppgraderingar. De nya funktionerna testas grundligt och levereras till era team utan avbrott så att de alltid har tillgång till den senaste programvaran.

Övergången till Cloud Service omfattar tre faser – Planering, Körning och Efter publicering.
För en lyckad och smidig övergång bör du säkerställa korrekt planering och följa bästa praxis som beskrivs i den här handboken.

Bilden nedan visar en illustrativ representation av den rekommenderade övergångsprocessen till Cloud Service.

![bild](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### Planering

Innan du påbörjar en övergångsresa till Cloud Service bör du bekanta dig med Experience Manager som Cloud Service och granska de betydande ändringar som gjorts i den samt även se vilka funktioner som har ersatts eller ersatts.

<table>
<tr>
<td>Projektidentifiering och utvärdering</td>
<td><ul><li>Se <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Observerbara ändringar av Experience Manager som Cloud Service</a> för att förstå de viktiga skillnaderna mellan Adobe Experience Manager som Cloud Service och Experience Manager 6.x.</li><li>Mer information om funktioner som har markerats som inaktuella finns i <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">Föråldrade funktioner</a>.</li><li>[Endast för Cloud Service-migreringar] Utvärderar Cloud Servicens beredskap: Kör <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">Best Practices Analyzer(BPA)</a> i källmiljön </li><li>Gör en bedömning mot märkbara förändringar och borttagna funktioner i Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Granska</td>
<td><ul><li>Utför ansträngningsberäkning och resursövningar baserat på upptäckt</li></ul></td>
</tr>
<tr>
<td>Mät</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Fastställa nyckeltal</a> för projekt, kriterier för framgång och projekttidslinjer</li></ul></td>
</tr>
</table>

>[!NOTE]
>Best Practices Analyzer Report snabbar upp processen att beräkna den tid och kostnad som krävs för att gå över till AEM som en Cloud Service genom att tillhandahålla information som annars skulle behöva samlas in och utvärderas manuellt.


<br>

### Körning 

Innan du startar körningsfasen av ett projekt bör du vara ombord på Cloud Servicen. Du måste också bekanta dig med Cloud Manager. Detta är den mekanism som används för att distribuera projektkod till en Experience Manager Cloud Service-instans.

Med Cloud Manager kan organisationer självhantera Experience Manager i molnet. Det innehåller en kontinuerlig integrering och ett kontinuerligt leveransramverk ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview)) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

#### Innehållsmigrering

1. [Verktyget](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration)  Innehållsöverföring: används för att flytta befintligt innehåll över från en AEM (lokal eller AMS) till AEM Cloud Service-målinstansen.
2. [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) : används för att importera och exportera muterbart innehåll i databasen.


#### Baktor/optimera

| Komma igång | Granska och reaktorkod | Dispatcher Review |
|---|---|---|
| <ul><li>[Konfiguration av lokal Dev](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Local Dispatcher Setup](https://video.tv.adobe.com/v/30602/)</li><li>[Kompilera koden med SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Granska AEM Dev Guidelines](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>Bakgrundsuppgifter och tidskrävande jobb</li><li>Sling Scheduler</li><li>Användning av indataström med mera</li></ul></li></ul> | <ul><li>Kör [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) i källmiljön.[**Endast migrering**]<ul><li>Om projektstrukturering (baserat på [molnarkityp](https://github.com/adobe/aem-project-archetype))<ul><li>Separation av kod och innehåll (mutable vs Immutable)</li><li>[Anpassade indexdefinitioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[Anpassade körningslägen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>Granska och utför nödvändiga ändringar</li><li>[Distribuera ](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) på lokal SDK</li><li>Utför röktestning via AEM SDK</li></ul> | <ul><li>Granska [Dispatcher-konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration) för omfaktorisering</li><li>Utnyttja [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher)-verktyget där det är lämpligt. [**Endast migrering**]</li><li>Testning kan utföras med [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Resurskunder: Granska och uppdatera resurser i arbetsflöden med [verktyg för resursmigrering](https://github.com/adobe/aem-cloud-migration)


#### Driftsättning/GoLive

1. [Distribuera till Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Manager
2. Kör kundkod via [Cloud Manager Quality Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)
3. [Distribuera till utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Migrering**] endastInnehållsöverföring med paket eller  [innehållsöverföringsverktyg](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) (CTT)
5. Utför rekommenderade testcykler (rök, kvalitetskontroll med mera)
6. Befordra till Cloud Manager Production Pipeline
7. Validering av röktest
8. GoLive

<br>

### Post GoLive

I fasen efter publicering bör du se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar. 

>[!TIP]
> Det finns verktyg för att felsöka AEM som en Cloud Service-miljö
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

