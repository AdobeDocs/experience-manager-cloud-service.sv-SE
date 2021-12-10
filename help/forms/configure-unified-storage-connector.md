---
title: Hur konfigurerar jag Unified Storage Connector för AEM Forms?
description: Lär dig hur du hanterar anslutningsprogrammet för enhetlig lagring för AEM Forms. Använd Unified Storage Connector för att ansluta AEM Forms till externa datalager.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---


# Hantera koppling för enhetlig lagring för AEM Forms {#manage-unified-storage-connector}

Du kan använda Unified Storage Connector för att ansluta AEM Forms till externa datalager.

Du kan till exempel fylla i värden för fält i ett anpassat formulär och skicka det till ett AEM arbetsflöde. Du kan konfigurera AEM arbetsflöden ytterligare för att lagra data i en extern lagringsplats, till exempel Microsoft Azure-lagringsservern. Använd Unified Storage Connector för att skapa en anslutning mellan AEM arbetsflöden och det externa lagringsutrymmet.

## Ansluta AEM arbetsflöden med en Microsoft Azure-lagringsserver {#connect-workflows-with-azure}

Skapa en Azure-lagringskonfiguration och referera till den konfigurationen med Unified Storage Connector. Du kan sedan konfigurera AEM arbetsflödesmodeller för att externalisera datalagringen för att ansluta dem till en Azure-lagringsserver.

### Skapa [!DNL Azure] lagringskonfiguration {#create-azure-storage-configuration}

Innan du utför dessa steg måste du se till att du har en [!DNL Azure] lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till [!DNL Azure] lagringskonto.

Utför följande steg för att skapa en [!DNL Azure] lagringskonfiguration:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. Välj en mapp för att skapa konfigurationen och tryck på **[!UICONTROL Create]**.
1. Ange en rubrik för konfigurationen i dialogrutan **[!UICONTROL Title]** fält.
1. Ange namnet på [!DNL Azure] lagringskonto i **[!UICONTROL Azure Storage Account]** fält.
1. Ange nyckeln för åtkomst till Azure-lagringskontot i **[!UICONTROL Azure Access Key]** fält och knacka **[!UICONTROL Save]**.

### Konfigurera koppling för enhetlig lagring för AEM arbetsflöden {#configure-unified-storage-connector-workflows}

Så här konfigurerar du Unified Storage Connector för AEM arbetsflöden:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Unified Storage Connector]**.

1. I **[!UICONTROL Workflow]** avsnitt, Välj **[!UICONTROL Azure]** från listrutan Lagring.
1. Ange [konfigurationssökväg för Azure-lagringskonfigurationen](#create-azure-storage-configuration) i **[!UICONTROL Storage Configuration Path]** fält.
1. Tryck **[!UICONTROL Publish]** och sedan trycka **[!UICONTROL Save]** för att spara konfigurationen.

### Konfigurera en AEM arbetsflödesmodell för extern datalagring {#configure-workflow-external-data-storage}

Utför följande steg för att konfigurera en AEM arbetsflödesmodell för en extern datalagring:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Välj ett modellnamn och tryck **[!UICONTROL Edit]**.
1. Tryck på ikonen Sidinformation och tryck på **[!UICONTROL Open Properties]**.
1. Välj **[!UICONTROL Externalize workflow data storage]**.
1. Tryck **[!UICONTROL Save & Close]** för att spara egenskaperna.

>[!NOTE]
>
>Alternativen för att spara steget Tilldela uppgift som utkast och för att hämta historiken för steget Tilldela uppgift är inte tillgängliga när du konfigurerar en AEM arbetsflödesmodell för extern datalagring.

### Riktlinjer för AEM arbetsflöden för extern datalagring {#guidelines-workflows-external-data-storage}

Nedan följer några riktlinjer när du använder AEM arbetsflöden och lagrar data till externa datalager, som Microsoft Azure-lagringsservern:

* Använd variabler för att lagra data när du definierar in- och utdatafiler och bilagor i arbetsflödesmodellstegen. Markera inte **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]** alternativ. The **[!UICONTROL Relative to Payload]** och **Tillgängligt på en absolut sökväg** visas inte automatiskt när du [konfigurera en AEM arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage).

* Använd variabler för att lagra datafiler och bilagor när du skickar ett anpassat formulär till ett AEM arbetsflöde. Markera inte **[!UICONTROL Relative to Payload]** när du skickar ett anpassat formulär till ett AEM arbetsflöde. The **[!UICONTROL Relative to Payload]** alternativet visas inte automatiskt när du [konfigurera en AEM arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage).

* Använd inte ett anpassat AEM arbetsflödessteg i en arbetsflödesmodell för att lagra data i CRX DE-databasen.

* När du [konfigurera en AEM arbetsflödesmodell för extern datalagring](#configure-workflow-external-data-storage)skapar du inte anpassade kolumner för AEM Inkorg baserat på data i ett arbetsflöde.
