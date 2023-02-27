---
title: Introduktion till [!DNL AEM Forms] as a Cloud Service
description: Upptäck AEM Forms och lär dig hur du kan producera affärsklara dokument och formulärinnehåll. Lär dig mer om Platform-as-a-Service (PaaS) och hur du hanterar digitala formulär och affärsprocesser i storföretagsklass, samt hur du kopplar Forms till aktuella datakällor.
landing-page-description: Lär dig hur du använder formulär i AEM as a Cloud Service.
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 37274b28ab2343fd3cdfb4747c9dee701c699b46
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 4%

---

# Introduktion {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] erbjuder en molnbaserad lösning för Platform as a Service (PaaS) som ger företag möjlighet att skapa, hantera, publicera och uppdatera komplexa digitala formulär samtidigt som inlämnade data integreras med bakomliggande processer, affärsregler och data sparas i ett externt datalager. Tjänsten är alltid aktuell, alltid tillgänglig och alltid tillgänglig.

Du kan använda tjänsten för att skapa och distribuera interaktiva och engagerande digitala formulär. Ta till exempel en organisation som vill digitalisera sin kundregistreringsresa. De har flera datakällor med befintliga kunddata. De vill förifylla formulär, lägga till e-signera formulär och arkivera ifyllda formulär som PDF-filer. Dessutom har man flera tryckta blanketter (PDF forms) som man också vill konvertera till digitala blanketter.



Organisationen kan använda [!DNL AEM Forms] as a Cloud Service att skapa digitala formulär, koppla ihop formulär med befintliga datakällor, integrera formulär med [!DNL Adobe Sign] för att lägga till e-signaturer i formulär och generera DoR (Document of Record) för att arkivera inskickade formulär som PDF-filer. Man kan också använda tjänsten för att konvertera PDF forms till digitala blanketter.

Organisationen kan använda [!DNL AEM Forms] as a Cloud Service och få alla dessa funktioner i molnet utan att behöva någon lokal infrastruktur. Tjänsten befriar också organisationer från komplexa uppgraderingscykler eftersom den alltid är uppdaterad med de senaste funktionerna.

## Viktiga funktioner {#key-features}

|  |  |
|---|---|
| Adaptiv Forms | Skapa och hantera interaktiva, dynamiska, responsiva, mobilvänliga och datadrivna formulär för webbplatser, appar och andra digitala kanaler och tryckkanaler. Läs följande för att komma igång, förstå och implementera registreringsupplevelser: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html"> Skapa ett adaptivt formulär </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">Formatera ett anpassat formulär</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> Skicka data till ett datalager eller arbetsflöde</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> Skapa en post för formuläret för långtidsarkivering</a></li></ul> |
| Kommunikations-API:er | Automatisera framtagning, hantering och leverans av personaliserad, datadriven kommunikation med RESTful-API:er on demand eller vid schemalagda intervaller som månadsrapporter och kontobesked. Kom igång, förstå och skapa genom att granska följande: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> Generera skräddarsydd kommunikation </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> Sammanställa eller dela upp dokument från PDF </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">Skapa dokument som följer PDF/A </a></li></ul> |
| Tjänsten Automated forms conversion | Konvertera blanketter från PDF till adaptiva Forms som enkelt kan hanteras och distribueras online. Kom igång genom att granska följande: <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">Konfigurera tjänsten Automated forms conversion</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html">Konvertera PDF-formulär till anpassningsbara formulär</a></li></ul> |
| Formers Workflow | Automatisera affärsprocesser som innefattar blanketter och dokumenttjänster. Tilldela, dirigera, granska och godkänn blanketter och dokument när de rör sig genom olika steg i en affärsprocess. Kom igång genom att granska följande:  <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">Skicka ett formulär eller dokument för granskning</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">Skapa ett arbetsflöde för avvisande av godkännande</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">Lägg till postdokument </a> eller <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step"> e-signera </a> steg till ett affärsarbetsflöde</a></li></ul> |
| E-signaturer | Integrera med Adobe Sign och DocuSign för att enkelt skicka Forms och dokument till användare för e-signering. <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">E-signera ett adaptivt formulär med Adobe Sign </a></li><li></a> <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-docusign-adaptive-forms.html">E-signera ett adaptivt formulär med DocuSign </a></li></ul> |
| Forms Analytics | Använd Adobe Analytics för att få värdefulla insikter om användarbeteende och -preferenser. <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics.html?lang=en">Ansluta ett adaptivt formulär till Adobe Analytics</a></li></ul> |
| Datakällor | Koppla enkelt era formulär och dokument till externa datakällor för att hämta in och skicka data. <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=en">Anslut till en RDBMS- eller återställningsslutpunkt</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en">Anslut till molntjänsten Microsoft Dynamics 365 eller Salesforce</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=en">Anslut till Microsoft Azure Blob Storage</a></li></ul> |


