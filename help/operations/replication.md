---
title: Replikering
description: Distribution och felsökning av replikering.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 405922266ed15c2db135921132c89fa459b38d1b
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---

# Replikering {#replication}

Adobe Experience Manager som Cloud Service använder funktionen [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) för att flytta innehållet som ska replikeras till en pipeline-tjänst som körs på Adobe I/O som ligger utanför AEM.

>[!NOTE]
>
>Läs [Distribution](/help/core-concepts/architecture.md#content-distribution) om du vill ha mer information.

## Metoder för publicering av innehåll {#methods-of-publishing-content}

### Snabb borttagning/publicering - planerad avstängning/publicering {#publish-unpublish}

På så sätt kan du publicera de markerade sidorna direkt, utan de ytterligare alternativ som är möjliga via Hantera publikation.

Mer information finns i [Hantera publikation](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### På- och avaktiveringstider - utlösarkonfiguration {#on-and-off-times-trigger-configuration}

De ytterligare möjligheterna i **On Time** och **Off Time** är tillgängliga på fliken [Basic (Grundläggande) i Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Om du vill genomföra den automatiska replikeringen för detta måste du aktivera **Automatisk replikering** i [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md) **Utlösarkonfiguration vid fel**:

![Konfiguration av OSGi på av utlösare](/help/operations/assets/replication-on-off-trigger.png)

### Aktivering av träd {#tree-activation}

Så här utför du en trädaktivering:

1. Navigera från AEM Start-meny till **Verktyg > Distribution > Distribution**
2. Välj kortet **forwardPublisher**
3. **Välj Distribute** i webbkonsolens användargränssnitt för forwardPublisher

   ![](assets/distribute.png "DistribueraDistribuera")
4. Markera sökvägen i sökvägsläsaren, välj att lägga till en nod, ett träd eller att ta bort efter behov och välj **Skicka**

### Publicera arbetsflöde för innehållsträd {#publish-content-tree-workflow}

Du kan utlösa en trädreplikering genom att välja **Verktyg - Arbetsflöde - Modeller** och kopiera **publiceringsinnehållsträdet** som är körklar, vilket visas nedan:

![](/help/operations/assets/publishcontenttreeworkflow.png)

Ändra inte och anropa inte den ursprungliga modellen. I stället måste du först kopiera modellen och sedan ändra eller anropa kopian.

Precis som för alla arbetsflöden kan den också anropas via API. Mer information finns i [Interagera med arbetsflöden programmatiskt](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

Du kan också uppnå detta genom att skapa en arbetsflödesmodell som använder steget `Publish Content Tree`:

1. Gå till **Verktyg - Arbetsflöde - Modeller** från AEM som Cloud Service.
1. På sidan Arbetsflödesmodeller trycker du på **Create** i skärmens övre högra hörn
1. Lägg till en titel och ett namn i modellen. Mer information finns i [Skapa arbetsflödesmodeller](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. Markera den nyskapade modellen i listan och tryck på **Redigera**
1. I följande fönster drar och släpper du Processsteg till det aktuella modellflödet:

   ![Processsteg](/help/operations/assets/processstep.png)

1. Klicka på steget Process i flödet och välj **Konfigurera** genom att trycka på växlingsikonen
1. Klicka på fliken **Process** och välj `Publish Content Tree` i listrutan.

   ![Reaktivering](/help/operations/assets/newstep.png)

1. Ange eventuella ytterligare parametrar i fältet **Arguments**. Flera kommaavgränsade argument kan vara sammanfogade. Till exempel:

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >En lista över parametrar finns i avsnittet **Parametrar** nedan.

1. Tryck på **Klart** för att spara arbetsflödesmodellen.

**Parametrar**

* `replicateAsParticipant` (booleskt värde, standard:  `false`). Om den är konfigurerad som `true` använder replikeringen `userid` för det huvud som utförde deltagarsteget.
* `enableVersion` (booleskt värde, standard:  `true`). Den här parametern avgör om en ny version skapas vid replikering.
* `agentId` (strängvärde, standard betyder att endast agenter för publicering används). Vi rekommenderar att du uttryckligen anger agentId; Om du till exempel anger värdet: publicera. Om agenten anges till `preview` publiceras den till förhandsgranskningstjänsten
* `filters` (strängvärde, standard innebär att alla sökvägar aktiveras). Tillgängliga värden är:
   * `onlyActivated` - bara sökvägar som inte är markerade som aktiverade aktiveras.
   * `onlyModified` - aktivera endast sökvägar som redan är aktiverade och som har ett ändringsdatum efter aktiveringsdatumet.
   * Ovanstående kan vara ORed med vertikalstreck (|). Till exempel, `onlyActivated|onlyModified`.

**Loggning**

När arbetsflödessteget för trädaktivering startar loggas konfigurationsparametrarna på INFO-loggnivån. När sökvägar aktiveras loggas även en INFO-sats.

En slutgiltig INFO-sats loggas sedan när arbetsflödessteget har replikerat alla sökvägar.

Dessutom kan du öka loggningsnivån för loggarna under `com.day.cq.wcm.workflow.process.impl` till DEBUG/TRACE för att få ännu mer logginformation.

Om fel uppstår avslutas arbetsflödessteget med ett `WorkflowException`, som omsluter det underliggande undantaget.

Här nedan hittar du exempel på loggar som genereras under ett arbetsflöde för publiceringsinnehåll:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Återuppta support**

Arbetsflödet bearbetar innehåll i segment, som representerar en delmängd av det fullständiga innehåll som ska publiceras. Om arbetsflödet stoppas av systemet kommer det att starta om och bearbeta segmentet som ännu inte bearbetats. En loggsats anger att innehållet har återupptagits från en viss sökväg.

### Replikerings-API {#replication-api}

Du kan publicera innehåll med replikerings-API:t som finns i AEM som en Cloud Service.

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

När resurser replikeras som i exemplet ovan kommer endast de agenter som är aktiva som standard att användas. I AEM som Cloud Service är detta bara agenten som kallas&quot;publicera&quot;, som kopplar författaren till publiceringsnivån.

En ny agent med namnet&quot;preview&quot; har lagts till som stöd för förhandsvisningsfunktionen, som inte är aktiv som standard. Den här agenten används för att ansluta författaren till förhandsgranskningsnivån. Om du bara vill replikera via förhandsgranskningsagenten måste du uttryckligen välja den här förhandsgranskningsagenten via en `AgentFilter`.

Se exemplet nedan om hur du gör detta:

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

Den övergripande `ReplicationStatus` för en resurs ändras bara om replikeringsåtgärden innehåller minst en agent som är aktiv som standard. I exemplet ovan är detta inte fallet eftersom replikeringen bara använder agenten för förhandsgranskning. Du måste därför använda den nya metoden `getStatusForAgent()` som gör att du kan fråga efter status för en viss agent. Den här metoden fungerar även för agenten&quot;publish&quot;. Det returnerar ett värde som inte är null om någon replikeringsåtgärd har utförts med den angivna agenten.

### Hantera publikation {#manage-publication}

Med Hantera publikation får du fler alternativ än Snabbpublicering, så att du kan inkludera underordnade sidor, anpassa referenserna och starta tillämpliga arbetsflöden samt erbjuda möjlighet att publicera vid ett senare tillfälle.

Om du tar med en mapps underordnade objekt för alternativet Publicera senare, aktiveras arbetsflödet Publicera innehållsträd, som beskrivs i den här artikeln.

Mer detaljerad information om Hantera publikation finns i [Publishing Fundamentals documentation](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

## Felsökning {#troubleshooting}

Om du vill felsöka replikering går du till replikeringsköerna i webbgränssnittet för AEM Author Service:

1. Navigera från AEM Start-meny till **Verktyg > Distribution > Distribution**
2. Välj kortet **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Kontrollera köstatusen som ska vara grön
4. Du kan testa anslutningen till replikeringstjänsten
5. Välj fliken **Loggar** som visar historiken för innehållspublikationer

![](assets/logs.png "LogsLogs")

Om innehållet inte kunde publiceras återställs hela publikationen från AEM Publish Service.
I så fall bör köerna ses över för att identifiera vilka objekt som orsakade att offentliggörandet avbröts. Om du klickar på en kö med röd status visas kön med väntande objekt, från vilken enskilda eller alla objekt kan rensas vid behov.
