---
title: AEM projektstruktur
description: Lär dig hur du definierar paketstrukturer för distribution till Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 3%

---

# AEM projektstruktur

>[!TIP]
>
>Bekanta dig med grundläggande [AEM Project Archetype-användning](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE) och [FileVault Content Maven-plugin](/help/implementing/developing/tools/maven-plugin.md) när den här artikeln bygger på dessa inlärningar och begrepp.

I den här artikeln beskrivs de ändringar som krävs för Adobe Experience Manager Maven-projekt som är AEM as a Cloud Service-kompatibla genom att säkerställa att de respekterar delningen av ändringsbart och oföränderligt innehåll. Beroenden skapas också för att skapa icke-konfliktskapande, deterministiska distributioner, och de paketeras i en distributionsbar struktur.

AEM programdistributioner måste bestå av ett enda AEM. Paketet ska i sin tur innehålla delpaket som innehåller allt som krävs för att programmet ska fungera, inklusive kod, konfiguration och allt baslinjeinnehåll som stöds.

AEM kräver en separation av **content** och **code**, vilket innebär att ett enstaka innehållspaket **inte kan** distribueras till **både** `/apps` och körningsskrivbara områden (till exempel `/content`, `/conf`, `/home` eller något annat som inte är `/apps`) i databasen. Programmet måste i stället separera kod och innehåll i separata paket för distribution till AEM.

Den paketstruktur som beskrivs i det här dokumentet är kompatibel med **både** lokala utvecklingsdistributioner och AEM Cloud Service-distributioner.