<!-- 
>[!BEGINTABS]

>[!TAB Adaptive Forms]

Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>

>[!TAB Automated Forms Conversion Service]

Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>

>[!TAB Communications API (Document Services)]

Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.

>[!TAB Advanced Analytics]

The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>


>[!ENDTABS] 

| Adaptive Forms | Communications APIs  | Automated Forms Conversion Service | Forms Workflows | E-Sign | Forms Analytics | Data Model | 
|---|---|---|---|---|---| ---|
|Create and manage interactive, dynamic, responsive, mobile-friendly, and data-driven forms for your websites, apps, and other digital and Print channels. | Automate creation, management, and delivery of personalized, data-driven communications with RESTful APIs (Application Programming Interfaces) on-demand or at scheduled intervals. | Convert legacy PDF-based forms into Adaptive Forms that can be easily managed and distributed online. | Automate business processes involving forms and document services. Assign, route, review, and approve forms and document as these move through different stages of a business process.| Integrate with Adobe Sign and DocuSign to easliy send send Forms and documents to users for e-signatures. | Use Adobe Analytics to gain valuable insights into user behavior and preferences. | Easily connect your forms and documents with external data sources to retieve and send data. |
|<ul><li>Create an Adaptive Form</li><li>Style an Adaptive Form</li><li>Submit data to a data store or a workflow</li></ul>|<ul><li>Generate personalized communciations</li><li>Assemble or disassemble PDF documents</li><li>Create PDF/A-compliant documents</li></ul>|<ul><li>Configure Automated Forms Conversion Service</li><li>Convert PDF forms to adaptive forms</li></ul>|<ul><li>Send a form or document for review</li><li>Create an approval rejection Workflow</li><li>Add Document of Record or e-signatures to a business workflow</li></ul>|<ul><li>E-sign an Adaptive Form with Adobe Sign</li><li>E-sign an Adaptive Form with DocuSign</li></ul>|<ul><li>Connect an Adaptive Form with Adobe Analytics</li></ul>|<ul><li>Connect to a RDBMS or Rest endpoint</li><li>Connect to Microsoft Dynamics 365 or Salesforce cloud service</li><li>Connect to Microsoft&reg; Azure Blob Storage</li></ul>|

<!--
| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

-->

## Senaste innovationer {#latest-innovations}

>[!BEGINTABS]

>[!TAB Headless Adaptive Forms &#x200B;]

|| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?)| Skapa och hantera [Headless Adaptive Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) inom Adobe Experience Manager. Ge utvecklarna möjlighet att skapa, publicera och hantera interaktiva formulär som kan öppnas och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. <br/> <br/> Blanketterna ska skickas in utan att man behöver ha ett traditionellt HTML-gränssnitt. Med andra ord kan du skicka formulärdata via programmering via en API eller backend-kod utan att behöva använda några synliga formulärelement i gränssnittet. <br/> <br/> Headless-formulär är användbara i olika scenarier, t.ex. när du skapar enkelsidiga program, progressiva webbprogram eller mobilprogram, där ett traditionellt HTML-formulärgränssnitt kanske inte är nödvändigt eller praktiskt. Genom att utvecklarna kan skicka in formulärdata direkt via API:er eller backend-kod kan headless-formulär effektivisera arbetsflödena och förbättra prestanda för webbapplikationer.|




>[!TAB Kärnkomponenter]

|| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?) | [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) är en uppsättning med 24 BEM-kompatibla komponenter med öppen källkod som bygger på grundvalen för Adobe Experience Manager WCM Core Components. De är särskilt utformade för att användas för att skapa Adaptiv Forms, som är formulär som anpassar sig efter användarens enhet, webbläsare och skärmstorlek. <br/> <br/> Dessa komponenter kan användas för att skapa enastående datainhämtnings- och registreringsupplevelser genom ett stort antal alternativ för formulärfält, inklusive textfält, kryssrutor, listrutor med mera. De innehåller även funktioner som validering, villkorsstyrd logik och responsiv design, som kan användas för att skapa formulär som är användarvänliga och enkla att använda. <br/> <br/>  Eftersom dessa komponenter är öppen källkod kan utvecklare dessutom enkelt anpassa och utöka komponenterna så att de passar organisationens specifika behov. Och komponenterna bygger på BEM-metoder som ser till att de är skalbara och underhållbara.|



