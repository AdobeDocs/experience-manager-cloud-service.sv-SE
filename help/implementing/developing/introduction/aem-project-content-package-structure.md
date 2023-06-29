---
title: AEM-projektstruktur
description: Lär dig hur du definierar paketstrukturer för distribution till Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 3%

---

# AEM-projektstruktur

>[!TIP]
>
>Bekanta dig med grundläggande [AEM Project Archetype-användning](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)och [Plugin-programmet FileVault Content Maven](/help/implementing/developing/tools/maven-plugin.md) eftersom den här artikeln bygger på dessa inlärningar och begrepp.

I den här artikeln beskrivs de ändringar som krävs för Adobe Experience Manager Maven-projekt som är AEM as a Cloud Service kompatibla genom att säkerställa att de respekterar uppdelningen av ändringsbart och oföränderligt innehåll. Beroenden skapas också för att skapa icke-konfliktskapande, deterministiska distributioner, och de paketeras i en distributionsbar struktur.

AEM programdistributioner måste bestå av ett enda AEM. Paketet ska i sin tur innehålla delpaket som innehåller allt som krävs för att programmet ska fungera, inklusive kod, konfiguration och allt baslinjeinnehåll som stöds.

AEM kräver separation av **innehåll** och **kod**, vilket innebär ett enda innehållspaket **inte** distribuera till **båda** `/apps` och körningssäkra områden (t.ex. `/content`, `/conf`, `/home`eller något som inte `/apps`) för databasen. Programmet måste i stället separera kod och innehåll i separata paket för distribution till AEM.

Den paketstruktur som beskrivs i det här dokumentet är kompatibel med **både** lokala utvecklingsdistributioner och AEM Cloud Service-distributioner.

