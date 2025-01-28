---
title: Underhållsaktiviteter i AEM as a Cloud Service
description: Lär dig mer om underhållsåtgärder i AEM as a Cloud Service och hur du konfigurerar dem.
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: 3692cf1b14fda80f35eb34583fbbf6b256a89917
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 0%

---


# Underhållsaktiviteter i AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Underhållsaktiviteter"
>abstract="Underhållsåtgärder är processer som körs enligt ett schema för att optimera databasen. Med AEM as a Cloud Service är behovet av att kunderna konfigurerar driftsegenskaperna för underhållsåtgärder minimal. Kunderna kan fokusera sina resurser på frågor som rör applikationsnivå och lämna infrastrukturåtgärderna åt Adobe."

Underhållsåtgärder är processer som körs enligt ett schema för att optimera databasen. Med AEM as a Cloud Service är behovet av att kunderna konfigurerar driftsegenskaperna för underhållsåtgärder minimal. Kunderna kan fokusera sina resurser på frågor som rör applikationsnivå och lämna infrastrukturåtgärderna åt Adobe.

## Konfigurera underhållsåtgärder {#maintenance-tasks-configuring}

I tidigare versioner av AEM kunde du konfigurera underhållsåtgärder med underhållskortet (Verktyg > Åtgärder > Underhåll). Underhållskortet för AEM as a Cloud Service är inte längre tillgängligt, så konfigurationer bör implementeras för källkontroll och driftsättas med Cloud Manager. Adobe hanterar de underhållsåtgärder som har inställningar som inte kan konfigureras av kunder (till exempel Datastore Garbage Collection). Andra underhållsuppgifter kan konfigureras av kunder, vilket beskrivs i tabellen nedan.

>[!CAUTION]
>
>Adobe förbehåller sig rätten att åsidosätta en kunds konfigurationsinställningar för underhållsaktiviteter för att minska problem som prestandaförsämringar.

