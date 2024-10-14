---
title: Lägg till en icke-produktionspipeline
description: Lär dig hur du lägger till en icke-produktionsprocess för att testa kvaliteten på koden innan du distribuerar den till produktionsmiljöer.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---


# Lägg till en icke-produktionspipeline {#configuring-non-production-pipelines}

Lär dig hur du konfigurerar icke-produktionsrörledningar för att testa kodens kvalitet innan du distribuerar den till produktionsmiljöer.

En användare måste ha rollen **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** för att kunna konfigurera icke-produktionspipelines.

## Icke-produktionsrörledningar {#non-production-pipelines}

Utöver [produktionspipelines](#configuring-production-pipelines.md) som distribueras till stagings- och produktionsmiljöer kan du även konfigurera icke-produktionspipelines för att validera koden.

Det finns två typer av icke-produktionsrörledningar:

* **Kodkvalitetsförgreningar** - Dessa kör kodkvaliteten genom att skanna koden i en Git-förgrening och kör stegen för bygg- och kodkvalitet.
* **Distributionspipelines** - Förutom att utföra steg för bygg- och kodkvalitet, som till exempel pipelines för kodkvalitet, distribuerar dessa pipelines koden till en icke-produktionsmiljö.

>[!NOTE]
>
>Du kan [redigera pipeline-inställningar](managing-pipelines.md) efter den första konfigurationen.

## Lägg till en ny icke-produktionspipeline {#adding-non-production-pipeline}

När du har konfigurerat programmet och har minst en miljö med Cloud Manager UI är du redo att lägga till en icke-produktionsprocess genom att följa de här stegen.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till kortet **Pipelines** från Cloud Manager hemskärm. Klicka på **+Lägg till** och välj **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. På fliken **Konfiguration** i dialogrutan **Lägg till icke-produktionsförlopp** väljer du den typ av icke-produktionsförlopp du ska lägga till.

   * **Kodkvalitetspipeline** - Skapa en pipeline som bygger din kod, kör enhetstester och utvärderar kodkvaliteten, men som INTE distribueras.
   * **Distributionspipeline** - Skapa en pipeline som bygger din kod, kör enhetstester, utvärderar kodkvalitet och distribuerar till en miljö.

   ![Lägg till icke-produktion-pipeline-dialogruta](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Ange ett **icke-produktionsförloppsnamn** för att identifiera din pipeline tillsammans med följande ytterligare information.

   * **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

      * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
      * **Vid Git-ändringar** - Det här alternativet startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

1. Om du väljer att skapa en **distributionspipeline** måste du också definiera beteendet **Viktiga måttfel**.

   * **Fråga varje gång** - Det här beteendet är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckades omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Det emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Det emulerar i princip en användare som manuellt godkänner varje fel.

1. Klicka på **Fortsätt**.

1. På fliken **Source Code** i dialogrutan **Add Non-Production Pipeline** måste du välja vilken typ av kod som pipeline ska bearbeta.

   * **[Fullständig stackkod](#full-stack-code)**
   * **[Måldistribution](#targeted-deployment)**

Mer information om olika typer av pipelines finns i [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Hur du slutför skapandet av din icke-produktionsprocess varierar beroende på vilken typ av källkod du har valt. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet så att du kan slutföra konfigurationen av din pipeline.

### Fullständig stapelkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfiguration.

>[!NOTE]
>
>Om det finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

Följ de här stegen för att slutföra konfigurationen av icke-produktionsflödet för kod i helhög.

1. På fliken **Source Code** måste du definiera följande alternativ.

   * **Berättigade distributionsmiljöer** - Om din pipeline är en distributionspipeline måste du välja till vilka miljöer den ska distribueras.
   * **Databas** - Det här alternativet definierar från vilken Git-repo som pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-grenen** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet. Det hjälper dig att hitta matchande grenar som du kan välja.
   * **Ignorera webbnivåkonfiguration** - När det här alternativet är markerat distribueras inte webbnivåkonfigurationen.
   * **Pipeline** - Om din pipeline är en distributionspipeline kan du välja att köra en testfas. Markera de alternativ som du vill aktivera i den här fasen. Om inget av alternativen är markerat visas inte testfasen när pipeline körs.

      * **Funktionstestning av produkt** - Kör [produktfunktionstester](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) mot utvecklingsmiljön.
      * **Anpassad funktionstestning** - Kör [anpassade funktionstester](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) mot utvecklingsmiljön.
      * **Anpassad gränssnittstestning** - Kör [anpassade gränssnittstester](/help/implementing/cloud-manager/ui-testing.md) för anpassade program.
      * **Experience Audit** - Kör [Experience Audit](/help/implementing/cloud-manager/experience-audit-dashboard.md)

   ![Pipeline i full hög](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Klicka på **Spara**.

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
>Rörledningar för webbnivå och konfiguration stöds inte i privata databaser. Mer information och en fullständig lista över begränsningar finns i [Lägga till privata databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Stegen för att slutföra skapandet av din icke-produktion, målinriktade distributionsprocess är desamma när du väljer en distributionstyp.

1. Välj vilken distributionstyp du behöver.

![Målinriktade distributionsalternativ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

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
   * **Rörledning** - För rörledningar som inte är avsedda för produktion i början har du möjlighet att aktivera **[Experience Audit](/help/implementing/cloud-manager/experience-audit-dashboard.md)**.

   ![Konfigurera pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)

1. Om du har aktiverat Experience Audit klickar du på **Continue** för att gå vidare till fliken **Experience Audit** där du kan definiera sökvägarna som alltid ska inkluderas i Experience Audit.

   * Om du har aktiverat **Experience Audit** finns mer information om hur du konfigurerar i dokumentet [Experience Audit](/help/implementing/cloud-manager/experience-audit-dashboard.md).
   * Om du inte gjorde det hoppar du över det här steget.

1. Klicka på **Spara** för att spara pipeline.

Pipelinen sparas och du kan nu [hantera dina pipelines](managing-pipelines.md) på kortet **Pipelines** på sidan **Programöversikt**.

## Hoppa över Dispatcher-paket {#skip-dispatcher-packages}

Om du vill att Dispatcher-paket ska byggas som en del av pipeline men inte vill att de ska publiceras för att skapa lagringsutrymme, kan du inaktivera publiceringen, vilket kan minska körningstiden för pipeline.

Följande konfiguration för att inaktivera publicering av Dispatcher-paket måste läggas till via projektfilen `pom.xml`. Den baseras på en miljövariabel, som fungerar som en flagga som du kan ange i Cloud Manager byggbehållare för att definiera när Dispatcher-paket ska ignoreras.

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
