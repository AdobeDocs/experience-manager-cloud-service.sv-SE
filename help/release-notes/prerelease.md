---
title: '"[!DNL Adobe Experience Manager] as a Cloud Service prerelease Channel"'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service prerelease Channel"'
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: c2f0b9c904374b5e59ce2b2f268fdd73dfdbfd21
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] as a Cloud Service prerelease Channel {#prerelease-channel}


## Introduktion {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service levererar nya funktioner på månadsbasis, enligt schemat [Experience Manager släpper färdplan](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service). För att bekanta sig med de funktioner som kommer att bli tillgängliga nästa månad kan kunderna prenumerera på betaversionskanalen, som nås genom att konfigurera i standardprogramutvecklingsmiljöer eller i sandlådeprogrammiljöer på lämpligt sätt. Kunderna kan förhandsgranska ändringar i Sites-konsolen samt bygga kod mot nya prerelease-API:er.

Listan över förhandsversionsfunktioner för en viss månad publiceras i [månadsversionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Aktivera förhandsversionen {#enable-prerelease}

Förhandsversionsfunktionerna kan användas på olika sätt:

* Molnmiljöer (standardprogramutvecklingsmiljöer eller sandlådeprogrammiljötyper)
* Lokal SDK

### Molnmiljöer {#cloud-environments}

Om du vill uppdatera en molnmiljö så att den använder förhandsversionen lägger du till en ny [miljövariabel](../implementing/cloud-manager/environment-variables.md) med hjälp av användargränssnittet för miljökonfiguration i Cloud Manager:

1. Navigera till **Program** > **Miljö** > **Miljökonfiguration** du vill uppdatera.
1. Lägg till en ny [miljövariabel](../implementing/cloud-manager/environment-variables.md):

   | Namn | Värde | Tjänsten används | Typ |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Alla | Variabel |

1. Spara ändringarna så uppdateras miljön med prerelease-funktionen aktiverad.

   ![Ny miljövariabel](assets/env-configuration-prerelease.png)


**Alternativt** kan du använda Cloud Manager API och CLI för att uppdatera systemvariablerna:

* Använd [Slutpunkt för miljövariablerna i API:t för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables), ange **AEM_RELEASE_CHANNEL** miljövariabel till värdet **prerelease**.

   ```
   PATCH /program/{programId}/environment/{environmentId}/variables
   [
           {
                   "name" : "AEM_RELEASE_CHANNEL",
                   "value" : "prerelease",
                   "type" : "string"
           }
   ]
   ```

* CLI:n för Cloud Manager kan även användas enligt instruktionerna på [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)

   ```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


Variabeln kan tas bort eller återställas till ett annat värde om du vill att miljön ska återställas till det vanliga (ej prerelease) kanalens beteende.

### Lokal SDK {#local-sdk}

Du kan se nya funktioner i Sites-konsolen i den lokala QuickStart SDK och koda mot nya API:er i förhandsversionen genom att låta din maven-projektreferens vara förhandsversionen `API Jar` i Maven Central. Du kan även se de här förhandsversionsfunktionerna på den lokala datorn genom att starta den vanliga QuickStart SDK i förhandsversionsläge:

* Hämta SDK från programdistributionsportalen och installera enligt beskrivningen i [Åtkomst till AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).
* Inkludera argumentet när du startar SDK QuickStart `-r prerelease`.
* Värdet är *klibbig* så att den bara kan väljas vid första starten. Installera om SDK för att ändra kommandoradsalternativet.

Eftersom det kan finnas flera AEM underhållsreleaser mellan de olika månadsvisa funktionsreleaserna kan du ladda ned dessa nya SDK och hänvisa till de nya Jar-versionerna av SDK API i större projekt. Underhållsreleaserna kommer inte att innehålla ytterligare förhandsversionsfunktioner, men kan innehålla andra mindre ändringar som felkorrigeringar, säkerhetskorrigeringar och prestandaförbättringar.
Javadocs publiceras i Maven Central.

Så här bygger du mot betaversionen av SDK:

1. modifiera maven-projektets pom.xml för att hänvisa till en speciell prerelease sdk api jar som publiceras i Maven central. Den innehåller nya Java api för prerelease-funktionerna och är beroende av sdk api jar. Den har samma version.

   Här är ett exempel på ett utdrag från det överordnade rummets beroendehanteringsavsnitt som refererar till det vanliga API-JAR:

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

   Ändra bara beroendet från `com.adobe.aem:aem-sdk-api` till `com.adobe.aem:aem-prerelease-sdk-api` enligt vad som anges nedan:

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

1. Distribuera till din lokala server
1. Om du är säker på att det fungerar som väntat lokalt, bekräftar du koden till en utvecklingsgren och använder ett icke-produktionsflöde i Cloud Manager för att distribuera till en miljö som prenumererar på betaversionskanalen

>[!CAUTION]
> 
> The `aem-prerelease-sdk-api` artifactId får aldrig användas vid distribution till Stage eller Production. Använd alltid aem-sdk-api när du distribuerar via produktionskanalen. Kod som refererar till prerelease-API:er ska inte heller distribueras via produktionskanalen.

The [AEM CS SDK build Analyzer maven plugin v1.0 och senare](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) identifierar om prerelease API används i ett projekt genom att undersöka beroendena. Om analyseraren hittar den använder den prerelease sdk api för att analysera projektet.

## Överväganden {#considerations}

Det finns några saker att tänka på när det gäller prerelease-kanalen:

* Vissa funktioner som kommer att lanseras i nästa månadsutgåva kanske inte ingår i prerelease-kanalen.
* Funktioner i betaversionen är strikta och avsedda att vara fullständiga snarare än betakvalitet. Om du upptäcker några problem ska du rapportera dem, precis som du skulle göra om du misstänker att det finns fel i en vanlig AEM.
* Om du vill avgöra om en miljö är konfigurerad för betaversionskanalen går du till AEM Console **Om** och kontrollera om AEM innehåller en *prerelease* suffix som ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![om](/help/release-notes/assets/about.png)
