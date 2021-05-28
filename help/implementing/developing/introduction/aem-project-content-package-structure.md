---
title: AEM-projektstruktur
description: Lär dig hur du definierar paketstrukturer för distribution till Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2869'
ht-degree: 12%

---

# AEM-projektstruktur

>[!TIP]
>
>Bekanta dig med grundläggande [AEM Project Archetype-användning](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) och [FileVault Content Maven-plugin](/help/implementing/developing/tools/maven-plugin.md) när den här artikeln bygger på dessa inlärningar och koncept.

I den här artikeln beskrivs de ändringar som krävs för Adobe Experience Manager Maven-projekt som ska AEM som en Cloud Service-kompatibel genom att säkerställa att de respekterar uppdelningen av muterbart och oföränderligt innehåll, att beroenden etableras för att skapa icke-konfliktskapande, deterministiska distributioner och att de paketeras i en installerbar struktur.

AEM programdistributioner måste bestå av ett enda AEM. Paketet ska i sin tur innehålla underpaket som innehåller allt som programmet behöver för att fungera, inklusive kod, konfiguration och eventuellt baslinjeinnehåll som stöds.

AEM kräver att **innehåll** och **kod** skiljs åt, vilket innebär att ett innehållspaket **inte** kan distribueras till **både** `/apps` och områden som är skrivbara vid körning (som `/content`, `/conf`, `/home`eller allt som inte är `/apps`) i databasen. Programmet måste i stället separera kod och innehåll i separata paket för distribution till AEM.

Den paketstruktur som beskrivs i det här dokumentet är kompatibel med **både** lokala utvecklingsdistributioner och AEM Cloud Service-distributioner.

