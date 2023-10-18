---
title: Hur ansluter AEM adaptiva formulär till Microsoft® SharePoint List?
description: Koppla ett anpassat formulär till Microsoft® SharePoint List. Lär dig hur du konfigurerar Microsoft® SharePoint-listan och skapar en formulärdatamodell med hjälp av konfigurationen. Dessutom får du lära dig att integrera FDM med ditt adaptiva formulär.
role: User, Developer
keywords: ansluta AEM adaptiva blanketter till Microsoft SharePoint List, ansluta adaptiva blanketter till Microsoft SharePoint List, integrera AEM adaptiva blanketter i Microsoft SharePoint List, integrera adaptiva blanketter till Microsoft SharePoint List, skicka data från ett adaptivt formulär till SharePoint List, skicka AEM arbetsflöde till SharePoint List.
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Ansluta ett anpassat formulär till Microsoft® SharePoint List

<span class="preview"> Det här är en förhandsversion som du kommer åt via vår [kanal för förhandsversion](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

**Microsoft® SharePoint**: Microsoft® SharePoint möjliggör samarbete genom att tillhandahålla dynamiska och effektiva gruppwebbplatser för alla team, avdelningar och avdelningar. Det används för att lagra, ordna, dela och få åtkomst till information från alla enheter med valfri webbläsare, till exempel Microsoft® Edge, Internet Explorer, Chrome eller Firefox. De två huvudkomponenterna i **Microsoft® SharePoint** är:

* **Microsoft® SharePoint Document Library**: Microsoft® SharePoint Document Library visar en lista med filer och mappar tillsammans med nyckelinformation, t.ex. det senaste ändringsdatumet och filens ägare. Den här funktionen gör det enkelt att ordna och navigera i filer.
Instruktioner om hur du integrerar en **Microsoft® SharePoint Document Library** med en adaptiv form, se [Inlämningsåtgärd för anpassat formulär](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) artikel.

* **Microsoft® SharePoint List**: Microsoft® SharePoint List är en samling data. Du kan lägga till kolumner för olika typer av data och skapa vyer för att visa data effektivt. Du kan enkelt gruppera, filtrera, sortera och formatera listorna.

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## Krav för att ansluta ett adaptivt formulär till Microsoft® SharePoint List {#prerequisites}

Utför följande steg innan du ansluter ett adaptivt formulär till Microsoft® SharePoint List:

1. [Konfigurera Microsoft® SharePoint List](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [Skapa en formulärdatamodell med Microsoft® SharePoint List-konfiguration](/help/forms/create-form-data-models.md)
1. [Konfigurera formulärdatamodellen för att hämta och skicka data](/help/forms/work-with-form-data-model.md#configure-services)
1. [Skapa ett adaptivt formulär](/help/forms/creating-adaptive-form-core-components.md)

Nu kan du:

* [Koppla Microsoft® SharePoint List till ett adaptivt formulär](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [Koppla Microsoft® SharePoint List till ett AEM arbetsflöde](#connect-sharepoint-list-workflow)

## Ansluta ett anpassat formulär till Microsoft® SharePoint List {#connect-af-sharepoint-list}

Integrera Microsoft® SharePoint List med ditt adaptiva formulär [konfigurera ett adaptivt formulär att använda en formulärdatamodell](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

När du har konfigurerat ett adaptivt formulär att använda en formulärdatamodell kan du:

* [Konfigurera åtgärden Skicka med en formulärdatamodell](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [Konfigurera regelredigeraren för att anropa en formulärdatamodell](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## Koppla Microsoft® SharePoint List till ett AEM arbetsflöde {#connect-sharepoint-list-workflow}

Så här integrerar du Microsoft® SharePoint List i ett AEM arbetsflöde:

1. [Skapa ett arbetsflöde för att anropa en formulärdatamodell](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)

   <!--
    To create a new workflow with the editor, perform the following steps:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [Konfigurera åtgärden Skicka för att starta ett AEM arbetsflöde](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


Lär dig hur [använd AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) för att samarbeta, hantera och bearbeta innehåll i en adaptiv form.

## Bästa praxis {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft® SharePoint List rather than Microsoft® SharePoint Document Library. -->
* I Microsoft® SharePoint List stöds inte följande kolumntyper:
   * bildkolumn
   * metadatakolumn
   * personkolumn
   * extern datakolumn

## Se även {#see-also}

* [Skapa ett Core-Component-baserat adaptivt formulär](/help/forms/creating-adaptive-form-core-components.md)
* [Konfigurera datakällor](/help/forms/configuring-submit-actions.md)
* [Skapa formulärdatamodell](/help/forms/create-form-data-models.md)
* [Använd Forms-centrerade AEM - stegvis referens för att automatisera affärsprocesser](/help/forms/aem-forms-workflow-step-reference.md)

## Ytterligare information

* [Skapa eller lägga till ett adaptivt formulär på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Bädda in ett anpassat formulär på en AEM Sites-sida](/help/forms/embed-adaptive-form-aem-sites.md)
* [Skapa, använda och anpassa teman i ett adaptivt formulär](/help/forms/using-themes-in-core-components.md)

>[!MORELIKETHIS]
>
>* [Skapa en anpassad inskickningsåtgärd för Adaptiv Forms](/help/forms/custom-submit-action-form.md)





