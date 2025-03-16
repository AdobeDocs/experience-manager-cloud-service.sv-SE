---
title: Introduktion till  [!DNL AEM Forms] as a Cloud Service
description: Upptäck AEM Forms för att ta fram företagsklara formulär, skapa arbetsflöden för företagsprocesser och använda dokumenttjänster för att ta fram och skydda dokument.
landing-page-description: Lär dig hur du använder formulär i AEM as a Cloud Service.
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: 4b4bc6f754c6336136d409cf49617c7fafd4f4c3
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 2%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>Letar du efter dokumentation för en annan version?</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html">AEM 6.5 Forms Documentation</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong> (aktuell)</li>
  </ul>
</div>

## Vad är AEM Forms as a Cloud Service?

AEM Forms as a Cloud Service är Adobe molnbaserade lösning för att skapa, hantera och leverera digitala formulär och kommunikation. Det gör det möjligt för organisationer att omvandla komplexa transaktioner till enkla, digitala upplevelser under hela kundresan. Du kan använda tjänsten för att:

* Digitalisera och effektivisera registreringen och introduktionsupplevelsen
* Leverera personaliserad kommunikation
* Automatisera arbetsflöden
* Integrera formulär och kommunikationsupplevelser med datakällor
* Spåra och optimera formulärprestanda

Tjänsten är alltid aktuell, alltid tillgänglig och alltid tillgänglig. Organisationer kan använda [!DNL AEM Forms] as a Cloud Service och få alla dessa funktioner i molnet utan att det krävs någon lokal infrastruktur. Tjänsten befriar också organisationer från komplexa uppgraderingscykler eftersom den alltid är uppdaterad med de senaste funktionerna.

