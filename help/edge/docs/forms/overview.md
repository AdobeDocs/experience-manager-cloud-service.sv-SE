---
title: Edge Delivery Services for AEM Forms - översikt
description: Skapa och leverera högpresterande formulär på Adobe Experience Manager Edge Delivery Services, med betoning på utvecklingsstrategin Universal Editor.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---


# Edge Delivery Services för AEM Forms


Edge Delivery Services för AEM Forms är en sammansatt uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera, publicera och öppna nya formulär. Dessa tjänster ger enastående och slagkraftiga formulärupplevelser som skapar engagemang och konverteringar. Dessa blankettupplevelser är enkla att skapa och utveckla.

Med de här tjänsterna kan du:

- **Skapa registreringsupplevelser med valfria verktyg:** Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda dokumentbaserad redigering (Microsoft SharePoint eller Google Drive), WYSIWYG Authoring (Universal Editor eller Adaptive Forms Editor). Du kan arbeta med flera innehållskällor på samma formulärwebbplats och använda de redigeringsverktyg du föredrar, till exempel Microsoft Excel, Google Sheets, Universal Editor eller Adaptive Forms Editor.

- **Leverera enastående digitala registreringsupplevelser:** Leverera digitala registreringsupplevelser som läses in och återges snabbt och kontinuerligt med övervakning av formulärprestanda via Operational Telemetry. Snabbare inläsningstider och optimerad användarupplevelse bidrar till att fler formulär fylls i och konverteras.

- **Använd utvecklarvänliga verktyg:** Edge Delivery Services för AEM Forms
använder HTML, modern CSS och vanilj JavaScript för att skapa exceptionella upplevelser och undvika den branta inlärningskurvan i ett specifikt ramverk. En utvecklare med grundläggande webbutvecklingskunskaper kan anpassa och enkelt bygga formulärkomponenter och upplevelser. Du behöver inte vänta på att en pipeline ska köras, du behöver bara checka in koden i GitHub så att ändringarna blir aktuella.

## Välja en redigeringsmetod


Med Adobe Experience Manager (AEM) Edge Delivery Services (EDS) kan du leverera blixtsnabba, skalbara webbupplevelser i toppklass. Den här guiden förklarar **hur du skapar och publicerar formulär för dessa upplevelser** - med en tydlig rekommendationshierarki:

- **Universell redigerare (UE) - Bästa val för de flesta team**
- **Dokumentbaserad redigering (dokument/ark) - Perfekt för snabba, enkla formulär**
- **Dokumentredigering (DA) - Används för att bädda in formulär på DA-skapade sidor**

När allt är klart kan du välja rätt redigeringsmetod, förstå överföringsalternativen och följa nästa steg mot produktionsklara formulär.


| Team och krav | Rekommenderad metod | Varför |
|--------------------|--------------------|-----|
| Marknadsförare/formgivare behöver visuell kontroll, villkorsstyrd logik eller AEM-integreringar | **Universell redigerare** | Dra-och-släpp, avancerade regler, skicka till FSS eller AEM Publish |
| Innehållsförfattare som redan arbetar i Word/Google Docs/Sheets; enkel datainhämtning till kalkylblad/e-post | **Dokumentbaserad redigering** | Välbekanta verktyg, snabbaste vägen för grundläggande formulär |
| Webbplatssidor inbyggda i **Dokumentredigering (DA)** | **Bädda in** ett UE- eller dokumentbaserat formulär på DA-sidan | DA skapar inte formulär själva |


## Detaljerade redigeringsmetoder

### Universal Editor

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">pre-release channel</a>. </span>
-->

[Universell redigerare](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) är ett visuellt dra och släpp-redigeringsverktyg för marknadsförare och designers som kombinerar snabbhet med kraftfulla företagsfunktioner:

- WYSIWYG redigering i realtid och förhandsgranskning av enheter.
- Direkt integrering med AEM resurser, arbetsflöden och FDM (Form Data Model).
- Smidig leverans till utvecklare för anpassade komponenter i vanilj JS/CSS.
- Avancerad regelredigerare för avancerad logik.
- Utbyggbarhet på serversidan för anpassade funktioner.
- WYSIWYG redigeringsupplevelse för enkel framtagning och visualisering av formulär.
- Dokumentera arkivfunktionalitet för att skapa manipuleringssäkra arkiv av inlämnade data.
- Integrering med Adobe Sign för elektroniska signaturer.
- Integrering med Adobe Workfront Fusion för att aktivera Adobe Workfront Fusion-scenarier när formulär skickas in.
- Integrering med olika datakällor för förifyllande av formulär och inlämning av data.
- Form Data Model (FDM) för att definiera datastrukturen och interaktionen med olika datakällor.
- Möjlighet att välja bland flera olika åtgärder för att skicka in formulär, inklusive att skicka data till Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, många fler datakällor.
- Skicka in med Forms Submission Service (FSS) eller AEM Publish

**Rekommendation**: Starta alla nya formulärprojekt med Universal Editor, såvida inte ditt team har dokumentcentrerat till 100 % och formuläret är mycket grundläggande.


### Dokumentbaserad redigering (med Microsoft Docs eller Google Sheets)

[Dokumentbaserad redigering](/help/edge/docs/forms/tutorial.md) är bäst lämpad för att skapa enkla, komplexa formulär med välbekanta verktyg som Microsoft Word, Google Docs eller Google Sheets. Den här metoden är idealisk för team som behöver ett snabbt och enkelt sätt att skapa formulär.

- Tillgängliga komponenter för en användarvänlig upplevelse.
- Standardiserad HTML-struktur för enhetlig rendering.
- Regler och valideringar för att säkerställa att data är korrekta.
- Alternativ för bifogade filer för insamling av ytterligare information.
- Integrering med Google reCAPTCHA för skräppostskydd.
- Möjlighet att skapa anpassade blankettkomponenter för specifika behov.
- Skicka formulärdata direkt till Microsoft Excel- eller Google-blad eller e-postadresser.
- Övervaka formulärens prestanda med telemetri


### Bädda in Forms i Document Authoring (DA)

Document Authoring (DA) är utformat för att skapa strukturerat sidinnehåll och stöder inte skapande av egna formulär. Om du vill lägga till ett formulär på en DA-skapad sida kan du skapa formuläret med hjälp av **Universal Editor** (rekommenderas) eller dokumentbaserad redigering och bädda in formuläret på dokumentredigeringssidan.

## Publicera Edge Delivery Services Forms {#edge-overview}

Följande diagram visar hur du kan redigera formulär i Microsoft Excel eller Google Sheets (dokumentbaserad redigering) och publicera till Edge Delivery Services. Här visas också AEM publiceringsmetod med WYSIWYG Authoring (Universal Editor).

![Publicera till Edge Delivery Services och AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |
-->

## Nästa steg

- [Funktioner i Universal Editor för Edge Delivery Services for Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Skapa ditt första formulär med Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md)
- [Skapa ditt första formulär med Google Sheets eller Microsoft Excel](/help/edge/docs/forms/tutorial.md).
- [Bädda in Forms i dokumentredigering (DA)](https://www.aem.live/developer/da-tutorial)


Nu kan du skapa ditt första högpresterande formulär med AEM Edge Delivery Services.


<!--
## Start creating forms

- [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
- [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
- [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
- [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
- [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
- [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
- [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
- [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
- [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
