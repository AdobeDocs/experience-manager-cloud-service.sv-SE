---
title: Introduktion till [!DNL AEM Forms] as a Cloud Service
description: Upptäck AEM Forms och lär dig hur du kan producera affärsklara dokument och formulärinnehåll. Lär dig mer om Platform-as-a-Service (PaaS) och hur du hanterar digitala formulär och affärsprocesser i storföretagsklass, samt hur du kopplar Forms till aktuella datakällor.
landing-page-description: Lär dig hur du använder formulär i AEM as a Cloud Service.
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: f8e229820bb7aef3923e955c928033ef7d3d9460
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 4%

---

# Introduktion {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] erbjuder en molnbaserad lösning för Platform as a Service (PaaS) som ger företag möjlighet att skapa, hantera, publicera och uppdatera komplexa digitala formulär samtidigt som inlämnade data integreras med bakomliggande processer, affärsregler och data sparas i ett externt datalager. Tjänsten är alltid aktuell, alltid tillgänglig och alltid tillgänglig.

Du kan använda tjänsten för att skapa och distribuera interaktiva och engagerande digitala formulär. Ta till exempel en organisation som vill digitalisera sin kundregistreringsresa. De har flera datakällor med befintliga kunddata. De vill förifylla formulär, lägga till e-signera formulär och arkivera ifyllda formulär som PDF-filer. Dessutom har man flera tryckta blanketter (PDF forms) som man också vill konvertera till digitala blanketter.

Organisationen kan använda [!DNL AEM Forms] as a Cloud Service att skapa digitala formulär, koppla ihop formulär med befintliga datakällor, integrera formulär med [!DNL Adobe Sign] för att lägga till e-signaturer i formulär och generera DoR (Document of Record) för att arkivera inskickade formulär som PDF-filer. Man kan också använda tjänsten för att konvertera PDF forms till digitala blanketter.

Organisationen kan använda [!DNL AEM Forms] as a Cloud Service och få alla dessa funktioner i molnet utan att behöva någon lokal infrastruktur. Tjänsten befriar också organisationer från komplexa uppgraderingscykler eftersom den alltid är uppdaterad med de senaste funktionerna.

## Viktiga funktioner {#key-features}

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


>[!ENDTABS] -->

| Adaptiv Forms | Tjänsten Automated forms conversion | Kommunikations-API:er | Forms Analytics |
|---|---|---|---|
| Med adaptiv Forms kan företag skapa och hantera interaktiva, datadrivna formulär för sina webbplatser och andra digitala kanaler, responsiva och mobilvänliga formulär. | Med Automated forms conversion Service kan man konvertera blanketter från PDF till interaktiva, digitala blanketter som enkelt kan hanteras och distribueras online. | Kommunikations-API:er är en uppsättning RESTful-API:er (Application Programming Interfaces) som gör att företag kan automatisera skapandet, hanteringen och leveransen av personaliserad, datadriven kommunikation. | Tjänsten ger OTB-stöd för att ansluta till Adobe Analytics. Att koppla ihop formulär med Adobe Analytics ger flera fördelar för företag, bland annat förbättrad förståelse för användarbeteende, bättre anpassning av marknadsföringen, minskat feltillstånd och förbättrad avkastning. |

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

[Headless Adaptive Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) är en lösning för att skapa och hantera headless-webbformulär på Adobe Experience Manager. Med den här funktionen kan organisationer skapa, publicera och hantera interaktiva formulär som kan öppnas och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. AEM Headless Adaptive Forms ger större flexibilitet och skalbarhet när det gäller formulärutveckling och -driftsättning samt en förbättrad användarupplevelse tack vare möjligheten att skräddarsy formulärdesign och funktionalitet efter specifika behov. Genom att utnyttja funktionerna i AEM och headless-tekniken utgör den här lösningen en stabil plattform för att skapa, hantera och distribuera webbformulär för olika användningsområden och tillämpningar.


>[!TAB Kärnkomponenter]

The [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) är en uppsättning med 24 BEM-kompatibla komponenter med öppen källkod som bygger på grundvalen för Adobe Experience Manager WCM Core Components. De är särskilt utformade för att användas för att skapa Adaptiv Forms, som är formulär som anpassar sig efter användarens enhet, webbläsare och skärmstorlek.

