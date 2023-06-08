---
title: Administrera arbetsflödesinstanser
description: Lär dig hur du administrerar arbetsflödesinstanser
feature: Administering
role: Admin
source-git-commit: 5801063c9c4c1c6b9f9e7f55ad4d66bb563e0eef
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# Administrera arbetsflödesinstanser {#administering-workflow-instances}

Arbetsflödeskonsolen innehåller flera verktyg för att administrera arbetsflödesinstanser för att säkerställa att de körs som förväntat.

Det finns en rad konsoler som du kan använda för att administrera dina arbetsflöden. Använd [global navigering](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) för att öppna **verktyg** välj **Arbetsflöde**:

* **Modeller**: Hantera arbetsflödesdefinitioner
* **Instanser**: Visa och hantera pågående arbetsflödesinstanser
* **Startare**: Hantera hur arbetsflöden ska startas
* **Arkiv**: Visa historik över arbetsflöden som har slutförts
* **Fel**: Visa historik över arbetsflöden som slutförts med fel
* **Tilldela automatiskt**: Konfigurera automatisk tilldelning av arbetsflöden till mallar

## Övervaka status för arbetsflödesinstanser {#monitoring-the-status-of-workflow-instances}

1. Använd navigeringsval **verktyg** sedan **Arbetsflöde**.
1. Välj **Instanser** för att visa en lista över pågående arbetsflödesinstanser.
1. På den övre listen i det högra hörnet visas arbetsflödesinstanserna **Köra arbetsflöden**, **Status** och **Detaljer**.
1. **Köra arbetsflöden** visar antalet arbetsflöden som körs och deras status. I de angivna bilderna visas till exempel antalet **Köra arbetsflöden** och **Status** AEM.
   ![status-hälsosam](/help/sites-cloud/administering/assets/status-healthy.png)
   ![status-ohälsosam](/help/sites-cloud/administering/assets/status-unhealthy.png)
