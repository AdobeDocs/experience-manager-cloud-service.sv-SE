---
title: Replikering
description: Läs om distribution och felsökning av replikering i AEM as a Cloud Service.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: 1179e45f6e75a8a4f5e5e76903243f64d9f406ae
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---

# Replikering {#replication}

Adobe Experience Manager as a Cloud Service använder funktionen [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) för att flytta innehållet som ska replikeras till en pipeline-tjänst som körs på Adobe Developer utanför AEM-miljön.

>[!NOTE]
>
>Läs [Distribution](/help/overview/architecture.md#content-distribution) om du vill ha mer information.

## Metoder för publicering av innehåll {#methods-of-publishing-content}

>[!NOTE]
>
>Om du är intresserad av att publicera satsvis kan du skapa ett arbetsflöde med [Arbetsflödessteget för trädaktivering](#tree-activation) som effektivt kan hantera stora nyttolaster.
>&#x200B;>Vi rekommenderar inte att du skapar en egen anpassad masspubliceringskod.
>&#x200B;>Om du måste anpassa av någon anledning kan du utlösa ett arbetsflöde med det här steget genom att använda befintliga arbetsflödes-API:er.
>&#x200B;>Det är alltid en god vana att bara publicera innehåll som måste publiceras. Och var försiktig med att inte försöka publicera stora mängder innehåll, om det inte är nödvändigt. Det finns dock inga gränser för hur mycket innehåll du kan skicka via arbetsflöden med arbetsflödessteget Trädaktivering.

### Snabb borttagning/publicering - planerad avstängning/publicering {#publish-unpublish}

Med den här funktionen kan du publicera de valda sidorna direkt, utan de ytterligare alternativ som är möjliga via Hantera publikation.

Mer information finns i [Hantera publikation](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### På- och avaktiveringstider - utlösarkonfiguration {#on-and-off-times-trigger-configuration}

De ytterligare möjligheterna för **På tid** och **Fråntid** finns på fliken [Grundläggande i Sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md#basic).

Aktivera **Automatisk replikering** i [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md) **Vid utlösarkonfiguration** om du vill genomföra den automatiska replikeringen för den här funktionen:

![OSGi på av utlösarkonfiguration](/help/operations/assets/replication-on-off-trigger.png)

### Hantera publikation {#manage-publication}

Med Hantera publikation får du fler alternativ än Snabbpublicering, så att du kan inkludera underordnade sidor, anpassa referenserna och starta tillämpliga arbetsflöden och erbjuda möjlighet att publicera senare.

Om du tar med en mapps underordnade objekt för alternativet Publicera senare, anropas arbetsflödet Publicera innehållsträd, som beskrivs i den här artikeln.

Mer detaljerad information om Hantera publikation finns i [Dokumentationen om grunderna för publicering](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Arbetsflödessteg för trädaktivering {#tree-activation}

Arbetsflödessteget Trädaktivering är avsett att effektivt återge en djup hierarki av innehållsnoder. Den pausas automatiskt när kön växer för stor så att andra replikeringar kan fortsätta parallellt med minimal fördröjning.

Skapa en arbetsflödesmodell som använder processsteget `TreeActivation`:

1. Gå till **Verktyg - Arbetsflöde - Modeller** från AEM as a Cloud Service hemsida.
1. På sidan Arbetsflödesmodeller trycker du på **Create** i skärmens övre högra hörn.
1. Lägg till en titel och ett namn i modellen. Mer information finns i [Skapa arbetsflödesmodeller](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE).
1. Markera den skapade modellen i listan och tryck på **Redigera**
1. I följande fönster tar du bort steget som visas som standard
1. Dra och släpp Processsteget till det aktuella modellflödet:

   ![Processsteg](/help/operations/assets/processstep.png)

1. Välj processsteget i flödet och välj **Konfigurera** genom att trycka på skiftnyckelsikonen.
1. Markera fliken **Process** och välj `Publish Content Tree` i listrutan. Markera sedan kryssrutan **Avancerat för hanterare**

   ![Treeactivation](/help/operations/assets/new-treeactivationstep.png)

1. Ange eventuella ytterligare parametrar i fältet **Arguments**. Flera kommaavgränsade argument kan sammanfogas. Till exempel:

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >En lista med parametrar finns i avsnittet **Parametrar** nedan.

1. Tryck på **Klar** för att spara arbetsflödesmodellen.

**Parametrar**

| Namn | standard | description |
| -------------- | ------- | --------------------------------------------------------------- |
| bana |         | rotsökväg att börja från |
| agentId | publicera | Replikeringsagentens namn som ska användas |
| chunkSize | 50 | Antal sökvägar att paketera i en enda replikering |
| maxTreeSize | 500000 | Maximalt antal noder för ett träd som ska betraktas som litet |
| maxQueueSize | 10 | Maximalt antal objekt i replikeringskön |
| enableVersion | false | Aktivera versionshantering |
| dryRun | false | Om värdet är true anropas inte replikeringen |
| userId |         | bara för jobb. I arbetsflödet används användaren som anropar arbetsflödet |
| filter |         | Lista med nodfilternamn. Se filter som stöds nedan |

**Supportfilter**

| Namn | Beskrivning |
| ------------- | ------------------------------------------- |
| onlyModified | Noder: både nya och befintliga som har ändrats sedan den senaste publiceringen |
| onlyActivated | Noder: som har publicerats före den senaste publiceringen |


**Återuppta support**

Arbetsflödet bearbetar innehåll i segment, som representerar en delmängd av det fullständiga innehåll som ska publiceras.  Om arbetsflödet stoppas av systemet fortsätter det där det slutade.

**Övervaka arbetsflödets förlopp**

1. Gå till **Verktyg - Allmänt - Jobb** på AEM as a Cloud Service hemsida.
1. Titta på raden som motsvarar ditt arbetsflöde. Kolumnen *progress* ger en indikation på hur replikeringen fortskrider. Den kan till exempel visa 41/564 och vid uppdatering kan den uppdateras till 52/564.

   ![Behandlingsaktiveringsförlopp](/help/operations/assets/treeactivation-progress.png)


1. Om du markerar raden och öppnar den visas ytterligare information om arbetsflödets körningsstatus.

   ![Statusinformation för återaktivering](/help/operations/assets/treeactivation-progress-details.png)



### Publicera arbetsflöde för innehållsträd {#publish-content-tree-workflow}

>[!NOTE]
>
>Den här funktionen är ersatt med ett mer prestandaförbättrat trädaktiveringssteg, som kan inkluderas i ett anpassat arbetsflöde.

<details>
<summary>Klicka här om du vill veta mer om den här borttagna funktionen.</summary>

Du kan utlösa en trädreplikering genom att välja **Verktyg - Arbetsflöde - Modeller** och kopiera arbetsflödesmodellen **Publicera innehållsträd** som är körklar, vilket visas nedan:

![Arbetsflödeskortet för publiceringsinnehållsträdet](/help/operations/assets/publishcontenttreeworkflow.png)

Anropa inte den ursprungliga modellen. Kontrollera i stället att först kopiera modellen och anropa kopian.

Precis som med alla arbetsflöden kan den också anropas via API. Mer information finns i [Interagera med arbetsflöden programmatiskt](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=sv-SE#extending-aem).

Du kan också skapa en arbetsflödesmodell som använder processsteget `Publish Content Tree`.

1. Gå till **Verktyg - Arbetsflöde - Modeller** från AEM as a Cloud Service hemsida.
1. På sidan Arbetsflödesmodeller trycker du på **Create** i skärmens övre högra hörn.
1. Lägg till en titel och ett namn i modellen. Mer information finns i [Skapa arbetsflödesmodeller](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE).
1. Markera den skapade modellen i listan och tryck på **Redigera**
1. I följande fönster drar och släpper du Processsteg till det aktuella modellflödet:

   ![Processsteg](/help/operations/assets/processstep.png)

1. Välj processsteget i flödet och välj **Konfigurera** genom att trycka på skiftnyckelsikonen.
1. Markera fliken **Process** och välj `Publish Content Tree` i listrutan. Markera sedan kryssrutan **Avancerat för hanterare**

   ![Treeactivation](/help/operations/assets/newstep.png)

1. Ange eventuella ytterligare parametrar i fältet **Arguments**. Flera kommaavgränsade argument kan sammanfogas. Till exempel:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >En lista med parametrar finns i avsnittet **Parametrar** nedan.

1. Tryck på **Klar** för att spara arbetsflödesmodellen.

**Parametrar**

* `includeChildren` (booleskt värde, standard: `false`). Värdet `false` betyder att bara sökvägen publiceras. `true` betyder att även underordnade objekt publiceras.
* `replicateAsParticipant` (booleskt värde, standard: `false`). Om den är konfigurerad som `true` använder replikeringen `userid` för det huvud som utförde deltagarsteget.
* `enableVersion` (booleskt värde, standard: `false`). Den här parametern avgör om en ny version skapas vid replikering.
* `agentId` (strängvärde, standard innebär att endast agenter för publicering används). Vi rekommenderar att du anger agentens ID explicit, till exempel anger värdet: publish. Agenten anges till `preview` publicerar till förhandsgranskningstjänsten.
* `filters` (strängvärde, standard betyder att alla sökvägar aktiveras). Tillgängliga värden är:
   * `onlyActivated` - aktivera endast sidor som (redan) har aktiverats. Fungerar som en form av omaktivering.
   * `onlyModified` - aktivera endast sökvägar som redan är aktiverade och har ett ändringsdatum som är senare än aktiveringsdatumet.
   * Ovanstående kan vara ORed med vertikalstreck (|). Exempel: `onlyActivated|onlyModified`.

**Loggar**

När arbetsflödessteget för trädaktivering startar loggas dess konfigurationsparametrar på INFO-loggnivån. När sökvägar aktiveras loggas även en INFO-sats.

En slutgiltig INFO-sats loggas när arbetsflödessteget har replikerat alla sökvägar.

Du kan också öka loggningsnivån för loggarna under `com.day.cq.wcm.workflow.process.impl` till DEBUG/TRACE för att få ännu mer logginformation.

Om det finns fel avslutas arbetsflödessteget med `WorkflowException`, som omsluter det underliggande undantaget.

Här följer exempel på loggar som genereras under ett exempel på arbetsflöde för publiceringsinnehåll:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

</details>

### Replikerings-API {#replication-api}

Du kan publicera innehåll med det replikerings-API som finns i AEM as a Cloud Service.

Mer information finns i [API-dokumentationen](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

**Grundläggande användning av API**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**Replikering med specifika agenter**

Vid replikering av resurser, som i exemplet ovan, används bara de agenter som är aktiva som standard. I AEM as a Cloud Service betyder det bara agenten&quot;publish&quot;, som kopplar författaren till publiceringsnivån.

En ny agent med namnet&quot;preview&quot; har lagts till som stöd för förhandsvisningsfunktionen, som inte är aktiv som standard. Den här agenten används för att ansluta författaren till förhandsgranskningsnivån. Om du bara vill replikera via förhandsgranskningsagenten måste du uttryckligen välja den här förhandsgranskningsagenten med hjälp av en `AgentFilter`.

Se följande exempel:

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

Om du inte anger ett sådant filter och bara använder agenten för publicering, används inte agenten för förhandsgranskning och replikeringsåtgärden påverkar inte förhandsgranskningsnivån.

Den övergripande `ReplicationStatus` för en resurs ändras bara om replikeringsåtgärden innehåller minst en agent som är aktiv som standard. I exemplet ovan var detta inte fallet. Replikeringen använde just agenten för förhandsgranskning. Du måste därför använda den nya metoden `getStatusForAgent()` som tillåter att du frågar efter status för en viss agent. Den här metoden fungerar även för agenten&quot;publish&quot;. Det returnerar ett värde som inte är null om någon replikeringsåtgärd har utförts med den angivna agenten.

### Metoder för att verifiera innehåll {#invalidating-content}

Du kan göra innehåll ogiltigt direkt genom att antingen använda Sling Content Invalidation (SCD) från författaren (den önskade metoden) eller genom att använda replikerings-API:t för att anropa den publicerade Dispatcher flush-replikeringsagenten. Mer information finns på sidan [Caching](/help/implementing/dispatcher/caching.md).

**Kapacitetsbegränsningar för replikerings-API**

Replikera färre än 100 banor i taget, med 500 som gräns. Ovanför gränsen genereras en `ReplicationException`.
Om programlogiken inte kräver atomisk replikering kan den här gränsen överskridas genom att `ReplicationOptions.setUseAtomicCalls` anges till false, vilket tar ett valfritt antal sökvägar, men internt skapar bucklor som ligger under den här gränsen.

Storleken på innehållet som skickas per replikeringsanrop får inte överstiga `10 MB`. Den här regeln omfattar noder och egenskaper, men inte binärfiler (arbetsflödespaket och innehållspaket betraktas som binärfiler).


## Felsökning {#troubleshooting}

Om du vill felsöka replikering går du till Replikeringsköer i webbgränssnittet för AEM Author Service:

1. Navigera från AEM [Global Navigation](/help/sites-cloud/authoring/basic-handling.md#global-navigation) till **Verktyg** > **Distribution** > **Distribution**
1. Välj kortet **publicera**

   ![Status](assets/publish-status.png "Status")

1. Kontrollera köstatusen som ska vara grön
1. Du kan testa anslutningen till replikeringstjänsten
1. Välj fliken **Loggar** som visar historiken för innehållspublikationer

![Loggar](assets/publish-logs.png "Loggar")

Om innehållet inte kunde publiceras återställs hela publikationen från AEM Publish Service.

I så fall visar den huvudsakliga, redigerbara kön en röd status och bör granskas för att identifiera vilka objekt som gjorde att publiceringen avbröts. Genom att klicka på den kön visas de väntande objekten, från vilka ett eller alla objekt kan rensas vid behov.