>[!TIP]
>
>Konfigurationerna som beskrivs i det här dokumentet tillhandahålls av [AEM Project Maven Archetype 24 eller senare](https://github.com/adobe/aem-project-archetype/releases).

## Mutable kontra Immutable Areas of the Repository {#mutable-vs-immutable}

The `/apps` och `/libs` AEM **oföränderlig** eftersom de inte kan ändras (skapa, uppdatera, ta bort) efter att AEM startats (det vill säga vid körning). Alla försök att ändra ett oföränderligt område vid körning misslyckas.

Allt annat i databasen, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`och så vidare, är alla **mutabel** områden, vilket innebär att de kan ändras under körning.

>[!WARNING]
>
>Precis som i tidigare versioner av AEM `/libs` bör inte ändras. Endast AEM produktkod kan distribueras till `/libs`.

### Oak Index {#oak-indexes}

Oak indexes (`/oak:index`) hanteras av den AEM as a Cloud Service distributionsprocessen. Orsaken är att Cloud Manager måste vänta tills ett nytt index har distribuerats och indexerats om fullständigt innan det går över till den nya kodbilden.

Därför måste Oak-index, även om de kan ändras vid körning, distribueras som kod så att de kan installeras innan några ändringsbara paket installeras. Därför `/oak:index` konfigurationer är en del av kodpaketet och inte en del av innehållspaketet [enligt nedan](#recommended-package-structure).

>[!TIP]
>
>Mer information om indexering på AEM as a Cloud Service finns i [Innehållssökning och indexering](/help/operations/indexing.md).

## Rekommenderad paketstruktur {#recommended-package-structure}

![Experience Manager projektpaketstruktur](assets/content-package-organization.png)

I det här diagrammet visas en översikt över den rekommenderade projektstrukturen och artefakter för paketdistribution.

Den rekommenderade programdistributionsstrukturen är följande:

### Kodpaket / OSGi Bundles

+ OSGi-paketfilen genereras och bäddas in direkt i hela projektet.

+ The `ui.apps` paketet innehåller all kod som ska distribueras och endast distribueras till `/apps`. Vanliga element i `ui.apps` paketet innehåller, men är inte begränsat till:
   + [Komponentdefinitioner och HTML](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) skript
      + `/apps/my-app/components`
   + JavaScript och CSS (via [Klientbibliotek](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Övertäckningar](/help/implementing/developing/introduction/overlays.md) av `/libs`
      + `/apps/cq`, `/apps/dam/`och så vidare.
   + Kontextmedvetna reservkonfigurationer
      + `/apps/settings`
   + ACL-listor (behörigheter)
      + Alla `rep:policy` för alla banor under `/apps`
   + [Förkompilerade paketerade skript](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>Samma kod måste distribueras till alla miljöer. Den här koden säkerställer att valideringar i scenmiljön också är i produktion. Mer information finns i avsnittet om [Runmodes](/help/implementing/deploying/overview.md#runmodes).


### Innehållspaket

+ The `ui.content` paketet innehåller allt innehåll och all konfiguration. Innehållspaketet innehåller alla noddefinitioner som inte finns i `ui.apps` eller `ui.config` paket, med andra ord, ingenting i `/apps` eller `/oak:index`. Vanliga element i `ui.content` paketet innehåller, men är inte begränsat till:
   + Kontextmedvetna konfigurationer
      + `/conf`
   + Nödvändiga, komplexa innehållsstrukturer (d.v.s. innehållsbygge som bygger på och sträcker sig utanför de ursprungliga innehållsstrukturer som definierats i Repo Init).
      + `/content`, `/content/dam`och så vidare.
   + Styrda taggar för taxonomier
      + `/content/cq:tags`
   + Äldre noder (helst migrera dessa noder till platser som inte är-/osv.)
      + `/etc`

### Behållarpaket

+ The `all` paketet är ett behållarpaket som ENDAST innehåller installerbara artefakter, den oSGI-paketerade JAR-filen, `ui.apps`, `ui.config`och `ui.content` paket som inbäddade. The `all` paketet får inte ha **allt innehåll och all kod** själva, men delegera i stället all distribution till databasen till dess underpaket eller till OSGi bundle Jar-filer.

  Paket ingår nu i Maven [Inbäddad konfiguration för plugin-programmet FileVault Package Maven](#embeddeds)i stället för `<subPackages>` konfiguration.

  För komplexa Experience Manager-distributioner kan det vara önskvärt att skapa flera `ui.apps`, `ui.config`och `ui.content` projekt/paket som representerar specifika webbplatser eller klientorganisationer i AEM. Om du väljer det här sättet ska du se till att delningen mellan ändringsbart och oföränderligt innehåll respekteras och att de nödvändiga innehållspaketen och OSGi-paketerade JAR-filer bäddas in som delpaket i `all` behållarinnehållspaket.

  En innehållsstruktur för en komplex distribution kan till exempel se ut så här:

   + `all` innehållspaketet bäddar in följande paket för att skapa en enda distributionsartefakt
      + `common.ui.apps` distribuerar kod som krävs av **båda** plats A och plats B
      + `site-a.core` OSGi bundle Jar krävs av webbplats A
      + `site-a.ui.apps` distribuerar kod som krävs av plats A
      + `site-a.ui.config` distribuerar OSGi-konfigurationer som krävs av plats A
      + `site-a.ui.content` distribuerar innehåll och konfiguration som krävs av plats A
      + `site-b.core` OSGi bundle Jar krävs av webbplats B
      + `site-b.ui.apps` distribuerar kod som krävs av plats B
      + `site-b.ui.config` distribuerar OSGi-konfigurationer som krävs av plats B
      + `site-b.ui.content` distribuerar innehåll och konfiguration som krävs av plats B

+ The `ui.config` paketet innehåller alla [OSGi-konfigurationer](/help/implementing/deploying/configuring-osgi.md):
   + Betraktad kod och hör till OSGi-paket, men innehåller inte vanliga innehållsnoder. Därför markeras det som ett behållarpaket
   + Organisationsmapp som innehåller körlägesspecifika OSGi-konfigurationsdefinitioner
      + `/apps/my-app/osgiconfig`
   + Vanlig OSGi-konfigurationsmapp som innehåller standardkonfigurationer för OSGi som gäller för alla mål AEM as a Cloud Service distributionsmål
      + `/apps/my-app/osgiconfig/config`
   + Kör lägesspecifika OSGi-konfigurationsmappar som innehåller standardkonfigurationer för OSGi som gäller för alla mål AEM as a Cloud Service distributionsmål
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi-konfigurationsskript
      + [Repo Init](#repo-init) är det rekommenderade sättet att distribuera (ändringsbart) innehåll som logiskt är en del av AEM. Repo Init OSGi-konfigurationerna ska vara platser i lämpliga `config.<runmode>` enligt ovan och användas för att definiera:
         + Baslinjeinnehållsstrukturer
         + Användare
         + Tjänstanvändare
         + Grupper
         + ACL-listor (behörigheter)

### Extra programpaket{#extra-application-packages}

Om andra AEM-projekt, som i sig själva består av sina egna kod- och innehållspaket, används av den AEM distributionen, bör deras behållarpaket bäddas in i projektets `all` paket.

Ett AEM projekt som innehåller två AEM program kan se ut så här:

+ `all` innehållspaketet bäddar in följande paket för att skapa en enda distributionsartefakt
   + `core` OSGi bundle Jar krävs av AEM
   + `ui.apps` distribuerar kod som krävs av AEM
   + `ui.config` distribuerar OSGi-konfigurationer som krävs av AEM
   + `ui.content` distribuerar innehåll och konfiguration som krävs för AEM
   + `vendor-x.all` distribuerar allt (kod och innehåll) som krävs av X-leverantörens program
   + `vendor-y.all` distribuerar allt (kod och innehåll) som krävs av leverantörens Y-program

## Pakettyper {#package-types}

Paket ska märkas med sin deklarerade pakettyp. Pakettyper gör det lättare att klargöra syftet med och distributionen av ett paket.

+ Behållarpaket måste ange sina `packageType` till `container`. Behållarpaket får inte innehålla vanliga noder. Endast OSGi-paket, konfigurationer och underpaket tillåts. Behållare i AEM as a Cloud Service får inte användas [installera kopplingar](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Kodpaket (ej ändringsbara) måste ange sina `packageType` till `application`.
+ Innehållspaket (mutable) måste ange sina `packageType` till `content`.


Mer information finns i [Apache Jackrabbit FileVault - dokumentation för Plugin-programmet Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Pakettyper för Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html)och [FileVault Maven-konfigurationsfragment](#marking-packages-for-deployment-by-adoube-cloud-manager) nedan.

>[!TIP]
>
>Se [POM XML-kodfragment](#xml-package-types) nedan om du vill ha ett fullständigt kodfragment.

## Markera paket för distribution med Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Som standard hämtar Adobe Cloud Manager alla paket som skapats av Maven-bygget. Men eftersom behållaren (`all`) är den enda distributionsartefakten som innehåller all kod och alla innehållspaket. Du måste se till att **endast** behållaren (`all`) distribueras. För att säkerställa detta måste andra paket som genereras av Maven-bygget markeras med FileVaults Maven-pluginkonfiguration `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` för innehållspaket.

>[!TIP]
>
>Se [POM XML-kodfragment](#pom-xml-snippets) nedan om du vill ha ett fullständigt kodfragment.

## Repo Init{#repo-init}

Repo Init innehåller instruktioner, eller skript, som definierar JCR-strukturer, från vanliga nodstrukturer som mappträd till användare, tjänstanvändare, grupper och ACL-definition.

De viktigaste fördelarna med Repo Init är att de har implicit behörighet att utföra alla åtgärder som definieras av deras skript. Sådana skript anropas tidigt under driftsättningens livscykel för att säkerställa att alla nödvändiga JCR-strukturer finns när tidskoden körs.

Medan Repo Init-skripten finns i `ui.config` -projekt som skript, kan och bör användas för att definiera följande muterbara strukturer:

+ Baslinjeinnehållsstrukturer
+ Tjänstanvändare
+ Användare
+ Grupper
+ ACL

Repo Init-skript lagras som `scripts` poster i `RepositoryInitializer` OSGi-fabrikskonfigurationer. Därför kan de vara implicit inriktade på körning, vilket möjliggör skillnader mellan AEM Author och AEM Publish Services Repo Init-skript, eller till och med mellan miljöer (Dev, Stage och Prod).

Repo Init OSGi-konfigurationer skrivs bäst i [`.config` Konfigurationsformat för OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) eftersom de har stöd för flera rader, vilket är ett undantag till de bästa sätten att använda [`.cfg.json` för att definiera OSGi-konfigurationer](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

När du definierar användare och grupper betraktas bara grupper som en del av programmet och de är integrerade i dess funktion. Du definierar fortfarande användare och grupper för organisation vid körning i AEM. Om ett anpassat arbetsflöde till exempel tilldelar arbete till en namngiven grupp, definierar du den gruppen med hjälp av Repo Init i AEM. Men om grupperingen bara är organisatorisk, till exempel&quot;Wendy&#39;s Team&quot; och&quot;Sean&#39;s Team&quot;, är de här grupperna bäst definierade och hanterade vid körning i AEM.

>[!TIP]
>
>Repo Init-skript *måste* definieras i den infogade `scripts` eller `references` fungerar inte.

Det fullständiga språket för Repo Init-skript finns på [Dokumentation för Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Se [Repo Init-fragment](#snippet-repo-init) nedan om du vill ha ett fullständigt kodfragment.

## Databasstrukturpaket {#repository-structure-package}

Kodpaket kräver att konfigurationen för plugin-programmet FileVault Maven konfigureras för att referera till en `<repositoryStructurePackage>` som kräver att strukturella beroenden är korrekta (för att säkerställa att ett kodpaket inte installeras över ett annat). Du kan [skapa ett eget strukturpaket för databasen för ditt projekt](repository-structure-package.md).

**Endast obligatoriskt** för kodpaket, det vill säga paket som är märkta med `<packageType>application</packageType>`.

Mer information om hur du skapar ett databasstrukturpaket för ditt program finns i [Utveckla ett databasstrukturpaket](repository-structure-package.md).

Innehållspaket (`<packageType>content</packageType>`) **inte** kräver det här strukturpaketet för databasen.

>[!TIP]
>
>Se [POM XML-kodfragment](#xml-repository-structure-package) nedan om du vill ha ett fullständigt kodfragment.

## Bädda in delpaket i behållarpaketet{#embeddeds}

Innehåll eller kodpaket placeras i en speciell &quot;side-car&quot;-mapp och kan installeras antingen AEM författare, AEM publicering eller båda med hjälp av plugin-programmet FileVault Maven `<embeddeds>` konfiguration. Använd inte `<subPackages>` konfiguration.

Vanliga användningsfall är:

+ Behörighetslistor/behörigheter som skiljer sig åt mellan AEM författaranvändare och AEM publiceringsanvändare
+ Konfigurationer som används för att stödja aktiviteter endast för AEM författare
+ Kod som integreringar med back-office-system som bara krävs för att köras av AEM

![Bädda in paket](assets/embeddeds.png)

Om du vill ange AEM författare, AEM publicera eller båda, är paketet inbäddat i `all` behållarpaket i en speciell mappsökväg, i följande format:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Bryter ned den här mappstrukturen:

+ Den första nivåmappen **måste vara** `/apps`.
+ Mappen på den andra nivån representerar programmet med `-packages` efter korrigering till mappnamnet. Det finns ofta bara en mapp på andra nivån som alla underpaket är inbäddade i, men hur många mappar på andra nivån som helst kan skapas för att bäst representera programmets logiska struktur:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >Delpaketets inbäddade mappar namnges som suffix till `-packages`. Detta namn säkerställer att distributionskoden och innehållspaketen **not** distribuerade målmapparna för alla underpaket `/apps/<app-name>/...`  vilket leder till destruktiv och cyklisk installation.

+ Mappen på den tredje nivån måste vara antingen
  `application`, `content` eller `container`
   + The `application` mapp innehåller kodpaket
   + The `content` mapp innehåller innehållspaket
   + The `container` mappen innehåller alla [extra programpaket](#extra-application-packages) som kan ingå i AEM.
Mappnamnet motsvarar [pakettyper](#package-types) av de paket som den innehåller.
+ Mappen på den fjärde nivån innehåller underpaketen och måste vara någon av:
   + `install` så du kan installera på **båda** AEM författare och AEM publicera
   + `install.author` så att du kan installera **endast** AEM
   + `install.publish` så att du kan installera **endast** endast AEM `install.author` och `install.publish` är mål som stöds. Andra körningslägen **stöds inte**.

En distribution som innehåller AEM författare och publicerar specifika paket kan till exempel se ut så här:

+ `all` Behållarpaket bäddar in följande paket för att skapa en enda distributionsartefakt
   + `ui.apps` inbäddad i `/apps/my-app-packages/application/install` distribuerar kod till både AEM författare och AEM publicera
   + `ui.apps.author` inbäddad i `/apps/my-app-packages/application/install.author` distribuerar kod till endast AEM författare
   + `ui.content` inbäddad i `/apps/my-app-packages/content/install` distribuerar innehåll och konfiguration till både AEM författare och AEM publicera
   + `ui.content.publish` inbäddad i `/apps/my-app-packages/content/install.publish` distribuerar innehåll och konfiguration till endast AEM publicera

>[!TIP]
>
>Se [POM XML-kodfragment](#xml-embeddeds) nedan om du vill ha ett fullständigt kodfragment.

### Behållarpaketets filterdefinition {#container-package-filter-definition}

På grund av inbäddningen av kod- och innehållsunderpaket i behållarpaketet måste de inbäddade målsökvägarna läggas till i behållarprojektets `filter.xml`. Detta säkerställer att de inbäddade paketen inkluderas i behållarpaketet när de byggs.

Lägg bara till `<filter root="/apps/<my-app>-packages"/>` poster för mappar på andra nivån som innehåller underpaket som ska distribueras.

>[!TIP]
>
>Se [POM XML-kodfragment](#xml-container-package-filters) nedan om du vill ha ett fullständigt kodfragment.

## Bädda in paket från tredje part {#embedding-3rd-party-packages}

Alla paket måste vara tillgängliga via [Adobe allmänna Maven-arkivet](https://repo1.maven.org/maven2/com/adobe/) eller en tillgänglig, refererbar tredjepartsdatabas för Maven-felaktigheter.

Om tredjepartspaketen finns i **Adobe allmänna Maven-arkivet** behövs ingen ytterligare konfiguration för att Adobe Cloud Manager ska kunna lösa artefakterna.

Om tredjepartspaketen finns i en **offentlig databas för Maven-felaktigheter från tredje part** måste den här databasen registreras i projektets `pom.xml` och inbäddad med metoden [ovan](#embeddeds).

Tredjepartsprogram/-anslutningar bör bäddas in med dess `all` paket som en behållare i projektbehållaren (`all`).

Att lägga till Maven-beroenden följer Maven-standardpraxis, och inbäddning av tredjepartsartefakter (kod och innehållspaket) är [ovan](#embedding-3rd-party-packages).

>[!TIP]
>
>Se [POM XML-kodfragment](#xml-3rd-party-maven-repositories) nedan om du vill ha ett fullständigt kodfragment.

## Paketberoenden mellan `ui.apps` från `ui.content` Paket {#package-dependencies}

För att paketen ska kunna installeras på rätt sätt rekommenderar vi att du skapar beroenden mellan paket.

Den allmänna regeln är paket som innehåller ändringsbart innehåll (`ui.content`) ska vara beroende av den oföränderliga koden (`ui.apps`) som har stöd för återgivning och användning av det ändringsbara innehållet.

Ett betydande undantag från den här allmänna regeln är om det oföränderliga kodpaketet (`ui.apps` eller något annat), __endast__ innehåller OSGi-paket. I så fall ska inget AEM deklarera ett beroende av det. Orsaken är att oföränderliga kodpaket som __endast__ innehåller OSGi-paket, som inte är registrerade med AEM [Pakethanteraren](/help/implementing/developing/tools/package-manager.md). Alla AEM som är beroende av paketet är därför inte beroende av och kan inte installeras.

>[!TIP]
>
>Se [POM XML-kodfragment](#xml-package-dependencies) nedan om du vill ha ett fullständigt kodfragment.

De vanligaste mönstren för innehållspaketberoenden är:

### Enkla distributionspaketberoenden {#simple-deployment-package-dependencies}

Det enkla skiftläget anger `ui.content` varierbart innehållspaket som är beroende av `ui.apps` oföränderligt kodpaket.

+ `all` har inga beroenden
   + `ui.apps` har inga beroenden
   + `ui.content` är beroende av `ui.apps`

### Komplexa distributionspaketberoenden {#complex-deploxment-package-dependencies}

Komplexa driftsättningar bygger vidare på det enkla fallet och ställer in beroenden mellan motsvarande muterbara innehåll och oföränderliga kodpaket. Om det behövs kan beroenden etableras även mellan oföränderliga kodpaket.

+ `all` har inga beroenden
   + `common.ui.apps.common` har inga beroenden
   + `site-a.ui.apps` är beroende av `common.ui.apps`
   + `site-a.ui.content` är beroende av `site-a.ui.apps`
   + `site-b.ui.apps` är beroende av `common.ui.apps`
   + `site-b.ui.content` är beroende av `site-b.ui.apps`

## Lokal utveckling och driftsättning {#local-development-and-deployment}

De projektstrukturer och den organisation som beskrivs i den här artikeln är **fullständigt kompatibel** lokala AEM.

## POM XML-kodfragment {#pom-xml-snippets}

Följande är Maven `pom.xml` konfigurationsksnuttar som kan läggas till i Maven-projekt för att anpassas till ovanstående rekommendationer.

### Pakettyper {#xml-package-types}

Kod- och innehållspaket, som distribueras som underpaket, måste deklarera en pakettyp för **program** eller **innehåll**, beroende på vad de innehåller.

#### Behållarpakettyper {#container-package-types}

Behållaren `all/pom.xml` projekt **inte** deklarera `<packageType>`.

#### Kodpakettyper (ej ändringsbara) {#immutable-package-types}

Kodpaket måste ange sina `packageType` till `application`.

I `ui.apps/pom.xml`, `<packageType>application</packageType>` bygg konfigurationsdirektiv för `filevault-package-maven-plugin` plugin-deklarationen deklarerar pakettypen.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.apps</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### Pakettyper för innehåll (ändringsbart) {#mutable-package-types}

Innehållspaket måste ange sina `packageType` till `content`.

I `ui.content/pom.xml`, `<packageType>content</packageType>` byggkonfigurationsdirektivet för `filevault-package-maven-plugin` plugin-deklarationen deklarerar pakettypen.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Markera paket för distribution av Adobe Cloud Manager {#cloud-manager-target}

I alla projekt som genererar ett paket, **utom** för behållarprojektet (`all`), lägger du till `<cloudManagerTarget>none</cloudManagerTarget>` i `<properties>`-konfigurationen för plugin-deklarationen `filevault-package-maven-plugin` för att vara säker på att de **inte** distribueras av Adobe Cloud Manager. Behållaren (`all`) ska vara det fristående paket som distribueras via Cloud Manager, som i sin tur bäddar in all kod och alla innehållspaket som krävs.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Repo Init{#snippet-repo-init}

Repo Init-skript som innehåller Repo Init-skript definieras i `RepositoryInitializer` OSGi-fabrikskonfiguration via `scripts` -egenskap. Eftersom dessa skript definieras i OSGi-konfigurationer kan de enkelt omfångas i körningsläge med hjälp av de vanliga `../config.<runmode>` mappsemantik.

Eftersom skript vanligtvis är flerradsdeklarationer är det enklare att definiera dem i `.config` -filen, än den JSON-baserade `.cfg.json` format.

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

The `scripts` OSGi-egenskapen innehåller direktiv enligt definitionen i [Apache Sling&#39;s Repo Init language](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Databasstrukturpaket {#xml-repository-structure-package}

I `ui.apps/pom.xml` och andra `pom.xml` som deklarerar ett kodpaket (`<packageType>application</packageType>`) lägger du till följande konfiguration av databasstrukturpaket i plugin-programmet FileVault Maven. Du kan [skapa ett eget strukturpaket för databasen för ditt projekt](repository-structure-package.md).

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### Bädda in delpaket i behållarpaketet {#xml-embeddeds}

I `all/pom.xml`lägger du till följande `<embeddeds>` direktiv till `filevault-package-maven-plugin` plugin-deklaration. Kom ihåg: **inte** använder `<subPackages>` konfiguration. Orsaken är att den inkluderar delpaketen i `/etc/packages` i stället för `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

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

### Behållarpaketets filterdefinition {#xml-container-package-filters}

I `all` projekt `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **include** alla `-packages` mappar som innehåller underpaket att distribuera:

```xml
<filter root="/apps/my-app-packages"/>
```

Om flera `/apps/*-packages` används i de inbäddade målen, måste alla räknas upp här.

### Maven Repositories från tredje part {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Om du lägger till fler Maven-databaser kan det ta längre tid att bygga maven när ytterligare Maven-databaser kontrolleras för beroenden.

I reaktorprojektets `pom.xml`, lägger du till alla nödvändiga direktiv från tredjepartsdatabasen för Maven. Den fullständiga `<repository>` -konfigurationen bör vara tillgänglig från tredjepartsprovidern för databas.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public Third-Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### Paketberoenden mellan `ui.apps` från `ui.content` Paket {#xml-package-dependencies}

I `ui.content/pom.xml`lägger du till följande `<dependencies>` direktiv till `filevault-package-maven-plugin` plugin-deklaration.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### Rensa behållarprojektets målmapp {#xml-clean-container-package}

I `all/pom.xml`, lägg till `maven-clean-plugin` plugin-program som rensar målkatalogen före Maven-bygget.

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## Ytterligare resurser {#additional-resources}

+ [Hantera paket med Maven](/help/implementing/developing/tools/maven-plugin.md)
+ [Plugin-programmet FileVault Content Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
