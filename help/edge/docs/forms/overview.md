---
title: AEM Forms Edge Delivery Service - översikt
description: AEM Forms Edge Delivery Service har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e21b681b12e90110436c7319797809c8d6b75eea
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service

Effektivisera framtagningen av blanketter och få snabbare ifyllnad med Adobe AEM Forms Edge Delivery Service. Med denna kraftfulla, samverkande tjänst kan ni skapa formulär i företagsklass med enastående prestanda och visuella tilltalande funktioner. AEM prioriterar både användarupplevelsen och affärsmålen, vilket ger blixtsnabba laddningstider och fler slutförda formulär.

![EDS Forms Key features](/help/edge/assets/eds-forms-key-features.png){width="70%"}

Du kan använda tjänsten för att:

* **Captivate-användare med enastående formulär**: Skapa enkelt komplexa och engagerande formulär med ett bibliotek med färdiga komponenter. Integrera enkelt reCAPTCHA, skicka formulär direkt till e-post och möjliggör smidiga filöverföringar för säkra lagringslösningar som Sharepoint, Azure Storage och Amazon S3. Du kan till och med skapa egna skräddarsydda blankettkomponenter för att förverkliga din unika vision.

* **Skapa digitala registreringsupplevelser med valfria verktyg**: Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda både dokumentbaserad redigering (Microsoft 365 och Google Workspace) och AEM (AEM Editors). Det innebär att du kan arbeta med flera innehållskällor på samma webbplats och använda de redigeringsverktyg du föredrar, till exempel Microsoft Excel, Google Sheets eller Adaptiv Forms Editor.

* **Bygg formulär med perfekt Lightroom-poäng**: Bygg formulär som läses in och återges snabbt, även på långsamma internetanslutningar. Snabbare inläsningstider och optimerad användarupplevelse bidrar till snabbare ifyllnad av formulär och förbättrad konverteringsgrad.


<!-- >
* **Captivate users with stunning forms**: 
Build complex and engaging forms with ease using a library of pre-built components. Easily integrate reCAPTCHA, submit forms directly to email, and allow seamless file uploads to secure storage solutions like Sharepoint, Azure Storage, and Amazon S3. Even create your own custom forms components to bring your unique vision to life. 

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Börja skapa formulär

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Skapa ett formulär med hjälp av eds-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skapa ett formulär med Google eller Microsoft Excel</b>
        </a>
        <p>Skapa formulär som läses in och återges snabbt och automatiskt flödar om på mobila enheter.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Skicka formulär" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skicka formulär till kalkylblad</b>
        </a>
        <p>Skicka formulär direkt till Microsoft Excel- eller Google-ark.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Använda format eller teman i ett formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Anpassa ett tema</b>
        </a>
        <p>Skapa en enhetlig varumärkesbild genom att använda samma tema i alla formulär.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Lägga till valideringar i formulärfält" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd fältvalideringar</b>
        </a>
        <p>Minska antalet fel och frustration genom att kontrollera indata i blanketterna för korrekt formatering.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Använd regler för att lägga till dynamiskt beteende i ett formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd regler för att lägga till dynamiskt beteende i ett formulär</b>
        </a>
        <p>Återanvänd förkonfigurerade fragment i flera formulär.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Översätta ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Översätta ett formulär</b>
        </a>
        <p>Nå ut bättre med formulären och håll kostnaderna i schack.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Lägga till repeterbara avsnitt i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Lägga till repeterbara avsnitt</b>
        </a>
        <p>Skapa och lägg enkelt till repeterbara avsnitt i ett formulär.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Skapa anpassade blankettkomponenter med JavaScript och CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skapa anpassade komponenter</b>
        </a>
        <p>Använd JavaScript och CSS som standard för att skapa komponenter och teman.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Använd reCAPTCHA i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd reCAPTCHA</b>
        </a>
        <p>Använd OTB reCAPTCHA-integrering för robust skydd för skräppost och robotar.</p>
    </div>


</div>


</br>









