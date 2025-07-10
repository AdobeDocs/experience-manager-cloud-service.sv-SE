---
title: Edge Delivery Services for AEM Forms - översikt
description: Edge Delivery Services för AEM Forms har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 0%

---


# Komma igång med Forms på AEM Edge Delivery Services

<span class="preview"> Den här funktionen är en förhandsversion och kan nås via vår [förhandsutgåva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=sv-SE#new-features). </span>

Den här guiden hjälper dig att förstå och implementera formulär med Adobe Experience Manager (AEM) Edge Delivery Services (EDS). Oavsett om du skapar ett enkelt kontaktformulär eller ett komplext datainsamlingsverktyg går du igenom alternativen på den här sidan.

## Förstå Forms i Edge Delivery Services

Edge Delivery Services är en modern Adobe-lösning för att leverera webbinnehåll, inklusive blanketter, med enastående prestanda och flexibilitet. Med Edge Delivery Services kan man

* **Leverera snabbare upplevelser:** Forms laddas otroligt snabbt eftersom de serveras från ett globalt nätverk av edge-servrar (CDN) nära dina användare. Detta ger nöjdare användare och kan öka andelen ifyllda formulär.
* **Uppdatera Forms enklare:** Med Edge Delivery Services kan du ofta få snabbare utvecklingscykler och innehållsuppdateringar, så att du snabbt kan anpassa formulären.
* **Skapa modern, responsiv Forms:** Skapa formulär som ser bra ut och fungerar smidigt på alla enheter.
* **Dra nytta av skalbarhet och tillförlitlighet:** Formulären är lika robusta och skalbara som den underliggande Edge-infrastrukturen.

Den här guiden kommer att:

* Förklara olika sätt att skapa (författare) formulär för dina Edge Delivery Sites.
* Visa hur du konfigurerar vad som ska hända när en användare skickar ett formulär (överföringsåtgärder).
* Hjälp dig att välja de bästa metoderna för dina specifika behov och dina teamkunskaper.
* Tillhandahåll arkitekturdiagram och metodtips.

## Viktiga termer som du bör känna till

* **Edge Delivery Services (EDS):** Adobe Performance-first-arkitektur för att leverera AEM-innehåll via CDN:er. Kallas även Project Franklin.
* **AEM Forms:** Adobe lösning för att skapa, hantera och bearbeta formulär.
* **Universell redigerare (UE):** En visuell WYSIWYG-redigerare för AEM-innehåll, inklusive formulär.
* **Dokumentbaserad redigering:** Skapa formulär med Microsoft Word eller Google Docs/Sheets.
* **Dokumentredigering (DA):** En Adobe-värdtjänst för redigering av innehåll (inklusive sidor som kan hantera formulär) för Edge Delivery Services.
* **Forms Submission Service (FSS):** En Adobe-tjänst som gör det enklare att skicka formulärdata till kalkylblad eller e-post.
* **AEM Publish Instance:** Den aktiva AEM-miljön som kan bearbeta komplexa formuläröverföringar.
* **CORS (Cross-Origin Resource Sharing):** En webbläsarsäkerhetsfunktion som behöver konfigureras när formulär från olika domäner bäddas in.
* **CDN (Content Delivery Network):** Ett nätverk med servrar som levererar webbinnehåll snabbt till användare baserat på deras geografiska plats.


**Konceptuell diagram över interaktion med Edge Delivery Services-formulär**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Formulärinteraktion](/help/forms/assets/eds-form-interaction.png)
Bilden visar hur en användare interagerar med ett formulär som levereras snabbt via ett CDN. De data de skickar hanteras sedan av ett backend-system.

## Hur arbetar Forms på Edge?

Med EDS kan webbplatsinnehållet (inklusive formulärstrukturen) komma från olika källor som AEM as a Cloud Service, SharePoint, Google Drive eller tjänsten Document Authoring (DA). Innehållet publiceras sedan till ett globalt CDN. När en användare besöker din webbplats kan innehållet hanteras direkt från närmaste CDN-edge-server, vilket ger maximal hastighet.

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**Förenklad Edge Delivery Services-arkitektur med Forms**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Arkitektur](/help/forms/assets/eds-simplified-architecture.png)
Bilden visar vägen: formulären definieras i ett redigeringssystem, publiceras i kanten, skickas till användarna och inskickade data bearbetas av en serverdel.

