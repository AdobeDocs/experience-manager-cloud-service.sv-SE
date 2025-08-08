---
title: Hur integrerar man AEM arbetsflöde med ett adaptivt formulär?
description: Utforska processen med automatisk start av arbetsflöden med AEM Forms Submit Action.
keywords: AEM Workflow, Integrated Adaptive Form with AEM workflow, Invoke AEM workflow Submit Action
feature: Adaptive Forms, Core Components
exl-id: b7788e3d-acd8-4867-b232-f9767cf6b2f5
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 0%

---

# Integrera AEM adaptiva blanketter med AEM Workflow: Effektivare affärsprocesser

Åtgärden **[!UICONTROL Invoke an AEM Workflow]** kopplar ett anpassat formulär till ett AEM-arbetsflöde. När ett formulär skickas startar det associerade arbetsflödet automatiskt på författarinstansen. Du kan spara datafiler, bilagor och postdokument på arbetsflödets eller en variabels nyttolastplats. Om arbetsflödet är markerat för extern datalagring och konfigurerat för en extern datalagring är endast variabelalternativet tillgängligt. Du kan välja i listan över variabler som är tillgängliga för arbetsflödesmodellen. Om arbetsflödet markeras för extern datalagring i ett senare skede och inte när arbetsflödet skapas, kontrollerar du att de variabelkonfigurationer som krävs finns på plats.

>[!NOTE]
>
>  Lär dig hur du [skapar en arbetsflödesmodell](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE#extending-aem) för att definiera serien med steg som körs när en användare startar arbetsflödet. Du kan också definiera modellegenskaper, t.ex. om arbetsflödet är tillfälligt eller använder flera resurser.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

## Fördelar

Några av fördelarna med att integrera AEM arbetsflöde med Adaptive Forms är:

* Integrering med AEM Workflow möjliggör automatisering av komplexa affärsprocesser som innefattar inlämning av blanketter.
* AEM Workflow har stöd för villkorsstyrd logik, vilket möjliggör dynamiska beslut baserade på formulärdata eller externa faktorer.
* AEM Workflow dirigerar uppgifter baserat på fördefinierade regler och villkor och ser till att uppgifter tilldelas rätt personer eller grupper.

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## Integrera AEM Workflow med Adaptive Forms {#steps-to-integrate-workflow-with-af}

>[!BEGINTABS]

>[!TAB Foundation Component]

Så här ställer du in automatiserad process med [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE#extending-aem) för ett adaptivt formulär baserat på Foundation-komponenter:

1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. Välj **[!UICONTROL Submit Action]** Skicka åtgärd **som** i listrutan **[!UICONTROL Invoke an AEM workflow]**.
1. Välj arbetsflödesmodell i listrutan **[!UICONTROL Workflow Model]**.
1. Välj ett alternativ i listrutan **[!UICONTROL Store Data file using]**.

   **Datafil**: Den innehåller data som har skickats till det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Data File Path]** för att ange filens namn och sökväg i förhållande till nyttolasten. Sökvägen `/addresschange/data.xml` skapar till exempel en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också ange att bara `data.xml` ska skicka skickade data utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

   ![invoke-workflow-fc](/help/forms/assets/invoke-workflow-fc.png)

1. Välj ett alternativ i listrutan **[!UICONTROL Store attachments using]**.

   **Bifogade filer**: Du kan använda alternativet **[!UICONTROL Attachment Path]** för att ange mappnamnet för att lagra de bifogade filer som överförts till det anpassade formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj ett alternativ i listrutan **[!UICONTROL Documents of record using]**.

   **Postdokument**: Det innehåller det postdokument som genererats för det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Document of Record Path]** för att ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Sökvägen `/addresschange/DoR.pdf` skapar till exempel en mapp med namnet `addresschange` relativt till nyttolasten och placerar `DoR.pdf` relativt nyttolasten. Du kan även ange att bara `DoR.pdf` ska spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.
