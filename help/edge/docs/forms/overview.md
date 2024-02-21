---
title: AEM Forms Edge Delivery Service - översikt
description: AEM Forms Edge Delivery Service har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 6fc55366119662ed803008f4cec8731e43120942
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}

AEM Forms Edge Delivery Service är en sammansättningsbar tjänst från Adobe som gör att du kan skapa och leverera effektiva webbformulär. Den här sammanställningsbara tjänsten är sömlöst integrerad med Adobe Experience Manager (AEM) för att du ska kunna utforma, bygga och driftsätta slagkraftiga, blixtsnabba webbformulär med ett intuitivt och effektivt arbetsflöde.

AEM Forms Edge Delivery Service hjälper dig att:

* **Skapa visuellt slagkraftiga formulär**: Gör intryck på den bleka, kakformsdesignen och fånga upp användarna med dynamiska, moderna former som speglar er varumärkesidentitet. Utnyttja färdiga komponenter eller skapa egna komponenter för att förverkliga din vision snabbt och enkelt.

* **Skapa formulär med perfekt fyr**: Bygg formulär som läses in och återges snabbt, även på långsamma internetanslutningar. Snabbare inläsningstider och optimerad användarupplevelse bidrar till snabbare ifyllnad av formulär och förbättrad konverteringsgrad.

* **Förenkla framtagning och inlämning**: Skapa formulär med välbekanta verktyg som Microsoft Excel eller Google Sheets i stället för med de traditionella redigeringsmiljöerna. Skicka blanketter direkt till Microsoft Excel- eller Google-ark och använd deras ekosystem för att enkelt bearbeta inlämnade data.

## Kom igång med AEM Forms Edge Delivery Service

<div>

<style>
    .card-container {
        width: calc(33% - 10px);
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
            <br><b style="margin-top: 5px;">Skapa ett formulär</b>
        </a>
        <p>Skapa formulär som läses in och återges snabbt och automatiskt flödar om på mobila enheter.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Lägga till valideringar i formulärfält" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd fältvalideringar</b>
        </a>
        <p>Minska antalet fel och frustration genom att kontrollera indata i blanketterna för korrekt formatering.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skapa formulärfragment</b>
        </a>
        <p>Återanvänd förkonfigurerade fragment i flera formulär.</p>
    </div>
    <!-- Repeat the same structure for other cards -->

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
  <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
          <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Översätta ett EDS-formulär" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Översätta ett formulär</b>
      </a>
      <p>Nå ut bättre med formulären och håll kostnaderna i schack.</p>
  </div>
  <div class="card-container">
      <a href="/help/edge/docs/forms/style-theme-forms.md">
          <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Använda format eller teman i ett formulär" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Anpassa ett tema</b>
      </a>
      <p>Skapa en enhetlig varumärkesbild genom att använda samma tema i alla formulär.</p>
  </div>
  <div class="card-container">
    <a href="/help/edge/docs/forms/repeatable-forms.md">  
      <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Lägga till repeterbara avsnitt i ett EDS-formulär" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Lägga till repeterbara avsnitt</b>
      </a>
      <p>Skapa och lägg enkelt till repeterbara avsnitt i ett formulär.</p>
  </div>
</div>
<!-- Repeat the same structure for other cards -->

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
  <div class="card-container">
    <a href="/help/edge/docs/forms/custom-components-forms.md"> 
      <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Skapa anpassade blankettkomponenter med JavaScript och CSS"  style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Skapa anpassade komponenter</b>
      </a>
      <p>ange JavaScript och CSS som standard för att skapa komponenter och teman.</p>
  </div>
  <div class="card-container">
    <a href="/help/edge/docs/forms/recaptacha-forms.md">  
      <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Använd reCAPTCHA i ett EDS-formulär" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Använd reCAPTCHA</b>
      </a>
      <p>Använd OTB reCAPTCHA-integrering för robust skydd för skräppost och robotar.</p>
  </div>
  <div class="card-container">
    <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
      <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Skicka formulär" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Skicka formulär till kalkylblad</b>
      </a>
      <p>Skicka formulär direkt till Microsoft Excel- eller Google-ark.</p>
  </div>
</div>
</div>

</br>

<!-- 
<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: 5px;">
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
       <a href="/help/edge/docs/forms/create-forms.md"> <img src="/help/edge/assets/smock_devices_18_n.svg"alt="Create a form using eds forms" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;"> Create a form</b> </a>
        <p> Create forms that that load and render quickly and automatically reflows on mobile devices.</p> <a href="/help/edge/docs/forms/create-forms.md"> </a>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/validate-forms.md"> <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Apply field validations</b> </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/form-fragments.md">  <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use Form Fragments in an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Create form fragments</b> </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/translate-forms.md">  <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Translate a form </b> </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/style-theme-forms.md">  <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Customize a theme</b> </a>
        <p>Create a consistent brand image by applying same theme across forms. </p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Add repeatable sections</b> </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
   <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
         <a href="/help/edge/docs/forms/custom-components-forms.md"> <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS" style="width: 75px, Height: 50px; border-radius: 5px;">  
        <b style="margin-top: 10px;">Create custom components</b> </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
         <a href="/help/edge/docs/forms/recaptacha-forms.md">  <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Use reCAPTCHA</b> </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>
        <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Submit form to spreadsheet</b> </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
    
</div>

-->








