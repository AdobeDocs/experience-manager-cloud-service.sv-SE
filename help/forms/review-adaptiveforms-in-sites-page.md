---
title: Hur skickar man ett anpassat formulär för granskning? Hur hanterar man granskningar för ett formulär som är anpassat?
description: Granskning är en mekanism som gör att granskare kan utföra olika uppgifter för adaptiva formulär med steget Tilldela uppgift.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Skapa och hantera granskningar för ett adaptivt formulär {#review-step-forms-aem-sites-page}

Med hjälp av [Tilldela steg](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) i AEM arbetsflöde granskar granskaren det skickade formuläret och utför en åtgärd på det. Följ de här stegen för att granska det skickade formuläret i steget Tilldela:

1. [Skapa ett AEM arbetsflöde](#create-an-aem-workflow)
1. [Konfigurera åtgärden skicka för den adaptiva formulärbehållaren](#configure-submit-action)
1. [Skicka ett anpassat formulär efter granskning](#submit-af-after-review)

## Skapa ett AEM arbetsflöde {#create-an-aem-workflow}

1. Öppna författarinstansen i redigeringsläge.
1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL Create]** > **[!UICONTROL Create Model]**
1. Ange arbetsflödets namn och lägg till steget **[Tilldela uppgift]**
1. Välj ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. Dialogrutan **[!UICONTROL Assign Task]** öppnas.
1. Öppna fliken [!UICONTROL Form and Document] och öppna listrutan [!UICONTROL Pre-populated] och ange:

   * Välj indatafil med
   * Välj indatabilagor med

   ![Granskningssteg](/help/forms/assets/assigntask-review1.gif)

1. Öppna fliken **[!UICONTROL Assignee]**, öppna listrutan [!UICONTROL Pre-populated] och ange **[!UICONTROL Assign  options]**:

   ![Granskningssteg](/help/forms/assets/review-assignstep.png)

1. Klicka på **[!UICONTROL Done]** om du vill spara ändringarna.

## Konfigurera Skicka-åtgärd {#configure-submit-action}

Konfigurera nu åtgärden Skicka för en komponent med adaptiv formulärbehållare på webbplatsens sida:

1. Gå till webbplatsens sida.
1. Välj ![settings_icon](assets/settings_icon.png) för en adaptiv formulärbehållare. Dialogrutan **[!UICONTROL Adaptive Form Container]** öppnas.
1. Öppna fliken **[!UICONTROL Submission]** och ange **[!UICONTROL Submit Action]** för att [Anropa ett AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Klicka på [Klar] för att spara inställningarna.

![submittab-reviewStep](/help/forms/assets/submissiontab-reviewstep.gif)

## Skicka ett anpassat formulär efter granskning {#submit-af-after-review}

Så här granskar och bekräftar du det inskickade adaptiva formuläret:

1. Gå till [!UICONTROL Tools] > [!UICONTROL Workflow] > [!UICONTROL Instances]
1. I Inkorgen ser du att en instans håller på att skapas.
1. Markera instansen och klicka på [!UICONTROL Open].
1. Nu kan du se det inskickade formuläret.

Granskaren utför olika åtgärder som:

* **Skicka**: Granskaren slutför formuläret och skickar det för vidare bearbetning.
* **Spara**: Granskaren sparar formuläret i det aktuella läget utan att skicka det.
* **Återställ**: Granskaren rensar alla ändringar som gjorts i formuläret och återställer det till det ursprungliga läget.
* **Delegera**: Granskaren överför ägarskap av formuläret till en annan person för vidare åtgärd eller granskning.
