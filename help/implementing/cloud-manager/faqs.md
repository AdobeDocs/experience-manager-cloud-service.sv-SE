---
title: Vanliga frågor om Cloud Manager
description: Hitta svar på de vanligaste frågorna om Cloud Manager på AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---


# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Det här dokumentet ger svar på de vanligaste frågorna om Cloud Manager på AEM as a Cloud Service.

## Går det att använda Java™ 11 med Cloud Manager-byggen? {#java-11-cloud-manager}

Ja. Lägg till `maven-toolchains-plugin` med rätt inställningar för Java™ 11.

Processen är dokumenterad [här](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

Se till exempel [projektets exempelprojektkod](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## Mitt bygge misslyckas med ett fel om maven-scr-plugin efter byte från Java™ 8 till Java™ 11. Vad kan jag göra? {#build-fails-maven-scr-plugin}

AEM Cloud Manager-bygget kan misslyckas när du försöker byta från Java™ 8 till 11. Om följande fel uppstår måste du ta bort `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Instruktioner om hur du tar bort det här plugin-programmet finns i [här](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/).

## Mitt bygge misslyckas med ett fel om RequireJavaVersion efter byte från Java™ 8 till Java™ 11. Vad kan jag göra? {#build-fails-requirejavaversion}

För Cloud Manager-byggen `maven-enforcer-plugin` kan misslyckas med det här felet.

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

Felet är känt eftersom Cloud Manager använder en annan version av Java™ för att köra maven-kommandot jämfört med att kompilera kod. Bara utelämna `requireJavaVersion` från `maven-enforcer-plugin` konfigurationer.

## Kodkvalitetskontrollen misslyckades och distributionen stoppas. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Ja. Alla fel i kodkvalitetskontrollen utom säkerhetsklassificeringen är icke-kritiska mått, så de kan kringgås som en del av en distributionskanal genom att objekten i resultatgränssnittet expanderas.

En användare med [Distributionshanteraren, Project Manager eller Business Owner](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles) rollerna kan åsidosätta problemen. I så fall fortsätter pipelinen eller så kan de acceptera problemen. I så fall upphör pipeline med ett fel.

Se dokumenten [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate) och [Konfigurera icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines) för mer information.

## Kan jag använda SNAPSHOT för versionen av Maven-projektet? {#use-snapshot}

Ja. Git-grenen för utvecklardistributioner `pom.xml` måste innehålla `-SNAPSHOT` i slutet av `<version>` värde.

Med det här värdet kan efterföljande distribution fortfarande installeras när versionen inte ändras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

Du kan också ange versionen till `-SNAPSHOT` för byggen eller driftsättningarna av faser och produktion. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg åt dig i Git. Denna tagg kan vid behov hänvisas till senare.

Mer information om versionshantering finns i [dokumenteras här](/help/implementing/cloud-manager/managing-code/project-version-handling.md).

## Hur fungerar paketering och paketversionshantering för driftsättning av faser och produktioner? {#snapshot-version}

I fas- och produktionsdistributioner genereras en automatisk version som [dokumenteras här](/help/implementing/cloud-manager/managing-code/project-version-handling.md).

För anpassad versionshantering i scen- och produktionsinstallationer ställer du in en korrekt version med tre delar som `1.0.0`. Öka versionen varje gång du distribuerar till produktionen.

Cloud Manager lägger automatiskt till sin version i scen- och produktionsbyggen och skapar en Git-gren. Ingen särskild konfiguration krävs. Om du inte ställer in en maven-version enligt beskrivningen ovan lyckas distributionen ändå och en version ställs in automatiskt.

## Min maven-konstruktion misslyckas för distributioner av Cloud Manager, men den byggs lokalt utan fel. Vad är det för fel? {#maven-build-fail}

Se [den här Git-resursen](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) för mer information.

## Vad gör jag om en Cloud Manager-distribution misslyckas vid distributionssteget på AEM as a Cloud Service? {#cloud-manager-deployment-cloud-service}

Den vanligaste orsaken till att en distribution misslyckas beror på otillräcklig behörighet för `sling-distribution-importer` användare. I sådana fall misslyckas distributionssteget under en Cloud Manager-distribution och fel som följande genereras.

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

The `sling-distribution-importer` användaren behöver ytterligare behörigheter för innehållssökvägarna som definieras i `ui.content package`. Den här regeln innebär vanligtvis att du måste lägga till behörigheter för båda `/conf` och `/var`.

Lösningen är att lägga till en [RepositoryInitializer OSGi-konfiguration](/help/implementing/deploying/overview.md#repoint) skript i programdistributionspaketet för att lägga till åtkomstkontrollistor för `sling-distribution-importer` användare.

I föregående exempelfel är paketet `myapp-base.ui.content-*.zip` innehåller innehåll under `/conf` och `/var/workflow`. Behörigheter för `sling-distribution-importer` under dessa banor behövs.

Här är ett exempel på en [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) OSGi-konfiguration som lägger till ytterligare behörigheter för `sling-distribution-importer` användare. Konfigurationen lägger till behörigheter under `/var`. En sådan konfiguration måste läggas till i programpaketet under `/apps/myapp/config` (där myapp är den mapp där programkoden lagras).

## Distributionen av min Cloud Manager misslyckas vid distributionssteget i AEM as a Cloud Service och jag har redan lagt till en OSGi-konfiguration för RepositoryInitializer. Vad mer kan jag göra? {#build-failures}

If [lägga till en RepositoryInitializer OSGi-konfiguration](#cloud-manager-deployment-cloud-service) inte löste felet, det kan bero på något av dessa ytterligare problem.

* Distributionen kan misslyckas på grund av en felaktig OSGi-konfiguration som bryter en färdig tjänst.
   * Kontrollera loggarna under distributionen så att du kan se om det finns några uppenbara fel.

* Distributionen kan misslyckas på grund av felaktiga Dispatcher- eller Apache-konfigurationer.
   * Testa dina Apache- och Dispatcher-konfigurationer lokalt med den Docker-bild som ingår i SDK:n.
   * Se [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md#content-delivery) om hur du konfigurerar Dispatcher Docker-behållaren för enkel lokal testning.

* Distributionen kan misslyckas på grund av ett annat fel under replikering av innehållspaketen (Sling-distribution) från författaren till publiceringsinstanser.
   * Följ de här stegen för att simulera problemet i en lokal konfiguration.
      1. Installera en författare och publicera instansen lokalt med de senaste AEM SDK-burkarna.
      1. Logga in på författarinstansen.
      1. Gå till **verktyg** -> **Distribution** -> **Distribution**.
      1. Distribuera innehållspaketen som är en del av kodbasen och se om kön blockeras med ett fel.

## Jag kan inte ange en variabel med ett aio-kommando. Vad kan jag göra? {#set-variable}

Du kan få en `403` fel som följande när du försöker lista eller ange pipeline-variabler med hjälp av `aio` kommandon.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

I det här fallet måste användaren som kör dessa kommandon läggas till i **Distributionshanteraren** i Admin Console.

Se [API-behörigheter](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/) för mer information.
