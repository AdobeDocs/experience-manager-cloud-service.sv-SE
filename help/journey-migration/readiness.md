---
title: Beredskapsfas
description: Lär dig mer om de steg du måste ta så att du kan vara säker på att AEM-installationen är klar att flyttas till molnet.
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
feature: Migration
role: Admin
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 1%

---

# Beredskapsfas {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planera övergången"
>abstract="Innan du börjar din övergångsresa till Cloud Service bör du bekanta dig med AEM as a Cloud Service. Granska de ändringar som gjorts och de funktioner som ersatts eller ersatts."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

I den här fasen av AEM as a Cloud Service migreringsresa bekanta du dig med AEM as a Cloud Service. Du kan granska de ändringar som gjorts och förstå vad som krävs för att planera en lyckad migrering till molnet.

## Story hittills {#story-so-far}

I det föregående dokumentet, [Komma igång med flytt till AEM as a Cloud Service](/help/journey-migration/getting-started.md), finns en lista med faser som du måste genomgå så att du kan migrera till AEM as a Cloud Service. Det redogör också för fördelarna med att migrera.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå vilka faktorer du måste tänka på så att du kan vara säker på att din AEM-installation är klar att flyttas till molnet:

* Läs om märkbara ändringar och borttagna funktioner
* Lär dig planera för övergången till AEM as a Cloud Service

## Se de anmärkningsvärda förändringarna i AEM as a Cloud Service-arkitekturen {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service har många nya funktioner och möjligheter för att hantera dina AEM-projekt.

Förutom dessa förbättringar har det införts flera skillnader mellan anläggningsinstallationer av AEM och Adobe Managed Services jämfört med AEM as a Cloud Service.