Följande tabell visar vilka underhållsuppgifter som är tillgängliga.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Underhållsaktivitet</th>
    <th>Vem äger konfigurationen</th>
    <th>Konfigurera (valfritt)</th>
  </tr>  
  <tr>
    <td>Skräpsamling för datastaarkiv</td>
    <td>Adobe</td>
    <td>Ej tillämpligt - ägs till fullo av Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Rensa version</td>
    <td>Kund</td>
    <td>Borttagning av version är för närvarande inaktiverat som standard, men principen kan konfigureras enligt beskrivningen i avsnittet <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Rensa och Rensa granskningslogg </a>.<br/><br/>Rensning kommer snart att vara aktiverat som standard, med dessa värden åsidosatta.<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>Rensa granskningslogg</td>
    <td>Kund</td>
    <td>Rensa granskningslogg är för närvarande inaktiverat som standard, men principen kan konfigureras enligt beskrivningen i avsnittet <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Rensa version och Rensa granskningslogg - underhållsaktiviteter</a>.<br/><br/>Rensning kommer snart att vara aktiverat som standard, med dessa värden åsidosatta.<br>
   </td>
   </td>
  </tr>
  <tr>
    <td>Lucene Binaries Cleanup</td>
    <td>Adobe</td>
    <td>Oanvänd och därför inaktiverad av Adobe.</td>
  </td>
  </tr>
  <tr>
    <td>Ad hoc-aktivitetsrensning</td>
    <td>Kund</td>
    <td>
    <p>Måste göras i git. Åsidosätt den körklara konfigurationsnoden för underhållsfönstret under <code>/libs</code> genom att skapa egenskaper under mappen <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> eller <code>granite_monthly</code>.</p>
    <p>Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation. Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan. Ge den namnet <code>granite_TaskPurgeTask</code>, med attributet <code>sling:resourceType</code> inställt på <code>granite/operations/components/maintenance/task</code> och attributet <code>granite.maintenance.name</code> inställt på <code>TaskPurge</code>. Konfigurera OSGI-egenskaperna, se <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> för en lista över egenskaper.</p>
  </td>
  </tr>
    <tr>
    <td>Rensa arbetsflöde</td>
    <td>Kund</td>
    <td>
    <p>Måste göras i git. Åsidosätt den körklara konfigurationsnoden för underhållsfönstret under <code>/libs</code> genom att skapa egenskaper under mappen <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> eller <code>granite_monthly</code>. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation.</p>
    <p>Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den <code>granite_WorkflowPurgeTask</code>) med lämpliga egenskaper. Konfigurera OSGI-egenskaperna i <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances">AEM 6.5-underhållsaktivitetens dokumentation</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Rensa projekt</td>
    <td>Kund</td>
    <td>
    <p>Måste göras i git. Åsidosätt den körklara konfigurationsnoden för underhållsfönstret under <code>/libs</code> genom att skapa egenskaper under mappen <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> eller <code>granite_monthly</code>. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation.</p>
    <p>Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den <code>granite_ProjectPurgeTask</code>) med lämpliga egenskaper. Se listan över <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi">OSGi-egenskaper</a> för <b>Adobe Projects Renge Configuration</b> .</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Konfiguration av underhållsfönster</th>
    <th>Vem äger konfigurationen</th>
    <th>Konfigurationstyp</th>
    <th>Parametrar</th>
  </tr>
  <tr>
    <td>Dagligen</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
  <td>
  <p><strong>windowSchedule=day</strong> (det här värdet ska inte ändras)</p>
  <p><strong>windowStartTime=HH:MM</strong> använder som 24-timmars klocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska börja köras.</p>
  <p><strong>windowEndTime=HH:MM</strong> använder som 24-timmars klocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska sluta köras om de inte redan har slutförts.</p>
  <p>En underhållsaktivitet kan inte utföras mer än en gång under den här tidsramen.</p>
  </td> 
  </tr>
  <tr>
    <td>Vecka</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>
    <p><strong>windowSchedule=week</strong> (det här värdet ska inte ändras)</p>
    <p><strong>windowStartTime=HH:MM</strong> använder som 24-timmars klocka. Definierar när underhållsaktiviteterna som är kopplade till veckounderhållet ska börja köras.</p>
    <p><strong>windowEndTime=HH:MM</strong> använder som 24-timmars klocka. Definierar när underhållsaktiviteterna som är kopplade till veckounderhållet ska sluta köras om de inte redan har slutförts.</p>
    <p>En underhållsaktivitet kan inte utföras mer än en gång under den här tidsramen.</p>
    <p><strong>windowScheduleWeekdays= Array med två värden från 1-7 (till exempel [5,5])</strong> Det första värdet i arrayen är startdagen när jobbet schemaläggs och det andra värdet är slutdagen när jobbet stoppas. Den exakta tiden för start och slut styrs av windowStartTime respektive windowEndTime.</p>
    </td>
  </tr>
  <tr>
    <td>Månadsvis</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>
    <p><strong>windowSchedule=monthly</strong> (det här värdet ska inte ändras)</p>
    <p><strong>windowStartTime=HH:MM</strong> använder som 24-timmars klocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret för månatligt underhåll ska börja köras.</p>
    <p><strong>windowEndTime=HH:MM</strong> använder som 24-timmars klocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret för månatligt underhåll ska sluta köras om de inte redan har slutförts.</p>
    <p>En underhållsaktivitet kan inte utföras mer än en gång under den här tidsramen.</p>
    <p><strong>windowScheduleWeekdays=Array med två värden från 1-7 (till exempel [5,5])</strong> Det första värdet i arrayen är startdagen när jobbet schemaläggs och det andra värdet är slutdagen när jobbet stoppas. Den exakta tiden för start och slut styrs av windowStartTime respektive windowEndTime.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 att schemalägga den första veckan i månaden eller 1 att schemalägga den sista veckan i månaden. Om ett värde saknas schemaläggs jobben effektivt på den dag som styrs av windowScheduleWeekdays (varje månad).</p>
    </td>
    </tr>
    </tbody>
</table>

**Platser**:

* Dagligen - /apps/settings/granite/operations/intenance/granite_day
* Varje vecka - /apps/settings/granite/operations/intenance/granite_week
* Månadsvis - /apps/settings/granite/operations/intenance/granite_monthly

**Kodexempel**:

Kodexempel 1 (dagligen)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

Kodexempel 2 (varje vecka)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

Kodexempel 3 (månadsvis)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

## Underhållsaktiviteter vid rensning av version och granskningslogg {#purge-tasks}

När du rensar versioner och granskningsloggen minskas storleken på databasen, och i vissa scenarier kan prestandan förbättras.

>[!NOTE]
>
>AEM Guides-kunder bör inte konfigurera version Rensa.

### Standardvärden {#defaults}

