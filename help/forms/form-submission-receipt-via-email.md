---
title: Hur skickar man en bekräftelse på att man skickat in ett formulär via e-post i AEM Forms?
description: Med AEM Forms kan du konfigurera åtgärden Skicka via e-post som skickar en bekräftelse till en användare när formulär skickas.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Skicka en bekräftelse på att formulär har skickats via e-post {#sending-a-form-submission-acknowledgement-via-email}

## Inlämning av data i anpassade formulär {#adaptive-form-data-submission}

Adaptiv Forms har flera färdiga [Skicka funktionsmakron](configuring-submit-actions.md) arbetsflöden för att skicka formulärdata till olika slutpunkter.

Till exempel **[!UICONTROL Send email]** Skicka åtgärd skickar ett e-postmeddelande när ett anpassat formulär har skickats. Den kan även konfigureras för att skicka formulärdata och PDF i e-postmeddelandet.

I den här artikeln beskrivs stegen för att aktivera e-poståtgärden för ett adaptivt formulär och olika konfigurationer som tillhandahålls.

>[!NOTE]
>
>Du kan också använda **[!UICONTROL Send PDF via email]** möjlighet att skicka det ifyllda formuläret via e-post som en bifogad fil i PDF. Konfigurationsalternativen som är tillgängliga för den här åtgärden är samma som de alternativ som är tillgängliga för **[!UICONTROL Send email]** åtgärd. Åtgärden Email PDF är bara tillgänglig för XFA-baserad Adaptive Forms

## Skicka e-poståtgärd {#email-action}

Med åtgärden Skicka e-post kan en författare automatiskt skicka e-post till en eller flera mottagare när ett anpassat formulär har skickats.

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, select **[!UICONTROL Form Container]** and select ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### Använda namn på adaptiva formulärfält för att dynamiskt skapa e-postinnehåll {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Fältnamnen i ett adaptivt formulär kallas platshållare som ersätts med värdet i det fältet när användaren skickar formuläret.

I **[!UICONTROL Send email]** kan du använda platshållare som bearbetas när åtgärden utförs. Det betyder att e-postens rubriker (som **[!UICONTROL To]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Subject]**) genereras när användaren skickar formuläret.

Om du vill definiera en platshållare anger du `${<field name>}` i ett fält efter markering **[!UICONTROL Send email]** som Skicka-åtgärd.

Om formuläret till exempel innehåller **[!UICONTROL Email address]** fält, namngivna `email_addr`för att hämta användarens e-post-ID kan du ange följande i **[!UICONTROL To]**, **[!UICONTROL CC]**, eller **[!UICONTROL BCC]** fält.

`${email_addr}`

När en användare skickar formuläret skickas ett e-postmeddelande till det e-post-ID som anges i `email_addr` formulärfält.

>[!NOTE]
>
>Du hittar namnet på ett fält i **[!UICONTROL Edit]** för fältet.

Variabelplatshållare kan också användas i **[!UICONTROL Subject]** och **[!UICONTROL Email Template]** fält.

Till exempel:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Fält i upprepningsbara paneler kan inte användas som variabla platshållare.

