---
title: Forms-centrerade arbetsflöden på OSGi | Hantera användardata
seo-title: Forms-centric workflows on OSGi | Handling user data
description: Forms-centrerade arbetsflöden på OSGi | Hantera användardata
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---


# Forms-centrerade arbetsflöden på OSGi | Hantera användardata {#forms-centric-workflows-on-osgi-handling-user-data}

Med Forms-centrerade AEM kan ni automatisera Forms-centrerade affärsprocesser. Arbetsflöden består av en serie steg som körs i en ordning som anges i den associerade arbetsflödesmodellen. Varje steg utför en specifik åtgärd, till exempel att tilldela en uppgift till en användare eller skicka ett e-postmeddelande. Arbetsflöden kan samverka med resurser i databasen, användarkonton och tjänster. Därför kan arbetsflöden samordna komplicerade aktiviteter som berör någon aspekt av Experience Manager.

Ett formulärbaserat arbetsflöde kan aktiveras eller startas på något av följande sätt:

* Skicka ett program från AEM Inbox
* Skicka en ansökan från AEM [!DNL Forms] App
* Skicka ett anpassat formulär
* Använda en bevakad mapp
* Skicka ett interaktivt meddelande eller ett brev

Mer information om arbetsflöden och funktioner för Forms-centrerade AEM finns i [Forms-centrerat arbetsflöde i OSGi](aem-forms-workflow.md).

## Användardata och datalager {#user-data-and-data-stores}

När ett arbetsflöde aktiveras genereras en nyttolast automatiskt för arbetsflödesinstansen. Varje arbetsflödesinstans tilldelas ett unikt instans-ID och ett tillhörande nyttolast-ID. Nyttolasten innehåller databasplatserna för användar- och formulärdata som är associerade med en arbetsflödesinstans. Dessutom lagras utkast och historiska data för en arbetsflödesinstans även i AEM.

Standarddatabasplatserna där nyttolast, utkast och historik för en arbetsflödesinstans finns är följande:

>[!NOTE]
>
>Du kan konfigurera olika platser för lagring av nyttolast, utkast och historikdata när du skapar ett arbetsflöde eller program. Granska arbetsflödet för att identifiera de platser där data lagras i ett arbetsflöde eller i ett program.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Arbetsflöde <br /> instance</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Nyttolast</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Utkast</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>Historik</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Du kan komma åt och ta bort användardata från en arbetsflödesinstans i databasen. För att uppnå detta måste du känna till instans-ID:t för arbetsflödesinstansen som är associerad med användaren. Du kan hitta instans-ID för en arbetsflödesinstans genom att använda användarnamnet för den användare som initierade arbetsflödesinstansen eller som är den aktuella tilldelaren för arbetsflödesinstansen.

Du kan dock inte identifiera eller så kan resultatet vara tvetydigt när du identifierar arbetsflöden som är kopplade till en initierare i följande scenarier:

* **Arbetsflöde som aktiveras via en bevakad mapp**: Det går inte att identifiera en arbetsflödesinstans med dess initierare om arbetsflödet aktiveras av en bevakad mapp. I det här fallet kodas användarinformationen i de lagrade data.
* **Arbetsflöde initierat från publiceringens AEM**: Alla arbetsflödesinstanser skapas med en tjänstanvändare när adaptiv Forms, interaktiv kommunikation eller brev skickas från AEM publiceringsinstans. I dessa fall hämtas inte användarnamnet för den inloggade användaren i arbetsflödets instansdata.

### Åtkomst till användardata {#access}

Så här identifierar och får du åtkomst till användardata som lagras för en arbetsflödesinstans:

1. AEM författarinstans går du till `https://'[server]:[port]'/crx/de` och navigera till **[!UICONTROL Tools > Query]**.

   Välj **[!UICONTROL SQL2]** från **[!UICONTROL Type]** nedrullningsbar meny.