Rensa är för närvarande inte aktiverat som standard, men det kommer att ändras i framtiden. Miljöer som skapades innan standardrensningen aktiverades får ett mer konservativt tröskelvärde så att rensning inte inträffar oväntat. Se avsnitten Rensa och Rensa granskningslogg för version nedan för mer information om standardprincipen för rensning.
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

Standardvärdena för tömning kan åsidosättas genom att en konfigurationsfil deklareras och distribueras enligt beskrivningen nedan.

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### Använda en konfiguration {#configure-purge}

Deklarera en konfigurationsfil och distribuera den enligt anvisningarna i följande steg.

>[!NOTE]
>När du har distribuerat noden för versionsrensning i konfigurationsfilen måste du behålla den deklarerad och inte ta bort den. Konfigurationsflödet misslyckas om du försöker göra det.
> 
>På samma sätt måste du behålla granskningsloggens deklarerade nod och inte ta bort den när du distribuerar granskningsloggens tömningsnod i konfigurationsfilen.

**1** Skapa en fil med namnet `mt.yaml` eller liknande.

**2** Placera filen någonstans under en mapp på den översta nivån med namnet `config` eller liknande, enligt beskrivningen i [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#folder-structure).

**3** - Deklarera egenskaper i konfigurationsfilen, som innehåller:

* några egenskaper ovanför datanoden - mer information finns i [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#common-syntax) . Egenskapsvärdet `kind` ska vara *MaintenanceTasks* och versionen ska vara *1*.

* ett dataobjekt med både `versionPurge` och `auditLogPurge` objekt.

Se definitioner och syntax för objekten `versionPurge` och `auditLogPurge` nedan.

Strukturera konfigurationen på liknande sätt som i följande exempel:

```
kind: "MaintenanceTasks"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  versionPurge:
    maximumVersions: 15
    maximumAgeDays: 20
    paths: ["/content"]
    minimumVersions: 1
    retainLabelledVersions: false
  auditLogPurge:
    rules:
      - replication:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
      - pages:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
      - dam:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
```

Kom ihåg att för att konfigurationen ska vara giltig:

* alla egenskaper måste definieras. Det finns inga ärvda standardvärden.
* Typerna (heltal, strängar, booleska värden etc.) i egenskapstabellen nedan måste respekteras.

**4** - Skapa en konfigurationspipeline i Cloud Manager, enligt beskrivningen i artikeln [för konfigurationspipeline.](/help/operations/config-pipeline.md#managing-in-cloud-manager)

### Rensa version {#version-purge}

>[!NOTE]
>
>AEM Guides-kunder bör inte konfigurera version Rensa.

#### Standard för rensning av version {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

Rensa är för närvarande inte aktiverat som standard, men det kommer att ändras i framtiden.

Miljöer som skapades när standardrensningen är aktiverad får följande standardvärden:

* Versioner äldre än 30 dagar tas bort.
* De senaste fem versionerna de senaste 30 dagarna bevaras.
* Oavsett reglerna ovan bevaras den senaste versionen (utöver den aktuella filen).

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Miljöer som skapades innan standardrensningen är aktiverad kommer att ha standardvärdena som listas nedan, men vi rekommenderar att du sänker dessa värden för att optimera prestanda.

* Versioner äldre än 7 år tas bort.
* Alla versioner de senaste sju åren sparas.
* Efter 7 år tas andra versioner än den senaste versionen (utöver den aktuella filen) bort.

#### Egenskaper för versionsrensning {#version-purge-properties}

Tillåtna egenskaper visas nedan.

Kolumnerna som indikerar *standard* anger standardvärdena i framtiden, när standardvärden används. *TBD* visar ett miljö-ID som fortfarande inte har bestämts.

| Egenskaper | framtida standard för envs>TBD | framtida standard för envs&lt;=TBD | obligatoriskt | type | Värden |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| banor | [/content ] | [/content ] | Ja | array med strängar | Anger under vilka sökvägar versioner ska rensas när nya versioner skapas.  Kunder måste deklarera den här egenskapen, men det enda tillåtna värdet är /content. |
| maximumAgeDays | 30 | 2557 (7 år + 2 skottdagar) | Ja | Heltal | Alla versioner som är äldre än det konfigurerade värdet tas bort. Om värdet är 0 utförs inte rensning baserat på versionens ålder. |
| maximumVersions | 5 | 0 (ingen gräns) | Ja | Heltal | Alla versioner som är äldre än den n:te nyaste versionen tas bort. Om värdet är 0 utförs inte rensning baserat på antalet versioner. |
| minimumVersions | 1 | 1 | Ja | Heltal | Det minsta antalet versioner som behålls oavsett ålder. Observera att minst en version alltid behålls. Värdet måste vara 1 eller högre. |
| keepLabelledVersioned | false | false | Ja | boolesk | Avgör om explicit märkta versioner ska exkluderas från rensningen. För bättre databasoptimering rekommenderar vi att du anger värdet till false. |


**Egenskapsinteraktioner**

Följande exempel visar hur egenskaper interagerar när de kombineras.

Exempel:

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

Om det finns 11 versioner dag 23, kommer den äldsta versionen att rensas nästa gång underhållsaktiviteten rensas, eftersom egenskapen `maximumVersions` är inställd på 10.

Om det finns 5 versioner på dag 31 kommer endast 3 att rensas eftersom egenskapen `minimumVersions` är inställd på 2.

Exempel:

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

Inga versioner som är senare än 30 dagar rensas eftersom egenskapen `maximumVersions` är inställd på 0.

En version som är äldre än 30 dagar behålls.

### Rensa granskningslogg {#audit-purge}

#### Granska rensningsstandardinställningar för logg {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

Rensa är för närvarande inte aktiverat som standard, men det kommer att ändras i framtiden.

Miljöer som skapades när standardrensningen är aktiverad får följande standardvärden:

* Replikerings-, DAM- och sidgranskningsloggar som är äldre än 7 dagar tas bort.
* Alla möjliga händelser loggas.

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Miljöer som skapades innan standardrensningen är aktiverad kommer att ha standardvärdena som listas nedan, men vi rekommenderar att du sänker dessa värden för att optimera prestanda.

* Replikerings-, DAM- och sidgranskningsloggar som är äldre än 7 år tas bort.
* Alla möjliga händelser loggas.

>[!NOTE]
>Vi rekommenderar att kunder som har lagstadgade krav på att skapa icke redigerbara granskningsloggar integreras med specialiserade externa tjänster.

#### Rensa egenskaper för granskningslogg {#audit-purge-properties}

Tillåtna egenskaper visas nedan.

Kolumnerna som indikerar *standard* anger standardvärdena i framtiden, när standardvärden används. *TBD* visar ett miljö-ID som fortfarande inte har bestämts.


| Egenskaper | framtida standard för envs>TBD | framtida standard för envs&lt;=TBD | obligatoriskt | type | Värden |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| regler | - | - | Ja | Objekt | En eller flera av följande noder: replikering, sidor, dam. Var och en av dessa noder definierar regler, med egenskaperna nedan. Alla egenskaper måste deklareras. |
| maximumAgeDays | 7 dagar | för alla, 2557 (7 år + 2 skottdagar) | Ja | heltal | För replikering, sidor eller damm: antalet dagar som granskningsloggarna sparas. Granskningsloggar som är äldre än det konfigurerade värdet rensas. |
| contentPath | &quot;/content&quot; | &quot;/content&quot; | Ja | Sträng | Sökvägen som granskningsloggarna rensas under, för den relaterade typen. Måste vara inställt på /content. |
| typer | alla värden | alla värden | Ja | Uppräkningsmatris | De uppräknade värdena för **replikering** är: Aktivera, Inaktivera, Ta bort, Testa, Invertera, Intern omröstning. För **sidor** är de uppräknade värdena: PageCreated, PageModified, PageMoved, PageDeleted, VersionCreated, PageRestated, PageRolled Out, PageValid, PageInvalid. De uppräknade värdena för **dam** är: ASSET_EXPIRING, METADATA_UPDATED, ASSET_EXPIRED, ASSET_REMOVED, RESTORED, ASSET_MOVED, ASSET_VIEWED, PROJECT_VIEWED, PUBLISHED_EXTERNAL, COLLECTION_VIEWED, VERSIONED, ADDED_COMMENT, RENDITION_UPDATED, ACCEPTED, DOWNLOADED, SUBASSET_UPDATED, SUBASSET_REMOVED, ASSET_CREATED, ASSET_SHARED, RENDITION_REMOVED, ASSET_PUBLISHED, ORIGINAL_UPDATED, RENDITION_TION HÄMTAD, AVVISAD. |
