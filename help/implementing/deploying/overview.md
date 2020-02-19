---
title: Distribuera till AEM som en molntjänst
description: 'Distribuera till AEM som en molntjänst '
translation-type: tm+mt
source-git-commit: 3cf5d17eab937c99c8bcaeb0ed8074672e71650f

---


# Distribuera till AEM som en molntjänst {#deploying-to-aem-as-a-cloud-service}

## Introduktion {#introduction}

De grundläggande funktionerna i kodutveckling liknar i AEM en molntjänst jämfört med lösningarna AEM On Premise och Managed Services. Utvecklare skriver kod och testar den lokalt, som sedan skickas till fjärr-AEM som en molntjänstmiljö. Cloud Manager, som var ett valfritt verktyg för innehållsleverans för hanterade tjänster, krävs. Detta är nu den enda mekanismen för att distribuera kod till AEM som en molntjänstmiljö.

Uppdateringen av AEM-versionen är alltid en separat distributionshändelse jämfört med att skicka anpassad kod. Om de visas på ett annat sätt bör anpassade kodreleaser testas mot den AEM-version som är i produktion eftersom det är den version som kommer att användas ovanpå. Uppdateringar av AEM-versioner som görs därefter, som är vanliga i jämförelse med hanterade tjänster idag, tillämpas automatiskt. De är avsedda att vara bakåtkompatibla med den kundkod som redan har distribuerats.

I följande video visas en översikt på hög nivå över hur du distribuerar kod till AEM som en molntjänst:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

I resten av det här dokumentet beskrivs hur utvecklare bör anpassa sina rutiner så att de arbetar med både AEM som en Cloud-tjänsts versionsuppdateringar och kunduppdateringar.

>[!NOTE]
>Vi rekommenderar att kunder med befintliga kodbaser genomgår en omstrukturering av databasen som beskrivs i [AEM-dokumentationen](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).


## Uppdateringar av AEM-versioner {#version-updates}

Det är viktigt att förstå att AEM uppdateras ofta, eventuellt så ofta som en gång om dagen, och kommer att fokusera på felkorrigeringar och prestandaförbättringar. Uppdateringen görs transparent och utan driftstopp. Uppdateringen är avsedd att vara bakåtkompatibel, vilket innebär att du inte behöver ändra egen kod. AEM-uppdateringar är i själva verket oberoende händelser från kundkoddistributioner. AEM-uppdateringen distribueras ovanpå den senaste lyckade kodningen, vilket innebär att ändringar som har implementerats sedan den senaste push-åtgärden inte kommer att distribueras.

>[!NOTE]
>
> Om anpassad kod publicerades till mellanlagring och sedan avvisades av dig, kommer nästa AEM-uppdatering att ta bort dessa ändringar för att återspegla Git-taggen för den senaste lyckade kundreleasen till produktionen.

Med jämna mellanrum kommer en ny funktion att publiceras med fokus på funktionstillägg och förbättringar som kommer att påverka användarupplevelsen mer än med de dagliga versionerna. En funktionsrelease aktiveras inte av driftsättningen av en stor ändringslista, utan snarare genom att en versionsväxling aktiveras som har ackumulerats under flera dagar eller veckor genom de dagliga uppdateringarna.

Hälsokontroller används för att övervaka programmets hälsa. Om dessa kontroller misslyckas under en AEM-uppdatering som en molntjänst, fortsätter inte releasen för den miljön och Adobe undersöker varför uppdateringen orsakade det oväntade beteendet.

### Sammansatt nodarkiv {#composite-node-store}

Som vi nämnt ovan kommer uppdateringarna i de flesta fall att innebära noll driftavbrott, även för författaren, som är ett kluster med noder. Rullande uppdateringar är möjliga på grund av funktionen&quot;composite node store&quot; i Oak. Med den här funktionen kan AEM referera till flera databaser samtidigt. I en rullande driftsättning innehåller den nya Green AEM-versionen en egen `/libs` (den TjärMK-baserade oföränderliga databasen), som skiljer sig från den äldre Blue AEM-versionen, även om båda refererar till en delad DocumentMK-baserad muterbar databas som innehåller områden som `/content`, `/conf`och `/etc` andra. Eftersom både den blå och den gröna har sina egna versioner av `/libs`kan de båda vara aktiva under den rullande uppdateringen, som båda tar trafik tills den blå har ersatts helt av den gröna.