## Välja formulärredigeringsmetod

Du kan skapa formulär för dina Edge Delivery Services-webbplatser på tre olika sätt. Ditt val beror på teamets kompetens, formulärets komplexitet och dina projektbehov.

### Vilken redigeringsmetod passar dig?

Använd det här beslutsträdet när du vill välja:

**Beslutsträd för formulärredigering**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![Välja rätt plattform](/help/forms/assets/eds-authoring-selection.png)

Detta beslutsträd hjälper dig att välja en redigeringsmetod som baseras på ditt team och dina formulärbehov.

### Skapa Forms med dokument (Word/Google Docs)

Den här metoden passar bra för att snabbt [skapa formulär om ditt team är bekväm med Microsoft Word eller Google Docs/Sheets](/help/edge/docs/forms/create-forms.md).

**Så här fungerar det: Från dokument till webbformulär**

Du definierar formulärfält, etiketter och typer direkt i ett Word-dokument eller i ett Google-blad med hjälp av ett särskilt tabellformat eller ett&quot;formulärblock&quot;. När du publicerar det här dokumentet konverterar Edge Delivery Services automatiskt det till ett webbklart HTML-formulär som användare kan interagera med på din webbplats.

**Funktioner och funktioner**

* Skriv i välkända verktyg: Word, Google Docs, Google Sheets.
* Definiera fält: textinmatningar, e-post, listrutor, kryssrutor, alternativknappar, textområden.
* Lägg till etiketter, platshållare och hjälpmeddelanden.
* Ange grundläggande valideringsregler: obligatoriska fält, e-postformat.
* Integrera reCAPTCHA för skräppostskydd.
* Tillåt filöverföringar.
* Publicera direkt: Ändringar i dokumentet återspeglas snabbt på den publicerade webbplatsen.
* Utöka med anpassad kod: Avancerade användare kan lägga till anpassade formulärkomponenter och format via GitHub.

**Överväganden**

* Ditt team använder regelbundet Word eller Google Docs/Sheets för innehåll.
* Du måste snabbt skapa enkla till måttligt komplexa formulär.
* Du vill skicka formulärdata direkt till ett kalkylblad eller en e-postadress med minimal konfiguration.

**Hur inskickningar fungerar (främst Forms Submission Service)**

Forms skapade på det här sättet [skickar vanligtvis data till AEM Forms överföringstjänst](/help/forms/forms-submission-service.md). Du konfigurerar detta (ofta i själva källdokumentet) för att skicka data till ett Google-blad, en Excel-fil på OneDrive/SharePoint eller som ett e-postmeddelande.

**Dokumentbaserat redigeringskoncept**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![Dokumentbaserad](/help/forms/assets/eds-doc-based.png)
I det här diagrammet visas hur ett formulär som har definierats i ett dokument blir ett live-webbformulär.

### Forms Visually with Universal Editor

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) har ett modernt dra och släpp-gränssnitt för att skapa formulär direkt i webbläsaren.

**Så här fungerar det: dra och släpp-formulärbyggnad**

Du använder ett visuellt gränssnitt för att dra formulärkomponenter (som inmatningsfält, knappar och listrutor) till sidan. Sedan kan du konfigurera varje komponents egenskaper (etiketter, validering osv.) via en egenskapspanel. Den universella redigeraren visar en förhandsgranskning av formuläret i realtid.

**Funktioner och funktioner**

* Skapa visuella formulär med ett bibliotek med färdiga komponenter.
* Konfigurera realtidsvalidering och affärslogik (t.ex. visa/dölj fält baserat på val).
* Se förhandsvisningar live för olika enheter (dator, mobil).
* Integrera med AEM-funktioner som Content Fragments, AEM Workflows och user permissions.
* Använd&quot;Experience Builder&quot; för att få hjälp med att skapa eller redigera formulär med hjälp av uppmaningar.

**Överväganden**

