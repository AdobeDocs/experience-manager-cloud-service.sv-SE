---
title: Universal Editor för Edge Delivery Services for Forms
description: Använd Universell redigerare för Edge Delivery Services for Forms för att skapa Adaptiv Forms.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---


# Universal Editor för Edge Delivery Services for Forms

<span class="preview"> Det här är en förhandsversion som är tillgänglig via vår <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">förhandsversion </a>. </span>

Den universella redigeraren revolutionerar formulärframtagningen för Adobe Edge Delivery Services genom att erbjuda ett enkelt, visuellt och intuitivt What You See Is What You Get-gränssnitt (WYSIWYG). Det är utformat för innehållsskapare och formulärförfattare och eliminerar komplexiteten i traditionella formulärgenereringsprocesser, vilket gör det tillgängligt även för icke-tekniska användare.

Med den universella redigeraren kan du snabbt skapa responsiva, interaktiva formulär med färdiga komponenter som textfält, kryssrutor och alternativknappar. Dess robusta funktionsuppsättning har stöd för dynamiska regler, smidig dataintegrering och avancerad personalisering, vilket säkerställer att alla formulär är skräddarsydda efter era behov.

Den universella redigeraren är en smidig lösning för att skapa och hantera formulär, oavsett om du hanterar enkel rendering på klientsidan, ser till att webbläsaren är kompatibel eller följer strikta tillgänglighetsstandarder.

