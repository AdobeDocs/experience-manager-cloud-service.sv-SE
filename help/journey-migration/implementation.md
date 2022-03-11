---
title: Implementeringsfas
description: Kontrollera att koden och innehållet är klara för migrering till molnet
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 9%

---

# Implementeringsfas {#implementation-phase}

Under kundens implementeringsfas kommer du att utforska de verktyg du kan använda för att göra koden och innehållet redo att flyttas över till AEM as a Cloud Service.

## Story hittills {#story-so-far}

I de föregående delarna av resan har du gått igenom [bekanta dig med förändringar i AEM as a Cloud Service](/help/journey-migration/getting-started.md), samt avgöra om distributionen är klar att flyttas till molnet med [beredskapsfas](/help/journey-migration/readiness.md).

Artikeln fortsätter med råd om hur du använder verktygen från Adobe för att se till att koden och innehållet är klara att flyttas till molnet.

## Syfte {#objective}

Syftet med detta dokument är att

* Vi presenterar dig för Cloud Manager, AEM kontinuerlig integrering och leveransramverk som används för att distribuera kod till AEM as a Cloud Service
* Kom igång snabbt med verktyget för innehållsöverföring
* Beskriv de verktyg för kodomfaktorisering som du måste använda för att uppdatera koden för AEM as a Cloud Service

## Använda Cloud Manager {#using-cloud-manager}

Innan du börjar måste du bekanta dig med Cloud Manager eftersom det är den enda metoden att distribuera kod till AEM as a Cloud Service.

Med Cloud Manager kan organisationer själva hantera AEM i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

Du kan bekanta dig med Cloud Manager genom att läsa resurserna nedan:

* [Onboarding för Experience Manager as a Cloud Service](/help/onboarding/home.md) för att förstå självhjälpsresurser om onboarding för Experience Manager as a Cloud Service.

* [Integrera Git med Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) för att lära dig mer om hur du använder en enstaka Git-databas för att driftsätta kod.

