---
title: Underhållsaktiviteter i AEM som en Cloud Service
description: Underhållsaktiviteter i AEM som en Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
translation-type: tm+mt
source-git-commit: 8adead735a5c3c0a03ee6f81372c1714634932ec
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---

# Underhållsaktiviteter i AEM som en Cloud Service

Underhållsåtgärder är processer som körs enligt ett schema för att optimera databasen. Med AEM som Cloud Service är behovet av att kunderna konfigurerar driftsegenskaperna för underhållsåtgärder minimalt. Kunderna kan fokusera sina resurser på frågor som rör applikationsnivå och lämna infrastrukturåtgärderna åt Adobe.

Mer information om underhållsåtgärder finns på följande sidor:

* [AEM Maintenance Guide](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Underhållsuppgifter för instrumentpanelen för åtgärder](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Konfigurera underhållsåtgärder

I tidigare versioner av AEM kunde du konfigurera underhållsåtgärder med underhållskortet (Verktyg > Åtgärder > Underhåll). Underhållskortet är inte längre tillgängligt för AEM som Cloud Service, så konfigurationer bör implementeras med källkontroll och driftsättas med hjälp av Cloud Manager. Adobe hanterar underhållsåtgärder som inte kräver kundbeslut (t.ex. Datastore Garbage Collection) medan andra underhållsåtgärder kan konfigureras av kunden (se tabellen nedan).

>[!CAUTION]
>
>Adobe förbehåller sig rätten att åsidosätta en kunds konfigurationsinställningar för underhållsaktiviteter för att minska problem som prestandaförsämringar.

I följande tabell visas underhållsåtgärder som är tillgängliga när AEM släpps som en Cloud Service.

| Underhållsaktivitet | Vem äger konfigurationen | Konfigurera (valfritt) |
|---|---|---|
| Skräpsamling för datastaarkiv | Adobe | Ej tillämpligt - ägs till fullo av Adobe |
| Rensa version | Adobe | Helägd av Adobe, men i framtiden kommer kunderna att kunna konfigurera vissa parametrar. |
| Rensa granskningslogg | Adobe | Helägd av Adobe, men i framtiden kommer kunderna att kunna konfigurera vissa parametrar. |
| Lucene Binaries Cleanup | Adobe | Oanvänd och därför inaktiverad av Adobe. |
| Ad hoc-aktivitetsrensning | Kund | Måste göras i github. <br> Åsidosätt den färdiga konfigurationsnoden i underhållfönstret under  `/libs` genom att skapa egenskaper under mappen  `/apps/settings/granite/operations/maintenance/granite_weekly` eller  `granite_daily`. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation. <br> Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den  `granite_TaskPurgeTask`) med lämpliga egenskaper. <br> Konfigurera OSGI-egenskaperna i dokumentationen för  [AEM 6.5 Maintenance Task](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Rensa arbetsflöde | Kund | Måste göras i github. <br> Åsidosätt den körklara konfigurationsnoden för underhållsfönstret under  `/libs` genom att skapa egenskaper under `/apps/settings/granite/operations/maintenance/granite_weekly` mappen  `granite_daily`. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation. <br> Aktivera underhållsaktiviteten genom att lägga till en annan nod under noden ovan (namnge den  `granite_WorkflowPurgeTask`) med lämpliga egenskaper. <br> Konfigurera OSGI-egenskaperna i  [AEM 6.5 Maintenance Task-dokumentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Rensa projekt | Kund | Måste göras i github. <br> Åsidosätt den färdiga konfigurationsnoden i underhållfönstret under  `/libs` genom att skapa egenskaper under mappen  `/apps/settings/granite/operations/maintenance/granite_weekly` eller  `granite_daily`. Se tabellen i underhållsfönstret nedan för ytterligare konfigurationsinformation. <br> Aktivera underhållsaktiviteten genom att lägga till en nod under noden ovan (namnge den  `granite_ProjectPurgeTask`) med lämpliga egenskaper. <br> Konfigurera OSGI-egenskaper, se  [AEM 6.5 Maintenance Task-dokumentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Kunderna kan schemalägga underhållsaktiviteter för arbetsflödestömning, Ad-hoc-aktivitetsrensning och projekttömning som ska utföras under underhållsperioden varje dag, vecka eller månad. Dessa konfigurationer bör redigeras direkt i källkontrollen. Tabellen nedan beskriver de konfigurationsparametrar som är tillgängliga för varje fönster.

<table>
  <tr>
    <th>Konfiguration av underhållsfönster</th>
    <th>Vem äger konfigurationen</th>
    <th>Konfigurationstyp</th>
    <th>Plats</th>
    <th>Exempel</th>
    <th>Parametrar</th>
  </tr>
  <tr>
    <td>Dagligen</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>Se plats 1 nedan</td>
    <td>Se kodexempel 1 nedan</td>
  <td>
  <strong>windowSchedule</strong> = day (det här värdet ska inte ändras) 
  <strong>windowStartTime</strong> = HH:MM med 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska börja köras.
  <strong>windowEndTime</strong> = HH:MM med 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska sluta köras om de inte redan har slutförts.
  </td> 
  </tr>
  <tr>
    <td>Vecka</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>Se plats 2 nedan</td>
    <td>Se kodexempel 2 nedan</td>
    <td>
    <strong>windowSchedule</strong> = week (det här värdet ska inte ändras) 
    <strong>windowStartTime</strong> = HH:MM med 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till veckounderhållet ska börja köras.
    <strong>windowEndTime</strong> = HH:MM med 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till veckounderhållet ska sluta köras om de inte redan har slutförts.
    <strong>windowScheduleWeekdays = Array med 2 värden mellan 1 och 7. t.ex. [5,5].</strong> Det första värdet i arrayen är startdagen när jobbet schemaläggs och det andra värdet är slutdagen då jobbet stoppas. Den exakta tiden för start och slut styrs av windowStartTime respektive windowEndTime.
    </td> 
  </tr>
  <tr>
    <td>Månadsvis</td>
    <td>Kund</td>
    <td>JCR-noddefinition</td>
    <td>Se plats 3 nedan</td>
    <td>Se kodexempel 3 nedan</td>
    <td>
    <strong>windowSchedule</strong> = day (det här värdet ska inte ändras) 
    <strong>windowStartTime</strong> = HH:MM med 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret för månatligt underhåll ska börja köras.
    <strong>windowEndTime</strong> = HH:MM med 24-timmarsklocka. Definierar när underhållsaktiviteterna som är kopplade till fönstret för månatligt underhåll ska sluta köras om de inte redan har slutförts.
    <strong>windowScheduleWeekdays = Array med 2 värden mellan 1 och 7. t.ex. [5,5].</strong> Det första värdet i arrayen är startdagen när jobbet schemaläggs och det andra värdet är slutdagen då jobbet stoppas. Den exakta tiden för start och slut styrs av windowStartTime respektive windowEndTime.
    <strong>windowFirstLastStartDay - 0/1</strong> 0 för att schemalägga den första veckan i månaden eller 1 för att schemalägga den sista veckan i månaden. Om ett värde saknas schemaläggs jobben effektivt varje dag enligt windowScheduleWeekdays varje månad.
    </td> 
    </tr>
</table>

Platser:

1. /apps/settings/granite/operations/intenance/granite_day
2. /apps/settings/granite/operations/intenance/granite_week
3. /apps/settings/granite/operations/intenance/granite_monthly

Kodexempel:

Kodexempel 1

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

Kodexempel 2

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

Kodexempel 3

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

| Konfiguration av underhållsfönster | Vem äger konfigurationen | Konfigurationstyp | Plats | Exempel | Parametrar |
|---|---|---|---|---|---|
| Dagligen | Kund | JCR-noddefinition | Se plats 2 nedan | Se kodexempel 2 nedan | **windowSchedule= day** (det här värdet ska inte ändras).  <br> **windowStartTime= HH:** MMusing as 24 hour clock. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska börja köras. <br> **windowEndTime= HH:** MMusing as 24 hour clock. Definierar när underhållsaktiviteterna som är kopplade till fönstret Dagligt underhåll ska sluta köras om de inte redan har slutförts. |
