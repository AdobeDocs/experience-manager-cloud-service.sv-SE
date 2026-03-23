---
title: Lägg till en icke-produktionspipeline
description: Lär dig hur du lägger till en icke-produktionsprocess för att testa kvaliteten på koden innan du distribuerar den till produktionsmiljöer.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 8391980183b8c5a91046e01474200b9eaf8e0546
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---


# Lägg till en icke-produktionspipeline {#configuring-non-production-pipelines}

När du har konfigurerat ett program och skapat minst en miljö i användargränssnittet i Cloud Manager kan du lägga till rörledningar som inte är avsedda för produktion. Med dessa rörledningar kan du testa kodkvaliteten innan du distribuerar den till produktionsmiljöer.

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera icke-produktionspipelines.

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägg till en ny icke-produktionspipeline {#adding-non-production-pipeline}

När du har konfigurerat ett program och skapat minst en miljö i användargränssnittet i Cloud Manager kan du lägga till rörledningar som inte är avsedda för produktion. Använd dessa rörledningar för att testa kodkvaliteten innan du distribuerar till produktionsmiljöer.

**Så här lägger du till en ny icke-produktionsflöde:**

1. Logga in på Cloud Manager på [experience.adobe.com](https://experience.adobe.com).
1. Klicka på **Experience Manager** i avsnittet **Snabbåtkomst**.
1. Klicka på **Cloud Manager** på den vänstra panelen.
1. Välj en organisation som du vill ha.
1. Klicka på ett program på konsolen **Mina program**.
1. Klicka på **Rörledningar** på den vänstra panelen.
1. Klicka på **Lägg till pipeline** > **Lägg till icke-produktionsförlopp** på sidan **Förgreningar**, nära det övre högra hörnet.

   ![Lägg till icke-produktionsflöde](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. På fliken **Konfiguration** i dialogrutan **Lägg till icke-produktionsförlopp** väljer du någon av följande icke-produktionsförloppsrör som du vill skapa:

   * **Kodkvalitetspipeline** - Skapar en pipeline som bygger koden på en GIT-gren, kör enhetstester och utvärderar kodkvaliteten utan att distribuera den till någon miljö.
   * **Distributionspipeline** - Skapar en pipeline som bygger koden, kör enhetstester, utvärderar kodkvaliteten och distribuerar till en icke-produktionsmiljö.

   ![Lägg till icke-produktion-pipeline-dialogruta](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Under avsnittet **Pipelinekonfiguration** skriver du en beskrivning för din icke-produktionspipeline i fältet **Namn på icke-produktionspipeline**.
1. Under avsnittet **Distributionsalternativ** väljer du en av följande distributionsutlösare som du vill använda:

   * **Manuell** - Du kan starta pipelinen manuellt.
   * **Vid Git-ändringar** - Startar pipelinen när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

1. Välj det **viktiga måttfel** som du vill använda.

   * **Fråga varje gång** - Det här beteendet är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckades omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Det emulerar i stort sett en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Det emulerar i stort sett en användare som manuellt godkänner varje fel.

1. Klicka på **Fortsätt**.

1. De återstående stegen som du använder för att slutföra konfigurationen av produktionsflödet beror på vilken typ av källkod du väljer att använda.
På fliken **Source Code** i dialogrutan **Add Non-Production Pipeline** väljer du vilken typ av kod som icke-produktionsflödet ska bearbeta.

   * **[Jag använder fullständig stackkod](#full-stack-code)**
   * **[Jag använder riktad distribution](#targeted-deployment)**

   Mer information om olika typer av pipelines finns i [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).


### Jag använder fullständig stackkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och framände som innehåller en eller flera AEM-serverprogram tillsammans med HTTPD/Dispatcher-konfiguration.

>[!NOTE]
>
>Om det finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

Så här slutför du konfigurationen av icke-produktionsflödet för kod i helhög:

1. I avsnittet **Source-kod** definierar du följande alternativ.

   * **Berättigade distributionsmiljöer** - Endast tillgängligt när du redigerar en icke-produktionspipeline. Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.
   * **Databas** - I listrutan väljer du Git-databasen som pipeline använder som källa. Cloud Manager skapar kod från den databas du väljer här.

     >[!TIP]
     > 
     >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-grenen** - I listrutan väljer du vilken gren i den valda databasen som pipeline ska bygga från. Standardvärdet är `main`. I pipeline används den valda grenen som källa för bygge och distribution. Om det behövs klickar du på **Uppdatera** för att uppdatera listan över tillgängliga grenar för den valda databasen. Använd det här alternativet om en nyligen skapad gren inte visas i listan.
   * **Skapa strategi**
      * **Fullständigt bygge** - Bygger alla moduler i databasen varje gång
      * BETA **Smart Build** - Skapar endast moduler som har ändrats sedan den senaste implementeringen.<br>Lär dig mer om [att använda Smart Build i en icke-produktionsprocess](#about-smart-build).

        >[!IMPORTANT]
        >
        >Smart Build är endast tillgängligt för pipelines för kodkvalitet och distributionspipelines för Dev Full Stack Code.

   * Kryssrutan **Ignorera webbnivåkonfiguration** - När det här alternativet är markerat distribueras inte webbnivåkonfigurationen.

1. Om din pipeline är en distributionspipeline i avsnittet **Pipeline** kan du välja att köra en testfas. Markera de alternativ som du vill aktivera i den här fasen. Om inget av alternativen är markerat visas inte testfasen när pipeline körs.

   * **Funktionstestning av produkt** - Kör [produktfunktionstester](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) mot utvecklingsmiljön.
   * **Anpassad funktionstestning** - Kör [anpassade funktionstester](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) mot utvecklingsmiljön.
   * **Anpassad gränssnittstestning** - Kör [anpassade gränssnittstester](/help/implementing/cloud-manager/ui-testing.md) för anpassade program.
   * **Experience Audit** - Kör [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Pipeline i full hög](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Klicka på **Spara**.

Pipelinen sparas och du kan nu [hantera dina pipelines]&#x200B;(hantera pipe)
lines.md) på kortet **Pipelines** på sidan **Programöversikt** .

### Jag använder målinriktad distribution {#targeted-deployment}

En riktad distribution distribuerar kod endast för utvalda delar av AEM-programmet. I en sådan distribution kan du välja att **Inkludera** ska vara en av följande typer av kod:

![Målinriktade distributionsalternativ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **Front End Code** - Konfigurera JavaScript och CSS för frontdelen av ditt AEM-program.
   * Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.
   * I dokumentet [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) finns information om hur den här processen fungerar tillsammans med vissa överväganden som du bör vara medveten om för att få ut mesta möjliga av processen.
* **Webbnivåkonfiguration** - Konfigurera Dispatcher-egenskaper för att lagra, bearbeta och leverera webbsidor till klienten.
   * Mer information finns i dokumentet [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Om det finns en kodrapport på webbnivå för den valda miljön är det här valet inaktiverat.
   * Om en pipeline med hela stackar redan distribueras till en miljö kan du fortfarande skapa en konfigurationspipeline på webbnivå för samma miljö. När du gör det ignorerar Cloud Manager webskiktskonfigurationen i pipeline för hela stacken.

     >[!NOTE]
     >
     >Rörledningar för webbnivå och konfiguration stöds inte i privata databaser. Mer information och en fullständig lista över begränsningar finns i [Lägga till privata databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. Ange följande alternativ under avsnittet **Source-kod**:

   * **Databas** - Det här alternativet definierar från vilken GIT-databas som icke-produktionsflödet ska hämta koden.

     >[!TIP]
     > 
     >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-grenen** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden. Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet. Här hittas de matchande grenar som du kan välja.
   * **Kodplats** - Det här alternativet definierar sökvägen i grenen för den valda rapporten från vilken pipelinen ska hämta koden.

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. Om du har aktiverat Experience Audit klickar du på **Continue** för att gå vidare till fliken **Experience Audit** där du kan definiera sökvägarna som alltid ska inkluderas i Experience Audit.

   * Om du har aktiverat **Experience Audit** finns mer information om hur du konfigurerar i dokumentet [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md).
   * Om du inte gjorde det hoppar du över det här steget.

1. Klicka på **Spara** för att spara pipeline.

Pipelinen sparas och du kan nu [hantera dina pipelines](managing-pipelines.md) på kortet **Pipelines** på sidan **Programöversikt**.


## Om att använda Smart Build i en icke-produktionsprocess{#about-smart-build}

**Smart Build** i Cloud Manager är en optimerad byggstrategi för icke-produktionspipelines. Smart Build minskar byggtiden genom att cache-lagra moduler och återskapa endast de moduler som har ändrats sedan den senaste körningen. Oförändrade moduler återanvänds från cacheminnet, medan endast ändrade moduler och deras beroenden återskapas, vilket förbättrar effektiviteten för iterativa utvecklingsarbetsflöden.

Smart Build är för närvarande endast tillgängligt för följande:

* Kodkvalitetsledningar.
* Utveckla rörledningar för driftsättning i högklasser.

>[!NOTE]
>
>Den första körningen efter aktiveringen av Smart Build fungerar som en fullständig version eftersom cachen är tom.

Smart Build rekommenderas när du har följande:
* Du utvecklar och implementerar ofta inkrementella förändringar.
* Ditt projekt innehåller flera Maven-moduler.
* Fullversioner tar lång tid.

Smart Build är inte alltid idealiskt när du har följande:
* Din version är starkt beroende av plugin-program som utför åtgärder utanför Maven beroendediagram.
* Du måste verifiera alla versioner av varje körning.

### Förstå byggprestanda{#smart-build-performance}

Den prestandaökning som kan uppnås med Smart Build beror på flera faktorer, bland annat följande:

* Antalet moduler i projektet.
* Kodändringarnas frekvens och omfattning.
* Distributionen av beroenden mellan moduler.

I allmänhet kan projekt med många oberoende moduler se den största förbättringen.

### Cacheavanmälan per modul{#smart-build-cache-optout}

Smart Build har finkornig kontroll som gör att du kan inaktivera cachelagring för specifika moduler. Den här funktionen är användbar när vissa moduler:

* Använd plugin-program som `exec-maven-plugin` eller `maven-antrun-plugin`.
* Utför filåtgärder som inte spåras av Maven-beroenden.
* Cachelagrat innehåll ger inkonsekventa resultat.

### Inaktivera cachelagring för en modul{#smart-build-disable-caching}

Du kan lägga till följande egenskap i den påverkade modulens `pom.xml`:

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

Den här syntaxen tvingar modulen att återskapa varje pipeline-körning medan andra moduler fortfarande har nytta av cachelagring.

### Begränsningar och överväganden när Smart Build används{#smart-build-limitations}

Tänk på följande när du använder Smart Build:

* Smart Build bygger på Maven-beroendeanalys.
* Ändringar utanför beroendediagrammet kan inte utlösa rekonstruktioner.
* Vissa plugin-program kanske inte är helt kompatibla med cachning.
* Du kan när som helst växla tillbaka till **Fullständigt bygge** genom att redigera icke-produktionsflödet.

Om du stöter på oväntat byggbeteende bör du inaktivera cachelagring för specifika moduler eller tillfälligt byta din byggstrategi till **Fullständigt bygge**.

### Felsöka problem med Smart Build{#smart-build-troubleshoot}

| Problem | Föreslagna lösningar |
| --- | --- |
| Byggresultaten är inkonsekventa | ・ Inaktivera cachelagring för berörda moduler.<br> ・ Verifiera plugin-programmets beteende (särskilt `exec`/`antrun` plugin-program). |
| Ingen prestandaförbättring | ・ Kontrollera att flera körningar har utförts (cacheupphettning).<br> ・ Kontrollera om de flesta moduler ändras ofta. |
| Oväntade artefakter eller saknade ändringar | ・ Kontrollera om ändringarna ligger utanför Maven-beroendespårning.<br> ・ Använd **Fullständigt bygge** för verifiering. |

Se [Lägg till en icke-produktionsprocess](#adding-non-production-pipeline) om du vill aktivera Smart Build.











<!--
## Add a non-production pipeline {#adding-non-production-pipeline}

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

1. Sign into Cloud Manager at [experiece.adobe.com](https://experience.adobe.com).
1. In the **Quick access** section, click **Experience Manager**.
1. In the left side panel, click **Cloud Manager**.
1. Select an organization that you want.
1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code {#full-stack-code}

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## Uteslut Dispatcher-paket {#exclude-dispatcher-packages}

Om du vill att Dispatcher-paket ska byggas in i din pipeline men inte överföras för att bygga lagring inaktiverar du publicering. Om du gör det kan det korta körtiden.

Lägg till följande konfiguration i projektfilen `pom.xml` om du vill inaktivera publicering av Dispatcher-paket. Ange en miljövariabel i Cloud Manager byggbehållare för att flagga när Dispatcher-paket ska ignoreras. Pipelinen läser den här flaggan och ignorerar dem därefter.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
