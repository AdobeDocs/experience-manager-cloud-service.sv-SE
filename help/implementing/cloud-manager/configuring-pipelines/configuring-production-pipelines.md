---
title: Konfigurera produktionsförlopp
description: Lär dig hur du konfigurerar produktionspipelines för att skapa och distribuera kod till produktionsmiljöer.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 0%

---


# Konfigurera en produktionspipeline {#configure-production-pipeline}

Lär dig hur du konfigurerar produktionspipelines för att skapa och distribuera kod till produktionsmiljöer. En produktionspipeline distribuerar kod först till scenmiljön och när den godkänns distribueras samma kod till produktionsmiljön.

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera produktionspipelines.

>[!NOTE]
>
>Det går inte att konfigurera en produktionspipeline förrän programskapandet är klart, en Git-databas har minst en gren och en uppsättning för produktions- och stagningsmiljö skapas.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägga till en ny produktionspipeline {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med användargränssnittet för [!UICONTROL Cloud Manager] kan du lägga till en produktionspipeline genom att följa de här stegen.

>[!TIP]
>
>Innan du konfigurerar en pipeline för användargränssnitt bör du läsa [AEM snabbplatsskapande resa](/help/journey-sites/quick-site/overview.md) för att få en komplett guide med hjälp av det lättanvända AEM snabbplatsverktyget. Den här resan hjälper dig att effektivisera utvecklingen av AEM sajt, så att du snabbt kan anpassa din sajt utan någon AEM bakomliggande kunskap.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera till kortet **Pipelines** på sidan **Programöversikt** och klicka på **Lägg till** för att välja **Lägg till produktionspipeline**.

   ![Rörledningskortet i programhanteraren - översikt](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Dialogrutan **Lägg till produktionspipeline** visas. Ange ett **Pipelinenamn** som identifierar din pipeline tillsammans med följande alternativ. Klicka på **Fortsätt**.

   **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

   * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
   * **Vid Git-ändringar** - Detta alternativ startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

   **Beteende vid viktiga måttfel** - Under pipeline-konfiguration eller redigering kan **Distributionshanteraren** definiera pipelinens beteende när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckades omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.

   ![Konfiguration av produktionspipeline](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. På fliken **Source Code** måste du välja vilken typ av kod som pipeline ska bearbeta.

   * **[Fullständig stackkod](#full-stack-code)**
   * **[Måldistribution](#targeted-deployment)**

Mer information om olika typer av pipelines finns i [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Stegen för att slutföra skapandet av produktionsflödet varierar beroende på vilken typ av källkod du har valt. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet så att du kan slutföra konfigurationen av din pipeline.

### Fullständig stapelkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfiguration.

>[!NOTE]
>
>Om det redan finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

Följ de här stegen för att slutföra konfigurationen av produktionsflödet för kod i helhög.

1. På fliken **Source Code** måste du definiera följande alternativ.

   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Läs dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) om du vill veta mer om hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git Branch** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.
   * **Ignorera webbnivåkonfiguration** - När det här alternativet är markerat distribueras inte webbnivåkonfigurationen.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipelinen innan den distribueras till produktion.
   * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

   ![Fullständig stackkod](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Tryck eller klicka på **Fortsätt** för att gå vidare till fliken **Experience Audit** där du kan definiera sökvägarna som alltid ska inkluderas i Experience Audit.

   ![Lägg till Experience Audit](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Ange sökvägar som ska inkluderas i Experience Audit.

   * Mer information finns i dokumentet [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-dashboard.md#configuration).

1. Klicka på **Spara** för att spara din pipeline.

Sökvägar som har konfigurerats för Experience Audit skickas till tjänsten och utvärderas utifrån prestanda-, hjälpmedels-, SEO-test (sökmotoroptimering), bästa praxis och PWA-tester (Progressive Web App) när pipeline körs. Mer information finns i [Om Experience Audit Results](/help/implementing/cloud-manager/experience-audit-dashboard.md).

Pipelinen sparas och du kan nu [hantera dina pipelines](managing-pipelines.md) på kortet **Pipelines** på sidan **Programöversikt**.

### Målinriktad distribution {#targeted-deployment}

En riktad distribution distribuerar bara kod för utvalda delar av AEM. I en sådan distribution kan du välja att **Inkludera** ska vara en av följande typer av kod:

* **Konfig** - Konfigurera inställningar för olika funktioner i AEM.
   * Se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md) för en lista över konfigurationer som stöds, som omfattar vidarebefordran av loggar, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer, och för att hantera dem i din databas så att de distribueras korrekt.
   * När du kör en riktad distributionsprocess distribueras konfigurationerna, förutsatt att de sparas i den miljö, databas och gren som du har definierat i pipeline.
   * Det kan bara finnas en konfigurationspipeline per miljö.
* **Front End Code** - Konfigurera JavaScript och CSS för frontdelen av AEM.
   * Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.
   * I dokumentet [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) finns information om hur den här processen fungerar tillsammans med vissa överväganden som du bör vara medveten om för att få ut mesta möjliga av processen.
* **Webbnivåkonfiguration** - Konfigurera dispatcheregenskaper för att lagra, bearbeta och leverera webbsidor till klienten.
   * Mer information finns i dokumentet [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Om det finns en kodrapport på webbnivå för den valda miljön är det här valet inaktiverat.
   * Om du har en befintlig pipeline som distribueras i en hel hög till en miljö, kommer den befintliga konfigurationen på hela stacken att ignoreras om du skapar en konfigurationspipeline för en webbskikt för samma miljö.

>[!NOTE]
>
>Rörledningar för webbnivå och konfiguration stöds inte i privata databaser. Mer information och en fullständig lista över begränsningar finns i dokumentet [Lägga till privata databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Stegen för att slutföra skapandet av din produktion är riktade distributionsflöden desamma när du väljer en distributionstyp.

1. Välj vilken distributionstyp du behöver.

![Målinriktade distributionsalternativ](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Definiera **berättigade distributionsmiljöer**.

   * Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.

1. Ange följande alternativ under **Source Code**:

   * **Databas** - Det här alternativet definierar från vilken Git-repo som pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-grenen** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet. Här hittas de matchande grenar som du kan välja.
   * **Kodplats** - Det här alternativet definierar sökvägen i grenen för den valda rapporten från vilken pipelinen ska hämta koden.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipelinen innan den distribueras till produktion.
   * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen. Endast tillgängligt för riktade distributioner på webbnivå.

   ![Konfigurera pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Klicka på **Spara**.

Pipelinen sparas och du kan nu [hantera dina pipelines](managing-pipelines.md) på kortet **Pipelines** på sidan **Programöversikt**.

## Hoppa över Dispatcher-paket {#skip-dispatcher-packages}

Om du vill att dispatcherpaket ska byggas som en del av pipeline, men inte vill att de ska publiceras för att skapa lagring, kan du inaktivera publicering av dem, vilket kan minska körningstiden för pipeline.

Följande konfiguration för att inaktivera publiceringsdispatcherpaket måste läggas till via projektfilen `pom.xml`. Den baseras på en miljövariabel, som fungerar som en flagga som du kan ange i Cloud Manager byggbehållare för att definiera när dispatcherpaket ska ignoreras.

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
