---
title: Distribuera till AEM as a Cloud Service
description: Läs mer om grunderna och de bästa sätten att distribuera till AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3429'
ht-degree: 0%

---

# Distribuera till AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introduktion {#introduction}

De grundläggande funktionerna för kodutveckling liknar de i AEM as a Cloud Service jämfört med AEM On Premise och Managed Services. Utvecklare skriver kod och testar den lokalt, som sedan skickas till fjärrmiljöer på AEM as a Cloud Service. Cloud Manager, som var ett valfritt verktyg för innehållsleverans för Managed Services, krävs. Det här leveransverktyget är nu den enda mekanismen för att distribuera kod till AEM as a Cloud Service miljö för utveckling, scener och produktion. För snabb funktionsvalidering och felsökning innan du distribuerar de tidigare miljöerna kan koden synkroniseras från en lokal miljö till en [Rapid Development Environment](/help/implementing/developing/introduction/rapid-development-environments.md).

Uppdateringen av [AEM](/help/implementing/deploying/aem-version-updates.md) är alltid en separat distributionshändelse från att trycka [egen kod](#customer-releases). Om du tittar på en annan metod bör anpassade kodreleaser testas mot den AEM versionen som är i produktion eftersom det är det som distribueras högst upp. AEM versionsuppdateringar som görs därefter, som är vanliga och som tillämpas automatiskt. De är avsedda att vara bakåtkompatibla med den kundkod som redan har distribuerats.

I resten av det här dokumentet beskrivs hur utvecklare bör anpassa sina rutiner så att de kan arbeta med både AEM as a Cloud Service versionsuppdateringar och kunduppdateringar.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Kundreleaser {#customer-releases}

### Kodning mot rätt AEM {#coding-against-the-right-aem-version}

För tidigare AEM ändrades den senaste AEM versionen sällan (ungefär en gång om året med kvartalsvisa servicepaket) och kunderna uppdaterar produktionsinstanserna till den senaste snabbstarten på egen tid med referens till API Jar. Program på AEM as a Cloud Service uppdateras automatiskt till den senaste versionen av AEM oftare, så anpassad kod för interna releaser bör byggas mot den senaste AEM versionen.

Precis som för befintliga AEM som inte är molnbaserade stöds en lokal offlineutveckling baserad på en specifik snabbstart och förväntas vara det verktyg som normalt används för felsökning.

>[!NOTE]
>Det finns små skillnader i hur programmet fungerar på en lokal dator jämfört med Adobe Cloud. Dessa arkitektoniska skillnader måste respekteras under lokal utveckling och kan leda till ett annat beteende vid driftsättning i molninfrastrukturen. På grund av dessa skillnader är det viktigt att utföra de fullständiga testerna på dev- och stage-miljöer innan ny anpassad kod distribueras i produktionen.

För att utveckla anpassad kod för en intern release, den relevanta versionen av [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) ska hämtas och installeras. Mer information om hur du använder AEM as a Cloud Service Dispatcher Tools finns i [den här sidan](/help/implementing/dispatcher/disp-overview.md).

I följande video visas en översikt på hög nivå över hur du distribuerar kod till AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Distribuera innehållspaket via Cloud Manager och Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Distributioner via Cloud Manager {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

Kunder distribuerar anpassad kod till molnmiljöer via Cloud Manager. Cloud Manager omvandlar lokalt sammansatta innehållspaket till en artefakt som överensstämmer med Sling-funktionsmodellen, vilket är hur ett program på AEM as a Cloud Service beskrivs när det körs i en molnmiljö. När du tittar på paketen i [Pakethanteraren](/help/implementing/developing/tools/package-manager.md) i molnmiljöer innehåller namnet&quot;cp2fm&quot; och alla metadata har tagits bort för de omformade paketen. De kan inte interagera med dem, vilket innebär att de inte kan hämtas, replikeras eller öppnas. Detaljerad dokumentation om konverteraren kan [hittades här](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Innehållspaket som skrivits för program på AEM as a Cloud Service måste ha en ren separation mellan oföränderligt och muterbart innehåll och Cloud Manager installerar bara det muterbara innehållet, och ett meddelande som följande skickas:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

Resten av detta avsnitt beskriver kompositionen och konsekvenserna av oföränderliga och ändringsbara paket.

### Oändringsbara innehållspaket {#immutabe-content-packages}

Allt innehåll och all kod som lagras i den oföränderliga databasen måste checkas in i Git och distribueras via Cloud Manager. Kod distribueras med andra ord aldrig direkt till en AEM som körs, till skillnad från den aktuella AEM. Det här arbetsflödet säkerställer att koden som körs för en viss release i valfri molnmiljö är identisk, vilket eliminerar risken för oavsiktlig kodvariation i produktionen. Som ett exempel bör OSGI-konfigurationen implementeras för källkontroll i stället för att hanteras vid körning med hjälp av AEM webbkonsols konfigurationshanterare.

När programändringar på grund av distributionsmönstret aktiveras av en växel kan de inte vara beroende av ändringar i den ändringsbara databasen förutom för tjänstanvändare, deras åtkomstkontrollistor, nodtyper och ändringar i indexdefinitioner.

För kunder med befintliga kodbaser är det viktigt att gå igenom den databasomstrukturering som beskrivs i AEM dokumentation för att se till att innehåll som tidigare fanns under /etc flyttas till rätt plats.

Vissa ytterligare begränsningar gäller för dessa kodpaket, till exempel [installera kopplingar](https://jackrabbit.apache.org/filevault/installhooks.html) stöds inte.

## OSGI-konfiguration {#osgi-configuration}

Som nämnts ovan bör OSGI-konfigurationen implementeras för källkontroll i stället för via webbkonsolen. Tekniker för detta är:

* Göra nödvändiga ändringar i utvecklarens lokala AEM med AEM webbkonsols konfigurationshanterare och exportera sedan resultaten till det AEM projektet i det lokala filsystemet
* Om du skapar OSGI-konfigurationen manuellt i det AEM projektet i det lokala filsystemet refererar AEM konsolens konfigurationshanterare till egenskapsnamnen.

Läs mer om OSGI-konfiguration på [Konfigurera OSGi för AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Muterbart innehåll {#mutable-content}

Ibland kan det vara användbart att förbereda innehållsändringar i källkontrollen så att den kan distribueras av Cloud Manager när en miljö har uppdaterats. Det kan t.ex. vara rimligt att använda vissa rotmappsstrukturer. Eller justera ändringar i redigerbara mallar för att aktivera principkomponenter som uppdaterats av programdistributionen.

Det finns två strategier för att beskriva innehållet som distribueras av Cloud Manager till den ändringsbara databasen, innehållspaket som kan ändras och `repoinit` -programsatser.

### Innehållspaket som kan ändras {#mutable-content-packages}

Innehåll som mappsökvägshierarkier, tjänstanvändare och åtkomstkontroller (ACL:er) är vanligtvis implementerade i ett maven-arkivtypsbaserat AEM. Teknikerna är bland annat att exportera från AEM eller skriva direkt som XML. Under bygg- och distributionsprocessen paketerar Cloud Manager det resulterande innehållspaketet som kan ändras. Det muterbara innehållet installeras vid tre olika tidpunkter under distributionsfasen i pipeline:

Innan den nya versionen av programmet startas:

* indexdefinitioner (lägg till, ändra, ta bort)

Under starten av den nya versionen av programmet men före bytet:

* Tjänstanvändare (lägg till)
* Tjänstanvändarens åtkomstkontrollistor (lägg till)
* nodtyper (lägg till)

Efter övergång till en ny version av programmet:

* Allt annat innehåll som kan definieras med jacka-kanin-valvet. Till exempel:
   * Mappar (lägg till, ändra, ta bort)
   * Redigerbara mallar (lägg till, ändra, ta bort)
   * Kontextmedveten konfiguration (allt under `/conf`) (lägg till, ändra, ta bort)
   * Skript (paket kan utlösa Install-kopplingar vid olika faser av installationsprocessen för paketinstallationen. Se [Jackrabbits dokumentation om filevault](https://jackrabbit.apache.org/filevault/installhooks.html) om att installera kopplingar. AEM CS använder för närvarande Fireworks version 3.4.0, som begränsar möjligheten att installera kopplingar till administratörer, systemanvändare och medlemmar i administratörsgruppen).

Det går att begränsa installationer av muterbart innehåll till författare eller publicering genom att bädda in paket i en install.author- eller install.publish-mapp under `/apps`. Omstrukturering för att återspegla denna uppdelning gjordes i AEM 6.5 och närmare information om den rekommenderade projektomstruktureringen finns i [AEM 6.5-dokumentation.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>Innehållspaket distribueras till alla miljötyper (dev, stage, prod). Det går inte att begränsa distributionen till en viss miljö. Denna begränsning finns för att säkerställa möjligheten att testa automatiserad körning. Innehåll som är specifikt för en viss miljö kräver manuell installation [Pakethanteraren](/help/implementing/developing/tools/package-manager.md).

Det finns inte heller någon mekanism för att återställa ändringar i det ändringsbara innehållspaketet efter att de har tillämpats. Om kunderna upptäcker ett problem kan de välja att åtgärda det i nästa kodversion eller som en sista utväg, återställa hela systemet till en tidpunkt före distributionen.

Alla inkluderade tredjepartspaket måste valideras som AEM as a Cloud Service kompatibla, annars leder inkludering till ett distributionsfel.

Som nämnts ovan bör kunder med befintliga kodbaser uppfylla kraven i den omstrukturering av databasen som krävs för de ändringar i 6.5-databasen som beskrivs i [AEM 6.5-dokumentation.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## Repoinit {#repoinit}

I följande fall är det att föredra att använda handkodning för att skapa explicit innehåll `repoinit` programsatser i OSGI-fabrikskonfigurationer:

* Skapa/ta bort/inaktivera tjänstanvändare
* Skapa/ta bort grupper
* Skapa/ta bort användare
* Lägg till åtkomstkontrollistor

  >[!NOTE]
  >
  >Definitionen av åtkomstkontrollistor kräver att nodstrukturerna redan finns. Därför kan det vara nödvändigt att skapa en sökvägsprogramsats innan.

* Lägg till sökväg (t.ex. för rotmappsstrukturer)
* Lägga till CND (nodetypdefinitioner)

Repoinit är att föredra för de här användningsområdena för innehållsändringar som stöds på grund av följande fördelar:

* `Repoinit` skapar resurser vid start så att logiken kan ta tillvara dessa resurser för givet. I det ändringsbara innehållspaketet skapas resurser efter start, så programkod som förlitar sig på dem kan misslyckas.
* `Repoinit` är en relativt säker instruktionsuppsättning eftersom du uttryckligen kontrollerar vilken åtgärd som ska vidtas. De enda åtgärder som stöds är dessutom additiva, förutom några säkerhetsrelaterade fall som tillåter borttagning av användare, tjänstanvändare och grupper. En borttagning av något i det ändringsbara innehållspaketet är däremot explicit. När du definierar ett filter tas allt som ingår i ett filter bort. Försiktighet bör dock iakttas eftersom det finns scenarier där förekomsten av nytt innehåll kan ändra programmets beteende.
* `Repoinit` utför snabba och atomiska operationer. Blandbara innehållspaket i kontrast kan i hög grad vara beroende av prestanda beroende på de strukturer som täcks av ett filter. Även om du uppdaterar en enskild nod kan en ögonblicksbild av ett stort träd skapas.
* Det går att validera `repoinit` programsatser på en lokal enhetsmiljö vid körning eftersom de körs när OSGi-konfigurationen registreras.
* `Repoinit` -programsatser är atomiska och explicita och hoppas över om läget redan matchar.

När Cloud Manager distribuerar programmet körs dessa programsatser, oberoende av installationen av innehållspaket.

Skapa `repoinit` -programsatser, följ proceduren nedan:

1. Lägg till OSGi-konfiguration för fabriks-PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` i en konfigurationsmapp för projektet. Använd ett beskrivande namn för konfigurationen som **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Lägg till `repoinit` -programsatser till egenskapen script för config. Syntaxen och alternativen beskrivs i [Sling-dokumentation](https://sling.apache.org/documentation/bundles/repository-initialization.html). En överordnad mapp bör skapas explicit före de underordnade mapparna. Ett exempel på en explicit skapelse av `/content` före `/content/myfolder`, före `/content/myfolder/mysubfolder`. För åtkomstkontrollistor som ställs in på lågnivåstrukturer bör du ställa in dem på en högre nivå och arbeta med en `rep:glob` begränsning. Till exempel: `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Validera på den lokala utvecklingsmiljön vid körning.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>För åtkomstkontrollistor definierade för noder under `/apps` eller `/libs` den `repoinit`körs körningen i en tom databas. Paketen installeras efter `repoinit` så att programsatser inte kan förlita sig på något som definierats i paketen, utan måste definiera villkoren, som de överordnade strukturerna under.

>[!TIP]
>
>För åtkomstkontrollistor kan det vara besvärligt att skapa djupa strukturer. Därför är det rimligare att definiera en åtkomstkontrollista på en högre nivå och begränsa var den ska agera genom en `rep:glob` begränsning.

Mer information om `repoinit` finns i [Sling-dokumentation](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Package Manager &quot;one offs&quot; för paket med olika innehåll {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Pakethanteraren - migrerar paket med ändringsbart innehåll"
>abstract="Utforska användningen av Package Manager för de användningsområden där ett innehållspaket ska installeras som en av. I installationen ingår att importera specifikt innehåll från produktion till testning för att felsöka ett produktionsproblem, överföra ett litet innehållspaket från en lokal miljö till AEM Cloud-miljöer, med mera."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en" text="Verktyget Innehållsöverföring"

I vissa fall bör ett innehållspaket installeras som en&quot;engångspaket&quot;. Om du till exempel importerar visst innehåll från produktion till mellanlagring felsöker du ett produktionsproblem. För dessa scenarier [Pakethanteraren](/help/implementing/developing/tools/package-manager.md) kan användas i miljöer på AEM as a Cloud Service.

Eftersom Package Manager är ett runtime-koncept går det inte att installera innehåll eller kod i den oföränderliga databasen, så dessa innehållspaket bör endast bestå av ändringsbart innehåll (huvudsakligen `/content` eller `/conf`). Om innehållspaketet innehåller innehåll som är blandat (både muterbart och oföränderligt innehåll) installeras endast det muterbara innehållet.

>[!IMPORTANT]
>
>Pakethanterarens användargränssnitt kan returnera ett **undefined** felmeddelande om ett paket tar längre tid än tio minuter att installera.
>
>Den här tidpunkten beror inte på ett fel i installationen, utan på en timeout som Cloud Servicen har för alla begäranden.
>
>Försök inte installera igen om du ser ett sådant fel. Installationen fortsätter korrekt i bakgrunden. Om du startar om installationen kan vissa konflikter uppstå vid flera samtidiga importprocesser.

Alla innehållspaket som installeras med hjälp av Cloud Manager (både ändringsbart och oföränderligt) visas i ett låst läge i AEM användargränssnitt. Dessa paket kan inte installeras om, byggas om eller laddas ned, och finns listade med en **&quot;cp2fm&quot;** som anger att installationen hanterades av Cloud Manager.

### Inklusive paket från tredje part {#including-third-party}

Det är vanligt att kunder inkluderar färdiga paket från tredjepartskällor som programvaruleverantörer som Adobe översättning partners. Rekommendationen är att lagra dessa paket i en fjärrdatabas och referera till dem i `pom.xml`. Den här metoden är möjlig för offentliga databaser och även för privata databaser med lösenordsskydd, vilket beskrivs i [lösenordsskyddade maven-databaser](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Om det inte går att lagra paketet i en fjärrdatabas kan kunderna placera det i en lokal, filsystemsbaserad Maven-databas som är kopplad till SCM som en del av projektet. Det refereras av det som beror på det. Databasen deklareras i projektsökvägen enligt nedan:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Alla inkluderade tredjepartspaket måste följa AEM riktlinjer för as a Cloud Service kodning och paketering som beskrivs i den här artikeln, annars leder inkludering till ett distributionsfel.

The following Maven `POM.xml` utdrag visar hur tredjepartspaket kan bäddas in i projektets&quot;Behållarpaket&quot;, vanligtvis namngivna **all** genom **filevault-package-maven-plugin** Konfiguration av plugin-programmet Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

## Hur rullande distributioner fungerar {#how-rolling-deployments-work}

Precis som AEM uppdateringar distribueras kundreleaser med hjälp av en strategi för rullande driftsättning för att eliminera driftavbrott i utvecklarkluster under rätt omständigheter. Den allmänna händelsesekvensen beskrivs nedan, där noder med både den gamla och den nya versionen av kundkoden körs i samma version AEM koden.

* Noder med den gamla versionen är aktiva och en release som kan användas för den nya versionen har skapats och blir tillgängliga.
* Om det finns nya eller uppdaterade indexdefinitioner bearbetas motsvarande index. Noder med den gamla versionen använder alltid de gamla indexen, medan noder med den nya versionen alltid använder de nya indexen.
* Nodes med den nya versionen som startats, medan gamla versioner fortfarande betjänar trafiken.
* Noder med den gamla versionen körs och fortsätter att fungera medan noder med den nya versionen kontrolleras för beredskap via hälsokontroller.
* Noder med den nya versionen som är klar, tar emot trafik och ersätter noderna med den gamla versionen som nu visas.
* Med tiden ersätts noderna med den gamla versionen av noderna med den nya versionen tills endast noder med nya versioner finns kvar, vilket slutför distributionen.
* Allt nytt eller ändrat ändringsbart innehåll distribueras sedan.

## Index {#indexes}

Nya eller ändrade index orsakar ett extra indexerings- eller omindexeringssteg innan den nya versionen kan ta över trafik. Information om indexhantering i AEM as a Cloud Service finns i [den här artikeln](/help/operations/indexing.md). Du kan kontrollera indexeringsstatusen för byggsidor i Cloud Manager och få ett meddelande när den nya versionen är klar att börja trafikera.

>[!NOTE]
>
>Den tid som krävs för en rullande distribution varierar beroende på indexets storlek. Orsaken är att den nya versionen inte accepterar trafik förrän det nya indexet genereras.

För närvarande fungerar inte AEM as a Cloud Service med indexhanteringsverktyg som ACS Commons Sörja för att index bryts.

## Replikering {#replication}

Publiceringsfunktionen är bakåtkompatibel med [AEM Replication Java™ API:er](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html).

Om du vill utveckla och testa med replikering med molnklar AEM snabbstart måste du använda de klassiska replikeringsfunktionerna med en författare-/publiceringskonfiguration. Om användargränssnittets startpunkt på AEM Author tas bort för molnet går användarna till `http://localhost:4502/etc/replication` för konfiguration.

## Bakåtkompatibel kod för rullande distributioner {#backwards-compatible-code-for-rolling-deployments}

AEM as a Cloud Service strategi för rullande driftsättning innebär, som beskrivs ovan, att både den gamla och den nya versionen kan användas samtidigt. Var därför försiktig med kodändringar som inte är bakåtkompatibla med den gamla AEM som fortfarande används.

Dessutom bör den gamla versionen testas för kompatibilitet med alla nya muterbara innehållsstrukturer som tillämpas i den nya versionen om det finns en återställning, eftersom muterbart innehåll inte tas bort.

### Tjänstanvändare och ACL-ändringar {#service-users-and-acl-changes}

Om du ändrar tjänstanvändare, eller åtkomstkontrollistor som har åtkomst till innehåll eller kod, kan det leda till fel i de äldre AEM versionerna, vilket leder till åtkomst till innehållet eller koden för de gamla tjänstanvändarna. Rekommendationen är att göra ändringar spridda över minst två versioner, där den första versionen fungerar som en länk innan den rensas i den efterföljande versionen.

### Indexändringar {#index-changes}

Om ändringar görs i index är det viktigt att den nya versionen fortsätter att använda sina index tills den avslutas, medan den gamla versionen använder sin egen ändrade indexuppsättning. Utvecklaren bör följa de tekniker för indexhantering som beskrivs [i den här artikeln](/help/operations/indexing.md).

### Konservativ kodning för återställningar {#conservative-coding-for-rollbacks}

Om ett fel rapporteras eller upptäcks efter distributionen kan det vara nödvändigt att återställa den gamla versionen. Se till att den nya koden är kompatibel med alla nya strukturer som skapas av den nya versionen eftersom de nya strukturerna (allt innehåll som kan ändras) inte återställs. Om den gamla koden inte är kompatibel måste korrigeringar tillämpas i efterföljande kundreleaser.

## Rapid Development Environment (RDE) {#rde}

[Snabba utvecklingsmiljöer](/help/implementing/developing/introduction/rapid-development-environments.md) (eller RDE i korthet) gör det möjligt för utvecklare att snabbt driftsätta och granska ändringar, vilket minimerar den tid som krävs för att testa funktioner som redan har befunnits fungera i en lokal utvecklingsmiljö.

Till skillnad från vanliga utvecklingsmiljöer, som distribuerar kod via molnhanterarens pipeline, använder utvecklare kommandoradsverktyg för att synkronisera kod från en lokal utvecklingsmiljö till den lokala utvecklingsmiljön. När ändringarna har testats i en RDE distribuerar du dem till en vanlig Cloud Development-miljö via Cloud Manager-pipelinen, vilket placerar koden via lämpliga kvalitetsportar.

## Körningslägen {#runmodes}

I befintliga AEM kan kunderna köra instanser med godtyckliga körningslägen och använda OSGI-konfiguration eller installera OSGI-paket för dessa specifika instanser. Körningslägen som är definierade inkluderar *service* (författare och publicera) och miljön (rde, dev, stage, prod).

AEM as a Cloud Service å andra sidan är mer övertygande om vilka körlägen som finns tillgängliga och hur OSGI-paket och OSGI-konfigurationer kan mappas till dem:

* OSGI-konfigurationens körningslägen måste referera till RDE, utveckling, stadium, produktion för miljön eller författaren, publicera för tjänsten. En kombination av `<service>.<environment_type>` stöds, medan dessa miljöer måste användas i just denna ordning (till exempel `author.dev` eller `publish.prod`). OSGI-tokens ska refereras direkt från koden i stället för att använda `getRunModes` som inte längre innehåller `environment_type` vid körning. Mer information finns i [Konfigurera OSGi för AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Körningslägena för OSGI-paket är begränsade till tjänsten (författare, publicera). OSGI-paket per körning ska installeras i innehållspaketet under antingen `install.author` eller `install.publish`.

AEM as a Cloud Service tillåter inte att körningslägen används för att installera innehåll för specifika miljöer eller tjänster. Om en utvecklingsmiljö måste sjösättas med data eller HTML som inte finns i mellanlagrings- eller produktionsmiljöerna kan du använda Package Manager.

De körlägeskonfigurationer som stöds är:

* **config** (*Standardvärdet gäller för alla AEM*)
* **config.author** (*Gäller för alla AEM författartjänster*)
* **config.author.dev** (*Gäller för AEM Dev Author Service*)
* **config.author.rde** (*Gäller AEM RDE Author Service*)
* **config.author.stage** (*Gäller för AEM mellanlagringsförfattartjänst*)
* **config.author.prod** (*Gäller för tjänsten AEM Production Author*)
* **config.publish** (*Gäller AEM Publiceringstjänst*)
* **config.publish.dev** (*Gäller för AEM Dev Publish Service*)
* **config.publish.rde** (*Gäller AEM RDE-publiceringstjänsten*)
* **config.publish.stage** (*Gäller för AEM mellanlagringspubliceringstjänst*)
* **config.publish.prod** (*Gäller för AEM produktionspubliceringstjänst*)
* **config.dev** (*Gäller för AEM Dev-tjänster*)
* **config.rde** (*Gäller RDE-tjänster*)
* **config.stage** (*Gäller för AEM mellanlagringstjänster*)
* **config.prod** (*Gäller AEM produktionstjänster*)

Den OSGI-konfiguration som har de mest matchande körningslägena används.

Vid lokal utveckling, en startparameter för körningsläge, `-r`, används för att ange OSGI-konfigurationen för körningsläge.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Konfiguration av underhållsaktiviteter i källkontroll {#maintenance-tasks-configuration-in-source-control}

Konfigurationer för underhållsaktiviteter måste sparas i källkontrollen eftersom **Verktyg > Åtgärder** skärmen är inte tillgänglig i molnmiljöer. Denna förmån säkerställer att ändringarna sparas avsiktligt i stället för att tillämpas och glöms bort. Se [Underhållsaktivitetsartikel](/help/operations/maintenance.md) om du vill ha mer information.
