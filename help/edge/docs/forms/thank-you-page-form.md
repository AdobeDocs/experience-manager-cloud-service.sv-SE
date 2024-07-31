---
title: Visa ett anpassat tackmeddelande efter att formuläret har skickats
description: Lär dig konfigurera tacksidor och omdirigering för Forms Block för att optimera användarupplevelsen och effektivisera användarresorna.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Visa ett anpassat tackmeddelande efter att formuläret har skickats

När en användare har skickat in ett formulär är det viktigt att kunna erbjuda en smidig upplevelse genom ett tackmeddelande. Det bekräftar inte bara att ansökan har lämnats in, det ger också nöjdare användare och leder dem vidare på kundresan.

* **Tack**! Ett tackmeddelande är en hörnsten i användarupplevelsen och ger trygghet och förmedlar viktig information samtidigt som varumärkesidentiteten förstärks. Det fungerar som ett direkt erkännande av användarens åtgärder och ger en känsla av komplettering och tillfredsställelse.

* **Omdirigering**: En omdirigering spelar en avgörande roll för att styra användare mot relevanta destinationer, optimera engagemanget och i slutändan öka konverteringsgraden. En omdirigering ger en smidig navigeringsupplevelse genom att användaren smidigt vägleds till nästa steg i kundresan. Du kan till exempel dirigera om användaren till betalningssidan efter att du har samlat in initiala uppgifter.

Standardbeteendet för Adaptive Forms Block är att visa följande tackmeddelande när det skickas. Meddelandet visas högst upp i formuläret när formuläret har skickats.

![standardtackmeddelande](/help/edge/assets/thank-you-message.png)

Du kan dock anpassa den här upplevelsen efter dina specifika behov. Alternativen är:

* Visa ett anpassat tackmeddelande efter att formuläret har skickats
* Dirigera om användare till en annan sida efter inskickandet för ytterligare åtgärder

>[!NOTE]
>
> Du kan använda följande [frågekalkylblad](/help/edge/docs/forms/assets/enquiry.xlsx) för att anpassa tackmeddelandet efter dina önskemål.

## Konfigurera ett anpassat tackmeddelande

Om du vill visa ett personligt tackmeddelande när formuläret har skickats kan du konfigurera kalkylbladet så att det visas.

Följ stegen nedan för att konfigurera ett anpassat tackmeddelande för ditt adaptiva Forms-block:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.
1. Lägg till ett anpassat tackmeddelande i kolumnen `value` för fälttypen `submit` i kalkylbladet.

   ![Anpassat tackmeddelande](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Lägg till exempel till meddelandet `Submission Successful!` i kolumnen `value` för fälttypen `submit`.

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Anpassat tackmeddelande](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Dirigera om användare till en annan sida efter att de skickats in

Att dirigera om en användare till en annan sida efter att formuläret har skickats in kan förbättra användarupplevelsen genom att tillhandahålla relevant information, bekräfta åtgärder och vägleda användarna mot önskat resultat. Exempel:

* när en användare har slutfört ett inköpsformulär omdirigeras de till en betalningssida för att slutföra transaktionen på ett säkert sätt.
* När man skickar in ett registreringsformulär för en händelse eller webbinarium dirigeras man om till en bekräftelsesida med händelseinformation som datum, tid och plats.

Följ stegen nedan för att omdirigera användare till en annan sida:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.
1. Klistra in URL:en i kolumnen `value` för fälttypen `submit` i kalkylbladet för att omdirigera användaren när formuläret har skickats.
Om du vill dirigera om sidan till en annan sida använder du URL:en för sidan [Edge Delivery Documentation](https://www.aem.live/docs/) .

   ![Tack! Omdirigerings-URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Omdirigera tackmeddelande](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

Du kan också skapa en ny dokumentfil och lägga till dess förhandsgransknings-URL i kolumnen `value` för fälttypen `submit`.

När en användare har skickat in ett formulär är det viktigt att du skickar ett tydligt tackmeddelande. Det bekräftar att inlämningen är klar och att användaren blir nöjdare.

## Se även

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 



## See also

{{see-more-forms-eds}}