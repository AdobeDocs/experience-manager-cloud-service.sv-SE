---
title: Administrera arbetsflödesinstanser
description: Lär dig administrera arbetsflödesinstanser med arbetsflödeskonsolen
feature: Administering
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
solution: Experience Manager Sites
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 0%

---

# Administrera arbetsflödesinstanser {#administering-workflow-instances}

Arbetsflödeskonsolen innehåller flera verktyg för att administrera arbetsflödesinstanser för att säkerställa att de körs som förväntat.

Det finns en rad konsoler som du kan använda för att administrera dina arbetsflöden. Använd den [globala navigeringen](/help/sites-cloud/authoring/basic-handling.md#global-navigation) för att öppna rutan **Verktyg** och välj sedan **Arbetsflöde**:

* **Modeller**: Hantera arbetsflödesdefinitioner
* **Instanser**: Visa och hantera arbetsflödesinstanser som körs
* **Startprogram**: Hantera hur arbetsflöden ska startas
* **Arkiv**: Visa historik över slutförda arbetsflöden
* **Fel**: Visa historik över arbetsflöden som slutförts med fel
* **Tilldela automatiskt**: Konfigurera automatisk tilldelning av arbetsflöden till mallar

## Övervaka status för arbetsflödesinstanser {#monitoring-the-status-of-workflow-instances}

1. Välj **Verktyg** och sedan **Arbetsflöde** med Navigering.
1. Välj **Instanser** om du vill visa listan över pågående arbetsflödesinstanser.
1. På den övre listen i det högra hörnet visar arbetsflödesinstanserna **Löpande arbetsflöden**, **Status** och **Information**.
1. **Arbetsflöden som körs** visar antalet arbetsflöden som körs och deras status. I de angivna bilderna visas till exempel antalet **pågående arbetsflöden** och **Status** för AEM-instansen:

   * **Status: Felfri**
     ![status-hälsosam](/help/sites-cloud/administering/assets/status-healthy.png)

   * **Status: Ohälsosamt**
     ![statusfelfri](/help/sites-cloud/administering/assets/status-unhealthy.png)

1. Om du vill ha **statusinformation** för arbetsflödesinstanser klickar du på **Information** för att visa **antalet arbetsflödesinstanser som körs**, **slutförda arbetsflödesinstanser**, **avbrutna arbetsflödesinstanser**, **misslyckade arbetsflödesinstanser** och så vidare. Nedan visas till exempel de bilder som visar **statusinformation** med:

   * **Statusinformation: Felfri**
     ![status-details-hälsosam](/help/sites-cloud/administering/assets/status-details-healthy.png)

   * **Statusinformation: Ohälsosam**
     ![status-details-unsafe](/help/sites-cloud/administering/assets/status-details-unhealthy.png)

   >[!NOTE]
   >
   > Om du vill att arbetsflödesinstansen ska vara felfri följer du god praxis vid [regelbunden rensning av arbetsflödesinstanser](#regular-purging-of-workflow-instances) eller [arbetsflödets bästa praxis](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-best-practices.html).

## Sök efter arbetsflödesinstanser {#search-workflow-instances}

1. Välj **Verktyg** och sedan **Arbetsflöde** med Navigering.
1. Välj **Instanser** om du vill visa listan över pågående arbetsflödesinstanser. Välj **Filter** i det vänstra hörnet på den övre listen. Du kan också använda tangenterna Alt+1. Följande dialogruta visas:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Välj sökvillkor för arbetsflödet i dialogrutan Filter. Du kan söka baserat på följande indata:

   * Nyttolastsökväg: Välj en specifik sökväg
   * Arbetsflödesmodell: Välj en arbetsflödesmodell
   * Tilldelad: Välj en arbetsflödestilldelad
   * Typ: Aktivitet, arbetsflödesobjekt eller arbetsflödesfel
   * Aktivitetsstatus: Aktiv, Fullständig eller Avbruten
   * Var jag är: Ägare OCH tilldelad, Endast ägare, Endast tilldelad
   * Startdatum: Startdatum före eller efter ett angivet datum
   * Slutdatum: Slutdatum före eller efter ett angivet datum
   * Förfallodatum: Förfallodatum före eller efter ett angivet datum
   * Uppdateringsdatum: Uppdateringsdatum före eller efter ett angivet datum

## Göra uppehåll, återuppta och avsluta en arbetsflödesinstans {#suspending-resuming-and-terminating-a-workflow-instance}

1. Välj **Verktyg** och sedan **Arbetsflöde** med Navigering.
1. Välj **Instanser** om du vill visa listan över pågående arbetsflödesinstanser.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Välj ett specifikt objekt och använd sedan **Avsluta**, **Gör uppehåll** eller **Återuppta**, beroende på vad som är lämpligt. Bekräftelse och/eller ytterligare information krävs:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >Om du vill avsluta eller avbryta ett arbetsflöde måste det vara i ett läge där användaren väntar på att göra något, t.ex. i ett deltagarsteg. Om du försöker avbryta ett arbetsflöde som för närvarande kör jobb (aktiva trådar som körs) kanske inte resultatet blir som du förväntar dig.


## Visa arkiverade arbetsflöden {#viewing-archived-workflows}

1. Välj **Verktyg** och sedan **Arbetsflöde** med Navigering.

1. Välj **Arkiv** om du vill visa en lista över de arbetsflödesinstanser som har slutförts.

   ![arkiverade instanser](/help/sites-cloud/administering/assets/archived-instances.png)

   >[!NOTE]
   >
   >
   >Avbrottsstatusen betraktas som ett slutfört avbrott eftersom det inträffar som ett resultat av en användaråtgärd, till exempel:
   >
   >* användning av åtgärden **Avsluta**
   >* När en sida, som är underställd ett arbetsflöde, (framtvingas) tas bort, avslutas arbetsflödet.

1. Markera ett specifikt objekt och **Öppna historik** om du vill se mer information:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Åtgärdar fel i arbetsflödesinstansen {#fixing-workflow-instance-failures}

När ett arbetsflöde misslyckas tillhandahåller AEM konsolen **Fel** så att du kan undersöka och vidta lämpliga åtgärder när den ursprungliga orsaken har hanterats:

* **Felinformation**
Öppnar ett fönster för att visa **Felmeddelande**, **Steg och **Felhög** .

* **Öppna historik**
Visar information om arbetsflödeshistoriken.

* **Försök igen** Kör komponentinstansen för skriptsteget igen. Använd kommandot Försök igen när du har åtgärdat orsaken till det ursprungliga felet. Du kan till exempel försöka utföra steget igen när du har åtgärdat ett fel i skriptet som utförs av processteget.
* **Avsluta** arbetsflödet om felet har orsakat en situation som inte kan stämmas av. Arbetsflödet kan t.ex. förlita sig på miljöförhållanden som information i databasen som inte längre är giltig för arbetsflödesinstansen.
* **Avsluta och försök igen** som liknar **Avsluta** förutom att en ny arbetsflödesinstans startas med den ursprungliga nyttolasten, titeln och beskrivningen.

Så här undersöker du fel och sedan återupptar eller avslutar du arbetsflödet:

1. Välj **Verktyg** och sedan **Arbetsflöde** med Navigering.

1. Välj **Fel** om du vill visa listan över arbetsflödesinstanser som inte slutfördes korrekt.
1. Välj ett specifikt objekt och sedan lämplig åtgärd:

![arbetsflödesfel](/help/sites-cloud/administering/assets/workflow-failure.png)

## Vanlig tömning av arbetsflödesinstanser {#regular-purging-of-workflow-instances}

Om du minimerar antalet arbetsflödesinstanser ökas arbetsflödesmotorns prestanda, så att du regelbundet kan rensa avslutade eller pågående arbetsflödesinstanser från databasen.

Konfigurera **Adobe Granite Workflow Renge Configuration** om du vill rensa arbetsflödesinstanser utifrån deras ålder och status. Du kan också rensa arbetsflödesinstanser av alla modeller eller av en viss modell.

Du kan också skapa flera konfigurationer av tjänsten för att rensa arbetsflödesinstanser som uppfyller olika villkor. Skapa till exempel en konfiguration som tömmer instanser av en viss arbetsflödesmodell när de körs mycket längre än förväntat. Skapa en annan konfiguration som tömmer alla slutförda arbetsflöden efter några dagar för att minimera databasens storlek.

Om du vill konfigurera tjänsten kan du konfigurera OSGi-konfigurationsfilerna i [OSGi-konfigurationsfilerna](/help/implementing/deploying/configuring-osgi.md). I följande tabell beskrivs de egenskaper som du behöver för båda metoderna.

>[!NOTE]
>För att lägga till konfigurationen i databasen är tjänst-PID:
>`com.adobe.granite.workflow.purge.Scheduler`
>Eftersom tjänsten är en fabrikstjänst måste namnet på noden `sling:OsgiConfig` ha ett identifierarsuffix, till exempel:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

| Egenskapsnamn (webbkonsol) | OSGi-egenskapsnamn | Beskrivning |
|--- |--- |--- |
| Jobbnamn  | `scheduledpurge.name` | Ett beskrivande namn för den schemalagda rensningen. |
| Arbetsflödesstatus | `scheduledpurge.workflowStatus` | Status för de arbetsflödesinstanser som ska rensas. Följande värden är giltiga:<br><br>- SLUTFÖRT: Slutförda arbetsflödesinstanser rensas.<br>- KÖRNING: Körande arbetsflödesinstanser rensas. |
| Modeller att tömma | `scheduledpurge.modelIds` | ID:t för arbetsflödesmodellerna som ska rensas.<br>ID är sökvägen till modellnoden, till exempel:<br> `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model` <br><br> Ange inget värde för att rensa instanser av alla arbetsflödesmodeller.<br>Om du vill ange flera modeller klickar du på knappen `+` i webbkonsolen. |
| Arbetsflödesålder | `scheduledpurge.daysold` | Åldern på arbetsflödesinstanserna som ska rensas, i dagar. |
| Arbetsflödets nyttolastspaket | `scheduledpurge.purgePackagePayload` | Anger om nyttolastpaketet ska rensas: `true` eller `false`. |


## Ange maximal storlek för inkorgen {#setting-the-maximum-size-of-the-inbox}

Du kan ange den maximala storleken för inkorgen genom att konfigurera **Adobe Granite Workflow Service**, se [Lägga till en OSGi-konfiguration i databasen](/help/implementing/deploying/configuring-osgi.md). I följande tabell beskrivs egenskapen som du konfigurerar.

>[!NOTE]
>För att lägga till konfigurationen i databasen är tjänst-PID:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Egenskapsnamn (webbkonsol) | OSGi-egenskapsnamn |
|---|---|
| Max Inbox Query Size | granite.workflow.inboxQuerySize |

## Använda arbetsflödesvariabler för kundägda datalager {#using-workflow-variables-customer-datastore}

Data som bearbetas av arbetsflöden lagras i Adobe tillhandahållna lagringsutrymme (JCR). Dessa data kan vara känsliga till sin natur. Du kanske vill spara alla användardefinierade metadata/data i ditt egna hanterade lagringsutrymme i stället för det lagringsutrymme som tillhandahålls av Adobe. I dessa avsnitt beskrivs hur du ställer in dessa variabler för extern lagring.

### Ange modellen för extern lagring av metadata {#set-model-for-external-storage}

På arbetsflödesmodellnivån anges en flagga som anger att modellen (och dess körningsinstanser) har extern lagring av metadata. Arbetsflödesvariabler sparas inte i JCR för arbetsflödesinstanser av modeller som är markerade för extern lagring.

Egenskapen *userMetadataPersistenceEnabled* lagras på noden *jcr:content* i arbetsflödesmodellen. Den här flaggan bevaras i arbetsflödets metadata som *cq:userMetaDataCustomPersistenceEnabled*.

Bilden nedan visar hur du anger flaggan i ett arbetsflöde.

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
