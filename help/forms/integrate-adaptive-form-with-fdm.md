---
title: Hur integrerar man FDM (Form Data Model) för ett formulär med adaptiv form?
description: Lär dig skapa formulär baserade på en formulärdatamodell (FDM). Generera och redigera exempeldata för datamodellsobjekt i FDM.
feature: Edge Delivery Services, Adaptive Forms, Form Data Model
role: Admin, User
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# Integrera blanketter med Form Data Model

Genom att integrera formulär med en formulärdatamodell (FDM) kan du använda olika backend-datakällor för att skapa en formulärdatamodell (FDM). Du kan använda FDM (Form Data Model) som ett schema i olika formulärarbetsflöden. Konfigurera datakällorna och skapa en FDM (Form Data Model) som bygger på datamodellsobjekten och tjänsterna som finns i datakällorna.

## Fördelar med att integrera Forms med FDM (Form Data Model)

* **Sömlös serverdelsanslutning**: Koppla formulär till olika serverdelssystem (t.ex. databaser, REST API:er, SOAP-tjänster, CRM:er) utan anpassad kod. Detta möjliggör datautbyte i realtid och minskar integreringsarbetet.
* **Centraliserat dataschema** Formulärdatamodellen fungerar som ett enhetligt dataschema som förenklar mappning och hantering av dataobjekt och tjänster som används i flera formulär och arbetsflöden.

* **Förbättrad förifyllnad och inskickning av formulär**: Konfigurera enkelt åtgärder för förifyllnad och inskickning med hjälp av formulärdatatjänster för att säkerställa korrekt och aktuell datahämtning och lagring.

* **Stöd för dynamiska arbetsflöden**: Formulärdatamodell kan integreras med arbetsflöden för att automatisera affärsprocesser som baseras på skickade eller hämtade data, vilket ökar den övergripande effektiviteten.

## Förutsättningar

Kontrollera att du har utfört följande steg innan du konfigurerar formuläret med formulärdatamodellen:

* [Konfigurera Data Source](/help/forms/configure-data-sources.md): Konfigurera datakällan för att ansluta formuläret till backend-data.
* [Skapa formulärdatamodell (FDM)](/help/forms/create-form-data-models.md): Skapa en datamodell med dataobjekt och tjänster från den konfigurerade datakällan.
* [Konfigurera datamodellsobjekt och datatjänster](/help/forms/work-with-form-data-model.md): Mappa datamodellsobjekt och datatjänster för att säkerställa ett jämnt dataflöde mellan formuläret och datakällan.

>[!BEGINTABS]

>[!TAB Foundation Component]

Utför följande steg för att konfigurera formulärdatamodellen med ett adaptivt formulär baserat på Foundation-komponenten som:

1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit Using Form Data Model]**.

   ![skicka med formulärdatamodell](/help/forms/assets/submit-uisng-fdm-fc.png)

1. Välj den skapade **[!UICONTROL Data Model to submit]**-konfigurationen.
Om du vill skicka bilagor till databasen väljer du **Skicka formulärbilagor**. DoR-dokumentet (Document of Recore) sparas i databasen genom att du väljer **Skicka postdokument**.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

>[!TAB Kärnkomponent]

Utför följande steg för att konfigurera formulärdatamodellen med ett adaptivt formulär baserat på kärnkomponenten som:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. Välj **[!UICONTROL Submit Action]** Skicka med formulärdatamodell **[i listrutan]**.
   ![skicka med formulärdatamodell](/help/forms/assets/submit-uisng-fdm-cc.png)

1. Välj den skapade **[!UICONTROL Data Model to submit]**-konfigurationen.
Om du vill skicka bilagor till databasen väljer du **Skicka formulärbilagor**. DoR-dokumentet (Document of Recore) sparas i databasen genom att du väljer **Skicka postdokument**.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

>[!TAB Universell redigerare]

Utför följande steg för att konfigurera formulärdatamodellen med ett adaptivt formulär som har skapats i Universal:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.

   Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.

1. Klicka på fliken **Skicka** och välj **[!UICONTROL Submit using Form Data Model]**.

   ![OneDrive GIF](/help/forms/assets/submit-uisng-fdm-ue.png)
Om du väljer **Spara bifogade filer med ursprungligt namn** sparas de bifogade filerna i mappen med sina ursprungliga filnamn. Du kan också spara DoR-dokument (Document of Record) i Azure Blob Storage.

1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save&Close]**

Detaljerade instruktioner om hur du integrerar formulär som har skapats i den universella redigeraren finns i artikeln [Integrera Forms med formulärdatamodellen i den universella redigeraren](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

>[!ENDTABS]

## Relaterade artiklar

{{af-submit-action}}
