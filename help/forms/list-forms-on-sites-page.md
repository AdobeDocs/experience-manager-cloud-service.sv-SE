---
title: Hur listar man blanketter på en Adobe Experience Manager Sites-sida med Forms Portal?
description: Lär dig lista med formulär på en AEM Sites-sida.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 37e3ddd9-b20d-4156-b52e-64e36c455184
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Visa formulär på sidan Webbplatser

Föreställ dig att en användare besöker bankens webbplats i ett formulär där kontot öppnas. Banken använder Forms Portal-komponenten för att hjälpa användarna att snabbt hitta formuläret genom att ange specifika nyckelord eller filtrera efter kategorier som&quot;Nytt konto&quot; eller&quot;Privat bank&quot;, så att användarna enkelt kan hitta formuläret utan att behöva bläddra igenom långa listor.

Med komponenten **Sök och lista** i Forms Portal kan du visa och lista formulär på en webbplatssida. Användarna kan konfigurera och presentera en omfattande lista med formulär som bygger på specifika kriterier för att uppfylla organisationens krav. Anonyma användare kan besöka sidan Sites för att visa och bläddra bland de tillgängliga formulären. De listade formulären kan sorteras i stigande eller fallande ordning med hjälp av det nedrullningsbara alternativet **Sortera efter** i skärmens övre högra hörn.

![Ikonen Sök och visa](assets/search-and-lister-component.png)


## Visa formulär på webbplatssidan

Så här lägger du till portalkomponenten **Sök och visa** på din webbplatssida:

1. Öppna AEM Sites-sidan i **redigeringsläge**.
1. Gå till **[!UICONTROL Page Information]** > **[!UICONTROL Edit Template]**
   ![Redigera mallprincip](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Klicka på **[!UICONTROL Policy]** och markera kryssrutan **[!UICONTROL Search & Lister]** under **[Projektnamn för AEM-arkityp] - Forms och kommunikationsportal**.

   ![Principval](/help/forms/assets/search-lister-enable-policy.png)

1. Klicka på **[!UICONTROL Done]**.
1. Öppna nu AEM Sites-sidan igen i redigeringsläget.
1. Leta reda på det avsnitt i sidredigeraren där du kan lägga till Forms Portal-komponenten.

1. Klicka på ikonen **Lägg till** . Ikonen är ett plustecken (+) som anger att du kan lägga till nya komponenter.

   Om du klickar på ikonen **Lägg till** visas dialogrutan **Infoga ny komponent** som visar olika komponenter som ska infogas.

   >[!NOTE]
   >
   > Du kan också dra och släppa komponenten.

1. Bläddra bland de tillgängliga komponenterna i dialogrutan och välj önskad komponent i listan. Välj till exempel **sök- och listkomponenten** i listan om du vill lägga till Forms Portal-komponenten **Sök och visa**.

   ![Komponenten Sök och visa](/help/forms/assets/add-search-lister.png)

Konfigurera nu egenskaperna för komponenten **Sök och Lister**.

## Förstå egenskaperna för sök- och listkomponenten

Du kan enkelt anpassa komponentegenskaperna **Sök och Lister** med dialogrutan Konfigurera för en smidig användarupplevelse. Konfigurera genom att markera komponenten och sedan välja ikonen ![Konfigurera](assets/configure_icon.png). Dialogrutan **[!UICONTROL Search and Lister]** öppnas.

### Fliken Visa

![Visa flik](/help/forms/assets/search-and-lister-display-tab.png)

1. I **[!UICONTROL Title]** anger du namnet på komponenten Sök efter och visa. Med en titel kan användarna göra en snabb sökning i hela formulärlistan.
1. I listan **[!UICONTROL Layout]** väljer du den layout som ska representera formulären i kort- eller listformatet.
1. Välj **[!UICONTROL Hide Search]** och **[!UICONTROL Hide Sorting]** om du vill dölja sök- och sorteringsfunktionerna.
1. I **[!UICONTROL Tooltip]** anger du det verktygstips som visas när du hovrar över komponenten.

### Fliken Resurser

![Fliken Resurser](/help/forms/assets/search-and-lister-asset-tab.png)

1. På fliken **[!UICONTROL Asset Folder]** anger du den plats från vilken formulären hämtas och visas på sidan.
1. Med **[!UICONTROL Add another location]** kan du konfigurera flera mapplatser.

### Fliken Resultat

![Visa flik](/help/forms/assets/search-and-lister-result-tab.png)

Konfigurera det maximala antalet formulär som ska visas per sida på fliken **[!UICONTROL Results]**. Standardvärdet är åtta formulär per sida.

## Visa formulär på sidan Webbplatser med komponenten Sök och lista

Om du vill visa en lista med formulär använder du Forms Portal-komponenten **Sök efter och visa** . Förhandsgranska AEM Sites-sidan om du vill se en lista över formulär från mappen **Assets** som visas på skärmen. Du kan också söka efter ett specifikt formulär med sökfältet.

![Ikonen Sök och visa](assets/search-and-lister-component.png)

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=sv-SE#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->


## Nästa steg

I nästa artikel kan vi lära oss [hur du sparar formulär som utkast och listar dem på en webbplatssida med hjälp av Forms Portal-komponenten Utkast och överföringar](/help/forms/save-core-component-based-form-as-draft.md).

## Relaterade artiklar

{{forms-portal-see-also}}

## Se även {#see-also}

{{see-also}}