Adobe [!DNL Experience Manager Forms as a Cloud Service] är en kundcentrerad lösning som stöder varje steg i kundresan:

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Adaptiv Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Skapa responsiva, dynamiska formulär som anpassar sig efter användarens inmatning och enhetstyp:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">Skapa adaptiv Forms</a> - Skapa formulär som automatiskt justeras efter olika skärmstorlekar och användarindata</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type">Komponentbibliotek</a> - Använd olika indatafält och gränssnittskomponenter</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components">Stilanpassad Forms</a> - Använd enhetlig profilering och visuell design i dina formulär</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">Använd färdiga teman och mallar</a> - Snabba upp utvecklingen med färdiga komponenter</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components">Formulärvalidering</a> - Implementera verifieringsregler på klient- och serversidan</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components">Skicka åtgärder</a> - Konfigurera vad som händer när användare skickar formulär</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/generate-document-of-record-core-components">Postdokument</a> - Skapa permanenta poster för skickade formulärdata</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page">Lägg till Forms på AEM Sites-sidor</a> - Integrera enkelt formulär på din webbplats</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page">Lägg till Forms på en webbplats från tredje part</a> - Integrera enkelt formulär på webbplatsen</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Kommunikations-API:er</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Generera, hantera och skydda dokument programmatiskt:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-generation">Generera anpassad kommunikation</a> - Skapa anpassade dokument baserade på mallar och data</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation">Sammanställ och hantera PDF-filer</a> - Kombinera, dela och ändra PDF-dokument</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">Skapa PDF/A-dokument</a> - Generera dokument med arkivkvalitet</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#signature-apis">Använd signaturer</a> - Skydda dokument med signaturer</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#encryption-apis">Kryptera och dekryptera PDF-filer</a> - Skydda känsligt dokumentinnehåll</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Konvertera XDP till PostScript</a> - Omforma XDP-dokument till PostScript-format</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Konvertera XDP till PCL</a> - Omforma XDP-dokument till skrivarkommandospråk</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Konvertera XDP till ZPL</a> - Omforma XDP-dokument till Zebra-utskriftsspråk</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">Konvertera PDF till PDF/A-standarder</a> - Skapa arkivkompatibla PDF-dokument</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-pdf-documents-to-pdf-x-standards">Lägg till digitala signaturer</a> - Signera dokument digitalt för autentisering</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Edge Delivery Services för Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Skapa och leverera blanketter med Edge Delivery Services:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/overview">Edge Delivery Forms - översikt</a> - Läs mer om formulär med Edge Delivery Services</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/getting-started-universal-editor">Universal Editor för Forms</a> - Skapa formulär med WYSIWYG Universal Editor</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial">Dokumentbaserad redigering</a> - Skapa formulär med Microsoft Word eller Google Docs</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms">Formatera Edge Delivery Forms</a> - Använd anpassad formatering i dina formulär</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Headless Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Leverera formulärupplevelser över alla kanaler och i alla sammanhang:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview">Introduktion till Headless Forms</a> - Lär dig mer om det headless-sättet att hantera formulär</li>
        <li>Bygg formulär med React eller andra ramverk</li>
        <li>Integrera formulär i mobilappar, webbplatser och chattapplikationer</li>
        <li>Utnyttja era befintliga gränssnittskomponenter med formulärfunktioner</li>
        <li>Bevara logiken i backend-formuläret samtidigt som du har flexibilitet i förgrunden</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Automatisering av arbetsflöden</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Automatisera affärsprocesser som innefattar blanketter och dokument:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#assign-task-step">Skapa affärsprocesser</a> - Skicka formulär för godkännande eller feedback, arbetsflöden efter överföring eller serverdelsarbetsflöden för att hantera registreringsprocesser</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">Använd Adobe Sign i ett AEM-arbetsflöde</a> - Skicka ett dokument för signering </li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">Generera ett postdokument </a> - Generera on demand- eller on form submit-dokument</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>E-signaturer</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Lägga in juridiskt bindande elektroniska signaturer i era formulär och dokument:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms">Adobe Sign-integrering</a> - Aktivera e-signaturer i Adaptiv Forms</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">Lägg till e-signaturer i arbetsflöden</a> - Inkludera signatursteg i affärsprocesser</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">Postdokument med signaturer</a> - Generera signerade poster för formulärinskickade formulär</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Analyser och insikter</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Få insikter om formuläranvändning och prestanda:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">Aktivera Adobe Analytics</a> - Spåra formuläranvändning och prestanda</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics">Integrering med manuell analys</a> - Konfigurera analyser för detaljerad spårning</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports">Visa analysrapporter</a> - Analysera formulärprestanda och användarbeteende</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Dataintegrering</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Koppla formulären till era befintliga datakällor och system:</p>
      <h4>Adobe Ecosystem</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign">Adobe Sign</a> - Skicka för elektroniska signaturer via Adobe Sign</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-adaptive-form-with-market-engage/integrate-form-to-marketo-engage">Marketo Engage</a> - Integrera formulär med Adobe Marketo Engage</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#invoke-an-aem-workflow">AEM Workflow</a> - Utlösa AEM-arbetsflöden med formulärinskickningar</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#workfront-fusion">Workfront</a> - Skicka ett anpassat formulär till Adobe Workfront Fusion</li>
      </ul>
      <h4>Microsoft Integrations</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics">Microsoft Dynamics 365</a> - Integrera med Microsoft CRM</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage">Azure Blob Storage</a> - Lagra formulärdata i Microsoft molnlagring</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/connect-to-sharepoint/connect-forms-to-sharepoint-document-library">SharePoint Document Library</a> - Ansluta till Microsoft SharePoint dokumentbibliotek</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#connect-af-sharepoint-list">SharePoint List</a> - Ansluta till Microsoft SharePoint-listan</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-onedrive">OneDrive</a> - Anslut till Microsoft OneDrive</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/forms-microsoft-power-automate-integration">Microsoft Power Automate</a> - utlösa Microsoft Power Automate-flöden</li>
      </ul>
      <h4>Andra datakällor och tjänster</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration">Salesforce</a> - Integrera med Salesforce CRM</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-rest-endpoint">RESTful Services</a> - Anslut till en REST API-slutpunkt</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources">RDBMS-databaser</a> - Anslut till relationsdatabaser</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-email">E-post</a> - Skicka formulärdata via e-post</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/introduction-to-forms-portal/save-core-component-based-form-as-draft">Forms Portal</a> - Skicka till Forms Portal för att spara utkastet</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-pdf-via-email">Skicka PDF via e-post</a> - Skicka en PDF-version av det skickade formuläret via e-post</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-using-form-data-model">Skicka med formulärdatamodell</a> - Skicka data med en formulärdatamodell</li>
      </ul>
    </div>
  </div>
