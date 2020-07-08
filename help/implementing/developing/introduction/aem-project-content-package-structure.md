---
title: AEM-projektstruktur
description: Lär dig hur du definierar paketstrukturer för distribution till Adobe Experience Manager Cloud Service.
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '2530'
ht-degree: 17%

---


# AEM-projektstruktur

>[!TIP]
>
>Bekanta dig med grundläggande [AEM Project Archetype-användning](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)och plugin-programmet [FileVault Content Maven](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) när den här artikeln bygger vidare på dessa inlärningar och koncept.

I denna artikel beskrivs de ändringar som krävs för Adobe Experience Manager Maven-projekt som är kompatibla med AEM-Cloud Service genom att säkerställa att de respekterar uppdelningen av muterbart och oföränderligt innehåll. att nödvändiga beroenden har fastställts för att skapa icke-konfliktskapande, deterministiska driftsättningar, och att de paketeras i en installerbar struktur.

AEM-programdistributioner måste bestå av ett enda AEM-paket. Paketet ska i sin tur innehålla underpaket som innehåller allt som programmet behöver för att fungera, inklusive kod, konfiguration och eventuellt baslinjeinnehåll som stöds.

AEM kräver att **innehåll** och **kod** skiljs åt, vilket innebär att ett innehållspaket **inte** kan distribueras till **både** `/apps` och områden som är skrivbara vid körning (som `/content`, `/conf`, `/home`eller allt som inte är `/apps`) i databasen. Programmet måste i stället separera kod och innehåll i separata paket för distribution till AEM.

Den paketstruktur som beskrivs i det här dokumentet är kompatibel med **både** lokala utvecklingsdistributioner och AEM Cloud Service-distributioner.