* [Adobe Experience as a Cloud Service-konfiguration](/help/security/ims-support.md#aem-configuration) för att lära dig mer om hur du hanterar produkter och användaråtkomst i Admin Console.

## Använd verktygen från Adobe för att göra ditt innehåll och din kod i molnet redo {#use-tools-to-make-code-and-content-cloud-ready}

Hur övergången till Cloud Service ser ut beror på vilka system du har köpt och vilka rutiner du har under hela programvaruutvecklingen.

I följande bild visas de huvudsakliga stegen som ingår i fasen, som innefattar att konvertera kod och innehåll för användning med AEM as a Cloud Service:

![bild](/help/journey-migration/assets/exec-image1.png)

Vi börjar med att gå igenom de verktyg du behöver för att uppnå detta i kapitlen nedan.

## Innehållsmigrering {#content-migration}

Om du vill migrera innehåll från den aktuella AEM till Cloud Servicen kan du använda verktyget för innehållsöverföring i Adobe.

Med det här verktyget kan du ange önskad delmängd av innehållet som du vill överföra från din AEM-källinstans till din AEM Cloud Service-instans.

Innehållsmigrering är en flerstegsprocess som kräver planering, spårning och samarbete mellan olika team.

En fullständig beskrivning av hur verktyget fungerar och hur vi rekommenderar att du använder det finns i [Dokumentation för verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Omstrukturering av kod {#code-refactor}

### Konfigurera för utveckling {#set-up-for-development}

Det är dags att börja omfaktorisera de befintliga funktionerna så att de blir kompatibla med Cloud Services.

För att göra detta måste du ta en titt på dokumentationen som beskriver de grundläggande verktygen du behöver för att börja omfaktorisera koden:


* Under planeringen är det en god idé att ha en lista över områden som måste omarbetas för att vara kompatibla med AEM as a Cloud Service. Du kan granska [Utvecklingsriktlinjer](/help/implementing/developing/introduction/development-guidelines.md) om du vill ha mer information om hur du kan omforma och optimera kod för Cloud Service.
* Läs mer om [Hantera konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) på AEM as a Cloud Service.
* Lär dig hur du konfigurerar en lokal utvecklingsmiljö genom att hämta [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* Äntligen bekanta dig med [AEM as a Cloud Service Java API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Dessutom kan du:

* I den här videon får du veta hur du installerar Dispatcher SDK lokalt:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* I den här videon ser du hur du konfigurerar Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### En förändring i sinneset {#a-change-in-mindset}

Att utveckla och köra kod i AEM as a Cloud Service kräver en förändring i sinnesen. Observera att koden måste vara flexibel, särskilt eftersom en instans kan avbrytas när som helst. Kod som körs i Cloud Service måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs.

Vissa ändringar krävs för att AEM Maven-projekt ska vara molnkompatibla. AEM as a Cloud Service kräver separation av *innehåll* och *kod* till distinkta paket för distribution till AEM:

* `/apps` och `/libs` betraktas som oföränderliga AEM eftersom de inte kan ändras efter att AEM startats (det vill säga vid körning). Detta inkluderar åtgärder för att skapa, uppdatera eller ta bort. Alla försök att ändra ett oföränderligt område vid körning misslyckas.

* Allt annat i databasen (till exempel `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) är alla ändringsbara områden, vilket innebär att de kan ändras under körning.

Du kan lära dig mer genom att läsa [Rekommenderad paketstruktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) dokumentation.


### Migreringsverktyg för molnet {#cloud-migration-tools}

I Adobe finns flera verktyg som hjälper dig att snabba upp vissa av dina åtgärder för kodomfaktorisering. Om du förstår dessa verktyg och de problem de löser blir migreringen mindre komplicerad och tidsödande.

* [Migrering av arbetsflöde för tillgångar](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), ett verktyg som används för att automatiskt migrera arbetsflöden för bearbetning av resurser
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), ett verktyg som konverterar dina befintliga Dispatcher-konfigurationer till ett format som är klart för AEM as a Cloud Service.
* [Databasmodernisering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en), ett verktyg som tar ett AEM flerlägesprojekt som indata och konverterar det till ett AEM as a Cloud Service
* [Indexkonverterare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en), ett verktyg som konverterar index till ett formulär som är kompatibelt med AEM as a Cloud Service
* [Moderniseringsverktyg](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), en svit med verktyg som kan användas för att konvertera äldre AEM till de moderna och stödda funktionerna i AEM as a Cloud Service.

När du väl har konfigurerat den lokala utvecklingsmiljön kan du bekanta dig med den AEM as a Cloud Service SDK:n genom att kontakta [dokumentation](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Schemalägg en fryst kod {#schedule-a-code-freeze}

För att kunna hantera kodutvecklingen på din aktiva AEM tillsammans med kodomfaktoriseringsuppgifterna som en del av din övergångsresa, rekommenderar vi att du planerar en frysperiod tills du har slutfört omstruktureringen av ditt Maven-projekt så att det blir kompatibelt med AEM as a Cloud Service.

När projektomstruktureringen är klar kan du återuppta utvecklingen av ny kod baserat på den nya strukturen. Detta minskar antalet fel i molnhanterarens pipeline under koddistribution och testning.

>[!NOTE]
>Aktiviteterna Innehållsöverföring och Kodreaktorn behöver inte utföras sekventiellt. Dessa åtgärder kan utföras oberoende av varandra. Korrekt projektstruktur krävs dock för att innehållet ska återges korrekt i Cloud Service-miljön.

## Bästa metoder för koddriftsättning och testning {#best-practices}

Molnhanterarens pipeline stöder körning av tester som körs mot scenmiljön.

Följ god praxis i dokumenten nedan när det gäller kvalitetstestning av kod:

* [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md), ett dokument som beskriver processen att skriva testskript och som beskriver konceptet med rekommenderad täckning på minst 50 %.
* [Förstå regler för anpassad kodkvalitet](/help/implementing/cloud-manager/custom-code-quality-rules.md) som syftar till att beskriva de anpassade regler för kodkvalitet som körs av Cloud Manager och som baseras på bästa praxis från AEM Engineering.

## Förbereder för GoLive {#preparing-for-go-live}

När du förbereder källsystemet för migrering måste du utföra åtgärder på system- och AEM-nivå. Du kan börja med att verifiera att innehållsdatabasen är i ett väl underhållet tillstånd genom att kontrollera [rensning av revision](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) och [skräpinsamling för datalager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) aktivitetsstatus. Om du kör AEM version 6.3 (eftersom verktyget Innehållsöverföring är kompatibelt från version 6.3 och framåt) bör du utföra offlinekomprimering följt av skräpinsamlingen i datalagret.

[Konsekvenskontroll av data](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) rekommenderas för alla AEM versioner för att säkerställa att innehållsarkivet är i ett bra läge för att starta migreringsaktiviteter.

Åtkomst på systemadministratörsnivå krävs för att installera och konfigurera [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

Vi rekommenderar även att du granskar resurser, sidor, AEM projekt, användare och grupper som inte används för att spara tid när du migrerar. Se [Hälsa för innehållsdatabas](#repository-health) -avsnitt.

### Hälsa för innehållsdatabas {#repository-health}

En gång för alla [produktionsklona](#proof-of-migration) fastställs, fortsätta för att kontrollera databasens hälsa. Som nämndes i föregående avsnitt är målet att rensa och komprimera databasen på källan innan migreringen startar. Det här steget kan spara mycket tid i annat fall för felsökning när migreringen startar.

| Åtgärdsobjekt | Viktiga uppgifter |
|---------|----------|
| Användare, grupper och behörigheter | Ni måste förstå hur många användare, grupper och komplex medlemskapet är. Leta efter möjligheter att rensa bort oanvända användare, grupper i källan före migrering. |
| Ofullständig resursbearbetning | Försök att slutföra bearbetningen av resurser i källsystemet innan du påbörjar migreringen för att undvika potentiella problem AEM as a Cloud Service eftermigrering. |
| Innehållshälsa | Vi rekommenderar att du frågar efter skadat innehåll och tömmer det innan du startar migreringen. Du kan till exempel söka efter resurser eller sidor som inte har ursprungliga återgivningar eller som fastnat i arbetsflödesbearbetningen. Se även [Resurshälsa](#asset-health). |

## Samlar in data {#gathering-data}

>[!NOTE]
> The [Strategi för innehållsmigrering och tidslinje](#content-strategy-and-timeline) mer ingående information om hur man extrapolerar insamlade data och skapar en migreringsplan.

Genom att samla in data kan du planera migreringsaktiviteterna och tillhörande uppgifter. Extraherings- och inmatningstiderna är särskilt användbara eftersom datapunkterna kan kopplas till en viss migreringsuppsättningens storlek. Därför kan dessa datapunkter extrapoleras för att ta fram en plan:

* Total tid som tagits för [extrahering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Total tid som tagits för [förtäring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Total tid som tagits för uppräkning [extrahering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* Total tid som tagits för uppräkning [förtäring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

En annan viktig datapunkt är hur lång tid det tar att slutföra [användarmappning](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), om detta är kopplat till innehållsmigreringen. Du kan ta den här datapunkten i beaktande för mer realistiska uppskattningar, eftersom den kommer att läggas till i den övergripande extraheringstidslinjen och det kanske inte krävs att den körs under de övre uppdateringarna.

Dessa datapunkter kan även hjälpa dig [Fastställa KPI:er](/help/journey-migration/readiness.md#establish-kpis) och andra migreringsrelaterade uppgifter.

### Migreringsplan {#migration-plan}

Baserat på de datapunkter du har samlat in (se ovan) kan du skapa en migreringsplan som kan integreras i en makroprojektplan. Detta steg kommer att göra det möjligt för alla viktiga intressenter att visualisera och planera kring migreringsaktiviteterna.

I följande tabell visas en typisk migreringsplan:

| Migreringsiteration | Startdatum | Beräknat slutdatum | Beroenden | Beräknad varaktighet (i dagar) | Ytterligare information/åtgärdsobjekt |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-SSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

Som du kan se i tabellen ovan är det praktiskt att följa ett specifikt namnformat för att identifiera migreringsiterationerna, till exempel: **PRDCLONE** för AEM källmiljö, **FÖRFATTARE/PUBLICERARE** för AEM as a Cloud Service miljö, **CSSTAGE-AUTHOR** för den AEM as a Cloud Service instansen och så vidare.

Några viktiga detaljer som påverkar migreringsplanen:

**Totalt antal extraheringar som krävs**

* Skapar- och publiceringsextraheringar i specifika miljöer betraktas som två parallella extraheringar eftersom de är oberoende av varandra.
* Antal Top Up-extraheringar baserat på databastillväxt under specifika tidsperioder.

**Totalt antal förslag som krävs**

* Det är viktigt att hämta det här objektet till planen, eftersom en extraherad uppsättning kan hämtas in i flera Cloud Service.
* Antal toppfrågor.
* Att migrera innehåll från källförfattaren till molntjänstförfattarinstansen och från källpubliceringen till Cloud Service Publish är det bästa sättet att undvika att samla in allt författarinnehåll i Cloud Service Publish.

### Migreringsspårare {#migration-tracker}

Du kan använda flyttningsspåraren för att anteckna tider för både inledande och övre körningar. Dessa datapunkter hjälper dig att formulera realistiska krav på frysning av innehåll innan den sista uppsättningen.

Spåraren hjälper dig även att:

* Identifiera eventuella avvikelser från planeraren som kräver justeringar i tidslinjerna i planen eller i farten
* Tillhandahålla en realistisk status som kan användas i all nödvändig kommunikation
* Planera för inledande eller framtida toppmigreringar

I följande tabell visas en funktionell flyttningsspårare:

| Källa (miljö/instans/URL) | Mål (miljö/instans/URL) | Namn på migreringsuppsättning, typ (inledande eller övre) | Storlek på migreringsuppsättning (MB) | Användarmappning (Ja/Nej) | Varaktighet för extrahering (start, slut, tid) | Inmatningstid (start, slut, tid) | Problem / lösningar / Detaljer |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## Strategi för innehållsmigrering och tidslinje {#content-strategyand-timeline}

I följande avsnitt visas viktiga steg och tillhörande uppgifter som kan användas för att utforma en strategi för innehållsmigrering och tidslinje.

![bild](/help/journey-migration/assets/content-migration2.png)

### Engagemang {#fitment}

* Rensning av revisioner, skräpinsamling i datalager och konsekvenskontroll av data. Se även [Förbereder för GoLive](#preparing-for-go-live)
* [Samla in statistik](#gathering-data) om AEM källdatabas:
   * Storlek på segmentlager
   * Storlek på indexarkiv
   * Antal sidor
   * Antal tillgångar
   * Antal användare och grupper
* Ta reda på om följande funktioner är aktiverade i AEM (krävs även i AEM as a Cloud Service):
   * Smart taggning
   * Likhetssökning
   * Sök efter text i Word- och PDF-dokument
* Samla in Best Practice Analyzer [rapport](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importera till [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Granska självanalysrekommendationen för att säkerställa att AEM as a Cloud Service kan hantera lagringskraven.
* Skapa en Adobe Support-biljett för eventuella förtydliganden innan du fortsätter med migreringsplanen.

### Bevis på migration {#proof-of-migration}

* Begär en produktionsklona som:
   * Finns i samma nätverkszon
   * Tillhandahåller produktionsinnehåll som användare och grupper
   * Klonar författare och publicering - en nod var om det är ett kluster eller en publiceringsgrupp
* Välj en delmängd av innehållet som ska migreras så att:
   * Det är en blandning av alla tillgängliga innehållstyper
   * Innehåller alla användare och grupper om det finns [användarmappning](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) krävs
* Inkluderar antingen 25 % av innehållet eller upp till 1 TB av innehållet, beroende på vilket som är lägst.
* Kör minst en full och [uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) migration, från produktionsklonen till den AEM as a Cloud Service icke-produktionsmiljön,
* Lös eventuella problem som:
   * Diskutrymme på AEM
   * Anslutning mellan AEM och AEM as a Cloud Service
   * Alla [begränsningar relaterade till förtäring](go-live.md#known-limitations).
* Registrera hur lång tid det tar [extraktion och förtäring](#gathering-data):
   * Se hur mycket innehåll som läggs till per vecka
   * Extrapolera tiden som mäts från migreringsbeviset för att skapa en [migreringsplan](#migration-plan).

## What&#39;s Next {#what-is-next}

När du har förstått hur du ska bedöma om AEM är redo att flyttas till molnet, och vi har lärt oss hur vi använder de verktyg som behövs för att göra det klart, är det dags att gå vidare till [direktfas](/help/journey-migration/go-live.md).
