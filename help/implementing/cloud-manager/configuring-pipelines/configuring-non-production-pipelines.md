---
title: Konfigurera icke-produktionsförlopp
description: Lär dig hur du konfigurerar icke-produktionsrörledningar för att testa kodens kvalitet innan du distribuerar den till produktionsmiljöer.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: aac397310babe1aa1e950c176459beaf665b72ce
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---


# Konfigurera icke-produktionsförlopp {#configuring-non-production-pipelines}

Lär dig hur du konfigurerar icke-produktionsrörledningar för att testa kodens kvalitet innan du distribuerar den till produktionsmiljöer.

## Icke-produktionsförlopp {#non-production-pipelines}

Förutom [produktionsrörledningar](#configuring-production-pipelines.md) som distribuerar till stagings- och produktionsmiljöer, kan du även konfigurera rörledningar som inte är avsedda för produktion för att validera koden.

Det finns två typer av icke-produktionsrörledningar:

* **Kodkvalitetsförlopp** - Dessa kör kodkvalitetskontroller i koden i en Git-gren och utför stegen för bygg- och kodkvalitet.
* **Distributionsförlopp** - Förutom att utföra steg för bygg- och kodkvalitet, som till exempel pipelines för kodkvalitet, distribuerar dessa pipelines koden till en icke-produktionsmiljö.

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägga till en ny icke-produktionspipeline {#adding-non-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med användargränssnittet i Cloud Manager är du redo att lägga till en icke-produktionsprocess genom att följa de här stegen.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Öppna **Pipelines** från startskärmen i Cloud Manager. Klicka på **+Lägg till** och markera **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. På **Konfiguration** -fliken i **Lägg till icke-produktionsförlopp** väljer du vilken typ av icke-produktionsflöde du ska lägga till.

   * **Kodkvalitetspipeline** - Skapa en pipeline som bygger din kod, kör enhetstester och utvärderar kodkvaliteten, men distribuerar INTE.
   * **Distributionsförlopp** - Skapa en pipeline som bygger din kod, kör enhetstester, utvärderar kodkvaliteten och distribuerar till en miljö.

   ![Dialogrutan Lägg till icke-produktionsförlopp](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Ange en **Namn på icke-produktionsförlopp** för att identifiera ditt flöde tillsammans med följande ytterligare information.

   * **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

      * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
      * **Vid Git-ändringar** - Detta alternativ startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

1. Om du väljer att skapa en **Distributionsförlopp** Du måste också definiera **Beteende vid viktiga måttfel**.

   * **Fråga varje gång** - Det här är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Detta emulerar i princip en användare som manuellt godkänner varje fel.

1. Klicka **Fortsätt**.

1. På **Källkod** -fliken i **Lägg till icke-produktionsförlopp** måste du välja vilken typ av kod som pipeline ska bearbeta.

   * **[Front End-kod](#front-end-code)**
   * **[Fullständig stackkod](#full-stack-code)**
   * **[Webbnivåkonfiguration](#web-tier-config)**

Hur du slutför skapandet av din icke-produktionsprocess varierar beroende på vilket alternativ du har för **Källkod** du markerade. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet för att slutföra konfigurationen av din pipeline.

### Front End-kod {#front-end-code}

En frontkodspipeline distribuerar frontkodsbyggen som innehåller ett eller flera gränssnittsprogram på klientsidan. Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) om du vill ha mer information om den här typen av pipeline.

Följ de här stegen för att slutföra konfigurationen av produktionsflödet för icke-produktion av slutkod.

1. På **Källkod** måste du definiera följande alternativ.

   * **Berättigade driftsättningsmiljöer** - Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.
   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.
   * **Kodplats** - Det här alternativet definierar den sökväg i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.

   ![Front-end-pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Klicka **Spara**.

Pipelinen sparas och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

### Fullständig stackkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationen. Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) om du vill ha mer information om den här typen av pipeline.

>[!NOTE]
>
>Om det redan finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

Följ de här stegen för att slutföra konfigurationen av icke-produktionsflödet för kod i helhög.

1. På **Källkod** måste du definiera följande alternativ.

   * **Berättigade driftsättningsmiljöer** - Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.
   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet hittar de grenar som matchar dig.
   * **Ignorera webbnivåkonfiguration** - När du markerar det här alternativet distribueras inte webbnivåkonfigurationen.

   * **Pipeline** - Om din pipeline är en distributionsprocess kan du välja att köra en testfas. Markera de alternativ du vill aktivera i den här fasen. Om inget av alternativen är markerat visas inte testfasen under pipeline-körningen.

      * **Funktionstestning av produkten** - Kör [funktionsprovningar av produkter](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) mot utvecklingsmiljön.
      * **Anpassad funktionstestning** - Kör [anpassade funktionstester](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) mot utvecklingsmiljön.
      * **Testning av anpassat användargränssnitt** - Kör [anpassade gränssnittstester](/help/implementing/cloud-manager/ui-testing.md) för anpassade program.

   ![Pipeline i full hög](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Klicka **Spara**.

Pipelinen sparas och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

### Webbnivåkonfiguration {#web-tier-config}

En konfigurationspipeline för webbskikt Distribuerar konfigurationer för HTTPD/Dispatcher. Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) om du vill ha mer information om den här typen av pipeline.

>[!NOTE]
>
>Om det redan finns en kodrapport på webbnivå för den valda miljön inaktiveras den här markeringen.

Följ de här stegen för att slutföra konfigurationen av icke-produktionsflödet för kod på webbnivå.

1. På **Källkod** måste du definiera följande alternativ.

   * **Berättigade driftsättningsmiljöer** - Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.
   * **Databas** - Det här alternativet definierar från vilken Git-repo pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se dokumentet [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) om du vill lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
   * **Kodplats** - Det här alternativet definierar den sökväg i förgreningen för den valda rapporten från vilken pipelinen ska hämta koden.
      * För konfigurationspipelines på webbnivå är detta vanligtvis sökvägen som innehåller `conf.d`, `conf.dispatcher.d`och `opt-in` kataloger.
      * Om projektstrukturen till exempel genererades från [AEM Project Archetype,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) banan `/dispatcher/src`.

   ![Rörledning på webbnivå](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Klicka **Spara**.

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
