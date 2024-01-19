---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: AEM arbetsflöde, Integrera anpassat formulär med AEM arbetsflöde, Anropa AEM Skicka åtgärd
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Integrera AEM anpassat formulär med AEM arbetsflöde: Effektivisera affärsprocesser

The **[!UICONTROL Invoke an AEM Workflow]** Åtgärden Skicka associerar ett anpassat formulär med ett AEM. När ett formulär skickas startar det associerade arbetsflödet automatiskt på författarinstansen. Du kan spara datafiler, bilagor och postdokument på arbetsflödets eller en variabels nyttolastplats. Om arbetsflödet är markerat för extern datalagring och konfigurerat för en extern datalagring är endast variabelalternativet tillgängligt. Du kan välja i listan över variabler som är tillgängliga för arbetsflödesmodellen. Om arbetsflödet markeras för extern datalagring i ett senare skede och inte när arbetsflödet skapas, kontrollerar du att de variabelkonfigurationer som krävs finns på plats.

>[!NOTE]
>
>  Lär dig hur [skapa en arbetsflödesmodell](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem) för att definiera serie steg som körs när en användare startar arbetsflödet. Du kan också definiera modellegenskaper, t.ex. om arbetsflödet är tillfälligt eller använder flera resurser.

AEM as a Cloud Service erbjuder olika åtgärder för att skicka in formulär. Du kan läsa mer om de här alternativen i [Inlämningsåtgärd för anpassat formulär](/help/forms/configure-submit-actions-core-components.md)  artikel.

## Fördelar

Några av fördelarna med att integrera AEM arbetsflöden med Adaptive Forms är:

* AEM arbetsflödesintegration möjliggör automatisering av komplexa affärsprocesser som innefattar inskickning av blanketter.
* AEM Workflow har stöd för villkorsstyrd logik, vilket möjliggör dynamiska beslut baserade på formulärdata eller externa faktorer.
* AEM arbetsflöde dirigerar uppgifter baserat på fördefinierade regler och villkor, och ser till att uppgifter tilldelas rätt personer eller grupper.

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## Integrera AEM arbetsflöde med adaptiv Forms {#steps-to-integrate-workflow-with-af}

Konfigurera automatiserad process med [AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem) för ett adaptivt formulär utför du följande steg:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på  **[!UICONTROL Submission]** -fliken.
1. Från **[!UICONTROL Submit Action]** nedrullningsbar lista, välja **[!UICONTROL Invoke an AEM Workflow]** .
   ![Åtgärdskonfiguration för Skicka e-post](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Välj arbetsflödesmodell från **[!UICONTROL Workflow Model]** listruta.
1. Välj alternativ på menyn **[!UICONTROL Store Data file using]** listruta.

   **Datafil**: Den innehåller data som skickats till den adaptiva formen. Du kan använda **[!UICONTROL Data File Path]** om du vill ange filens namn och sökväg i förhållande till nyttolasten. Till exempel `/addresschange/data.xml` sökväg skapar en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också bara ange `data.xml` om du bara vill skicka skickade data utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj alternativ på menyn **[!UICONTROL Store attachments using]** listruta.

   **Bifogade filer**: Du kan använda **[!UICONTROL Attachment Path]** om du vill ange mappnamnet för lagring av de bilagor som överförts till det adaptiva formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj alternativ på menyn **[!UICONTROL Documents of record using]** listruta.

   **Dokument för registrering**: Det innehåller det dokument som genererats för det adaptiva formuläret. Du kan använda **[!UICONTROL Document of Record Path]** om du vill ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Till exempel `/addresschange/DoR.pdf` sökväg skapar en mapp med namnet `addresschange` i förhållande till nyttolasten och placerar `DoR.pdf` i förhållande till nyttolast. Du kan också bara ange `DoR.pdf` om du bara vill spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.
1. Klicka på **[!UICONTROL Done]**.

>[!NOTE]
>
> Läs mer om [Forms-centrerade AEM - stegvis referens för automatisering av affärsprocesser](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Relaterade artiklar

{{af-submit-action}}