</div>

## Komma igång med AEM Forms as a Cloud Service

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>För företagsanvändare</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Lär dig grunderna</strong>: Lär dig mer om <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">Adaptiv Forms</a> och hur de kan digitalisera dina affärsprocesser.</li>
        <li style="margin-bottom: 8px;"><strong>Utforska mallar</strong>: Bläddra bland de <a href="https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">fördefinierade mallarna och temana</a> för att få ett försprång i dina formulärprojekt.</li>
        <li style="margin-bottom: 8px;"><strong>Lär dig skapa formulär</strong>: Följ <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring">formulärredigeringsguiden</a> för att skapa ditt första formulär.</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>För utvecklare</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Konfigurera din miljö</strong>: Konfigurera din <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-local-development-environment">lokala utvecklingsmiljö</a> för AEM Forms.</li>
        <li style="margin-bottom: 8px;"><strong>Lär dig arkitekturen</strong>: Förstå <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture">arkitekturen i AEM Forms as a Cloud Service</a>.</li>
        <li style="margin-bottom: 8px;"><strong>Utforska API:er</strong>: Bekanta dig med <a href="https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/"> tillgängliga API:er </a> och SDK:er för att utöka och integrera Forms.</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>För administratörer</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Anmäl dig till Cloud Service</strong>: Följ <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service">startguiden</a> för att konfigurera AEM Forms as a Cloud Service.</li>
        <li style="margin-bottom: 8px;"><strong>Konfigurera tjänster</strong>: Konfigurera <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">integreringar med andra Adobe-tjänster</a> som Adobe Analytics.</li>
        <li style="margin-bottom: 8px;"><strong>Migrera från AEM 6.5</strong>: Om du kommer från AEM 6.5 följer du <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html">migreringsguiden</a> för att gå över till Cloud Service.</li>
      </ol>
    </div>
  </div>
</div>

## Tidiga Adobe-funktioner

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; margin-bottom: 30px;">
  <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
    <h3>AEM Forms Tidig åtkomst</h3>
  </div>
  <div class="card-body" style="padding: 20px; background-color: #ffffff;">
    <p><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms-programmet för tidig åtkomst</a> ger exklusiv åtkomst till de senaste funktionerna innan de är allmänt tillgängliga, inklusive:</p>
    <ul style="margin-top: 10px; padding-left: 25px;">
      <li style="margin-bottom: 8px;"><strong>AEM Forms AI Assistant (Gen AI)</strong> - Skapa formulär snabbare med AI-baserade förslag</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms Workfront Fusion Connector</strong> - Automatisera arbetsflöden som utlöses av formuläröverföringar</li>
      <li style="margin-bottom: 8px;"><strong>Forms</strong> - Skapa formulärupplevelser i chattstil på alla AEM Sites-sidor</li>
      <li style="margin-bottom: 8px;"><strong>WYSIWYG Authoring for Edge Delivery</strong> - Bygg formulär med den universella redigeraren för Edge Delivery Services</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms till Marketo Connector</strong> - Integrera formulärinskickat material med Marketo Engage</li>
    </ul>
    <p>En fullständig lista över innovationer och detaljerad dokumentation för tidig åtkomst finns på <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms Tidig åtkomst-programsidan</a>.</p>
  </div>
</div>

<div style="background-color: #f0f7ff; border-left: 4px solid #1473e6; padding: 20px; margin: 30px 0; border-radius: 4px;">
  <h3 style="margin-top: 0; color: #1473e6;">Vill du komma igång?</h3>
  <p><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service" style="font-weight: bold; color: #1473e6;">Anmäl dig till AEM Forms as a Cloud Service</a> idag och omvandla din organisations digitala formulärupplevelse.</p>
</div>