* Ni måste skapa komplexa formulär med villkorsstyrd logik, flerstegspaneler eller personalisering.
* Ditt team (t.ex. marknadsförare, företagsanvändare) föredrar visuella verktyg.
* Ni behöver vara väl integrerade med AEM as a Cloud Service för styrning, arbetsflöden eller använda AEM-material i era formulär.

**Hur inskickningar fungerar (Forms Submission Service eller AEM Publish)**

Forms som byggts med Universal Editor kan

* Använd den enkla [Forms Submission Service](/help/forms/forms-submission-service.md) (för att skicka data till kalkylblad eller e-post).
* Skicka data till AEM Publish-instansen för mer avancerad bearbetning (som att starta ett AEM-arbetsflöde, använda formulärdatamodellen eller integrera med andra företagssystem).

**Universal Editor Concept**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![Universell redigerare](/help/forms/assets/eds-ue-based.png)

I det här diagrammet visas huvuddelarna i den universella redigeraren som används för att skapa formulär.

### Använda Forms med Document Authoring (DA)

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial) är en Adobe-värdtjänst som du kan använda för att skapa och hantera innehåll på din huvudwebbplats (sidor, artiklar) som levereras via Edge Delivery Services. Det är ett alternativ till att använda SharePoint eller Google Drive för källinnehåll från Edge Delivery Services.

**Om dokumentredigering (DA) för Edge Delivery Services-innehåll**

Document Authoring är en redigeringsmiljö för större företag som använder Adobe designsystem (Spectrum) och AEM dokumentmodell (Block, Sections). Den är utformad för strukturerad innehållshantering för EDS.

**Hur handhar handtag för Forms (inbäddning, inte direktredigering)**

DA är **inte ett verktyg för att skapa formulär från grunden**. I stället använder du DA för att skapa dina webbsidor, och sedan *bäddar du in* formulär (som har skapats med dokumentbaserad redigering eller den universella redigeraren) på dessa DA-skapade sidor.

**Steg för att bädda in Forms på dina DA-sidor**

1. **Skapa ditt formulär:** Bygg ditt formulär med:
   * Dokumentbaserad redigering (Word/Google Docs)
   * Universal Editor

1. **Publicera ditt formulär:** Kontrollera att det här formuläret är publicerat och tillgängligt via en egen Edge Delivery-URL (t.ex. `https://your-eds-project.hlx.page/forms/contact-us`).
1. **Skapa din sida i DA:** Skapa eller redigera sidan i Dokumentredigering där du vill att formuläret ska visas.
1. **Bädda in formuläret:** Använd ett specifikt &quot;block&quot; eller en komponent på din DA-sida för att referera till och bädda in formuläret från dess URL. DA-sidan hämtar och visar sedan det externt skapade formuläret.

**Dokumentredigering med inbäddat formulär**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![Dokumentredigering](/help/forms/assets/eds-da-based.png)

I det här diagrammet visas att du först skapar ett formulär med UE eller Docs och sedan bäddar in det på en sida som du bygger upp i Dokumentredigering.


### Jämföra redigeringsalternativ

