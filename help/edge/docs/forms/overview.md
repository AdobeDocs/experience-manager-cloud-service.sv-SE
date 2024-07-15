---
title: Översikt över AEM Forms-Edge Delivery Services
description: AEM Forms Edge Delivery Services som tagits fram för bästa prestanda och som gör det möjligt att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 2766a351938062127babb01d5ed35bd37b705c21
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# AEM Forms-Edge Delivery Services

AEM Forms Edge Delivery Services är en sammanslagen uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera, publicera och öppna nya formulär. Dessa tjänster ger enastående och slagkraftiga formulärupplevelser som skapar engagemang och konverteringar. Dessa blankettupplevelser är enkla att skapa och utveckla.

Med de här tjänsterna kan du:

* **Skapa registreringsupplevelser med valfria verktyg:** Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda dokumentbaserad redigering (Microsoft SharePoint eller Google Drive), WYSIWYG-redigering (Universal Editor eller Adaptive Forms Editor). Du kan arbeta med flera innehållskällor på samma formulärwebbplats och använda de redigeringsverktyg du föredrar, till exempel Microsoft Excel, Google Sheets, Universal Editor eller Adaptive Forms Editor.

* **Leverera enastående digitala registreringsupplevelser:** Leverera digitala registreringsupplevelser som läses in och återges snabbt och kontinuerligt med övervakning av formulärens prestanda via realtidsövervakning (RUM). Snabbare inläsningstider och optimerad användarupplevelse bidrar till att fler formulär fylls i och konverteras.

* **Använd utvecklarvänliga verktyg:** AEM Forms-Edge Delivery Services använder normal HTML, modern CSS och vanilj JavaScript för att skapa exceptionella upplevelser och undviker den branta inlärningskurvan i ett specifikt ramverk. En utvecklare med grundläggande webbutvecklingskunskaper kan anpassa och enkelt bygga formulärkomponenter och upplevelser. Du behöver inte vänta på att en pipeline ska köras, du behöver bara checka in koden i GitHub så att ändringarna blir aktuella.

## Översikt över AEM Forms-Edge Delivery Services {#edge-overview}

AEM Forms Edge Delivery-tjänster ger stor flexibilitet när det gäller hur du skapar formulär på din webbplats. Du kan skapa innehåll och formulär med [WYSIWYG-redigering](/help/forms/creating-adaptive-form-core-components.md) samt [dokumentbaserad redigering](/help/edge/docs/forms/create-forms.md). AEM Forms-Edge Delivery Services har ett formulärblock som kallas [Adaptivt Forms-block](/help/edge/docs/forms/create-forms.md) för att lägga till ett formulär på din Edge Delivery Services webbplats.

Du kan till exempel skapa formulär direkt i Microsoft Excel eller Google Sheets och dessa kalkylblad omvandlas till formulär för webbplatsen. Alla nya formulär- och formulärinnehåll, till exempel ett nytt formulärfält, är omedelbart tillgängliga på webbplatsen utan att något nytt behöver göras.

Följande diagram visar hur du kan redigera formulär i Microsoft Excel eller Google Sheets (dokumentbaserad redigering) och publicera på Edge Delivery Services. Den visar också den AEM publiceringsmetoden med WYSIWYG Authoring (Universal Editor eller Adaptive Forms Editor).

