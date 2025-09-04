---
title: Dela endast scenen och endast produktion
description: Lär dig hur du kan dela upp driftsättningar för staging och produktion med dedikerade pipelines.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines"
source-git-commit: 09a1bccd03d4efb277c8f3bb5baf6dbaaa8b6d87
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---

# Dela rörledningar enbart för stadier och endast för produktion {#stage-prod-only}

Du kan dela upp distributioner för staging och produktion med hjälp av dedikerade pipelines.

## Ökning {#overview}

Mellanlagrings- och produktionsmiljöer är nära kopplade. Som standard är distributioner till dem länkade till en enda pipeline. Det vill säga, en driftsättningspipeline distribueras till både testnings- och produktionsmiljöerna i det programmet. Även om denna koppling normalt är lämplig, finns det vissa användningsområden där det finns nackdelar:

* Om du vill distribuera till enbart scenen avvisar du steget **Befordra till produkt** i pipeline. Körningen markeras dock som avbruten.
* Om du vill distribuera den senaste koden i en staging-miljö till produktion måste du distribuera om hela pipelinen inklusive staging-distributionen även om ingen kod har ändrats där.
* Det går inte att uppdatera miljöer under distributioner. Om du pausar för att testa i testmiljön i flera dagar innan du befordrar till produktion, är produktionsmiljön fortfarande låst och kan inte uppdateras. Det här scenariot gör icke-beroende aktiviteter som att uppdatera [miljövariabler](/help/implementing/cloud-manager/environment-variables.md) omöjliga.

Enkla rörledningar för scener och enbart för produkter erbjuder lösningar för dessa användningsområden genom att tillhandahålla dedikerade driftsättningsalternativ.

* **Distributionsförlopp endast för scenen:** Distribuerar bara till en staging-miljö där körningen är klar när distributionen och testerna är klara. En pipeline som bara är i ett steg fungerar på samma sätt som den standardkopplade kompletta stackproduktionskanalen, men utan stegen för produktionsdistribution (godkännande, schema, driftsättning).
* **Distributionsförlopp endast för produktion:** Distribuerar endast till produktion genom att välja den senaste lyckade scenkörningen. Distribuera sedan dess artefakter till produktionen. Med rörledningar som endast är avsedda för produktion återanvänds scenens distributionsartefakter, utan att byggfasen slutförs.

Rörledningar med endast scener och endast produkter utförs inte medan en produktionspipeline med fullständig stackproduktion pågår, och vice versa. Om utlösaren **On Git Changes** är konfigurerad för både produktionsflödet för enbart scenen och hela stacken och pekar på samma gren och databas, startas endast den enbart för scenen automatiskt. Skrivskyddade pipelines startar inte **`On Git Changes`** eftersom de inte är direkt länkade till en databas.

Rörledningar som endast är avsedda för produktion aktiveras manuellt eftersom de inte är direkt länkade till en databas för **Vid Git-ändringar**.

De här dedikerade rörledningarna ger större flexibilitet, men du bör notera följande detaljer om drift och rekommendationer.

>[!NOTE]
>
>I rörledningar som endast är avsedda för produktion används alltid artefakter från den pipeline som bara är till för scenen. Detta gäller även om standardproduktionsflödet under tiden har driftsatt något annat på scenen.
>
>* Scenariot kan leda till oönskade kodåterställningar.
>* Adobe rekommenderar att du slutar använda den kopplade standardproduktionskanalen när du väl har börjat använda pipelines som endast är för prod och endast för scenen.
>* Om du fortfarande bestämmer dig för att köra både standardrörledningarna och rörledningar för scen/endast för produkt, bör du tänka på att artefakter återanvänds för att undvika att koda om.

## Skapa pipeline {#pipeline-creation}