>[!TIP]
>
>De konfigurationer som beskrivs i det här dokumentet tillhandahålls av [AEM Project Maven Archetype 21 eller senare](https://github.com/adobe/aem-project-archetype/releases).

## Muterbara kontra oföränderliga områden i databasen {#mutable-vs-immutable}

`/apps` och `/libs`**betraktas som oföränderliga områden i AEM, eftersom de inte kan ändras (skapa, uppdatera, ta bort) efter att AEM startats (dvs. vid körning).** Alla försök att ändra ett oföränderligt område vid körning misslyckas.

Everything else in the repository, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. are all **mutable** areas, meaning they can be changed at runtime.

>[!WARNING]
>
>Precis som i tidigare versioner av AEM bör `/libs` du inte ändra. Endast AEM-produktkod kan distribueras till `/libs`.

### Oak Index {#oak-indexes}

Oak-index (`/oak:index`) hanteras specifikt av distributionsprocessen för AEM Cloud-tjänster. Detta beror på att Cloud Manager måste vänta tills ett nytt index har distribuerats och indexerats om fullständigt innan det går över till den nya kodbilden.

Därför måste Oak-index, även om de kan ändras vid körning, distribueras som kod så att de kan installeras innan några ändringsbara paket installeras. Därför är konfigurationer en del av kodpaketet och inte en del av innehållspaketet `/oak:index` [enligt beskrivningen nedan.](#recommended-package-structure)

>[!TIP]
>
>Mer information om hur du indexerar i AEM som en Cloud Service finns i dokumentet [Innehållssökning och indexering.](/help/operations/indexing.md)

## Rekommenderad paketstruktur {#recommended-package-structure}

![Experience Manager projektpaketstruktur](assets/content-package-organization.png)

I det här diagrammet visas en översikt över den rekommenderade projektstrukturen och artefakter för paketdistribution.

Den rekommenderade programdistributionsstrukturen är följande:

+ Paketet, eller kodpaketet, innehåller all kod som ska distribueras och endast distribueras till `ui.apps` `/apps`. Vanliga delar av `ui.apps` paketet omfattar, men är inte begränsade till:
   + OSGi-paket
      + `/apps/my-app/install`
   + [OSGi-konfigurationer](/help/implementing/deploying/configuring-osgi.md)
      + `/apps/my-app/config`
   + [HTML](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) -skript
      + `/apps/my-app/components`
   + JavaScript och CSS (via klientbibliotek)
      + `/apps/my-app/clientlibs`
   + [Övertäckningar](/help/implementing/developing/introduction/overlays.md) för /libs
      + `/apps/cq`, `/apps/dam/`osv.
   + Kontextmedvetna reservkonfigurationer
      + `/apps/settings`
   + ACL-listor (behörigheter)
      + Alla banor `rep:policy` under `/apps`
   + Repo Init OSGi-konfigurationsdirektiv (och medföljande skript)
      + [Repo Init](#repo-init) är det rekommenderade sättet att distribuera (muterbart) innehåll som logiskt är en del av AEM-programmet. Repo Init ska användas för att definiera:
         + Baslinjeinnehållsstrukturer
            + `/conf/my-app`
            + `/content/my-app`
            + `/content/dam/my-app`
         + Användare
         + Tjänstanvändare
         + Grupper
         + ACL-listor (behörigheter)
            + Alla `rep:policy` sökvägar (ändringsbara eller oföränderliga)
+ Paketet, eller innehållspaketet, innehåller allt innehåll och all konfiguration. `ui.content` Innehållspaketet innehåller allt som inte finns i `ui.apps` paketet, eller med andra ord något som inte finns i `/apps` eller `/oak:index`. Vanliga delar av `ui.content` paketet omfattar, men är inte begränsade till:
   + Kontextmedvetna konfigurationer
      + `/conf`
   + Nödvändiga, komplexa innehållsstrukturer (t.ex. Innehållsbygge som bygger på och sträcker sig förbi innehållsstrukturer för baslinjen som definierats i Repo Init.
      + `/content`, `/content/dam`osv.
   + Styrda taggar för taxonomier
      + `/content/cq:tags`
   + Etc legacy nodes
      + `/etc`
+ Paketet `all` är ett behållarpaket som ENDAST innehåller paketen `ui.apps` och `ui.content` som inbäddade. Paketet `all` får inte ha något **eget innehåll**, utan ska delegera all driftsättning till databasen till sina underpaket.

   Paket ingår nu i Maven [FileVault-pluginens inbäddade konfiguration](#embeddeds), i stället för i `<subPackages>` konfigurationen.

   För komplexa Experience Manager-distributioner kan det vara önskvärt att skapa flera projekt `ui.apps` och `ui.content` paket som representerar specifika webbplatser eller klientorganisationer i AEM. Om detta görs ser du till att delningen mellan ändringsbart och icke ändringsbart innehåll respekteras och att de nödvändiga innehållspaketen läggs till som underpaket i `all` behållarinnehållspaketet.

   En innehållsstruktur för en komplex distribution kan till exempel se ut så här:

   + `all` innehållspaketet bäddar in följande paket för att skapa en enda distributionsartefakt
      + `ui.apps.common` distribuerar kod som krävs för **både** plats A och plats B
      + `ui.apps.site-a` distribuerar kod som krävs av plats A
      + `ui.content.site-a` distribuerar innehåll och konfiguration som krävs av plats A
      + `ui.apps.site-b` distribuerar kod som krävs av plats B
      + `ui.content.site-b` distribuerar innehåll och konfiguration som krävs av plats B

## Pakettyper {#package-types}

Paket ska märkas med sin deklarerade pakettyp.

+ Behållarpaket får inte ha någon `packageType` uppsättning.
+ Kodpaket (oföränderliga) måste anges `packageType` till `application`.
+ Innehållspaket (mutable) måste anges `packageType` till `content`.

Mer information finns i dokumentationen [till](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) Apache Jackrabbit FileVault - Package Maven Plugin och konfigurationsfragmentet [för](#marking-packages-for-deployment-by-adoube-cloud-manager) FileVault Maven nedan.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-package-types) nedan för ett fullständigt kodavsnitt.

## Markera paket för distribution med Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Som standard hämtar Adobe Cloud Manager alla paket som skapas av Maven-bygget, men eftersom behållarpaketet (`all`) är en enda distributionsartefakt som innehåller all kod och alla innehållspaket måste vi se till att **endast** behållarpaketet (`all`) distribueras. För att säkerställa detta måste andra paket som genereras av Maven-bygget markeras med FileVaults Maven-pluginkonfiguration `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` för innehållspaket.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#pom-xml-snippets) nedan för ett fullständigt kodavsnitt.

## Repo Init{#repo-init}

Repo Init innehåller instruktioner, eller skript, som definierar JCR-strukturer, från vanliga nodstrukturer som mappträd till användare, tjänstanvändare, grupper och ACL-definition.

De viktigaste fördelarna med Repo Init är att de har implicit behörighet att utföra alla åtgärder som definieras av deras skript, och att de anropas tidigt under distributionens livscykel för att säkerställa att alla nödvändiga JCR-strukturer finns när koden körs.

Rep Init-skript som finns i projektet fungerar som skript, men de kan och bör användas för att definiera följande muterbara strukturer: `ui.apps`

+ Baslinjeinnehållsstrukturer
   + Examples: `/content/my-app`, `/content/dam/my-app`, `/conf/my-app/settings`
+ Tjänstanvändare
+ Användare
+ Grupper
+ ACL

Repo Init-skript lagras som `scripts` poster i `RepositoryInitializer` OSGi-fabrikskonfigurationer, och kan därför implicit användas i runmode, vilket möjliggör skillnader mellan AEM Author och AEM Publish Services Repo Init-skript, eller till och med mellan Envs (Dev, Stage och Prod).

Observera, att när du definierar Användare, och Grupper, anses bara grupper vara en del av programmet, och att de är en del av dess funktion bör definieras här. Organisationens användare och grupper bör fortfarande definieras vid körning i AEM. Om ett anpassat arbetsflöde till exempel tilldelar arbete till en namngiven grupp, bör den gruppen definieras i via Repo Init i AEM-programmet, men om grupperingen bara är organisatorisk, till exempel&quot;Wendy&#39;s Team&quot; och&quot;Sean&#39;s Team&quot;, är dessa bäst definierade och hanteras vid körning i AEM.

>[!TIP]
>
>Repo Init-skript *måste* definieras i det textbundna `scripts` fältet och `references` konfigurationen kommer inte att fungera.

Den fullständiga ordlistan för Repo Init-skript finns i dokumentationen [till](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)Apache Sling Repo Init.

>[!TIP]
>
>Se avsnittet [Kodfragment för](#snippet-repo-init) upprepning nedan för ett fullständigt kodavsnitt.

## Databasstrukturpaket {#repository-structure-package}

Kodpaket kräver att konfigurationen för plugin-programmet FileVault Maven konfigureras för att referera till en `<repositoryStructurePackage>` som kräver att strukturella beroenden är korrekta (för att säkerställa att ett kodpaket inte installeras över ett annat). Du kan [skapa ett eget databasstrukturpaket för projektet](repository-structure-package.md).

Detta **krävs endast** för kodpaket, vilket innebär alla paket som är markerade med `<packageType>application</packageType>`.

Mer information om hur du skapar ett databasstrukturpaket för programmet finns i [Utveckla ett databasstrukturpaket](repository-structure-package.md).

Observera att innehållspaket (`<packageType>content</packageType>`) **inte** kräver det här strukturpaketet för databasen.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-repository-structure-package) nedan för ett fullständigt kodavsnitt.

## Bädda in underpaket i behållarpaketet{#embeddeds}

Innehåll eller kodpaket placeras i en särskild&quot;side-car&quot;-mapp och kan användas för installation på antingen AEM-författare, AEM-publicering eller både och med hjälp av plugin-programmet FileVault Maven `<embeddeds>` . Observera att `<subPackages>` konfigurationen inte ska användas.

Vanliga användningsfall är:

+ ACL:er/behörigheter som skiljer sig mellan AEM-författaranvändare och AEM-publiceringsanvändare
+ Konfigurationer som används för att stödja aktiviteter endast på AEM-författare
+ Kod som integreringar med bakomliggande system som bara krävs för att köras på AEM-författare

![Bädda in paket](assets/embeddeds.png)

Om du vill ange AEM-författare, AEM-publicering eller båda som mål, bäddas paketet in i `all` behållarpaketet på en speciell mappsökväg i följande format:

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

Bryter ned mappstrukturen:

+ Mappen på första nivån **måste vara** `/apps`.
+ Mappen på den andra nivån representerar programmet med `-packages` fast post till mappnamnet. Ofta finns det bara en mapp på andra nivån som alla underpaket är inbäddade i, men du kan skapa valfritt antal mappar på andra nivån för att bäst representera programmets logiska struktur:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`
   >[!WARNING]
   >
   >Mappar som bäddats in i underpaket namnges med suffixet `-packages`. Detta garanterar att distributionskoden och innehållspaketen **inte** distribueras till målmappen/målmapparna i något underpaket `/apps/<app-name>/...`, vilket skulle leda till destruktivt och cykliskt installationsbeteende.

+ Mappen på den tredje nivån måste vara antingen
   `application` eller `content`
   + Mappen innehåller `application` kodpaket
   + Mappen innehåller `content` innehållspaket. Mappnamnet måste motsvara [pakettyperna](#package-types) i de paket som den innehåller.
+ Mappen på den fjärde nivån innehåller underpaketen och måste vara någon av:
   + `install` för installation på **både** AEM-redigerare och AEM-publicering
   + `install.author` för installation **endast** på AEM-redigerare
   + `install.publish` för att **endast** installera på AEM publishObservera att endast `install.author` och `install.publish` stöds som mål. Andra körningslägen **stöds inte**.

En distribution som innehåller AEM-författare och publicerar specifika paket kan till exempel se ut så här:

+ `all` Behållarpaket bäddar in följande paket för att skapa en enda distributionsartefakt
   + `ui.apps` inbäddad i `/apps/my-app-packages/application/install` distribuerar kod till både AEM-författare och AEM-publicering
   + `ui.apps.author` inbäddad i `/apps/my-app-packages/application/install.author` distribuerar kod till endast AEM-författare
   + `ui.content` inbäddat i `/apps/my-app-packages/content/install` distribuerar innehåll och konfiguration till både AEM-författare och AEM-publicering
   + `ui.content.publish` inbäddad i `/apps/my-app-packages/content/install.publish` distribuerar innehåll och konfiguration till endast AEM-publicering

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-embeddeds) nedan för ett fullständigt kodavsnitt.

### Behållarpaketets filterdefinition {#container-package-filter-definition}

På grund av inbäddningen av kod- och innehållsunderpaket i behållarpaketet måste de inbäddade målsökvägarna läggas till i behållarprojektens för `filter.xml` att säkerställa att de inbäddade paketen inkluderas i behållarpaketet när de byggs.

Lägg bara till poster `<filter root="/apps/<my-app>-packages"/>` för mappar på andra nivån som innehåller underpaket som ska distribueras.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-container-package-filters) nedan för ett fullständigt kodavsnitt.

## Bädda in paket från tredje part {#embedding-3rd-party-packages}

Alla paket måste vara tillgängliga via [Adobes publika arkiv](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) för Maven-felaktigheter eller en tillgänglig offentlig, refererbar databas för Maven-felaktigheter från tredje part.

Om tredjepartspaketen finns i **Adobes offentliga Maven-databas** behövs ingen ytterligare konfiguration för att Adobe Cloud Manager ska kunna lösa artefakterna.

Om tredjepartspaketen finns i en **offentlig tredjepartsdatabas för Maven-felaktigheter** måste den här databasen registreras i projektets `pom.xml` och bäddas in enligt den metod som [beskrivs ovan](#embeddeds). Om programmet/kopplingen från tredje part kräver både kod- och innehållspaket måste varje paket bäddas in på rätt platser i behållarpaketet (`all`).

Om du lägger till Maven-beroenden följer standardMaven-rutiner, och inbäddning av artefakter från tredje part (kod- och innehållspaket) [beskrivs ovan](#embedding-3rd-party-packages).

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-3rd-party-maven-repositories) nedan för ett fullständigt kodavsnitt.

## Paketberoenden mellan `ui.apps` från `ui.content` paket {#package-dependencies}

För att paketen ska kunna installeras på rätt sätt rekommenderar vi att du skapar beroenden mellan paketen.

Den allmänna regeln är paket som innehåller muterbart innehåll (`ui.content`) som ska vara beroende av den oföränderliga koden (`ui.apps`) som stöder återgivning och användning av det muterbara innehållet.

Ett betydande undantag från den här allmänna regeln är om det oföränderliga kodpaketet (`ui.apps` eller något annat) __endast__ innehåller OSGi-paket. I så fall ska inget AEM-paket deklarera ett beroende av det. Detta beror på att oföränderliga kodpaket som __bara__ innehåller OSGi-paket inte är registrerade med AEM Package Manager, och därför kommer alla AEM-paket som är beroende av det att ha ett otillfredsställande beroende och inte kunna installeras.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-package-dependencies) nedan för ett fullständigt kodavsnitt.

De vanligaste mönstren för innehållspaketberoenden är:

### Enkla distributionspaketberoenden {#simple-deployment-package-dependencies}

I det enkla fallet anges att det `ui.content` ändringsbara innehållspaketet ska vara beroende av det `ui.apps` ändringsbara kodpaketet.

+ `all` har inga beroenden
   + `ui.apps` har inga beroenden
   + `ui.content` är beroende av `ui.apps`

### Komplexa distributionspaketberoenden {#complex-deploxment-package-dependencies}

Komplexa driftsättningar bygger vidare på det enkla fallet och ställer in beroenden mellan motsvarande muterbara innehåll och oföränderliga kodpaket. Om det behövs kan beroenden etableras även mellan oföränderliga kodpaket.

+ `all` har inga beroenden
   + `ui.apps.common` har inga beroenden
   + `ui.apps.site-a` är beroende av `ui.apps.common`
   + `ui.content.site-a` är beroende av `ui.apps.site-a`
   + `ui.apps.site-b` är beroende av `ui.apps.common`
   + `ui.content.site-b` är beroende av `ui.apps.site-b`

## Lokal utveckling och driftsättning {#local-development-and-deployment}

De projektstrukturer och den organisation som beskrivs i den här artikeln är **helt kompatibla** med AEM-instanser för lokal utveckling.

## POM XML-kodfragment {#pom-xml-snippets}

Nedan följer Maven- `pom.xml` konfigurationsfragment som kan läggas till i Maven-projekt för att anpassa sig till ovanstående rekommendationer.

### Pakettyper {#xml-package-types}

Kod- och innehållspaket, som distribueras som underpaket, måste deklarera pakettypen **application** eller **content**, beroende på vad de innehåller.

#### Behållarpakettyper {#container-package-types}

Behållarprojektet `all/pom.xml` deklarerar **inte** en `<packageType>`.

#### Kodpakettyper (ej ändringsbara) {#immutable-package-types}

Kodpaket måste anges `packageType` till `application`.

I `ui.apps/pom.xml`koden deklarerar `<packageType>application</packageType>` byggkonfigurationsdirektiven för `filevault-package-maven-plugin` plugin-deklarationen sin pakettyp.

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
        <name>${my-app.ui.apps}</name>
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

Innehållspaket måste anges `packageType` till `content`.

I `ui.content/pom.xml`filen deklareras pakettypen av direktivet `<packageType>content</packageType>` build configuration för `filevault-package-maven-plugin` plugin-deklarationen.

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
        <name>${my-app.ui.content}</name>
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

I alla projekt som genererar ett paket, **utom** för behållarprojektet (`all`), lägger du till `<cloudManagerTarget>none</cloudManagerTarget>` i `<properties>`-konfigurationen för plugin-deklarationen `filevault-package-maven-plugin` för att vara säker på att de **inte** distribueras av Adobe Cloud Manager. The container (`all`) package should be the singular package deployed via Cloud Manager, which in turn embeds all required code and content packages.

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

Repo Init-skript som innehåller Repo Init-skript definieras i `RepositoryInitializer` OSGi-fabrikskonfigurationen via `scripts` egenskapen. Observera att eftersom dessa skript definieras i OSGi-konfigurationer kan de enkelt omfångas i runmode med hjälp av vanliga `../config.<runmode>` mappsemantik.

Observera att eftersom skript vanligtvis är flerradsdeklarationer är det enklare att definiera dem i `.config` filen än i XML-basformatet `sling:OsgiConfig` .

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

I `ui.apps/pom.xml` och andra `pom.xml` som deklarerar ett kodpaket (`<packageType>application</packageType>`) lägger du till följande konfiguration av databasstrukturpaket i plugin-programmet FileVault Maven. Du kan [skapa ett eget databasstrukturpaket för projektet](repository-structure-package.md).

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

I `all/pom.xml`lägger du till följande `<embeddeds>` direktiv till `filevault-package-maven-plugin` plugin-deklarationen. Kom ihåg att du **inte** ska använda `<subPackages>` konfigurationen eftersom detta inkluderar underpaketen i `/etc/packages` stället för `/apps/my-app-packages/<application|content>/install(.author|.publish)?`.

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

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
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

          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Code package's artifact is named `.content` -->
              <artifactId>core.wcm.components.content</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/application/install</target>
          </embedded>

          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Content package's artifact is named `.conf` -->
              <artifactId>core.wcm.components.conf</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/content/install</target>
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

### Maven Repositories från tredje part {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Om du lägger till fler Maven-databaser kan det ta längre tid att bygga maven när ytterligare Maven-databaser kontrolleras om det finns beroenden.

I reaktorprojektets `pom.xml`exempel lägger du till eventuella direktiv från tredje part om databasen för Maven. Den fullständiga `<repository>` konfigurationen bör vara tillgänglig från tredjepartsprovidern.

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

### Paketberoenden mellan `ui.apps` från `ui.content` paket {#xml-package-dependencies}

I `ui.content/pom.xml`lägger du till följande `<dependencies>` direktiv till `filevault-package-maven-plugin` plugin-deklarationen.

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

### Rensa Target-mappen för behållarprojektet {#xml-clean-container-package}

Lägg till det plugin-program som `all/pom.xml` `maven-clean-plugin` ska rensa målkatalogen innan en Maven byggs.

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

+ [Hantera paket med Maven](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [Plugin-programmet FileVault Content Package Maven](http://jackrabbit.apache.org/filevault-package-maven-plugin/)