## Kundreleaser {#customer-releases}

### Kodning mot rätt AEM-version {#coding-against-the-right-aem-version}

För tidigare AEM-lösningar ändrades den senaste AEM-versionen sällan (ungefär en gång per år med kvartalsvisa servicepaket) och kunderna skulle uppdatera produktionsinstanserna till den senaste snabbstarten på egen tid med referens till API Jar. Men AEM som en molntjänst uppdateras automatiskt till den senaste versionen av AEM oftare, så anpassad kod för interna releaser bör byggas mot de nyare AEM-gränssnitten.

Precis som för befintliga AEM-versioner som inte finns i molnet stöds en lokal offlineutveckling baserad på en viss snabbstart och förväntas vara det verktyg som i de flesta fall är det bästa för felsökning.

>[!NOTE]
>Det finns små skillnader i hur programmet fungerar på en lokal dator jämfört med Adobe Cloud. Dessa arkitektoniska skillnader måste respekteras under lokal utveckling och kan leda till ett annat beteende vid driftsättning i molninfrastrukturen. På grund av dessa skillnader är det viktigt att utföra de fullständiga testerna på dev- och stage-miljöer innan ny anpassad kod distribueras i produktionen.

För att kunna utveckla anpassad kod för en intern release bör den relevanta versionen av [AEM som en molntjänst-SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) hämtas och installeras. Mer information om hur du använder AEM som verktyg för Cloud Service Dispatcher finns på [den här sidan](/help/implementing/dispatcher/overview.md).

## Distribuera innehållspaket via Cloud Manager och Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Distributioner via Cloud Manager {#deployments-via-cloud-manager}

