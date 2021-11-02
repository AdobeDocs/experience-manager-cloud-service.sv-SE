---
title: Adobe Content Package Maven Plugin
description: Använd plugin-programmet Content Package Maven för att distribuera AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 4%

---

# Adobe Content Package Maven Plugin {#adobe-content-package-maven-plugin}

Använd pluginen Adobe Content Package Maven för att integrera paketets driftsättnings- och hanteringsuppgifter i dina Maven-projekt.

Distributionen av de konstruerade paketen till AEM utförs av pluginmodulen för innehållspaketet för Adobe och möjliggör automatisering av uppgifter som normalt utförs med AEM [Pakethanteraren:](/help/implementing/developing/tools/package-manager.md)

* Skapa nya paket från filer i filsystemet.
* Installera och avinstallera paket på AEM.
* Bygg paket som redan har definierats på AEM.
* Hämta en lista med paket som är installerade på AEM.
* Ta bort ett paket från AEM.

I det här dokumentet beskrivs hur du använder Maven för att hantera dessa uppgifter. Men det är också viktigt att förstå [hur AEM projekt och deras paket är strukturerade.](#aem-project-structure)

>[!NOTE]
>
>Paketskapandet ägs nu av [Apache Jackrabbit FileVault Package Maven plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin/). Distributionen av de konstruerade paketen till AEM utförs av plugin-programmet Maven för innehållspaket för Adobe enligt beskrivningen här.

## Paket och AEM projektstruktur {#aem-project-structure}

AEM as a Cloud Service följer de senaste metoderna för pakethantering och projektstruktur som implementerats av den senaste AEM Project Archetype.

>[!TIP]
>
>Mer information finns i [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) artikel i den AEM as a Cloud Service dokumentationen samt [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) dokumentation. Båda stöds fullt ut för AEM 6.5.

## Hämta innehållspaketet Maven Plugin {#obtaining-the-content-package-maven-plugin}

Plugin-programmet finns på [Maven Central Repository.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Innehållspaket Maven Plugin - mål och parametrar

Om du vill använda plugin-programmet Content Package Maven lägger du till följande plugin-element i build-elementet i din POM-fil:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Om du vill att Maven ska kunna hämta plugin-programmet använder du profilen i [Hämta innehållspaketet Maven Plugin](#obtaining-the-content-package-maven-plugin) på den här sidan.

## Mål för Innehållspaketet Maven Plugin {#goals-of-the-content-package-maven-plugin}

Mål- och målparametrarna som finns i innehållspaketets plugin-program beskrivs i följande avsnitt. Parametrar som beskrivs i avsnittet Vanliga parametrar kan användas för de flesta målen. Parametrar som gäller för ett mål beskrivs i avsnittet för det målet.

### Plugin-prefix {#plugin-prefix}

Plugin-prefixet är `content-package`. Använd det här prefixet för att köra ett mål från kommandoraden, som i följande exempel:

```shell
mvn content-package:build
```

### Parameterprefix {#parameter-prefix}

Om inget annat anges använder målen och parametrarna `vault` -prefix, som i följande exempel:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Mål där proxies används för AEM använder den första giltiga proxykonfigurationen som finns i inställningarna för Maven. Om ingen proxykonfiguration hittas används ingen proxy. Se `useProxy` -parametern i [Gemensamma parametrar](#common-parameters) -avsnitt.

### Gemensamma parametrar {#common-parameters}

Parametrarna i följande tabell är gemensamma för alla mål utom när de anges i **Mål** kolumn.

| Namn | Typ | Krävs | Standardvärde | Beskrivning | Mål |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | Nej | `false` | Värdet för `true` gör att bygget misslyckas när ett fel inträffar. Värdet för `false` gör att bygget ignorerar felet. | Alla mål utom `package` |
| `name` | `String` | `build`: Ja, `install`: Nej, `rm`: Ja | `build`: Ingen standard, `install`: Värdet för `artifactId` Maven-projektets egendom | Namnet på paketet som ska användas | Alla mål utom `ls` |
| `password` | `String` | Ja | `admin` | Lösenordet som används för autentisering med AEM | Alla mål utom `package` |
| `serverId` | `String` | Nej | Server-ID som användarnamn och lösenord för autentisering ska hämtas från | Alla mål utom `package` |
| `targetURL` | `String` | Ja | `http://localhost:4502/crx/packmgr/service.jsp` | URL:en för HTTP-tjänstens API för AEM | Alla mål utom `package` |
| `timeout` | `int` | Nej | `5` | Anslutningens timeout för kommunikation med pakethanterartjänsten, i sekunder | Alla mål utom `package` |
| `useProxy` | `boolean` | Nej | `true` | Värdet för `true` gör att Maven använder den första aktiva proxykonfigurationen som hittas för proxybegäranden till Package Manager. | Alla mål utom `package` |
| `userId` | `String` | Ja | `admin` | Användarnamnet som ska autentiseras med AEM | Alla mål utom `package` |
| `verbose` | `boolean` | Nej | `false` | Aktiverar eller inaktiverar utförlig loggning | Alla mål utom `package` |

### bygga {#build}

Skapar ett innehållspaket som redan har definierats på en AEM.

>[!NOTE]
>
>Detta mål behöver inte genomföras inom ett Maven-projekt.

#### Parametrar {#parameters}

Alla parametrar för byggmålet beskrivs i [Gemensamma parametrar](#common-parameters) -avsnitt.

### installera {#install}

Installerar ett paket i databasen. För att detta mål ska kunna uppnås krävs inget Maven-projekt. Målet är bundet till `install` Maven byggs livscykel.

#### Parametrar {#parameters-1}

Förutom följande parametrar finns beskrivningarna i [Gemensamma parametrar](#common-parameters) -avsnitt.

| Namn | Typ | Krävs | Standardvärde | Beskrivning |
|---|---|---|---|---|---|
| `artifact` | `String` | Nej | Värdet för `artifactId` Maven-projektets egendom | En sträng i formuläret `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | Nej | Inget | ID för den artefakt som ska installeras |
| `groupId` | `String` | Nej | Inget | The `groupId` av den artefakt som ska installeras |
| `install` | `boolean` | Nej | `true` | Avgör om paketet ska packas upp automatiskt när det överförs |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | Nej | Värdet för `localRepository` systemvariabel | Den lokala Maven-databasen som inte kan konfigureras med plugin-konfigurationen eftersom systemegenskapen alltid används |
| `packageFile` | `java.io.File` | Nej | Den primära artefakten som definieras för projektet Maven | Namnet på den paketfil som ska installeras |
| `packaging` | `String` | Nej | `zip` | Den typ av förpackning av artefakten som ska installeras |
| `pomRemoteRepositories` | `java.util.List` | Ja | Värdet för `remoteArtifactRepositories` egenskap som är definierad för projektet Maven | Det här värdet kan inte konfigureras med plugin-konfigurationen och måste anges i projektet. |
| `project` | `org.apache.maven.project.MavenProject` | Ja | Projektet som plugin-programmet är konfigurerat för | Maven-projektet som är implicit eftersom projektet innehåller plugin-konfigurationen |
| `repositoryId` (POM), `repoID` (kommandorad) | `String` | Nej | `temp` | ID för databasen som artefakten hämtas från |
| `repositoryUrl` (POM), `repoURL` (kommandorad) | `String` | Nej | Inget | URL:en för databasen som artefakten hämtas från |
| version | Sträng | Nej | Inget | Den version av artefakten som ska installeras |

### ls {#ls}

Visar de paket som distribuerats till [Pakethanteraren.](/help/implementing/developing/tools/package-manager.md)

#### Parametrar {#parameters-2}

Alla parametrar för ls-målet beskrivs i [Gemensamma parametrar](#common-parameters) -avsnitt.

### rm {#rm}

Tar bort ett paket från [Pakethanteraren.](/help/implementing/developing/tools/package-manager.md)

#### Parametrar {#parameters-3}

Alla parametrar för RM-målet beskrivs i [Gemensamma parametrar](#common-parameters) -avsnitt.

### avinstallera {#uninstall}

Avinstallerar ett paket. Paketet finns kvar på servern i avinstallerat läge.

#### Parametrar {#parameters-4}

Alla parametrar för avinstallationsmålet beskrivs i [Gemensamma parametrar](#common-parameters) -avsnitt.

### package {#package}

Skapar ett innehållspaket. Standardkonfigurationen för paketmålet omfattar innehållet i katalogen där kompilerade filer sparas. Körningen av paketmålet kräver att kompileringsfasen har slutförts. Paketmålet är bundet till paketfasen av bygglivscykeln för Maven.

#### Parametrar {#parameters-5}

Förutom följande parametrar finns mer information i beskrivningen av `name` -parametern i [Gemensamma parametrar](#common-parameters) -avsnitt.

| Namn | Typ | Krävs | Standardvärde | Beskrivning |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | Nej | Inget | Den arkivkonfiguration som ska användas |
| `builtContentDirectory` | `java.io.File` | Ja | Värdet på utdatakatalogen för Maven-bygget | Katalogen som innehåller innehållet som ska inkluderas i paketet |
| `dependencies` | `java.util.List` | Nej | Inget |  |
| `embeddedTarget` | `java.lang.String` | Nej | Inget |  |
| `embeddeds` | `java.util.List` | Nej | Inget |  |
| `failOnMissingEmbed` | `boolean` | Ja | `false` | Värdet för `true` gör att bygget misslyckas när en inbäddad artefakt inte hittas i projektberoendena. Värdet för `false` gör att sådana fel ignoreras. |
| `filterSource` | `java.io.File` | Nej | Inget | Den här parametern definierar en fil som anger källan för arbetsytefiltret. Filtren som anges i konfigurationen och injiceras via inbäddade eller underpaket sammanfogas med filinnehållet. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | Nej | Inget | Den här parametern innehåller filterelement som definierar paketinnehållet. När de körs inkluderas filtren i `filter.xml` -fil. Se [Använda filter](#using-filters) nedan. |
| `finalName` | `java.lang.String` | Ja | The `finalName` definieras i Maven-projektet (byggfasen) | Namnet på den genererade paketets ZIP-fil, utan `.zip` filtillägg |
| `group` | `java.lang.String` | Ja | The `groupID` definieras i projektet Maven | The `groupId` av det genererade innehållspaketet som är en del av målinstallationssökvägen för innehållspaketet |
| `outputDirectory` | `java.io.File` | Ja | Byggkatalogen som definieras i projektet Maven | Den lokala katalog där innehållspaketet sparas |
| `prefix` | `java.lang.String` | Nej | Inget |  |
| `project` | `org.apache.maven.project.MavenProject` | Ja | Inget | The Maven project |
| `properties` | `java.util.Map` | Nej | Inget | Dessa parametrar definierar ytterligare egenskaper som du kan ange i `properties.xml` -fil. Dessa egenskaper kan inte skriva över följande fördefinierade egenskaper: `group` (använd `group` parameter att ställa in), `name` (använd `name` parameter att ställa in), `version` (använd `version` parameter att ställa in), `description` (anges från projektbeskrivningen), `groupId` (`groupId` av projektbeskrivningen för Maven), `artifactId` (`artifactId` av projektbeskrivningen för Maven), `dependencies` (använd `dependencies` parameter att ställa in), `createdBy` (värdet på `user.name` system property), `created` (aktuell systemtid), `requiresRoot` (använd `requiresRoot` parameter att ställa in), `packagePath` (genereras automatiskt från grupp- och paketnamnet) |
| `requiresRoot` | `boolean` | Ja | false | Definierar om paketet kräver en rot. Det här kommer att bli `requiresRoot` egenskapen för `properties.xml` -fil. |
| `subPackages` | `java.util.List` | Nej | Inget |  |
| `version` | `java.lang.String` | Ja | Versionen som definierats i Maven-projektet | Innehållspaketets version |
| `workDirectory` | `java.io.File` | Ja | Den katalog som definieras i Maven-projektet (byggfasen) | Katalogen som innehåller innehållet som ska inkluderas i paketet |

#### Använda filter {#using-filters}

Använd elementet filters för att definiera paketinnehållet. Filtren läggs till i `workspaceFilter` -elementet i `META-INF/vault/filter.xml` paketets fil.

I följande filterexempel visas XML-strukturen som ska användas:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### Importläge {#import-mode}

The `mode` -elementet definierar hur innehåll i databasen påverkas när paketet importeras. Följande värden kan användas:

* **Sammanfoga:** Innehåll i paketet som inte redan finns i databasen läggs till. Innehåll som finns både i paketet och i databasen ändras inte. Inget innehåll tas bort från databasen.
* **Ersätt:** Innehåll i paketet som inte finns i databasen läggs till i databasen. Innehåll i databasen ersätts med matchande innehåll i paketet. Innehåll tas bort från databasen när den inte finns i paketet.
* **Uppdatering:** Innehåll i paketet som inte finns i databasen läggs till i databasen. Innehåll i databasen ersätts med matchande innehåll i paketet. Befintligt innehåll tas bort från databasen.

När filtret inte innehåller `mode` element, standardvärdet för `replace` används.

### help {#help}

#### Parametrar {#parameters-6}

| Namn | Typ | Krävs | Standardvärde | Beskrivning |
|---|---|---|---|---|
| `detail` | `boolean` | Nej | `false` | Avgör om alla inställningsbara egenskaper ska visas för varje mål |
| `goal` | `String` | Nej | Inget | Parametrarna definierar namnet på målet som hjälpen ska visas för. Om inget värde anges visas hjälpen för alla mål. |
| `indentSize` | `int` | Nej | `2` | Antalet blanksteg som ska användas för indrag för varje nivå (måste vara positivt om det är definierat) |
| `lineLength` | `int` | Nej | `80` | Den maximala längden för en visningsrad (måste vara positiv om den har definierats) |

## Inkludera en miniatyrbild eller egenskapsfil i paketet {#including-a-thumbnail-image-or-properties-file-in-the-package}

Ersätt standardpaketkonfigurationsfilerna för att anpassa paketegenskaperna. Ta till exempel med en miniatyrbild för att skilja på paketet i [Pakethanteraren.](/help/implementing/developing/tools/package-manager.md)

Källfilerna kan finnas var som helst i filsystemet. I POM-filen definierar du byggresurser som kopierar källfilerna till `target/vault-work/META-INF` för införande i förpackningen.

Följande POM-kod lägger till filerna i `META-INF` projektkällans mapp till paketet:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Följande POM-kod lägger bara till en miniatyrbild i paketet. Miniatyrbilden måste ha ett namn `thumbnail.png`och måste finnas i `META-INF/vault/definition` paketets mapp. I det här exemplet finns källfilen i `/src/main/content/META-INF/vault/definition` projektmapp:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Använda den AEM projekttypen för att generera AEM projekt {#using-archetypes}

Den senaste AEM Project Archetype implementerar paketstrukturen med bästa praxis för både lokala implementeringar och AMS-implementeringar och rekommenderas för alla AEM projekt.

>[!TIP]
>
>Mer information finns i [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) artikel i den AEM as a Cloud Service dokumentationen samt [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) dokumentation. Båda stöds fullt ut för AEM 6.5.
