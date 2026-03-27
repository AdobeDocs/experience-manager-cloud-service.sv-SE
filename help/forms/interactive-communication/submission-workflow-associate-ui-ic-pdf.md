---
title: Inlämningsarbetsflöde för Associate UI - IC Generate PDF Output
description: Förstå hur insändning och arbetsflöde fungerar för Associate UI och följ ett exempelarbetsflöde som genererar PDF från JSON (Interactive Communication).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Inlämningsarbetsflöde för associerat användargränssnitt

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

I den här artikeln beskrivs hur insändning och arbetsflöde fungerar när du aktiverar ett arbetsflöde för det associerade användargränssnittet. Sedan går vi igenom hur du konfigurerar ett arbetsflöde för att skicka in. Genomgången använder till exempel att generera en PDF från nyttolasten för interaktiv kommunikation. Du kan anpassa stegen för andra arbetsflödestyper.

<!--## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).-->

## Konfigurera ett överföringsarbetsflöde

Följande steg visar hur du skapar ett arbetsflöde som körs när användare skickar från det associerade användargränssnittet. Här använder vi till exempel **återgivning av grafikkortet till PDF** med **IC Render PDF Output** som är färdig. När en användare skickar från det associerade användargränssnittet skickas nyttolasten till arbetsflödet. I det här steget används **communicationDom** (IC-JSON) från nyttolasten för att skapa PDF.

### Nyttolaststruktur

Arbetsflödet tar emot en JSON-nyttolast. Fältet **communicationDom** innehåller det IC-JSON som används för PDF-generering. I steget **IC Render PDF Output** används det som mallindata.

| Fält | Beskrivning |
|-------|-------------|
| communicationDom | IC-JSON för PDF |
| auditMetadata | Granskningsinformation |
| submitData | Skickade formulärdata (JSON) |
| prefillData | Förifyll data (JSON) |
| referens, cookies, queryString, clientIP, userAgent, formSubmitter | Begär metadata |

### Skapa arbetsflödesmodellen

1. **Grundläggande:** Skapa en arbetsflödesmodell (lägg till ett arbetsflöde som **pdfrenderworkflow**).

   ![Fliken Grundläggande arbetsflödesmodell](/help/forms/assets/associate-ui-add-workflow.png)

1. **Variabler:** Lägg till variabler som matchar nyttolasten och steget: **communicationDom** (JSON), **auditMetadata** (JSON), **outputDocument** (dokument).

   ![Arbetsflödesvariabler](/help/forms/assets/associate-ui-add-variables.png)

1. **Steg:** Lägg till steget **IC Render PDF Output**.
   ![Lägg till arbetsflödessteg](/help/forms/assets/associate-ui-add-step.png)

1. På fliken **Indata** anger du **Select template (JsonObject)** till **Variable** → **communicationDom**. Spara steget och modellen.

   ![Konc.int. återgivning av PDF Output - fliken Input](/help/forms/assets/associate-ui-input-variable.png)

1. På fliken **Utdata** anger du **Select template (JsonObject)** till **Variable** → **communicationDom**. Spara steget och modellen.

   ![Arbetsflödesvariabler och arbetsyta](/help/forms/assets/assocaite-ui-output-variable.png)

### Koppla arbetsflödet till associerat gränssnitt

I [Aktivera och konfigurera associerat gränssnitt](/help/forms/interactive-communication/enable-configure-associate-ui.md) aktiverar du associerad vy och i **Arbetsflöde** anger du **Konfigurera arbetsflöde för uppdatering** till På och väljer den här arbetsflödesmodellen. Publicera IC:et och [integrera Associate UI](/help/forms/interactive-communication/invoke-associate-ui.md) så inskickade data utlöser det här arbetsflödet.

![Interaktiva kommunikationsinställningar - arbetsflödeskonfiguration för associerat gränssnitt](/help/forms/assets/associate-ui-configure-workflow.png)

När **Externalisera arbetsflödets datalagring** är aktiverat konfigurerar du den externa användaren så att arbetsflödesdata lagras i din externa lagring (till exempel Azure). Se [Gör arbetsflödesdata externt](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html).

## Se även

- [Associera gränssnittet i interaktiv kommunikationsredigerare](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Aktivera och konfigurera associerat gränssnitt för interaktiv kommunikation](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integrera associerat gränssnitt i ditt program](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Externalisera arbetsflödesdata](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)