![Universell redigerare](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Viktiga funktioner i Universal Editor för Edge Delivery Services for Forms



| ![WYSIWYG-gränssnitt](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![Regelredigeraren](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![Skicka åtgärder](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**WYSIWYG-gränssnitt**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**Regelredigeraren**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**Skicka åtgärder**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| Universell redigerare har ett WYSIWYG-gränssnitt för formulärdesign med ett färdigbyggt komponentbibliotek, responsiv design, mallbaserad framtagning och fältändringar i realtid. | Med regelredigeraren kan användare skapa dynamiska formulärinteraktioner med händelsestyrda regler, omedelbar validering och felhantering via lättviktiga JavaScript och JSON. | Skicka funktionsmakron har stöd för serverdelsintegrering, logik för villkorlig inskickning, säkra slutpunkter och preprocessorer, vilket effektiviserar inskickningsarbetsflödena. |

| ![Publicerar/avpublicerar](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![Anpassade komponenter](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Publicerar/avpublicerar**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**Responsivt läge**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**Anpassade komponenter**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| Styr enkelt formulärens synlighet - publicera eller avpublicera dem direkt från redigeraren med bara några klick. | Skapa formulär som smidigt kan anpassas till olika enheter (datorer, surfplattor och mobila enheter). Använd responsivt läge för att förhandsgranska och testa formulär för olika skärmstorlekar. | Med anpassade komponenter kan utvecklare utöka formulärfunktionerna genom att skapa unika element som är anpassade till specifika användningsfall inom organisationen. |

| ![Formatering](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![Tjänster för förifyllnad](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![A/B-testning](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Formatering**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **Förfyll tjänster** (kommer snart) | [**A/B-testning**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| Med formatering med CSS kan utvecklare anpassa utseendet på formulärelement och skapa en visuellt tilltalande design som passar ihop med webbplatsens estetik. | I förifyllda tjänster fylls formulärfält automatiskt i med relevanta användardata från olika källor, vilket minskar behovet av manuell inmatning och förbättrar användarupplevelsen. | A/B-tester gör det möjligt för organisationer att experimentera med olika formulärdesigner, layouter och funktioner för att identifiera de mest framgångsrika varianterna. |

| ![Analys och spårning](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![Formulärfragment](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![Databindning](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Analys och spårning**](https://www.aem.live/developer/martech-integration) | **Formulärfragment** (kommer snart) | [**Databindning**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| Få insikter om användarbeteende, formulärinteraktioner och överföringshastighet med inbyggda analyser och spårning för att möjliggöra datadriven optimering av formulär. | Med Form Fragments kan man återanvända de vanligaste sektionerna en gång och återanvända dem i flera olika formulär, vilket ger enhetlighet och minskar behovet av underhåll. | Databindning möjliggör direkta anslutningar mellan formulärfält och backend-datakällor, med stöd för realtidsuppdateringar och avancerad datamappning. |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![Bädda in Forms](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![Tack!](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**CAPTCHA**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **Bädda in Forms** (kommer snart) | [**Tack!**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| Använd reCAPTCHA för att skydda formulär från automatiserade portar och säkerställa säker och tillförlitlig datainsamling. | Bädda in formulär direkt på Edge Delivery Services Sites-sidor med den inbyggda inbäddningskomponenten i Universal Editor. | Anpassa enkelt bekräftelsemeddelandet eller sidan som visas för användarna när formuläret har skickats. |


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## Fördefinierade formulärkomponenter

Universell redigerare innehåller följande formulärkomponenter:

<table>
  <thead>
    <tr>
      <th></th> 
      <th>Formulärkomponenter</th>
      <th>Beskrivning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="Formulärkomponenter" style="width: 100%;"></td> 
      <td><b>Dragspel</b></td>
      <td>Komprimerbar panelstruktur för att ordna innehåll.</td>
    </tr>
    <tr>
      <td><b>Knapp</b></td>
      <td>Lägger till interaktiva element för åtgärder som navigering eller anpassad logik.</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Förhindrar skräppost genom att kräva att användare utför en mänsklig verifieringsuppgift med Google reCaptcha eller HCaptcha.</td>
    </tr>
    <tr>
      <td><b>Kryssruta</b></td>
      <td>Låter användarna konfigurera en kryssruta.</td>
    </tr>
    <tr>
      <td><b>Kryssrutegrupp</b></td>
      <td>Tillåter användare att välja flera alternativ från en grupp.</td>
    </tr>
    <tr>
      <td><b>Datumväljaren</b></td>
      <td>Låter användarna välja ett datum med hjälp av ett kalendergränssnitt.</td>
    </tr>
    <tr>
      <td><b>Nedrullningsbara listor</b></td>
      <td>Innehåller alternativ för en eller flera markeringar från en fördefinierad lista.</td>
    </tr>
    <tr>
      <td><b>E-post</b></td>
      <td>Hämtar e-postadresser med grundläggande formatvalidering.</td>
    </tr>
    <tr>
      <td><b>Bifogad fil</b></td>
      <td>Aktiverar överföring av dokument, bilder eller andra filtyper.</td>
    </tr>
    <tr>
      <td><b>Formulärfragment</b></td>
      <td>Återanvändbara formulärkomponenter för avsnitt som adressfält eller kontaktinformation.</td>
    </tr>
    <tr>
      <td><b>Bild</b></td>
      <td>Stöder överföring och visning av bilder i formulär.</td>
    </tr>
    <tr>
      <td><b>Modal</b></td>
      <td>Visar en popup-dialogruta som ofta används för varningar, ytterligare information eller bekräftelser.</td>
    </tr>
    <tr>
      <td><b>Numeriskt fält</b></td>
      <td>Hämtar numerisk inmatning, vilket tillåter validering av tal eller intervall.</td>
    </tr>
    <tr>
      <td><b>Panel</b></td>
      <td>Ordnar formuläravsnitt med expanderbara/komprimerbara paneler.</td>
    </tr>
    <tr>
      <td><b>Alternativknappar</b></td>
      <td>Aktiverar envalsmarkering från en grupp med alternativ.</td>
    </tr>
    <tr>
      <td><b>Klassificering</b></td>
      <td>Användare kan ange en stjärnbaserad klassificering.</td>
    </tr>
    <tr>
      <td><b>Återställ knapp</b></td>
      <td>Återställer formulärfälten till deras standardläge.</td>
    </tr>
    <tr>
      <td><b>Skicka-knapp</b></td>
      <td>Utlöser inskickning av formulär och initierar definierade arbetsflöden.</td>
    </tr>
    <tr>
      <td><b>Telefonnummerfält</b></td>
      <td>Hämtar telefonnummer med formatering baserat på land.</td>
    </tr>
    <tr>
      <td><b>Text</b></td>
      <td>Innehåller ett dedikerat avsnitt där du kan visa juridiska villkor och samla in användaravtal via kryssrutor.</td>
    </tr>
    <tr>
      <td><b>Textfält</b></td>
      <td>DCaptures single-line input, such as names or email address.</td>
    </tr>
    <tr>
      <td><b>guide</b></td>
      <td>Hjälper användarna steg för steg genom en formulärprocess i flera delar.</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## Onboarding

<span class="preview"> Det här är en förhandsversion som är tillgänglig via vår <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">förhandsversion </a>. </span>

## Vanliga frågor och svar

**Q. Vem kan använda den universella redigeraren?**
Universell redigerare är utformad för en bred publik, inklusive:

* Innehållsutvecklare som vill skapa visuellt tilltalande formulär.
* Utvecklare som behöver avancerade anpassnings- och integreringsfunktioner.
* Organisationer som vill ha skalbara, säkra och kompatibla lösningar för blanketter.

**F: Kan jag integrera formulär som skapats med den universella redigeraren i mina befintliga system?**
Absolut. Den universella redigeraren stöder smidig databindning med backend-system, vilket möjliggör uppdateringar i realtid och avancerad datamappning. Den kan även integreras med verktyg som Adobe Workfront för uppgiftshantering och har stöd för säkra slutpunkter för arbetsflöden för inlämning av data.

**F: Går det att anpassa formulärkomponenterna?**
Ja, i Universell redigerare kan utvecklare skapa anpassade komponenter som är anpassade efter specifika organisatoriska behov. Dessutom kan du utöka redigerarens funktionalitet med hjälp av UI-tillägg och anpassade arbetsflöden.

**F: Hur hanterar den universella redigeraren tillgängligheten?**
Den universella redigeraren följer standarderna för tillgänglighet, inklusive WCAG (Web Content Accessibility Guidelines). Detta garanterar att formulären kan användas av personer med funktionshinder, vilket ger en heltäckande upplevelse.

**F: Vilken typ av analys kan jag få från formulären?**
Den universella redigeraren innehåller inbyggda analys- och spårningsverktyg för att övervaka användarinteraktioner, formuläröverföringshastighet och konverteringsstatistik. Dessa insikter hjälper er att optimera era formulär för bättre prestanda.


## Börja skapa formulär

{{universal-editor-see-also}}