| Kriterier | Dokumentbaserad redigering | Universal Editor (WYSIWYG) | Forms in Document Authoring (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Primärt redigeringsverktyg** | Word/Google Docs/Sheets | Webbläsare (AEM Universal Editor) | Ej tillämpligt (Forms är *inbäddat*) |
| **Teamkunskapsnivå** | Välbekant med dokumentredigerare | Bekvämt med visuella webbverktyg | Använder DA för sidinnehåll |
| **Vanlig formulärkomplexitet** | Enkel till måttlig | Medelhög till komplex, företagsnivå | Beroende på det inbäddade formuläret |
| **Överföringsalternativ 1 (enkelt)** | Forms Submission Service (to Sheet/Email) | Forms Submission Service (to Sheet/Email) | Följer inbäddade formulärinställningar |
| **Överföringsalternativ 2 (avancerat)** | Ej tillämpligt | AEM Publish (arbetsflöde, FDM osv.) | Följer inbäddade formulärinställningar |
| **AEM Backend Integration** | Minimal | Hög (med AEM Publish) | Indirekt, via inbäddad Universal Editor-blankett |
| **Bäst för..** | Snabb framtagning av enkla blanketter av content team, snabb datainhämtning. | Marknadsförare, affärsanvändare som behöver visuell kontroll, komplexa blanketter eller djupgående integrering med AEM. | Webbplatser där primärt innehåll hanteras i DA och kräver formulär från andra källor. |

**Utökat beslutsträd**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![Beslutsträd](/help/forms/assets/eds-enhanced-decision.png)

## Funktionsjämförelse av redigeringsmetoder

I följande tabell finns en detaljerad jämförelse av de viktigaste funktionerna i olika AEM-metoder för att skapa formulär, som hjälper dig att välja den metod som passar bäst för dina behov. &#x200B;

| **Funktion** | **Universell redigerare (WYSIWYG)** | **Dokumentbaserad redigering** | **Dokumentredigering (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Enhetlig komposition med platser** | ✅ |                              | ✅ (med inbäddade formulär) |
| **Stöd för inbäddning av formulär** | ✅ | ✅ | ✅ (bädda in från Universal Editor eller Docs) |
| **Regler (dynamiskt beteende)** | Avancerad regelredigerare med anpassade funktioner | Begränsad: Visa/dölj, beräkna värde, anpassade funktioner | Beroende på inbäddat formulär |
| **Stöd för bifogade filer** | ✅ | ℹ️ (tidig åtkomst) | Beroende på inbäddat formulär |
| **CAPTCHA-stöd** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Beroende på inbäddat formulär |
| **Överföringsfunktioner** | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Endast kalkylblad | Följer inbäddade formulärinställningar |
| **Dataschema** | FDM, anpassad | Egen | Baserat på inbäddat formulär |
| **Förifyll** | 💡 (via guiden) | ✅ | Beroende på inbäddat formulär |
| **Fragment** | ✅ | ✅ | Beroende på inbäddat formulär |
| **Visuell regelredigerare** | ✅ |                              |                              |
| **Lokalisering** | 💡 (via platser) | ℹ️ (handbok för Excel/ark) | Beroende på inbäddat formulär |
| **Dataschema (dataträd)** | 💡 (via UI-tillägg) |                              |                              |
| **Mallstöd** | Endast ursprungligt innehåll |                              |                              |
| **Portal** |                               |                              |                              |
| **Tema** | ℹ️ (på projektnivå) | ℹ️ (på projektnivå) | ℹ️ (baserat på värdwebbplats) |
| **Egen komponent** | ✅ | ✅ | ✅ (om den inbäddade komponenten stöder det) |
| **OTB och anpassade funktioner** | ✅ | ✅ | ✅ (i inbäddat formulär) |
| **Fragmentreferens** |                               |                              |                              |
| **Signeringsintegrering** |                               |                              |                              |
| **Experimentation** | ✅ | ✅ | Beroende på inbäddningskontext |
| **Aktivitetshantering via Workfront** | ✅ |                              |                              |
| **Personalization-tillägg** | 💡 |                              |                              |
| **Anpassning av redigerare** | ✅ (via UI-tillägg) |                              |                              |
| **Skicka åtgärd** | ✅ | Endast kalkylblad | Baserat på inbäddat formulär |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

Så här kan du gå vidare:

[Välj din inskickningsstrategi](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) för att avgöra om ditt projekt kräver Forms inskickningstjänst (idealisk för kalkylblad/e-postutdata) eller den flexibilitet och backend-integrering som AEM Publicera inskickningsåtgärder erbjuder.

Läs artikeln [Best Practices for Creating Forms](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md) om du vill veta mer om hur du utformar effektiva, tillgängliga och användarvänliga formulär.

## Nästa steg

Den här guiden innehåller en översikt över hur du använder formulär med AEM Edge Delivery Services. Mer detaljerade, stegvisa instruktioner om specifika konfigurationer finns i Adobe Experience Manager officiella dokumentation:

* [Dokumentbaserad redigering med Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Universell redigerare med Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Dokumentredigering (DA) och inbäddat innehåll](https://www.aem.live/developer/da-tutorial)
* [AEM Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
