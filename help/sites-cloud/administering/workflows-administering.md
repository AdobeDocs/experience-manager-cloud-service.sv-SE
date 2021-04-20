---
title: Administrera arbetsflödesinstanser
description: Lär dig hur du administrerar arbetsflödesinstanser
feature: Administering
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---


# Administrera arbetsflödesinstanser {#administering-workflow-instances}

Arbetsflödeskonsolen innehåller flera verktyg för att administrera arbetsflödesinstanser för att säkerställa att de körs som förväntat.

Det finns en rad konsoler som du kan använda för att administrera dina arbetsflöden. Använd [global navigering](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) för att öppna rutan **Verktyg** och välj sedan **Arbetsflöde**:

* **Modeller**: Hantera arbetsflödesdefinitioner
* **Instanser**: Visa och hantera pågående arbetsflödesinstanser
* **Startprogram**: Hantera hur arbetsflöden ska startas
* **Arkiv**: Visa historik över arbetsflöden som har slutförts
* **Fel**: Visa historik över arbetsflöden som slutförts med fel
* **Tilldela** automatiskt: Konfigurera automatisk tilldelning av arbetsflöden till mallar

## Övervaka status för arbetsflödesinstanser {#monitoring-the-status-of-workflow-instances}

1. Välj **Verktyg** och **Arbetsflöde** med Navigering.
1. Välj **Instanser** om du vill visa listan över pågående arbetsflödesinstanser.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Sök efter arbetsflödesinstanser {#search-workflow-instances}

1. Välj **Verktyg** och **Arbetsflöde** med Navigering.
1. Välj **Instanser** om du vill visa listan över pågående arbetsflödesinstanser. Välj **Filter** i den övre listen i det vänstra hörnet. Du kan också använda tangenterna Alt+1. Följande dialogruta visas:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Välj sökvillkor för arbetsflödet i dialogrutan Filter. Du kan söka baserat på följande indata:

   * Nyttolastsökväg: Markera en specifik bana
   * Arbetsflödesmodell: Välj en arbetsflödesmodell
   * Uppdragare: Välj en arbetsflödestilldelare
   * Typ: Aktivitet, arbetsflödesobjekt eller arbetsflödesfel
   * Aktivitetsstatus: Aktiv, fullständig eller avslutad
   * Var jag är: Ägare OCH tilldelad, endast ägare, endast tilldelad
   * Startdatum: Startdatum före eller efter ett angivet datum
   * Slutdatum: Slutdatum före eller efter ett angivet datum
   * Förfallodatum: Förfallodatum före eller efter ett angivet datum
   * Uppdateringsdatum: Uppdaterat datum före eller efter ett angivet datum

## Pausa, återuppta och avsluta en arbetsflödesinstans {#suspending-resuming-and-terminating-a-workflow-instance}

1. Välj **Verktyg** och **Arbetsflöde** med Navigering.
1. Välj **Instanser** om du vill visa listan över pågående arbetsflödesinstanser.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Markera ett specifikt objekt och använd sedan **Avsluta**, **Gör uppehåll** eller **Fortsätt**, beroende på vad som är lämpligt. bekräftelse och/eller ytterligare uppgifter krävs:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Visa arkiverade arbetsflöden {#viewing-archived-workflows}

1. Välj **Verktyg** och **Arbetsflöde** med Navigering.

1. Välj **Arkiv** om du vill visa en lista över de arbetsflödesinstanser som har slutförts.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >Avbruten status betraktas som en avslutad åtgärd eftersom den inträffar till följd av en användaråtgärd. till exempel:
   >
   >* användning av åtgärden **Avsluta**
   >* när en sida, som är underställd ett arbetsflöde, tas bort (framtvingar), avslutas arbetsflödet


1. Markera ett specifikt objekt och **Öppna historik** för mer information:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Åtgärdar fel i arbetsflödesinstansen {#fixing-workflow-instance-failures}

När ett arbetsflöde misslyckas tillhandahåller AEM konsolen **Misslyckanden** så att du kan undersöka och vidta lämpliga åtgärder när den ursprungliga orsaken har hanterats:

* **FelinformationÖppnar**
ett fönster där 
**Felmeddelande**,  **** Stepand- **felhög**.

* **Öppna**
historik Visar information om arbetsflödeshistoriken.

* **Försök** stega igenKör komponentinstansen för skriptsteget igen. Använd kommandot Försök igen när du har åtgärdat orsaken till det ursprungliga felet. Du kan till exempel försöka utföra steget igen när du har åtgärdat ett fel i skriptet som utförs av processteget.
* **Avsluta** Avsluta arbetsflödet om felet har orsakat en situation som inte kan stämmas av för arbetsflödet. Arbetsflödet kan t.ex. förlita sig på miljöförhållanden som information i databasen som inte längre är giltig för arbetsflödesinstansen.
* **Avsluta och** RetryLiknar  **** Terminate förutom att en ny arbetsflödesinstans startas med den ursprungliga nyttolasten, titeln och beskrivningen.

Så här undersöker du fel och sedan återupptar eller avslutar du arbetsflödet:

1. Välj **Verktyg** och **Arbetsflöde** med Navigering.

1. Välj **Fel** om du vill visa listan över arbetsflödesinstanser som inte slutfördes korrekt.
1. Välj ett specifikt objekt och sedan lämplig åtgärd:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Vanlig tömning av arbetsflödesinstanser {#regular-purging-of-workflow-instances}

Om du minimerar antalet arbetsflödesinstanser ökas arbetsflödesmotorns prestanda, så att du regelbundet kan rensa avslutade eller pågående arbetsflödesinstanser från databasen.

Konfigurera **Rensa arbetsflöde i Adobe** för att rensa arbetsflödesinstanser efter ålder och status. Du kan också rensa arbetsflödesinstanser av alla modeller eller av en viss modell.

Du kan också skapa flera konfigurationer av tjänsten för att rensa arbetsflödesinstanser som uppfyller olika villkor. Skapa till exempel en konfiguration som tömmer instanser av en viss arbetsflödesmodell när de körs mycket längre än förväntat. Skapa en annan konfiguration som tömmer alla slutförda arbetsflöden efter ett visst antal dagar för att minimera databasens storlek.

Om du vill konfigurera tjänsten kan du konfigurera OSGi-konfigurationsfiler i [OSGi-konfigurationsfiler](/help/implementing/deploying/configuring-osgi.md). I följande tabell beskrivs de egenskaper som du behöver för båda metoderna.

>[!NOTE]
>För att lägga till konfigurationen i databasen är tjänst-PID:
>`com.adobe.granite.workflow.purge.Scheduler`
>Eftersom tjänsten är en fabrikstjänst kräver namnet på noden `sling:OsgiConfig` ett identifierarsuffix, till exempel:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Egenskapsnamn (webbkonsol)</th>
   <th>OSGi-egenskapsnamn</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Jobbnamn</td>
   <td>scheduledpurge.name</td>
   <td>Ett beskrivande namn för den schemalagda rensningen.</td>
  </tr>
  <tr>
   <td>Arbetsflödesstatus</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>Status för de arbetsflödesinstanser som ska rensas. Följande värden är giltiga:</p>
    <ul>
     <li>SLUTFÖRT: Slutförda arbetsflödesinstanser rensas.</li>
     <li>KÖRS: Körande arbetsflödesinstanser rensas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modeller att tömma</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>ID:t för arbetsflödesmodellerna som ska rensas. ID är sökvägen till modellnoden, till exempel:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Ange inget värde för att rensa instanser av alla arbetsflödesmodeller.</p> <p>Om du vill ange flera modeller klickar du på plusknappen (+) i webbkonsolen. </p> </td>
  </tr>
  <tr>
   <td>Arbetsflödesålder</td>
   <td>scheduledpurge.daysold</td>
   <td>Åldern på arbetsflödesinstanserna som ska rensas, i dagar.</td>
  </tr>
 </tbody>
</table>

## Ange maximal storlek för inkorgen {#setting-the-maximum-size-of-the-inbox}

Du kan ange den största tillåtna storleken för inkorgen genom att konfigurera **arbetsflödestjänsten Adobe Granite**, se [lägga till en OSGi-konfiguration i databasen](/help/implementing/deploying/configuring-osgi.md). I följande tabell beskrivs egenskapen som du konfigurerar.

>[!NOTE]
>För att lägga till konfigurationen i databasen är tjänst-PID:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Egenskapsnamn (webbkonsol) | OSGi-egenskapsnamn |
|---|---|
| Max Inbox Query Size | granite.workflow.inboxQuerySize |