>[!TIP]
>
>Konfigurationerna som beskrivs i det här dokumentet tillhandahålls av [AEM Project Maven Archetype 24 eller senare](https://github.com/adobe/aem-project-archetype/releases).

## Mutable kontra Immutable Areas of the Repository {#mutable-vs-immutable}

Områdena `/apps` och `/libs` i AEM betraktas som **oföränderliga** eftersom de inte kan ändras (skapa, uppdatera, ta bort) efter att AEM startats (d.v.s. vid körning). Alla försök att ändra ett oföränderligt område vid körning misslyckas.

Allt annat i databasen, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp` och så vidare, är alla **muterbara** områden, vilket innebär att de kan ändras under körning.

>[!WARNING]
>
>Precis som i tidigare versioner av AEM ska `/libs` inte ändras. Endast AEM produktkod kan distribueras till `/libs`.

### Oak Index {#oak-indexes}

Oak-index (`/oak:index`) hanteras av AEM as a Cloud Service distributionsprocess. Orsaken är att Cloud Manager måste vänta tills ett nytt index har distribuerats och indexerats om fullständigt innan det går över till den nya kodbilden.

Även om Oak-index kan ändras vid körning måste de därför distribueras som kod så att de kan installeras innan några ändringsbara paket installeras. Därför är `/oak:index`-konfigurationer en del av kodpaketet och inte en del av innehållspaketet [&#x200B; enligt beskrivningen nedan](#recommended-package-structure).

>[!TIP]
>
>Mer information om indexering i AEM as a Cloud Service finns i [Innehållssökning och indexering](/help/operations/indexing.md).

## Rekommenderad paketstruktur {#recommended-package-structure}

![Projektpaketstruktur för Experience Manager](assets/content-package-organization.png)

I det här diagrammet visas en översikt över den rekommenderade projektstrukturen och artefakter för paketdistribution.

Den rekommenderade programdistributionsstrukturen är följande:

### Kodpaket / OSGi Bundles

+ OSGi-paketfilen genereras och bäddas in direkt i hela projektet.

+ Paketet `ui.apps` innehåller all kod som ska distribueras och endast distribueras till `/apps`. Vanliga element i paketet `ui.apps` innehåller, men är inte begränsade till:
   + [Komponentdefinitioner och HTML](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=sv-SE)-skript
      + `/apps/my-app/components`
   + JavaScript och CSS (via [klientbibliotek](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Övertäckningar](/help/implementing/developing/introduction/overlays.md) av `/libs`
      + `/apps/cq`, `/apps/dam/` och så vidare.
   + Kontextmedvetna reservkonfigurationer
      + `/apps/settings`
   + ACL-listor (behörigheter)
      + Alla `rep:policy` för alla sökvägar under `/apps`
   + [Förkompilerade paketerade skript](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html?lang=sv-SE)

>[!NOTE]
>
>Samma kod måste distribueras till alla miljöer. Den här koden säkerställer att valideringar i scenmiljön också är i produktion. Mer information finns i avsnittet [Körningslägen](/help/implementing/deploying/overview.md#runmodes).


### Innehållspaket

+ Paketet `ui.content` innehåller allt innehåll och all konfiguration. Innehållspaketet innehåller alla noddefinitioner som inte finns i `ui.apps`- eller `ui.config`-paketen, eller med andra ord något som inte finns i `/apps` eller `/oak:index`. Vanliga element i paketet `ui.content` innehåller, men är inte begränsade till:
   + Kontextmedvetna konfigurationer
      + `/conf`
   + Nödvändiga, komplexa innehållsstrukturer (d.v.s. innehållsbygge som bygger på och sträcker sig utanför de ursprungliga innehållsstrukturer som definierats i Repo Init).
      + `/content`, `/content/dam` och så vidare.
   + Styrda taggar för taxonomier
      + `/content/cq:tags`
   + Äldre noder (helst migrera dessa noder till platser som inte är-/osv.)
      + `/etc`

### Behållarpaket

+ Paketet `all` är ett behållarpaket som ENDAST innehåller distributionsbara artefakter, den OSGI-paketerade JAR-filen, `ui.apps`, `ui.config` och `ui.content`-paket som inbäddade. Paketet `all` får inte ha **något eget innehåll eller någon egen kod**, utan i stället delegera all distribution till databasen till dess underpaket eller OSGi-paketera JAR-filer.

  Paket inkluderas nu med Maven [FileVault-pluginens inbäddade konfiguration](#embeddeds) i stället för `<subPackages>` -konfigurationen.

  För komplexa Experience Manager-distributioner kan det vara önskvärt att skapa flera `ui.apps`-, `ui.config`- och `ui.content`-projekt/paket som representerar specifika webbplatser eller klientorganisationer i AEM. Om du gör det ser du till att delningen mellan ändringsbart och icke ändringsbart innehåll respekteras och att de nödvändiga innehållspaketen och OSGi-paketets JAR-filer bäddas in som delpaket i `all`-behållarinnehållspaketet.

  En innehållsstruktur för en komplex distribution kan till exempel se ut så här:

   + Innehållspaketet `all` bäddar in följande paket för att skapa en enda distributionsartefakt
      + `common.ui.apps` distribuerar kod som krävs av **både** plats A och plats B
      + `site-a.core` OSGi bundle Jar krävs av webbplats A
      + `site-a.ui.apps` distribuerar kod som krävs av plats A
      + `site-a.ui.config` distribuerar OSGi-konfigurationer som krävs för plats A
      + `site-a.ui.content` distribuerar innehåll och konfiguration som krävs av plats A
      + `site-b.core` OSGi bundle Jar krävs av webbplats B
      + `site-b.ui.apps` distribuerar kod som krävs av plats B
      + `site-b.ui.config` distribuerar OSGi-konfigurationer som krävs av plats B
      + `site-b.ui.content` distribuerar innehåll och konfiguration som krävs av plats B

+ Paketet `ui.config` innehåller alla [OSGi-konfigurationer](/help/implementing/deploying/configuring-osgi.md):
   + Betraktad kod och hör till OSGi-paket, men innehåller inte vanliga innehållsnoder. Därför markeras det som ett behållarpaket
   + Organisationsmapp som innehåller körlägesspecifika OSGi-konfigurationsdefinitioner
      + `/apps/my-app/osgiconfig`
   + Vanlig OSGi-konfigurationsmapp som innehåller standardkonfigurationer för OSGi som gäller för alla AEM as a Cloud Service-måldistributionsmål
      + `/apps/my-app/osgiconfig/config`
   + Kör lägesspecifika OSGi-konfigurationsmappar som innehåller standardkonfigurationer för OSGi som gäller för alla AEM as a Cloud Service-måldistributionsmål
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi-konfigurationsskript
      + [Repo Init](#repo-init) rekommenderas för att distribuera (muterbart) innehåll som logiskt är en del av AEM. Repo Init OSGi-konfigurationerna ska placeras i lämplig `config.<runmode>`-mapp enligt ovan och användas för att definiera:
         + Baslinjeinnehållsstrukturer
         + Användare
         + Tjänstanvändare
         + Grupper
         + ACL-listor (behörigheter)

### Extra programpaket{#extra-application-packages}

Om andra AEM-projekt, som i sig själva består av sina egna kod- och innehållspaket, används av den AEM distributionen, bör deras behållarpaket bäddas in i projektets `all`-paket.

Ett AEM projekt som innehåller två AEM program kan se ut så här:

+ Innehållspaketet `all` bäddar in följande paket för att skapa en enda distributionsartefakt
   + `core` OSGi bundle Jar krävs av AEM
   + `ui.apps` distribuerar kod som krävs för AEM
   + `ui.config` distribuerar OSGi-konfigurationer som krävs av AEM
   + `ui.content` distribuerar innehåll och konfiguration som krävs för AEM
   + `vendor-x.all` distribuerar allt (kod och innehåll) som krävs av leverantör X-programmet
   + `vendor-y.all` distribuerar allt (kod och innehåll) som krävs av leverantörens Y-program

## Pakettyper {#package-types}

Paket ska märkas med sin deklarerade pakettyp. Pakettyper gör det lättare att klargöra syftet med och distributionen av ett paket.

+ Behållarpaket måste ange `packageType` till `container`. Behållarpaket får inte innehålla vanliga noder. Endast OSGi-paket, konfigurationer och underpaket tillåts. Behållare i AEM as a Cloud Service får inte använda [installera kopplingar](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Kodpaket (ej ändringsbara) måste ange `packageType` till `application`.
+ Innehållspaket (mutable) måste ange `packageType` till `content`.


Mer information finns i [dokumentationen för Apache Jackrabbit FileVault - Package Maven Plugin &#x200B;](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Pakettyper för Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html) och [konfigurationsfragmentet för FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) nedan.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-package-types) nedan för ett fullständigt fragment.

## Markera paket för distribution av Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Som standard skördar Adobe Cloud Manager alla paket som produceras av Maven-bygget. Eftersom behållarpaketet (`all`) är en enda distributionsartefakt som innehåller alla kod och innehållspaket, måste du se till att **endast** behållarpaketet (`all`) distribueras. För att säkerställa detta måste andra paket som genereras av Maven-bygget markeras med FileVaults Maven-pluginkonfiguration `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` för innehållspaket.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#pom-xml-snippets) nedan för ett fullständigt fragment.

## Repo Init{#repo-init}

Repo Init innehåller instruktioner, eller skript, som definierar JCR-strukturer, från vanliga nodstrukturer som mappträd till användare, tjänstanvändare, grupper och ACL-definition.

De viktigaste fördelarna med Repo Init är att de har implicit behörighet att utföra alla åtgärder som definieras av deras skript. Sådana skript anropas tidigt under driftsättningens livscykel för att säkerställa att alla nödvändiga JCR-strukturer finns när tidskoden körs.

Repo Init-skript som finns i `ui.config`-projektet som skript kan och bör användas för att definiera följande muterbara strukturer:

+ Baslinjeinnehållsstrukturer
+ Tjänstanvändare
+ Användare
+ Grupper
+ ACL:er

Repo Init-skript lagras som `scripts` poster i `RepositoryInitializer` OSGi-fabrikskonfigurationer. Därför kan de vara implicit inriktade genom körningsläge, vilket möjliggör skillnader mellan AEM författare och AEM Publish Services Repo Init-skript eller till och med mellan miljöer (Dev, Stage och Prod).

Repo Init OSGi-konfigurationer skrivs bäst i [`.config` OSGi-konfigurationsformatet &#x200B;](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) eftersom de har stöd för flera rader, vilket är ett undantag till de bästa sätten att använda [`.cfg.json` för att definiera OSGi-konfigurationer](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

När du definierar användare och grupper betraktas bara grupper som en del av programmet och de är integrerade i dess funktion. Du definierar fortfarande användare och grupper för organisation vid körning i AEM. Om ett anpassat arbetsflöde till exempel tilldelar arbete till en namngiven grupp, definierar du den gruppen med hjälp av Repo Init i AEM. Men om grupperingen bara är organisatorisk, till exempel&quot;Wendy&#39;s Team&quot; och&quot;Sean&#39;s Team&quot;, är de här grupperna bäst definierade och hanterade vid körning i AEM.

>[!TIP]
>
>Repo Init-skript *måste* definieras i det textbundna `scripts` fältet, annars fungerar inte `references`-konfigurationen.

Det fullständiga språket för Repo Init-skript finns i [dokumentationen för Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Se avsnittet [Kodfragment för inledande &#x200B;](#snippet-repo-init) nedan för ett fullständigt kodavsnitt.

## Databasstrukturpaket {#repository-structure-package}

Kodpaket kräver att konfigurationen för plugin-programmet FileVault Maven konfigureras så att det refererar till en `<repositoryStructurePackage>` som kräver att strukturella beroenden är korrekta (för att säkerställa att ett kodpaket inte installeras över ett annat). Du kan [skapa ett eget databasstrukturpaket för ditt projekt](repository-structure-package.md).

**Endast obligatoriskt** för kodpaket, vilket innebär alla paket som är markerade med `<packageType>application</packageType>`.

Mer information om hur du skapar ett databasstrukturpaket för programmet finns i [Utveckla ett databasstrukturpaket](repository-structure-package.md).

Innehållspaket (`<packageType>content</packageType>`) **kräver inte** det här databasstrukturpaketet.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-repository-structure-package) nedan för ett fullständigt fragment.

## Bädda in delpaket i behållarpaketet{#embeddeds}

Innehåll eller kodpaket placeras i en speciell &quot;side-car&quot;-mapp och kan användas för installation på antingen AEM författare, AEM publicering eller båda med hjälp av plugin-programmets `<embeddeds>`-konfiguration för FileVault Maven. Använd inte `<subPackages>`-konfigurationen.

Vanliga användningsfall är:

+ Behörighetslistor/behörigheter som skiljer sig åt mellan AEM författaranvändare och AEM publiceringsanvändare
+ Konfigurationer som används för att stödja aktiviteter endast för AEM författare
+ Kod som integreringar med back-office-system som bara krävs för att köras av AEM

![Bädda in paket](assets/embeddeds.png)

Om du vill ange AEM författare, AEM publicera eller båda, är paketet inbäddat i behållarpaketet `all` på en speciell mappsökväg i följande format:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Bryter ned den här mappstrukturen:

+ Mappen **på första nivån måste vara** `/apps`.
+ Mappen på den andra nivån representerar programmet med `-packages` efter mappnamnet. Det finns ofta bara en mapp på andra nivån som alla underpaket är inbäddade i, men hur många mappar på andra nivån som helst kan skapas för att bäst representera programmets logiska struktur:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >Delpaketets inbäddade mappar namnges med suffixet `-packages`. Namngivningen säkerställer att distributionskoden och innehållspaketen **inte** distribueras till målmapparna för alla underpaket `/apps/<app-name>/...` vilket leder till destruktiv och cyklisk installation.

+ Mappen på den tredje nivån måste vara antingen
  `application`, `content` eller `container`
   + Mappen `application` innehåller kodpaket
   + Mappen `content` innehåller innehållspaket
   + Mappen `container` innehåller alla [extra programpaket](#extra-application-packages) som kan ingå i AEM.
Det här mappnamnet motsvarar [pakettyperna](#package-types) för paketen som det innehåller.
+ Mappen på den fjärde nivån innehåller underpaketen och måste vara någon av:
   + `install` så att du kan installera på **både** AEM författare och AEM publicera
   + `install.author` så att du installerar **only** på AEM författare
   + `install.publish` så att du installerar **endast** vid AEM publicering
Endast `install.author` och `install.publish` stöds som mål. Andra körningslägen **stöds inte**.

En distribution som innehåller AEM författare och publicerar specifika paket kan till exempel se ut så här:

+ `all`-behållarpaketet bäddar in följande paket för att skapa en enda distributionsartefakt
   + `ui.apps` inbäddad i `/apps/my-app-packages/application/install` distribuerar kod till både AEM författare och AEM publicera
   + `ui.apps.author` inbäddad i `/apps/my-app-packages/application/install.author` distribuerar kod till endast AEM författare
   + `ui.content` inbäddad i `/apps/my-app-packages/content/install` distribuerar innehåll och konfiguration till både AEM författare och AEM publicera
   + `ui.content.publish` inbäddad i `/apps/my-app-packages/content/install.publish` distribuerar innehåll och konfiguration till enbart AEM publicera

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-embeddeds) nedan för ett fullständigt fragment.

### Behållarpaketets filterdefinition {#container-package-filter-definition}

På grund av inbäddningen av kod- och innehållsunderpaket i behållarpaketet måste de inbäddade målsökvägarna läggas till i behållarprojektets `filter.xml`. Detta säkerställer att de inbäddade paketen inkluderas i behållarpaketet när de byggs.

Lägg bara till `<filter root="/apps/<my-app>-packages"/>`-posterna för mappar på andra nivån som innehåller underpaket som ska distribueras.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-container-package-filters) nedan för ett fullständigt fragment.

## Bädda in paket från tredje part {#embedding-3rd-party-packages}

Alla paket måste vara tillgängliga via databasen [Adobe offentliga Maven-artefakter](https://repo1.maven.org/maven2/com/adobe/) eller en tillgänglig offentlig, refererbar tredjepartsdatabas för Maven-artefakter.

Om tredjepartspaketen finns i **Adobe offentliga Maven-artefaktdatabasen** behövs ingen ytterligare konfiguration för att Adobe Cloud Manager ska kunna lösa artefakterna.

Om tredjepartspaketen finns i en **offentlig tredjepartsdatabas för Maven-felaktigheter** måste den här databasen registreras i projektets `pom.xml` och bäddas in enligt metoden [som beskrivs ovan](#embeddeds).

Tredjepartsprogram/-anslutningar bör bäddas in med dess `all`-paket som en behållare i projektets behållarpaket (`all`).

Om du lägger till Maven-beroenden följer standardMaven-rutiner, och inbäddning av tredjepartsartefakter (kod- och innehållspaket) [beskrivs ovan](#embedding-3rd-party-packages).

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-3rd-party-maven-repositories) nedan för ett fullständigt fragment.

## Paketberoenden mellan `ui.apps` från `ui.content`-paket {#package-dependencies}

För att paketen ska kunna installeras på rätt sätt rekommenderar vi att du skapar beroenden mellan paket.

Den allmänna regeln är paket som innehåller muterbart innehåll (`ui.content`) som ska vara beroende av den oföränderliga koden (`ui.apps`) som stöder återgivning och användning av det muterbara innehållet.

Ett betydande undantag från den här allmänna regeln är om det oföränderliga kodpaketet (`ui.apps` eller något annat), __only__, innehåller OSGi-paket. I så fall ska inget AEM deklarera ett beroende av det. Orsaken är att oföränderliga kodpaket som __endast__ innehåller OSGi-paket inte är registrerade med AEM [Package Manager](/help/implementing/developing/tools/package-manager.md). Alla AEM som är beroende av paketet är därför inte beroende av och kan inte installeras.

>[!TIP]
>
>Se avsnittet [POM XML-kodfragment](#xml-package-dependencies) nedan för ett fullständigt fragment.

De vanligaste mönstren för innehållspaketberoenden är:

### Enkla distributionspaketberoenden {#simple-deployment-package-dependencies}

I det enkla fallet anges att det `ui.content`-ändringsbara innehållspaketet ska vara beroende av det `ui.apps`-oföränderliga kodpaketet.

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

Projektstrukturerna och organisationen som beskrivs i den här artikeln är **fullständigt kompatibla** lokala AEM instanser.

## POM XML-kodfragment {#pom-xml-snippets}

Nedan följer Maven `pom.xml`-konfigurationsfragment som kan läggas till i Maven-projekt för att anpassa sig till ovanstående rekommendationer.

### Pakettyper {#xml-package-types}

Kod- och innehållspaket, som distribueras som underpaket, måste deklarera pakettypen **application** eller **content**, beroende på vad de innehåller.

#### Behållarpakettyper {#container-package-types}

Behållarprojektet `all/pom.xml` **deklarerar inte** en `<packageType>`.

#### Kodpakettyper (ej ändringsbara) {#immutable-package-types}

Kodpaket måste ange `packageType` till `application`.

I `ui.apps/pom.xml` deklarerar byggkonfigurationsdirektiven `<packageType>application</packageType>` för plugin-deklarationen `filevault-package-maven-plugin` pakettypen.

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

Innehållspaket måste ange `packageType` till `content`.

I `ui.content/pom.xml` deklarerar byggkonfigurationsdirektivet `<packageType>content</packageType>` för plugin-deklarationen `filevault-package-maven-plugin` pakettypen.

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

I alla projekt som genererar ett paket, **utom** för behållarprojektet (`all`), lägger du till `<cloudManagerTarget>none</cloudManagerTarget>` i `<properties>`-konfigurationen för plugin-deklarationen `filevault-package-maven-plugin` för att vara säker på att de **inte** distribueras av Adobe Cloud Manager. Behållarpaketet (`all`) ska vara ett enskilt paket som distribueras via Cloud Manager, vilket i sin tur bäddar in all nödvändig kod och alla nödvändiga innehållspaket.

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

Repo Init-skript som innehåller Repo Init-skript definieras i OSGi-fabrikskonfigurationen `RepositoryInitializer` via egenskapen `scripts`. Eftersom dessa skript definieras i OSGi-konfigurationer kan de enkelt omfångas i körningsläge med hjälp av det vanliga `../config.<runmode>`-mappsemantik.

Eftersom skript vanligtvis är flerradsdeklarationer är det enklare att definiera dem i filen `.config` än det JSON-baserade `.cfg.json`-formatet.

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

OSGi-egenskapen `scripts` innehåller direktiv enligt definitionen i [Apache Slings Repo Init-språk](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

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

### Bädda in delpaket i behållarpaketet {#xml-embeddeds}

I `all/pom.xml` lägger du till följande `<embeddeds>`-direktiv i plugin-deklarationen för `filevault-package-maven-plugin`. Kom ihåg att **inte** använder `<subPackages>`-konfigurationen. Orsaken är att det inkluderar delpaketen i `/etc/packages` i stället för `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

I `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) för projektet `all` inkluderar **alla** mappar som innehåller underpaket som ska distribueras: `-packages`

```xml
<filter root="/apps/my-app-packages"/>
```

Om flera `/apps/*-packages` används i de inbäddade målen måste alla räknas upp här.

### Maven Repositories från tredje part {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Om du lägger till fler Maven-databaser kan det ta längre tid att bygga maven när ytterligare Maven-databaser kontrolleras för beroenden.

I reaktorprojektets `pom.xml` lägger du till eventuella nödvändiga direktiv från tredje part för databasen Maven. Den fullständiga `<repository>`-konfigurationen bör vara tillgänglig från tredjepartsprovidern för databas.

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

### Paketberoenden mellan `ui.apps` från `ui.content`-paket {#xml-package-dependencies}

I `ui.content/pom.xml` lägger du till följande `<dependencies>`-direktiv i plugin-deklarationen för `filevault-package-maven-plugin`.

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

I `all/pom.xml` lägger du till plugin-programmet `maven-clean-plugin` som rensar målkatalogen före en Maven-konstruktion.

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
