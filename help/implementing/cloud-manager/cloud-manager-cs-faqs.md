---
title: Vanliga frågor om Cloud Manager
description: Hitta svar på de vanligaste frågorna om Cloud Manager på AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 11ac22974524293ce3e4ceaa26e59fe75ea387e6
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---


# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Det här dokumentet innehåller svar på de vanligaste frågorna om Cloud Manager på AEM as a Cloud Service.

## Går det att använda Java 11 med Cloud Manager-byggen? {#java-11-cloud-manager}

AEM Cloud Manager-bygget kan misslyckas när du försöker byta från Java 8 till 11. Problemet kan ha många orsaker och de vanligaste är beskrivna i det här avsnittet.

* Lägg till `maven-toolchains-plugin` med rätt inställningar för Java 11.
   * Detta dokumenteras [här](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).
   * Se till exempel [projektets exempelprojektkod](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Om följande fel uppstår måste du ta bort `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar.
   * Instruktioner finns i [här.](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   ```text
   [main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
   ```

* För Cloud Manager-byggen `maven-enforcer-plugin` misslyckas med fel `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Det här är ett känt fel som beror på att Cloud Manager använder en annan version av Java för att köra maven-kommandot jämfört med att kompilera kod. Utelämna för tillfället `requireJavaVersion` från `maven-enforcer-plugin` konfigurationer.

## Kodkvalitetskontrollen misslyckades och distributionen stoppas. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Alla fel i kodkvalitetskontrollen utom säkerhetsklassificeringen är icke-kritiska mått, så de kan kringgås genom att objekten i resultatgränssnittet expanderas.

En användare i [Distributionshanteraren, programhanteraren eller affärsägaren](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md) roll kan åsidosätta problemen, och i så fall fortsätter pipeline. Användningarna kan också acceptera problemen, och i så fall upphör pipeline med ett fel.

Se dokumentet [Testning av kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md) för mer information.

## Kan jag använda SNAPSHOT för versionen av Maven-projektet? Hur fungerar versionshantering av paketen och källfilerna för driftsättning av scener och produktion? {#snapshot-version}

Följande scenarier gäller versionshantering av paket- och paketburar-filer för driftsättning av scener och produktion.

* Git-grenen för utvecklardistributioner `pom.xml` måste innehålla `-SNAPSHOT` i slutet av `<version>` värde.
   * Detta gör att efterföljande distribution fortfarande kan installeras när versionen inte ändras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

* I fas- och produktionsdistributioner genereras en automatisk version som [dokumenteras här.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

* För anpassad versionshantering i scen- och produktionsinstallationer ställer du in en korrekt version med tre delar som `1.0.0`. Öka versionen varje gång du distribuerar till produktionen.

* Cloud Manager lägger automatiskt till sin version i scen- och produktionsbyggen och skapar en Git-gren. Ingen särskild konfiguration krävs. Om du inte ställer in en maven-version enligt beskrivningen ovan kommer distributionen fortfarande att lyckas och en version ställs in automatiskt.

* Du kan ställa in versionen på `-SNAPSHOT` för byggen och driftsättningar utan problem. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg åt dig i Git. Om det behövs kan du hänvisa till den här taggen senare.

* Om du vill testa experimentell kod i en utvecklingsmiljö kan du skapa en ny Git-gren och ställa in pipeline så att den grenen används.
   * Detta är användbart när distributioner misslyckas och du vill testa med äldre versioner av koden för att avgöra vilken ändring som orsakade felet.

   * Git-kommandot nedan skapar en fjärrgren med namnet `testbranch1` baserat på den befintliga implementeringen `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Den här grenen kan användas i Cloud Manager utan att påverka andra grenar.

   ```shell
   git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1
   ```

   * Se [git-dokumentation](https://git-scm.com/book/en/v2/Git-Internals-Git-References) för mer information.

   * Om du vill ta bort testgrenen senare använder du kommandot delete:

   ```shell
   git push origin --delete testbranch1
   ```

## Min maven-konstruktion misslyckas för distributioner av Cloud Manager, men den byggs lokalt utan fel. Vad är det för fel? {#maven-build-fail}

Se [Git-resurs](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) för mer information.

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

I det här fallet `sling-distribution-importer` användaren behöver ytterligare behörigheter för innehållssökvägarna som definieras i `ui.content package`.  Det innebär vanligtvis att du måste lägga till behörigheter för båda `/conf` och `/var`.

Lösningen är att lägga till en [RepositoryInitializer OSGi-konfiguration](/help/implementing/deploying/overview.md#repoint) skript i programdistributionspaketet för att lägga till åtkomstkontrollistor för `sling-distribution-importer` användare.

I föregående exempelfel är paketet `myapp-base.ui.content-*.zip` innehåller innehåll under `/conf` och `/var/workflow`. Behörigheter för `sling-distribution-importer` under dessa banor behövs.

Här är ett exempel [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) av en sådan OSGi-konfiguration som lägger till ytterligare behörigheter för `sling-distribution-importer` användare.  Den här konfigurationen lägger till behörigheter under `/var`.  Den här XML-filen nedan [1] måste läggas till i programpaketet under `/apps/myapp/config` (där myapp är den mapp där programkoden lagras).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

Om det inte gick att lösa felet genom att lägga till en OSGi-konfiguration för RepositoryInitializer kan det bero på något av dessa ytterligare problem.

* Distributionen kan misslyckas på grund av en felaktig OSGi-konfiguration som bryter en färdig tjänst.
   * Kontrollera loggarna under distributionen för att se om det finns några uppenbara fel.

* Distributionen kan misslyckas på grund av felaktig dispatcher eller Apache-konfigurationer.
   * Testa dina Apache- och Dispatcher-konfigurationer lokalt med den Docker-bild som ingår i SDK:n.
   * Se [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md#content-delivery) om hur du konfigurerar Docker-behållaren för dispatcher för enkel lokal testning.

* Distributionen kan misslyckas på grund av ett annat fel under replikering av innehållspaketen (Sling-distribution) från författaren till publiceringsinstanser.
   * Följ de här stegen för att simulera problemet i en lokal konfiguration.
      1. Installera en författare och publicera instansen lokalt med de senaste AEM SDK-burkarna.
      1. Logga in i författarinstansen.
      1. Gå till **verktyg** -> **Distribution** -> **Distribution**.
      1. Distribuera innehållspaketen som är en del av kodbasen och se om kön blockeras med ett fel.

## Jag kan inte ange en variabel med ett aio-kommando. Vad kan jag göra? {#set-variable}

Du kan få en `403` fel som följande när du försöker lista eller ange pipeline-variabler via `aio` kommandon.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

I det här fallet måste användaren som kör dessa kommandon läggas till i **Distributionshantering** i Admin Console.

Se [API-behörigheter](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) för mer information.
