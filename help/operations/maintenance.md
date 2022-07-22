---
title: Underhållsaktiviteter på AEM as a Cloud Service
description: Underhållsaktiviteter på AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 8bd001f6f70ce1aa9a63623b3ad68793fa355c9a
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---

# Underhållsaktiviteter på AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Underhållsåtgärder"
>abstract="Underhållsåtgärder är processer som körs enligt ett schema för att optimera databasen. Med AEM as a Cloud Service är behovet av att kunderna konfigurerar driftsegenskaperna för underhållsåtgärder minimal. Kunderna kan fokusera sina resurser på frågor som rör applikationsnivå och lämna infrastrukturåtgärderna åt Adobe."

Underhållsåtgärder är processer som körs enligt ett schema för att optimera databasen. Med AEM as a Cloud Service är behovet av att kunderna konfigurerar driftsegenskaperna för underhållsåtgärder minimal. Kunderna kan fokusera sina resurser på frågor som rör applikationsnivå och lämna infrastrukturåtgärderna åt Adobe.

## Konfigurera underhållsåtgärder

I tidigare versioner av AEM kunde du konfigurera underhållsåtgärder med underhållskortet (Verktyg > Åtgärder > Underhåll). Underhållskortet är inte längre tillgängligt för AEM as a Cloud Service, så konfigurationer bör implementeras för källkontroll och driftsättas med hjälp av Cloud Manager. Adobe hanterar underhållsuppgifter som har inställningar som inte kan konfigureras av kunder (t.ex. Datastore Skräpsamling, Rensa granskningslogg, Rensa version). Andra underhållsuppgifter kan konfigureras av kunder, vilket beskrivs i tabellen nedan.

>[!CAUTION]
>
>Adobe förbehåller sig rätten att åsidosätta en kunds konfigurationsinställningar för underhållsaktiviteter för att minska problem som prestandaförsämringar.

I följande tabell visas underhållsåtgärder som är tillgängliga när AEM as a Cloud Service släpps.

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
    <td>Adobe</td>
    <td>För att författarnivån ska kunna fortsätta att fungera måste äldre versioner av varje del av innehållet under <code>/content</code> databasens nod rensas enligt följande:<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->
     <ol>
       <li>Versioner som är äldre än 30 dagar tas bort</li>
       <li>De senaste 5 versionerna de senaste 30 dagarna sparas</li>
       <li>Oavsett reglerna ovan bevaras den senaste versionen.</li>
     </ol><br>OBS! beteendet som beskrivs ovan används som standard för nya miljöer som skapas efter den 14 mars 2022. Skicka in en kundsupportanmälan om du behöver andra inställningar.</td>
  </td>
  </tr>
  <tr>
    <td>Rensa granskningslogg</td>
    <td>Adobe</td>
    <td>För att författarnivån ska fortsätta att fungera måste äldre granskningsloggar finnas under <code>/content</code> databasens nod rensas enligt följande:<br><br> <!-- See above for the two line breaks -->
     <ol>
       <li>Granskningsloggar som är äldre än 3 dagar tas bort för replikeringsgranskning</li>
       <li>För DAM-granskning (Assets) tas granskningsloggar som är äldre än 30 dagar bort</li>
       <li>Vid sidgranskning tas loggar som är äldre än 3 dagar bort.</li>
     </ol><br>OBS! beteendet som beskrivs ovan används som standard för nya miljöer som skapas efter den 14 mars 2022. Skicka in en kundsupportanmälan om du behöver andra inställningar.</td>
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
    <p>Måste göras i git. Åsidosätt den färdiga konfigurationsnoden för underhållsperioden under <code>/libs</code> genom att skapa egenskaper under mappen <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> eller <code>granite_daily</code>.</p>
    <p>Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation. Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den) <code>granite_TaskPurgeTask</code>) med lämpliga egenskaper. Konfigurera OSGI-egenskaperna.</p>
  </td>
  </tr>
    <tr>
    <td>Rensa arbetsflöde</td>
    <td>Kund</td>
    <td>
    <p>Måste göras i git. Åsidosätt den färdiga konfigurationsnoden för underhållsperioden under <code>/libs</code> genom att skapa egenskaper under mappen <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> eller <code>granite_daily</code>. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation.</p>
    <p>Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den) <code>granite_WorkflowPurgeTask</code>) med lämpliga egenskaper. Konfigurera OSGI-egenskaperna finns i <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances">AEM 6.5 Maintenance Task - dokumentation</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Rensa projekt</td>
    <td>Kund</td>
    <td>
    <p>Måste göras i git. Åsidosätt den färdiga konfigurationsnoden för underhållsperioden under <code>/libs</code> genom att skapa egenskaper under mappen <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> eller <code>granite_daily</code>. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation.</p>
    <p>Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den) <code>granite_ProjectPurgeTask</code>) med lämpliga egenskaper. Konfigurera OSGI-egenskaperna.</p>
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
  <p><strong>windowStartTime=HH:MM</strong> med som 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska börja köras.</p>
  <p><strong>windowEndTime=HH:MM</strong> med som 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska sluta köras om de inte redan har slutförts.</p>
  </td> 
  </tr>
  <tr>
    <td>Vecka</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>
    <p><strong>windowSchedule=week</strong> (det här värdet ska inte ändras)</p>
    <p><strong>windowStartTime=HH:MM</strong> med som 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till veckounderhållet ska börja köras.</p>
    <p><strong>windowEndTime=HH:MM</strong> med som 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till veckounderhållet ska sluta köras om de inte redan har slutförts.</p>
    <p><strong>windowScheduleWeekdays= Array med 2 värden mellan 1 och 7 (t.ex. [5,5])</strong> Det första värdet i arrayen är startdagen när jobbet schemaläggs och det andra värdet är slutdagen då jobbet stoppas. Den exakta tiden för start och slut styrs av windowStartTime respektive windowEndTime.</p>
    </td>
  </tr>
  <tr>
    <td>Månadsvis</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>
    <p><strong>windowSchedule=day</strong> (det här värdet ska inte ändras)</p>
    <p><strong>windowStartTime=HH:MM</strong> med som 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret för månatligt underhåll ska börja köras.</p>
    <p><strong>windowEndTime=HH:MM</strong> med som 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret för månatligt underhåll ska sluta köras om de inte redan har slutförts.</p>
    <p><strong>windowScheduleWeekdays=Array med 2 värden mellan 1 och 7 (t.ex. [5,5])</strong> Det första värdet i arrayen är startdagen när jobbet schemaläggs och det andra värdet är slutdagen då jobbet stoppas. Den exakta tiden för start och slut styrs av windowStartTime respektive windowEndTime.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 att schemalägga den första veckan i månaden eller 1 att schemalägga den sista veckan i månaden. Om ett värde saknas schemaläggs jobben effektivt varje dag enligt windowScheduleWeekdays varje månad.</p>
    </td> 
    </tr>
    </tbody>
</table>

**Platser**:

* Dagligen - /apps/settings/granite/operations/intenance/granite_day
* Varje vecka - /apps/settings/granite/operations/intenance/granite_week
* Varje månad - /apps/settings/granite/operations/intenance/granite_monthly

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