![Publish till Edge Delivery Services och AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

AEM Forms-Edge Delivery Services använder GitHub så att kunder kan hantera och driftsätta kod direkt från sina GitHub-databaser. Du kan till exempel skriva formulär i antingen [Google Sheets](/help/edge/docs/forms/create-forms.md) eller [Microsoft Excel](/help/edge/docs/forms/create-forms.md) och komponenterna i formulären kan utvecklas med CSS och JavaScript i en GitHub-databas.

När formulären är klara kan du använda [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), ett Chrome-tillägg, för att förhandsgranska och publicera innehållsuppdateringar.

![Installera AEM Sidekick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

Valet mellan [dokumentbaserad redigering](#document-based-authoring-features) och [WYSIWYG-redigering](#wysiwyg-authoring-features) beror på dina specifika krav:

* [Dokumentbaserad redigering](#document-based-authoring-features) passar bra för enkla formulär som bara samlar in grundläggande information med ett fåtal fält (t.ex. kontaktformulär, formulär för leadgenerering eller formulär för serviceförfrågningar) och där du behöver snabb dataanslutning med hjälp av ett kalkylblad. Du kan skapa dessa formulär på samma sätt som du skapar dokument i Google Sheets eller Microsoft Excel.

* För komplexa formulär, som formulär som kräver flera paneler, komplexa regler och affärslogik, datamanipulering, integrering med externa system eller smidiga arbetsflöden med AEM funktioner, är [WYSIWYG-redigering](#wysiwyg-authoring-features) ett bättre alternativ.


### Viktiga funktioner för dokumentbaserad redigering och WYSIWYG-redigering

Dokumentbaserad redigering har en grundläggande uppsättning funktioner och WYSIWYG-redigering ger tillgång till fler funktioner än den dokumentbaserade redigeringen, vilket gör att du kan skapa mer komplexa och interaktiva formulär. De viktigaste funktionerna för både dokumentbaserad redigering och WYSIWYG-redigering är:

#### Dokumentbaserade redigeringsfunktioner

Med dokumentbaserad redigering kan du skapa formulär med välbekanta verktyg som Microsoft Excel eller Google Sheets. Dessa formulär har följande funktioner:

* Tillgängliga komponenter för en användarvänlig upplevelse.
* Standardiserad HTML-struktur för enhetlig återgivning.
* Regler och valideringar för att säkerställa att data är korrekta.
* Alternativ för bifogade filer för insamling av ytterligare information.
* Integrering med Google reCAPTCHA för skräppostskydd.
* Möjlighet att skapa anpassade blankettkomponenter för specifika behov.
* Skicka formulärdata direkt till Microsoft Excel- eller Google-blad eller e-postadresser.
* Övervaka formulärens prestanda med hjälp av övervakning av användning i realtid (RUM)

#### WYSIWYG-funktioner

WYSIWYG Authoring innehåller WYSIWYG-gränssnitt (Universal Editor och Adaptive Forms Editor) för att skapa blanketter och har alla funktioner som finns i Document-based Authoring, plus en mängd andra funktioner:

* Avancerad regelredigerare för avancerad logik.
* Utbyggbarhet på serversidan för anpassade funktioner.
* WYSIWYG-redigering för enkel framtagning och visualisering av formulär.
* Dokumentera arkivfunktionalitet för att skapa manipuleringssäkra arkiv av inlämnade data.
* Integrering med Adobe Sign för elektroniska signaturer.
* Integrering med Adobe Workfront Fusion för att aktivera Adobe Workfront Fusion-scenarier när formulär skickas in.
* Integrering med olika datakällor för förifyllande av formulär och inlämning av data.
* Form Data Model (FDM) för att definiera datastrukturen och interaktionen med olika datakällor.
* Möjlighet att välja bland flera olika åtgärder för att skicka in formulär, inklusive att skicka data till Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, många fler datakällor.

Alla ovanstående funktioner är också tillgängliga via Adaptiv Forms Editor.

WYSIWYG-redigering (Universal Editor och [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) bygger på [dokumentbaserad redigering](/help/edge/docs/forms/create-forms.md) och ger en mer avancerad verktygslåda för att skapa och hantera komplexa formulär.

>[!NOTE]
>
>
> WYSIWYG-redigeringsfunktionen är tillgänglig i ett program som tagits i bruk tidigt. Om du är intresserad kan du skicka ett snabbt e-postmeddelande från din arbetsadress till aem-forms-ea@adobe.com och begära åtkomst till funktionen.

### AEM Forms-Edge Delivery Services: Skapa, publicera och skicka in Forms

I följande diagram illustreras hur man skapar, publicerar och skickar in blanketter med hjälp av dokumentbaserad redigering och WYSIWYG-redigering.

![Dokumentbaserad redigering ](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG-redigering](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Börja skapa formulär

* [Kom igång med AEM Forms Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [Skapa ett formulär med Google eller Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Konfigurera dina Google-blad eller Microsoft Excel-filer så att du kan börja ta emot &#x200B;](/help/edge/docs/forms/submit-forms.md)
* [Publish formulär och börja samla in data](/help/edge/docs/forms/publish-forms.md)
* [Anpassa utseendet på &#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [Lägga till repeterbara avsnitt i ett &#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [Visa ett anpassat tackmeddelande efter att formuläret har skickats &#x200B;](/help/edge/docs/forms/thank-you-page-form.md)
* [Komponenter för adaptiva formulärblock och deras egenskaper](/help/edge/docs/forms/form-components.md)
* [Realtime-användarövervakning](https://www.aem.live/developer/rum#authentication)

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