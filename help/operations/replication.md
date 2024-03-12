---
title: Replikering
description: Lär dig mer om distribution och felsökning av replikering på AEM as a Cloud Service.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# Replikering {#replication}

Adobe Experience Manager as a Cloud Service använder [Distribution av säljinnehåll](https://sling.apache.org/documentation/bundles/content-distribution.html) möjlighet att flytta det innehåll som ska replikeras till en pipeline-tjänst som körs på Adobe Developer och som ligger utanför AEM.

>[!NOTE]
>
>Läs [Distribution](/help/overview/architecture.md#content-distribution) för mer information.

## Metoder för publicering av innehåll {#methods-of-publishing-content}

>[!NOTE]
>
>Om du är intresserad av bulkpublicering kan du använda [Publicera arbetsflöde för innehållsträd](#publish-content-tree-workflow).
>Det här arbetsflödessteget är särskilt utformat för Cloud Service och kan effektivt hantera stora nyttolaster.
>Vi rekommenderar inte att du skapar en egen anpassad masspubliceringskod.
>Om du måste anpassa av någon anledning kan du utlösa det här arbetsflödes-/arbetsflödessteget genom att använda befintliga arbetsflödes-API:er.
>Det är alltid en god vana att bara publicera innehåll som måste publiceras. Och var försiktig med att inte försöka publicera stora mängder innehåll, om det inte är nödvändigt. Det finns dock inga gränser för hur mycket innehåll du kan skicka via arbetsflödet Publicera innehållsträd.

### Snabb borttagning/publicering - planerad avstängning/publicering {#publish-unpublish}

Med den här funktionen kan du publicera de valda sidorna direkt, utan de ytterligare alternativ som är möjliga via Hantera publikation.

Mer information finns i [Hantera publikation](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### På- och avaktiveringstider - utlösarkonfiguration {#on-and-off-times-trigger-configuration}

Ytterligare möjligheter för **I tid** och **Fråntid** är tillgängliga från [Fliken Grundläggande i Sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md#basic).

Aktivera om du vill genomföra den automatiska replikeringen för den här funktionen **Automatisk replikering** i [OSGi-konfiguration](/help/implementing/deploying/configuring-osgi.md) **Konfiguration av utlösare vid avstängning**:

![Konfiguration av OSGi på av utlösare](/help/operations/assets/replication-on-off-trigger.png)

### Hantera publikation {#manage-publication}

Med Hantera publikation får du fler alternativ än Snabbpublicering, så att du kan inkludera underordnade sidor, anpassa referenserna och starta tillämpliga arbetsflöden och erbjuda möjlighet att publicera senare.

Om du tar med en mapps underordnade objekt för alternativet Publicera senare, anropas arbetsflödet Publicera innehållsträd, som beskrivs i den här artikeln.

Mer information om Hantera publikation finns i [Dokumentation för Publishing Fundamentals](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Publicera arbetsflöde för innehållsträd {#publish-content-tree-workflow}

Du kan aktivera en trädreplikering genom att välja **Verktyg - Arbetsflöde - Modeller** och kopiera **Publicera innehållsträd** körklar arbetsflödesmodell, enligt nedan:

![Arbetsflödeskortet för publiceringsinnehållsträdet](/help/operations/assets/publishcontenttreeworkflow.png)

Anropa inte den ursprungliga modellen. Kontrollera i stället att först kopiera modellen och anropa kopian.

Precis som med alla arbetsflöden kan den också anropas via API. Mer information finns i [Interagera med arbetsflöden programmatiskt](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html#extending-aem).

Du kan också skapa en arbetsflödesmodell som använder `Publish Content Tree` processteg:

1. Från den AEM as a Cloud Service hemsidan går du till **Verktyg - Arbetsflöde - Modeller**.
1. Tryck på **Skapa** i skärmens övre högra hörn.
1. Lägg till en titel och ett namn i modellen. Mer information finns i [Skapa arbetsflödesmodeller](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html).
1. Markera den skapade modellen i listan och tryck på **Redigera**
1. I följande fönster drar och släpper du Processsteg till det aktuella modellflödet:

   ![Processsteg](/help/operations/assets/processstep.png)

1. Markera processteget i flödet och välj **Konfigurera** genom att trycka på skiftnyckelsikonen.
1. Välj **Process** och markera `Publish Content Tree` i listrutan och markera sedan **Avancerad hanterare** kryssruta

   ![Reaktivering](/help/operations/assets/newstep.png)

1. Ange eventuella ytterligare parametrar i dialogrutan **Argument** fält. Flera kommaavgränsade argument kan sammanfogas. Till exempel:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >En lista med parametrar finns i **Parametrar** nedan.

1. Tryck **Klar** för att spara arbetsflödesmodellen.

**Parametrar**

* `includeChildren` (booleskt värde, standard: `false`). Värdet `false` innebär att det endast är banan som offentliggörs, `true` innebär att även barn publiceras.
* `replicateAsParticipant` (booleskt värde, standard: `false`). Om konfigurerad som `true`används `userid` av huvudmannen som utförde deltagarsteget.
* `enableVersion` (booleskt värde, standard: `false`). Den här parametern avgör om en ny version skapas vid replikering.
* `agentId` (strängvärde, standard betyder att endast agenter för publicering används). Vi rekommenderar att du anger agentens ID explicit, till exempel anger värdet: publish. Ange att agenten ska `preview` publicerar till förhandsgranskningstjänsten.
* `filters` (strängvärde, standard betyder att alla sökvägar aktiveras). Tillgängliga värden är:
   * `onlyActivated` - aktivera endast sidor som har (redan) aktiverats. Fungerar som en form av omaktivering.
   * `onlyModified` - aktivera endast sökvägar som redan är aktiverade och som har ett ändringsdatum efter aktiveringsdatumet.
   * Ovanstående kan vara ORed med vertikalstreck (|). Till exempel: `onlyActivated|onlyModified`.

**Loggning**

När arbetsflödessteget för trädaktivering startar loggas dess konfigurationsparametrar på INFO-loggnivån. När sökvägar aktiveras loggas även en INFO-sats.

En slutgiltig INFO-sats loggas när arbetsflödessteget har replikerat alla sökvägar.

Du kan även öka loggningsnivån nedan `com.day.cq.wcm.workflow.process.impl` till DEBUG/TRACE för att få ännu mer logginformation.

Om det finns fel avslutas arbetsflödessteget med ett `WorkflowException`, som omsluter det underliggande undantaget.

Här följer exempel på loggar som genereras under ett exempel på arbetsflöde för publiceringsinnehåll:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Återuppta support**

Arbetsflödet bearbetar innehåll i segment, som representerar en delmängd av det fullständiga innehåll som ska publiceras. Om arbetsflödet stoppas av systemet startas det om och bearbetar det segment som ännu inte bearbetats. En loggsats anger att innehållet återupptogs från en viss sökväg.

### Replikerings-API {#replication-api}

Du kan publicera innehåll med hjälp av replikerings-API:t på AEM as a Cloud Service.

Mer information finns i [API-dokumentation](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

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

Vid replikering av resurser, som i exemplet ovan, används bara de agenter som är aktiva som standard. På AEM as a Cloud Service betyder det bara agenten&quot;publish&quot;, som kopplar författaren till publiceringsnivån.

En ny agent med namnet&quot;preview&quot; har lagts till som stöd för förhandsvisningsfunktionen, som inte är aktiv som standard. Den här agenten används för att ansluta författaren till förhandsgranskningsnivån. Om du bara vill replikera via förhandsgranskningsagenten måste du uttryckligen välja den här förhandsgranskningsagenten via en `AgentFilter`.

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

Det övergripande `ReplicationStatus` för en resurs ändras bara om replikeringsåtgärden innehåller minst en agent som är aktiv som standard. I exemplet ovan var detta inte fallet. Replikeringen använde just agenten för förhandsgranskning. Därför måste du använda den nya `getStatusForAgent()` -metod, som tillåter frågor om status för en viss agent. Den här metoden fungerar även för agenten&quot;publish&quot;. Det returnerar ett värde som inte är null om någon replikeringsåtgärd har utförts med den angivna agenten.

### Metoder för att verifiera innehåll {#invalidating-content}

Du kan göra innehåll ogiltigt direkt genom att antingen använda Sling Content Invalidation (SCD) från författaren (den föredragna metoden) eller genom att använda replikerings-API:t för att anropa replikeringsagenten för publiceringsrensningen för Dispatcher. Se [Cachning](/help/implementing/dispatcher/caching.md) sida för mer information.

**Kapacitetsbegränsningar för replikerings-API**

Replikera färre än 100 banor i taget, med 500 som gräns. Ovanför gränsen är `ReplicationException` kastas.
Om programlogiken inte kräver atomisk replikering kan den här gränsen överskridas genom att du ställer in `ReplicationOptions.setUseAtomicCalls` till false, vilket accepterar valfritt antal banor, men internt skapar buketter som ligger under denna gräns.

Storleken på innehållet som skickas per replikeringsanrop får inte överskrida `10 MB`. Den här regeln omfattar noder och egenskaper, men inte binärfiler (arbetsflödespaket och innehållspaket betraktas som binärfiler).


## Felsökning {#troubleshooting}

Om du vill felsöka replikering går du till replikeringsköerna i webbgränssnittet för AEM författartjänst:

1. Navigera AEM Start-menyn till **Verktyg > Distribution > Distribution**
2. Välj kort **publicera**
   ![Status](assets/publish-status.png "Status")
3. Kontrollera köstatusen som ska vara grön
4. Du kan testa anslutningen till replikeringstjänsten
5. Välj **Loggar** som visar historiken för innehållspublikationer

![Loggar](assets/publish-logs.png "Loggar")

Om innehållet inte kunde publiceras återställs hela publikationen från AEM Publiceringstjänst.
I så fall visar den huvudsakliga, redigerbara kön en röd status och bör granskas för att identifiera vilka objekt som gjorde att publiceringen avbröts. Genom att klicka på den kön visas de väntande objekten, från vilka ett eller alla objekt kan rensas vid behov.
