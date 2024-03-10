---
title: Översikt över AEM Forms-Edge Delivery Services
description: AEM Forms Edge Delivery Services som tagits fram för bästa prestanda och som gör det möjligt att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 2b64cc8d2afb7d6064d1f60ba023448171862236
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# AEM Forms-Edge Delivery Services

Effektivisera framtagningen av blanketter och få snabbare ifyllnad med Adobe AEM Forms-Edge Delivery Services. Dessa kraftfulla, sammanställbara tjänster gör att du kan skapa formulär i enterpriseklass med enastående prestanda och visuella fördelar. AEM prioriterar både användarupplevelsen och affärsmålen, vilket ger blixtsnabba laddningstider och ökad konvertering av formulär.

Du kan använda tjänsten för att:

* **Skapa enastående registreringsupplevelser**: Skapa registreringsupplevelser som läses in och återges snabbt, även på långsamma internetanslutningar. Snabbare inläsningstider och optimerad användarupplevelse bidrar till snabbare ifyllnad av formulär och förbättrad konverteringsgrad.

* **Skapa registreringsupplevelser med valfria verktyg**: Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Använd båda **dokumentbaserad redigering** (Microsoft SharePoint eller Google Drive) och **AEM** (Adaptiv Forms Editor). Det innebär att du kan arbeta med flera innehållskällor i samma formulär och använda de redigeringsverktyg du föredrar, till exempel Microsoft Excel, Google Sheets eller Adaptiv Forms Editor.

* **Använd utvecklarvänliga verktyg:** AEM Forms använder HTML, modern CSS och vanilj JavaScript för att skapa exceptionella upplevelser utan den vanliga overheadkostnaden. Utvecklare med grundläggande kunskaper i HTML, CSS och JS bör kunna bygga egna komponenter och behöver inte lära sig något specifikt språk eller ramverk. Du behöver inte vänta på en pipeline, checka in koden i Github och ändringarna är aktuella. Dessutom behövs ingen pipeline eller väntan, checka in koden i Github och ändringarna är live.


## Översikt över AEM Forms-Edge Delivery Services {#edge-overview}

Följande diagram visar hur du kan redigera innehåll i Microsoft Excel eller Google Sheets (dokumentbaserad redigering) och publicera till Edge Delivery Services. Den visar också den AEM publiceringsmetoden med Adaptiv Forms Editor.

![Edge Delivery Architecture](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services är en sammansatt uppsättning tjänster som ger stor flexibilitet när det gäller hur du skapar innehåll på din webbplats. Som tidigare nämnts kan du använda båda [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) med [AEM](/help/implementing/universal-editor/introduction.md) och [dokumentbaserad redigering](https://www.aem.live/docs/authoring)

Du kan till exempel använda innehåll direkt från Microsoft Excel eller Google Sheets. Det innebär att innehåll från dessa källor kan bli formulär på din webbplats. Det nya innehållet läggs till omedelbart utan någon omgenereringsprocess.

Edge Delivery Services använder GitHub så att kunder kan hantera och driftsätta kod direkt från sina GitHub-databaser. Du kan t.ex. skriva formulär i antingen Google Sheets eller Microsoft Excel och komponenterna i formulären kan utvecklas med CSS och JavaScript i GitHub. När du är klar kan du använda webbläsartillägget Sidekick för att förhandsgranska och publicera innehållsuppdateringar.

AEM Forms Edge Delivery Services innehåller ett blankettblock som kallas [Adaptivt Forms-block](/help/edge/docs/forms/create-forms.md) för att lägga till ett formulär på din Edge Delivery Services webbplats.

### Viktiga funktioner i AEM Forms Edge Delivery Services

Dokumentbaserad framtagning av en grundläggande uppsättning funktioner och AEM ger möjlighet att skapa mer komplexa och interaktiva blanketter. Följande tabell visar de viktigaste funktionerna för båda:

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

|                                           | Dokumentbaserad redigering | AEM (Adaptiv Forms Editor) |
| ----------------------------------------- | ------------------------ | ------------------------------------ |
| **Formulärfunktioner** |                          |                                      |
| Tillgängliga komponenter | ✓ | ✓ |
| Standardiserad HTML-struktur | ✓ | ✓ |
| Regler och valideringar | ✓ | ✓ |
| Bifogade filer (filöverföring) | ✓ | ✓ |
| Google reCAPTCHA | ✓ | ✓ |
| Egna komponenter | ✓ | ✓ |
| Skicka till e-post | ✓ | ✓ |
| **Avancerade funktioner** |                          |                                      |
| Avancerade regler med visuell regelredigerare |                          | ✓ |
| Utbyggbarhet på serversidan |                          | ✓ |
| Flera överföringsåtgärder |                          | ✓ |
| **Formulärdesign och -hantering** |                          |                                      |
| Adaptiv Forms-editor för WYSIWYG-redigering |                          | ✓ |
| **Integreringar** |                          |                                      |
| Dokument för registrering |                          | ✓ |
| Integrering med Adobe Sign |                          | ✓ |
| Integrering med Adobe Analytics |                          | ✓ |
| Integrering med Marketo |                          | ✓ |
| Integrering med flera datakällor |                          | ✓ |
| Flera överföringsåtgärder |                          | ✓ |


## Börja skapa formulär

* [Komma igång - självstudiekurs för utvecklare](/help/edge/docs/forms/tutorial.md)
* [Skapa ett formulär med Google eller Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Skicka formulär direkt till Microsoft Excel- eller Google-blad](/help/edge/docs/forms/submit-forms.md)
* [Förbättra formulärens utseende: en guide till formatering](/help/edge/docs/forms/style-theme-forms.md)


<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->