---
title: Hur skickar man ett anpassat formulär för granskning? Hur hanterar man granskningar för ett formulär som är anpassat?
description: Granskning är en mekanism som gör att granskare kan utföra olika uppgifter för adaptiva formulär med steget Tilldela uppgift.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Skapa och hantera granskningar för ett adaptivt formulär {#review-step-forms-aem-sites-page}

Använda [Tilldela steg](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) AEM av arbetsflödet granskar granskaren det inskickade formuläret och utför en åtgärd på det. Följ de här stegen för att granska det skickade formuläret i steget Tilldela:

1. [Skapa ett AEM arbetsflöde](#create-an-aem-workflow)
1. [Konfigurera åtgärden skicka för den adaptiva formulärbehållaren](#configure-submit-action)
1. [Skicka ett anpassat formulär efter granskning](#submit-af-after-review)

## Skapa ett AEM arbetsflöde {#create-an-aem-workflow}

1. Öppna författarinstansen i redigeringsläge.
1. Gå till **[!UICONTROL Tools]** >  **[!UICONTROL Workflow]** >  **[!UICONTROL Models]** > **[!UICONTROL Create]** > **[!UICONTROL Create Model]**
1. Ange arbetsflödets namn och lägg till **[Tilldela uppgift]** steg
1. Tryck ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. The **[!UICONTROL Assign Task]** öppnas.
1. Öppna [!UICONTROL Form and Document] flik och öppna [!UICONTROL Pre-populated] och ange:

   * Välj indatafil med
   * Välj indatabilagor med

   ![Granskningssteg](/help/forms/assets/assigntask-review1.gif)

1. Öppna **[!UICONTROL Assignee]** flik och öppna [!UICONTROL Pre-populated] listruta och ange **[!UICONTROL Assign  options]**:

   ![Granskningssteg](/help/forms/assets/review-assignstep.png)

1. Klicka **[!UICONTROL Done]** för att spara ändringarna.

## Konfigurera Skicka-åtgärd {#configure-submit-action}

Konfigurera nu åtgärden Skicka för en komponent med adaptiv formulärbehållare på webbplatsens sida:

1. Gå till webbplatsens sida.
1. Tryck ![settings_icon](assets/settings_icon.png) för en adaptiv formulärbehållare. The **[!UICONTROL Adaptive Form Container]** öppnas.
1. Öppna **[!UICONTROL Submission]** -flik och ange **[!UICONTROL Submit Action]** till [Anropa ett AEM arbetsflöde](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Klicka [Klar] för att spara inställningarna.

![submittab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Skicka ett anpassat formulär efter granskning {#submit-af-after-review}

Så här granskar och bekräftar du det inskickade adaptiva formuläret:

1. Gå till [!UICONTROL Tools] >  [!UICONTROL Workflow] >  [!UICONTROL Instances]
1. I Inkorgen ser du att en instans håller på att skapas.
1. Markera instansen och klicka på [!UICONTROL Open].
1. Nu kan du se det inskickade formuläret.

Granskaren utför olika åtgärder som:

* **Skicka**: Granskaren fyller i formuläret och skickar det för vidare behandling.
* **Spara**: Granskaren sparar formuläret i det aktuella läget utan att skicka det.
* **Återställ**: Granskaren rensar alla ändringar som gjorts i formuläret och återställer det till det ursprungliga läget.
* **Delegera**: Granskaren överför äganderätten till formuläret till en annan person för ytterligare åtgärder eller granskning.