1. För **Statusinformation** av arbetsflödesinstanser klickar du på **Detaljer** för att visa **antal arbetsflödesinstanser som körs**, **slutförda arbetsflödesinstanser**, **avbrutna arbetsflödesinstanser**, **misslyckade arbetsflödesinstanser** och så vidare. nedan visas till exempel de bilder som visas **Statusinformation** med **Status: Hälsosam** och **Status: Ohälsosam**.
   ![status-details-good](/help/sites-cloud/administering/assets/status-details-healthy.png)

   ![status-details-unsafe](/help/sites-cloud/administering/assets/status-details-unhealthy.png)

   >[!NOTE]
   >
   > Om du vill att arbetsflödesinstansen ska vara felfri följer du god praxis på [regelbunden rensning av arbetsflödesinstanser](#regular-purging-of-workflow-instances) eller [arbetsflöden](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-best-practices.html?lang=en).

## Sök efter arbetsflödesinstanser {#search-workflow-instances}

1. Använd navigeringsval **verktyg** sedan **Arbetsflöde**.
1. Välj **Instanser** om du vill visa en lista över pågående arbetsflödesinstanser. I den övre rälen, i det vänstra hörnet, väljer du **Filter**. Du kan också använda tangenterna Alt+1. Följande dialogruta visas:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Välj sökvillkor för arbetsflödet i dialogrutan Filter. Du kan söka baserat på följande indata:

   * Nyttolastsökväg: Markera en specifik bana
   * Arbetsflödesmodell: Välj en arbetsflödesmodell
   * Uppdragare: Välj en arbetsflödestilldelare
   * Typ: Aktivitet, arbetsflödesobjekt eller arbetsflödesfel
   * Aktivitetsstatus: Aktiv, Fullständig eller Avbruten
   * Var jag är: Ägare OCH tilldelad, endast ägare, endast tilldelad
   * Startdatum: Startdatum före eller efter ett angivet datum
   * Slutdatum: Slutdatum före eller efter ett angivet datum
   * Förfallodatum: Förfallodatum före eller efter ett angivet datum
   * Uppdateringsdatum: Uppdaterat datum före eller efter ett angivet datum

## Göra uppehåll, återuppta och avsluta en arbetsflödesinstans {#suspending-resuming-and-terminating-a-workflow-instance}

1. Använd navigeringsval **verktyg** sedan **Arbetsflöde**.
1. Välj **Instanser** om du vill visa en lista över pågående arbetsflödesinstanser.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Markera ett specifikt objekt och använd sedan **Avsluta**, **Gör uppehåll**, eller **Återuppta**, beroende på vad som är lämpligt, bekräftelse och/eller ytterligare uppgifter krävs:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >Om du vill avsluta eller avbryta ett arbetsflöde måste det vara i ett läge där användaren väntar på att göra något, till exempel i ett deltagarsteg. Om du försöker avbryta ett arbetsflöde som för närvarande kör jobb (aktiva trådar som körs) kanske inte resultatet blir som du förväntar dig.


## Visa arkiverade arbetsflöden {#viewing-archived-workflows}

1. Använd navigeringsval **verktyg** sedan **Arbetsflöde**.

1. Välj **Arkiv** om du vill visa en lista över arbetsflödesinstanser som har slutförts.

   ![arkiverade instanser](/help/sites-cloud/administering/assets/archived-instances.png)

   >[!NOTE]
   >
   >
   >Avbruten status betraktas som en avslutad åtgärd eftersom den inträffar till följd av en användaråtgärd. till exempel:
   >
   >* användning av **Avsluta** åtgärd
   >* När en sida, som är underställd ett arbetsflöde, (framtvingas) tas bort, avslutas arbetsflödet.


1. Markera ett specifikt objekt och sedan **Öppna historik** för mer information:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Åtgärdar fel i arbetsflödesinstansen {#fixing-workflow-instance-failures}

När ett arbetsflöde misslyckas, innehåller AEM **Fel** så att du kan undersöka och vidta lämpliga åtgärder när originalorsaken har hanterats:

* **Felinformation**
Öppnar ett fönster för att visa 
**Felmeddelande**, **Step och **Felstapel**.

* **Öppna historik**
Visar information om arbetsflödeshistoriken.

* **Försök igen** Kör komponentinstansen Script Step igen. Använd kommandot Försök igen när du har åtgärdat orsaken till det ursprungliga felet. Du kan till exempel försöka utföra steget igen när du har åtgärdat ett fel i skriptet som utförs av processteget.
* **Avsluta** Avsluta arbetsflödet om felet har orsakat en oförenlig situation för arbetsflödet. Arbetsflödet kan t.ex. förlita sig på miljöförhållanden som information i databasen som inte längre är giltig för arbetsflödesinstansen.
* **Avsluta och försök igen** liknar **Avsluta** förutom att en ny arbetsflödesinstans startas med den ursprungliga nyttolasten, titeln och beskrivningen.

Så här undersöker du fel och sedan återupptar eller avslutar du arbetsflödet:

1. Använd navigeringsval **verktyg** sedan **Arbetsflöde**.

1. Välj **Fel** för att visa en lista över arbetsflödesinstanser som inte har slutförts korrekt.
1. Välj ett specifikt objekt och sedan lämplig åtgärd:

![arbetsflödesfel](/help/sites-cloud/administering/assets/workflow-failure.png)

## Vanlig tömning av arbetsflödesinstanser {#regular-purging-of-workflow-instances}

Om du minimerar antalet arbetsflödesinstanser ökas arbetsflödesmotorns prestanda, så att du regelbundet kan rensa avslutade eller pågående arbetsflödesinstanser från databasen.

Konfigurera **Rensa arbetsflöde för Adobe Granite** för att rensa arbetsflödesinstanser utifrån deras ålder och status. Du kan också rensa arbetsflödesinstanser av alla modeller eller av en viss modell.

Du kan också skapa flera konfigurationer av tjänsten för att rensa arbetsflödesinstanser som uppfyller olika villkor. Skapa till exempel en konfiguration som tömmer instanser av en viss arbetsflödesmodell när de körs mycket längre än förväntat. Skapa en annan konfiguration som tömmer alla slutförda arbetsflöden efter några dagar för att minimera databasens storlek.

Om du vill konfigurera tjänsten kan du konfigurera OSGi-konfigurationsfilerna på [OSGi-konfigurationsfiler](/help/implementing/deploying/configuring-osgi.md). I följande tabell beskrivs de egenskaper som du behöver för båda metoderna.

>[!NOTE]
>För att lägga till konfigurationen i databasen är tjänst-PID:
>`com.adobe.granite.workflow.purge.Scheduler`
>Eftersom tjänsten är en fabrikstjänst är namnet på `sling:OsgiConfig` noden kräver ett identifierarsuffix, till exempel:
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

Du kan ange den maximala storleken för inkorgen genom att konfigurera **Adobe Granite Workflow Service**, se [lägga till en OSGi-konfiguration i databasen](/help/implementing/deploying/configuring-osgi.md). I följande tabell beskrivs egenskapen som du konfigurerar.

>[!NOTE]
>För att lägga till konfigurationen i databasen är tjänst-PID:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Egenskapsnamn (webbkonsol) | OSGi-egenskapsnamn |
|---|---|
| Max Inbox Query Size | granite.workflow.inboxQuerySize |

## Använda arbetsflödesvariabler för kundägda datalager {#using-workflow-variables-customer-datastore}

Data som bearbetas av arbetsflöden lagras i den Adobe-tillhandahållna lagringen (JCR). Dessa data kan vara känsliga till sin natur. Du kanske vill spara alla användardefinierade metadata/data i ditt egna hanterade lagringsutrymme i stället för det lagringsutrymme som Adobe tillhandahåller. I dessa avsnitt beskrivs hur du ställer in dessa variabler för extern lagring.

### Ange modellen för extern lagring av metadata {#set-model-for-external-storage}

På arbetsflödesmodellnivån anges en flagga som anger att modellen (och dess körningsinstanser) har extern lagring av metadata. Arbetsflödesvariabler sparas inte i JCR för arbetsflödesinstanser av modeller som är markerade för extern lagring.

Egenskapen *userMetadataPersistenceEnabled* lagras på *jcr:innehållsnod* av arbetsflödesmodellen. Den här flaggan bevaras i arbetsflödets metadata som *cq:userMetaDataCustomPersistenceEnabled*.

Bilden nedan måste ange flaggan i ett arbetsflöde.

![workflow-externalize-config](/help/sites-cloud/administering/assets/workflow-externalize-config.png)

### API:er för metadata i extern lagring {#apis-for-metadata-external-storage}

Om du vill lagra variablerna externt måste du implementera de API:er som arbetsflödet visar.

UserMetaDataPersistenceContext

I följande exempel visas hur du använder API:t.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
} 
```


