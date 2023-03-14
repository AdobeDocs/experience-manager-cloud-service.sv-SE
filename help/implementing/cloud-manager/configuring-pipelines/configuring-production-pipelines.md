---
title: Konfigurera produktionsförlopp
description: Lär dig hur du konfigurerar produktionspipelines för att skapa och distribuera kod till produktionsmiljöer.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 3348662e3da4dad75b851d7af7251d456321a3ec
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---


# Konfigurera en produktionspipeline {#configure-production-pipeline}

Lär dig hur du konfigurerar produktionsledningarna för att skapa och distribuera koden till produktionsmiljöer. En produktionspipeline distribuerar koden först till scenmiljön och när den godkänns distribueras samma kod till produktionsmiljön.

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
>Innan du konfigurerar en frontendpipeline ska du läsa [AEM för att skapa webbplatser snabbt](/help/journey-sites/quick-site/overview.md) för att få en komplett guide med hjälp av det lättanvända AEM för att skapa webbplatser. Den här resan hjälper dig att effektivisera utvecklingen av AEM sajt, så att du snabbt kan anpassa din sajt utan någon AEM bakomliggande kunskap.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** sida och klicka på **Lägg till** för att markera **Lägg till produktionspipeline**.

   ![Pipelines-kortet i programhanteraren - översikt](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. The **Lägg till produktionspipeline** visas. Ange en **Pipelinenamn** för att identifiera ditt flöde tillsammans med följande alternativ. Klicka **Fortsätt**.

   **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

   * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
   * **Vid Git-ändringar** - Detta alternativ startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

   **Beteende vid viktiga måttfel** - Under pipeline-konfiguration eller -redigering **Distributionshanteraren** har alternativet att definiera hur pipelinen fungerar när ett viktigt fel påträffas i någon av kvalitetsportarna. De tillgängliga alternativen är:

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.

   ![Konfiguration av produktionspipeline](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. På **Källkod** måste du definiera var pipelinen ska hämta sin kod och vilken typ av kod den är.

   * **[Front End-kod](#front-end-code)**
   * **[Fullständig stackkod](#full-stack-code)**
   * **[Webbnivåkonfiguration](#web-tier-config)**

Hur du slutför produktionen varierar beroende på vilket alternativ du väljer för **Källkod** du markerade. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet för att slutföra konfigurationen av din pipeline.

### Front End-kod {#front-end-code}

En frontkodspipeline distribuerar frontkodsbyggen som innehåller ett eller flera gränssnittsprogram på klientsidan. Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) om du vill ha mer information om den här typen av pipeline.

Följ de här stegen för att slutföra konfigurationen av produktionsflödet för slutkoden.

1. På **Källkod** måste du definiera följande alternativ.

   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.
   >[!TIP]
   > 
   >Se dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.
   * **Kodplats** - Det här alternativet definierar den sökväg i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipeline innan den distribueras till produktion.

   ![Front end-kod](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Klicka **Spara** för att spara ditt flöde.

Pipelinen sparas och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

### Fullständig stackkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationen. Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) om du vill ha mer information om den här typen av pipeline.

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
   * **Kodplats** - Det här alternativet definierar den sökväg i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipeline innan den distribueras till produktion.
   * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

   ![Fullständig stackkod](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Klicka **Fortsätt** för att gå vidare till **Experience Audit** där du kan definiera sökvägar som alltid ska inkluderas i Experience Audit.

   ![Lägg till Experience Audit](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Ange en sökväg som ska inkluderas i Experience Audit.

   * Sidsökvägar måste börja med `/`.
   * Om du till exempel vill inkludera `https://wknd.site/us/en/about-us.html` Ange sökvägen i Experience Audit `/us/en/about-us.html`.

   ![Definiera en sökväg för Experience Audit](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Klicka **Lägg till sida** och sökvägen fylls i automatiskt med adressen till din miljö och läggs till i sökvägstabellen.

   ![Spara bana till tabellen](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Fortsätt att lägga till banor efter behov genom att upprepa de två föregående stegen.

   * Du kan lägga till högst 25 banor.
   * Om du inte definierar några sökvägar inkluderas webbplatsens hemsida som standard i Experience Audit.

1. Klicka på **Spara** för att spara ditt flöde.

Sökvägar som har konfigurerats för Experience Audit skickas till tjänsten och utvärderas efter prestanda, tillgänglighet, SEO (sökmotoroptimering), bästa praxis och PWA (Progressive Web App) när pipeline körs. Se [Upplevelsegranskningsresultat](/help/implementing/cloud-manager/experience-audit-testing.md) för mer information.

Pipelinen sparas och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

### Webbnivåkonfiguration {#web-tier-config}

En konfigurationspipeline för webbskikt Distribuerar konfigurationer för HTTPD/Dispatcher. Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) om du vill ha mer information om den här typen av pipeline.

Följ de här stegen för att slutföra konfigurationen av produktionsflödet för kod i helhög.

1. På **Källkod** måste du definiera följande alternativ.

   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.
   >[!TIP]
   > 
   >Se dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.
   * **Kodplats** - Det här alternativet definierar sökvägen i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.
      * För konfigurationspipelines på webbnivå är detta vanligtvis sökvägen som innehåller `conf.d`, `conf.dispatcher.d`och `opt-in` kataloger.
      * Om projektstrukturen till exempel genererades från [AEM Project Archetype,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) banan `/dispatcher/src`.
   * **Pausa innan du distribuerar till produktion** - Det här alternativet pausar pipeline innan den distribueras till produktion.
   * **Schemalagd** - Med det här alternativet kan användaren aktivera den schemalagda produktionsdistributionen.

   ![Webbskiktskod](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Klicka **Spara** för att spara ditt flöde.

>[!NOTE]
>
>Om du har en befintlig pipeline som distribueras i en hel hög till en miljö, kommer den befintliga konfigurationen på hela stacken att ignoreras om du skapar en konfigurationspipeline för en webbskikt för samma miljö.

Pipelinen sparas och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

## Developing Sites with the Front-End Pipeline {#developing-with-front-end-pipeline}

Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.

Se dokumentet [Developing Sites with the Front-End Pipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) för hur denna process fungerar tillsammans med vissa överväganden som måste beaktas för att man ska få ut mesta möjliga av denna process.

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