Dessa komponenter kan användas för att skapa enastående datainhämtnings- och registreringsupplevelser genom ett stort antal alternativ för formulärfält, inklusive textfält, kryssrutor, listrutor med mera. De innehåller även funktioner som validering, villkorsstyrd logik och responsiv design, som kan användas för att skapa formulär som är användarvänliga och enkla att använda.

Eftersom dessa komponenter är öppen källkod kan utvecklare dessutom enkelt anpassa och utöka komponenterna så att de passar organisationens specifika behov. Och dessa komponenter bygger på BEM-metoder som ser till att de är skalbara och underhållbara.


>[!TAB Microsoft PowerAutomate Connector &#x200B;]

Microsoft Power Automate Connector for AEM Forms är en anslutning som gör att du kan integrera Adobe Experience Manager (AEM) Forms med Microsoft Power Automate (tidigare Microsoft Flow). Power Automate är en molnbaserad tjänst som gör att du kan skapa automatiserade arbetsflöden mellan olika program och tjänster.

Med Power Automate Connector för AEM kan du skapa arbetsflöden som automatiskt utlöses när ett adaptivt formulär skickas in. Du kan t.ex. skapa ett arbetsflöde som automatiskt skickar ett e-postmeddelande till en viss person när en användare skickar ett formulär eller skapar en uppgift i Microsoft Planner när en användare fyller i ett formulär.

Det finns många fördelar med att använda Power Automate Connector för AEM Forms, bland annat:

* **Automatisering**: Ni kan automatisera rutinuppgifter och effektivisera processerna, spara tid och minska antalet fel.

* **Integrering**: Tack vare kopplingen kan du integrera Adobe Experience Manager Forms med andra program och tjänster så att du kan arbeta med fler verktyg.

* **Anpassning**: Du kan skapa arbetsflöden som är anpassade efter dina specifika behov, med möjlighet att lägga till anpassade åtgärder, villkor och utlösare.

* **Analyser**: Power Automate ger detaljerad analys och rapportering så att ni kan övervaka och optimera arbetsflödena över tid.

Generellt sett är Power Automate Connector för AEM Forms ett kraftfullt verktyg som gör att du kan automatisera och integrera din AEM Forms med andra program och tjänster, vilket förbättrar effektiviteten och produktiviteten.

>[!TAB Microsoft Storage Connectors: OneDrive och Sharepoint]

AEM Forms Microsoft Storage Connectors för OneDrive och SharePoint är anslutningar som gör att du kan integrera Adobe Experience Manager (AEM) Forms med Microsoft OneDrive och SharePoint. Med dessa kopplingar kan du lagra och hantera AEM Forms-data och -dokument i Microsoft molnbaserade lagringslösningar.

Med dessa anslutningar kan du lagra och hantera AEM Forms-data och -dokument i Microsoft OneDrive. Med den här kopplingen kan du överföra datafiler och bifogade filer till OneDrive och SharePoint direkt från AEM Forms.

Det finns flera fördelar med att använda AEM Forms Microsoft Storage Connectors för OneDrive och SharePoint:

* **Integrering**: Med dessa anslutningar kan du integrera AEM Forms med Microsoft molnbaserade lagringslösningar, så att du kan utnyttja dessa plattformars kapacitet.

* **Samarbete**: OneDrive och SharePoint är samarbetsplattformar som gör det möjligt för teammedlemmar att arbeta tillsammans med filer och dokument. Genom att integrera AEM Forms med dessa plattformar kan ni förbättra samarbetet och samarbetet.

* **Säkerhet**: OneDrive och SharePoint har robusta säkerhetsfunktioner som säkerställer att data och dokument lagras och är åtkomliga på ett säkert sätt.

På det hela taget är AEM Forms Microsoft Storage Connectors för OneDrive och SharePoint kraftfulla verktyg som gör att du kan lagra och hantera AEM Forms-data och -dokument i Microsoft molnbaserade lagringslösningar, vilket förbättrar samarbete och säkerhet.

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