---
title: Konfigurera produktionsförlopp
description: Lär dig hur du konfigurerar produktionspipelines för att skapa och distribuera kod till produktionsmiljöer.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---


# Konfigurera en produktionspipeline {#configure-production-pipeline}

Lär dig hur du konfigurerar produktionspipelines för att skapa och distribuera kod till produktionsmiljöer. En produktionspipeline distribuerar kod först till scenmiljön och när den godkänns distribueras samma kod till produktionsmiljön.

En användare måste ha **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** roll för att konfigurera produktionspipelinor.

>[!NOTE]
>
>Det går inte att konfigurera en produktionspipeline förrän programskapandet är klart, en Git-databas har minst en gren och en uppsättning för produktions- och stagningsmiljö skapas.

Innan du börjar distribuera koden måste du konfigurera dina pipeline-inställningar från [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägga till en ny produktionspipeline {#adding-production-pipeline}

När du har konfigurerat programmet och har minst en miljö som använder [!UICONTROL Cloud Manager] Du kan nu lägga till en produktionspipeline genom att följa de här stegen.

>[!TIP]
>
>Innan du konfigurerar en frontendpipeline ska du läsa [AEM för att skapa webbplatser snabbt](/help/journey-sites/quick-site/overview.md) för att få en komplett guide med hjälp av det lättanvända AEM snabbverktyget för att skapa webbplatser. Den här resan hjälper dig att effektivisera utvecklingen av AEM sajt, så att du snabbt kan anpassa din sajt utan någon AEM bakomliggande kunskap.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation

1. På **[Mina program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** väljer du programmet.

1. Navigera till **Pipelines** från **Programöversikt** sida och klicka **Lägg till** för att markera **Lägg till produktionspipeline**.

   ![Pipelines-kortet i programhanteraren - översikt](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. The **Lägg till produktionspipeline** visas. Ange en **Pipelinenamn** för att identifiera ditt flöde tillsammans med följande alternativ. Klicka **Fortsätt**.

   **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

   * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
   * **Vid Git-ändringar** - Detta alternativ startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

   **Beteende vid viktiga måttfel** - Under pipeline-konfiguration eller -redigering **Distributionshanteraren** har alternativet att definiera hur pipelinen fungerar när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.

   ![Konfiguration av produktionsflöde](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. På **Källkod** måste du välja vilken typ av kod som pipeline ska bearbeta.

   * **[Fullständig stapelkod](#full-stack-code)**
   * **[Målinriktad distribution](#targeted-deployment)**

Se [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) för mer information om olika typer av rörledningar.

Stegen för att slutföra skapandet av produktionsflödet varierar beroende på vilken typ av källkod du har valt. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet så att du kan slutföra konfigurationen av din pipeline.

### Fullständig stapelkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationen.

>[!NOTE]
>
>Om det redan finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

Följ de här stegen för att slutföra konfigurationen av produktionsflödet för kod i helhög.

1. På **Källkod** måste du definiera följande alternativ.

   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.
   * **Ignorera webbnivåkonfiguration** - När du markerar det här alternativet distribueras inte webbnivåkonfigurationen.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipeline innan den distribueras till produktion.
   * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

   ![Fullständig stackkod](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Tryck eller klicka **Fortsätt** för att gå vidare till **Experience Audit** där du kan definiera sökvägar som alltid ska inkluderas i Experience Audit.

   ![Lägg till Experience Audit](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Ange sökvägar som ska inkluderas i Experience Audit.

   * Se dokumentet [Testning av Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md#configuration) för mer information.

1. Klicka **Spara** för att spara på rörledningen.

Sökvägar som har konfigurerats för Experience Audit skickas till tjänsten och utvärderas utifrån prestanda-, hjälpmedels-, SEO-test (sökmotoroptimering), bästa praxis och PWA-tester (Progressive Web App) när pipeline körs. Se [Upplevelsegranskningsresultat](/help/implementing/cloud-manager/experience-audit-testing.md) för mer information.

Pipelinen har sparats och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

### Målinriktad distribution {#targeted-deployment}

En riktad distribution distribuerar bara kod för utvalda delar av AEM. I en sådan distribution kan du välja **Inkludera** någon av följande typer av kod:

* **Konfig** - Konfigurera inställningar för trafikfilterregler i AEM.
   * Se dokumentet [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) om du vill lära dig hur du hanterar konfigurationerna i din databas så att de distribueras på rätt sätt.
   * När en riktad distributionsprocess körs, [WAF-konfigurationer](/help/security/traffic-filter-rules-including-waf.md) distribueras, förutsatt att de sparas i den miljö, databas och gren som du definierade i pipeline.
   * Det kan bara finnas en konfigurationspipeline per miljö.
* **Front End-kod** - Konfigurera JavaScript och CSS för den främre delen av AEM.
   * Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.
   * Se dokumentet [Developing Sites with the Front-End Pipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) om hur den här processen fungerar tillsammans med vissa överväganden för att vara medveten om att utnyttja hela potentialen i den här processen.
* **Webbnivåkonfiguration** - Konfigurera dispatcheregenskaper för att lagra, bearbeta och leverera webbsidor till klienten.
   * Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) för mer information.
   * Om det finns en kodrapport på webbnivå för den valda miljön är det här valet inaktiverat.
   * Om du har en befintlig pipeline som distribueras i en hel hög till en miljö, kommer den befintliga konfigurationen på hela stacken att ignoreras om du skapar en konfigurationspipeline för en webbskikt för samma miljö.

Stegen för att slutföra skapandet av din produktion är riktade distributionsflöden desamma när du väljer en distributionstyp.

1. Välj vilken distributionstyp du behöver.

![Alternativ för målinriktad distribution](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Definiera **Berättigade driftsättningsmiljöer**.

   * Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.

1. Under **Källkod** definierar du följande alternativ:

   * **Databas** - Det här alternativet definierar från vilken Git-repo som pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet. Här hittas de matchande grenar som du kan välja.
   * **Kodplats** - Det här alternativet definierar den sökväg i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipeline innan den distribueras till produktion.
   * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen. Endast tillgängligt för riktade distributioner på webbnivå.

   ![Konfigurera pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Klicka **Spara**.

Pipelinen har sparats och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

## Hoppa över Dispatcher-paket {#skip-dispatcher-packages}

Om du vill att dispatcherpaket ska byggas som en del av pipeline, men inte vill att de ska publiceras för att skapa lagring, kan du inaktivera publicering av dem, vilket kan minska körningstiden för pipeline.

Följande konfiguration för att inaktivera publiceringsdispatcherpaket måste läggas till via ditt projekt `pom.xml` -fil. Den baseras på en miljövariabel, som fungerar som en flagga som du kan ange i Cloud Managers byggbehållare för att definiera när dispatcherpaket ska ignoreras.

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