>[!TIP]
>
>Konfigurationerna som beskrivs i det här dokumentet tillhandahålls av [AEM Project Maven Archetype 24 eller senare](https://github.com/adobe/aem-project-archetype/releases).

## Muterbara kontra oföränderliga områden i databasen {#mutable-vs-immutable}

`/apps` och `/libs`**betraktas som oföränderliga områden i AEM, eftersom de inte kan ändras (skapa, uppdatera, ta bort) efter att AEM startats (dvs. vid körning).** Alla försök att ändra ett oföränderligt område vid körning misslyckas.

Allt annat i databasen, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp` osv. är alla **ändringsbara** områden, vilket innebär att de kan ändras under körning.

>[!WARNING]
>
>Precis som i tidigare versioner av AEM ska `/libs` inte ändras. Endast AEM produktkod kan distribueras till `/libs`.

### Oak Indexes {#oak-indexes}

Oak-index (`/oak:index`) hanteras specifikt av AEM som en distributionsprocess för Cloud Service. Detta beror på att Cloud Manager måste vänta tills ett nytt index har distribuerats och indexerats om fullständigt innan det går över till den nya kodbilden.

Därför måste Oak-index, även om de kan ändras vid körning, distribueras som kod så att de kan installeras innan några ändringsbara paket installeras. Därför är `/oak:index`-konfigurationer en del av kodpaketet och inte en del av innehållspaketet [enligt beskrivningen nedan](#recommended-package-structure).

>[!TIP]
>
>Mer information om hur du indexerar AEM som en Cloud Service finns i dokumentet [Innehållssökning och indexering](/help/operations/indexing.md).

## Rekommenderad paketstruktur {#recommended-package-structure}

![Experience Manager projektpaketstruktur](assets/content-package-organization.png)

I det här diagrammet visas en översikt över den rekommenderade projektstrukturen och artefakter för paketdistribution.

Den rekommenderade programdistributionsstrukturen är följande:

### Kodpaket / OSGi Bundles

+ OSGi-paketfilen genereras och bäddas in direkt i hela projektet.

+ Paketet `ui.apps` innehåller all kod som ska distribueras och endast distribueras till `/apps`. Vanliga element i `ui.apps`-paketet omfattar, men är inte begränsade till:
   + [Komponentdefinitioner och ](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html) HTLscripts
      + `/apps/my-app/components`
   + JavaScript och CSS (via [Klientbibliotek](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Överlappningar ](/help/implementing/developing/introduction/overlays.md) av  `/libs`
      + `/apps/cq`,  `/apps/dam/`osv.
   + Kontextmedvetna reservkonfigurationer
      + `/apps/settings`
   + ACL-listor (behörigheter)
      + Valfri `rep:policy` för alla sökvägar under `/apps`

+ Paketet `ui.config` innehåller alla [OSGi-konfigurationer](/help/implementing/deploying/configuring-osgi.md):
   + Organisationsmapp som innehåller körlägesspecifika OSGi-konfigurationsdefinitioner
      + `/apps/my-app/osgiconfig`
   + Vanlig OSGi-konfigurationsmapp som innehåller standardOSGi-konfigurationer som gäller för alla AEM som mål för Cloud Service-distribution
      + `/apps/my-app/osgiconfig/config`
   + Kör lägesspecifika OSGi-konfigurationsmappar som innehåller standardkonfigurationer för OSGi som gäller för alla AEM som Cloud Servicens distributionsmål
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi-konfigurationsskript
      + [Repo ](#repo-init) Init är det rekommenderade sättet att distribuera (muterbart) innehåll som logiskt är en del av AEM. Repo Init OSGi-konfigurationerna ska placeras i lämplig `config.<runmode>`-mapp enligt ovan och användas för att definiera:
         + Baslinjeinnehållsstrukturer
         + Användare
         + Tjänstanvändare
         + Grupper
         + ACL-listor (behörigheter)

>[!NOTE]
>
>Samma kod måste distribueras till alla miljöer. Detta är nödvändigt för att säkerställa en nivå av konfidensvalidering i scenmiljön som också är i produktion. Mer information finns i avsnittet [Runmodes](/help/implementing/deploying/overview.md#runmodes).


### Innehållspaket

+ Paketet `ui.content` innehåller allt innehåll och all konfiguration. Innehållspaketet innehåller alla noddefinitioner som inte finns i `ui.apps`- eller `ui.config`-paketen, eller med andra ord något som inte finns i `/apps` eller `/oak:index`. Vanliga element i `ui.content`-paketet omfattar, men är inte begränsade till:
   + Kontextmedvetna konfigurationer
      + `/conf`
   + Nödvändiga, komplexa innehållsstrukturer (t.ex. Innehållsbygge som bygger på och sträcker sig förbi innehållsstrukturer för baslinjen som definierats i Repo Init.)
      + `/content`,  `/content/dam`osv.
   + Styrda taggar för taxonomier
      + `/content/cq:tags`
   + Äldre noder (helst migrera dessa till platser som inte är/osv.)
      + `/etc`

### Behållarpaket

+ Paketet `all` är ett behållarpaket som ENDAST innehåller distribuerbara artefakter, den OSGI-paketerade JAR-filen, `ui.apps`, `ui.config` och `ui.content`-paket som inbäddade. `all`-paketet får inte ha **något eget innehåll eller någon egen kod**, utan delegera all distribution till databasen till dess underpaket eller OSGi buntfiler i JAR.

   Paket ingår nu med Maven [FileVault Package Maven-pluginens inbäddade konfiguration](#embeddeds), i stället för `<subPackages>`-konfigurationen.

   För komplexa Experience Manager-distributioner kan det vara önskvärt att skapa flera `ui.apps`-, `ui.config`- och `ui.content`-projekt/paket som representerar specifika webbplatser eller klientorganisationer i AEM. Om detta görs ser du till att delningen mellan ändringsbart och ej ändringsbart innehåll respekteras och att de nödvändiga innehållspaketen och OSGi-paketerade JAR-filer bäddas in som underpaket i `all`-behållarinnehållspaketet.

   En innehållsstruktur för en komplex distribution kan till exempel se ut så här:

   + `all` innehållspaketet bäddar in följande paket för att skapa en enda distributionsartefakt
      + `common.ui.apps` distribuerar kod som krävs av både  **** plats A och plats B
      + `site-a.core` OSGi bundle Jar krävs av webbplats A
      + `site-a.ui.apps` distribuerar kod som krävs av plats A
      + `site-a.ui.config` distribuerar OSGi-konfigurationer som krävs av plats A
      + `site-a.ui.content` distribuerar innehåll och konfiguration som krävs av plats A
      + `site-b.core` OSGi bundle Jar krävs av webbplats B
      + `site-b.ui.apps` distribuerar kod som krävs av plats B
      + `site-b.ui.config` distribuerar OSGi-konfigurationer som krävs av plats B
      + `site-b.ui.content` distribuerar innehåll och konfiguration som krävs av plats B

### Extra programpaket{#extra-application-packages}

Om andra AEM-projekt, som i sig själva består av sina egna kod- och innehållspaket, används av den AEM distributionen, bör deras behållarpaket bäddas in i projektets `all`-paket.

Ett AEM projekt som innehåller 2 AEM program kan se ut så här:

+ `all` innehållspaketet bäddar in följande paket för att skapa en enda distributionsartefakt
   + `core` OSGi bundle Jar krävs av AEM
   + `ui.apps` distribuerar kod som krävs av AEM
   + `ui.config` distribuerar OSGi-konfigurationer som krävs av AEM
   + `ui.content` distribuerar innehåll och konfiguration som krävs för AEM
   + `vendor-x.all` distribuerar allt (kod och innehåll) som krävs av X-leverantörens program
   + `vendor-y.all` distribuerar allt (kod och innehåll) som krävs av leverantörens Y-program

## Pakettyper {#package-types}

Paket ska märkas med sin deklarerade pakettyp.

+ Behållarpaket måste ange `packageType` som `container`. Behållarpaket får inte innehålla OSGi-paket, OSGi-konfigurationer och får inte använda [installationsnätverk](http://jackrabbit.apache.org/filevault/installhooks.html).
+ Kodpaket (ej ändringsbart) måste ange `packageType` som `application`.
+ Innehållspaket (mutable) måste ange `packageType` som `content`.


Mer information finns i [dokumentationen till Apache Jackrabbit FileVault - Package Maven Plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) och [konfigurationsfragmentet för FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) nedan.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-package-types) nedan för ett fullständigt kodfragment.

## Markera paket för distribution av Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Som standard hämtar Adobe Cloud Manager alla paket som skapas av Maven-bygget, men eftersom behållarpaketet (`all`) är en enda distributionsartefakt som innehåller all kod och alla innehållspaket måste vi se till att **endast** behållarpaketet (`all`) distribueras. För att säkerställa detta måste andra paket som genereras av Maven-bygget markeras med FileVaults Maven-pluginkonfiguration `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` för innehållspaket.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#pom-xml-snippets) nedan för ett fullständigt kodfragment.

## Repo Init{#repo-init}

Repo Init innehåller instruktioner, eller skript, som definierar JCR-strukturer, från vanliga nodstrukturer som mappträd till användare, tjänstanvändare, grupper och ACL-definition.

De viktigaste fördelarna med Repo Init är att de har implicit behörighet att utföra alla åtgärder som definieras av deras skript, och att de anropas tidigt under distributionens livscykel för att säkerställa att alla nödvändiga JCR-strukturer finns när koden körs.

Medan Repo Init-skripten i sig själva finns i `ui.config`-projektet som skript, kan och bör de användas för att definiera följande muterbara strukturer:

+ Baslinjeinnehållsstrukturer
+ Tjänstanvändare
+ Användare
+ Grupper
+ ACL

Repo Init-skript lagras som `scripts`-poster för `RepositoryInitializer` OSGi-fabrikskonfigurationer och kan därför implicit användas i körläge, vilket möjliggör skillnader mellan AEM Author och AEM Publish Services Repo Init-skript, eller till och med mellan miljöer (Dev, Stage och Prod).

Repo Init OSGi-konfigurationer skrivs bäst i [`.config` OSGi-konfigurationsformatet](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) eftersom de stöder flera rader, vilket är ett undantag till de bästa sätten att använda [`.cfg.json` för att definiera OSGi-konfigurationer](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Observera, att när du definierar Användare, och Grupper, anses bara grupper vara en del av programmet, och att de är en del av dess funktion bör definieras här. Organisationens användare och grupper bör fortfarande definieras vid körning i AEM. Om ett anpassat arbetsflöde till exempel tilldelar arbete till en namngiven grupp, bör den gruppen definieras i via Repo Init i AEM, men om grupperingen bara är organisatorisk, till exempel&quot;Wendy&#39;s Team&quot; och&quot;Sean&#39;s Team&quot;, är dessa bäst definierade och hanteras vid körning i AEM.

>[!TIP]
>
>Repo Init-skript *måste* definieras i det infogade `scripts`-fältet och `references`-konfigurationen fungerar inte.

Den fullständiga ordlistan för Repo Init-skript finns i [dokumentationen för Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Se avsnittet [Kodfragment för initiering av repo](#snippet-repo-init) nedan för ett fullständigt kodfragment.

## Databasstrukturpaket {#repository-structure-package}

Kodpaket kräver att konfigurationen för plugin-programmet FileVault Maven konfigureras så att den refererar till en `<repositoryStructurePackage>` som kräver att strukturella beroenden är korrekta (för att säkerställa att ett kodpaket inte installeras över ett annat). Du kan [skapa ett eget databasstrukturpaket för ditt projekt](repository-structure-package.md).

Detta **krävs endast** för kodpaket, vilket innebär alla paket som är markerade med `<packageType>application</packageType>`.

Mer information om hur du skapar ett databasstrukturpaket för programmet finns i [Utveckla ett databasstrukturpaket](repository-structure-package.md).

Observera att innehållspaket (`<packageType>content</packageType>`) **inte** kräver det här databasstrukturpaketet.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-repository-structure-package) nedan för ett fullständigt kodfragment.

## Bädda in underpaket i behållarpaketet{#embeddeds}

Innehåll eller kodpaket placeras i en speciell &quot;side-car&quot;-mapp och kan användas för installation på antingen AEM författare, AEM publicering eller båda med hjälp av plugin-programmet FileVault Maven `<embeddeds>`-konfigurationen. Observera att `<subPackages>`-konfigurationen inte bör användas.

Vanliga användningsfall är:

+ Behörighetslistor/behörigheter som skiljer sig åt mellan AEM författaranvändare och AEM publiceringsanvändare
+ Konfigurationer som används för att stödja aktiviteter endast för AEM författare
+ Kod som integreringar med back-office-system som bara krävs för att köras av AEM

![Bädda in paket](assets/embeddeds.png)

Om du vill ange AEM författare, AEM publicera eller båda, bäddas paketet in i `all`-behållarpaketet i en speciell mappsökväg i följande format:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Bryter ned mappstrukturen:

+ Mappen **på första nivån måste vara** `/apps`.
+ Mappen på den andra nivån representerar programmet med `-packages` efter mappnamnet. Ofta finns det bara en mapp på andra nivån som alla underpaket är inbäddade i, men du kan skapa valfritt antal mappar på andra nivån för att bäst representera programmets logiska struktur:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Mappar som bäddats in i underpaket namnges med suffixet `-packages`. Detta garanterar att distributionskoden och innehållspaketen **inte** distribueras till målmappen/målmapparna i något underpaket `/apps/<app-name>/...`, vilket skulle leda till destruktivt och cykliskt installationsbeteende.

+ Mappen på den tredje nivån måste vara antingen
   `application`,  `content` eller  `container`
   + Mappen `application` innehåller kodpaket
   + Mappen `content` innehåller innehållspaket
   + Mappen `container` innehåller alla [extra programpaket](#extra-application-packages) som kan ingå i AEM.
Mappnamnet motsvarar [pakettyperna](#package-types) för paketen som det innehåller.
+ Mappen på den fjärde nivån innehåller underpaketen och måste vara någon av:
   + `install` för installation på **både** AEM-redigerare och AEM-publicering
   + `install.author` för installation **endast** på AEM-redigerare
   + `install.publish` för att  **** endast installera AEM publicera Observera att endast  `install.author` och  `install.publish` stöds som mål. Andra körningslägen **stöds inte**.

En distribution som innehåller AEM författare och publicerar specifika paket kan till exempel se ut så här:

+ `all` Behållarpaket bäddar in följande paket för att skapa en enda distributionsartefakt
   + `ui.apps` inbäddad i  `/apps/my-app-packages/application/install` distribuerar kod till både AEM författare och AEM
   + `ui.apps.author` inbäddad i  `/apps/my-app-packages/application/install.author` distribuerar kod till endast AEM författare
   + `ui.content` inbäddat i  `/apps/my-app-packages/content/install` distribuerar innehåll och konfiguration till både AEM författare och AEM publicera
   + `ui.content.publish` inbäddad i  `/apps/my-app-packages/content/install.publish` distribuerar innehåll och konfiguration till endast AEM publicera

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-embeddeds) nedan för ett fullständigt kodfragment.

### Behållarpaketets filterdefinition {#container-package-filter-definition}

På grund av inbäddningen av kod- och innehållsunderpaket i behållarpaketet måste de inbäddade målsökvägarna läggas till i behållarprojektets `filter.xml` för att de inbäddade paketen ska inkluderas i behållarpaketet när de byggs.

Lägg bara till `<filter root="/apps/<my-app>-packages"/>`-posterna för mappar på andra nivån som innehåller underpaket som ska distribueras.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-container-package-filters) nedan för ett fullständigt kodfragment.

## Bädda in paket från tredje part {#embedding-3rd-party-packages}

Alla paket måste vara tillgängliga via [Adobe offentliga Maven-artefaktarkivet](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) eller en tillgänglig offentlig, refererbar databas från tredje part för Maven-artefakter.

Om tredjepartspaketen finns i **Adobes offentliga Maven-databas** behövs ingen ytterligare konfiguration för att Adobe Cloud Manager ska kunna lösa artefakterna.

Om tredjepartspaketen finns i en **offentlig tredjepartsdatabas för Maven-felaktigheter** måste den här databasen registreras i projektets `pom.xml` och bäddas in enligt den metod som [beskrivs ovan](#embeddeds).

Tredjepartsprogram/-anslutningar bör bäddas in med `all`-paketet som en behållare i projektets behållarpaket (`all`).

Om du lägger till Maven-beroenden följer standardMaven-rutiner, och inbäddning av artefakter från tredje part (kod och innehållspaket) är [som anges ovan](#embedding-3rd-party-packages).

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-3rd-party-maven-repositories) nedan för ett fullständigt kodfragment.

## Paketberoenden mellan `ui.apps` från `ui.content`-paket {#package-dependencies}

För att paketen ska kunna installeras på rätt sätt rekommenderar vi att du skapar beroenden mellan paketen.

Den allmänna regeln är paket som innehåller muterbart innehåll (`ui.content`) som ska vara beroende av den oföränderliga koden (`ui.apps`) som stöder återgivning och användning av det muterbara innehållet.

Ett betydande undantag från den här allmänna regeln är om det oföränderliga kodpaketet (`ui.apps` eller något annat), __endast__ innehåller OSGi-paket. I så fall ska inget AEM deklarera ett beroende av det. Detta beror på att oföränderliga kodpaket __endast__ som innehåller OSGi-paket inte är registrerade med AEM Package Manager, och därför kommer alla AEM som är beroende av paketet att ha ett otillfredsställande beroende och inte kunna installeras.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-package-dependencies) nedan för ett fullständigt kodfragment.

De vanligaste mönstren för innehållspaketberoenden är:

### Beroenden för enkelt distributionspaket {#simple-deployment-package-dependencies}

Det enkla fallet anger att det ändringsbara innehållspaketet `ui.content` är beroende av det ändringsbara kodpaketet `ui.apps`.

+ `all` har inga beroenden
   + `ui.apps` har inga beroenden
   + `ui.content` är beroende av  `ui.apps`

### Komplexa distributionspaketberoenden {#complex-deploxment-package-dependencies}

Komplexa driftsättningar bygger vidare på det enkla fallet och ställer in beroenden mellan motsvarande muterbara innehåll och oföränderliga kodpaket. Om det behövs kan beroenden etableras även mellan oföränderliga kodpaket.

+ `all` har inga beroenden
   + `common.ui.apps.common` har inga beroenden
   + `site-a.ui.apps` är beroende av  `common.ui.apps`
   + `site-a.ui.content` är beroende av  `site-a.ui.apps`
   + `site-b.ui.apps` är beroende av  `common.ui.apps`
   + `site-b.ui.content` är beroende av  `site-b.ui.apps`

## Lokal utveckling och distribution {#local-development-and-deployment}

Projektstrukturerna och organisationen som beskrivs i den här artikeln är **helt kompatibla** lokala AEM.

## POM XML-kodfragment {#pom-xml-snippets}

Nedan följer Maven `pom.xml`-konfigurationsksnuttar som kan läggas till i Maven-projekt för att anpassa sig till ovanstående rekommendationer.

### Pakettyper {#xml-package-types}

Kod- och innehållspaket, som distribueras som underpaket, måste deklarera pakettypen **application** eller **content**, beroende på vad de innehåller.

#### Behållarpakettyper {#container-package-types}

Behållaren `all/pom.xml` projektet **deklarerar inte** ett `<packageType>`.

#### Kodpakettyper (ej ändringsbara) {#immutable-package-types}

Kodpaket måste ange `packageType` som `application`.

I `ui.apps/pom.xml` deklarerar `<packageType>application</packageType>` byggkonfigurationsdirektiven för `filevault-package-maven-plugin` plugin-deklarationen pakettypen.

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

#### Innehållspakettyper (muterbara) {#mutable-package-types}

Innehållspaket måste ange `packageType` som `content`.

I `ui.content/pom.xml` deklarerar `<packageType>content</packageType>` build configuration-direktivet för `filevault-package-maven-plugin` plugin-deklarationen sin pakettyp.

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

### Markerar paket för distribution av Adobe Cloud Manager {#cloud-manager-target}

I alla projekt som genererar ett paket, **utom** för behållarprojektet (`all`), lägger du till `<cloudManagerTarget>none</cloudManagerTarget>` i `<properties>`-konfigurationen för plugin-deklarationen `filevault-package-maven-plugin` för att vara säker på att de **inte** distribueras av Adobe Cloud Manager. Behållarpaketet (`all`) ska vara det enskilda paket som distribueras via Cloud Manager, som i sin tur bäddar in all kod och alla innehållspaket som behövs.

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

Repo Init-skript som innehåller Repo Init-skript definieras i OSGi-fabrikskonfigurationen via egenskapen `scripts`. `RepositoryInitializer` Observera att eftersom dessa skript definieras i OSGi-konfigurationer kan de enkelt omfångas i körningsläge med det vanliga `../config.<runmode>`-mappsemantiken.

Observera, att eftersom skript vanligtvis är flerradsdeklarationer är det enklare att definiera dem i `.config`-filen än det JSON-baserade `.cfg.json`-formatet.

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

Egenskapen `scripts` OSGi innehåller direktiv enligt definitionen i [Apache Slings Repo Init-språk](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Databasstrukturpaket {#xml-repository-structure-package}

I `ui.apps/pom.xml` och alla andra `pom.xml` som deklarerar ett kodpaket (`<packageType>application</packageType>`) lägger du till följande konfiguration av databasstrukturpaket i plugin-programmet FileVault Maven. Du kan [skapa ett eget databasstrukturpaket för ditt projekt](repository-structure-package.md).

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

### Bädda in underpaket i behållarpaketet {#xml-embeddeds}

I `all/pom.xml` lägger du till följande `<embeddeds>`-direktiv i `filevault-package-maven-plugin`-deklarationen för plugin-programmet. Kom ihåg att **inte** ska använda konfigurationen `<subPackages>`, eftersom detta inkluderar underpaketen i `/etc/packages` i stället för `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

I `all`-projektets `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) **inkluderar** du alla `-packages`-mappar som innehåller underpaket som ska distribueras:

```xml
<filter root="/apps/my-app-packages"/>
```

Om flera `/apps/*-packages` används i de inbäddade målen måste alla räknas upp här.

### Maven Repositories {#xml-3rd-party-maven-repositories} från tredje part

>[!WARNING]
>
>Om du lägger till fler Maven-databaser kan det ta längre tid att bygga maven när ytterligare Maven-databaser kontrolleras om det finns beroenden.

Lägg till eventuella nödvändiga direktiv från tredje part om databasen för Maven i reaktorprojektets `pom.xml`. Den fullständiga `<repository>`-konfigurationen bör vara tillgänglig från tredjepartsprovidern för databas.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
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

### Paketberoenden mellan `ui.apps` från `ui.content`-paket {#xml-package-dependencies}

I `ui.content/pom.xml` lägger du till följande `<dependencies>`-direktiv i `filevault-package-maven-plugin`-deklarationen för plugin-programmet.

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

### Rensar målmappen för behållarprojektet {#xml-clean-container-package}

I `all/pom.xml` lägger du till plugin-programmet `maven-clean-plugin` som rensar målkatalogen innan en Maven byggs.

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
+ [Plugin-programmet FileVault Content Package Maven](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