Kunder distribuerar anpassad kod till molnmiljöer via Cloud Manager. Det bör noteras att Cloud Manager omvandlar lokalt sammansatta innehållspaket till en artefakt som överensstämmer med Sling Feature Model, som är hur ett AEM-program som molntjänst beskrivs när det körs i en molnmiljö. När du tittar på paketen i Package Manager i Cloud-miljöer kommer namnet därför att innehålla &quot;cp2fm&quot; och alla omformade paket har tagits bort. De kan inte interagera med dem, vilket innebär att de inte kan hämtas, replikeras eller öppnas. Detaljerad dokumentation om konverteraren finns [här](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Innehållspaket som skrivits för AEM som ett molntjänstprogram måste ha en ren separation mellan oföränderligt och muterbart innehåll, och Cloud Manager kommer att framtvinga det genom att misslyckas med bygget och skicka ett meddelande som:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

Resten av detta avsnitt beskriver kompositionen och konsekvenserna av oföränderliga och muterbara paket.

### Oändringsbara innehållspaket {#immutabe-content-packages}

Allt innehåll och all kod som lagras i den oföränderliga databasen måste checkas in i Git och distribueras via Cloud Manager. Kod distribueras med andra ord aldrig direkt till en AEM-instans, till skillnad från aktuella AEM-lösningar. Detta garanterar att koden som körs för en viss release i en molnmiljö är identisk, vilket eliminerar risken för oavsiktlig kodvariation i produktionen. Som ett exempel bör OSGI-konfigurationen implementeras för källkontroll i stället för att hanteras vid körning via konfigurationshanteraren för AEM-webbkonsolen.

När programändringar på grund av det blå-gröna distributionsmönstret aktiveras av en växel kan de inte vara beroende av ändringar i den ändringsbara databasen, med undantag för tjänstanvändare, deras åtkomstkontrollistor, nodtyper och indexdefinitionsändringar.

För kunder med befintliga kodbaser är det viktigt att gå igenom den databasomstrukturering som beskrivs i AEM-dokumentationen för att se till att innehåll som tidigare fanns under /etc flyttas till rätt plats.

## OSGI-konfiguration {#osgi-configuration}

Som nämnts ovan bör OSGI-konfigurationen implementeras för källkontroll i stället för via webbkonsolen. Tekniker för detta är:

* Göra nödvändiga ändringar i utvecklarens lokala AEM-miljö med konfigurationshanteraren för AEM-webbkonsolen och exportera sedan resultaten till AEM-projektet i det lokala filsystemet
* Om du skapar OSGI-konfigurationen manuellt i AEM-projektet på det lokala filsystemet refererar AEM-konsolens konfigurationshanterare till egenskapsnamnen.

## Muterbart innehåll {#mutable-content}

I vissa fall kan det vara användbart att förbereda innehållsändringar i källkontrollen så att den kan distribueras av Cloud Manager när en miljö har uppdaterats. Det kan till exempel vara rimligt att skapa startvärden för vissa rotmappsstrukturer eller att göra ändringar i redigerbara mallar för att aktivera principer i de för komponenter som uppdaterades i programdistributionen.

Det finns två strategier för att beskriva det innehåll som ska distribueras av Cloud Manager till den ändringsbara databasen, innehållspaket som kan ändras och registersatser.

### Innehållspaket som kan ändras {#mutable-content-packages}

Innehåll som mappsökvägshierarkier, tjänstanvändare och åtkomstkontroller (ACL:er) är vanligtvis implementerade i ett maven-arkivtypsbaserat AEM-projekt. Teknikerna kan vara att exportera från AEM eller skriva direkt som XML. Under bygg- och distributionsprocessen paketerar Cloud Manager det resulterande innehållspaketet som kan ändras. Det muterbara innehållet installeras vid tre olika tillfällen under distributionsfasen i pipeline:

Innan den nya versionen av programmet startas:

* indexdefinitioner (lägg till, ändra, ta bort)

Under starten av den nya versionen av programmet men före bytet:

* Tjänstanvändare (lägg till)
* Tjänstanvändarens åtkomstkontrollistor (lägg till)
* nodtyper (lägg till)

Efter övergång till en ny version av programmet:

* Allt annat innehåll som kan definieras via jackrabbit-valvet. Exempel:
   * Mappar (lägg till, ändra, ta bort)
   * Redigerbara mallar (lägg till, ändra, ta bort)
   * Kontextmedveten konfiguration (vad som helst under `/conf`) (lägg till, ändra, ta bort)
   * Skript (paket kan utlösa Install hooks i olika faser av installationsprocessen för paketinstallationen

Det går att begränsa installation av muterbart innehåll för författare eller publicering genom att bädda in paket i en install.author- eller install.publish-mapp under `/apps`. Mer information finns i [AEM-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html) om rekommenderad projektomstrukturering.

>[!NOTE]
> Innehållspaket distribueras till alla miljötyper (dev, stage, prod). Det går inte att begränsa distributionen till en viss miljö. Denna begränsning finns för att säkerställa möjligheten att testa automatiserad körning. Innehåll som är specifikt för en viss miljö kräver manuell installation via Package Manager.

Det finns heller ingen mekanism för att återställa ändringar i det ändringsbara innehållspaketet efter att de har tillämpats. Om kunderna upptäcker ett problem kan de välja att åtgärda det i nästa kodversion eller som en sista utväg, återställa hela systemet till en tidpunkt före distributionen.

Alla inkluderade paket från tredje part måste valideras som AEM som en molntjänst som är kompatibel med, annars leder detta till ett distributionsfel.

Som nämnts ovan bör kunder med befintliga kodbaser följa den struktureringsövning av databasen som beskrivs i [AEM-dokumentationen](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html).

## Repoinit {#repoinit}

I följande fall är det att föredra att manuellt koda uttryckliga innehållsskapande `repoinit` -satser i OSGI-fabrikskonfigurationer:

* Skapa/ta bort/inaktivera tjänstanvändare
* Skapa/ta bort grupper
* Skapa/ta bort användare
* Lägg till åtkomstkontrollistor
   > [!NOTE]
   > Definitionen av åtkomstkontrollistor kräver att nodstrukturerna redan finns. Därför kan det vara nödvändigt att skapa en sökvägsprogramsats innan.
* Lägg till sökväg (t.ex. för rotmappsstrukturer)
* Lägg till CND (nodetype definition)

Repoinit är att föredra för de här användningsområdena för innehållsändringar som stöds på grund av följande fördelar:

* Repoinit skapar resurser vid start så att logiken kan ta tillvara dessa resurser för givet. I det ändringsbara innehållspaketet skapas resurser efter start, så programkod som förlitar sig på dem kan misslyckas.
* Repoinit är en relativt säker instruktionsuppsättning eftersom du uttryckligen kontrollerar vilken åtgärd som ska vidtas. De enda åtgärder som stöds är dessutom additiva, med undantag för ett fåtal säkerhetsrelaterade fall där användare, tjänstanvändare och grupper kan tas bort. En borttagning av något i det variabla innehållspaketet är däremot explicit.  När du definierar ett filter tas allt som täcks av ett filter bort. Försiktighet bör dock iakttas eftersom det finns scenarier där förekomsten av nytt innehåll kan ändra programmets beteende.
* Repoinit utför snabba och atomiska operationer. Blandbara innehållspaket i kontrast kan i hög grad vara beroende av prestanda beroende på de strukturer som täcks av ett filter. Även om du uppdaterar en enskild nod kan en ögonblicksbild av ett stort träd skapas.
* Det är möjligt att validera repoinit-satser i en lokal enhetsmiljö vid körning eftersom de körs när OSGi-konfigurationen registreras.
* Repoinit-satser är atomiska och explicita och hoppas över om läget redan matchar.

När Cloud Manager distribuerar programmet körs dessa programsatser, oberoende av installationen av innehållspaket.

Så här skapar du repoinit-satser:

1. Lägg till OSGi-konfiguration för PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` i en konfigurationsmapp i projektet
1. Lägg till repoinit-satser i egenskapen script för config. Syntaxen och alternativen beskrivs i [Sling-dokumentationen](https://sling.apache.org/documentation/bundles/repository-initialization.html). Observera att en överordnad mapp bör skapas explicit före deras underordnade mappar. Exempel: en explicit generering av `/content` before `/content/myfolder`, before `/content/myfolder/mysubfolder`. För ACL-listor som ställs in på lågnivåstrukturer rekommenderar vi att du ställer in dem på en högre nivå och arbetar med en `rep:glob` begränsning.  Exempel `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Validera på den lokala utvecklingsmiljön vid körning.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>För åtkomstkontrollistor som definierats för noder under `/apps` eller `/libs` repoinit startas körningen i en tom databas. Paketen installeras efter ompekning, så programsatser kan inte förlita sig på något som definierats i paketen, utan måste definiera villkoren som de överordnade strukturerna under.

>[!TIP]
>
>För åtkomstkontrollistor kan det vara krångligt att skapa djupa strukturer, och det är därför mer rimligt att definiera en åtkomstkontrollista på en högre nivå och begränsa var den ska agera via en begränsning av rep:glob.

Mer information om repoinit finns i [Sling-dokumentationen](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Package Manager &quot;one offs&quot; för paket med olika innehåll {#package-manager-oneoffs-for-mutable-content-packages}

I vissa fall bör ett innehållspaket installeras som en&quot;engångspaket&quot;. Du kan till exempel importera specifikt innehåll från produktion till mellanlagring för att felsöka ett produktionsproblem. I dessa scenarier kan Package Manager användas i AEM som molntjänstmiljöer.

Eftersom Package Manager är ett runtime-koncept går det inte att installera innehåll eller kod i den oföränderliga databasen, så dessa innehållspaket bör endast bestå av ändringsbart innehåll (huvudsakligen `/content` eller `/conf`). Om innehållspaketet innehåller innehåll som är blandat (både muterbart och oföränderligt) installeras endast det muterbara innehållet.

Alla innehållspaket som installeras via Cloud Manager (både ändringsbart och oföränderligt) visas i ett låst läge i användargränssnittet för AEM Package Manager. Dessa paket kan inte installeras om, byggas om eller laddas ned, och visas med suffixet **&quot;cp2fm&quot;** , vilket anger att installationen hanterades av Cloud Manager.

### Inklusive paket från tredje part {#including-third-party}

Det är vanligt att kunder inkluderar färdiga paket från tredjepartsleverantörer som programvaruleverantörer som Adobes översättningspartners. Rekommendationen är att lagra dessa paket i en fjärrdatabas och referera till dem i `pom.xml`. Detta är bara möjligt för offentliga databaser.

Om det inte går att lagra paketet i en fjärrdatabas kan kunderna placera det i en lokal, filsystemsbaserad Maven-databas som är kopplad till SCM som en del av projektet och som refereras av det som beror på det. Databasen skulle deklareras i projektforumen som visas nedan:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Alla inkluderade paket från tredje part måste följa AEM som riktlinjer för molntjänstkodning och paketering som beskrivs i den här artikeln, annars leder inkludering till ett distributionsfel.

Följande XML-kodutdrag för Maven POM visar hur paket från tredje part kan bäddas in i projektets &quot;Container&quot;-paket, som vanligtvis kallas **&#39;all&#39;**, via pluginkonfigurationen **filevault-package-maven-plugin** Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## Hur rullande distributioner fungerar {#how-rolling-deployments-work}

Precis som med AEM-uppdateringar distribueras kundreleaser med en strategi för rullande driftsättning för att eliminera driftavbrott i utvecklarkluster under rätt omständigheter. Den allmänna händelsesekvensen beskrivs nedan, där **Blue** är den gamla versionen av kundkoden och **Green** är den nya versionen. Både Blue och Green kör samma version av AEM-kod.

* Den blå versionen är aktiv och en release-kandidat för Green är inbyggd och tillgänglig
* Om det finns nya eller uppdaterade indexdefinitioner bearbetas motsvarande index. Observera att den blå distributionen alltid använder de gamla indexen, medan den gröna alltid använder de nya indexen.
* Grönt startar medan Blue fortfarande serverar
* Blue is running and service while Green is being checking by health checks
* Gröna noder som är klara att ta emot trafik och ersätta blå noder, som tas ned
* Med tiden ersätts blå noder av gröna noder tills endast grönt finns kvar, vilket slutför distributionen
* Allt nytt eller ändrat ändringsbart innehåll distribueras

## Index {#indexes}

Nya eller ändrade index kommer att orsaka ytterligare ett indexerings- eller omindexeringssteg innan den nya (gröna) versionen kan ta över trafiken. Information om indexhantering i Skyline finns i [den här artikeln](/help/operations/indexing.md). Du kan kontrollera statusen för indexeringsjobbet på Cloud Managers byggsida och får ett meddelande när den nya versionen är klar att börja trafikera.

>[!NOTE]
>
>Den tid som krävs för en rullande distribution varierar beroende på indexets storlek, eftersom den gröna versionen inte kan ta emot trafik förrän det nya indexet har genererats.

För närvarande fungerar inte Skyline med verktyg för indexhantering som ACS Commons Sörja för ekindexering.

## Replikering {#replication}

Publiceringsmekanismen är bakåtkompatibel med Java-API:erna för [AEM Replication](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

För att kunna utveckla och testa med replikering med molnförberedda AEM Quickstart måste de klassiska replikeringsfunktionerna användas med en författar-/publiceringskonfiguration. Om användargränssnittets startpunkt på AEM Author har tagits bort för molnet går användarna till `http://localhost:4502/etc/replication` för konfiguration.

## Bakåtkompatibel kod för rullande distributioner {#backwards-compatible-code-for-rolling-deployments}

Som anges ovan innebär AEM som en strategi för rullande driftsättning i molnet att både den gamla och den nya versionen kan användas samtidigt. Var därför försiktig med kodändringar som inte är bakåtkompatibla med den gamla AEM-versionen som fortfarande används.

Dessutom bör den gamla versionen testas för kompatibilitet med nya ändringsbara innehållsstrukturer som tillämpas i den nya versionen i händelse av återställning, eftersom det ändringsbara innehållet inte tas bort.

### Tjänstanvändare och ACL-ändringar {#service-users-and-acl-changes}

Ändring av tjänstanvändare eller åtkomstkontrollistor som behövs för att få tillgång till innehåll eller kod kan leda till fel i de äldre AEM-versionerna, vilket ger åtkomst till innehållet eller koden för de gamla tjänstanvändarna. För att åtgärda detta är det en rekommendation att göra ändringar spridda över minst två versioner, där den första versionen fungerar som en brygga innan den rensas i den efterföljande versionen.

### Indexändringar {#index-changes}

Om ändringar görs i index är det viktigt att den blå versionen fortsätter att använda sina index tills den avslutas, medan den gröna versionen använder sin egen ändrade indexuppsättning. Utvecklaren bör följa de indexhanteringstekniker som beskrivs [i den här artikeln](/help/operations/indexing.md).

### Konservativ kodning för återställningar {#conservative-coding-for-rollbacks}

Om ett fel rapporteras eller upptäcks efter distributionen är det möjligt att en återställning till den blå versionen krävs. Det är klokt att se till att den blå koden är kompatibel med alla nya strukturer som skapas av den gröna versionen eftersom de nya strukturerna (allt innehåll som kan ändras) inte återställs. Om den gamla koden inte är kompatibel måste korrigeringar tillämpas i efterföljande kundreleaser.

## Runmodes {#runmodes}

I befintliga AEM-lösningar kan kunderna köra instanser med godtyckliga körningslägen och använda OSGI-konfiguration eller installera OSGI-paket för dessa specifika instanser. Körningslägen som definieras omfattar vanligtvis *tjänsten* (författare och publicering) och miljön (dev, stage, prod).

Å andra sidan är AEM som en molntjänst mer övertygande om vilka körningslägen som finns tillgängliga och hur OSGI-paket och OSGI-konfigurationer kan mappas till dem:

* OSGI-konfigurationens körningslägen måste referera till dev, stage, prod för miljön eller författaren, publicera för tjänsten. En kombination av `<service>.<environment_type>` stöds, men dessa måste användas i den här speciella ordningen (till exempel author.dev eller publish.prod). OSGI-tokens ska refereras direkt från koden i stället för att använda `getRunModes` metoden, som inte längre inkluderar `environment_type` vid körning.
* Körningslägena för OSGI-paket är begränsade till tjänsten (författare, publicera). OSGI-paket per körning ska installeras i innehållspaketet under antingen `install/author` eller `install/publish`.

Precis som de befintliga AEM-lösningarna finns det inget sätt att använda körningslägen för att installera enbart innehåll för specifika miljöer eller tjänster. Om man ville skapa en egen utvecklarmiljö med data eller HTML som inte finns på scenen eller i produktionen kunde man använda pakethanteraren.

De runmode-konfigurationer som stöds är:

* **config** (*Standardvärdet gäller alla AEM-tjänster*)
* **config.author** (*Gäller alla AEM Author-tjänster*)
* **config.author.dev** (*Gäller AEM Dev Author service*)
* **config.author.stage** (*Gäller AEM Staging Author service*)
* **config.author.prod** (*Gäller AEM Production Author service*)
* **config.publish** (*Gäller AEM Publish-tjänsten*)
* **config.publish.dev** (*Gäller AEM Dev Publish-tjänsten*)
* **config.publish.stage** (*Gäller publiceringstjänsten* AEM Staging)
* **config.publish.prod** (*Gäller AEM Production Publish-tjänsten*)
* **config.dev** (*Gäller för AEM Dev-tjänster)
* **config.stage** (*Gäller för AEM-mellanlagringstjänster)
* **config.prod** (*Gäller för AEM Production Services)

Den OSGI-konfiguration som har de mest matchande körlägena används.

Vid lokal utveckling kan en startparameter för körningsläge skickas in för att ange vilken OSGI-konfiguration som ska användas i körningsläget.

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Konfiguration av underhållsaktiviteter i källkontroll {#maintenance-tasks-configuration-in-source-control}

Konfigurationer av underhållsaktiviteter måste sparas i källkontrollen eftersom **Verktyg > Åtgärder** inte längre är tillgängliga i molnmiljöer. Fördelen med detta är att man ser till att ändringarna bevaras avsiktligt i stället för att tillämpas reaktivt och kanske glöms bort. Mer information finns i artikeln [om](/help/operations/maintenance.md) underhållsaktiviteten.