Rörledningar som endast är avsedda för produktion och endast för scenen skapas på ungefär samma sätt som standardanslutna [produktionspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) och [icke-produktionspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Mer information finns i de dokumenten.

1. Klicka på **Lägg till pipeline** i fönstret **Pipelines**.

   * Välj **Lägg till icke-produktionsförlopp** om du vill [skapa en pipeline som bara är för scenen](#stage-only).
   * Välj **Lägg till endast produktion i pipeline** för att [skapa en pipeline som bara är avsedd för produktion](#prod-only).

![Skapar en pipeline enbart för produkt/scen](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>Vissa alternativ kan vara nedtonade om motsvarande rörledningar redan finns.
>
>* **Lägg till endast produktion i pipeline** är inte tillgängligt om det inte finns någon pipeline som bara är för stadiet än.
>* **Lägg till produktionspipeline** är inte tillgängligt om det redan finns en kopplad standardpipeline.
>* Endast en prod- och endast en fasledning tillåts per program.

### Skapa en pipeline som bara är en mellannivå {#stage-only}

1. I dialogrutan **Lägg till icke-produktionspipeline** väljer du fältet **Distributionspipeline** för din pipeline på fliken **Konfiguration**.
1. Ange ett namn på fritext i fältet Namn på icke-produktionsförlopp.
1. Välj önskade distributionsalternativ och klicka sedan på **Fortsätt**.

   ![Fliken Konfiguration i dialogrutan Lägg till icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. På fliken **Source Code** väljer du **Full Stack Code**. Med det här alternativet byggs och distribueras hela AEM-programmet (serverdelen, Dispatcher/web tier config och alla front end-moduler i svaret).

1. I listrutan **Godtagbara distributionsmiljöer** väljer du **stage** -miljön som distributionsmiljö för din pipeline. När du väljer fas skapas en pipeline som är dedikerad till scenmiljön (produktionskampanjen sker i en separat pipeline).

1. Välj din **databas** och **Git-gren** i respektive listruta och klicka sedan på **Fortsätt**.

   ![Fliken Source-kod i dialogrutan Lägg till icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. På fliken **Experience Audit** är den angivna webbplats-URL:en den publicerings-URL som Cloud Manager granskar för sidkvalitet.

1. I fältet **Sidsökväg** anger du vilka sidor du vill granska och klickar sedan på **![Lägg till ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) Lägg till sida** .

   Experience Audit analyserar varje väg ni lägger till för prestanda, tillgänglighet, progressiva webbprogram, bästa praxis, SEO och andra kvalitetskontroller. Du kan lägga till flera banor och ta bort alla genom att klicka på ikonen ![Korsstorlek 400](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg) .

   ![Fliken Experience Audit (Upplevelsegranskning) i dialogrutan Add Non-Production Pipeline (Lägg till icke-produktionsförlopp)](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. Klicka på **Spara**.


### Skapa en pipeline som endast är avsedd för produktion {#prod-only}

1. I dialogrutan **Lägg till endast produktionspipeline** anger du sluttextnamnet för pipelinen i textfältet **Namn på pipeline**.
1. Skriv det namn du vill ha i fältet **Pipelinenamn**.
1. Under **Alternativ för produktionsdistribution** väljer du **Paus innan du distribuerar till produktion**.

   Med det här alternativet infogas en manuell godkännandeport precis före produktionssteget. Pipelinen stoppar och väntar på att en godkännare (t.ex. en Distributionshanterare eller en Business Owner) ska godkänna eller avbryta produktionsdistributionen.

   Använd detta för ändringskontroll eller sista-minuten-kontroller.

1. Klicka på **Spara** om du vill skapa en pipeline som bara är för produktion med dessa alternativ.

   ![Skapar en pipeline som endast är avsedd för produktion](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## Köra rörledningar med enbart scener och enbart prod {#running}

Du kan starta de nya pipelinerna [precis som andra pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). Du kan även utlösa en pipeline som bara är avsedd för produktion direkt från en pipeline som bara är för ett steg och som har körningsinformation.

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### Köra rörledningar som bara innehåller scenen {#stage-only-run}

I körningsinformationen visas en **Befordra bygge**-knapp efter teststegen. Klicka på den om du vill utlösa en pipeline som bara är avsedd för produktion och som distribuerar den här körningens scendefekter till produktionen. Knappen visas endast vid den senaste körningen av enbart scenen.

![En pipeline som endast är för scenen körs](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

När du klickar på **Befordra bygge** öppnas en bekräftelsedialogruta om det finns en pipeline som endast är avsedd för scenen. Klicka på **Kör**.

![Befordra bygge - Kör pipeline-dialogruta](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

Om det inte finns någon dialogruta uppmanas du att skapa en.

![Befordra bygge - Ingen giltig pipeline-dialogruta](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### Kör prod-only-pipelines {#prod-only-run}

För en **pipeline som bara är avsedd för produktion**, visar Cloud Manager källartefakterna som distribueras till produktionen. Kontrollera steget **Förberedelse av felaktigheter** för källkörningen och öppna det för att visa information och loggar.


![Information om felaktigheter](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)

