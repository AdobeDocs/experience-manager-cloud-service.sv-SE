---
title: Hur sparar man huvudkomponentbaserad adaptiv form som ett utkast?
description: Lär dig spara grundkomponentbaserade adaptiva formulär som utkast och skapa en Forms Portal och använda färdiga kärnkomponenter på en AEM Sites-sida.
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---


# Spara grundkomponentbaserad adaptiv form som ett utkast {#save-af-form}

Att spara adaptiva formulär som utkast är en viktig funktion som förbättrar användareffektiviteten och exaktheten. Med den här funktionen kan användare spara förloppet och gå tillbaka för att slutföra uppgifterna senare utan att förlora den angivna informationen. Om du anger ett `save-as-draft`-alternativ får du flexibilitet när det gäller att hantera tiden, minskar risken för dataförlust och bevarar precisionen för inskickade data. Du kan spara formulär som utkast för att slutföra dem senare.

## Överväganden

* [Möjliggör adaptiva kärnkomponenter i Forms för er miljö.](/help/forms/enable-adaptive-forms-core-components.md)

* Kontrollera att kärnkomponenten [är inställd på version 3.0.24 eller senare](https://github.com/adobe/aem-core-forms-components) för att använda den här funktionen.
* Kontrollera att du har ett [Azure-lagringskonto och en åtkomstnyckel](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) för att auktorisera åtkomst till Azure-lagringskontot.

## Spara ett adaptivt formulär som ett utkast

[!DNL Experience Manager Forms] Dataintegrering (data-integration.md) ger [!DNL Azure] lagringskonfiguration för att integrera formulär med [!DNL Azure] lagringstjänster. FDM (Form Data Model) kan användas för att skapa adaptiv Forms som samverkar med [!DNL Azure]-servern för att möjliggöra affärsarbetsflöden.

Om du vill spara formuläret som ett utkast kontrollerar du att du har ett Azure-lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till lagringskontot [!DNL Azure]. Så här sparar du ett formulär som ett utkast:

1. [Skapa Azure Storage-konfiguration](#create-azure-storage-configuration)
1. [Konfigurera Unified Storage Connector för Forms Portal](#configure-usc-forms-portal)
1. [Skapa regel för att spara ett anpassat formulär som ett utkast](#rule-to-save-adaptive-form-as-draft)


### 1. Skapa Azure Storage-konfiguration {#create-azure-storage-configuration}

När du har ett Azure-lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till [!DNL Azure]-lagringskontot utför du följande steg för att skapa Azure Storage-konfigurationen:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.

   ![Val av Azure-lagringskort](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Välj en konfigurationsmapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.

   ![Välj Azure Storage Configuration-mapp](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Ange en rubrik för konfigurationen i fältet **[!UICONTROL Title]**.
1. Ange namnet på lagringskontot [!DNL Azure] i fälten **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access Key]**.

   ![Azure-lagringskonfiguration](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. Klicka på **Spara**.

>[!NOTE]
>
> Du kan hämta **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access Key]** från [Microsoft Azure-portalen](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Konfigurera Unified Storage Connector för Forms Portal {#configure-usc-forms-portal}

När du har skapat Azure Storage-konfigurationen konfigurerar du Unified Storage Connector för Forms Portal enligt följande:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Unified Storage Connector]**.

   ![Enhetlig anslutningslagring](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. I avsnittet **[!UICONTROL Forms Portal]** väljer du **[!UICONTROL Azure]** i listrutan **[!UICONTROL Storage]**.
1. Ange [konfigurationssökvägen för Azure-lagringskonfigurationen](#create-azure-storage-configuration) i fältet **[!UICONTROL Storage Configuration Path]**.

   ![Inställning för enhetlig anslutningslagring](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Välj **[!UICONTROL Save]** och välj sedan **[!UICONTROL Publish]** för att publicera konfigurationen.

### 3. Skapa regler för att spara ett adaptivt formulär som ett utkast {#rule-to-save-adaptive-form-as-draft}

Om du vill spara ett formulär som ett utkast skapar du en **Spara formulär**-regel för en formulärkomponent, till exempel en knapp. När användaren klickar på knappen aktiveras regeln och formuläret sparas som ett utkast. Så här skapar du regeln **Spara formulär** för en knappkomponent:

1. Öppna ett adaptivt formulär i redigeringsläge i instansen Författare.
1. I den vänstra rutan väljer du ikonen ![Komponenter](assets/components_icon.png) och drar komponenten **[!UICONTROL Button]** till formuläret.
1. Markera komponenten **[!UICONTROL Button]** och välj sedan ikonen ![Konfigurera](assets/configure_icon.png).
1. Välj ikonen **[!UICONTROL Edit Rules]** för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create]** om du vill konfigurera och skapa regeln.
1. I avsnittet **[!UICONTROL When]** väljer du **är klickad** och i avsnittet **[!UICONTROL Then]** väljer du alternativet **Spara formulär**.
1. Välj **[!UICONTROL Done]** om du vill spara regeln.

![Skapa regel för knapp](/help/forms/assets/save-form-as-drfat-create-rule.png)

När du förhandsgranskar ett adaptivt formulär, fyller i det och klickar på knappen **Spara formulär** sparas formuläret som ett utkast för senare bruk.

## Komponenten Utkast och inskickat material till en lista över utkast på AEM Sites-sidan

AEM Forms tillhandahåller portalkomponenten **Utkast och inskickningar** direkt för att visa sparade formulär på AEM Sites-sidor. Komponenten **Utkast och inskickningar** visar formulär som har sparats som utkast för senare ifyllnad samt skickade formulär. Den här komponenten ger en personlig upplevelse för alla inloggade användare genom att lista de utkast och inskickade data som rör den adaptiva Forms som har skapats av användaren.

Du kan använda färdiga Forms Portal-komponenter för att lista formulärutkast på AEM Sites-sidan. Utför följande steg för att använda portalkomponenten **Utkast och överföringar**:

1. [Aktivera Forms Portal-komponenten för utkast och inskickat material](#enable-component)
2. [Lägg till komponenten Utkast och överföringar på AEM Sites-sidan](#Add-drafts-submissions-component)
3. [Konfigurera komponenten Utkast och överföringar](#configure-drafts-submissions-component)

### 1. Aktivera Forms Portal-komponenten för utkast och inskickat material{#enable-component}

Så här aktiverar du komponenten **[!UICONTROL Drafts & Submissions]** i mallprincipen:

1. Öppna AEM Sites-sidan i **redigeringsläge**.
1. Gå till **[!UICONTROL Page Information]** > **[!UICONTROL Edit Template]**
   ![Redigera mallprincip](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Klicka på **[!UICONTROL Policy]** och markera kryssrutan **[!UICONTROL Drafts & Submissions]** under **[AEM Archetype Project Name] - Forms and Communications Portal**.

   ![Principval](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Klicka på **[!UICONTROL Done]**.

När en portalkomponent är aktiverad kan du använda den i författarinstansen av din AEM Sites-sida.

### 2. Lägg till komponenten Utkast &amp; Submissions (Utkast &amp; överföringar) på AEM Sites-sidan{#Add-drafts-submissions-component}

Du kan skapa och anpassa Forms Portal på webbplatser som skapats med AEM genom att lägga till och konfigurera portalkomponenterna. Kontrollera att komponenten [Utkast och överföringar är aktiverad](#enable-component) innan du använder dem på AEM Sites-sidan.

Om du vill lägga till en komponent drar och släpper du komponenten från komponentrutan **Utkast och överföringar** till layoutbehållaren på sidan. Du kan också välja ikonen Lägg till i layoutbehållaren och lägga till komponenten från dialogrutan **[!UICONTROL Insert New Component]** .

![Lägg till utkast och skicka-komponent](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. Konfigurera komponenten Utkast och överföringar {#configure-drafts-submissions-component}

Komponenten **Utkast och inskickningar** visar formulär som har sparats som utkast för att fylla i senare och skickade formulär. Så här konfigurerar du **Utkast och överföringar**:
1. Markera komponenten **Utkast och överföringar**.
1. Klicka på ikonen ![Konfigurera](assets/configure_icon.png) så visas dialogrutan.
1. Ange följande i dialogrutan **[!UICONTROL Drafts and Submissions]**:
   * **Titel** Om du vill identifiera en komponent på en webbplatssida visas titeln som standard ovanpå komponenten.
   * **Typ**: För att ange formulärlistan som utkast eller skickade formulär.
   * **Layout**: Om du vill visa en lista med formulärutkast eller skickade formulär i kort- eller listformat.

   ![Egenskaper för utkast och skicka komponent](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. Klicka på **Klar**.

När **[!UICONTROL Select Type]** har valts som **Utkast av Forms** visas de formulär som har sparats som utkast:
![Ikonen Utkast ](assets/drafts-component.png)

När **[!UICONTROL Select Type]** har valts som **Skickat Forms** visas de skickade formulären:

![Ikonen Skicka](assets/submission-listing.png)

Du kan öppna formuläret genom att klicka på respektive formulär.

<!--

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

## Se även {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->