>[!TAB Microsoft PowerAutomate Connector &#x200B;]

|| |—|—| |![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999)| AEM Forms Power Automate Connector gör att du kan integrera Adobe Experience Manager (AEM) Forms med Microsoft Power Automate (tidigare Microsoft Flow). Power Automate är en molnbaserad tjänst som gör att du kan skapa automatiserade arbetsflöden mellan olika program och tjänster.  <br/> <br/> Med AEM Form Power Automate Connector kan du skapa arbetsflöden som automatiskt utlöses när ett adaptivt formulär skickas in. Du kan t.ex. skapa ett arbetsflöde som automatiskt skickar ett e-postmeddelande till en viss person när en användare skickar ett formulär eller skapar en uppgift i Microsoft Planner när en användare fyller i ett formulär.  <br/> <br/> AEM Forms Power Automate Connector är ett kraftfullt verktyg som gör att du kan automatisera och integrera din adaptiva Forms med andra program och tjänster som är kopplade till Microsoft Power Automate, så att du kan arbeta med fler verktyg. Du kan skapa arbetsflöden som är anpassade efter dina specifika behov, med möjlighet att lägga till anpassade åtgärder, villkor och utlösare. Dessutom ger Power Automate detaljerade analyser och rapporter så att du kan övervaka och optimera arbetsflödena över tid.|


>[!TAB Microsoft Storage Connectors: OneDrive och Sharepoint]

|| |—|—| |![](/help/forms/assets/onedrive-and-sharepoint.jpg)|AEM Forms Microsoft Storage Connectors för OneDrive och SharePoint är anslutningar som gör att du kan integrera Adobe Experience Manager (AEM) Forms med Microsoft OneDrive och SharePoint. Med den här kopplingen kan du överföra datafiler och bifogade filer till OneDrive och SharePoint direkt från Adaptiv Forms. |


>[!ENDTABS]

<!--

| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

Adaptive Forms enable organizations to quickly design and deploy responsive, mobile-friendly forms without the need for extensive coding or development. With Adaptive Forms, businesses can create complex, multi-step forms with conditional logic, validations, and integrations with back-end systems such as CRMs and databases.

Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development.

In addition, AEM Adaptive Forms offer several other features, including:

Advanced workflows for routing, approval, and submission of form data
Real-time validation and error checking to ensure data accuracy
Integration with third-party data sources and APIs for pre-filling form fields or validating data
Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics
Overall, AEM Adaptive Forms provide businesses with a powerful tool for creating and managing complex, interactive forms that can be easily integrated into their digital experiences. |




| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2611;  | &#x2612; |
| Auto-scaling based on load | &#x2611;  | &#x2612; |
| Zero downtime for upgrades | &#x2611;  | &#x2612; |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2611;  | &#x2612; | 
| Topologies optimized for maximum resilience and efficiency| &#x2611;  | &#x2612; | 
| Cloud-native development environment | &#x2611;  | &#x2612; | 
| Self-Service via Cloud Manager | &#x2611;  | &#x2612; | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2611;  | &#x2612; | 
| Adaptive Forms | &#x2611; | &#x2611; | 
| Data Integration with multiple data sources| &#x2611; | &#x2611; | 
| Communications APIs (Document Services) | &#x2611;* | &#x2611; | 
| Automated Forms Conversion Service | &#x2611; | &#x2611; | 
| Integration with [!DNL Micosoft Power Automate] | &#x2611; | &#x2612; | 
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; | 
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Launch] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Analytics] | &#x2611; | &#x2611; | 
| Easy connectivity with Microsoft Dynamics and Salesforce | &#x2611; | &#x2612; |
| Custom submit action for with [!DNL DocuSign] | &#x2611; | &#x2612; | 
| Microsoft Azure data store connector | &#x2611; | &#x2612; |
| Hardened Rule editor | &#x2611; | &#x2612; | 
| Forms Portal | &#x2611; | &#x2611; | 
| AEM Workflows | &#x2611; | &#x2611; | 
| Document of Record | &#x2611; | &#x2611; | 
| Adaptive Forms Wizard | &#x2611; | &#x2612; | 
| Custom XCI for Document of Record| &#x2611; | &#x2612; |
| Invisible Captcha | &#x2611; | &#x2611; |
| Reusable Form Data Model configurations | &#x2611; | &#x2611; |
| Acroform-based Document of Record | &#x2611; | &#x2611; | 
| Government ID based identity authentication for Adobe Sign enabled Adaptive Forms | &#x2611; | &#x2611; | 
| Document Security | &#x2612; | &#x2611; |


* [Notable changes in comparison to AEM 6.5 Forms](notable-changes.md)
* [Frequently asked questions](faq.md)

-->