---
title: Skapa och synkronisera Live-kopior
description: Lär dig hur du skapar och synkroniserar Live-kopior för att återanvända innehållet på hela webbplatsen.
feature: Multi Site Manager
role: Admin
exl-id: 53ed574d-e20d-4e73-aaa2-27168b9d05fe
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '4270'
ht-degree: 0%

---

# Skapa och synkronisera Live-kopior {#creating-and-synchronizing-live-copies}

Du kan skapa en Live-kopia från en sida eller en plantryckskonfiguration för att återanvända innehållet på hela webbplatsen. Hantera arv och synkronisering. Du kan styra hur ändringar av innehållet ska spridas.

## Hantera layoutkonfigurationer {#managing-blueprint-configurations}

En plankonfiguration identifierar en befintlig webbplats som du vill använda som källa för en eller flera Live Copy-sidor.

>[!TIP]
>
>Med layoutkonfigurationer kan du överföra innehållsändringar till Live-kopior. Se [Live-kopior - Source, utkast och layoutkonfigurationer](overview.md#source-blueprints-and-blueprint-configurations).

När du skapar en ritningskonfiguration väljer du en mall som definierar den interna strukturen för ritningen. Standardmallen för utkast förutsätter att källwebbplatsen har följande egenskaper:

* Webbplatsen har en rotsida.
* De direkt underordnade sidorna i roten är språkgrenar på webbplatsen. När du skapar en Live-kopia visas språken som valfritt innehåll som ska inkluderas i kopian.
* Roten för varje språkgren har en eller flera underordnade sidor. När du skapar en Live-kopia visas underordnade sidor så att du kan ta med dem i Live-kopian.

>[!NOTE]
>
>En annan struktur kräver en annan designmall.

När du har skapat en ritningskonfiguration konfigurerar du följande egenskaper:

* **Namn**: Namnet på designkonfigurationen
* **Source-sökväg**: Sökvägen till rotsidan på webbplatsen som du använder som källa (utkast)
* **Beskrivning**. (Valfritt) En beskrivning av designkonfigurationen, som visas i listan över designkonfigurationer att välja mellan när du skapar en webbplats

När du använder en ritningskonfiguration kan du associera den med en utrullningskonfiguration som bestämmer hur Live-kopior av källan/ritytan synkroniseras. Se [Ange vilka utrullningskonfigurationer som ska användas](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use).

### Skapa och redigera layoutkonfigurationer {#creating-editing-blueprint-configurations}

Blåtryckskonfigurationer betraktas som oföränderliga data och kan därför inte redigeras under körning. Därför måste alla konfigurationsändringar distribueras via Git med CI/CD-pipeline.

Mer information finns i artikeln [Antagbara ändringar av Adobe Experience Manager (AEM) as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Följande steg är bara tillgängliga för en administratör på en lokal utvecklingsinstans för testnings- och utvecklingssyften. Dessa alternativ är inte tillgängliga i någon AEMaaCS-molninstans.

#### Skapa en skissformskonfiguration lokalt {#creating-a-blueprint-configuration}

Så här skapar du en ritningskonfiguration:

1. [Navigera](/help/sites-cloud/authoring/basic-handling.md#global-navigation) till menyn **Verktyg** och välj sedan menyn **Platser** .
1. Välj **utkast** för att öppna konsolen **Skapa utkast**:

   ![Utskriftskonfigurationer](../assets/blueprint-configurations.png)

1. Välj **Skapa**.
1. Välj en ritningsmall och sedan **Nästa** för att fortsätta.
1. Välj den källsida som ska användas som utkast och **Nästa** för att fortsätta.
1. Definiera:

   * **Titel**: obligatorisk titel för ritningen
   * **Beskrivning**: En valfri beskrivning som ger mer information.

1. **Skapa** skapar en ritningskonfiguration baserat på din specifikation.

### Redigera eller ta bort en utkastkonfiguration lokalt{#editing-or-deleting-a-blueprint-configuration}

Du kan redigera eller ta bort en befintlig ritningskonfiguration:

1. [Navigera](/help/sites-cloud/authoring/basic-handling.md#global-navigation) till menyn **Verktyg** och välj sedan menyn **Platser** .
1. Välj **utkast** för att öppna konsolen **Skapa utkast**:

   ![Utskriftskonfigurationer](../assets/blueprint-configurations.png)

1. Välj önskad konfiguration av utkast - lämpliga åtgärder blir tillgängliga i verktygsfältet:

   * **Egenskaper**; du kan använda detta för att visa och sedan redigera egenskaperna för konfigurationen.
   * **Ta bort**

## Skapa en Live Copy {#creating-a-live-copy}

Du kan skapa en Live-kopia på flera olika sätt.

### Skapa en Live-kopia av en sida {#creating-a-live-copy-of-a-page}

Du kan skapa en Live-kopia av vilken sida eller gren som helst. När du skapar Live-kopian kan du ange vilka rollout-konfigurationer som ska användas för att synkronisera innehållet:

* De valda rollout-konfigurationerna gäller för Live Copy-sidan och dess underordnade sidor.
* Om du inte anger några utplaceringskonfigurationer avgör MSM vilka utplaceringskonfigurationer som ska användas. Se [Ange vilken utrullningskonfiguration som ska användas](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use).

Du kan skapa en Live-kopia av vilken sida som helst:

* Sidor som refereras av en [blå konfiguration](#creating-a-blueprint-configuration)
* Och sidor som inte har någon anslutning till en konfiguration
* Live-kopia på sidorna i en annan Live-kopia ([kapslade Live-kopior](overview.md#nested-live-copies))

Den enda skillnaden är att tillgängligheten för kommandot **Rollout** på käll-/plantryckssidorna är beroende av om källan refereras av en plantryckskonfiguration:

* Om du skapar Live-kopian från en källsida som **är** refererad till i en ritningskonfiguration, är kommandot Rollout tillgängligt på käll-/ritningssidan.
* Om du skapar Live-kopian från en källsida som **inte** refereras till i en ritningskonfiguration, kommer kommandot Rollout inte att vara tillgängligt på käll-/ritningssidorna.

Så här skapar du en Live-kopia:

1. I konsolen **Platser** väljer du **Skapa** och sedan **Live-kopia**.

   ![Skapa Live-kopia](../assets/create-live-copy.png)

1. Markera källsidan och välj sedan **Nästa**. Till exempel:

   ![Välj Live Copy-källa](../assets/live-copy-from.png)

1. Ange målsökvägen för Live-kopian (öppna den överordnade mappen/sidan för Live-kopian) och välj sedan **Nästa**.

   ![Välj mål för Live-kopia](../assets/live-copy-to.png)

   >[!NOTE]
   >
   >Målsökvägen får inte finnas i källsökvägen.

1. Ange:

   * en **rubrik** för sidan.
   * ett **namn** som används i URL:en.

   ![Live Copy-egenskaper](../assets/live-copy-properties.png)

1. Använd kryssrutan **Uteslut undersidor**:

   * Markerad: skapa en Live-kopia av endast den markerade sidan (grund Live-kopia)
   * Inte markerad: skapa en Live-kopia som innehåller alla underordnade till den markerade sidan (djup Live-kopia)

1. (Valfritt) Om du vill ange en eller flera utrullningskonfigurationer som ska användas för Live-kopian använder du listrutan **Utrullningskonfigurationer** för att välja dem. Markerade konfigurationer visas under den nedrullningsbara väljaren.
1. Välj **Skapa**. Ett bekräftelsemeddelande visas. Här kan du välja antingen **Öppna** eller **Klar**.

   >[!NOTE]
   >
   >Ett felmeddelande kan visas med meddelandet&quot;Det gick inte att skicka formuläret&quot;. Detta inträffar på grund av en timeout i nätverket. Processen att skapa den aktiva kopian körs emellertid i bakgrunden. Vänta några minuter och kontrollera att sidorna i live-kopian har skapats korrekt.

### Skapa en Live-kopia av en plats från en designkonfiguration {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

Skapa en Live Copy med hjälp av en ritningskonfiguration för att skapa en webbplats baserad på innehållet i ritningen (källan). När du skapar en Live-kopia från en ritningskonfiguration väljer du en eller flera språkgrenar i den ritningskälla som ska kopieras och sedan markerar du de kapitel som ska kopieras från språkgrenarna. Se [Skapa en designkonfiguration](#creating-a-blueprint-configuration).

Om du utelämnar vissa språkgrenar från Live-kopian kan du lägga till dem senare. Mer information finns i [Skapa en Live-kopia i en Live-kopia (Konfiguration av utkast)](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration).

>[!CAUTION]
>
>När ritytan innehåller länkar och referenser som aktiverar ett stycke i en annan gren, uppdateras inte målen på sidorna för Live-kopia, utan de är fortfarande kopplade till det ursprungliga målet.

När du skapar platsen anger du värden för följande egenskaper:

* **Ursprungliga språk**: De språkgrenar i den planeringskälla som ska inkluderas i Live Copy
* **Inledande kapitel**: De underordnade sidorna i grenarna för utkast-språk som ska inkluderas i Live-kopian
* **Målsökväg**: Platsen för rotsidan på Live Copy-webbplatsen
* **Titel**: Titeln på rotsidan på webbplatsen Live Copy
* **Namn**: (Valfritt) Namnet på JCR-noden som lagrar Live-kopians rotsida (standardvärdet baseras på titeln)
* **Webbplatsägare**: (Valfritt) Information om den part som ansvarar för Live Copy
* **Live-kopia**: Välj det här alternativet om du vill skapa en direktrelation med källwebbplatsen. Om du inte markerar det här alternativet skapas en kopia av ritningen, men den synkroniseras inte med källan.
* **Utrullningskonfigurationer**: (Valfritt) Välj en eller flera utrullningskonfigurationer som ska användas för synkronisering av Live-kopian. Som standard ärvs utrullningskonfigurationerna från ritningen. Mer information finns i [Ange vilka utrullningskonfigurationer som ska användas](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use).

Så här skapar du en Live-kopia av en webbplats från en designkonfiguration:

1. I konsolen **Platser** väljer du **Skapa** och sedan **Plats** i listrutan.
1. Välj den designkonfiguration som ska användas som källa för Live-kopian och fortsätt med **Nästa**:

   ![Skapa webbplats från utkast](../assets/create-site-from-blueprint.png)

1. Använd väljaren **Inledande språk** för att ange vilka språk som ska användas för Live-kopian på webbplatsen för utkast.

   Alla tillgängliga språk är markerade som standard. Om du vill ta bort ett språk markerar du **X** som visas bredvid språket.

   Till exempel:

   ![Ange egenskaper när du skapar platsen](../assets/create-site-properties.png)

1. Använd listrutan **Inledande kapitel** för att välja de avsnitt i ritningen som ska ingå i Live-kopian. Alla tillgängliga kapitel inkluderas som standard, men kan tas bort.
1. Ange värden för de återstående egenskaperna och välj sedan **Skapa**. I bekräftelsedialogrutan väljer du **Klar** för att återgå till konsolen **Platser** eller **Öppna platsen** för att öppna webbplatsens rotsida.

### Skapa en Live-kopia i en Live-kopia (utkast-konfiguration) {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

När du skapar en Live-kopia i den befintliga Live-kopian (som skapats med en ritningskonfiguration) kan du infoga en eller flera språkversioner som inte fanns med när Live-kopian skapades.

## Övervaka din Live Copy {#monitoring-your-live-copy}

### Se status för en Live-kopia {#seeing-the-status-of-a-live-copy}

Egenskaperna för en Live Copy-sida visar följande information om Live Copy:

* **Source**: Källsidan för Live Copy-sidan
* **Status**: Synkroniseringsstatusen för Live-kopian, inklusive om Live-kopian är uppdaterad med källan, när den senaste synkroniseringen inträffade och vem som utförde synkroniseringen
* **Konfiguration**:

   * Om sidan fortfarande omfattas av Live Copy-arv
   * Om konfigurationen ärvs från den överordnade sidan
   * Alla utrullningskonfigurationer som används i Live Copy

Så här visar du egenskaperna:

1. I konsolen **Platser** väljer du sidan Live-kopia och öppnar egenskaperna.
1. Välj fliken **Live-kopia**.

   Till exempel:

   ![Fliken Live-kopia i sidegenskaper](../assets/live-copy-inherit.png)

   Mer information finns i avsnittet [Använda Live-kopieringsöversikt](live-copy-overview.md#using-the-live-copy-overview) i artikeln Live-kopieringsöversiktskonsolen.

### Visa Live-kopior av en blå sida {#seeing-the-live-copies-of-a-blueprint-page}

Du får en lista över de Live Copy-sidor som använder den aktuella (utkast) sidan som källa för utkast (som refereras i en designkonfiguration). Använd den här listan för att hålla reda på Live-kopior. Listan visas på fliken **Utskrift** i [sidegenskaperna](/help/sites-cloud/authoring/sites-console/page-properties.md).

![Fliken Utskrift för sidegenskaper](../assets/live-copy-blueprint-tab.png)

## Synkronisera din Live-kopia {#synchronizing-your-live-copy}

Du kan synkronisera din Live-kopia på flera olika sätt.

### Rulla ut ett utkast {#rolling-out-a-blueprint}

Rulla ut en ritningssida för att överföra innehållsändringar till Live-kopior. En **utrullningsåtgärd** kör de utrullningskonfigurationer som använder utlösaren [Vid utrullning](live-copy-sync-config.md#rollout-triggers).

>[!NOTE]
>
>Konflikter kan uppstå om nya sidor med samma sidnamn skapas både i den blå grenen och i en beroende Live Copy-gren.
>
>Sådana [konflikter måste hanteras och lösas vid utrullning](rollout-conflicts.md).

#### Skapa en skiss från Sidegenskaper {#rolling-out-a-blueprint-from-page-properties}

1. I konsolen **Platser** markerar du sidan i planen och öppnar egenskaperna.
1. Öppna fliken **Utskrift**.
1. Välj **Rollout**.

   ![Utrullningsknapp](../assets/rollout.png)

1. Ange sidorna och eventuella underordnade sidor och bekräfta sedan med bockmarkeringen:

   ![Välj sidor att rulla ut](../assets/select-rollout-pages.png)

1. Ange om utrullningsjobbet ska köras omedelbart (**nu**) eller vid ett annat datum/tid (**senare**).

   ![Definiera utrullningstid](../assets/rollout-now-later.png)

Utsläppen bearbetas som asynkrona jobb och kan kontrolleras på sidan [***Status för asynkrona jobb**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations).

#### Rulla ut en skiss från referensspåret {#roll-out-a-blueprint-from-the-reference-rail}

1. I konsolen **Platser** markerar du sidan i den aktiva kopian och öppnar panelen **[Referenser](/help/sites-cloud/authoring/basic-handling.md#references)** (i verktygsfältet).
1. Välj alternativet **Utskrift** i listan om du vill visa de utkast som är associerade med den här sidan.
1. Välj önskad rityta i listan.
1. Välj **Rollout**.

   ![Utrullningsutkast från referenslinjen](../assets/rollout-blueprint-from-references.png)

1. Du ombeds bekräfta information om utrullningen:

   * **Utrullningsomfång**:

     Ange om omfånget gäller enbart för den valda sidan eller om det ska omfatta underordnade sidor.

   * **Schema**:

     Ange om utrullningsjobbet ska köras omedelbart (**nu**) eller vid ett senare datum/tid (**senare**).

     ![Definiera utrullningsområde och schema](../assets/rollout-scope-schedule.png)

1. När du har bekräftat informationen väljer du **Rollout** för att utföra åtgärden.

Utsläppen bearbetas som asynkrona jobb och kan kontrolleras på sidan [**Status för asynkrona jobb**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations).

#### Rulla ut en utkast från Live Copy-översikt {#roll-out-a-blueprint-from-the-live-copy-overview}

Åtgärden [**Utrullning** är även tillgänglig från Live-kopieringsöversikten](live-copy-overview.md#using-the-live-copy-overview) när en utskrivningssida är markerad.

1. Öppna [Live Copy Overview](live-copy-overview.md#using-the-live-copy-overview) och välj en designsida.
1. Välj **Utrullning** i verktygsfältet.

   ![Live-kopia - översikt](../assets/live-copy-overview-actions-blueprint.png)

1. Ange sidorna och eventuella underordnade sidor och bekräfta sedan med bockmarkeringen:

   ![Välj sidor för utrullning](../assets/select-rollout-pages.png)

1. Ange om utrullningsjobbet ska köras omedelbart (**nu**) eller vid ett annat datum/tid (**senare**).

   ![Definiera distributionsschema](../assets/rollout-now-later.png)

Utsläppen bearbetas som asynkrona jobb och kan kontrolleras på sidan [**Status för asynkrona jobb**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations).

### Synkronisera en Live-kopia {#synchronizing-a-live-copy}

Synkronisera en Live Copy-sida för att dra in innehållsändringar från källan till Live Copy.

#### Synkronisera en Live-kopia från Sidegenskaper {#synchronize-a-live-copy-from-page-properties}

Synkronisera en Live-kopia för att dra ändringar från källan till Live-kopian.

>[!NOTE]
>
>Synkronisering kör de utrullningskonfigurationer som använder utlösaren [Vid utrullning](live-copy-sync-config.md#rollout-triggers).

1. I konsolen **Platser** väljer du sidan Live-kopia och öppnar egenskaperna.
1. Öppna fliken **Live-kopia**.
1. Välj **Synkronisera**.

   ![Knappen Synkronisera](../assets/synchronize.png)

   Bekräftelse krävs. Använd **Synkronisera** för att fortsätta.

#### Synkronisera en Live-kopia från Live Copy-översikt {#synchronize-a-live-copy-from-the-live-copy-overview}

Åtgärden [Synkronisera är också tillgänglig från Live-kopieringsöversikten](live-copy-overview.md#using-the-live-copy-overview) när en Live-kopia-sida är markerad.

1. Öppna [Live Copy-översikten](live-copy-overview.md#using-the-live-copy-overview) och välj en Live-kopieringssida.
1. Välj **Synkronisera** i verktygsfältet.
1. Bekräfta **utrullningsåtgärden** i dialogrutan efter att du har angett om du vill inkludera:

   * **Sidor och undersidor**
   * **Endast sida**

   ![Utrullade sidor med eller utan undersidor](../assets/rollout-page-and-subpages.png)

## Ändra innehåll i Live Copy {#changing-live-copy-content}

Om du vill ändra Live Copy-innehåll kan du:

* Lägg till stycken på sidan.
* Uppdatera befintligt innehåll genom att bryta Live Copy-arvet för alla sidor och komponenter.

>[!TIP]
>
>Om du skapar en sida manuellt i Live Copy, är den nya sidan lokal för Live-kopian, vilket innebär att den inte har någon motsvarande källsida som den är kopplad till.
>
>Ett tips som du kan använda för att skapa en lokal sida som ingår i relationen är att skapa den lokala sidan i källan och utföra en djup utrullning. Då skapas sidan lokalt som Live-kopior.

>[!NOTE]
>
>Konflikter kan uppstå om nya sidor med samma sidnamn skapas både i den blå grenen och i en beroende Live Copy-gren.
>
>Sådana [konflikter måste hanteras och lösas vid utrullning](rollout-conflicts.md).

### Lägga till komponenter på en Live Copy-sida {#adding-components-to-a-live-copy-page}

Du kan när som helst lägga till komponenter på en Live Copy-sida. Live Copy-objektets arvsstatus och dess styckesystem styr inte möjligheten att lägga till komponenter.

När Live Copy-sidan synkroniseras med källsidan ändras inte de tillagda komponenterna. Se även [Ändra ordning på komponenter på en Live-kopieringssida.](#changing-the-order-of-components-on-a-live-copy-page)

>[!TIP]
>
>Ändringar som görs lokalt för en komponent som markerats som en behållare skrivs inte över av innehållet i ritningen i en utrullning. Mer information finns i [Bästa praxis för MSM](best-practices.md#components-and-container-synchronization).

### Pausa arv för en sida {#suspending-inheritance-for-a-page}

När du skapar en Live-kopia sparas Live-kopieringskonfigurationen på rotsidan för de kopierade sidorna. Alla underordnade sidor på rotsidan ärver Live Copy-konfigurationerna. Komponenterna på Live Copy-sidorna ärver också Live Copy-konfigurationen.

Du kan göra uppehåll i Live Copy-arvet för en Live Copy-sida så att du kan ändra sidegenskaper och komponenter. När du gör uppehåll i arv synkroniseras inte längre sidegenskaperna och komponenterna med källan.

>[!TIP]
>
>Du kan också [koppla loss en Live-kopia](#detaching-a-live-copy) från dess utkast om du vill ta bort alla anslutningar. Till skillnad från att avbryta arv är borttagningsåtgärden permanent och icke-återvändbar.

#### Pausa arv från Sidegenskaper {#suspending-inheritance-from-page-properties}

Så här gör du uppehåll i arv på en sida:

1. Öppna egenskaperna för Live-kopieringssidan antingen med kommandot **Visa egenskaper** i konsolen **Webbplatser** eller med **Sidinformation** i verktygsfältet för sidan.
1. Välj fliken **Live-kopia**.
1. Välj **Gör uppehåll** i verktygsfältet. Du kan sedan välja något av följande:

   * **Gör uppehåll**: om du bara vill göra uppehåll för den aktuella sidan.
   * **Gör uppehåll med underordnade**: om du vill göra uppehåll i den aktuella sidan tillsammans med eventuella underordnade sidor.

1. Välj **Gör uppehåll** i bekräftelsedialogrutan.

#### Pausa arv från Live Copy-översikt {#suspending-inheritance-from-the-live-copy-overview}

Åtgärden [Gör uppehåll är även tillgänglig från Live-kopieringsöversikten](live-copy-overview.md#using-the-live-copy-overview) när en Live-kopia-sida är markerad.

1. Öppna [Live Copy-översikten](live-copy-overview.md#using-the-live-copy-overview) och välj en Live-kopieringssida.
1. Välj **Gör uppehåll** i verktygsfältet.
1. Välj lämpligt alternativ från:

   * **Gör uppehåll**
   * **Pausa med underordnade**

   ![Pausa med underordnade](../assets/suspend-with-children.png)

1. Bekräfta åtgärden **Gör uppehåll** i dialogrutan **Gör uppehåll i Live-kopia**:

   ![Bekräfta uppehåll](../assets/confirm-suspend.png)

### Återuppta arv för en sida {#resuming-inheritance-for-a-page}

Att skjuta upp Live Copy-arv för en sida är en tillfällig åtgärd. När åtgärden **Återuppta** har pausats blir den tillgänglig så att du kan återskapa den aktiva relationen.

![Återuppta arv](../assets/resume-inheritance.png)

När du återaktiverar arv synkroniseras inte sidan automatiskt med källan. Du kan begära en synkronisering, om detta krävs, antingen:

* I dialogrutan **Återuppta**/**Återgå** , till exempel:

  ![Återuppta och synkronisera](../assets/resume-and-synch.png)

* I ett senare skede, genom att manuellt välja synkroniseringsåtgärden.

>[!NOTE]
>
>När du återaktiverar arv synkroniseras inte sidan automatiskt med källan. Om det är nödvändigt kan du begära en synkronisering manuellt, antingen när du återupptar eller senare.

#### Återuppta arv från Sidegenskaper {#resuming-inheritance-from-page-properties}

När [har pausats](#suspending-inheritance-from-page-properties) ändras åtgärden **Återuppta** i verktygsfältet för sidegenskaperna:

![Återuppta knapp](../assets/resume.png)

När du väljer det här alternativet visas dialogrutan. Om det behövs kan du välja en synkronisering och sedan bekräfta åtgärden.

#### Återuppta en Live Copy-sida från Live Copy-översikten {#resume-a-live-copy-page-from-the-live-copy-overview}

Åtgärden [Återuppta är också tillgänglig från Live-kopieringsöversikten](live-copy-overview.md#using-the-live-copy-overview) när en Live-kopia-sida är markerad.

1. Öppna [Live Copy Overview](live-copy-overview.md#using-the-live-copy-overview) och välj en pausad Live Copy-sida. Sidan visas som **ARV AVBRUTEN**.
1. Välj **Fortsätt** i verktygsfältet.
1. Ange om du vill synkronisera sidan när arvet har återställts och bekräfta sedan åtgärden **Återuppta** i dialogrutan **Återuppta Live-kopia**.

### Ändra arvsdjup (grund/djup) {#changing-inheritance-depth-shallow-deep}

I en befintlig Live-kopia kan du ändra siddjupet, det vill säga om underordnade sidor ska tas med.

* Byt till en ytlig Live Copy:

   * Kommer att ha omedelbar effekt och är icke-reversibel.

   * Frigör underordnade sidor explicit från Live Copy. Ytterligare ändringar av underordnade kan inte bevaras om de ångras.

   * Alla underordnade `LiveRelationships` tas bort, även om det finns kapslade `LiveCopies`.

* Byt till en djup Live Copy:

   * Lämnar underordnade sidor orörda.
   * Om du vill se effekten av switchen kan du göra en utrullning, så tillämpas alla innehållsändringar enligt utrullningskonfigurationen.

* Byt till en ytlig Live Copy och gå sedan tillbaka till:

   * Hanterar alla underordnade objekt i (tidigare) Grund Live Copy som om de skapats manuellt och därför flyttas bort med `[oldname]_msm_moved name`.

Så här anger eller ändrar du djup:

1. Öppna egenskaperna för Live-kopieringssidan antingen med kommandot **Visa egenskaper** i konsolen **Webbplatser** eller med **Sidinformation** i verktygsfältet för sidan.
1. Välj fliken **Live-kopia**.
1. I avsnittet **Konfiguration** anger eller avmarkerar du alternativet **Live Copy-arv** beroende på om underordnade sidor inkluderas:

   * Markerad - en djup Live-kopia (de underordnade sidorna inkluderas)
   * Avmarkerad - en tunn Live-kopia (underordnade sidor exkluderas)

   >[!CAUTION]
   >
   >Om du växlar till en ytlig Live-kopia får den omedelbar effekt och går inte att ångra.
   >
   >Mer information finns i [Live-kopior - Disposition](overview.md#live-copies-composition).

1. Välj **Spara** om du vill behålla uppdateringarna.

### Avbryta arv för en komponent {#cancelling-inheritance-for-a-component}

Avbryt Live-kopiarv för en komponent så att komponenten inte längre är synkroniserad med källkomponenten. Du kan aktivera arv vid ett senare tillfälle om det behövs.

>[!NOTE]
>
>När du återaktiverar arv synkroniseras inte komponenten automatiskt med källan. Du kan begära en synkronisering manuellt om det behövs.

Avbryt arv för att ändra komponentinnehållet eller ta bort komponenten:

1. Markera den komponent som du vill avbryta arv för.

   ![Arv i komponentverktygsfältet](../assets/inheritance-toolbar.png)

1. I komponentens verktygsfält väljer du ikonen **Avbryt arv** .

   ![Avbryta arvsikon](../assets/cancel-inheritance-icon.png)

1. Bekräfta åtgärden med **Ja** i dialogrutan Avbryt arv.

   Komponentverktygsfältet uppdateras med alla (lämpliga) redigeringskommandon.

### Återaktivera arv för en komponent {#re-enabling-inheritance-for-a-component}

Om du vill aktivera arv för en komponent väljer du ikonen **Aktivera arv igen** i komponentens verktygsfält.

![Aktivera arvsikonen igen](../assets/re-enable-inheritance-icon.png)

### Ändra ordning på komponenter på en Live Copy-sida {#changing-the-order-of-components-on-a-live-copy-page}

Om en Live-kopia innehåller komponenter som är en del av ett styckesystem, kommer arvet av det styckesystemet att följa följande regler:

* Komponenternas ordning i ett ärvt styckesystem kan ändras, även om arv är etablerat.
* Vid utrullning återställs komponenternas ordning från ritningen. Om nya komponenter lades till i Live Copy innan de lanserades, ordnas de om tillsammans med komponenterna ovanför vilka de lades till.
* Om arvet av styckesystemet avbryts återställs inte komponenternas ordning vid utrullning och förblir som i Live Copy.

>[!NOTE]
>
>När du återställer ett annullerat arv i ett styckesystem återställs inte ordningen på komponenterna **automatiskt** från ritningen. Du kan begära en synkronisering manuellt om det behövs.

Använd följande procedur för att avbryta arv av styckesystemet.

1. Öppna sidan Live Copy.
1. Dra en befintlig komponent till en ny plats på sidan.
1. Bekräfta åtgärden med **Ja** i dialogrutan **Avbryt arv**.

### Åsidosätta egenskaper för en Live Copy-sida {#overriding-properties-of-a-live-copy-page}

Sidegenskaperna för en Live-kopia-sida ärvs som standard från källsidan och kan inte redigeras.

Du kan avbryta arv av en egenskap när du behöver ändra egenskapsvärdet för Live-kopian. En länkikon anger att arv är aktiverat för egenskapen.

![Ärvda sidegenskaper](../assets/properties-inherited.png)

När du avbryter arv kan du ändra egenskapsvärdet. En ikon med en bruten länk anger att arvet har avbrutits.

![Egenskaper ärvs inte](../assets/properties-not-inherited.png)

Du kan senare återaktivera arv för en egenskap om det behövs.

>[!NOTE]
>
>När du återaktiverar arv synkroniseras inte sidegenskapen Live Copy automatiskt med källegenskapen. Du kan begära en synkronisering manuellt om det behövs.

1. Öppna egenskaperna för Live-kopieringssidan med alternativet **Visa egenskaper** i konsolen **Webbplatser** eller med ikonen **Sidinformation** i verktygsfältet för sidan.
1. Om du vill avbryta arvet av en egenskap markerar du länkikonen som visas till höger om egenskapen.

   ![Knappen Avbryt arv](../assets/cancel-inheritance-button.png)

1. I bekräftelsedialogrutan **Avbryt arv** väljer du **Ja**.

### Återställa egenskaper för en Live Copy-sida {#revert-properties-of-a-live-copy-page}

Om du vill aktivera arv för en egenskap markerar du ikonen **Återställ arv** som visas bredvid egenskapen.

![Knappen Återställ arv](../assets/revert-inheritance-button.png)

### Återställa en Live Copy-sida {#resetting-a-live-copy-page}

Du kan återställa en Live Copy-sida och göra följande:

* Ta bort alla annulleringar av arv och
* Returnera sidan till samma läge som källsidan.

Återställningen påverkar ändringar som du har gjort i sidegenskaper, styckesystem och komponenter.

#### Återställ en Live Copy-sida från Sidegenskaperna {#reset-a-live-copy-page-from-the-page-properties}

1. I konsolen **Webbplatser** markerar du sidan Live-kopia och väljer **Visa egenskaper**.
1. Öppna fliken **Live-kopia**.
1. Välj **Återställ** i verktygsfältet.

   ![Återställningsknapp](../assets/reset.png)

1. I dialogrutan **Återställ Live-kopia** bekräftar du med **Återställ**.

#### Återställ en Live Copy-sida från Live Copy-översikten {#reset-a-live-copy-page-from-the-live-copy-overview}

Åtgärden [**Återställ** är även tillgänglig från Live-kopieringsöversikt](live-copy-overview.md#using-the-live-copy-overview) när en Live-kopieringssida är markerad.

1. Öppna [Live Copy-översikten](live-copy-overview.md#using-the-live-copy-overview) och välj en Live-kopieringssida.
1. Välj **Återställ** i verktygsfältet.
1. Bekräfta åtgärden **Återställ** i dialogrutan **Återställ Live-kopia**:

   ![Bekräfta återställning av Live Copy](../assets/reset-live-copy.png)

## Jämföra en Live Copy-sida med en designsida {#comparing-a-live-copy-page-with-a-blueprint-page}

Om du vill spåra de ändringar du har gjort kan du visa planeringsidan i **Referenser** och jämföra den med Live Copy-sidan:

1. I konsolen **Webbplatser** navigerar [till en ritning eller en Live-kopia-sida och markerar den](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna panelen **[Referenser](/help/sites-cloud/authoring/basic-handling.md#references)** och välj något av följande beroende på sammanhanget:

   * **Utskrift**
   * **Live-kopior**

1. Välj en specifik Live Copy beroende på sammanhanget:

   * **Jämför med skiss**
   * **Jämför med Live-kopia**

   Till exempel:

   ![Jämför live-kopior](../assets/compare-live-copy.png)

1. Live Copy- och designsidorna öppnas sida vid sida.

   Mer information om hur du använder jämförelsefunktionen finns i [Sidskillnad](/help/sites-cloud/authoring/sites-console/page-diff.md).

## Koppla loss en Live-kopia {#detaching-a-live-copy}

Kopplingsåtgärden tar permanent bort den aktiva relationen mellan en Live-kopia och dess käll-/ritningssida. Alla MSM-relevanta egenskaper tas bort från Live Copy och Live Copy-sidorna blir en fristående kopia.

>[!CAUTION]
>
>Du kan inte återskapa direktrelationen när du har kopplat loss Live-kopian.
>
>Om du vill ta bort den aktiva relationen med alternativet att återställa den senare kan du [avbryta arv av Live-kopia](#suspending-inheritance-for-a-page) för sidan.

Det påverkar var i trädet du använder **Koppla loss**:

* **Koppla loss från en rotsida i en Live-kopia**

  När den här åtgärden utförs på rotsidan för en Live-kopia tas den aktiva relationen mellan alla sidor i planen och dess Live-kopia bort.

  Ytterligare ändringar av sidor i planen **påverkar inte** Live-kopian.

* **Koppla loss på en undersida till en Live-kopia**

  När den här åtgärden utförs på en undersida (eller en gren) i en Live-kopia:

   * Den aktiva relationen tas bort för den undersidan (eller grenen) och
   * (under)sidorna i Live Copy-grenen behandlas som om de skapats manuellt.

  Undersidorna är dock fortfarande beroende av den överordnade grenens aktiva relation, så en ytterligare utrullning av ritningssidan/-sidorna kommer att göra båda:

   1. Byt namn på den eller de frånkopplade sidorna:

      * Detta beror på att MSM betraktar dem som manuellt skapade sidor som orsakar en konflikt eftersom de har samma namn som de Live Copy-sidor som de försöker skapa.

   1. Skapa en ny Live Copy-sida med det ursprungliga namnet som innehåller ändringarna från utrullningen.

  >[!NOTE]
  >
  >Mer information om sådana situationer finns i [MSM-utrullningskonflikter](rollout-conflicts.md).

### Frigöra en Live Copy-sida från Sidegenskaper {#detach-a-live-copy-page-from-the-page-properties}

Så här frigör du en Live-kopia:

1. I konsolen **Webbplatser** markerar du sidan Live-kopia och väljer **Visa egenskaper**.
1. Öppna fliken **Live-kopia**.
1. Välj **Koppla loss** i verktygsfältet.

   ![Knappen Frigör](../assets/detach-button.png)

1. En bekräftelsedialogruta visas. Välj **Koppla loss** för att slutföra åtgärden.

### Frigöra en Live Copy-sida från Live Copy-översikten {#detach-a-live-copy-page-from-the-live-copy-overview}

Åtgärden [Koppla loss är även tillgänglig från Live-kopieringsöversikten](live-copy-overview.md#using-the-live-copy-overview) när en Live-kopieringssida är markerad.

1. Öppna [Live Copy-översikten](live-copy-overview.md#using-the-live-copy-overview) och välj en Live-kopieringssida.
1. Välj **Koppla loss** från verktygsfältet.
1. Bekräfta åtgärden **Koppla loss** i dialogrutan **Koppla loss Live-kopia**:

   ![Kopplar loss en Live-kopia](../assets/detach-live-copy.png)