1. Utför någon av följande frågor beroende på vilken information som är tillgänglig:

   * Kör följande om arbetsflödesinitieraren är känd:

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Gör följande om användaren vars data du hittar är den som är tilldelad det aktuella arbetsflödet:

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   Frågan returnerar platsen för alla arbetsflödesinstanser för den angivna arbetsflödesinitieraren eller den aktuella arbetsflödestilldelaren.

   Följande fråga returnerar till exempel två arbetsflödesinstanser från `/var/workflow/instances` nod vars arbetsflödesinitierare är `srose`.

   ![workflow-instance](assets/workflow-instance.png)

1. Gå till en arbetsflödesinstanssökväg som returneras av frågan. Egenskapen status visar arbetsflödesinstansens aktuella status.

   ![status](assets/status.png)

1. I arbetsflödesinstansnoden navigerar du till `data/payload/`. The `path` egenskapen lagrar sökvägen till arbetsflödesinstansens nyttolast. Du kan navigera till sökvägen för att komma åt data som lagras i nyttolasten.

   ![nyttload-path](assets/payload-path.png)

1. Navigera till platserna för utkast och historik för arbetsflödesinstansen.

   Till exempel:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Upprepa steg 3-5 för alla arbetsflödesinstanser som returneras av frågan i steg 2.

   >[!NOTE]
   >
   >AEM [!DNL Forms] lagras data även i offlineläge. Det är möjligt att data för en arbetsflödesinstans lagras lokalt på enskilda enheter och skickas till [!DNL Forms] när programmet synkroniseras med servern.

### Ta bort användardata {#delete-user-data}

Du måste vara AEM administratör för att kunna ta bort användardata från arbetsflödesinstanser genom att utföra följande steg:

1. Följ instruktionerna i [Åtkomst till användardata](forms-workflow-osgi-handling-user-data.md#access) och notera följande:

   * Sökvägar till arbetsflödesinstanser som är associerade med användaren
   * Status för arbetsflödesinstanserna
   * Sökvägar till nyttolaster för arbetsflödesinstanser
   * Banor till utkast och historik för arbetsflödesinstanser

1. Utför det här steget för arbetsflödesinstanser i **KÖRS**, **UPPHÄVD**, eller **STAL** status:

   1. Gå till `https://'[server]:[port]'/aem/start.html` och logga in med administratörsautentiseringsuppgifter.
   1. Navigera till **[!UICONTROL Tools > Workflow> Instances]**.
   1. Välj relevanta arbetsflödesinstanser för användaren och tryck på **[!UICONTROL Terminate]** för att avsluta instanser som körs.

      Mer information om hur du arbetar med arbetsflödesinstanser finns i [Administrera arbetsflödesinstanser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#authoring).

1. Gå till [!DNL CRXDE Lite] konsol, navigera till nyttolastsökvägen för en arbetsflödesinstans och ta bort `payload` nod.
1. Navigera till utkastssökvägen för en arbetsflödesinstans och ta bort `draft` nod.
1. Navigera till historiksökvägen för en arbetsflödesinstans och ta bort `history` nod.
1. Navigera till arbetsflödesinstanssökvägen för en arbetsflödesinstans och ta bort `[workflow-instance-ID]` nod för arbetsflödet.

   >[!NOTE]
   >
   >Om du tar bort arbetsflödesinstansnoden tas arbetsflödesinstansen bort för alla arbetsflödesdeltagare.

1. Upprepa steg 2-6 för alla arbetsflödesinstanser som identifieras för en användare.
1. Identifiera och ta bort offlineutkast och skicka data från AEM [!DNL Forms] app-outbox för arbetsflödesdeltagare för att undvika att skickas till servern.

Du kan också använda API:er för att komma åt och ta bort noder och egenskaper. Mer information finns i följande dokument.

* [Så här programmässigt kommer du åt AEM JCR](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/access-jcr.html?lang=en#platform)
* [Tar bort noder och egenskaper](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API-referens](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

