---
title: Adobe Content Package Maven Plugin
description: Använd plugin-programmet Content Package Maven för att distribuera AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Adobe Content Package Maven Plugin {#adobe-content-package-maven-plugin}

Använd pluginen Adobe Content Package Maven för att integrera paketets driftsättnings- och hanteringsuppgifter i dina Maven-projekt.

Distributionen av de konstruerade paketen till AEM utförs av plugin-programmet Maven för innehållspaket för Adobe och möjliggör automatisering av åtgärder som normalt utförs med AEM [Package Manager](/help/implementing/developing/tools/package-manager.md)

* Skapa nya paket från filer i filsystemet.
* Installera och avinstallera paket på AEM.
* Bygg paket som redan har definierats på AEM.
* Hämta en lista med paket som är installerade på AEM.
* Ta bort ett paket från AEM.

I det här dokumentet beskrivs hur du använder Maven för att hantera dessa uppgifter. Men det är också viktigt att förstå [hur AEM projekt och deras paket är strukturerade](#aem-project-structure).

>[!NOTE]
>
>Använd alltid de senaste tillgängliga versionerna av dessa plugin-program.

>[!NOTE]
>
>Paketet **creation** ägs nu av plugin-programmet [Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/).
>
>I den här artikeln beskrivs **distributionen** för de konstruerade paket som ska AEM enligt Adobe Content Package Maven plugin.

## Paket och AEM projektstruktur {#aem-project-structure}

AEM as a Cloud Service följer de senaste metoderna för pakethantering och projektstruktur som implementerats av den senaste AEM Project Archetype.

>[!TIP]
>
>Se artikeln [AEM Projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) i AEM as a Cloud Service-dokumentationen och dokumentationen för [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html). Båda stöds fullt ut för AEM 6.5.

## Hämta innehållspaketet Maven Plugin {#obtaining-the-content-package-maven-plugin}

Plugin-programmet är tillgängligt från [Maven Central Repository](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public).

## Innehållspaket Maven Plugin - mål och parametrar

Om du vill använda plugin-programmet Content Package Maven lägger du till följande plugin-element i build-elementet i din POM-fil:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Om du vill att Maven ska kunna hämta plugin-programmet använder du profilen som finns i avsnittet [Hämtning av innehållspaketets plugin](#obtaining-the-content-package-maven-plugin) på den här sidan.

## Mål för Innehållspaketet Maven Plugin {#goals-of-the-content-package-maven-plugin}

Mål- och målparametrarna som finns i innehållspaketets plugin-program beskrivs i följande avsnitt. Parametrar som beskrivs i avsnittet Vanliga parametrar kan användas för de flesta målen. Parametrar som gäller för ett mål beskrivs i avsnittet för det målet.

### Plugin-prefix {#plugin-prefix}

Insticksprefixet är `content-package`. Använd det här prefixet för att köra ett mål från kommandoraden, som i följande exempel:

```shell
mvn content-package:build
```

### Parameterprefix {#parameter-prefix}

Om inget annat anges använder målen och parametrarna för plugin-programmet prefixet `vault`, som i följande exempel:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Mål där proxies används för AEM använder den första giltiga proxykonfigurationen som finns i inställningarna för Maven. Om ingen proxykonfiguration hittas används ingen proxy. Se parametern `useProxy` i avsnittet [Vanliga parametrar](#common-parameters).

### Gemensamma parametrar {#common-parameters}

Parametrarna i följande tabell är gemensamma för alla mål utom när de anges i kolumnen **Mål** .

| Namn | Typ | Obligatoriskt | Standardvärde | Beskrivning | Mål |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | Nej | `false` | Värdet `true` gör att bygget misslyckas när ett fel inträffar. Värdet `false` gör att felet ignoreras. | Alla mål utom `package` |
| `name` | `String` | `build`: Ja, `install`: Nej, `rm`: Ja | `build`: Inget standardvärde, `install`: Värdet för egenskapen `artifactId` i Maven-projektet | Namnet på paketet som ska användas | Alla mål utom `ls` |
| `password` | `String` | Ja | `admin` | Lösenordet som används för autentisering med AEM | Alla mål utom `package` |
| `serverId` | `String` | Nej | Server-ID som användarnamn och lösenord för autentisering ska hämtas från | Alla mål utom `package` |
| `targetURL` | `String` | Ja | `http://localhost:4502/crx/packmgr/service.jsp` | URL:en för HTTP-tjänstens API för AEM | Alla mål utom `package` |
| `timeout` | `int` | Nej | `5` | Anslutningens timeout för kommunikation med pakethanterartjänsten, i sekunder | Alla mål utom `package` |
| `useProxy` | `boolean` | Nej | `true` | Värdet `true` gör att Maven använder den första aktiva proxykonfigurationen som hittas för proxybegäranden till Package Manager. | Alla mål utom `package` |
| `userId` | `String` | Ja | `admin` | Användarnamnet som ska autentiseras med AEM | Alla mål utom `package` |
| `verbose` | `boolean` | Nej | `false` | Aktiverar eller inaktiverar utförlig loggning | Alla mål utom `package` |

### bygg {#build}

Skapar ett innehållspaket som redan har definierats på en AEM.

>[!NOTE]
>
>Detta mål behöver inte genomföras inom ett Maven-projekt.

#### Parametrar {#parameters}

Alla parametrar för byggmålet beskrivs i avsnittet [Vanliga parametrar](#common-parameters).

### installera {#install}

Installerar ett paket i databasen. För att detta mål ska kunna uppnås krävs inte något Maven-projekt. Målet är bundet till `install`-fasen av Maven-byggets livscykel.

#### Parametrar {#parameters-1}

Förutom följande parametrar kan du läsa beskrivningarna i avsnittet [Vanliga parametrar](#common-parameters) .

| Namn | Typ | Obligatoriskt | Standardvärde | Beskrivning |
|---|---|---|---|---|
| `artifact` | `String` | Nej | Värdet för egenskapen `artifactId` i Maven-projektet | En sträng med formatet `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | Nej | Ingen | ID för den artefakt som ska installeras |
| `groupId` | `String` | Nej | Ingen | `groupId` för den artefakt som ska installeras |
| `install` | `boolean` | Nej | `true` | Avgör om paketet ska packas upp automatiskt när det överförs |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | Nej | Värdet för systemvariabeln `localRepository` | Den lokala Maven-databasen som inte kan konfigureras med plugin-konfigurationen eftersom systemegenskapen alltid används |
| `packageFile` | `java.io.File` | Nej | Den primära artefakten som definieras för projektet Maven | Namnet på den paketfil som ska installeras |
| `packaging` | `String` | Nej | `zip` | Den typ av förpackning av artefakten som ska installeras |
| `pomRemoteRepositories` | `java.util.List` | Ja | Värdet för egenskapen `remoteArtifactRepositories` som är definierad för projektet Maven | Det här värdet kan inte konfigureras med plugin-konfigurationen och måste anges i projektet. |
| `project` | `org.apache.maven.project.MavenProject` | Ja | Projektet som plugin-programmet är konfigurerat för | Maven-projektet som är implicit eftersom projektet innehåller plugin-konfigurationen |
| `repositoryId` (POM), `repoID` (kommandorad) | `String` | Nej | `temp` | ID för databasen som artefakten hämtas från |
| `repositoryUrl` (POM), `repoURL` (kommandorad) | `String` | Nej | Ingen | URL:en för databasen som artefakten hämtas från |
| version | Sträng | Nej | Ingen | Den version av artefakten som ska installeras |

### ls {#ls}

Visar de paket som har distribuerats till [Package Manager](/help/implementing/developing/tools/package-manager.md).

#### Parametrar {#parameters-2}

Alla parametrar för ls-målet beskrivs i avsnittet [Vanliga parametrar](#common-parameters).

### rm {#rm}

Tar bort ett paket från [Package Manager](/help/implementing/developing/tools/package-manager.md).

#### Parametrar {#parameters-3}

Alla parametrar för RM-målet beskrivs i avsnittet [Vanliga parametrar](#common-parameters).

### avinstallera {#uninstall}

Avinstallerar ett paket. Paketet finns kvar på servern i avinstallerat läge.

#### Parametrar {#parameters-4}

Alla parametrar för avinstallationsmålet beskrivs i avsnittet [Vanliga parametrar](#common-parameters).


### help {#help}

#### Parametrar {#parameters-6}

| Namn | Typ | Obligatoriskt | Standardvärde | Beskrivning |
|---|---|---|---|---|
| `detail` | `boolean` | Nej | `false` | Avgör om alla inställningsbara egenskaper ska visas för varje mål |
| `goal` | `String` | Nej | Ingen | Parametrarna definierar namnet på målet som hjälpen ska visas för. Om inget värde anges visas hjälpen för alla mål. |
| `indentSize` | `int` | Nej | `2` | Antalet blanksteg som ska användas för indrag för varje nivå (måste vara positivt om det är definierat) |
| `lineLength` | `int` | Nej | `80` | Den maximala längden för en visningsrad (måste vara positiv om den har definierats) |

## Inkludera en miniatyrbild eller egenskapsfil i paketet {#including-a-thumbnail-image-or-properties-file-in-the-package}

Ersätt standardpaketkonfigurationsfilerna för att anpassa paketegenskaperna. Ta till exempel med en miniatyrbild för att skilja på paketet i [Pakethanteraren](/help/implementing/developing/tools/package-manager.md).

Källfilerna kan finnas var som helst i filsystemet. I POM-filen definierar du byggresurser som kopierar källfilerna till `target/vault-work/META-INF` för inkludering i paketet.

Följande POM-kod lägger till filerna i mappen `META-INF` i projektkällan i paketet:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Följande POM-kod lägger bara till en miniatyrbild i paketet. Miniatyrbilden måste ha namnet `thumbnail.png` och finnas i mappen `META-INF/vault/definition` i paketet. I det här exemplet finns källfilen i mappen `/src/main/content/META-INF/vault/definition` i projektet:

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
>Se artikeln [AEM Projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) i AEM as a Cloud Service-dokumentationen och dokumentationen för [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html). Båda stöds fullt ut för AEM 6.5.