Listan med objekt i tabellen nedan är delmängden av de ändringar som är mest relevanta för en migrering till AEM as a Cloud Service. Du kan läsa den fullständiga listan med [Observerbara ändringar i Adobe Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>Vad har ändrats?</th>
    <th>Referens</th>
    <th>Viktiga uppgifter</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Separera muterbara och oföränderliga filter i motsvarande paket</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html">AEM as a Cloud Service Notable Changes</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM Project Structure för AEM as a Cloud Service</a></td>
    <td>Ett enskilt paket som kan distribueras till AEM as a Cloud Service kan ha underpaket, främst för att innehålla muterbart och oföränderligt innehåll separerat till sina egna paket.</td>
  </tr>
  <tr>
    <td>Repo Init</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit Documentation</a></td>
    <td>Repoinit-skript är det bästa sättet att skapa initiala nodstrukturer, användare, grupper eller tjänstanvändare. Eftersom dessa skript kan användas i körläge och hanteras via kodpaketsdistribution, ger de stor flexibilitet för att utföra databasinitieringsuppgifter.</td>
  </tr>
  <tr>
    <td>Anpassade körningslägen tillåts inte</td>
    <td></td>
    <td>Det finns bara stöd för körningslägen som tillhandahålls i AEM as a Cloud Service.<br>När ytterligare utvecklingsmiljöer läggs till kopplas alla till körningsläget "dev".</td>
  </tr>
  <tr>
    <td>Cloud Manager Pipeline Execution är det enda sättet att driftsätta</td>
    <td></td>
    <td>I AEM as a Cloud Service är åtkomst till /system/console inte tillåten. Därför måste alla OSGi-konfigurationer ingå i koden och distribueras som kod.<br>OSGi-konfigurationerna är tillgängliga i skrivskyddat läge för visning via Developer Console via Cloud Manager</td>
  </tr>
  <tr>
    <td>Replikeringsagenter ersätts av Sling Content Distribution</td>
    <td></td>
    <td>Konceptet för replikeringsagenten ersätts av Sing Content Distribution. Om det finns anpassningar som använder replikeringsagenter måste de omformas.<br>Omvänd replikering stöds inte</td>
  </tr>
  <tr>
    <td>CRX/DE och Package Manager</td>
    <td></td>
    <td>CRX/DE tillåts endast i utvecklingsmiljön.<br>Pakethanteraren är tillgänglig för alla författarinstanser, men paketen som ska distribueras får bara innehålla muterbart innehåll (till exempel: /content eller /conf)</td>
  </tr>
  <tr>
    <td>Inbyggd CDN och egen CDN</td>
    <td></td>
    <td>AEM as a Cloud Service innehåller CDN för alla miljöer som är optimerade för de flesta användningsområden.<br>Om du vill konfigurera ett eget CDN måste du skicka en begäran till Adobe Support för att det ska godkännas.<br>Om det godkänns pekar leveransnätverket snabbt och inte mot AEM-instanser i någon miljö.</td>
  </tr>
  <tr>
    <td>Långa jobb</td>
    <td></td>
    <td>Undvik tidskrävande jobb som Sling Schedulers och Cron, eftersom AEM-instanserna som körs i behållarna kan komma och gå när som helst.<br>Tänk om de här funktionerna så att du kan avlasta dem till Adobe Developer.</td>
  </tr>
  <tr>
    <td>Växla till asynkrona åtgärder</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html#configuring-asynchronous-msm-operations">Konfigurera asynkrona åtgärder</a></td>
    <td>För att förbättra övergripande prestanda i dina miljöer körs vissa åtgärder i asynkront läge. De asynkrona jobben köas och körs när systemresurser är tillgängliga.</td>
  </tr>
  <tr>
    <td>Tokenbaserad autentisering och integreringsstrategier</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html#the-server-to-server-flow">Genererar åtkomsttoken för serversides-API:er</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication">Token-based Authentication Tutorial</a></td>
    <td>Det är vanligt att system utanför AEM försöker utföra HTTP-åtgärder i AEM.<br>Vi rekommenderar att du implementerar de strategier som beskrivs här i stället för att förlita dig på att skapa lokala användarnamn med lösenord i AEM.</td>
  </tr>
  <tr>
    <td>IO-fil/diskanvändning</td>
    <td></td>
    <td>Det finns ingen garanti för hur mycket diskutrymme som tilldelas och instanserna i behållarna kommer och går. Därför är det inte tillrådligt att använda I/O-åtgärder för fil för att skriva eller läsa från disken som är kopplad till AEM-instansen.</td>
  </tr>
  <tr>
    <td>DAM - uppdatera resursarbetsflöde</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html">Asset Compute Service</a></td>
    <td>Mediebearbetningsstegen som ingår i arbetsflödet för DAM-uppdatering av resurser ersätts nu av Asset Compute-tjänsten</td>
  </tr>
  <tr>
    <td>Metoder för överföring av resurser och processteg i arbetsflödet som stöds i AEM as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html#post-processing-workflows-steps">Överför API-jämförelser och WF-processsteg som stöds</a></td>
    <td>I AEM as a Cloud Service direktuppspelas resursen i eller utanför binärlagringen under överföring eller hämtning av en resurs. <br>Alla arbetsflödesprocessteg stöds inte i AEMaaCS.</td>
  </tr>
  <tr>
    <td>Arbetsflödeskörare</td>
    <td></td>
    <td>Ta bort alla arbetsflödeskörare som utlöser ett körklart eller anpassat arbetsflöde för DAM Update Asset från koden. <br>Alla resurser som överförs till AEM as a Cloud Service kommer att bearbetas av resurshanteringstjänsten. Anpassade steg finns i <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows"> Efterbearbetningsarbetsflöden </a> om hur du konfigurerar och konfigurerar efterbearbetningsarbetsflöden.</td>
  </tr>
  <tr>
    <td>Anpassade återgivningssteg</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html">Bearbetar profiler</a></td>
    <td>Alla anpassade återgivningsgenereringar, bildkonverteringar och videokodningar måste avlastas till resurshanteringstjänsten genom att motsvarande bearbetningsprofiler skapas.</td>
  </tr>
  <tr>
    <td>Innehållssökning och indexering</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html">Innehållssökning och indexeringsändringar</a></td>
    <td>Den underliggande bearbetningen av index förändras avsevärt och när den börjar spelas in.<br>Fullständig förståelse för och omfaktorisering av Oak-index innan de hanteras i koden som du distribuerar.</td>
  </tr>
  <tr>
    <td>Alla underhållsaktiviteter är inte konfigurerbara</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html">Underhållsuppgifter för AEM as a Cloud Service</a></td>
    <td>Du kan bara konfigurera vissa underhållsuppgifter med AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>Ändringar i publiceringsdatabasen</td>
    <td></td>
    <td>Direktändringar i publiceringsdatabasen tillåts inte, förutom de ändringar som finns under /home. Vi rekommenderar alltid att ändringar som görs på författaren distribueras. Alla kod- och konfigurationsändringar måste distribueras via motsvarande Cloud Manager-pipeline.</td>
  </tr>
  <tr>
    <td>Dispatcher Configurations and Caching</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html">Dispatcher i molnet</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html#other-content">Cachehantering<br></td>
    <td>Dispatcher-konfigurationerna måste följa en specifik struktur.<br>Konfigurationerna måste hanteras som en del av koden och distribueras via Cloud Manager pipeline.</td>
  </tr>
  <tr>
    <td>Säkerhetskopiera och återställa</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html">AEM as a Cloud Service Säkerhetskopiering och återställning</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Ändringar i autentisering</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html">IMS-stöd för AEM as a Cloud Service</td>
    <td>Om du tidigare har använt SAML 2.0-integrering på både författare och publicering innan du går över till Cloud Service är den största förändringen att AEM as a Cloud Service Author bara integreras med Adobe IMS. AEM as a Cloud Service Publish-nivån kan dock fortfarande använda SAML eller andra autentiseringsintegreringar. AEM as a Cloud Service har endast stöd för IMS-autentisering för författare, administratörer och utvecklare. IMS-autentiseringen ger inte stöd för externa slutanvändare på kundsajter som webbplatsbesökare.</td>
  </tr>
</tbody>
</table>

## Föråldrade funktioner {#deprecated-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Adobe rekommenderar att du använder [Funktioner som inte längre används](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html#deprecated-features) för att bekanta dig med funktioner som markerats som borttagna i Experience Manager as a Cloud Service. Se vilken påverkan AEM har.

## Planera för en granskning av din AEM-installation {#review-planning}

När du har vant dig vid de ändringar som gjorts i AEM as a Cloud Service är det dags att börja planera för en granskning av din befintliga installation. Om du gör det blir det lättare att mäta nivån på de ändringar som krävs för att flytta den till molnet.

I följande bild visas de viktigaste stegen under granskningsfasen:

![Viktiga steg under granskningsfasen](/help/journey-migration/assets/planning-phaseimg1.png)

Därefter tittar vi närmare på vad varje steg innebär.

### Utvärderar Cloud Service beredskap {#assess-cloud-readiness}

Det första steget är att bedöma om du är redo att gå över från din nuvarande version av AEM till Cloud Service och avgöra vilka områden som behöver omfaktorisering för att vara kompatibel med AEM as a Cloud Service.

Gör en omfattande utvärdering av AEM källkod mot de märkbara ändringarna och de inaktuella funktionerna för att avgöra hur stor insats som förväntas under övergångsresan.

Antalet resultat kan direkt påverka tidslinjerna och projektets övergripande framgång. Därför rekommenderar Adobe att du tar reda på så mycket som möjligt så att du kan planera leveransen. Eller starta konversationerna så att du kan göra om alla anpassningar som behövs för att följa AEM as a Cloud Service bästa praxis.

**Best Practice Analyzer**

Du kan snabba upp utvärderingen genom att köra Best Practices Analyzer mot din nuvarande AEM-version. Att förstå hur det fungerar är avgörande för att påskynda utvärderingsplaneringen.

Du kan läsa mer om hur det fungerar genom att läsa dokumentationen för [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

**Skapa en bedömningsrapport om beredskap i molnet**

Nästa steg är att skapa en rapport baserad på alla de kunskaper som hittills har förvärvats. Du skapar rapporten genom att generera Best Practices Analyzer-rapporter från Stage- och Production-instanserna och [överför dem sedan till Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) för att få en sammanfattande rapport över användbara objekt.

En vanlig rapport ska innehålla följande indata:

* Dokumentation som beskriver funktionerna i just din AEM-installation
* Information om anpassade AEM-konfigurationer och -koder
* Production Dispatcher-konfigurationer
* Domänmappningar (CDN-konfigurationer) (om det finns några)

**Socialisera rapporten**

När Best Practices Analyzer-rapporterna är klara kan du dela dem med relevanta team så att ni kan bekräfta era resultat och planera för nästa steg. Beroende på inställningarna kan du även distribuera en utskriven version av rapporten genom att använda [Förhandsgranska](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Granska resursplanering {#review-resource-planning}

När du har uppskattat den nivå av arbete som krävs för att gå över till Cloud Service bör du identifiera resurser, skapa ett team och kartlägga roller och ansvarsområden för övergångsprocessen.

### Fastställa nyckeltal {#establish-kpis}

Om du inte har fastställt nyckeltal (KPI) tidigare rekommenderar vi att du skapar nyckeltal för din AEM-implementering så att ditt team kan fokusera på det som är viktigast.

Se [Utveckla nyckeltal](https://experienceleague.adobe.com/welcome/aem/part6.html) så att du kan lära dig hur du väljer rätt nyckeltal för dina affärsmål.

## What&#39;s Next {#what-is-next}

När du har förstått omfattningen av de ändringar som krävs för att gå över till AEM as a Cloud Service är det dags att [göra koden och innehållet i molnet redo](/help/journey-migration/implementation.md) innan du faktiskt utför migreringen.

## Ytterligare resurser {#additional-resources}

* [Komma igång med Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - En omfattande guide om hur du använder Cloud Acceleration Manager för att snabba upp din övergång till molnet.
* [AEM as a Cloud Service: Introduktion, arkitektur och andra tankar](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM a Cloud Service Home](/help/overview/introduction.md) - Här kan du få en översikt över dokumentationen för Experience Manager as a Cloud Service.
* [AEM as a Cloud Service-översikt](/help/overview/introduction.md) - Den här guiden ger en översikt över Experience Manager som en molntjänst, inklusive en introduktion, terminologi och arkitektur.
* [Onboarding Journey](/help/journey-onboarding/overview.md) - Den här guiden ger en sammanfattning av hur du kommer igång med Experience Manager as a Cloud Service, inklusive hur du får tillgång till och konfigurerar ditt team.
