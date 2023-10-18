---
title: Vilka användargrupper finns tillgängliga direkt i AEM Forms as a Cloud Service?
description: Lista över användargrupper som inte ingår i rutan och behörigheter som tilldelats varje grupp
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: a942e87a33775851631a1fe123fa3e8d2686bb30
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 4%

---

# Grupper och behörigheter {#aem-forms-on-osgi-groups-and-privileges}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html) |
| AEM as a Cloud Service | Den här artikeln |

Du kan [skapa grupper](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) och tilldela profiler och [användare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) till grupperna. Dessa profiler styr behörigheter för de användare som ingår i gruppen.

När du har konfigurerat [!DNL AEM Forms] as a Cloud Service, de grupper som listas i tabellen nedan, t.ex. [!DNL forms-users] och blankettkonstruktörer kan automatiskt tilldelas

<table>
 <tbody>
  <tr>
   <td>Grupp</td> 
   <td>Behörigheter</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Skapa, förhandsgranska, publicera och skicka Adaptiv Forms</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>Överföra resurser till en AEM instans</li> 
     <li>Skapa teman</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>Create, preview, publish, and submit Adaptive Forms</li> 
     <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> 
     <li>Upload assets including scripts</li> 
     <li>Create themes</li> 
     <li>Import packages containing XDP</li> 
    </ul> </td> 
  </tr>
 <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Skapa och förhandsgranska Adaptiv Forms <!-- or interactive communications --> mallar</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>Skapa och ändra en formulärdatamodell</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>Hantera arbetsflödesprogram</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## Se även

* [Gå med i en Cloud Service-miljö](/help/forms/setup-forms-cloud-service.md)
* [Konfigurera en lokal utvecklingsmiljö](/help/forms/setup-local-development-environment.md)
* [Migrera från AEM 6.5 Forms till Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Skapa ett fristående anpassat formulär](/help/forms/creating-adaptive-form-core-components.md)
* [Lägg till ett anpassat formulär på AEM Sites-sidan](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

<!--

>[!MORELIKETHIS]
>
>* [Use AEM Forms workflow for business process automation](/help/forms/aem-forms-workflow.md)

-->