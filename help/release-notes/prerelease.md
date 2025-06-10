---
title: Adobe Experience Manager as a Cloud Service Prerelease Channel
description: Lär dig hur du använder betaversionskanalen för att få en förhandsvisning av kommande funktioner i AEM as a Cloud Service.
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: 36da09746f02daad82875329b0aa53ee4eb7c074
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# Adobe Experience Manager as a Cloud Service Prerelease Channel {#prerelease-channel}

Lär dig hur du använder betaversionskanalen för att få en förhandsvisning av kommande funktioner i AEM as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager as a Cloud Service har nya funktioner på ett regelbundet besök. Listan över nya och kommande funktioner för en viss funktionsrelease finns i [versionsinformationen.](/help/release-notes/release-notes-cloud/release-notes-current.md)

Kommande funktioner är i allmänhet tillgängliga på ett av två sätt:

* Som en del av ett program för tidig användning
* Som en del av betaversionskanalen

I det här dokumentet beskrivs hur du aktiverar betaversionskanalen. Prerelease-kanalen ger tillgång till tidiga funktioner som kommer att lanseras i en framtida version av AEM. Detta ger er möjlighet att validera nya funktioner och planera för deras införande i förväg. I dokumentet [Versionsinformation för Adobe Experience Manager (AEM) as a Cloud Service](/help/release-notes/home.md) finns mer information om AEM releaseschema.

## Aktivera förhandsversionen av kanalen för åtkomst och Prova kommande funktioner {#enable-prerelease}

Prerelease-kanalen kan aktiveras i alla utvecklings- och sandlådemiljöer. Prerelease-kanalen kan inte aktiveras i staging- eller produktionsmiljöer.

Prerelease-kanalen kan nås på två olika sätt:

* [Molnmiljöer](#cloud-environments)
* [Lokal SDK](#local-sdk)

### Molnmiljöer {#cloud-environments}

Om du vill uppdatera en molnmiljö så att den använder prerelease-kanalen måste du lägga till en ny miljövariabel. Du kan göra detta antingen med Cloud Manager användargränssnitt eller via CLI.

#### Lägg till miljövariabel med användargränssnittet {#add-with-ui}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Navigera till programmet där du vill aktivera betaversionskanalen.

1. Välj den miljö där du vill aktivera betaversionskanalen och få åtkomst till dess konfiguration via **Program** > **Miljö** > **Miljökonfiguration**.

1. Lägg till en ny [miljövariabel](/help/implementing/cloud-manager/environment-variables.md)

   | Namn | Värde | Tjänsten används | Typ |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Alla | Variabel |

1. Spara ändringarna så uppdateras miljön med prerelease-kanalen aktiverad.

   ![Ny miljövariabel](assets/env-configuration-prerelease.png)

#### Lägg till miljövariabel med CLI {#add-with-cli}

Du kan också använda Cloud Manager API och CLI för att uppdatera miljövariablerna.

* Använd [Cloud Manager API:ts miljövariabelslutpunkt ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) och ange miljövariabeln `AEM_RELEASE_CHANNEL` till värdet `prerelease`.

  ```text
  PATCH /program/{programId}/environment/{environmentId}/variables
  [
          {
                  "name" : "AEM_RELEASE_CHANNEL",
                  "value" : "prerelease",
                  "type" : "string"
          }
  ]
  ```

* [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) kan också användas

  ```shell
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

Variabeln kan tas bort om du vill återställa miljön till standardbeteendet (icke-prerelease-kanal).

### Lokal SDK {#local-sdk}

Du kan komma åt kommande funktioner i prerelease-kanalen i din lokala QuickStart SDK och koda mot nya API:er genom att konfigurera ditt Maven-projekt så att det refererar till prerelease-kanalen `API Jar` som finns i Maven Central. Du kan också se hur du kommer åt betaversionskanalen i den lokala utvecklingsmiljön genom att starta den vanliga snabbstarten av SDK i förhandsversionsläge.

#### Starta Quickstart SDK i förhandsversionsläge {#prerelease-mode}

1. Hämta SDK från programvarudistribution och installera enligt beskrivningen i [Åtkomst till AEM as a Cloud Service SDK.](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. Ta med argumentet `-r prerelease` när du startar SDK Quickstart.

Värdet är fästigt så att det bara kan markeras vid första starten. Installera om SDK om du vill ändra kommandoradsalternativet.

Eftersom det kan finnas flera AEM-underhållsreleaser mellan de olika månadsversionerna kan du ladda ned dessa nya SDK:er och hänvisa till de nya SDK API Jar-versionerna i Maven-projekt. Underhållsreleaserna kommer inte att innehålla ytterligare förhandsversionsfunktioner, men kan innehålla andra mindre ändringar som felkorrigeringar, säkerhetskorrigeringar och prestandaförbättringar.
Javadocs publiceras i Maven Central.

#### Bygg mot prerelease SDK {#build-sdk}

1. Ändra maven-projektets `pom.xml` så att den refererar till en separat prerelease SDK API jar som publiceras i Maven Central. Den innehåller ett nytt Java-API för prerelease-funktionerna och är beroende av SDK API jar. Den har samma version.

   Här är ett exempel på ett utdrag från det överordnade elevens beroendehanteringsavsnitt som refererar till den vanliga API-behållaren:

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   Och sedan användningen i en modul:

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   Om du vill ändra till prerelease SDK ändrar du bara beroendet från `com.adobe.aem:aem-sdk-api` till `com.adobe.aem:aem-prerelease-sdk-api` enligt vad som anges nedan:

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   Som vanligt kan enskilda projekt använda beroendet.

1. Distribuera till den lokala servern.

1. Om du är säker på att den fungerar som förväntat lokalt, bekräftar du koden till en utvecklingsgren och använder en icke-produktionsprocess från Cloud Manager för att distribuera till en [miljö där prerelease-kanalen är aktiverad.](#cloud-environments)

>[!CAUTION]
> 
> ArtefactId `aem-prerelease-sdk-api` får aldrig användas vid distribution till scenen eller produktionen. Använd alltid `aem-sdk-api` när du distribuerar via produktionsflödet. Kod som refererar till prerelease-API:er ska inte heller distribueras via produktionsflödet.

[AEM CS SDK Build Analyzer maven plugin v1.0 och senare](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=sv-SE#developing) upptäcker om prerelease API används i ett projekt genom att undersöka beroendena. Om analysatorn hittar den kommer den att använda förhandsversionen av SDK-API:t för att analysera projektet.

## Överväganden {#considerations}

Det finns några saker att tänka på när du använder betaversionskanalen.

* Prerelease-kanalen innehåller inte nödvändigtvis alla nya funktioner som ska lanseras i följande version.
* Funktioner i betaversionen är strikta och avsedda att vara fullständiga snarare än betakvalitet. Om du märker några problem ska du rapportera dem, precis som du skulle göra om du misstänker att det finns fel i en vanlig AEM-release.
* Om du vill avgöra om en miljö har konfigurerats för betaversionskanalen går du till sidan **Om** för AEM-konsolen och kontrollerar om AEM versionsnummer innehåller ett `PRERELEASE`-suffix, till exempel `Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE`.

![Om](/help/release-notes/assets/about.png)