1. Klicka på **[!UICONTROL Done]**.

   >[!NOTE]
   >
   > Läs mer om [Forms-orienterade AEM-arbetsflöden - stegreferens för att automatisera affärsprocesser](/help/forms/aem-forms-workflow-step-reference.md).

>[!TAB Kärnkomponent]

Så här ställer du in automatiserad process med [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE#extending-aem) för ett adaptivt formulär baserat på kärnkomponenter:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. Välj **[!UICONTROL Submit Action]** i listrutan **[!UICONTROL Invoke an AEM Workflow]**.

   ![Åtgärdskonfiguration för Skicka e-post](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Välj arbetsflödesmodell i listrutan **[!UICONTROL Workflow Model]**.
1. Välj ett alternativ i listrutan **[!UICONTROL Store Data file using]**.

   **Datafil**: Den innehåller data som har skickats till det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Data File Path]** för att ange filens namn och sökväg i förhållande till nyttolasten. Sökvägen `/addresschange/data.xml` skapar till exempel en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också ange att bara `data.xml` ska skicka skickade data utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj ett alternativ i listrutan **[!UICONTROL Store attachments using]**.

   **Bifogade filer**: Du kan använda alternativet **[!UICONTROL Attachment Path]** för att ange mappnamnet för att lagra de bifogade filer som överförts till det anpassade formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj ett alternativ i listrutan **[!UICONTROL Documents of record using]**.

   **Postdokument**: Det innehåller det postdokument som genererats för det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Document of Record Path]** för att ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Sökvägen `/addresschange/DoR.pdf` skapar till exempel en mapp med namnet `addresschange` relativt till nyttolasten och placerar `DoR.pdf` relativt nyttolasten. Du kan även ange att bara `DoR.pdf` ska spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.
1. Klicka på **[!UICONTROL Done]**.

   >[!NOTE]
   >
   > Läs mer om [Forms-orienterade AEM-arbetsflöden - stegreferens för att automatisera affärsprocesser](/help/forms/aem-forms-workflow-step-reference.md).

>[!TAB Universell redigerare]

Så här ställer du in automatiserad process med [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=sv-SE#extending-aem) för ett adaptivt formulär som har skapats i den universella redigeraren:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.

1. Klicka på fliken **Skicka** och välj åtgärden **[!UICONTROL Invoke an AEM Workflow]** Skicka.


   ![Åtgärdskonfiguration för Skicka e-post](/help/forms/assets/invoke-service-ue.png)

1. Välj arbetsflödesmodell i listrutan **[!UICONTROL Workflow Model]**.
1. Välj ett alternativ i listrutan **[!UICONTROL Store Data file using]**.

   **Datafil**: Den innehåller data som har skickats till det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Data File Path]** för att ange filens namn och sökväg i förhållande till nyttolasten. Sökvägen `/addresschange/data.xml` skapar till exempel en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också ange att bara `data.xml` ska skicka skickade data utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj ett alternativ i listrutan **[!UICONTROL Store attachments using]**.

   **Bifogade filer**: Du kan använda alternativet **[!UICONTROL Attachment Path]** för att ange mappnamnet för att lagra de bifogade filer som överförts till det anpassade formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

1. Välj ett alternativ i listrutan **[!UICONTROL Documents of record using]**.

   **Postdokument**: Det innehåller det postdokument som genererats för det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Document of Record Path]** för att ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Sökvägen `/addresschange/DoR.pdf` skapar till exempel en mapp med namnet `addresschange` relativt till nyttolasten och placerar `DoR.pdf` relativt nyttolasten. Du kan även ange att bara `DoR.pdf` ska spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.
1. Klicka på **[!UICONTROL Done]**.

   >[!NOTE]
   >
   > Läs mer om [Forms-orienterade AEM-arbetsflöden - stegreferens för att automatisera affärsprocesser](/help/forms/aem-forms-workflow-step-reference.md).

>[!ENDTABS]

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Relaterade artiklar

{{af-submit-action}}
