---
title: Hur konfigurerar jag USC (Unified Storage Connector) för AEM Forms?
description: Lär dig hantera USC (Unified Storage Connector) för AEM Forms. Använd USC (Unified Storage Connector) för att ansluta AEM Forms till externa datalagringsplatser.
role: Admin, Developer, User
feature: Adaptive Forms, Workflow
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Hantera USC (Unified Storage Connector) för AEM Forms {#manage-unified-storage-connector}

Du kan använda USC (Unified Storage Connector) för att ansluta AEM Forms till externa datalagringsplatser.

Du kan till exempel fylla i värden för fält i ett anpassat formulär och skicka det till ett AEM arbetsflöde. Du kan konfigurera AEM arbetsflöden ytterligare för att lagra data i en extern lagringsplats, till exempel Microsoft Azure-lagringsservern. Använd USC (Unified Storage Connector) för att skapa en anslutning mellan AEM arbetsflöden och det externa lagringsutrymmet.

## Ansluta AEM arbetsflöden med en Microsoft Azure-lagringsserver {#connect-workflows-with-azure}

Skapa en Azure-lagringskonfiguration och referera till den konfigurationen med hjälp av USC (Unified Storage Connector). Du kan sedan konfigurera AEM arbetsflödesmodeller för att externalisera datalagringen för att ansluta dem till en Azure-lagringsserver.

### Skapa [!DNL Azure] lagringskonfiguration {#create-azure-storage-configuration}

Innan du utför dessa steg måste du se till att du har en [!DNL Azure] lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till [!DNL Azure] lagringskonto.

Så här skapar du en [!DNL Azure] lagringskonfiguration:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. Välj en mapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.
1. Ange en rubrik för konfigurationen i dialogrutan **[!UICONTROL Title]** fält.
1. Ange namnet på [!DNL Azure] lagringskonto i **[!UICONTROL Azure Storage Account]** fält.
1. Ange nyckeln för åtkomst till Azure-lagringskontot i **[!UICONTROL Azure Access Key]** fält och markera **[!UICONTROL Save]**.

### Konfigurera USC (Unified Storage Connector) för AEM {#configure-unified-storage-connector-workflows}

Utför följande steg för att konfigurera USC (Unified Storage Connector) för AEM arbetsflöden:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Unified Storage Connector]**.

1. I **[!UICONTROL Workflow]** avsnitt, Välj **[!UICONTROL Azure]** från listrutan Lagring.
1. Ange [konfigurationssökväg för Azure-lagringskonfigurationen](#create-azure-storage-configuration) i **[!UICONTROL Storage Configuration Path]** fält.
1. Välj **[!UICONTROL Publish]** och sedan **[!UICONTROL Save]** för att spara konfigurationen.

### Konfigurera en AEM arbetsflödesmodell för extern datalagring {#configure-workflow-external-data-storage}

Utför följande steg för att konfigurera en AEM arbetsflödesmodell för en extern datalagring:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Välj ett modellnamn och välj **[!UICONTROL Edit]**.
1. Välj ikonen Sidinformation och välj **[!UICONTROL Open Properties]**.
1. Välj **[!UICONTROL Externalize workflow data storage]**.
1. Välj **[!UICONTROL Save & Close]** för att spara egenskaperna.

>[!NOTE]
>
>Alternativen för att spara steget Tilldela uppgift som utkast och för att hämta historiken för steget Tilldela uppgift inaktiveras när du konfigurerar en AEM arbetsflödesmodell för extern datalagring.

### Riktlinjer för AEM arbetsflöden för extern datalagring {#guidelines-workflows-external-data-storage}

Nedan följer några riktlinjer när du använder AEM arbetsflöden och lagrar data till externa datalager, som Microsoft Azure-lagringsservern:

* Använd variabler för att lagra data när du definierar in- och utdatafiler och bilagor i arbetsflödesmodellstegen. Markera inte **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]** alternativ. The **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]** visas inte automatiskt när du [konfigurera en AEM arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage).

* Använd variabler för att lagra datafiler och bilagor när du skickar ett anpassat formulär till ett AEM arbetsflöde. Markera inte **[!UICONTROL Relative to Payload]** när du skickar ett anpassat formulär till ett AEM arbetsflöde. The **[!UICONTROL Relative to Payload]** alternativet visas inte automatiskt när du [konfigurera en AEM arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage).

* Använd inte ett anpassat AEM arbetsflödessteg i en arbetsflödesmodell för att lagra data i CRX DE-databasen.

* När du [konfigurera en AEM arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage)ska du inte skapa anpassade kolumner för AEM Inkorg eftersom värdena för de anpassade kolumnerna inte hämtas om arbetsobjektet i AEM Inkorg tillhör ett arbetsflöde som är markerat för extern lagring.

>[!MORELIKETHIS]
>
>* [Konfigurera datakällor för AEM Forms](/help/forms/configure-data-sources.md)
>* [Konfigurera Azure-lagring för AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrera Microsoft Dynamics 365 och Salesforce med adaptiv Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Lägg till Forms Portal på en AEM Sites-sida](/help/forms/configure-forms-portal.md)
