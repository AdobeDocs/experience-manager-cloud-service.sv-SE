---
title: Hur konfigurerar jag USC (Unified Storage Connector) för AEM Forms?
description: Lär dig hantera USC (Unified Storage Connector) för AEM Forms. Använd USC (Unified Storage Connector) för att ansluta AEM Forms till externa datalagringsplatser.
role: Admin, Developer, User
feature: Adaptive Forms, Workflow
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: c17e4e70fa8cec176c908983230b03f2899bc1ca
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Hantera USC (Unified Storage Connector) för AEM Forms {#manage-unified-storage-connector}

Du kan använda USC (Unified Storage Connector) för att ansluta AEM Forms till externa datalagringsplatser.

Du kan till exempel fylla i värden för fält i ett anpassat formulär och skicka det till ett AEM-arbetsflöde. Du kan konfigurera AEM-arbetsflöden ytterligare så att data lagras i en extern lagringsplats, till exempel Microsoft Azure-lagringsservern. Använd USC (Unified Storage Connector) för att skapa en anslutning mellan AEM-arbetsflöden och den externa lagringen.

## Koppla AEM-arbetsflöden till en Microsoft Azure-lagringsserver {#connect-workflows-with-azure}

Skapa en Azure-lagringskonfiguration och referera till den konfigurationen med hjälp av USC (Unified Storage Connector). Du kan sedan konfigurera AEM Workflow-modeller så att datalagringen görs externt för att ansluta dem till en Azure-lagringsserver.

### Skapa lagringskonfiguration för [!DNL Azure] {#create-azure-storage-configuration}

Innan du utför de här stegen måste du se till att du har ett [!DNL Azure]-lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till lagringskontot [!DNL Azure].

Så här skapar du en [!DNL Azure]-lagringskonfiguration:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. Välj en mapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.
1. Ange en rubrik för konfigurationen i fältet **[!UICONTROL Title]**.
1. Ange namnet på lagringskontot [!DNL Azure] i fältet **[!UICONTROL Azure Storage Account]**.
1. Ange nyckeln för åtkomst till Azure-lagringskontot i fältet **[!UICONTROL Azure Access Key]** och välj **[!UICONTROL Save]**.

### Konfigurera USC (Unified Storage Connector) för AEM-arbetsflöden {#configure-unified-storage-connector-workflows}

Utför följande steg för att konfigurera USC (Unified Storage Connector) för AEM-arbetsflöden:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Unified Storage Connector]**.

1. Välj **[!UICONTROL Azure]** i listrutan Lagring i avsnittet **[!UICONTROL Workflow]**.
1. Ange [konfigurationssökvägen för Azure-lagringskonfigurationen](#create-azure-storage-configuration) i fältet **[!UICONTROL Storage Configuration Path]**.
1. Välj **[!UICONTROL Publish]** och välj sedan **[!UICONTROL Save]** för att spara konfigurationen.

### Konfigurera en AEM Workflow-modell för extern datalagring {#configure-workflow-external-data-storage}

Utför följande steg för att konfigurera en AEM Workflow-modell för en extern datalagring:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Välj ett modellnamn och välj **[!UICONTROL Edit]**.
1. Välj ikonen Sidinformation och välj **[!UICONTROL Open Properties]**.
1. Välj **[!UICONTROL Externalize workflow data storage]**.
1. Välj **[!UICONTROL Save & Close]** om du vill spara egenskaperna.

>[!NOTE]
>
>Alternativen för att spara steget Tilldela uppgift som utkast och för att hämta historiken för steget Tilldela uppgift inaktiveras när du konfigurerar en arbetsflödesmodell för AEM för extern datalagring.

### Riktlinjer för AEM Workflows för extern datalagring {#guidelines-workflows-external-data-storage}

Nedan följer några riktlinjer när du använder AEM Workflows och lagrar data till externa datalager, som Microsoft Azure-lagringsserver:

* Använd variabler för att lagra data när du definierar in- och utdatafiler och bilagor i arbetsflödesmodellstegen. Välj inte alternativen **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]**. Alternativen **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]** visas inte automatiskt när du [konfigurerar en AEM Workflow-modell för extern datalagring](#configure-workflow-external-data-storage).

* Använd variabler för att lagra datafiler och bilagor när du skickar ett anpassat formulär till ett AEM-arbetsflöde. Välj inte alternativet **[!UICONTROL Relative to Payload]** när du skickar ett anpassat formulär till ett AEM-arbetsflöde. Alternativet **[!UICONTROL Relative to Payload]** visas inte automatiskt när du [konfigurerar en AEM Workflow-modell för extern datalagring](#configure-workflow-external-data-storage).

* Använd inte ett anpassat AEM Workflow-steg i en arbetsflödesmodell för att lagra data i CRX DE-databasen.

* När du [konfigurerar en AEM-arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage) ska du inte skapa anpassade kolumner för AEM Inbox eftersom värdena för de anpassade kolumnerna inte hämtas om arbetsobjektet i AEM Inbox tillhör ett arbetsflöde som är markerat för extern lagring.

>[!MORELIKETHIS]
>
>* [Konfigurera datakällor för AEM Forms](/help/forms/configure-data-sources.md)
>* [Konfigurera Azure-lagring för AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrera Microsoft Dynamics 365](/help/forms/configure-msdynamics.md)
>  [Lägg till Forms Portal på en AEM Sites-sida &#x200B;](/help/forms/configure-forms-portal.md)
