---
title: Lägga till repeterbara avsnitt i ett formulär
description: Lägga till repeterbara avsnitt i ett EDS-formulär
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Lägga till repeterbara avsnitt i ett formulär

Med adaptiva formulärblock kan du lägga till eller göra ett avsnitt eller en komponent i ett formulär upprepningsbart. På så sätt kan användare ange information flera gånger för samma typ av data, vilket gör det enklare att samla in information som arbetserfarenhet eller utbildningsbakgrund.

Ta till exempel ett formulär som används för att samla in information om en persons arbetsupplevelse. Du kan ha ett upprepningsbart avsnitt där du kan hämta information om varje föregående jobb. Det repeterbara avsnittet innehåller vanligtvis fält som företagsnamn, befattning, anställningsdatum och ansvarsområden. Användaren kan lägga till flera instanser av det repeterbara avsnittet för att ange information om varje jobb som han/hon har utfört.



I slutet av den här artikeln lär du dig att:

* [Skapa ett upprepningsbart avsnitt i ett formulär](#add-repeatable-sections-to-a-form)
* [Ange minsta eller högsta antal upprepningar i ett formulär](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Skapa ett upprepningsbart avsnitt

Genom att skapa ett upprepningsbart avsnitt i ett formulär kan användarna ange flera instanser av samma datauppsättning, vilket gör det möjligt att effektivt samla in upprepad information. Så här skapar du ett upprepningsbart avsnitt i ett formulär:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.

1. Lägg till ett formulärfält med `type` egenskap inställd på `fieldset`
1. Ange `Name` av fältet. Egenskapen name används för att skapa ett upprepningsbart avsnitt.
1. Aktivera repeterbarhet genom att ange `repeatable` till `true`.
1. Ange en beskrivning `label` för fältet. Det fungerar som rubrik för det repeterbara avsnittet.

   Se bilden nedan för en illustration av en anställningshistorik i ett ansökningsformulär.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. För varje fält som du vill ta med i avsnittet anger du dess `Fieldset` till samma namn som du valde i steg 3.

   Ange till exempel `experience` i fältegenskapen för alla relevanta fält som ska inkluderas i `employment history` -avsnitt.

   ![exempel på ett upprepningsbart avsnittsfält och dess egenskaper](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera bladet. Det repeterbara avsnittet läggs till i formuläret.

   Under den repeterbara delen hittar användarna en intuitiv **Lägg till** och gör det enklare att lägga till flera avsnitt.

   ![upprepningsbart avsnitt, knappen Lägg till, om du vill lägga till flera avsnitt ](/help/edge/assets/repeatable-section-example.png)


## Ange minsta och högsta antal upprepningar

I formulärdesignen är det bra att ange minsta och högsta repetitioner för repeterbara avsnitt. På så sätt får ni kontroll och enhetlighet samtidigt som ni vägleder användarna effektivt. Så här anger du minsta eller högsta antal upprepningar:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.

1. För ett fält `type` `fieldset` och `repeatable` egenskap inställd på `true`:

   * ange `min` för att ange det minsta antal gånger som avsnittet kan upprepas.

   * ange `max` för att ange det maximala antal gånger som avsnittet kan upprepas.

   ![Ange egenskapen min och max för att ange hur många gånger avsnittet kan upprepas](/help/edge/assets/repeatable-section-set-min-max.png)

1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera bladet.

   När du lägger till ett upprepningsbart avsnitt hittar användarna en intuitiv **Ta bort** -ikonen, vilket gör det enklare att ta bort repeterbara avsnitt. När du väl har lagt till de här avsnitten kan de inte minskas till färre instanser än vad som anges i `min` -egenskap. Detta garanterar att minimikraven för ifyllande av formuläret uppfylls.

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Form block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-sharepoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## Se mer

* [Skapa och förhandsgranska ett formulär](/help/edge/docs/forms/create-forms.md)
* [Aktivera formulär för att skicka data](/help/edge/docs/forms/submit-forms.md)
* [Publicera ett formulär på webbplatssidan](/help/edge/docs/forms/publish-forms.md)
* [Lägga till valideringar i formulärfält](/help/edge/docs/forms/validate-forms.md)
* [Ändra teman och format för formulär](/help/edge/docs/forms/style-theme-forms.md)
* [Formulärkomponenter och deras egenskaper](/help/edge/docs/forms/form-components.md)
