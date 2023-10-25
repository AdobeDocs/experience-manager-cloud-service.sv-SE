---
title: Konfigurera icke-produktionsförlopp
description: Lär dig hur du konfigurerar icke-produktionsrörledningar för att testa kodens kvalitet innan du distribuerar den till produktionsmiljöer.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---


# Konfigurera icke-produktionsförlopp {#configuring-non-production-pipelines}

Lär dig hur du konfigurerar icke-produktionsrörledningar för att testa kodens kvalitet innan du distribuerar den till produktionsmiljöer.

En användare måste ha **[Distributionshanteraren](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** roll för att konfigurera icke-produktionsrörledningar.

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

1. Öppna **Pipelines** från startskärmen i Cloud Manager. Klicka **+Lägg till** och markera **Lägg till icke-produktionsförlopp**.

   ![Lägg till icke-produktionsflöde](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. På **Konfiguration** -fliken i **Lägg till icke-produktionsförlopp** väljer du vilken typ av icke-produktionsflöde du ska lägga till.

   * **Kodkvalitetspipeline** - Skapa en pipeline som bygger din kod, kör enhetstester och utvärderar kodkvaliteten, men distribuerar INTE.
   * **Distributionsförlopp** - Skapa en pipeline som bygger din kod, kör enhetstester, utvärderar kodkvaliteten och distribuerar till en miljö.

   ![Dialogrutan Lägg till icke-produktionsförlopp](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Ange en **Namn på icke-produktionsförlopp** för att identifiera ditt flöde tillsammans med följande ytterligare information.

   * **Utlösare för distribution** - Du har följande alternativ när du definierar distributionsutlösare för att starta pipeline.

      * **Manuell** - Använd det här alternativet om du vill starta pipelinen manuellt.
      * **Vid Git-ändringar** - Det här alternativet startar CI/CD-flödet när implementeringar läggs till i den konfigurerade Git-grenen. Med det här alternativet kan du fortfarande starta pipelinen manuellt efter behov.

1. Om du väljer att skapa en **Distributionsförlopp** måste du också definiera **Beteende vid viktiga måttfel**.

   * **Fråga varje gång** - Det här beteendet är standardinställningen och kräver manuell åtgärd vid viktiga fel.
   * **Misslyckas omedelbart** - Om du väljer det här alternativet avbryts pipelinen när ett viktigt fel inträffar. Det emulerar i princip en användare som manuellt avvisar varje fel.
   * **Fortsätt omedelbart** - Om du väljer det här alternativet fortsätter pipeline automatiskt när ett viktigt fel inträffar. Det emulerar i princip en användare som manuellt godkänner varje fel.

1. Klicka **Fortsätt**.

1. På **Källkod** -fliken i **Lägg till icke-produktionsförlopp** måste du välja vilken typ av kod som pipeline ska bearbeta.

   * **[Fullständig stapelkod](#full-stack-code)**
   * **[Målinriktad distribution](#targeted-deployment)**

Se dokumentet [CI/CD-rör](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) för mer information om olika typer av rörledningar.

Hur du slutför skapandet av din icke-produktionsprocess varierar beroende på vilken typ av källkod du har valt. Följ länkarna ovan för att gå till nästa avsnitt i det här dokumentet så att du kan slutföra konfigurationen av din pipeline.

### Fullständig stapelkod {#full-stack-code}

En fullständig kodrapport distribuerar samtidigt kodbyggen i bakände och i framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationen.

>[!NOTE]
>
>Om det finns en kodrapport med fullständig stapel för den valda miljön inaktiveras den här markeringen.

Följ de här stegen för att slutföra konfigurationen av icke-produktionsflödet för kod i helhög.

1. På **Källkod** måste du definiera följande alternativ.

   * **Berättigade driftsättningsmiljöer** - Om din pipeline är en distributionsprocess måste du välja till vilka miljöer den ska distribueras.
   * **Databas** - Det här alternativet definierar från vilken Git-repo som pipelinen ska hämta koden.

   >[!TIP]
   > 
   >Se [Lägga till och hantera databaser](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) så att du kan lära dig hur du lägger till och hanterar databaser i Cloud Manager.

   * **Git-gren** - Det här alternativet definierar från vilken gren i den valda pipeline som ska hämta koden.
      * Ange de första tecknen i förgreningsnamnet och funktionen Komplettera automatiskt i det här fältet. Det hjälper dig att hitta matchande grenar som du kan välja.
   * **Ignorera webbnivåkonfiguration** - När du markerar det här alternativet distribueras inte webbnivåkonfigurationen.
   * **Pipeline** - Om din pipeline är en distributionsprocess kan du välja att köra en testfas. Markera de alternativ som du vill aktivera i den här fasen. Om inget av alternativen är markerat visas inte testfasen när pipeline körs.

      * **Funktionstestning av produkten** - Kör [funktionsprovningar av produkter](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) mot utvecklingsmiljön.
      * **Anpassad funktionstestning** - Kör [anpassade funktionstester](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) mot utvecklingsmiljön.
      * **Anpassade gränssnittstestningar** - Kör [anpassade gränssnittstester](/help/implementing/cloud-manager/ui-testing.md) för anpassade program.
      * **Experience Audit** - Kör [Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md)

   ![Pipeline i full hög](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Klicka **Spara**.

Pipelinen har sparats och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

### Målinriktad distribution {#targeted-deployment}

En riktad distribution distribuerar bara kod för utvalda delar av AEM. I en sådan distribution kan du välja **Inkludera** någon av följande typer av kod:

* **[Konfig](#config)** - Konfigurera inställningar för din AEM, underhållsuppgifter, CDN-regler med mera.
   * Se dokumentet [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) om du vill lära dig hur du hanterar trafikfilterregler i din databas så att de distribueras på rätt sätt.
* **[Front End-kod](#front-end-code)** - Konfigurera JavaScript och CSS för den främre delen av AEM.
   * Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.
   * Se dokumentet [Developing Sites with the Front-End Pipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) om hur den här processen fungerar tillsammans med vissa överväganden för att vara medveten om att utnyttja hela potentialen i den här processen.
* **[Webbnivåkonfiguration](#web-tier-config)** - Konfigurera dispatcheregenskaper för att lagra, bearbeta och leverera webbsidor till klienten.

>[!NOTE]
>
>* Om det finns en kodrapport på webbnivå för den valda miljön är det här valet inaktiverat.
>* Om du har en befintlig pipeline som distribueras i en hel hög till en miljö, kommer den befintliga konfigurationen på hela stacken att ignoreras om du skapar en konfigurationspipeline för en webbskikt för samma miljö.
> * Det kan bara finnas en enda pipeline för konfigurationsdistribution per miljö.

Stegen för att slutföra skapandet av din icke-produktion, målinriktade distributionsprocess är desamma när du väljer en distributionstyp.

1. Välj vilken distributionstyp du behöver.

![Alternativ för målinriktad distribution](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

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

   ![Konfigurerar distributionspipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment.png)

1. Klicka **Spara**.

Pipelinen har sparats och du kan nu [hantera dina rörledningar](managing-pipelines.md) på **Pipelines** på **Programöversikt** sida.

När en riktad distributionsprocess körs, konfigurationer [såsom WAF-konfigurationer](/help/security/traffic-filter-rules-including-waf.md) distribueras, förutsatt att de sparas i den miljö, databas och gren som du definierade i pipeline.

## Hoppa över Dispatcher-paket {#skip-dispatcher-packages}

Om du vill att Dispatcher-paket ska byggas som en del av pipeline, men inte vill att de ska publiceras för att skapa lagring, kan du inaktivera publicering av dem, vilket kan minska körningstiden för pipeline.

Följande konfiguration för att inaktivera publicering av Dispatcher-paket måste läggas till via ditt projekt `pom.xml` -fil. Den baseras på en miljövariabel, som fungerar som en flagga som du kan ange i Cloud Managers byggbehållare för att definiera när Dispatcher-paket ska ignoreras.

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
