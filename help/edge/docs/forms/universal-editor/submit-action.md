---
title: Skicka funktionsmakron
description: Konfigurera Skicka-åtgärder för anpassat formulär.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ac005e5bc143c35eb29ba177a26aa6cc33897db4
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---


# Inlämningsåtgärd för anpassat formulär

En Skicka-åtgärd anger målet för de data som samlas in via ett anpassat formulär. Överföringsprocessen börjar när användaren klickar på knappen **[!UICONTROL Submit]** i formuläret. AEM Forms erbjuder två typer av skicka-åtgärder som beskrivs nedan och gör att du kan skapa och använda anpassade skicka-åtgärder som uppfyller dina specifika behov. De färdiga Skicka-åtgärderna är:

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [Skicka till REST-slutpunkt](#rest-endpoint-submission-ue)
* [Skicka e-post](#email-submission-ue)


### Skicka till REST-slutpunkt {#rest-endpoint-submission-ue}

Åtgärden Skicka till REST-slutpunkt används för att skicka skickade formulärdata till en angiven REST-slutpunkt. Slutpunkten kan tillhöra antingen en intern server där formuläret finns eller en extern server genom att använda en relativ sökväg eller en absolut sökväg. Om du vill skicka data till den AEM-server som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM-servern. Exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



Så här konfigurerar du en REST-slutpunkt:

1. Öppna ditt adaptiva formulär i **[!UICONTROL Editor]**.
1. Välj **[!UICONTROL Adaptive Form Block]**.
1. Klicka på egenskapsikonen ![properties](/help/forms/assets/Smock_Properties_18_N.svg) .
1. Välj **[!UICONTROL Submit to a REST endpoint]** i listrutan **[!UICONTROL Submit Action]**.
1. Ange REST-slutpunkts-URL.
1. Du kan också **aktivera POST-begäran** och ange en URL för att skicka begäran.

{width=50%,height=50%}![Aktivera efterbegäran för anpassningsbara formulär](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * Ange sökvägen till resursen om du vill skicka data till en intern server. Data bokförs på resursens sökväg. Exempel: `/content/restEndPoint`. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.
> * Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POST-begäran anonymt.

### Skicka e-post {#email-submission-ue}

Med Skicka e-poståtgärd kan du skicka ett e-postmeddelande till en eller flera mottagare när formuläret har skickats. Med Skicka e-post-konfigurationen kan du skapa ett e-postmeddelande som kan innehålla formulärdata i ett fördefinierat format. Ta till exempel följande mall där kundnamn, leveransadress, delstatsnamn och postnummer hämtas från skickade formulärdata. [Läs mer om e-postmallar i Adaptiv Forms](/help/forms/html-email-templates-in-adaptive-forms.md). Några fördelar med att konfigurera ett anpassat formulär med Skicka e-post-åtgärden är:

1. Det möjliggör snabb kommunikation när formulärdata skickas direkt till angivna e-postmottagare.
1. Det effektiviserar arbetsflödet genom att direkt integrera inskickade formulär i e-postmeddelanden.
1. Det hjälper organisationer att anpassa e-postinnehållet och på så sätt göra det lämpligt för specifika kommunikationsbehov.

{width=50%,height=50%}![Adaptiva formuläregenskaper i Universell redigerare](/help/forms/assets/submit-actions-ue.png)


Så här konfigurerar du en skicka-åtgärd som en e-postadress för att skicka formulär:

1. Öppna ditt adaptiva formulär i **Redigeraren**.
1. Välj din **[!UICONTROL Adaptive Form Block]**.
1. Klicka på egenskapsikonen ![properties](/help/forms/assets/Smock_Properties_18_N.svg) .
1. Välj alternativet **[!UICONTROL Send email]** i listrutan **[!UICONTROL Submit Action]**.
1. När du har valt alternativet Skicka e-post kan du konfigurera följande egenskaper så som de visas i bilden nedan.

<table>
  <thead>
    <tr>
      <th>Bild</th>
      <th>Egenskap</th>
      <th>Beskrivning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="E-postkonfiguration"></td> 
    <td><b>Från</td>
    <td>Ange avsändarens e-postadress.</td>
    </tr>
    <tr>
      <td><b>Till</td>
      <td>Ange de primära mottagarna av e-postmeddelandet. Flera e-postadresser kan läggas till, avgränsade med kommatecken.</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>Ange vilka mottagare som ska få en kopia (CC) av e-postmeddelandet.</td>
    </tr>
    <tr>
      <td><b>BCC</td>
      <td>Ange vilka mottagare som ska få en kopia (BCC) av e-postmeddelandet.</td>
    </tr>
    <tr>
      <td><b>Ämne</td>
      <td>Ange ämnesraden för e-postmeddelandet.</td>
    </tr>
    <tr>
      <td><b>Använd extern mall</td>
      <td>Gör att en extern e-postmall kan användas för att formatera e-postinnehållet. Ange URL-adressen eller sökvägen till den externa mallen för att integrera en fördesignad e-postmall som finns i din AEM Assets-mapp.</td>
    </tr>
    <tr>
      <td><b>Inkludera bifogad fil</td>
      <td>Anger om skickade formulärdata ska innehålla en bifogad fil som skickats via formuläret i e-postmeddelandet. Bifogade format som stöds är PDF, XML och JSON.</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## Visa ett anpassat tackmeddelande om inskickning av anpassade formulär {#submit-action-message-ue}

Med alternativet Vid sändning kan du konfigurera ett Skicka-åtgärdsmeddelande för sändning av anpassat formulär så här konfigurerar du ett Skicka-åtgärdsmeddelande för formuläret:

1. Öppna ditt adaptiva formulär i **Redigeraren**.
1. Välj din **[!UICONTROL Adaptive Form Block]**.
1. Klicka på egenskapsikonen ![properties](/help/forms/assets/Smock_Properties_18_N.svg) .
1. När du klickar visas följande alternativ:
   * **[!UICONTROL On Submit]**: Vid sändning kan du anpassa ett meddelande som ska visas när ett formulär skickas. Som standard visas ett anpassat meddelande&quot;Tack för att du skickat in formuläret&quot; för användaren när ett formulär har skickats.
Du kan också anpassa tackmeddelandet när du skickar in formulär genom att välja alternativet **[!UICONTROL Show message]** och lägga till/redigera meddelandet i **RTF-redigeraren**.


