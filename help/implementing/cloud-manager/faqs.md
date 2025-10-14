---
title: Vanliga frågor om Cloud Manager
description: Svar på de vanligaste frågorna om Cloud Manager i AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---


# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Det här dokumentet innehåller svar på de vanligaste frågorna om Cloud Manager i AEM as a Cloud Service.

## Går det att använda Java™ 11 med Cloud Manager-byggen? {#java-11-cloud-manager}

Ja. Lägg till `maven-toolchains-plugin` med rätt inställningar för Java™ 11.

Processen är dokumenterad - se [Guiden Skapa projekt](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

Se till exempel exempelprojektkoden [ för ](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)WKND.

## Mitt bygge misslyckas med ett fel om maven-scr-plugin efter byte från Java™ 8 till Java™ 11. Vad kan jag göra? {#build-fails-maven-scr-plugin}

Ditt AEM Cloud Manager-bygge kan misslyckas när du försöker byta från Java™ 8 till 11. Om följande fel inträffar måste du ta bort `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 > [Help 1]
```

Instruktioner om hur du tar bort det här plugin-programmet finns i [Från SCR-anteckningar till OSGI-anteckningar](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/).

## Mitt bygge misslyckas med ett fel om RequireJavaVersion efter byte från Java™ 8 till Java™ 11. Vad kan jag göra? {#build-fails-requirejavaversion}

För Cloud Manager-byggen kan `maven-enforcer-plugin` misslyckas med det här felet.

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

Felet är känt eftersom Cloud Manager använder en annan version av Java™ för att köra kommandot Maven jämfört med att kompilera kod. Utelämna helt enkelt `requireJavaVersion` från dina `maven-enforcer-plugin`-konfigurationer.

## Kodkvalitetskontrollen misslyckades och distributionen stoppas. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Ja. Alla fel i kodkvalitetskontrollen utom säkerhetsklassificeringen är icke-kritiska mått. Det innebär att de kan kringgås som en del av en distributionsprocess genom att objekten i resultatgränssnittet expanderas.

En användare med rollen [Distributionshanterare, Project Manager eller Business Owner](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles) kan åsidosätta problemen. I så fall fortsätter rörledningen eller så kan de acceptera problemen. I så fall upphör rörledningen med ett fel.

Mer information finns i dokumenten [Kodkvalitetstestning](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate) och [Konfigurera icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines).

## Kan jag använda SNAPSHOT för versionen av Maven-projektet? {#use-snapshot}

Ja. För utvecklardistributioner måste Git-grenen `pom.xml`-filerna innehålla `-SNAPSHOT` i slutet av `<version>`-värdet.

Med det här värdet kan efterföljande distribution installeras stilla när versionen inte ändras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

Du kan också ange versionen till `-SNAPSHOT` för fas- och produktionsbyggen eller distributioner. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg i Git. Denna tagg kan vid behov hänvisas till senare.

Mer information om versionshantering finns i [Hantering av maven-projektversioner](/help/implementing/cloud-manager/managing-code/project-version-handling.md).

## Hur fungerar paketering och paketversionshantering för driftsättning av faser och produktioner? {#snapshot-version}

I scen- och produktionsdistributioner genereras en automatisk version - se [Hantering av projektversioner i Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md).

För anpassad versionshantering i scen- och produktionsdistributioner anger du en korrekt 3-delsversion som `1.0.0`. Öka versionen varje gång du distribuerar till produktionen.

Cloud Manager lägger automatiskt till sin version i scen- och produktionsbyggen och skapar en Git-gren. Ingen särskild konfiguration krävs. Om du inte ställer in en maven-version enligt beskrivningen ovan lyckas distributionen ändå och en version ställs in automatiskt.

## Min maven-konstruktion misslyckas för Cloud Manager-distributioner men den byggs lokalt utan fel. Vad är det för fel? {#maven-build-fail}

Mer information finns i [den här Git-resursen](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md).

## Vad gör jag om en Cloud Manager-distribution misslyckas vid driftsättningen i AEM as a Cloud Service? {#cloud-manager-deployment-cloud-service}

Den vanligaste orsaken till att en distribution misslyckas beror på otillräcklig behörighet för användaren `sling-distribution-importer`. I sådana fall misslyckas distributionssteget under en Cloud Manager-distribution och fel som följande genereras.

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

Användaren `sling-distribution-importer` behöver ytterligare behörigheter för innehållssökvägarna som definieras i `ui.content package`. Den här regeln innebär vanligtvis att du måste lägga till behörigheter för både `/conf` och `/var`.

Lösningen är att lägga till ett [RepositoryInitializer OSGi-konfigurationsskript](/help/implementing/deploying/overview.md#repoint) i programdistributionspaketet för att lägga till åtkomstkontrollistor för användaren `sling-distribution-importer`.

I föregående exempelfel innehåller paketet `myapp-base.ui.content-*.zip` innehåll under `/conf` och `/var/workflow`. För att distributionen ska lyckas krävs behörigheter för `sling-distribution-importer` under dessa sökvägar.

Här är ett exempel på en [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) OSGi-konfiguration som lägger till ytterligare behörigheter för användaren `sling-distribution-importer`. Konfigurationen lägger till behörigheter under `/var`. En sådan konfiguration måste läggas till i programpaketet under `/apps/myapp/config` (där `myapp` är den mapp där programkoden lagras).

## Min Cloud Manager-distribution misslyckas vid distributionssteget i AEM as a Cloud Service och jag har redan lagt till en RepositoryInitializer OSGi-konfiguration. Vad mer kan jag göra? {#build-failures}

Om [tillägget av en OSGi-konfiguration för RepositoryInitializer](#cloud-manager-deployment-cloud-service) inte löste felet kan det bero på något av dessa ytterligare problem.

* Distributionen kan misslyckas på grund av en felaktig OSGi-konfiguration som bryter en körklar tjänst.
   * Kontrollera loggarna under distributionen så att du kan se om det finns några uppenbara fel.

* Distributionen kan misslyckas på grund av felaktiga Dispatcher- eller Apache-konfigurationer.
   * Testa dina Apache- och Dispatcher-konfigurationer lokalt med Docker-bilden som ingår i SDK.
   * Se [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md#content-delivery) om hur du konfigurerar Dispatcher Docker-behållaren för enkel lokal testning.

* Distributionen kan misslyckas på grund av ett annat fel under replikering av innehållspaketen (Sling-distribution) från författaren till publiceringsinstanser.
   * Följ de här stegen för att simulera problemet i en lokal konfiguration.
      1. Installera en författare och en Publish-instans lokalt med de senaste AEM SDK-burkarna.
      1. Logga in på författarinstansen.
      1. Gå till **Verktyg** > **Distribution** > **Distribution**.
      1. Distribuera innehållspaketen som är en del av kodbasen och se om kön blockeras med ett fel.

## Jag kan inte ange en variabel med ett aio-kommando. Vad kan jag göra? {#set-variable}

Du kan få ett `403`-fel som följande när du försöker lista eller ange pipeline-variabler med hjälp av `aio`-kommandon.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

I det här fallet måste användaren som kör dessa kommandon läggas till i rollen **Distributionshanteraren** i Admin Console.

Mer information finns i [API-behörigheter](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/).
