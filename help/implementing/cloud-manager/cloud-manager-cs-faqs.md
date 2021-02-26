---
title: Cloud Manager - Vanliga frågor om Cloud Services
seo-title: Vanliga frågor om Cloud Manager
description: Se Vanliga frågor om Cloud Services i Cloud Manager för att få felsökningstips
seo-description: Följ den här sidan för att få svar på frågor om Cloud Manager - Cloud Services och svar
translation-type: tm+mt
source-git-commit: 75a5ff02e5f7c0e0e3ba42c8559851d3c98c3c8d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Vanliga frågor om Cloud Manager {#cloud-manager-faqs}

Följande avsnitt innehåller svar på vanliga frågor om Cloud Manager för Cloud Services.

## Går det att använda Java 11 med Cloud Manager-byggen? {#java-11-cloud-manager}

Det går inte att skapa AEM Cloud Manager när du försöker byta från Java 8 till 11. Problemet kan ha många orsaker och de vanligaste är beskrivna nedan:

* Lägg till maven-toolchains-plugin med rätt inställningar för Java 11 enligt [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Se till exempel [exempelprojektkoden](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Om du råkar ut för felet nedan måste du ta bort användningen av `maven-scr-plugin` och konvertera alla OSGi-anteckningar till OSGi R6-anteckningar. Mer information finns i [här](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* För Cloud Manager-byggen misslyckas plugin-programmet för stavningskontroll med felet `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Det här är ett känt fel som beror på att Cloud Manager använder en annan version av Java för att köra maven-kommandot jämfört med att kompilera kod. Utelämna `requireJavaVersion` från dina Maven-enforcement-plugin-konfigurationer.

## Distributionen stoppas eftersom kodkvalitetskontrollen misslyckades. Finns det något sätt att kringgå den här kontrollen? {#deployment-stuck}

Alla kodkvalitetsfel utom *Säkerhetsgradering* är icke-kritiska mått, så de kan kringgås genom att objekten i resultatgränssnittet expanderas.

En användare med [Distributionshanteraren, Project Manager eller Business Owner](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)-rollen kan åsidosätta problemen. I så fall fortsätter pipeline eller så kan de acceptera problemen. I så fall avbryts pipeline med ett fel.  Mer information finns i [Tre-nivåportar när du kör en pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use).


## Får vi använda SNAPSHOT i den version av projektet Maven? Hur fungerar versionshantering av paketen och paketburkfilerna för Stage- och Production-distributioner? {#snapshot-version}

Titta på följande scenarier för att lära dig mer om versionshantering av paketen och källfilerna för Stage- och Production-distributioner:

1. För utvecklardistributioner måste Git-grenen `pom.xml`-filerna innehålla `-SNAPSHOT` i slutet av `<version>`-värdet. Detta gör att efterföljande distribution där versionen inte ändras kan installeras. I utvecklingsmiljöer läggs ingen automatisk version till eller genereras för maven-bygget.

1. I scen- och produktionsdistributionen genereras en automatisk version enligt [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. För anpassad versionshantering i Stage- och Production-distributioner anger du en korrekt maven-version på 3 delar som `1.0.0`. Öka versionen varje gång du ska göra en ny distribution till produktion.

1. Cloud Manager lägger automatiskt till sin version i Stage- och Production-byggen och skapar till och med en Git-gren. Ingen särskild konfiguration krävs. Om steg 3 ovan hoppas över fungerar distributionen ändå som den ska och en version ställs in automatiskt.

1. Det finns inga problem om du lämnar versionen med `-SNAPSHOT` för Stage- och Production-byggen eller -distributioner. Cloud Manager anger automatiskt rätt versionsnummer och skapar en tagg åt dig i Git. Om det behövs kan du hänvisa till den här taggen senare.

1. Om du vill testa experimentell kod i utvecklingsmiljön kan du skapa en ny Git-gren och ställa in pipeline så att den använder den andra grenen. Detta är användbart när distributioner börjar misslyckas och du vill testa med äldre versioner av koden för att se när den gick sönder.

   Git-kommandot nedan skapar en fjärrgren med namnet *testbranch1* mot en specifik befintlig implementering `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Den här speciella grenen kan användas i Cloud Manager utan att påverka andra grenar:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Mer information finns i [Git-dokumentationen](https://git-scm.com/book/en/v2/Git-Internals-Git-References).

   Om du vill ta bort testgrenen senare använder du kommandot delete:

   `git push origin --delete testbranch1`

## Det går inte att skapa Maven i Cloud Manager, men det byggs lokalt utan fel. Hur felsöker jag? {#maven-build-fail}

Mer information finns i [Git-resurs](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md).

## Vad ska jag göra om distributionen av Cloud Manager misslyckas vid distributionen i AEM som en Cloud Service-miljö? {#cloud-manager-deployment-cloud-service}

Den vanligaste orsaken till att distributioner misslyckas beror på otillräcklig behörighet för *sling-distribution-import*-användaren.
Se exemplet nedan för att förstå ett problem, en orsak och en lösning:

**Problem**
Under en Cloud Manager-distribution på AEM som en Cloud Service-miljö misslyckas distributionssteget och fel som de nedan observeras.

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**Orsak**

Användaren av sling-distribution-importeraren behöver ytterligare behörigheter per innehållssökvägarna som definieras i paketet ui.content.  Det innebär vanligtvis att vi måste lägga till behörigheter för både /conf och /var.

**LösningLösningen**
är att lägga till en  [RepositoryInitializer OSGi-](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) konfigurationskript i programdistributionspaketet för att lägga till åtkomstkontrollistor för användare som säljer distribution och importerar.
I exemplet ovan innehåller paketet myapp-base.ui.content-*.zip innehåll under `/conf` och `/var/workflow`. För att distributionen inte ska misslyckas måste vi lägga till behörigheter för försäljnings- och distributionsimportör under dessa sökvägar.
Här följer ett exempel på [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) för en sådan OSGi-konfiguration som lägger till ytterligare behörigheter för användaren som är Sing-distribution-importer.  Den här konfigurationen lägger till behörigheter under /var.  Den här xml-filen under [1] måste läggas till i programpaketet under `/apps/myapp/config` (där myapp är mappen där programkoden lagras).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. Om *sling-distribution-importer* inte är orsaken kan distributionen misslyckas på grund av en felaktig OSGi-konfiguration som bryter ut ur kartongtjänsten. Kontrollera loggarna under distributionen för att se om det finns några uppenbara fel.

1. Distributionen kan misslyckas på grund av felaktiga dispatcher- eller apache-konfigurationer. Testa dina Apache-konfigurationer och Dispatcher-konfigurationer lokalt med den Docker-bild som ingår i SDK:n. Se [Dispatcher i molnet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) om hur du konfigurerar Dispatcher Docker-behållaren för enkel lokal testning.

1. Distributionen kan misslyckas på grund av ett annat fel under replikering av innehållspaketen (sling distribution) från författaren till publiceringsinstanser.

   Se stegen nedan för att simulera detta i en lokal konfiguration:

   * Installera en Author- och Publish-instans (med de senaste AEM SDK-burkarna)
   * Logga in på Author-instansen
   * Gå till **Verktyg** -> **Distribution** -> **Distribution**
   * Distribuera innehållspaketen som är en del av kodbasen och se om kön blockeras med ett fel

## Det går inte att ange en variabel via aio cloud manager för att ange pipeline-variabler. Hur felsöker man dessa problem? {#set-variable}

Om du får ett `403`-fel när du försöker lista eller ange pipeline-variabler med kommandon som liknar dem nedan, måste du läggas till som en *Deployment Manager* Cloud Manager-produktroll i Admin Console.\
Mer information finns i [API-behörigheter](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md).

Relaterade kommandon och fel:

`$ aio cloudmanager:list-pipeline-variables 222`

*Fel*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Fel*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*Fel*:  `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
